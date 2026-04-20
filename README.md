<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Institutional Terminal (Light)</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --bg: #f8fafc; --text: #0f172a; }
        body { background-color: var(--bg); color: var(--text); font-family: 'Inter', sans-serif; overflow-x: hidden; transition: 0.4s; }
        
        /* Premium Light Glass */
        .glass-ui { 
            background: rgba(255, 255, 255, 0.8); 
            backdrop-filter: blur(30px); 
            border: 1px solid rgba(0, 0, 0, 0.05); 
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.03);
        }
        
        .sidebar { 
            position: fixed; top: 0; left: -300px; width: 300px; height: 100%; 
            background: white; z-index: 1000; transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 20px 0 50px rgba(0,0,0,0.05);
        }
        .sidebar.active { left: 0; }
        
        .overlay { 
            position: fixed; inset: 0; background: rgba(0,0,0,0.2); 
            z-index: 900; display: none; backdrop-filter: blur(5px);
        }
        .overlay.active { display: block; }

        .node-card { 
            background: white; border: 1px solid rgba(0,0,0,0.05); 
            border-radius: 35px; transition: 0.3s; 
        }
        .node-card:hover { transform: translateY(-10px); box-shadow: 0 25px 50px rgba(0,0,0,0.05); border-color: var(--gold); }
        
        .btn-primary { background: var(--gold); color: black; font-weight: 900; }
        .btn-secondary { background: #f1f5f9; color: #64748b; }
        
        #scan-line { position: fixed; top: 0; width: 100%; height: 2px; background: var(--gold); z-index: 1100; animation: scan 5s infinite linear; opacity: 0.3; }
        @keyframes scan { 0% { top: 0; } 100% { top: 100%; } }
    </style>
</head>
<body class="light-mode">

    <div id="scan-line"></div>
    <div class="overlay" id="overlay" onclick="toggleSidebar()"></div>

    <div class="sidebar p-8 flex flex-col justify-between" id="sidebar">
        <div>
            <div class="flex items-center gap-3 mb-12">
                <div class="w-8 h-8 bg-black rounded-lg flex items-center justify-center text-white font-black text-sm">N</div>
                <h2 class="font-black italic uppercase tracking-tighter">Menu</h2>
            </div>
            
            <nav class="space-y-6">
                <div class="flex items-center gap-4 text-sm font-bold text-slate-500 hover:text-black cursor-pointer transition">
                    <i class="fa-solid fa-user-gear"></i> Account Settings
                </div>
                <div class="flex items-center gap-4 text-sm font-bold text-slate-500 hover:text-black cursor-pointer transition">
                    <i class="fa-solid fa-shield-halved"></i> Security Protocol
                </div>
                <div class="flex items-center gap-4 text-sm font-bold text-slate-500 hover:text-black cursor-pointer transition">
                    <i class="fa-solid fa-clock-rotate-left"></i> Transaction History
                </div>
                <div class="flex items-center gap-4 text-sm font-bold text-slate-500 hover:text-black cursor-pointer transition">
                    <i class="fa-solid fa-headset"></i> 24/7 Support
                </div>
            </nav>
        </div>

        <button onclick="logout()" class="w-full py-4 bg-red-50 text-red-600 rounded-2xl font-black text-xs uppercase flex items-center justify-center gap-2 hover:bg-red-600 hover:text-white transition">
            <i class="fa-solid fa-power-off"></i> Terminate Session
        </button>
    </div>

    <nav class="glass-ui sticky top-0 z-[500] px-8 py-5 flex items-center justify-between border-b border-slate-100">
        <div class="flex items-center gap-4">
            <button onclick="toggleSidebar()" class="w-10 h-10 rounded-full hover:bg-slate-100 flex items-center justify-center">
                <i class="fa-solid fa-bars-staggered"></i>
            </button>
            <div class="flex flex-col">
                <h1 class="text-lg font-black italic tracking-tighter uppercase leading-none">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
                <span id="user-email-tag" class="text-[8px] font-bold text-slate-400 uppercase tracking-widest mt-1">Guest Terminal</span>
            </div>
        </div>
        
        <div class="flex items-center gap-4">
            <div class="hidden md:flex items-center gap-2 px-3 py-1 bg-green-50 rounded-full border border-green-100">
                <div class="w-1.5 h-1.5 bg-green-500 rounded-full animate-pulse"></div>
                <span class="text-[8px] font-black text-green-600 uppercase">Live Connectivity</span>
            </div>
            <button class="w-10 h-10 rounded-full bg-slate-100 flex items-center justify-center"><i class="fa-solid fa-bell text-slate-400"></i></button>
        </div>
    </nav>

    <main class="container mx-auto px-6 py-12 space-y-10">
        
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <div class="lg:col-span-2 glass-ui p-12 rounded-[50px] relative overflow-hidden">
                <p class="text-[10px] font-black text-slate-400 uppercase tracking-[0.5em] mb-4">Current Institutional Assets</p>
                <h2 id="balance-main" class="text-7xl md:text-8xl font-black italic tracking-tighter mb-12 text-slate-900">$0.00</h2>
                <div class="flex flex-wrap gap-4">
                    <button class="btn-primary px-10 py-5 rounded-2xl text-[10px] uppercase tracking-widest shadow-xl shadow-yellow-500/20 hover:scale-105 transition">Add Funds</button>
                    <button class="btn-secondary px-10 py-5 rounded-2xl text-[10px] uppercase tracking-widest hover:bg-slate-200 transition">Liquidate</button>
                </div>
            </div>

            <div class="glass-ui p-10 rounded-[50px] flex flex-col justify-between border-b-4 border-[#f3ba2f]">
                <div>
                    <h4 class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-6">Network Health</h4>
                    <div class="space-y-4">
                        <div class="flex justify-between items-center"><span class="text-xs font-bold text-slate-500">Hash Rate</span><span class="text-xs font-black">142.5 TH/s</span></div>
                        <div class="flex justify-between items-center"><span class="text-xs font-bold text-slate-500">Nodes Active</span><span class="text-xs font-black">12/15</span></div>
                        <div class="flex justify-between items-center"><span class="text-xs font-bold text-slate-500">System Load</span><span class="text-xs font-black text-green-500">Stable</span></div>
                    </div>
                </div>
                <div class="pt-6 border-t border-slate-50 flex items-center gap-4 text-slate-300">
                    <i class="fa-brands fa-cc-visa text-xl"></i>
                    <i class="fa-brands fa-cc-mastercard text-xl"></i>
                    <i class="fa-brands fa-bitcoin text-xl"></i>
                </div>
            </div>
        </div>

        <h3 class="text-xs font-black italic uppercase tracking-[0.6em] text-slate-300 text-center">Protocol Clusters v5.1</h3>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="nodes-container"></div>

    </main>

    <footer class="bg-white border-t border-slate-100 py-12 px-8">
        <div class="container mx-auto flex flex-col md:flex-row justify-between items-center gap-6">
            <p class="text-[9px] font-black text-slate-300 uppercase tracking-[0.5em]">&copy; 2026 Nexus Infinity Group. Institutional License #77291</p>
            <div class="flex gap-8 text-[9px] font-black text-slate-400 uppercase tracking-widest">
                <span class="hover:text-black cursor-pointer">Terms</span>
                <span class="hover:text-black cursor-pointer">Privacy</span>
                <span class="hover:text-black cursor-pointer">Audit</span>
            </div>
        </div>
    </footer>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // Your Firebase config
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

        // Sidebar Logic
        window.toggleSidebar = () => {
            document.getElementById('sidebar').classList.toggle('active');
            document.getElementById('overlay').classList.toggle('active');
        };

        // Logout Logic
        window.logout = () => {
            if(confirm("Sweetie, are you sure you want to terminate the session?")) {
                localStorage.removeItem('nexus_uid');
                location.reload();
            }
        };

        // Nodes Render
        const nodes = [
            {n: "Vortex", l: "Singapore", y: 1.5}, {n: "Aegis", l: "London", y: 2.2},
            {n: "Titan", l: "Dubai", y: 3.5}, {n: "Apex", l: "Tokyo", y: 5.8}
        ];
        document.getElementById('nodes-container').innerHTML = nodes.map(node => `
            <div class="node-card p-8 text-center">
                <div class="w-12 h-12 bg-slate-50 rounded-2xl flex items-center justify-center mx-auto mb-6 text-[#f3ba2f]">
                    <i class="fa-solid fa-atom"></i>
                </div>
                <h4 class="text-lg font-black italic uppercase mb-1">${node.l}</h4>
                <p class="text-[9px] font-bold text-slate-300 uppercase tracking-widest mb-6">${node.n} Cluster</p>
                <div class="flex justify-between text-[10px] font-black border-t border-slate-50 pt-4">
                    <span class="text-slate-400">DAILY</span><span class="text-green-500">+${node.y}%</span>
                </div>
            </div>
        `).join('');

        // Auth Sync
        let userUID = localStorage.getItem('nexus_uid');
        if(userUID) {
            document.getElementById('user-email-tag').innerText = userUID.replace("_", "@");
            onValue(ref(db, `users/${userUID}`), (snap) => {
                if(snap.exists()) {
                    document.getElementById('balance-main').innerText = '$' + snap.val().balance.toLocaleString(undefined, {minimumFractionDigits:2});
                }
            });
        }
    </script>
</body>
</html>
