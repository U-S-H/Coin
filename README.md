<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Apex Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --neon-red: #ff003c; --neon-pink: #ff00ff; --black: #050505; --glass: rgba(15, 15, 15, 0.96); }
        body { background: var(--black); color: white; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        
        /* LOGIN BACKGROUND IMAGE SYSTEM */
        #auth-section { 
            background: linear-gradient(rgba(0,0,0,0.85), rgba(0,0,0,0.85)), url('https://images.unsplash.com/photo-1639762681485-074b7f938ba0?q=80&w=2064&auto=format&fit=crop'); 
            background-size: cover; 
            background-position: center;
            background-attachment: fixed;
        }

        #splash { transition: opacity 0.8s ease, visibility 0.8s; }
        .splash-logo { background: linear-gradient(to tr, var(--neon-red), var(--neon-pink)); box-shadow: 0 0 50px rgba(255, 0, 60, 0.5); animation: pulse 2s infinite; }
        @keyframes pulse { 0%, 100% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.1); opacity: 0.8; } }

        .glass-panel { background: var(--glass); backdrop-filter: blur(40px); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 30px; transition: 0.3s; }
        .btn-master { background: linear-gradient(90deg, var(--neon-red), var(--neon-pink)); color: white; font-weight: 800; padding: 18px; border-radius: 20px; width: 100%; border: none; cursor: pointer; box-shadow: 0 8px 25px rgba(255, 0, 60, 0.3); }
        .input-dark { background: rgba(255,255,255,0.06); border: 1px solid rgba(255,255,255,0.1); border-radius: 18px; padding: 16px; color: white; width: 100%; outline: none; font-size: 14px; backdrop-filter: blur(10px); }
        .nav-item { color: #444; text-align: center; cursor: pointer; font-size: 10px; font-weight: 800; transition: 0.3s; }
        .nav-item.active { color: var(--neon-red); text-shadow: 0 0 10px var(--neon-red); }
        .hidden { display: none !important; }
        .proof-preview { max-width: 100px; border-radius: 10px; border: 1px solid var(--neon-red); display: none; margin-top: 10px; }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-24 h-24 splash-logo rounded-[2.5rem] flex items-center justify-center text-5xl font-black text-white">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-8 text-xs tracking-[0.4em]">NEXUS<span class="text-[#ff003c]">INFINITY</span></h1>
        <p class="text-[8px] text-zinc-500 mt-4 font-bold uppercase tracking-widest animate-pulse">Initializing Secure Protocol...</p>
    </div>

    <div id="auth-section" class="min-h-screen p-8 flex flex-col justify-center hidden">
        <div class="max-w-sm mx-auto w-full space-y-10">
            <div id="logo-tap" class="text-center">
                <div class="w-24 h-24 bg-gradient-to-tr from-zinc-900 to-black mx-auto rounded-[2rem] flex items-center justify-center text-5xl font-black border border-white/10 shadow-2xl">N</div>
                <h2 style="font-family: 'Syncopate'" class="mt-8 text-xl tracking-tighter">NEXUS<span class="text-[#ff003c]">INFINITY</span></h2>
                <p class="text-[9px] text-zinc-400 mt-2 font-bold uppercase tracking-[0.2em]">Institutional Access Terminal</p>
            </div>
            
            <div id="login-ui" class="space-y-4 p-8 glass-panel border border-white/10">
                <input type="text" id="l-user" placeholder="Terminal Account ID" class="input-dark">
                <input type="password" id="l-pass" placeholder="Institutional Key" class="input-dark">
                <button onclick="handleLogin()" class="btn-master">Authorize Connection</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] text-zinc-300 font-black uppercase cursor-pointer hover:text-white transition">Register New Node ID</p>
            </div>

            <div id="signup-ui" class="space-y-4 p-8 glass-panel border border-white/10 hidden">
                <input type="text" id="s-user" placeholder="Create Identity ID" class="input-dark">
                <input type="password" id="s-pass" placeholder="Create Security Key" class="input-dark">
                <button onclick="handleSignup()" class="btn-master">Initialize Identity</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-300 font-black uppercase cursor-pointer hover:text-white transition">Return to Terminal</p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-32">
        <nav class="p-6 sticky top-0 bg-black/80 backdrop-blur-3xl z-[500] border-b border-white/5 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-zinc-900 rounded-xl flex items-center justify-center font-black border border-white/10">N</div>
                <span id="nav-user" class="text-sm font-black italic text-[#ff003c] uppercase tracking-tighter">...</span>
            </div>
            <button onclick="logout()"><i class="fa-solid fa-power-off text-zinc-600"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-panel p-8 bg-gradient-to-br from-zinc-900 to-black relative overflow-hidden border border-white/5">
                <p class="text-[10px] font-black text-zinc-500 uppercase tracking-widest mb-2">Total Net Equity</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 flex justify-between border-t border-white/5 pt-6">
                    <div><p class="text-[7px] text-zinc-500 uppercase">Profit Yield</p><p id="profit-txt" class="text-lg font-black text-[#ff00ff]">+$0.00</p></div>
                    <div class="text-right"><p class="text-[7px] text-zinc-500 uppercase">Network</p><p class="text-[9px] font-black text-green-500 animate-pulse">STABLE</p></div>
                </div>
            </div>
            <div id="nodes-market" class="grid gap-4"></div>
        </div>

        <div id="page-finance" class="p-6 space-y-8 hidden">
            <div class="glass-panel p-7 space-y-6">
                <h3 class="text-lg font-black italic text-[#ff003c]">CAPITAL INJECTION</h3>
                <div class="bg-black/60 p-4 rounded-2xl border border-white/5">
                    <p class="text-[7px] text-zinc-500 font-black mb-1">TRC20 / BINANCE PAY ADDRESS</p>
                    <p class="text-[11px] font-black text-[#ff00ff] break-all">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Injection Amount ($)" class="input-dark">
                <input type="text" id="dep-tid" placeholder="Transaction TID / Hash" class="input-dark">
                <div>
                    <input type="file" id="dep-proof" accept="image/*" class="text-[10px] text-zinc-500 block w-full file:mr-4 file:py-2 file:px-4 file:rounded-full file:bg-zinc-800 file:text-white file:border-0">
                    <img id="preview-img" class="proof-preview">
                </div>
                <button onclick="submitDep()" class="btn-master">Authorize Deposit</button>
            </div>

            <div class="glass-panel p-7 space-y-6">
                <h3 class="text-lg font-black italic">CAPITAL PAYOUT</h3>
                <select id="w-method" class="input-dark bg-black">
                    <option value="Binance Pay">Binance Pay</option>
                    <option value="Trust Wallet">Trust Wallet (TRC20)</option>
                    <option value="OKX">OKX Exchange</option>
                    <option value="Kraken">Kraken Node</option>
                    <option value="Bybit">Bybit Network</option>
                    <option value="KuCoin">KuCoin Node</option>
                    <option value="Coinbase">Coinbase Wallet</option>
                </select>
                <input type="number" id="w-amt" placeholder="Payout Amount ($)" class="input-dark">
                <input type="text" id="w-addr" placeholder="Destination Address / ID" class="input-dark">
                <button onclick="submitWith()" class="btn-master !bg-zinc-900">Request Withdrawal</button>
            </div>
        </div>

        <div id="page-history" class="p-6 space-y-6 hidden">
            <h3 class="text-xl font-black italic uppercase">Terminal Logs</h3>
            <div id="history-list" class="space-y-4"></div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-black/80 backdrop-blur-3xl border-t border-white/5 p-6 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-shield-halved text-xl mb-1"></i><p>CORE</p></div>
            <div onclick="switchPage('finance')" class="nav-item"><i class="fa-solid fa-vault text-xl mb-1"></i><p>VAULT</p></div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-list-ul text-xl mb-1"></i><p>LOGS</p></div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#050505] z-[9999] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10"><h2 class="text-xl font-black italic text-[#ff003c]">ADMIN OVERRIDE</h2><button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl">&times;</button></div>
        <div id="admin-dep-list" class="space-y-6"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
          apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0",
          authDomain: "live-54fb4.firebaseapp.com",
          databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com",
          projectId: "live-54fb4",
          storageBucket: "live-54fb4.firebasestorage.app",
          messagingSenderId: "781910562842",
          appId: "1:781910562842:web:07a887f860d30fd17d99a3"
        };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        const nodesArr = [
            ...Array.from({length: 10}, (_, i) => ({ id: i+1, type: 'Standard', title: `Standard Node ${i+1}`, price: (i+1)*20, daily: ((i+1)*2.1).toFixed(2), days: 30 })),
            ...Array.from({length: 5}, (_, i) => ({ id: i+11, type: 'Apex', title: `Apex Elite-0${i+1}`, price: (i+1)*500, daily: ((i+1)*60).toFixed(2), days: 45 }))
        ];

        window.onload = () => {
            renderNodes();
            setTimeout(() => {
                document.getElementById('splash').style.opacity = '0';
                setTimeout(() => {
                    document.getElementById('splash').classList.add('hidden');
                    const user = localStorage.getItem('nexus_user');
                    if(user) showDashboard(user);
                    else document.getElementById('auth-section').classList.remove('hidden');
                }, 800);
            }, 3000);
        };

        function renderNodes() {
            document.getElementById('nodes-market').innerHTML = nodesArr.map(n => `
                <div class="glass-panel p-6 flex justify-between items-center ${n.type === 'Apex' ? 'border-[#ff003c]' : ''}">
                    <div><p class="text-[7px] font-black ${n.type === 'Apex' ? 'text-[#ff003c]' : 'text-zinc-500'} uppercase mb-1">${n.type}</p><h4 class="text-xl font-black italic">${n.title}</h4><p class="text-[9px] font-black text-green-500">+$${n.daily}/Day ROI</p></div>
                    <div class="text-right"><p class="text-lg font-black">$${n.price}</p><button onclick="buyNode(${n.id})" class="bg-white text-black px-5 py-2 rounded-xl text-[9px] font-black mt-1 uppercase">Deploy</button></div>
                </div>`).join('');
        }

        document.getElementById('dep-proof').onchange = (e) => {
            const reader = new FileReader();
            reader.readAsDataURL(e.target.files[0]);
            reader.onload = () => { 
                document.getElementById('preview-img').src = reader.result;
                document.getElementById('preview-img').style.display = 'block';
            };
        };

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof) return alert("Fill all protocol fields & Upload Proof!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, proof, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry);
            await set(ref(db, `admin/deposits/${hRef.key}`), entry);
            alert("Deposit Protocol Logged!");
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('balance-txt').innerText = '$' + (d.balance || 0).toLocaleString();
                document.getElementById('profit-txt').innerText = '+$' + (d.profit || 0).toLocaleString();
                if(d.history) {
                    const logs = Object.entries(d.history).reverse();
                    document.getElementById('history-list').innerHTML = logs.map(([k, l]) => `
                        <div class="glass-panel p-5 flex justify-between items-center border-l-4 ${l.status === 'pending' ? 'border-yellow-500' : 'border-green-500'}">
                            <div><p class="text-[10px] font-black uppercase">${l.type}</p><p class="text-[7px] text-zinc-500">${l.date}</p></div>
                            <div class="text-right"><p class="text-sm font-black">$${l.amount}</p><span class="text-[8px] font-black uppercase ${l.status==='pending'?'text-yellow-500':'text-green-500'}">${l.status}</span></div>
                        </div>`).join('');
                }
            });
        }

        let taps = 0; document.getElementById('admin-trigger').onclick = document.getElementById('logo-tap').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Auth Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; }
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/deposits'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-dep-list').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass-panel p-6 space-y-4">
                        <p class="text-xs">User: <span class="text-[#ff003c]">${l.user}</span> | Amt: <span class="text-green-500">$${l.amount}</span></p>
                        <p class="text-[9px] text-zinc-500">TID: ${l.tid}</p>
                        <img src="${l.proof}" class="w-full rounded-xl border border-white/10" onclick="window.open(this.src)">
                        <button onclick="approveDep('${id}','${l.user}',${l.amount},'${l.hKey}')" class="w-full bg-green-600 py-3 rounded-2xl text-[10px] font-black uppercase">Approve Injection</button>
                    </div>`).join('') : '<p class="text-center text-xs opacity-30">Waiting for protocols...</p>';
            });
        }

        window.approveDep = async (aKey, u, a, hKey) => {
            const snap = await get(ref(db, `users/${u}`));
            await update(ref(db, `users/${u}`), { balance: (snap.val().balance || 0) + parseFloat(a) });
            await update(ref(db, `users/${u}/history/${hKey}`), { status: 'Approved' });
            await remove(ref(db, `admin/deposits/${aKey}`));
            alert("Capital Authorized!");
        };

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Fill data!");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("ID Initialized!"); toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); }
            else alert("Denial of Access!");
        };

        window.switchPage = (p) => {
            ['home', 'finance', 'history'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            if(event) event.currentTarget.classList.add('active');
        };
        window.toggleAuth = (s) => {
            document.getElementById('login-ui').classList.toggle('hidden', s);
            document.getElementById('signup-ui').classList.toggle('hidden', !s);
        };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
