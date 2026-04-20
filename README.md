<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Institutional Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --slate: #0f172a; }
        body { background: #ffffff; font-family: 'Plus Jakarta Sans', sans-serif; overflow-x: hidden; }

        /* Splash Screen Animation */
        #splash {
            position: fixed; inset: 0; background: #000; z-index: 9999;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            transition: 1s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .splash-logo { animation: pulseLogo 2s infinite; }
        @keyframes pulseLogo { 0% { transform: scale(1); opacity: 0.8; } 50% { transform: scale(1.1); opacity: 1; } 100% { transform: scale(1); opacity: 0.8; } }

        /* Modern Inputs */
        .input-box {
            background: #f8fafc; border: 2px solid transparent; border-radius: 24px;
            padding: 20px; width: 100%; font-weight: 700; transition: 0.4s;
            outline: none; text-align: center;
        }
        .input-box:focus { border-color: var(--gold); background: #fff; box-shadow: 0 15px 40px rgba(243,186,47,0.15); }

        .btn-premium {
            background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%);
            color: #000; font-weight: 900; padding: 20px; border-radius: 24px;
            width: 100%; text-transform: uppercase; letter-spacing: 2px;
            box-shadow: 0 10px 30px rgba(243, 186, 47, 0.3); transition: 0.3s;
        }
        .btn-premium:active { transform: scale(0.96); }

        .trust-tag { font-size: 8px; font-weight: 900; letter-spacing: 2px; color: #cbd5e1; text-transform: uppercase; }
    </style>
</head>
<body>

    <div id="splash">
        <div class="text-white text-center">
            <div class="w-20 h-20 bg-white text-black rounded-3xl mx-auto mb-6 flex items-center justify-center text-4xl font-black splash-logo text-center">N</div>
            <h2 class="text-2xl font-black italic tracking-tighter mb-2">NEXUS <span class="text-[#f3ba2f]">INFINITY</span></h2>
            <p class="text-[10px] font-bold text-slate-500 tracking-[0.5em] uppercase">Securing Digital Assets</p>
        </div>
    </div>

    <div id="auth-screen" class="min-h-screen flex flex-col items-center justify-center p-8">
        
        <div class="w-full max-w-sm space-y-12">
            <div class="text-center space-y-4">
                <div class="w-16 h-16 bg-black rounded-[2rem] mx-auto flex items-center justify-center text-white text-3xl font-black shadow-2xl">N</div>
                <h1 class="text-3xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
                <div class="flex items-center justify-center gap-2">
                    <span class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></span>
                    <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest">Global Terminal Active</p>
                </div>
            </div>

            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal Username" class="input-box">
                <input type="password" id="l-pass" placeholder="Security Password" class="input-box">
                <button onclick="handleLogin()" class="btn-premium">Connect to Mainframe</button>
                <p class="text-center text-[10px] font-black text-slate-300 uppercase">No Node Access? <span onclick="toggleAuth(true)" class="text-black cursor-pointer underline">Initialize ID</span></p>
            </div>

            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Choose Username" class="input-box">
                <input type="email" id="s-email" placeholder="Official Email" class="input-box">
                <input type="password" id="s-pass" placeholder="Create Password" class="input-box">
                <button onclick="handleSignup()" class="btn-premium">Register Node</button>
                <p class="text-center text-[10px] font-black text-slate-300 uppercase">Already Registered? <span onclick="toggleAuth(false)" class="text-black cursor-pointer underline">Back to Login</span></p>
            </div>

            <div class="pt-10 border-t border-slate-50 grid grid-cols-2 gap-8 text-center">
                <div>
                    <p class="text-lg font-black italic">$2.4B+</p>
                    <p class="trust-tag">Assets Secured</p>
                </div>
                <div>
                    <p class="text-lg font-black italic">142.5 TH/s</p>
                    <p class="trust-tag">Node Power</p>
                </div>
            </div>

            <div class="flex justify-center gap-6 opacity-20 grayscale">
                <i class="fa-solid fa-shield-halved text-2xl"></i>
                <i class="fa-solid fa-fingerprint text-2xl"></i>
                <i class="fa-solid fa-lock text-2xl"></i>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden">
        </div>

    <script type="module">
        // Firebase Config (Aapka purana wala)
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

        // Splash Hide Logic
        window.onload = () => {
            setTimeout(() => {
                document.getElementById('splash').style.opacity = '0';
                setTimeout(() => document.getElementById('splash').style.display = 'none', 1000);
            }, 2500);
        };

        window.toggleAuth = (signup) => {
            document.getElementById('login-ui').classList.toggle('hidden', signup);
            document.getElementById('signup-ui').classList.toggle('hidden', !signup);
        };

        // Custom Auth & Persistence (Aapki request par)
        window.handleLogin = async () => {
            const user = document.getElementById('l-user').value.trim();
            const pass = document.getElementById('l-pass').value.trim();
            if(!user || !pass) return alert("Security Check: Missing Credentials!");

            const snap = await get(ref(db, `users/${user}`));
            if(snap.exists() && snap.val().password === pass) {
                localStorage.setItem('nexus_session', user);
                alert("Access Granted. Syncing Terminal...");
                location.reload(); // Dashboard logic is linked to localstorage check
            } else {
                alert("Unauthorized Access Attempt!");
            }
        };

        // Yahan aap baaki signup logic bhi add kar sakte hain
    </script>
</body>
</html>
