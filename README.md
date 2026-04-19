<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS PRO | Enterprise Mining System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root { --gold: #f3ba2f; --bg: #010204; }
        body.dark-mode { background-color: var(--bg); color: #ffffff; }
        body.light-mode { background-color: #f1f5f9; color: #0f172a; }
        .glass { backdrop-filter: blur(30px); border: 1px solid rgba(128,128,128,0.1); }
        .dark-mode .glass { background: rgba(15, 18, 23, 0.9); }
        .light-mode .glass { background: rgba(255, 255, 255, 0.8); }
        .crypto-card { transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        .crypto-card:hover { transform: scale(1.05); box-shadow: 0 20px 50px rgba(0,0,0,0.3); }
        .ticker-wrap { overflow: hidden; background: rgba(0,0,0,0.3); border-bottom: 1px solid rgba(255,255,255,0.05); }
        .ticker-move { display: flex; animation: ticker 30s linear infinite; }
        @keyframes ticker { 0% { transform: translateX(0); } 100% { transform: translateX(-50%); } }
        .system-log { font-family: 'Courier New', monospace; font-size: 10px; color: #10b981; }
        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-thumb { background: var(--gold); }
    </style>
</head>
<body class="dark-mode transition-all duration-700">

    <div class="ticker-wrap py-2">
        <div class="ticker-move gap-10 whitespace-nowrap uppercase font-black text-[9px] tracking-widest opacity-60">
            <span>BTC/USDT: $64,231.40 <span class="text-green-500">+2.4%</span></span>
            <span>ETH/USDT: $3,452.12 <span class="text-red-500">-0.8%</span></span>
            <span>BNB/USDT: $592.10 <span class="text-green-500">+1.2%</span></span>
            <span>SOL/USDT: $145.50 <span class="text-green-500">+5.6%</span></span>
            <span>XRP/USDT: $0.62 <span class="text-gray-400">0.0%</span></span>
            <span>BTC/USDT: $64,231.40 <span class="text-green-500">+2.4%</span></span>
            <span>ETH/USDT: $3,452.12 <span class="text-red-500">-0.8%</span></span>
        </div>
    </div>

    <nav class="glass sticky top-0 z-[100] px-8 py-4 flex items-center justify-between">
        <div class="flex items-center gap-4 cursor-pointer" id="master-logo">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black shadow-[0_0_15px_rgba(243,186,47,0.3)]">N</div>
            <h1 class="text-lg font-black tracking-tighter italic uppercase">Nexus<span class="text-[#f3ba2f]">Pro</span></h1>
        </div>
        <div class="flex items-center gap-6">
            <div class="hidden md:flex gap-4 text-[9px] font-bold opacity-40 uppercase tracking-widest">
                <span>CPU: 14%</span>
                <span>RAM: 32%</span>
                <span>SEC: AES-256</span>
            </div>
            <button onclick="toggleTheme()" class="w-8 h-8 rounded-full hover:bg-white/10 transition"><i class="fa-solid fa-moon"></i></button>
        </div>
    </nav>

    <main class="container mx-auto px-6 py-10">
        
        <div class="grid grid-cols-1 lg:grid-cols-4 gap-6 mb-12">
            <div class="lg:col-span-2 glass p-10 rounded-[40px] border-b-4 border-[#f3ba2f] relative overflow-hidden">
                <div class="absolute -right-10 -top-10 opacity-5"><i class="fa-solid fa-wallet text-[200px]"></i></div>
                <p class="text-[10px] font-black text-gray-500 uppercase tracking-widest mb-4">Total Liquidity Pool</p>
                <h2 id="balance-display" class="text-6xl font-black italic tracking-tighter mb-10">$0.00</h2>
                <div class="flex gap-4">
                    <button onclick="openPortal('deposit')" class="flex-1 bg-[#f3ba2f] text-black py-4 rounded-2xl font-black text-[10px] uppercase shadow-xl hover:brightness-110">Add Assets</button>
                    <button onclick="openPortal('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-4 rounded-2xl font-black text-[10px] uppercase hover:bg-white/10">Liquidate</button>
                </div>
            </div>
            
            <div class="glass p-8 rounded-[40px] flex flex-col justify-between">
                <p class="text-[9px] font-black text-gray-500 uppercase mb-4 tracking-widest">Wallet Distribution</p>
                <div class="space-y-4">
                    <div class="flex justify-between items-center"><span class="text-[10px] font-bold">BTC Wallet</span><span class="text-xs font-mono">0.00000</span></div>
                    <div class="flex justify-between items-center"><span class="text-[10px] font-bold">ETH Wallet</span><span class="text-xs font-mono">0.00000</span></div>
                    <div class="flex justify-between items-center"><span class="text-[10px] font-bold">USDT Node</span><span id="usdt-bal" class="text-xs font-mono">$0.00</span></div>
                </div>
                <div class="h-1 bg-white/5 rounded-full mt-4"><div class="w-1/3 h-full bg-[#f3ba2f] rounded-full"></div></div>
            </div>

            <div class="glass p-8 rounded-[40px] relative">
                <p class="text-[9px] font-black text-gray-500 uppercase mb-4 tracking-widest">Mining Pulse</p>
                <canvas id="hashChart" class="w-full h-32"></canvas>
            </div>
        </div>

        <div class="glass p-6 rounded-[30px] mb-12 overflow-hidden">
            <div class="flex items-center gap-2 mb-4">
                <div class="w-2 h-2 bg-green-500 rounded-full animate-ping"></div>
                <p class="text-[10px] font-black uppercase tracking-tighter">Live Security Console</p>
            </div>
            <div id="system-logs" class="system-log h-20 overflow-y-hidden space-y-1">
                <div>[INFO] Initializing Quantum Encryption...</div>
                <div>[INFO] Peer 192.168.1.1 connected to Node-Alpha</div>
                <div>[SEC] Hash verification successful.</div>
            </div>
        </div>

        <h3 class="text-sm font-black italic uppercase mb-8 tracking-[0.5em] text-gray-500 text-center">Global Node Clusters</h3>
        <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-4 gap-6" id="node-grid">
            </div>

    </main>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // Firebase Setup
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

        // Chart Logic
        const ctx = document.getElementById('hashChart').getContext('2d');
        const hashChart = new Chart(ctx, {
            type: 'line',
            data: {
                labels: ['', '', '', '', '', ''],
                datasets: [{
                    data: [12, 19, 15, 25, 22, 30],
                    borderColor: '#f3ba2f',
                    borderWidth: 2,
                    tension: 0.4,
                    pointRadius: 0
                }]
            },
            options: { plugins: { legend: { display: false } }, scales: { x: { display: false }, y: { display: false } } }
        });

        // Fake Logs Logic
        const logBox = document.getElementById('system-logs');
        const messages = [
            "[SEC] Encrypting transaction packet...",
            "[NET] Relay found in Singapore Node",
            "[DB] Balance synced with Mainnet",
            "[INFO] Block #992831 confirmed",
            "[AUTH] Session key refreshed"
        ];
        setInterval(() => {
            const div = document.createElement('div');
            div.innerText = messages[Math.floor(Math.random()*messages.length)];
            logBox.appendChild(div);
            if(logBox.childNodes.length > 6) logBox.removeChild(logBox.firstChild);
        }, 3000);

        // Render Nodes
        const nodes = [
            {n: "Alpha", l: "Dubai", m: 15, y: 1.5},
            {n: "Beta", l: "London", m: 50, y: 2.2},
            {n: "Gamma", l: "Zurich", m: 100, y: 3.5},
            {n: "Delta", l: "Tokyo", m: 500, y: 5.0}
        ];
        document.getElementById('node-grid').innerHTML = nodes.map(node => `
            <div class="crypto-card glass p-8 rounded-[35px] border border-white/5">
                <div class="flex justify-between items-center mb-6">
                    <span class="text-[9px] font-black text-[#f3ba2f] uppercase tracking-widest">${node.n} Cluster</span>
                    <i class="fa-solid fa-bolt-lightning text-yellow-500"></i>
                </div>
                <h4 class="text-xl font-black italic uppercase">${node.l}</h4>
                <div class="mt-4 space-y-2 mb-8">
                    <div class="flex justify-between text-[10px] opacity-40"><span>Entry</span><span>$${node.m}</span></div>
                    <div class="flex justify-between text-[10px] font-black text-green-500"><span>Daily</span><span>+${node.y}%</span></div>
                </div>
                <button class="w-full py-3 bg-white/5 rounded-xl text-[9px] font-black uppercase hover:bg-[#f3ba2f] hover:text-black transition">Deploy Node</button>
            </div>
        `).join('');

        window.toggleTheme = () => {
            document.body.classList.toggle('dark-mode');
            document.body.classList.toggle('light-mode');
        };
    </script>
</body>
</html>
