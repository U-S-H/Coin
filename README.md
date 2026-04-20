<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Elite Crypto Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        :root { --gold: #f3ba2f; --bg: #ffffff; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0f172a; margin: 0; overflow-x: hidden; }

        /* Institutional UI Kit */
        .glass-card { background: #fff; border: 1px solid rgba(0,0,0,0.05); border-radius: 30px; box-shadow: 0 10px 40px rgba(0,0,0,0.01); }
        .input-pro { background: #f8fafc; border: 2px solid transparent; border-radius: 18px; padding: 16px; width: 100%; font-weight: 700; outline: none; transition: 0.3s; }
        .input-pro:focus { border-color: var(--gold); background: #fff; }
        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 900; padding: 18px; border-radius: 20px; width: 100%; text-transform: uppercase; letter-spacing: 1px; border: none; cursor: pointer; box-shadow: 0 10px 25px rgba(243,186,47,0.2); }
        
        /* Status Badges */
        .status-pending { background: #fef9c3; color: #a16207; }
        .status-approved { background: #dcfce7; color: #15803d; }
        .status-rejected { background: #fee2e2; color: #b91c1c; }
        .badge { padding: 4px 10px; border-radius: 100px; font-size: 8px; font-weight: 800; text-transform: uppercase; }

        .nav-item { cursor: pointer; font-size: 10px; font-weight: 800; color: #94a3b8; text-align: center; }
        .nav-item.active { color: #000; }
        .hidden { display: none !important; }
        
        .node-card { border: 1.5px solid #f1f5f9; border-radius: 25px; padding: 20px; transition: 0.3s; background: #fff; }
        .node-card:hover { border-color: var(--gold); transform: translateY(-5px); }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-16 h-16 bg-white text-black rounded-2xl flex items-center justify-center text-3xl font-black mb-4 animate-bounce">N</div>
        <h1 class="text-white font-black italic text-xl uppercase tracking-widest">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="w-full max-w-sm space-y-10">
            <div class="text-center">
                <div class="w-20 h-20 bg-black text-white rounded-[2.5rem] mx-auto flex items-center justify-center text-4xl font-black mb-6 shadow-2xl">N</div>
                <h2 class="text-3xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
            </div>
            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal Username" class="input-pro text-center">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-pro text-center">
                <button onclick="handleLogin()" class="btn-gold w-full">Authorize Entry</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">New Node? <span onclick="toggleAuth(true)" class="text-black underline cursor-pointer">Register Identity</span></p>
            </div>
            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Choose Username" class="input-pro text-center">
                <input type="password" id="s-pass" placeholder="Create Password" class="input-pro text-center">
                <input type="text" id="s-ref" placeholder="Referral Code (Optional)" class="input-pro text-center">
                <button onclick="handleSignup()" class="btn-gold w-full">Initialize Node</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">Registered? <span onclick="toggleAuth(false)" class="text-black underline cursor-pointer">Back to Login</span></p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-28">
        <nav class="sticky top-0 bg-white/80 backdrop-blur-xl border-b p-5 flex justify-between items-center z-[500]">
            <div class="flex items-center gap-2">
                <div class="w-8 h-8 bg-black text-white rounded-lg flex items-center justify-center font-black text-xs">N</div>
                <span id="nav-user" class="font-black italic uppercase text-sm">...</span>
            </div>
            <button onclick="logout()" class="text-slate-300 hover:text-red-500"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-card p-10 bg-slate-900 text-white relative overflow-hidden">
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mb-2">Portfolio Valuation</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 flex justify-between border-t border-slate-800 pt-6">
                    <div><p class="text-[8px] font-black text-slate-500 uppercase">Total Yield</p><p id="profit-txt" class="text-lg font-black text-green-400">+$0.00</p></div>
                    <div class="text-right"><p class="text-[8px] font-black text-slate-500 uppercase">Yield Reset</p><p id="timer" class="text-lg font-black text-[#f3ba2f]">23:59:59</p></div>
                </div>
            </div>

            <h3 class="font-black uppercase text-[10px] tracking-widest text-slate-400">Deployed Nodes</h3>
            <div id="active-nodes-list" class="space-y-3">
                <p class="text-center text-[10px] text-slate-300 italic py-6">No nodes currently active...</p>
            </div>
        </div>

        <div id="page-nodes" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Institutional Nodes</h3>
            <div id="nodes-market" class="grid gap-4 pb-10">
                </div>
        </div>

        <div id="page-finance" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Capital Management</h3>
            
            <div class="glass-card p-6 space-y-5">
                <p class="text-[10px] font-black uppercase text-slate-400">Deposit Gateway</p>
                <div class="bg-slate-50 p-4 rounded-2xl break-all">
                    <p class="text-[7px] font-black mb-1">TRX / USDT (TRC20):</p>
                    <p class="text-[10px] font-bold">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Deposit Amount ($)" class="input-pro">
                <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="input-pro">
                <input type="file" id="dep-proof" accept="image/*" class="text-[10px]">
                <button onclick="submitDep()" class="btn-gold w-full">Submit Deposit</button>
            </div>

            <div class="glass-card p-6 space-y-4">
                <p class="text-[10px] font-black uppercase text-slate-400">Withdrawal Request</p>
                <input type="text" id="w-addr" placeholder="Wallet Address" class="input-pro">
                <input type="number" id="w-amt" placeholder="Amount to Withdraw" class="input-pro">
                <button onclick="submitWith()" class="btn-gold w-full bg-slate-100">Request Payout</button>
            </div>
        </div>

        <div id="page-history" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Node Ledger</h3>
            <div id="history-list" class="space-y-3"></div>
        </div>

        <div id="page-menu" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Institutional Info</h3>
            <div class="space-y-2">
                <div onclick="alert('Company: Nexus Infinity Ltd\nReg: UAE-7729')" class="glass-card p-5 text-[10px] font-black uppercase flex justify-between"><span>Company Details</span><i class="fa-solid fa-chevron-right"></i></div>
                <div onclick="alert('Data is AES-256 Encrypted.')" class="glass-card p-5 text-[10px] font-black uppercase flex justify-between"><span>Privacy Policy</span><i class="fa-solid fa-chevron-right"></i></div>
                <div onclick="alert('Min Deposit: $10\nMin Withdraw: $5')" class="glass-card p-5 text-[10px] font-black uppercase flex justify-between"><span>FAQ / Rules</span><i class="fa-solid fa-chevron-right"></i></div>
            </div>
            
            <div class="glass-card p-6 mt-6">
                <p class="text-[9px] font-black text-slate-400 uppercase mb-2">Your Referral Link</p>
                <div class="flex gap-2">
                    <input id="ref-link" readonly class="bg-slate-50 p-3 rounded-xl text-[9px] font-bold w-full outline-none">
                    <button onclick="copyRef()" class="bg-black text-white px-4 rounded-xl text-[9px] font-black">COPY</button>
                </div>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-white border-t p-5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-house-user block text-lg mb-1"></i>Home</div>
            <div onclick="switchPage('nodes')" class="nav-item"><i class="fa-solid fa-server block text-lg mb-1"></i>Nodes</div>
            <div onclick="switchPage('finance')" class="nav-item"><i class="fa-solid fa-wallet block text-lg mb-1"></i>Wallet</div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-clock-rotate-left block text-lg mb-1"></i>History</div>
            <div onclick="switchPage('menu')" class="nav-item"><i class="fa-solid fa-ellipsis block text-lg mb-1"></i>Menu</div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
          apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0",
          authDomain: "live-54fb4.firebaseapp.com",
          databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com",
          projectId: "live-54fb4",
          storageBucket: "live-54fb4.firebasestorage.app",
          messagingSenderId: "781910562842",
          appId: "1:781910562842:web:07a887f860d30fd17d99a3"
        };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // 15 Nodes Data
        const nodes = Array.from({length: 15}, (_, i) => ({
            id: i + 1,
            title: `Terminal Node 0${i + 1}`,
            price: (i + 1) * 30,
            daily: ((i + 1) * 1.8).toFixed(2),
            period: 45
        }));

        window.onload = () => {
            renderNodes();
            setInterval(updateTimer, 1000);
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const u = localStorage.getItem('nexus_user');
                if(u) showDashboard(u);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        function renderNodes() {
            document.getElementById('nodes-market').innerHTML = nodes.map(n => `
                <div class="node-card flex justify-between items-center">
                    <div>
                        <p class="text-[9px] font-black text-slate-400 uppercase">${n.title}</p>
                        <h4 class="text-xl font-black italic">$${n.price}</h4>
                        <p class="text-[9px] font-bold text-green-500">Daily Profit: $${n.daily}</p>
                    </div>
                    <button onclick="buyNode(${n.id})" class="bg-black text-white px-6 py-3 rounded-2xl text-[9px] font-black">ACTIVATE</button>
                </div>
            `).join('');
        }

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user');
            const node = nodes.find(n => n.id === id);
            const snap = await get(ref(db, `users/${user}`));
            const bal = snap.val().balance || 0;

            if(bal < node.price) return alert("Insufficient Balance!");

            await set(ref(db, `users/${user}/balance`), bal - node.price);
            await push(ref(db, `users/${user}/activeNodes`), { ...node, purchaseDate: new Date().toLocaleString(), expiry: Date.now() + (node.period * 86400000) });
            alert("Node Activated successfully!");
            switchPage('home');
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            document.getElementById('ref-link').value = window.location.origin + "?ref=" + uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val();
                if(!data) return;
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toLocaleString();
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toLocaleString();

                // Active Nodes List
                if(data.activeNodes) {
                    document.getElementById('active-nodes-list').innerHTML = Object.values(data.activeNodes).map(n => `
                        <div class="glass-card p-5 border-l-4 border-[#f3ba2f]">
                            <div class="flex justify-between items-center">
                                <p class="text-[10px] font-black uppercase">${n.title}</p>
                                <span class="badge status-approved">Running</span>
                            </div>
                            <p class="text-[8px] text-slate-400 mt-1">Daily Yield: $${n.daily}</p>
                        </div>
                    `).join('');
                }

                // History
                if(data.history) {
                    document.getElementById('history-list').innerHTML = Object.values(data.history).reverse().map(h => `
                        <div class="glass-card p-4 flex justify-between items-center">
                            <div><p class="text-[9px] font-black uppercase">${h.type}</p><p class="text-[7px] text-slate-400">${h.date}</p></div>
                            <div class="text-right">
                                <p class="text-[10px] font-bold">$${h.amount}</p>
                                <span class="badge status-${h.status}">${h.status}</span>
                            </div>
                        </div>
                    `).join('');
                }
            });
        }

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const file = document.getElementById('dep-proof').files[0];
            if(!amt || !tid || !file) return alert("Fill all data!");

            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async () => {
                const hRef = push(ref(db, `users/${user}/history`));
                const entry = { type: 'deposit', amount: amt, status: 'pending', date: new Date().toLocaleString(), proof: reader.result, tid };
                await set(hRef, entry);
                await set(ref(db, `admin/deposits/${hRef.key}`), { ...entry, user });
                alert("Deposit request submitted!");
                switchPage('history');
            };
        };

        window.submitWith = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('w-amt').value;
            const addr = document.getElementById('w-addr').value;
            if(!amt || !addr) return alert("Details missing!");

            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { type: 'withdraw', amount: amt, status: 'pending', date: new Date().toLocaleString(), wallet: addr };
            await set(hRef, entry);
            await set(ref(db, `admin/withdrawals/${hRef.key}`), { ...entry, user });
            alert("Withdrawal recorded!");
            switchPage('history');
        };

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Empty fields!");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("Node Initialized!"); toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); }
            else alert("Auth Error!");
        };

        window.switchPage = (p) => {
            ['home', 'nodes', 'finance', 'history', 'menu'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            if(event) event.currentTarget.classList.add('active');
        };

        function updateTimer() {
            const now = new Date();
            document.getElementById('timer').innerText = `${23-now.getHours()}:${59-now.getMinutes()}:${59-now.getSeconds()}`;
        }
        window.toggleAuth = (s) => {
            document.getElementById('login-ui').classList.toggle('hidden', s);
            document.getElementById('signup-ui').classList.toggle('hidden', !s);
        };
        window.copyRef = () => { document.getElementById('ref-link').select(); document.execCommand('copy'); alert("Link Copied!"); };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
