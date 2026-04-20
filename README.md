<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Master Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;700;800&display=swap');
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #ffffff; margin: 0; }
        .input-pro { background: #f8fafc; border: 2px solid transparent; border-radius: 20px; padding: 18px; width: 100%; font-weight: 700; outline: none; transition: 0.3s; text-align: center; }
        .input-pro:focus { border-color: #f3ba2f; background: #fff; }
        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 900; padding: 18px; border-radius: 20px; width: 100%; text-transform: uppercase; letter-spacing: 1px; cursor: pointer; border: none; box-shadow: 0 10px 25px rgba(243,186,47,0.2); }
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div id="auth-section" class="min-h-screen flex flex-col items-center justify-center p-6">
        <div class="w-full max-w-sm space-y-8 text-center">
            <div class="w-16 h-16 bg-black text-white rounded-[1.5rem] mx-auto flex items-center justify-center text-3xl font-black shadow-xl">N</div>
            <h1 class="text-3xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
            
            <div id="login-form" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal Username" class="input-pro">
                <input type="password" id="l-pass" placeholder="Password" class="input-pro">
                <button id="login-btn" class="btn-gold">Authorize Entry</button>
                <p class="text-[10px] font-black text-slate-400 uppercase">New Node? <span onclick="showSignup()" class="text-black underline cursor-pointer">Register Here</span></p>
            </div>

            <div id="signup-form" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Choose Username" class="input-pro">
                <input type="email" id="s-email" placeholder="Institutional Email" class="input-pro">
                <input type="password" id="s-pass" placeholder="Create Password" class="input-pro">
                <button id="signup-btn" class="btn-gold">Initialize Identity</button>
                <p class="text-[10px] font-black text-slate-400 uppercase">Have an ID? <span onclick="showLogin()" class="text-black underline cursor-pointer">Login Now</span></p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden">
        <nav class="p-6 border-b flex justify-between items-center">
            <h2 class="font-black italic uppercase text-lg">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
            <button onclick="logout()" class="text-slate-300"><i class="fa-solid fa-power-off"></i></button>
        </nav>
        <div class="p-8 space-y-6">
            <div class="bg-slate-50 p-10 rounded-[2.5rem]">
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest">Asset Balance</p>
                <h3 id="balance-val" class="text-5xl font-black italic tracking-tighter">$0.00</h3>
            </div>
            <p class="text-center text-[10px] font-bold text-slate-300 uppercase">Terminal Sync: Active</p>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

        // UI Switches
        window.showSignup = () => { document.getElementById('login-form').classList.add('hidden'); document.getElementById('signup-form').classList.remove('hidden'); };
        window.showLogin = () => { document.getElementById('signup-form').classList.add('hidden'); document.getElementById('login-form').classList.remove('hidden'); };

        // Signup Function
        document.getElementById('signup-btn').onclick = async () => {
            const user = document.getElementById('s-user').value.trim();
            const email = document.getElementById('s-email').value.trim();
            const pass = document.getElementById('s-pass').value.trim();

            if(!user || !pass) { alert("Username & Password required, sweetie!"); return; }

            const userRef = ref(db, 'users/' + user);
            const snapshot = await get(userRef);
            
            if(snapshot.exists()) {
                alert("Username already taken!");
            } else {
                await set(userRef, { username: user, email: email, password: pass, balance: 0 });
                alert("Identity Created! Now Login.");
                showLogin();
            }
        };

        // Login Function
        document.getElementById('login-btn').onclick = async () => {
            const user = document.getElementById('l-user').value.trim();
            const pass = document.getElementById('l-pass').value.trim();

            if(!user || !pass) return alert("Enter details!");

            const userRef = ref(db, 'users/' + user);
            const snapshot = await get(userRef);

            if(snapshot.exists() && snapshot.val().password === pass) {
                localStorage.setItem('nexus_user', user);
                showDashboard(user, snapshot.val().balance);
            } else {
                alert("Invalid Credentials!");
            }
        };

        function showDashboard(name, bal) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('balance-val').innerText = '$' + (bal || 0).toLocaleString();
        }

        window.logout = () => { localStorage.clear(); location.reload(); };

        // Auto-login check
        const savedUser = localStorage.getItem('nexus_user');
        if(savedUser) {
            const userRef = ref(db, 'users/' + savedUser);
            get(userRef).then(snap => {
                if(snap.exists()) showDashboard(savedUser, snap.val().balance);
            });
        }
    </script>
</body>
</html>
