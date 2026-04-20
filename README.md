<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Pro Financial Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --bg: #f8fafc; }
        body { background-color: var(--bg); color: #0f172a; font-family: 'Inter', sans-serif; }
        .glass-card { background: white; border: 1px solid rgba(0,0,0,0.05); box-shadow: 0 10px 40px rgba(0,0,0,0.02); border-radius: 40px; }
        .status-pending { color: #f59e0b; background: #fffbeb; padding: 4px 10px; border-radius: 20px; font-size: 9px; font-weight: 900; }
        .status-approved { color: #10b981; background: #ecfdf5; padding: 4px 10px; border-radius: 20px; font-size: 9px; font-weight: 900; }
        .progress-bar { height: 4px; background: #f1f5f9; border-radius: 10px; overflow: hidden; }
        .progress-fill { height: 100%; background: var(--gold); width: 65%; animation: grow 3s infinite alternate; }
        @keyframes grow { from { width: 30%; } to { width: 80%; } }
        .sidebar { position: fixed; top: 0; left: -300px; width: 300px; height: 100%; background: white; z-index: 1000; transition: 0.4s; box-shadow: 20px 0 60px rgba(0,0,0,0.05); }
        .sidebar.active { left: 0; }
        .overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.2); z-index: 900; display: none; backdrop-filter: blur(4px); }
        .overlay.active { display: block; }
    </style>
</head>
<body class="p-0 m-0">

    <div class="overlay" id="overlay" onclick="toggleMenu()"></div>
    
    <div class="sidebar p-8 flex flex-col justify-between" id="sidebar">
        <div class="space-y-10">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-black rounded-xl flex items-center justify-center text-white font-black">N</div>
                <h2 class="font-black italic uppercase">Terminal</h2>
            </div>
            <nav class="space-y-6 text-sm font-bold text-slate-400">
                <div class="flex items-center gap-4 hover:text-black cursor-pointer"><i class="fa-solid fa-chart-line"></i> Market Analytics</div>
                <div class="flex items-center gap-4 hover:text-black cursor-pointer" onclick="scrollSection('history-sec')"><i class="fa-solid fa-receipt"></i> Operations Log</div>
                <div class="flex items-center gap-4 hover:text-black cursor-pointer"><i class="fa-solid fa-shield-halved"></i> Security Node</div>
            </nav>
        </div>
        <button onclick="logout()" class="w-full py-4 bg-red-50 text-red-600 rounded-2xl font-black text-[10px] uppercase">Logout Session</button>
    </div>

    <nav class="sticky top-0 bg-white/80 backdrop-blur-md px-8 py-5 flex justify-between items-center z-[800] border-b border-slate-100">
        <div class="flex items-center gap-5">
            <i class="fa-solid fa-bars-staggered cursor-pointer text-xl" onclick="toggleMenu()"></i>
            <h1 class="text-xl font-black italic uppercase">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
        </div>
        <div class="flex items-center gap-4">
            <div id="countdown" class="text-[10px] font-black bg-slate-100 px-3 py-1 rounded-full text-slate-500">SYNC: 23:59:59</div>
            <div class="w-10 h-10 bg-slate-100 rounded-full flex items-center justify-center font-black text-xs">U</div>
        </div>
    </nav>

    <main class="container mx-auto px-6 py-10 space-y-12">
        
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <div class="lg:col-span-2 glass-card p-12 relative overflow-hidden">
                <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-4">Total Net Equity</p>
                <h2 id="balance-val" class="text-7xl font-black italic tracking-tighter mb-10">$0.00</h2>
                <div class="flex gap-4">
                    <button class="bg-[#f3ba2f] px-8 py-4 rounded-2xl font-black text-[10px] uppercase shadow-lg shadow-yellow-500/20">Add Funds</button>
                    <button class="bg-slate-50 px-8 py-4 rounded-2xl font-black text-[10px] uppercase text-slate-400">Withdraw</button>
                </div>
            </div>
            
            <div class="glass-card p-10 flex flex-col justify-between">
                <div>
                    <p class="text-[10px] font-black text-slate-400 uppercase mb-6">Profit Analytics</p>
                    <div class="space-y-4">
                        <div class="flex justify-between text-xs font-bold"><span>Daily Profit</span><span class="text-green-500">+$14.20</span></div>
                        <div class="flex justify-between text-xs font-bold"><span>Total Yield</span><span class="text-blue-500">$284.10</span></div>
                    </div>
                </div>
                <div class="pt-6 border-t border-slate-50">
                    <div class="flex justify-between text-[10px] font-black text-slate-300 mb-2 uppercase"><span>Cycle Progress</span><span>65%</span></div>
                    <div class="progress-bar"><div class="progress-fill"></div></div>
                </div>
            </div>
        </div>

        <h3 class="text-center text-xs font-black text-slate-300 uppercase tracking-[0.5em]">Active Cluster Monitoring</h3>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="nodes-render"></div>

        <div id="history-sec" class="glass-card p-10 mt-12">
            <div class="flex justify-between items-center mb-8">
                <h4 class="text-sm font-black italic uppercase">Transaction Ledger</h4>
                <i class="fa-solid fa-file-invoice text-slate-200 text-2xl"></i>
            </div>
            <div class="overflow-x-auto">
                <table class="w-full text-left">
                    <thead>
                        <tr class="text-[10px] font-black text-slate-300 uppercase border-b border-slate-50">
                            <th class="pb-4">Timestamp</th>
                            <th class="pb-4">Type</th>
                            <th class="pb-4">Amount</th>
                            <th class="pb-4">Status</th>
                        </tr>
                    </thead>
                    <tbody id="history-rows" class="text-xs font-bold">
                        </tbody>
                </table>
            </div>
        </div>

    </main>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // Firebase Config
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

        // Sidebar & UI Logic
        window.toggleMenu = () => {
            document.getElementById('sidebar').classList.toggle('active');
            document.getElementById('overlay').classList.toggle('active');
        };
        window.logout = () => { localStorage.clear(); location.reload(); };

        // Nodes Data with Profit Days
        const nodes = [
            {n: "Aegis", l: "Singapore", p: "1.5%", d: "24/30 Days"},
            {n: "Titan", l: "Dubai", p: "2.8%", d: "12/30 Days"},
            {n: "Vortex", l: "Zurich", p: "4.5%", d: "08/30 Days"},
            {n: "Apex", l: "London", p: "6.2%", d: "02/30 Days"}
        ];

        document.getElementById('nodes-render').innerHTML = nodes.map(node => `
            <div class="glass-card p-8 hover:border-[#f3ba2f] transition-all">
                <div class="flex justify-between items-center mb-6">
                    <span class="text-[9px] font-black text-slate-300 uppercase">${node.n}</span>
                    <i class="fa-solid fa-bolt text-yellow-400"></i>
                </div>
                <h4 class="text-lg font-black italic uppercase mb-1">${node.l}</h4>
                <p class="text-[10px] font-bold text-green-500 mb-6">+${node.p} Daily Yield</p>
                <div class="pt-4 border-t border-slate-50 flex justify-between text-[9px] font-black uppercase">
                    <span class="text-slate-400">Time Left</span>
                    <span>${node.d}</span>
                </div>
            </div>
        `).join('');

        // Sync History & Balance
        const userUID = localStorage.getItem('nexus_uid');
        if(userUID) {
            onValue(ref(db, `users/${userUID}`), (snap) => {
                const data = snap.val();
                if(data) {
                    document.getElementById('balance-val').innerText = '$' + (data.balance || 0).toLocaleString();
                    
                    // History Logic
                    const hRows = document.getElementById('history-rows');
                    if(data.history) {
                        hRows.innerHTML = data.history.map(tx => `
                            <tr class="border-b border-slate-50">
                                <td class="py-4 text-slate-400 text-[10px]">${tx.date}</td>
                                <td class="py-4 uppercase text-[10px]">${tx.type}</td>
                                <td class="py-4">$${tx.amt}</td>
                                <td class="py-4"><span class="status-${tx.status.toLowerCase()}">${tx.status}</span></td>
                            </tr>
                        `).join('');
                    } else {
                        hRows.innerHTML = `<tr><td colspan="4" class="py-10 text-center text-slate-300 uppercase text-[9px]">No transactions detected</td></tr>`;
                    }
                }
            });
        }

        // Countdown Timer Animation
        function startTimer() {
            let h=23, m=59, s=59;
            setInterval(() => {
                s--;
                if(s<0) { s=59; m--; }
                if(m<0) { m=59; h--; }
                document.getElementById('countdown').innerText = `SYNC: ${h}:${m}:${s}`;
            }, 1000);
        }
        startTimer();
    </script>
</body>
</html>
