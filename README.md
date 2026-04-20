<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --slate: #0f172a; --bg: #ffffff; }
        body { background: var(--bg); color: var(--slate); font-family: 'Inter', sans-serif; overflow-x: hidden; }
        
        /* Modern Glass Cards */
        .nexus-card { background: #fff; border: 1px solid rgba(0,0,0,0.04); border-radius: 40px; box-shadow: 0 20px 60px rgba(0,0,0,0.02); transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1); }
        .nexus-card:hover { transform: translateY(-10px); box-shadow: 0 30px 80px rgba(0,0,0,0.05); }

        /* Trust Badge Animation */
        .verified-badge { background: linear-gradient(135deg, #10b981 0%, #059669 100%); color: white; padding: 4px 12px; border-radius: 100px; font-size: 8px; font-weight: 900; letter-spacing: 1px; display: inline-flex; align-items: center; gap: 4px; }

        /* Login Styling */
        #auth-overlay { position: fixed; inset: 0; background: #fff; z-index: 5000; display: flex; align-items: center; justify-center; }
        .input-pro { background: #f8fafc; border: 2px solid transparent; border-radius: 20px; padding: 18px; width: 100%; font-weight: 700; transition: 0.3s; }
        .input-pro:focus { border-color: var(--gold); background: #fff; box-shadow: 0 10px 30px rgba(243,186,47,0.1); }

        /* New Corporate Section */
        .roadmap-item { border-left: 2px solid #f1f5f9; padding-left: 20px; position: relative; }
        .roadmap-item::before { content: ''; position: absolute; left: -6px; top: 0; width: 10px; height: 10px; background: var(--gold); border-radius: 50%; }

        .btn-main { background: var(--gold); color: #000; font-weight: 900; padding: 18px; border-radius: 22px; width: 100%; text-transform: uppercase; letter-spacing: 1.5px; transition: 0.3s; }
        .btn-main:hover { transform: scale(1.02); box-shadow: 0 15px 35px rgba(243,186,47,0.25); }
    </style>
</head>
<body>

    <div id="auth-overlay">
        <div class="w-full max-w-sm p-10">
            <div class="text-center mb-12">
                <div class="w-16 h-16 bg-black rounded-3xl mx-auto mb-6 flex items-center justify-center text-white text-3xl font-black">N</div>
                <h1 class="text-2xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
                <p id="auth-sub" class="text-[9px] font-black text-slate-400 uppercase tracking-[0.4em] mt-2">Institutional Node Access</p>
            </div>

            <div id="login-form" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal Username" class="input-pro">
                <input type="password" id="l-pass" placeholder="Security Password" class="input-pro">
                <button onclick="handleLogin()" class="btn-main">Connect to Mainframe</button>
                <p class="text-center text-[10px] font-black text-slate-300 uppercase mt-4">No node ID? <span onclick="switchAuth(true)" class="text-black cursor-pointer underline">Initialize ID</span></p>
            </div>

            <div id="signup-form" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Username" class="input-pro">
                <input type="email" id="s-email" placeholder="Official Email" class="input-pro">
                <input type="password" id="s-pass" placeholder="Create Password" class="input-pro">
                <button onclick="handleSignup()" class="btn-main">Create Identity</button>
                <p class="text-center text-[10px] font-black text-slate-300 uppercase mt-4">Have an ID? <span onclick="switchAuth(false)" class="text-black cursor-pointer underline">Log In</span></p>
            </div>
        </div>
    </div>

    <div id="main-dashboard" class="hidden">
        <nav class="sticky top-0 bg-white/80 backdrop-blur-2xl border-b border-slate-50 px-8 py-5 flex justify-between items-center z-[1000]">
            <div class="flex items-center gap-4">
                <h2 class="text-xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
                <div class="verified-badge hidden md:flex"><i class="fa-solid fa-circle-check"></i> SECURED NODE</div>
            </div>
            <div class="flex items-center gap-5">
                <div class="text-right hidden sm:block">
                    <p id="display-name" class="text-[10px] font-black uppercase">Admin</p>
                    <p class="text-[8px] font-bold text-slate-400">GOLD ELITE MEMBER</p>
                </div>
                <button onclick="logout()" class="w-10 h-10 bg-slate-50 rounded-2xl flex items-center justify-center text-slate-300"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </nav>

        <main class="container mx-auto px-6 py-10 space-y-12">
            
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                <div class="lg:col-span-2 nexus-card p-12 bg-gradient-to-br from-white to-slate-50 relative overflow-hidden">
                    <div class="absolute -right-20 -top-20 w-64 h-64 bg-yellow-500/5 rounded-full blur-3xl"></div>
                    <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-4">Total Net Equity (USD)</p>
                    <h2 id="balance-txt" class="text-7xl md:text-8xl font-black italic tracking-tighter mb-12 text-slate-900">$0.00</h2>
                    <div class="flex flex-wrap gap-4">
                        <button class="px-10 py-5 bg-[#f3ba2f] text-black font-black rounded-2xl text-[10px] uppercase shadow-xl shadow-yellow-500/20">Add Funds</button>
                        <button class="px-10 py-5 bg-white border border-slate-100 text-slate-400 font-black rounded-2xl text-[10px] uppercase">Withdraw Assets</button>
                    </div>
                </div>

                <div class="nexus-card p-10 flex flex-col justify-between">
                    <div>
                        <p class="text-[10px] font-black text-slate-400 uppercase mb-8">System Analytics</p>
                        <div class="space-y-6">
                            <div class="flex justify-between font-bold"> <span class="text-slate-400 text-xs italic">Daily Return</span> <span class="text-green-500 text-sm">+$24.40</span> </div>
                            <div class="flex justify-between font-bold"> <span class="text-slate-400 text-xs italic">Active Nodes</span> <span class="text-sm">1,242</span> </div>
                            <div class="flex justify-between font-bold"> <span class="text-slate-400 text-xs italic">Hash Rate</span> <span class="text-blue-500 text-sm">1.2 EH/s</span> </div>
                        </div>
                    </div>
                    <div class="pt-8 border-t border-slate-50 flex items-center gap-3">
                        <div class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
                        <span class="text-[9px] font-black text-slate-400 uppercase tracking-widest">Encrypted Cloud Link</span>
                    </div>
                </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div class="nexus-card p-10">
                    <h3 class="text-sm font-black uppercase mb-8 italic">Corporate Roadmap 2026</h3>
                    <div class="space-y-8">
                        <div class="roadmap-item"><p class="text-[10px] font-black">Q1: INFRASTRUCTURE EXPANSION</p><p class="text-[10px] text-slate-400">Deploying Zurich & Tokyo Quantum Nodes.</p></div>
                        <div class="roadmap-item opacity-40"><p class="text-[10px] font-black">Q3: NEXUS TOKEN LAUNCH</p><p class="text-[10px] text-slate-400">Institutional-grade liquidity pool opening.</p></div>
                    </div>
                </div>
                <div class="nexus-card p-10 bg-slate-900 text-white">
                    <h3 class="text-sm font-black uppercase mb-4 italic text-[#f3ba2f]">Why Trust Nexus?</h3>
                    <p class="text-xs text-slate-400 leading-relaxed mb-8">We utilize 256-bit AES encryption and multi-sig cold wallets to ensure your assets are protected under UK-Financial guidelines.</p>
                    <div class="flex gap-4 opacity-50">
                        <i class="fa-brands fa-cc-visa text-2xl"></i>
                        <i class="fa-brands fa-cc-mastercard text-2xl"></i>
                        <i class="fa-brands fa-bitcoin text-2xl"></i>
                    </div>
                </div>
            </div>

            <footer class="pt-20 pb-10 border-t border-slate-100">
                <div class="grid grid-cols-1 md:grid-cols-4 gap-12 text-center md:text-left">
                    <div class="col-span-2">
                        <h4 class="text-xl font-black italic uppercase mb-4">Nexus Infinity <span class="text-[#f3ba2f]">Institutional</span></h4>
                        <p class="text-xs text-slate-400 leading-loose max-w-sm">Registered under Entity #7729-10-UK. Regulated by GFCA. Level 42, The Shard, London Bridge Street, UK.</p>
                    </div>
                    <div>
                        <h5 class="text-[10px] font-black uppercase mb-6 text-slate-900">Framework</h5>
                        <ul class="text-xs text-slate-400 font-bold space-y-4">
                            <li class="hover:text-black cursor-pointer">Privacy Protocol</li>
                            <li class="hover:text-black cursor-pointer">Risk Management</li>
                        </ul>
                    </div>
                    <div>
                        <h5 class="text-[10px] font-black uppercase mb-6 text-slate-900">Inquiries</h5>
                        <p class="text-xs font-black">admin@nexus-infinity.pro</p>
                    </div>
                </div>
            </footer>
        </main>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
            apiKey: "AIzaSyBEqvT7AYCTZg1Bb6zEDtJn71QrYopX73M",
            authDomain: "coin-07.firebaseapp.com",
            databaseURL: "https://coin-07-default-rtdb.firebaseio.com",
            projectId: "coin-07",
            storageBucket: "coin-07.firebasestorage.app",
            appId: "1:341970060013:web:67374c0fd262b63bd342e4"
        };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        window.switchAuth = (signup) => {
            document.getElementById('login-form').classList.toggle('hidden', signup);
            document.getElementById('signup-form').classList.toggle('hidden', !signup);
            document.getElementById('auth-sub').innerText = signup ? "Initialize Global Identity" : "Institutional Node Access";
        };

        window.handleSignup = async () => {
            const user = document.getElementById('s-user').value.trim();
            const pass = document.getElementById('s-pass').value.trim();
            const email = document.getElementById('s-email').value.trim();
            if(!user || !pass) return alert("Credentials required!");
            
            const snap = await get(ref(db, `users/${user}`));
            if(snap.exists()) return alert("Username taken!");
            
            await set(ref(db, `users/${user}`), { username: user, email, password: pass, balance: 0 });
            alert("Node ID Generated! Log in now.");
            switchAuth(false);
        };

        window.handleLogin = async () => {
            const user = document.getElementById('l-user').value.trim();
            const pass = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${user}`));
            
            if(snap.exists() && snap.val().password === pass) {
                localStorage.setItem('nexus_current_user', user);
                renderApp(user);
            } else {
                alert("Security Breach: Invalid Credentials!");
            }
        };

        function renderApp(user) {
            document.getElementById('auth-overlay').classList.add('hidden');
            document.getElementById('main-dashboard').classList.remove('hidden');
            document.getElementById('display-name').innerText = user;

            onValue(ref(db, `users/${user}`), (snap) => {
                const d = snap.val();
                if(d) document.getElementById('balance-txt').innerText = '$' + (d.balance || 0).toLocaleString();
            });
        }

        window.logout = () => { localStorage.clear(); location.reload(); };

        const session = localStorage.getItem('nexus_current_user');
        if(session) renderApp(session);
    </script>
</body>
</html>
