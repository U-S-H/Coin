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
        .input-pro:focus { border-color: var(--gold); background: #fff; box-shadow: 0 10px 30px rgba(243,186,47,0.1); }
        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 900; padding: 18px; border-radius: 20px; width: 100%; text-transform: uppercase; letter-spacing: 1px; border: none; cursor: pointer; box-shadow: 0 10px 25px rgba(243,186,47,0.2); }
        
        .method-card { border: 2px solid #f1f5f9; border-radius: 20px; padding: 15px; cursor: pointer; transition: 0.3s; text-align: center; }
        .method-card.active { border-color: var(--gold); background: #fffdf5; }
        
        .nav-item { cursor: pointer; font-size: 10px; font-weight: 800; color: #94a3b8; text-align: center; transition: 0.3s; }
        .nav-item.active { color: #000; }
        .hidden { display: none !important; }

        /* Animations */
        @keyframes pulse-soft { 0%, 100% { opacity: 1; } 50% { opacity: 0.5; } }
        .live-dot { width: 8px; height: 8px; background: #22c55e; border-radius: 50%; animation: pulse-soft 2s infinite; }
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
                <input type="text" id="s-ref" placeholder="Referral Code (Optional)" class="input-pro text-center">
                <button onclick="handleSignup()" class="btn-gold w-full">Initialize Node</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">Have ID? <span onclick="toggleAuth(false)" class="text-black underline cursor-pointer">Back to Login</span></p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-28">
        <nav class="sticky top-0 bg-white/80 backdrop-blur-xl border-b p-5 flex justify-between items-center z-[500]">
            <div class="flex items-center gap-2">
                <div class="w-8 h-8 bg-black text-white rounded-lg flex items-center justify-center font-black text-xs">N</div>
                <span id="nav-user" class="font-black italic uppercase text-sm">USER</span>
            </div>
            <button onclick="logout()" class="text-slate-300 hover:text-red-500 transition"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-card p-10 bg-slate-900 text-white relative overflow-hidden">
                <div class="absolute -right-10 -top-10 w-40 h-40 bg-[#f3ba2f]/10 rounded-full blur-3xl"></div>
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mb-2">Equity Valuation</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                
                <div class="mt-8 flex items-center gap-4">
                    <div class="flex-1">
                        <p class="text-[8px] font-black text-slate-500 uppercase">Yield Countdown</p>
                        <p id="timer" class="text-lg font-black text-[#f3ba2f] tabular-nums">23:59:59</p>
                    </div>
                    <div class="flex-1 text-right">
                        <p class="text-[8px] font-black text-slate-500 uppercase">Daily Profit</p>
                        <p id="profit-txt" class="text-lg font-black text-green-400">+$0.00</p>
                    </div>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-4">
                <div class="glass-card p-6"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Active Nodes</p><p class="font-black text-sm">Institutional-01</p></div>
                <div class="glass-card p-6 flex items-center justify-center gap-2"><div class="live-dot"></div><p class="text-[9px] font-black uppercase tracking-widest">Network Live</p></div>
            </div>

            <div class="glass-card p-6">
                <p class="text-[9px] font-black text-slate-400 uppercase mb-3">Your Referral Node (Bonus Active)</p>
                <div class="flex gap-2">
                    <input id="ref-link" readonly class="bg-slate-50 p-3 rounded-xl text-[10px] font-bold w-full outline-none" value="">
                    <button onclick="copyRef()" class="bg-black text-white px-5 rounded-xl text-[9px] font-black uppercase">Copy</button>
                </div>
            </div>
        </div>

        <div id="page-deposit" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Asset Injection</h3>
            <div class="glass-card p-6 space-y-5">
                <div class="grid grid-cols-3 gap-2">
                    <div class="method-card active" onclick="selDep('trx')"><p class="text-[8px] font-black">TRX</p></div>
                    <div class="method-card" onclick="selDep('eth')"><p class="text-[8px] font-black">ETH</p></div>
                    <div class="method-card" onclick="selDep('usdt')"><p class="text-[8px] font-black">USDT</p></div>
                </div>
                <div class="bg-slate-50 p-4 rounded-2xl break-all">
                    <p class="text-[8px] font-black text-slate-400 mb-1">RECEPTION ADDRESS:</p>
                    <p id="dep-address" class="text-[10px] font-bold text-slate-700">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount (USD)" class="input-pro">
                <input type="text" id="dep-tid" placeholder="Transaction Hash" class="input-pro">
                <div class="text-left">
                    <p class="text-[9px] font-black text-slate-300 uppercase mb-2">Upload Transfer Proof:</p>
                    <input type="file" id="dep-proof" accept="image/*" class="text-[10px]">
                </div>
                <button onclick="submitDep()" class="btn-gold w-full">Confirm Deposit</button>
            </div>
        </div>

        <div id="page-withdraw" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Liquidate Capital</h3>
            <div class="glass-card p-6 space-y-4">
                <select id="w-meth" class="input-pro"><option value="trx">TRX (Trust Wallet)</option><option value="eth">ETH (MetaMask)</option><option value="usdt">USDT TRC-20</option></select>
                <input type="text" id="w-addr" placeholder="Destination Wallet Address" class="input-pro">
                <input type="number" id="w-amt" placeholder="Amount to Withdraw" class="input-pro">
                <button onclick="submitWith()" class="btn-gold w-full">Submit Liquidation</button>
            </div>
        </div>

        <div id="page-menu" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Terminal Settings</h3>
            <div class="space-y-3">
                <button onclick="showPop('faq')" class="glass-card p-5 w-full flex justify-between items-center"><span class="text-[10px] font-black uppercase">FAQ Center</span><i class="fa-solid fa-chevron-right text-slate-300"></i></button>
                <button onclick="showPop('policy')" class="glass-card p-5 w-full flex justify-between items-center"><span class="text-[10px] font-black uppercase">Privacy Policy</span><i class="fa-solid fa-chevron-right text-slate-300"></i></button>
                <button onclick="showPop('details')" class="glass-card p-5 w-full flex justify-between items-center"><span class="text-[10px] font-black uppercase">Company Details</span><i class="fa-solid fa-chevron-right text-slate-300"></i></button>
            </div>
            
            <div class="glass-card p-6 bg-slate-50">
                <p class="text-[9px] font-black uppercase text-slate-400 mb-2">System Version</p>
                <p class="text-[10px] font-bold">Nexus Infinity Core v4.0.2 (Institutional)</p>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-white border-t p-5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-grid-2 block text-lg mb-1"></i>Home</div>
            <div onclick="switchPage('deposit')" class="nav-item"><i class="fa-solid fa-plus-circle block text-lg mb-1"></i>Deposit</div>
            <div onclick="switchPage('withdraw')" class="nav-item"><i class="fa-solid fa-minus-circle block text-lg mb-1"></i>Withdraw</div>
            <div onclick="switchPage('menu')" class="nav-item"><i class="fa-solid fa-bars block text-lg mb-1"></i>Menu</div>
        </div>
    </div>

    <div id="modal" class="fixed inset-0 bg-white z-[2000] p-10 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10">
            <h2 id="modal-title" class="text-xl font-black uppercase italic">Title</h2>
            <button onclick="closePop()" class="text-3xl">&times;</button>
        </div>
        <div id="modal-body" class="text-xs text-slate-500 leading-relaxed space-y-4"></div>
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

        // UI Logic
        window.onload = () => {
            startTimer();
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const user = localStorage.getItem('nexus_user');
                if(user) showDashboard(user);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        window.toggleAuth = (s) => {
            document.getElementById('login-ui').classList.toggle('hidden', s);
            document.getElementById('signup-ui').classList.toggle('hidden', !s);
        };

        window.switchPage = (p) => {
            ['home', 'deposit', 'withdraw', 'menu'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            event.currentTarget.classList.add('active');
        };

        // Timer Logic
        function startTimer() {
            setInterval(() => {
                const now = new Date();
                const hours = 23 - now.getHours();
                const mins = 59 - now.getMinutes();
                const secs = 59 - now.getSeconds();
                document.getElementById('timer').innerText = `${String(hours).padStart(2, '0')}:${String(mins).padStart(2, '0')}:${String(secs).padStart(2, '0')}`;
            }, 1000);
        }

        // AUTH
        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            const r = document.getElementById('s-ref').value.trim();
            if(!u || !p) return alert("Credentials Required!");

            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists()) return alert("Username Taken!");

            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, referredBy: r });
            alert("ID Created! Login now.");
            toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) {
                localStorage.setItem('nexus_user', u);
                showDashboard(u);
            } else alert("Invalid Access Key!");
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            document.getElementById('ref-link').value = window.location.origin + window.location.pathname + "?ref=" + uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val();
                if(data) {
                    document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toLocaleString();
                    document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toLocaleString();
                }
            });
        }

        // DEPOSIT
        window.selDep = (t) => {
            document.querySelectorAll('.method-card').forEach(c => c.classList.remove('active'));
            event.currentTarget.classList.add('active');
            document.getElementById('dep-address').innerText = addresses[t];
        };

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const file = document.getElementById('dep-proof').files[0];
            if(!amt || !tid || !file) return alert("Fill all fields!");

            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async () => {
                await push(ref(db, 'admin/deposits'), {
                    user, amount: amt, tid, proof: reader.result, status: 'pending', date: new Date().toISOString()
                });
                alert("Deposit Logged. Awaiting Verification.");
                switchPage('home');
            };
        };

        // WITHDRAWAL
        window.submitWith = async () => {
            const user = localStorage.getItem('nexus_user');
            const addr = document.getElementById('w-addr').value;
            const amt = document.getElementById('w-amt').value;
            const meth = document.getElementById('w-meth').value;
            if(!amt || !addr) return alert("Enter wallet details!");

            await push(ref(db, 'admin/withdrawals'), {
                user, wallet: addr, amount: amt, method: meth, status: 'pending', date: new Date().toISOString()
            });
            alert("Liquidation Request Submitted.");
            switchPage('home');
        };

        // POPUPS
        window.showPop = (type) => {
            const modal = document.getElementById('modal');
            const title = document.getElementById('modal-title');
            const body = document.getElementById('modal-body');
            modal.classList.remove('hidden');

            if(type === 'faq') {
                title.innerText = "Help Center";
                body.innerHTML = "<p><b>How to deposit?</b><br>Go to Deposit page, copy address, and send assets. Upload TID & Screenshot.</p><p><b>Withdrawal Time?</b><br>Institutional withdrawals take 1-6 hours.</p>";
            } else if(type === 'policy') {
                title.innerText = "Privacy Policy";
                body.innerHTML = "<p>We use AES-256 encryption. Your node activity is private. No data is shared with third-party regulators.</p>";
            } else {
                title.innerText = "Company Info";
                body.innerHTML = "<p>Nexus Infinity Global Ltd.<br>Registered Entity #77291-UK.<br>Dubai Hub: Node-AX90.</p>";
            }
        };

        window.closePop = () => document.getElementById('modal').classList.add('hidden');
        window.copyRef = () => { document.getElementById('ref-link').select(); document.execCommand('copy'); alert("Referral Copied!"); };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
