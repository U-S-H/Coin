<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Elite Dashboard v2.0</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        
        :root { --gold: #f3ba2f; --slate: #1e293b; --bg: #fdfdfd; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: var(--slate); margin: 0; overflow-x: hidden; }

        /* UI COMPONENTS */
        .premium-card { background: white; border: 1px solid rgba(0,0,0,0.03); border-radius: 35px; box-shadow: 0 15px 45px rgba(0,0,0,0.02); transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1); }
        .premium-card:hover { transform: translateY(-8px); box-shadow: 0 25px 60px rgba(0,0,0,0.05); }

        .status-badge { padding: 4px 10px; border-radius: 100px; font-size: 8px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; }
        .elite { background: #eff6ff; color: #2563eb; }

        /* Inputs & Buttons */
        .input-banking { background: #f8fafc; border: 2px solid transparent; border-radius: 20px; padding: 18px; width: 100%; font-weight: 700; text-align: center; transition: 0.3s; }
        .input-banking:focus { border-color: var(--gold); background: #fff; }

        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: black; font-weight: 900; padding: 18px; border-radius: 20px; width: 100%; text-transform: uppercase; letter-spacing: 1.5px; border: none; box-shadow: 0 10px 25px rgba(243,186,47,0.3); transition: 0.3s; }
        .btn-gold:active { transform: scale(0.96); }

        /* Utils */
        .hidden { display: none !important; }
        .active-dot { width: 8px; height: 8px; background: #22c55e; border-radius: 50%; display: inline-block; position: relative; }
        .active-dot::after { content:''; position: absolute; inset: -4px; border: 2px solid #22c55e; border-radius: 50%; opacity: 0.5; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { transform: scale(1); opacity: 0.5; } 100% { transform: scale(1.5); opacity: 0; } }

        /* Splash Screen */
        #splash { position: fixed; inset: 0; background: #000; z-index: 9999; display: flex; flex-direction: column; align-items: center; justify-content: center; transition: 1s ease-in-out; }
    </style>
</head>
<body>

    <div id="splash">
        <div class="text-white text-center">
            <div class="w-16 h-16 bg-white text-black rounded-3xl mx-auto flex items-center justify-center text-3xl font-black mb-6">N</div>
            <h2 class="text-2xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
            <p class="text-slate-500 text-[10px] font-bold tracking-[0.4em] mt-2 uppercase">Institutional Terminal</p>
        </div>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="w-full max-w-sm space-y-12">
            <div class="text-center">
                <div class="w-20 h-20 bg-black text-white rounded-[2rem] mx-auto flex items-center justify-center text-4xl font-black mb-6 shadow-2xl">N</div>
                <h1 class="text-3xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
            </div>

            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal Username" class="input-banking">
                <input type="password" id="l-pass" placeholder="Password" class="input-banking">
                <button onclick="handleLogin()" class="btn-gold w-full">Connect to Node</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase mt-4">New terminal? <span onclick="toggleAuth(true)" class="text-black underline cursor-pointer">Request ID</span></p>
            </div>

            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Create Username" class="input-banking">
                <input type="password" id="s-pass" placeholder="Create Password" class="input-banking">
                <button onclick="handleSignup()" class="btn-gold w-full">Initialize Node</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase mt-4">Have an ID? <span onclick="toggleAuth(false)" class="text-black underline cursor-pointer">Login Now</span></p>
            </div>
        </div>
    </div>

    <div id="main-dashboard" class="hidden">
        
        <nav class="sticky top-0 bg-white/70 backdrop-blur-2xl px-6 py-5 flex justify-between items-center z-[500] border-b border-slate-50">
            <div id="admin-logo-trigger" class="flex items-center gap-3 cursor-pointer">
                <div class="w-9 h-9 bg-black text-white rounded-xl flex items-center justify-center font-black text-sm shadow-xl">N</div>
                <h2 class="font-black italic uppercase tracking-tighter text-lg">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
            </div>
            <div class="flex items-center gap-4">
                <p id="display-user" class="text-[10px] font-black uppercase text-slate-400">Admin</p>
                <button onclick="logout()" class="w-10 h-10 bg-slate-50 rounded-2xl flex items-center justify-center text-slate-300 hover:text-red-500 transition"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </nav>

        <main class="container mx-auto px-6 py-10 space-y-10">
            <div class="premium-card p-10 bg-gradient-to-br from-white to-slate-50">
                <div class="flex justify-between items-start mb-4">
                    <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest">Available Capital (USD)</p>
                    <span class="text-[9px] font-bold text-green-500 bg-green-50 px-3 py-1 rounded-full">+2.15% TODAY</span>
                </div>
                <h2 id="balance-txt" class="text-6xl font-black italic tracking-tighter text-slate-900 mb-10">$0.00</h2>
                <div class="flex gap-4">
                    <button class="px-8 py-4 bg-[#f3ba2f] text-black font-black rounded-xl text-[9px] uppercase tracking-widest flex-1">Add Assets</button>
                    <button class="px-8 py-4 bg-white border border-slate-100 text-slate-400 font-black rounded-xl text-[9px] uppercase tracking-widest flex-1 hover:bg-slate-50 transition">Liquidate</button>
                </div>
            </div>

            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                <div class="premium-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Profit</p><p id="profit-txt" class="text-sm font-black text-green-500">+$0.00</p></div>
                <div class="premium-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Membership</p><p class="status-badge elite">ELITE NODE</p></div>
                <div class="premium-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Network</p><p class="text-sm font-black">Online</p></div>
                <div class="premium-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Live Sync</p><div class="flex items-center justify-center gap-1"><div class="active-dot"></div><span class="text-[10px] font-bold italic">Active</span></div></div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="premium-card p-8">
                    <h3 class="text-[10px] font-black uppercase mb-6 tracking-widest italic text-slate-900">Roadmap 2026</h3>
                    <p class="text-[10px] text-slate-400 border-l-2 border-[#f3ba2f] pl-4">Q1: Institutional Expansion. Zurich & Tokyo Nodes Deployment.</p>
                </div>
                <div class="premium-card p-8 bg-slate-900 text-white">
                    <h3 class="text-[10px] font-black uppercase mb-3 tracking-widest italic text-[#f3ba2f]">Why Trust Us?</h3>
                    <p class="text-xs text-slate-400 Leading-relaxed max-w-sm mb-6">Nexus Infinity is protected by 256-bit AES encryption and multi-sig vaults.</p>
                    <div class="flex gap-4 opacity-20 grayscale">
                        <i class="fa-brands fa-cc-visa text-2xl"></i>
                        <i class="fa-brands fa-cc-mastercard text-2xl"></i>
                        <i class="fa-brands fa-bitcoin text-2xl"></i>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // APP CONFIG (Working with new config)
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

        // Splash Hiding Logic
        window.onload = () => {
            setTimeout(() => {
                document.getElementById('splash').style.opacity = '0';
                setTimeout(() => {
                    document.getElementById('splash').classList.add('hidden');
                    const savedSession = localStorage.getItem('nexus_user');
                    if(savedSession) showDashboard(savedSession);
                    else document.getElementById('auth-section').classList.remove('hidden');
                }, 1000);
            }, 2500);
        };

        window.toggleAuth = (s) => {
            document.getElementById('login-ui').classList.toggle('hidden', s);
            document.getElementById('signup-ui').classList.toggle('hidden', !s);
        };

        // SIGNUP LOGIC
        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Fill credentials, sweetie!");

            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists()) return alert("Node ID taken!");

            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("Identity Created! Log in now.");
            toggleAuth(false);
        };

        // LOGIN LOGIC
        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();

            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) {
                localStorage.setItem('nexus_user', u); // SAVE SESSION
                showDashboard(u);
            } else alert("Invalid Access Key!");
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('main-dashboard').classList.remove('hidden');
            document.getElementById('display-user').innerText = uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val();
                if(data) {
                    document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toLocaleString();
                    document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toLocaleString();
                }
            });
        }

        window.logout = () => { localStorage.clear(); location.reload(); };

        // SECRET ADMIN TRIGGER (4 Taps on logo)
        let taps = 0;
        document.getElementById('admin-logo-trigger').onclick = () => {
            taps++;
            if(taps === 4) { alert("ADMIN TERMINAL | Add User Management UI here."); taps = 0; }
            setTimeout(() => taps = 0, 3000);
        };
    </script>
</body>
</html>
