<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;700;800&display=swap');
        :root { --gold: #f3ba2f; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; margin: 0; overflow-x: hidden; }

        /* Welcome Splash */
        #splash {
            position: fixed; inset: 0; background: #000; z-index: 9999;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            transition: 1s ease-in-out;
        }
        .splash-logo { animation: pulse 2s infinite; background: white; color: black; width: 80px; height: 80px; border-radius: 24px; display: flex; align-items: center; justify-content: center; font-size: 40px; font-weight: 900; }
        @keyframes pulse { 0%, 100% { transform: scale(1); opacity: 0.8; } 50% { transform: scale(1.1); opacity: 1; } }

        /* Modern UI */
        .glass-card { background: white; border: 1px solid rgba(0,0,0,0.05); border-radius: 35px; box-shadow: 0 15px 50px rgba(0,0,0,0.02); }
        .input-pro { background: #f8fafc; border: 2px solid transparent; border-radius: 22px; padding: 18px; width: 100%; font-weight: 700; outline: none; transition: 0.3s; text-align: center; }
        .input-pro:focus { border-color: var(--gold); background: #fff; box-shadow: 0 10px 30px rgba(243,186,47,0.1); }
        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 900; padding: 18px; border-radius: 22px; width: 100%; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; border: none; box-shadow: 0 10px 30px rgba(243,186,47,0.25); transition: 0.3s; }
        .btn-gold:active { transform: scale(0.95); }
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div id="splash">
        <div class="splash-logo">N</div>
        <h2 class="text-white mt-6 font-black italic text-2xl tracking-tighter uppercase">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
        <p class="text-slate-500 text-[9px] font-bold tracking-[0.4em] mt-2 uppercase">Institutional Grade Security</p>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="w-full max-w-sm space-y-10">
            <div class="text-center">
                <div class="w-16 h-16 bg-black text-white rounded-[1.8rem] mx-auto flex items-center justify-center text-3xl font-black mb-6 shadow-2xl">N</div>
                <h1 class="text-3xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
            </div>

            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal Username" class="input-pro">
                <input type="password" id="l-pass" placeholder="Password" class="input-pro">
                <button id="login-btn" class="btn-gold">Authorize Entry</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">New Node? <span onclick="toggleAuth(true)" class="text-black underline cursor-pointer">Initialize ID</span></p>
            </div>

            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Choose Username" class="input-pro">
                <input type="email" id="s-email" placeholder="Institutional Email" class="input-pro">
                <input type="password" id="s-pass" placeholder="Create Password" class="input-pro">
                <button id="signup-btn" class="btn-gold">Create Identity</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">Registered? <span onclick="toggleAuth(false)" class="text-black underline cursor-pointer">Login Now</span></p>
            </div>

            <div class="pt-8 grid grid-cols-2 gap-4 border-t border-slate-50 opacity-40">
                <div class="text-center"><p class="text-xs font-black italic">$2.4B+</p><p class="text-[7px] font-bold uppercase tracking-widest">Assets Secured</p></div>
                <div class="text-center"><p class="text-xs font-black italic">99.9%</p><p class="text-[7px] font-bold uppercase tracking-widest">System Uptime</p></div>
            </div>
        </div>
    </div>

    <div id="main-dashboard" class="hidden">
        <nav class="sticky top-0 bg-white/80 backdrop-blur-xl border-b border-slate-50 px-6 py-5 flex justify-between items-center z-[500]">
            <div class="flex items-center gap-3">
                <div class="w-8 h-8 bg-black text-white rounded-lg flex items-center justify-center font-black text-xs">N</div>
                <h2 class="font-black italic uppercase tracking-tighter text-lg">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
            </div>
            <button onclick="logout()" class="w-10 h-10 bg-slate-50 rounded-full flex items-center justify-center text-slate-300 hover:text-red-500 transition"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <main class="container mx-auto px-6 py-10 space-y-8">
            <div class="glass-card p-12 bg-gradient-to-br from-white to-slate-50 relative overflow-hidden">
                <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-2">Institutional Asset Portfolio</p>
                <h2 id="balance-val" class="text-6xl md:text-7xl font-black italic tracking-tighter text-slate-900 mb-10">$0.00</h2>
                <div class="flex gap-4">
                    <button class="px-8 py-4 bg-[#f3ba2f] text-black font-black rounded-2xl text-[9px] uppercase tracking-widest">Deposit</button>
                    <button class="px-8 py-4 bg-white border border-slate-100 text-slate-400 font-black rounded-2xl text-[9px] uppercase tracking-widest">Withdraw</button>
                </div>
            </div>

            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                <div class="glass-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Profit</p><p id="profit-val" class="text-sm font-black text-green-500">+$0.00</p></div>
                <div class="glass-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Status</p><p class="text-sm font-black text-blue-500 italic">Elite Node</p></div>
                <div class="glass-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Nodes</p><p class="text-sm font-black">Active</p></div>
                <div class="glass-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Link</p><div class="flex items-center justify-center gap-1"><div class="w-1.5 h-1.5 bg-green-500 rounded-full animate-pulse"></div><span class="text-[9px] font-black">Secure</span></div></div>
            </div>
        </main>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // AAPKI NEW CONFIGURATION
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

        // UI Logic
        window.onload = () => {
            setTimeout(() => {
                document.getElementById('splash').style.opacity = '0';
                setTimeout(() => {
                    document.getElementById('splash').classList.add('hidden');
                    const session = localStorage.getItem('nexus_user');
                    if(session) showDashboard(session);
                    else document.getElementById('auth-section').classList.remove('hidden');
                }, 1000);
            }, 2500);
        };

        window.toggleAuth = (s) => {
            document.getElementById('login-ui').classList.toggle('hidden', s);
            document.getElementById('signup-ui').classList.toggle('hidden', !s);
        };

        // SIGNUP
        document.getElementById('signup-btn').onclick = async () => {
            const u = document.getElementById('s-user').value.trim();
            const e = document.getElementById('s-email').value.trim();
            const p = document.getElementById('s-pass').value.trim();

            if(!u || !p) return alert("Credentials required, sweetie!");
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists()) return alert("Username taken!");

            await set(ref(db, `users/${u}`), { username: u, email: e, password: p, balance: 0, profit: 0 });
            alert("Node Identity Created! Please Login.");
            toggleAuth(false);
        };

        // LOGIN
        document.getElementById('login-btn').onclick = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();

            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) {
                localStorage.setItem('nexus_user', u);
                showDashboard(u);
            } else {
                alert("Security Access Denied: Invalid Credentials!");
            }
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('main-dashboard').classList.remove('hidden');
            
            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val();
                if(data) {
                    document.getElementById('balance-val').innerText = '$' + (data.balance || 0).toLocaleString();
                    document.getElementById('profit-val').innerText = '+$' + (data.profit || 0).toLocaleString();
                }
            });
        }

        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
