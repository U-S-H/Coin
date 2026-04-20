<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Institutional Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --bg: #f9fbff; }
        body { background-color: var(--bg); color: #1e293b; font-family: 'Inter', sans-serif; }
        
        .premium-card { background: white; border-radius: 35px; border: 1px solid rgba(226, 232, 240, 0.8); box-shadow: 0 15px 45px rgba(0,0,0,0.02); transition: 0.4s; }
        .premium-card:hover { transform: translateY(-8px); box-shadow: 0 25px 60px rgba(0,0,0,0.06); }
        
        .status-badge { padding: 5px 12px; border-radius: 50px; font-size: 9px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; }
        .active-pulse { position: relative; }
        .active-pulse::after { content: ''; position: absolute; width: 8px; height: 8px; background: #22c55e; border-radius: 50%; right: -2px; top: -2px; animation: pulse 2s infinite; }
        
        @keyframes pulse { 0% { transform: scale(1); opacity: 1; } 100% { transform: scale(2.5); opacity: 0; } }
        
        .crypto-ticker { background: #000; color: #fff; font-size: 10px; font-weight: 900; padding: 8px 0; overflow: hidden; white-space: nowrap; }
        .ticker-wrap { display: inline-block; animation: ticker 30s linear infinite; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }

        .sidebar { position: fixed; left: -320px; width: 300px; height: 100%; background: white; z-index: 2000; transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1); box-shadow: 20px 0 60px rgba(0,0,0,0.05); }
        .sidebar.active { left: 0; }
        .overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.1); backdrop-filter: blur(5px); z-index: 1500; display: none; }
        .overlay.active { display: block; }
    </style>
</head>
<body>

    <div class="crypto-ticker">
        <div class="ticker-wrap uppercase tracking-widest">
            BTC/USD: $64,231.50 (+1.2%) &nbsp;&nbsp; | &nbsp;&nbsp; ETH/USD: $3,452.12 (-0.4%) &nbsp;&nbsp; | &nbsp;&nbsp; USDT/USD: $1.00 (STABLE) &nbsp;&nbsp; | &nbsp;&nbsp; NEXUS NODE HASHRATE: 142.5 TH/S &nbsp;&nbsp; | &nbsp;&nbsp; SYSTEM STATUS: OPTIMIZED
        </div>
    </div>

    <div class="overlay" id="overlay" onclick="toggleMenu()"></div>

    <aside class="sidebar p-10 flex flex-col justify-between" id="sidebar">
        <div class="space-y-12">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-black rounded-xl flex items-center justify-center text-white font-black">N</div>
                <h2 class="text-xl font-black italic uppercase tracking-tighter">Menu</h2>
            </div>
            <nav class="space-y-6">
                <div class="flex items-center gap-4 text-sm font-bold text-slate-400 hover:text-black cursor-pointer"><i class="fa-solid fa-gauge-high"></i> Dashboard</div>
                <div class="flex items-center gap-4 text-sm font-bold text-slate-400 hover:text-black cursor-pointer"><i class="fa-solid fa-shield-halved"></i> Security Center</div>
                <div class="flex items-center gap-4 text-sm font-bold text-slate-400 hover:text-black cursor-pointer"><i class="fa-solid fa-headset"></i> Support Terminal</div>
            </nav>
        </div>
        <button onclick="logout()" class="w-full py-4 bg-red-50 text-red-500 rounded-2xl font-black text-[10px] uppercase tracking-widest">Terminate Session</button>
    </aside>

    <nav class="sticky top-0 bg-white/80 backdrop-blur-xl border-b border-slate-100 px-8 py-5 flex justify-between items-center z-[1000]">
        <div class="flex items-center gap-6">
            <i class="fa-solid fa-bars-staggered text-xl cursor-pointer" onclick="toggleMenu()"></i>
            <h1 id="main-logo" class="text-xl font-black italic tracking-tighter uppercase cursor-pointer">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
        </div>
        <div class="flex items-center gap-4">
            <div class="hidden md:flex flex-col items-end mr-2">
                <span id="user-id" class="text-[9px] font-black text-slate-400 uppercase tracking-widest italic">Guest_User</span>
                <span class="text-[8px] font-bold text-green-500 uppercase">Verified Account</span>
            </div>
            <div class="w-10 h-10 bg-slate-100 rounded-full flex items-center justify-center font-black active-pulse">U</div>
        </div>
    </nav>

    <main class="container mx-auto px-6 py-10 space-y-10">
        
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            
            <div class="lg:col-span-2 premium-card p-12 bg-gradient-to-br from-white to-[#fcfdff]">
                <div class="flex justify-between items-start mb-6">
                    <p class="text-[10px] font-black text-slate-400 uppercase tracking-[0.4em]">Available Portfolio</p>
                    <span class="text-[10px] font-black text-green-500 bg-green-50 px-3 py-1 rounded-full">+2.45% Today</span>
                </div>
                <h2 id="balance-display" class="text-7xl md:text-8xl font-black italic tracking-tighter mb-12 text-slate-900">$0.00</h2>
                <div class="flex gap-4">
                    <button onclick="openModal('dep')" class="flex-1 md:flex-none px-12 py-5 bg-[#f3ba2f] text-black font-black rounded-2xl text-[10px] uppercase shadow-xl shadow-yellow-500/20 hover:scale-105 transition">Add Asset</button>
                    <button onclick="openModal('wit')" class="flex-1 md:flex-none px-12 py-5 bg-slate-100 text-slate-400 font-black rounded-2xl text-[10px] uppercase hover:bg-slate-200">Liquidate</button>
                </div>
            </div>

            <div class="premium-card p-10 flex flex-col justify-between border-b-4 border-[#f3ba2f]">
                <div>
                    <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-8">Node Performance</p>
                    <div class="space-y-6">
                        <div class="flex justify-between items-center"><span class="text-xs font-bold text-slate-500 italic">Daily Yield</span><span class="text-xs font-black text-green-500">+$14.20</span></div>
                        <div class="flex justify-between items-center"><span class="text-xs font-bold text-slate-500 italic">Total Profit</span><span id="profit-display" class="text-xs font-black text-blue-500">$0.00</span></div>
                        <div class="flex justify-between items-center"><span class="text-xs font-bold text-slate-500 italic">Node Status</span><span class="text-[9px] font-black bg-blue-50 text-blue-600 px-2 py-1 rounded">ACTIVE</span></div>
                    </div>
                </div>
                <div class="pt-8 border-t border-slate-50">
                    <button onclick="claimBonus()" class="w-full py-4 bg-black text-white text-[9px] font-black uppercase tracking-widest rounded-2xl hover:bg-slate-800 transition">Claim Daily Bonus</button>
                </div>
            </div>
        </div>

        <div class="space-y-6">
            <h3 class="text-center text-[11px] font-black text-slate-300 uppercase tracking-[0.6em]">Global Infrastructure Cluster</h3>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="nodes-container"></div>
        </div>

        <div class="premium-card p-10">
            <div class="flex justify-between items-center mb-10">
                <h4 class="text-sm font-black italic uppercase">Institutional Ledger</h4>
                <div class="flex items-center gap-2 text-[9px] font-bold text-slate-400 uppercase"><i class="fa-solid fa-lock text-green-500"></i> Encrypted Transaction Log</div>
            </div>
            <div class="overflow-x-auto">
                <table class="w-full text-left">
                    <thead class="text-[10px] font-black text-slate-300 uppercase border-b border-slate-100">
                        <tr><th class="pb-6">Date</th><th class="pb-6">Operation</th><th class="pb-6">Value (USD)</th><th class="pb-6">Status</th></tr>
                    </thead>
                    <tbody id="history-rows" class="text-xs font-bold"></tbody>
                </table>
            </div>
        </div>

    </main>

    <footer class="bg-white border-t border-slate-100 py-20 px-8">
        <div class="container mx-auto grid grid-cols-1 md:grid-cols-4 gap-16">
            <div class="col-span-1 md:col-span-2 space-y-6">
                <h2 class="text-2xl font-black italic uppercase">Nexus Infinity <span class="text-[#f3ba2f]">Group</span></h2>
                <p class="text-xs text-slate-400 leading-relaxed max-w-sm">Nexus Infinity is a licensed provider of high-frequency mining clusters and decentralized liquidity pools. Registered in the United Kingdom under Entity #77291-UK.</p>
                <div class="flex gap-6 grayscale opacity-40">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/5/5e/Visa_Inc._logo.svg" class="h-4">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/2/2a/Mastercard-logo.svg" class="h-4">
                    <i class="fa-brands fa-bitcoin text-xl"></i>
                </div>
            </div>
            <div class="space-y-6">
                <h4 class="text-[10px] font-black uppercase text-slate-900">Legal Framework</h4>
                <div class="flex flex-col gap-3 text-xs text-slate-400 font-bold">
                    <span class="hover:text-black cursor-pointer" onclick="alert('Privacy Policy v5.1 Updated')">Privacy Protocol</span>
                    <span class="hover:text-black cursor-pointer">Risk Disclosure</span>
                    <span class="hover:text-black cursor-pointer">AML Compliance</span>
                </div>
            </div>
            <div class="space-y-6">
                <h4 class="text-[10px] font-black uppercase text-slate-900">Corporate Office</h4>
                <p class="text-xs text-slate-400 leading-loose font-medium">Level 42, The Shard<br>London Bridge Street<br>United Kingdom</p>
                <p class="text-xs text-slate-900 font-black">admin@nexus-infinity.pro</p>
            </div>
        </div>
    </footer>

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
        let userUID = localStorage.getItem('nexus_uid');

        // Toggle Sidebar
        window.toggleMenu = () => { document.getElementById('sidebar').classList.toggle('active'); document.getElementById('overlay').classList.toggle('active'); };
        window.logout = () => { localStorage.clear(); location.reload(); };

        // Nodes Configuration
        const nodes = [
            {n:"Aegis", l:"Dubai", p:1.8, h:"98%"}, {n:"Vortex", l:"Zurich", p:2.5, h:"99%"},
            {n:"Apex", l:"London", p:5.2, h:"94%"}, {n:"Titan", l:"Tokyo", p:8.5, h:"91%"}
        ];
        document.getElementById('nodes-container').innerHTML = nodes.map(node => `
            <div class="premium-card p-8">
                <div class="flex justify-between items-center mb-6"><span class="text-[9px] font-black text-slate-300 uppercase">${node.n}_CLUSTER</span><i class="fa-solid fa-atom text-[#f3ba2f]"></i></div>
                <h4 class="text-xl font-black italic uppercase mb-1">${node.l}</h4>
                <p class="text-[10px] font-bold text-green-500 mb-6">+${node.p}% Daily Yield</p>
                <div class="pt-4 border-t border-slate-50 flex justify-between text-[9px] font-black uppercase">
                    <span class="text-slate-400">Node Health</span><span class="text-blue-500">${node.h}</span>
                </div>
            </div>
        `).join('');

        // Identity & Core Logic
        if(!userUID) {
            const email = prompt("Access Key Required (Email):");
            if(email) {
                userUID = email.replace(/[.#$[\]]/g, "_");
                localStorage.setItem('nexus_uid', userUID);
                set(ref(db, `users/${userUID}`), { email, balance: 0, profit: 0, history: [] }).then(()=>location.reload());
            }
        } else {
            document.getElementById('user-id').innerText = userUID;
            onValue(ref(db, `users/${userUID}`), (snap) => {
                const data = snap.val();
                if(data) {
                    document.getElementById('balance-display').innerText = '$' + (data.balance || 0).toLocaleString();
                    document.getElementById('profit-display').innerText = '$' + (data.profit || 0).toLocaleString();
                    const rows = document.getElementById('history-rows');
                    rows.innerHTML = data.history ? data.history.map(tx => `
                        <tr class="border-b border-slate-50">
                            <td class="py-6 text-slate-400 text-[10px]">${tx.date}</td>
                            <td class="py-6 uppercase text-[10px]">${tx.type}</td>
                            <td class="py-6">$${tx.amt}</td>
                            <td class="py-6"><span class="bg-slate-50 px-3 py-1 rounded-full text-blue-600 text-[9px] uppercase tracking-widest font-black">${tx.status}</span></td>
                        </tr>
                    `).join('') : `<tr><td colspan="4" class="py-10 text-center text-slate-300 uppercase">System Idle</td></tr>`;
                }
            });
        }
        
        window.claimBonus = () => alert("Syncing with Global Pool... Daily bonus will be credited in 12h, sweetie!");

        // Secret Admin Portal
        let taps = 0;
        document.getElementById('main-logo').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Auth Protocol:") === "coin786") alert("Terminal Access Granted! (Check previous version for full Admin UI)"); taps=0; }
            setTimeout(()=>taps=0, 2000);
        };
    </script>
</body>
</html>
