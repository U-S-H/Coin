<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Institutional Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        :root { --gold: #f3ba2f; --bg: #ffffff; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0f172a; margin: 0; overflow-x: hidden; }

        /* UI Kit */
        .glass-card { background: #fff; border: 1px solid rgba(0,0,0,0.05); border-radius: 30px; box-shadow: 0 10px 40px rgba(0,0,0,0.01); transition: 0.3s ease; }
        .input-pro { background: #f8fafc; border: 2px solid transparent; border-radius: 18px; padding: 16px; width: 100%; font-weight: 700; outline: none; transition: 0.3s; }
        .input-pro:focus { border-color: var(--gold); background: #fff; }
        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 900; padding: 18px; border-radius: 20px; width: 100%; text-transform: uppercase; letter-spacing: 1px; border: none; cursor: pointer; }
        
        /* Status Badges */
        .status-pending { background: #fef9c3; color: #a16207; }
        .status-approved { background: #dcfce7; color: #15803d; }
        .status-rejected { background: #fee2e2; color: #b91c1c; }
        .badge { padding: 4px 10px; border-radius: 100px; font-size: 8px; font-weight: 800; text-transform: uppercase; }

        .nav-item { cursor: pointer; font-size: 10px; font-weight: 800; color: #94a3b8; text-align: center; }
        .nav-item.active { color: #000; }
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-16 h-16 bg-white text-black rounded-2xl flex items-center justify-center text-3xl font-black mb-4">N</div>
        <h1 class="text-white font-black italic text-xl uppercase tracking-widest">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="w-full max-w-sm space-y-10">
            <div class="text-center">
                <div class="w-20 h-20 bg-black text-white rounded-[2rem] mx-auto flex items-center justify-center text-4xl font-black mb-6 shadow-2xl">N</div>
                <h2 class="text-3xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
            </div>
            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal ID" class="input-pro text-center">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-pro text-center">
                <button onclick="handleLogin()" class="btn-gold w-full">Authorize Entry</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">New Node? <span onclick="toggleAuth(true)" class="text-black underline cursor-pointer">Register Identity</span></p>
            </div>
            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Choose Username" class="input-pro text-center">
                <input type="password" id="s-pass" placeholder="Create Password" class="input-pro text-center">
                <button onclick="handleSignup()" class="btn-gold w-full">Initialize Node</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">Registered? <span onclick="toggleAuth(false)" class="text-black underline cursor-pointer">Back to Login</span></p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-28">
        <nav class="sticky top-0 bg-white/80 backdrop-blur-xl border-b p-5 flex justify-between items-center z-[500]">
            <div class="flex items-center gap-2">
                <div class="w-8 h-8 bg-black text-white rounded-lg flex items-center justify-center font-black text-xs">N</div>
                <span id="nav-user" class="font-black italic uppercase text-sm">USER</span>
            </div>
            <button onclick="logout()" class="text-slate-300"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-card p-10 bg-slate-900 text-white relative overflow-hidden">
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mb-2">Equity Valuation</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 flex items-center gap-4">
                    <div class="flex-1"><p class="text-[8px] font-black text-slate-500 uppercase">Countdown</p><p id="timer" class="text-lg font-black text-[#f3ba2f]">23:59:59</p></div>
                    <div class="flex-1 text-right"><p class="text-[8px] font-black text-slate-500 uppercase">Daily Profit</p><p id="profit-txt" class="text-lg font-black text-green-400">+$0.00</p></div>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4">
                <button onclick="switchPage('deposit')" class="glass-card p-6 text-[10px] font-black uppercase text-center"><i class="fa-solid fa-plus-circle block text-lg mb-2 text-[#f3ba2f]"></i>Deposit</button>
                <button onclick="switchPage('withdraw')" class="glass-card p-6 text-[10px] font-black uppercase text-center"><i class="fa-solid fa-minus-circle block text-lg mb-2 text-slate-400"></i>Withdraw</button>
            </div>
        </div>

        <div id="page-deposit" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Asset Injection</h3>
            <div class="glass-card p-6 space-y-5 text-center">
                <p class="text-[9px] font-black text-slate-400 uppercase">Copy Network Address</p>
                <div class="bg-slate-50 p-4 rounded-2xl break-all">
                    <p class="text-[7px] font-black text-slate-300 mb-1">USDT TRC20 / TRX:</p>
                    <p class="text-[10px] font-bold">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount (USD)" class="input-pro">
                <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="input-pro">
                <input type="file" id="dep-proof" accept="image/*" class="text-[10px] w-full">
                <button onclick="submitDep()" class="btn-gold w-full">Submit Transfer</button>
            </div>
        </div>

        <div id="page-history" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Institutional Ledger</h3>
            <div class="space-y-4">
                <p class="text-[10px] font-black text-slate-400 uppercase">Recent Transactions</p>
                <div id="history-list" class="space-y-3">
                    <p class="text-center text-[10px] text-slate-300 italic py-10">No records found in node...</p>
                </div>
            </div>
        </div>

        <div id="page-withdraw" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Withdraw Capital</h3>
            <div class="glass-card p-6 space-y-4">
                <input type="text" id="w-addr" placeholder="Wallet Address" class="input-pro">
                <input type="number" id="w-amt" placeholder="Amount (USD)" class="input-pro">
                <button onclick="submitWith()" class="btn-gold w-full">Initialize Payout</button>
            </div>
        </div>

        <div id="page-menu" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Information Hub</h3>
            <div class="space-y-2">
                <div class="glass-card p-5 text-[10px] font-black uppercase">FAQ Center</div>
                <div class="glass-card p-5 text-[10px] font-black uppercase">Privacy Policy</div>
                <div class="glass-card p-5 text-[10px] font-black uppercase">Company Terms</div>
            </div>
            <div class="glass-card p-6 mt-10">
                <p class="text-[9px] font-black text-slate-400 uppercase mb-2">Referral Code</p>
                <p id="ref-code" class="text-sm font-black italic"></p>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-white border-t p-5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-home block text-lg mb-1"></i>Home</div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-list-ul block text-lg mb-1"></i>History</div>
            <div onclick="switchPage('menu')" class="nav-item"><i class="fa-solid fa-info-circle block text-lg mb-1"></i>Info</div>
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

        window.onload = () => {
            setInterval(startTimer, 1000);
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const user = localStorage.getItem('nexus_user');
                if(user) showDashboard(user);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        window.switchPage = (p) => {
            ['home', 'deposit', 'history', 'withdraw', 'menu'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            if(event) event.currentTarget.classList.add('active');
        };

        function startTimer() {
            const now = new Date();
            document.getElementById('timer').innerText = `${23-now.getHours()}:${59-now.getMinutes()}:${59-now.getSeconds()}`;
        }

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Fill details!");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("Registered! Login now."); toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) {
                localStorage.setItem('nexus_user', u);
                showDashboard(u);
            } else alert("Error!");
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            document.getElementById('ref-code').innerText = uid.toUpperCase();

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val();
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0);
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0);
            });

            // LOAD HISTORY
            onValue(ref(db, `users/${uid}/transactions`), (snap) => {
                const logs = snap.val();
                let html = "";
                if(logs) {
                    Object.values(logs).reverse().forEach(t => {
                        html += `<div class="glass-card p-5 flex justify-between items-center">
                            <div><p class="text-[9px] font-black uppercase">${t.type}</p><p class="text-[8px] text-slate-400">${t.date}</p></div>
                            <div class="text-right">
                                <p class="text-[10px] font-bold mb-1">$${t.amount}</p>
                                <span class="badge status-${t.status}">${t.status}</span>
                            </div>
                        </div>`;
                    });
                    document.getElementById('history-list').innerHTML = html;
                }
            });
        }

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const file = document.getElementById('dep-proof').files[0];
            if(!amt || !tid || !file) return alert("All fields required!");

            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async () => {
                const data = { type: 'deposit', amount: amt, tid: tid, proof: reader.result, status: 'pending', date: new Date().toLocaleString() };
                const newRef = push(ref(db, `users/${user}/transactions`));
                await set(newRef, data);
                await set(ref(db, `admin/deposits/${newRef.key}`), { ...data, user });
                alert("Deposit Pending!");
                switchPage('history');
            };
        };

        window.submitWith = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('w-amt').value;
            const addr = document.getElementById('w-addr').value;
            if(!amt || !addr) return alert("Details required!");

            const data = { type: 'withdraw', amount: amt, wallet: addr, status: 'pending', date: new Date().toLocaleString() };
            const newRef = push(ref(db, `users/${user}/transactions`));
            await set(newRef, data);
            await set(ref(db, `admin/withdrawals/${newRef.key}`), { ...data, user });
            alert("Withdrawal Pending!");
            switchPage('history');
        };

        window.toggleAuth = (s) => {
            document.getElementById('login-ui').classList.toggle('hidden', s);
            document.getElementById('signup-ui').classList.toggle('hidden', !s);
        };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
