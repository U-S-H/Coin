<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Secure Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --bg: #f8fafc; }
        body { background-color: var(--bg); font-family: 'Inter', sans-serif; }
        .glass-ui { background: white; border: 1px solid rgba(0,0,0,0.05); border-radius: 35px; box-shadow: 0 15px 50px rgba(0,0,0,0.02); }
        .auth-input { background: #f1f5f9; border: 2px solid transparent; border-radius: 18px; padding: 15px; width: 100%; transition: 0.3s; font-weight: 600; outline: none; }
        .auth-input:focus { border-color: var(--gold); background: white; }
        .btn-gold { background: var(--gold); color: black; font-weight: 900; padding: 16px; border-radius: 18px; width: 100%; transition: 0.3s; text-transform: uppercase; letter-spacing: 1px; }
        .btn-gold:hover { transform: scale(1.02); box-shadow: 0 10px 20px rgba(243, 186, 47, 0.2); }
        #auth-overlay { position: fixed; inset: 0; background: white; z-index: 5000; display: flex; items-center; justify-center; }
    </style>
</head>
<body>

    <div id="auth-overlay">
        <div class="w-full max-w-md p-8">
            <div class="text-center mb-10">
                <h1 class="text-3xl font-black italic uppercase italic tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
                <p id="auth-tag" class="text-[10px] font-black text-slate-400 uppercase tracking-[0.3em] mt-2">Institutional Access Required</p>
            </div>

            <div id="login-form" class="space-y-4">
                <input type="text" id="l-user" placeholder="Username" class="auth-input">
                <input type="password" id="l-pass" placeholder="Password" class="auth-input">
                <button onclick="handleLogin()" class="btn-gold">Authorize Entry</button>
                <p class="text-center text-xs font-bold text-slate-400">New terminal? <span onclick="switchAuth(true)" class="text-black cursor-pointer underline">Create Identity</span></p>
            </div>

            <div id="signup-form" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Choose Username" class="auth-input">
                <input type="email" id="s-email" placeholder="Institutional Email" class="auth-input">
                <input type="password" id="s-pass" placeholder="Secure Password" class="auth-input">
                <button onclick="handleSignup()" class="btn-gold">Register Node</button>
                <p class="text-center text-xs font-bold text-slate-400">Already registered? <span onclick="switchAuth(false)" class="text-black cursor-pointer underline">Login</span></p>
            </div>
        </div>
    </div>

    <div id="main-app" class="hidden">
        <nav class="bg-white/80 backdrop-blur-md border-b border-slate-100 px-8 py-5 flex justify-between items-center sticky top-0 z-[1000]">
            <div class="flex items-center gap-4">
                <div class="w-8 h-8 bg-black rounded-lg flex items-center justify-center text-white font-black text-xs">N</div>
                <h2 class="text-lg font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
            </div>
            <div class="flex items-center gap-4">
                <div class="text-right">
                    <p id="nav-username" class="text-[10px] font-black text-slate-900 uppercase">User</p>
                    <p class="text-[8px] font-black text-green-500 uppercase">Tier 1 Elite</p>
                </div>
                <button onclick="logout()" class="w-10 h-10 bg-slate-50 rounded-full flex items-center justify-center text-slate-400"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </nav>

        <main class="container mx-auto px-6 py-10 space-y-8">
            <div class="glass-ui p-10 bg-gradient-to-br from-white to-slate-50 relative overflow-hidden">
                <div class="flex justify-between items-start">
                    <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest">Global Assets (USD)</p>
                    <i class="fa-solid fa-shield-check text-green-500"></i>
                </div>
                <h2 id="balance-val" class="text-6xl font-black italic tracking-tighter my-8">$0.00</h2>
                <div class="flex gap-4">
                    <button class="bg-[#f3ba2f] px-8 py-4 rounded-2xl text-[10px] font-black uppercase shadow-lg shadow-yellow-500/20">Deposit</button>
                    <button class="bg-white border border-slate-100 px-8 py-4 rounded-2xl text-[10px] font-black uppercase">Withdraw</button>
                </div>
            </div>

            <div class="grid grid-cols-2 md:grid-cols-4 gap-4 text-center">
                <div class="glass-ui p-6">
                    <p class="text-[8px] font-black text-slate-300 uppercase mb-1">Daily Profit</p>
                    <p class="text-sm font-black text-green-500">+$12.50</p>
                </div>
                <div class="glass-ui p-6">
                    <p class="text-[8px] font-black text-slate-300 uppercase mb-1">Nodes Active</p>
                    <p class="text-sm font-black">04</p>
                </div>
                <div class="glass-ui p-6">
                    <p class="text-[8px] font-black text-slate-300 uppercase mb-1">System Health</p>
                    <p class="text-sm font-black text-blue-500">99.9%</p>
                </div>
                <div class="glass-ui p-6">
                    <p class="text-[8px] font-black text-slate-300 uppercase mb-1">Live Sync</p>
                    <div class="flex items-center justify-center gap-1"><div class="w-1.5 h-1.5 bg-green-500 rounded-full animate-pulse"></div><span class="text-[10px] font-black italic">Active</span></div>
                </div>
            </div>

            <div class="glass-ui p-8">
                <h3 class="text-xs font-black uppercase mb-6 tracking-widest">Institutional Ledger</h3>
                <div id="history-list" class="space-y-4">
                    <p class="text-center text-[10px] font-bold text-slate-300 uppercase py-10">Waiting for data...</p>
                </div>
            </div>
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

        // Auth Navigation
        window.switchAuth = (showSignup) => {
            document.getElementById('login-form').classList.toggle('hidden', showSignup);
            document.getElementById('signup-form').classList.toggle('hidden', !showSignup);
            document.getElementById('auth-tag').innerText = showSignup ? "Create New Terminal ID" : "Institutional Access Required";
        };

        // SIGNUP LOGIC
        window.handleSignup = async () => {
            const user = document.getElementById('s-user').value.trim();
            const email = document.getElementById('s-email').value.trim();
            const pass = document.getElementById('s-pass').value.trim();

            if(!user || !pass || !email) return alert("Fill all fields, sweetie!");
            
            const userRef = ref(db, `users/${user}`);
            const snap = await get(userRef);
            
            if(snap.exists()) {
                alert("Username already taken!");
            } else {
                await set(userRef, { username: user, email: email, password: pass, balance: 0, history: [] });
                alert("Identity Created! Please Login.");
                switchAuth(false);
            }
        };

        // LOGIN LOGIC
        window.handleLogin = async () => {
            const user = document.getElementById('l-user').value.trim();
            const pass = document.getElementById('l-pass').value.trim();

            const userRef = ref(db, `users/${user}`);
            const snap = await get(userRef);

            if(snap.exists() && snap.val().password === pass) {
                localStorage.setItem('nexus_user', user);
                loadApp(user);
            } else {
                alert("Invalid Credentials, sweetie!");
            }
        };

        // LOAD APP
        function loadApp(userId) {
            document.getElementById('auth-overlay').classList.add('hidden');
            document.getElementById('main-app').classList.remove('hidden');
            document.getElementById('nav-username').innerText = userId;

            onValue(ref(db, `users/${userId}`), (snap) => {
                const data = snap.val();
                if(data) {
                    document.getElementById('balance-val').innerText = '$' + (data.balance || 0).toLocaleString();
                    // Load History
                    const hList = document.getElementById('history-list');
                    if(data.history) {
                        hList.innerHTML = data.history.map(tx => `
                            <div class="flex justify-between items-center p-4 bg-slate-50 rounded-2xl border border-slate-100">
                                <div><p class="text-[8px] font-black text-slate-400 uppercase">${tx.date}</p><p class="text-[11px] font-black uppercase">${tx.type}</p></div>
                                <div class="text-right"><p class="text-[11px] font-black">$${tx.amt}</p><p class="text-[9px] font-bold text-blue-500 uppercase">${tx.status}</p></div>
                            </div>
                        `).join('');
                    }
                }
            });
        }

        window.logout = () => { localStorage.clear(); location.reload(); };

        // SESSION CHECK
        const savedUser = localStorage.getItem('nexus_user');
        if(savedUser) loadApp(savedUser);
    </script>
</body>
</html>
