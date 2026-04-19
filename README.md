<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Quantum Mining Network</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --bg: #010204; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; transition: 0.5s; }
        .glass { background: rgba(15, 18, 23, 0.8); backdrop-filter: blur(25px); border: 1px solid rgba(255,255,255,0.05); }
        .neon-border { border: 1px solid rgba(243, 186, 47, 0.2); box-shadow: 0 0 15px rgba(243, 186, 47, 0.05); }
        .crypto-text { background: linear-gradient(90deg, #f3ba2f, #ffffff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        
        /* Floating Chat Bot */
        .chat-bot { position: fixed; bottom: 30px; right: 30px; width: 60px; height: 60px; background: var(--gold); border-radius: 50%; display: flex; items-center; justify-center; cursor: pointer; box-shadow: 0 10px 30px rgba(243, 186, 47, 0.4); z-index: 1000; animation: bounce 2s infinite; }
        
        /* Security Meter */
        .meter { height: 6px; border-radius: 10px; background: #1e293b; overflow: hidden; }
        .meter-fill { height: 100%; width: 65%; background: linear-gradient(90deg, #ef4444, #f3ba2f, #22c55e); }

        /* Referral Card */
        .referral-box { background: linear-gradient(135deg, rgba(243, 186, 47, 0.1) 0%, rgba(0,0,0,0) 100%); }
        
        @keyframes bounce { 0%, 100% { transform: translateY(0); } 50% { transform: translateY(-10px); } }
        .hidden-section { display: none; }
    </style>
</head>
<body class="dark-mode">

    <header class="glass sticky top-0 z-[100] border-b border-white/5 px-8 py-4 flex items-center justify-between">
        <div class="flex items-center gap-4 cursor-pointer" id="master-logo">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl shadow-lg">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="crypto-text">Infinity</span></span>
        </div>
        
        <div class="flex items-center gap-6">
            <select class="bg-transparent text-[10px] font-bold uppercase tracking-widest outline-none cursor-pointer border-none">
                <option class="bg-black">English</option>
                <option class="bg-black">العربية</option>
                <option class="bg-black">Urdu</option>
            </select>
            <div onclick="toggleTheme()" class="cursor-pointer opacity-60 hover:opacity-100 transition"><i class="fa-solid fa-circle-half-stroke"></i></div>
        </div>
    </header>

    <main class="container mx-auto px-6 py-10 space-y-10">

        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <div class="glass p-6 rounded-3xl neon-border">
                <p class="text-[9px] font-black text-gray-500 uppercase mb-2">Account Security Score</p>
                <div class="flex justify-between items-center mb-2">
                    <span class="text-xs font-bold text-yellow-500">65% (Medium)</span>
                    <i class="fa-solid fa-shield-halved text-yellow-500"></i>
                </div>
                <div class="meter"><div class="meter-fill"></div></div>
            </div>
            <div class="glass p-6 rounded-3xl neon-border">
                <p class="text-[9px] font-black text-gray-500 uppercase mb-2">Active Network Peers</p>
                <p class="text-xl font-black italic">14,293 <span class="text-[10px] text-green-500 ml-2">+12%</span></p>
            </div>
            <div class="glass p-6 rounded-3xl neon-border">
                <p class="text-[9px] font-black text-gray-500 uppercase mb-2">Global Market Cap</p>
                <p class="text-xl font-black italic text-[#f3ba2f]">$2.4T <i class="fa-solid fa-chart-line ml-2"></i></p>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <div class="lg:col-span-2 glass p-10 rounded-[50px] relative overflow-hidden">
                <p class="text-xs font-black text-gray-500 uppercase tracking-widest mb-4">Total Assets Balance</p>
                <h2 id="main-balance" class="text-7xl font-black italic tracking-tighter mb-10">$0.00</h2>
                <div class="flex gap-4">
                    <button onclick="openAction('deposit')" class="flex-1 bg-[#f3ba2f] text-black py-4 rounded-2xl font-black text-[11px] uppercase shadow-2xl hover:scale-[1.02] transition">Quick Deposit</button>
                    <button onclick="openAction('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-4 rounded-2xl font-black text-[11px] uppercase hover:bg-white/10">Liquidate Funds</button>
                </div>
            </div>
            
            <div class="glass p-8 rounded-[40px] referral-box border-2 border-[#f3ba2f]/10">
                <h4 class="text-sm font-black italic uppercase mb-6">Affiliate Hub</h4>
                <div class="space-y-4">
                    <div class="bg-black/40 p-4 rounded-2xl">
                        <p class="text-[9px] text-gray-500 uppercase mb-1">Your Referral Link</p>
                        <p class="text-[10px] font-mono truncate text-blue-400">nexus-infinity.io/ref=786x</p>
                    </div>
                    <div class="grid grid-cols-2 gap-4">
                        <div class="text-center"><p class="text-[8px] text-gray-500 uppercase">Invited</p><p class="font-black italic">12</p></div>
                        <div class="text-center"><p class="text-[8px] text-gray-500 uppercase">Earned</p><p class="font-black italic text-green-500">$142.00</p></div>
                    </div>
                    <button class="w-full py-3 bg-white/5 rounded-xl text-[9px] font-black uppercase tracking-widest hover:bg-[#f3ba2f] hover:text-black transition">Copy Link</button>
                </div>
            </div>
        </div>

        <div class="glass p-10 rounded-[50px] text-center border border-white/5">
            <h3 class="text-xs font-black uppercase tracking-[0.4em] mb-8 text-gray-500">Live Global Node Activity</h3>
            <div class="relative h-64 bg-slate-900/50 rounded-3xl overflow-hidden flex items-center justify-center">
                <i class="fa-solid fa-earth-americas text-9xl opacity-10 absolute"></i>
                <div class="relative z-10 space-y-2">
                    <div class="flex items-center gap-3 text-xs font-bold text-green-500"><div class="w-2 h-2 bg-green-500 rounded-full animate-ping"></div> Singapore Cluster: Active</div>
                    <div class="flex items-center gap-3 text-xs font-bold text-[#f3ba2f]"><div class="w-2 h-2 bg-[#f3ba2f] rounded-full animate-ping"></div> Dubai Cluster: Verifying...</div>
                    <div class="flex items-center gap-3 text-xs font-bold text-blue-500"><div class="w-2 h-2 bg-blue-500 rounded-full animate-ping"></div> USA Cluster: Processing</div>
                </div>
            </div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="nodes-container"></div>

    </main>

    <div class="chat-bot" onclick="toggleChat()">
        <i class="fa-solid fa-headset text-black text-2xl"></i>
    </div>

    <div id="chat-window" class="fixed bottom-28 right-8 w-80 glass rounded-[30px] p-6 hidden z-[1000] border-2 border-[#f3ba2f]/20">
        <div class="flex justify-between items-center mb-4">
            <h5 class="text-[10px] font-black uppercase italic">Nexus Sweetie Bot</h5>
            <button onclick="toggleChat()">&times;</button>
        </div>
        <div class="h-48 overflow-y-auto text-[10px] space-y-3 mb-4 pr-2 italic">
            <div class="bg-white/5 p-3 rounded-2xl rounded-tl-none">Hello sweetie! How can I help you with your mining nodes today?</div>
        </div>
        <div class="flex gap-2">
            <input type="text" placeholder="Type..." class="flex-1 bg-black/40 border border-white/10 rounded-xl p-3 text-[10px]">
            <button class="bg-[#f3ba2f] text-black px-4 rounded-xl"><i class="fa-solid fa-paper-plane"></i></button>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, onValue, update } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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
        const userId = localStorage.getItem('nexus_uid');

        // Render Nodes
        const nodes = [
            {n: "Vortex", l: "Singapore", m: 15, y: 1.5},
            {n: "Titan", l: "Dubai", m: 100, y: 3.5},
            {n: "Quantum", l: "Zurich", m: 1000, y: 7.2},
            {n: "Apex", l: "Sat-X", m: 10000, y: 18.0}
        ];
        document.getElementById('nodes-container').innerHTML = nodes.map(node => `
            <div class="glass p-8 rounded-[40px] neon-border hover:scale-105 transition-all">
                <div class="flex justify-between items-start mb-6">
                    <p class="text-[8px] font-black text-[#f3ba2f] uppercase tracking-widest">${node.n} NODE</p>
                    <i class="fa-solid fa-microchip text-gray-600"></i>
                </div>
                <h4 class="text-xl font-black italic uppercase">${node.l}</h4>
                <div class="my-6 space-y-2">
                    <div class="flex justify-between text-[9px] opacity-40"><span>MIN ENTRY</span><span>$${node.m}</span></div>
                    <div class="flex justify-between text-[9px] font-bold text-green-500"><span>DAILY YIELD</span><span>+${node.y}%</span></div>
                </div>
                <button class="w-full py-4 bg-white/5 rounded-2xl text-[9px] font-black uppercase hover:bg-[#f3ba2f] hover:text-black transition">Deploy</button>
            </div>
        `).join('');

        // Sync Balance
        if(userId) {
            onValue(ref(db, `users/${userId}`), (snap) => {
                if(snap.exists()) {
                    document.getElementById('main-balance').innerText = '$' + snap.val().balance.toLocaleString(undefined, {minimumFractionDigits:2});
                }
            });
        }

        window.toggleChat = () => document.getElementById('chat-window').classList.toggle('hidden');
        window.toggleTheme = () => document.body.classList.toggle('light-mode');
    </script>
</body>
</html>
