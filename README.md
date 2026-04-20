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

        /* Welcome Splash Screen */
        #splash {
            position: fixed; inset: 0; background: #000; z-index: 9999;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            transition: 1s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .splash-logo { animation: pulseLogo 2s infinite; background: white; color: black; width: 80px; height: 80px; border-radius: 24px; display: flex; align-items: center; justify-content: center; font-size: 40px; font-weight: 900; }
        @keyframes pulseLogo { 0%, 100% { transform: scale(1); opacity: 0.8; } 50% { transform: scale(1.1); opacity: 1; } }

        /* Modern Components */
        .glass-card { background: white; border: 1px solid rgba(0,0,0,0.04); border-radius: 40px; box-shadow: 0 20px 60px rgba(0,0,0,0.02); transition: 0.4s ease; }
        .input-pro { background: #f8fafc; border: 2px solid transparent; border-radius: 24px; padding: 20px; width: 100%; font-weight: 700; outline: none; transition: 0.3s; text-align: center; }
        .input-pro:focus { border-color: var(--gold); background: #fff; box-shadow: 0 15px 40px rgba(243,186,47,0.15); }
        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 900; padding: 20px; border-radius: 24px; width: 100%; text-transform: uppercase; letter-spacing: 1.5px; cursor: pointer; border: none; box-shadow: 0 10px 30px rgba(243,186,47,0.3); transition: 0.3s; }
        .btn-gold:active { transform: scale(0.96); }

        .roadmap-line { border-left: 2px solid #f1f5f9; padding-left: 20px; position: relative; margin-bottom: 20px; }
        .roadmap-line::before { content: ''; position: absolute; left: -6px; top: 0; width: 10px; height: 10px; background: var(--gold); border-radius: 50%; }

        .hidden { display: none !important; }
        .admin-btn { position: absolute; top: 0; left: 0; width: 50px; height: 50px; opacity: 0; cursor: pointer; z-index: 1000; }
    </style>
</head>
<body>

    <div id="splash">
        <div class="splash-logo">N</div>
        <h2 class="text-white mt-6 font-black italic text-2xl tracking-tighter uppercase">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
        <p class="text-slate-500 text-[10px] font-bold tracking-[0.5em] mt-2 uppercase">Institutional Grade terminal</p>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="w-full max-w-sm space-y-12">
            <div class="text-center">
                <div class="w-20 h-20 bg-black text-white rounded-[2rem] mx-auto flex items-center justify-center text-4xl font-black mb-6 shadow-2xl">N</div>
                <h1 class="text-3xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mt-2">Connecting to Secure Node...</p>
            </div>

            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal Username" class="input-pro">
                <input type="password" id="l-pass" placeholder="Security Password" class="input-pro">
                <button id="login-btn" class="btn-gold">Connect to Mainframe</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">No Node ID? <span onclick="toggleAuth(true)" class="text-black underline cursor-pointer">Register Identity</span></p>
            </div>

            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Create Username" class="input-pro">
                <input type="password" id="s-pass" placeholder="Create Security Password" class="input-pro">
                <button id="signup-btn" class="btn-gold">Initialize Identity</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">Have an ID? <span onclick="toggleAuth(false)" class="text-black underline cursor-pointer">Back to Login</span></p>
            </div>

            <div class="pt-10 grid grid-cols-2 gap-4 border-t border-slate-50 opacity-40 text-center">
                <div><p class="text-xs font-black italic">$2.4B+</p><p class="text-[7px] font-bold uppercase tracking-widest">Assets</p></div>
                <div><p class="text-xs font-black italic">AES-256</p><p class="text-[7px] font-bold uppercase tracking-widest">Encrypted</p></div>
            </div>
        </div>
    </div>

    <div id="main-dashboard" class="hidden">
        <div id="admin-trigger" class="admin-btn"></div>

        <nav class="sticky top-0 bg-white/80 backdrop-blur-2xl border-b border-slate-50 px-8 py-6 flex justify-between items-center z-[500]">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-black text-white rounded-2xl flex items-center justify-center font-black text-lg shadow-xl">N</div>
                <h2 class="font-black italic uppercase tracking-tighter text-xl">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
            </div>
            <button onclick="logout()" class="w-12 h-12 bg-slate-50 rounded-3xl flex items-center justify-center text-slate-300 hover:text-red-500 transition"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <main class="container mx-auto px-6 py-10 space-y-10">
            <div class="glass-card p-12 bg-gradient-to-br from-white to-slate-50 relative overflow-hidden">
                <div class="absolute -right-20 -top-20 w-64 h-64 bg-yellow-500/5 rounded-full blur-3xl"></div>
                <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-4">Total Net Equity (Institutional)</p>
                <h2 id="balance-val" class="text-7xl font-black italic tracking-tighter text-slate-900 mb-12">$0.00</h2>
                <div class="flex gap-4">
                    <button class="px-10 py-5 bg-[#f3ba2f] text-black font-black rounded-[1.5rem] text-[10px] uppercase tracking-widest shadow-xl shadow-yellow-500/20">Add Funds</button>
                    <button class="px-10 py-5 bg-white border border-slate-100 text-slate-400 font-black rounded-[1.5rem] text-[10px] uppercase tracking-widest">Withdraw</button>
                </div>
            </div>

            <div class="grid grid-cols-2 md:grid-cols-4 gap-6">
                <div class="glass-card p-8 text-center"><p class="text-[9px] font-black text-slate-300 uppercase mb-2 tracking-widest">Profit</p><p id="profit-val" class="text-lg font-black text-green-500">+$0.00</p></div>
                <div class="glass-card p-8 text-center"><p class="text-[9px] font-black text-slate-300 uppercase mb-2 tracking-widest">Status</p><p class="text-lg font-black text-blue-500 italic">Elite Node</p></div>
                <div class="glass-card p-8 text-center"><p class="text-[9px] font-black text-slate-300 uppercase mb-2 tracking-widest">Network</p><p class="text-lg font-black">Global</p></div>
                <div class="glass-card p-8 text-center"><p class="text-[9px] font-black text-slate-300 uppercase mb-2 tracking-widest">Security</p><div class="flex items-center justify-center gap-1"><div class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div><span class="text-xs font-black uppercase">Live</span></div></div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div class="glass-card p-10">
                    <h3 class="text-xs font-black uppercase mb-8 tracking-widest italic">Company Roadmap 2026</h3>
                    <div class="roadmap-line"><p class="text-[11px] font-black uppercase">Q1: Institutional Expansion</p><p class="text-[10px] text-slate-400">Deploying Zurich & Dubai Dedicated Nodes.</p></div>
                    <div class="roadmap-line opacity-40"><p class="text-[11px] font-black uppercase">Q3: Nexus Public Offering</p><p class="text-[10px] text-slate-400">Opening liquidity to private equity firms.</p></div>
                </div>
                <div class="glass-card p-10 bg-slate-900 text-white">
                    <h3 class="text-xs font-black uppercase mb-6 tracking-widest italic text-[#f3ba2f]">Why Trust Us?</h3>
                    <p class="text-xs text-slate-400 leading-relaxed mb-8">Nexus Infinity is protected by multi-signature vaults and high-frequency encryption. Registered Entity #77291-UK.</p>
                    <div class="flex gap-4 opacity-30 grayscale">
                        <i class="fa-brands fa-cc-visa text-2xl"></i>
                        <i class="fa-brands fa-cc-mastercard text-2xl"></i>
                        <i class="fa-brands fa-bitcoin text-2xl"></i>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-white z-[2000] p-10 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10">
            <h2 class="text-2xl font-black italic">Nexus Admin Terminal</h2>
            <button onclick="location.reload()" class="text-4xl font-thin">&times;</button>
        </div>
        <div id="admin-list" class="space-y-4"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // APP CONFIGURATION
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
                    const saved = localStorage.getItem('nexus_session');
                    if(saved) showDashboard(saved);
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
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Fill credentials, sweetie!");

            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists()) return alert("Node ID already exists!");

            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("Node Identity Initialized! Login now.");
            toggleAuth(false);
        };

        // LOGIN
        document.getElementById('login-btn').onclick = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();

            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) {
                localStorage.setItem('nexus_session', u);
                showDashboard(u);
            } else alert("Access Denied: Invalid Security Key!");
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

        // ADMIN SECRET (4 Taps on top-left invisible area)
        let taps = 0;
        document.getElementById('admin-trigger').onclick = () => {
            taps++;
            if(taps === 4) {
                if(prompt("System Key:") === "admin786") showAdminPanel();
                taps = 0;
            }
            setTimeout(() => taps = 0, 3000);
        };

        function showAdminPanel() {
            document.getElementById('admin-panel').classList.remove('hidden');
            onValue(ref(db, 'users'), (snap) => {
                const data = snap.val();
                let html = "";
                for(let id in data) {
                    html += `<div class="glass-card p-6 flex justify-between items-center">
                        <div><p class="text-xs font-black uppercase">${id}</p><p class="text-[10px] text-slate-400">Balance: $${data[id].balance}</p></div>
                        <div class="flex gap-2">
                            <button onclick="updateUser('${id}', 'balance')" class="bg-black text-white px-4 py-2 rounded-xl text-[9px] font-black uppercase">Update Bal</button>
                            <button onclick="updateUser('${id}', 'profit')" class="bg-green-500 text-white px-4 py-2 rounded-xl text-[9px] font-black uppercase">Update Prof</button>
                        </div>
                    </div>`;
                }
                document.getElementById('admin-list').innerHTML = html;
            });
        }

        window.updateUser = (uid, field) => {
            const val = prompt(`New ${field} for ${uid}:`);
            if(val) update(ref(db, `users/${uid}`), { [field]: parseFloat(val) });
        };
    </script>
</body>
</html>
