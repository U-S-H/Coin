<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        :root { --gold: #f3ba2f; --bg: #fdfdfd; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #1e293b; margin: 0; overflow-x: hidden; }

        /* UI Kit */
        .glass-card { background: white; border: 1px solid rgba(0,0,0,0.04); border-radius: 30px; box-shadow: 0 10px 40px rgba(0,0,0,0.02); transition: 0.3s; }
        .input-pro { background: #f8fafc; border: 2px solid transparent; border-radius: 18px; padding: 15px; width: 100%; font-weight: 700; outline: none; transition: 0.3s; }
        .input-pro:focus { border-color: var(--gold); background: #fff; }
        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 900; padding: 16px; border-radius: 18px; width: 100%; text-transform: uppercase; letter-spacing: 1px; cursor: pointer; border: none; box-shadow: 0 10px 25px rgba(243,186,47,0.2); }
        .btn-gold:active { transform: scale(0.97); }
        
        .hidden { display: none !important; }
        .nav-item { cursor: pointer; font-size: 10px; font-weight: 800; text-transform: uppercase; color: #94a3b8; transition: 0.3s; }
        .nav-item.active { color: #000; border-bottom: 2px solid var(--gold); }

        /* Welcome Toast */
        #welcome-toast { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); background: #000; color: #fff; padding: 12px 25px; border-radius: 50px; font-weight: 800; font-size: 11px; z-index: 10000; display: none; box-shadow: 0 20px 40px rgba(0,0,0,0.2); }
    </style>
</head>
<body>

    <div id="welcome-toast">WELCOME BACK, USER</div>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-16 h-16 bg-white text-black rounded-2xl flex items-center justify-center text-3xl font-black mb-4">N</div>
        <h2 class="text-white font-black italic text-xl uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="w-full max-w-sm space-y-10 text-center">
            <div class="w-16 h-16 bg-black text-white rounded-3xl mx-auto flex items-center justify-center text-3xl font-black shadow-xl">N</div>
            <h1 class="text-3xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
            
            <div id="login-form" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal ID" class="input-pro text-center">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-pro text-center">
                <button onclick="handleLogin()" class="btn-gold">Authorize Entry</button>
                <p class="text-[9px] font-black text-slate-400 uppercase">New Node? <span onclick="toggleAuth(true)" class="text-black underline cursor-pointer">Register Identity</span></p>
            </div>

            <div id="signup-form" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Create Username" class="input-pro text-center">
                <input type="password" id="s-pass" placeholder="Create Password" class="input-pro text-center">
                <button onclick="handleSignup()" class="btn-gold">Initialize Node</button>
                <p class="text-[9px] font-black text-slate-400 uppercase">Registered? <span onclick="toggleAuth(false)" class="text-black underline cursor-pointer">Login Now</span></p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-24">
        <nav class="sticky top-0 bg-white/80 backdrop-blur-xl border-b p-6 flex justify-between items-center z-[500]">
            <div class="flex items-center gap-2">
                <div class="w-8 h-8 bg-black text-white rounded-lg flex items-center justify-center font-black text-xs">N</div>
                <span class="font-black italic uppercase text-sm">Nexus<span class="text-[#f3ba2f]">Infinity</span></span>
            </div>
            <button onclick="logout()" class="text-slate-300"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-card p-10 bg-gradient-to-br from-white to-slate-50 relative overflow-hidden">
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mb-2">Portfolio Value</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="flex gap-3 mt-8">
                    <button onclick="switchPage('deposit')" class="flex-1 bg-black text-white p-4 rounded-xl text-[9px] font-black uppercase">Deposit</button>
                    <button onclick="switchPage('withdraw')" class="flex-1 border p-4 rounded-xl text-[9px] font-black uppercase">Withdraw</button>
                </div>
            </div>

            <div class="glass-card p-6">
                <p class="text-[8px] font-black text-slate-300 uppercase mb-3">Referral Node</p>
                <div class="flex gap-2">
                    <input id="ref-link" readonly class="bg-slate-50 p-3 rounded-lg text-[10px] font-bold w-full outline-none" value="nexus.io/ref/user123">
                    <button onclick="copyRef()" class="bg-slate-100 p-3 rounded-lg px-5 text-[10px] font-black uppercase">Copy</button>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4">
                <button onclick="switchPage('faq')" class="glass-card p-6 text-center text-[9px] font-black uppercase"><i class="fa-solid fa-circle-question block mb-2 text-lg text-blue-500"></i> Help Center</button>
                <button onclick="switchPage('legal')" class="glass-card p-6 text-center text-[9px] font-black uppercase"><i class="fa-solid fa-shield-halved block mb-2 text-lg text-green-500"></i> Legal Info</button>
            </div>
        </div>

        <div id="page-deposit" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Initialize Deposit</h3>
            <div class="glass-card p-6 space-y-4">
                <p class="text-[10px] font-black text-slate-400">SELECT GATEWAY:</p>
                <select id="dep-method" class="input-pro">
                    <option value="easypaisa">EasyPaisa (03XX-XXXXXXX)</option>
                    <option value="jazzcash">JazzCash (03XX-XXXXXXX)</option>
                </select>
                <input type="number" id="dep-amount" placeholder="Amount (USD)" class="input-pro">
                <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="input-pro">
                <div class="text-left">
                    <label class="text-[10px] font-black text-slate-300 uppercase">Upload Proof (Screenshot):</label>
                    <input type="file" id="dep-proof" accept="image/*" class="mt-2 text-xs">
                </div>
                <button onclick="submitDeposit()" class="btn-gold">Confirm Asset Transfer</button>
            </div>
        </div>

        <div id="page-withdraw" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Liquidate Assets</h3>
            <div class="glass-card p-6 space-y-4">
                <input type="text" id="w-user" placeholder="Account Title" class="input-pro">
                <input type="number" id="w-acc" placeholder="Account Number" class="input-pro">
                <input type="number" id="w-amount" placeholder="Amount to Withdraw" class="input-pro">
                <select id="w-method" class="input-pro">
                    <option value="easypaisa">EasyPaisa</option>
                    <option value="jazzcash">JazzCash</option>
                </select>
                <button onclick="submitWithdraw()" class="btn-gold">Submit Request</button>
            </div>
        </div>

        <div id="page-faq" class="p-6 space-y-4 hidden">
            <h3 class="font-black italic uppercase text-lg">Frequently Asked</h3>
            <div class="space-y-2">
                <div class="glass-card p-4"><p class="text-[10px] font-black uppercase">How long do deposits take?</p><p class="text-[10px] text-slate-400 mt-1">Usually 10-30 minutes for manual verification.</p></div>
                <div class="glass-card p-4"><p class="text-[10px] font-black uppercase">What is the min withdrawal?</p><p class="text-[10px] text-slate-400 mt-1">The institutional minimum is $10.00.</p></div>
            </div>
        </div>

        <div id="page-legal" class="p-6 space-y-6 hidden text-left">
            <h3 class="font-black italic uppercase text-lg text-center">Institutional Policy</h3>
            <div class="glass-card p-6 space-y-4">
                <section>
                    <p class="text-[10px] font-black uppercase text-gold mb-1">Company Details</p>
                    <p class="text-[9px] text-slate-400">Nexus Infinity Global Ltd. Registered in UK/UAE. Asset Protection ID: 7729-NX.</p>
                </section>
                <section>
                    <p class="text-[10px] font-black uppercase text-gold mb-1">Privacy Policy</p>
                    <p class="text-[9px] text-slate-400">Your data is AES-256 encrypted. We never share institutional data with third parties.</p>
                </section>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-white border-t p-5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-house block text-lg mb-1"></i>Home</div>
            <div onclick="switchPage('deposit')" class="nav-item"><i class="fa-solid fa-wallet block text-lg mb-1"></i>Deposit</div>
            <div onclick="switchPage('withdraw')" class="nav-item"><i class="fa-solid fa-money-bill-transfer block text-lg mb-1"></i>Withdraw</div>
            <div onclick="switchPage('legal')" class="nav-item"><i class="fa-solid fa-file-contract block text-lg mb-1"></i>Policy</div>
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

        // UI HELPERS
        window.onload = () => {
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const user = localStorage.getItem('nexus_user');
                if(user) showDashboard(user);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        window.toggleAuth = (s) => {
            document.getElementById('login-form').classList.toggle('hidden', s);
            document.getElementById('signup-form').classList.toggle('hidden', !s);
        };

        window.switchPage = (p) => {
            ['home', 'deposit', 'withdraw', 'faq', 'legal'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
        };

        // AUTH CORE
        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Fill details!");
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists()) return alert("Username taken!");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("ID Initialized! Please Login.");
            toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) {
                localStorage.setItem('nexus_user', u);
                showDashboard(u);
            } else alert("Access Denied!");
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('ref-link').value = `nexus.io/ref/${uid}`;
            
            // Welcome Toast
            const toast = document.getElementById('welcome-toast');
            toast.innerText = `WELCOME BACK, ${uid.toUpperCase()}`;
            toast.style.display = 'block';
            setTimeout(() => toast.style.display = 'none', 3000);

            onValue(ref(db, `users/${uid}`), (snap) => {
                if(snap.exists()) {
                    document.getElementById('balance-txt').innerText = '$' + (snap.val().balance || 0).toLocaleString();
                }
            });
        }

        // DEPOSIT (WITH BASE64)
        window.submitDeposit = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amount').value;
            const tid = document.getElementById('dep-tid').value;
            const file = document.getElementById('dep-proof').files[0];

            if(!amt || !tid || !file) return alert("Complete all fields!");

            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async () => {
                const base64Img = reader.result;
                await push(ref(db, 'admin/deposits'), {
                    user: user, amount: amt, tid: tid, proof: base64Img, status: 'pending', date: new Date().toISOString()
                });
                alert("Deposit Request Submitted! Awaiting Admin Approval.");
                switchPage('home');
            };
        };

        // WITHDRAWAL
        window.submitWithdraw = async () => {
            const user = localStorage.getItem('nexus_user');
            const name = document.getElementById('w-user').value;
            const acc = document.getElementById('w-acc').value;
            const amt = document.getElementById('w-amount').value;
            const method = document.getElementById('w-method').value;

            if(!amt || !acc) return alert("Fill all details!");

            await push(ref(db, 'admin/withdrawals'), {
                user: user, accountTitle: name, accountNumber: acc, amount: amt, method: method, status: 'pending', date: new Date().toISOString()
            });
            alert("Withdrawal Request Recorded.");
            switchPage('home');
        };

        window.copyRef = () => {
            const link = document.getElementById('ref-link');
            link.select();
            document.execCommand('copy');
            alert("Referral Link Copied!");
        };

        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
