<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Ultimate Mining Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --bg-dark: #010204; --bg-light: #f8fafc; }
        body.dark-mode { background-color: var(--bg-dark); color: #ffffff; }
        body.light-mode { background-color: var(--bg-light); color: #0f172a; }
        
        .glass-panel { backdrop-filter: blur(40px); border: 1px solid rgba(128,128,128,0.1); }
        .dark-mode .glass-panel { background: rgba(15, 18, 23, 0.85); }
        .light-mode .glass-panel { background: rgba(255, 255, 255, 0.85); }

        /* Scanning Visual */
        #scanner { position: fixed; top: 0; left: 0; width: 100%; height: 2px; background: var(--gold); box-shadow: 0 0 15px var(--gold); z-index: 1000; animation: scan 4s infinite; pointer-events: none; }
        @keyframes scan { 0%, 100% { top: 0%; } 50% { top: 100%; } }

        /* Ticker Animation */
        .ticker-wrap { background: rgba(0,0,0,0.4); border-bottom: 1px solid rgba(255,255,255,0.05); overflow: hidden; }
        .ticker-move { display: flex; animation: ticker 40s linear infinite; }
        @keyframes ticker { 0% { transform: translateX(0); } 100% { transform: translateX(-50%); } }

        .crypto-text { background: linear-gradient(90deg, #f3ba2f, #ffffff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .node-card { transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); border-radius: 40px; }
        .node-card:hover { transform: translateY(-10px); border-color: var(--gold); }
        .hidden-section { display: none; }
        input, select { background: rgba(0,0,0,0.2) !important; border: 1px solid rgba(255,255,255,0.1) !important; color: inherit; border-radius: 15px; }
        
        .status-dot { width: 8px; height: 8px; background: #10b981; border-radius: 50%; box-shadow: 0 0 10px #10b981; animation: blink 2s infinite; }
        @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }
    </style>
</head>
<body class="dark-mode transition-colors duration-500">

    <div id="scanner"></div>

    <div class="ticker-wrap py-2">
        <div class="ticker-move gap-12 whitespace-nowrap text-[9px] font-black tracking-widest uppercase opacity-60">
            <span>BTC/USDT: $68,432 <span class="text-green-500">▲ 2.1%</span></span>
            <span>ETH/USDT: $3,521 <span class="text-red-500">▼ 0.4%</span></span>
            <span>BNB/USDT: $602 <span class="text-green-500">▲ 1.5%</span></span>
            <span>USDT/TRX: 14.25 <span class="text-gray-400">0.0%</span></span>
            <span>SOL/USDT: $148 <span class="text-green-500">▲ 4.8%</span></span>
            <span>BTC/USDT: $68,432 <span class="text-green-500">▲ 2.1%</span></span>
            <span>ETH/USDT: $3,521 <span class="text-red-500">▼ 0.4%</span></span>
        </div>
    </div>

    <nav class="glass-panel sticky top-0 z-[200] px-8 py-5 flex items-center justify-between">
        <div class="flex items-center gap-4 cursor-pointer" id="master-logo">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl shadow-lg">N</div>
            <div>
                <h1 class="text-lg font-black tracking-tighter uppercase italic leading-none">Nexus<span class="crypto-text">Infinity</span></h1>
                <p class="text-[7px] font-bold text-gray-500 tracking-[0.4em] uppercase">Institutional Terminal</p>
            </div>
        </div>
        
        <div class="flex items-center gap-6">
            <div class="hidden md:flex items-center gap-2 px-4 py-1.5 bg-green-500/10 rounded-full">
                <div class="status-dot"></div>
                <span class="text-[8px] font-black text-green-500 uppercase tracking-widest">Mainnet Online</span>
            </div>
            <button onclick="toggleTheme()" class="text-lg hover:text-[#f3ba2f]"><i class="fa-solid fa-circle-half-stroke"></i></button>
        </div>
    </nav>

    <main class="container mx-auto px-6 py-10 space-y-12">
        
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <div class="lg:col-span-2 glass-panel p-12 rounded-[50px] border-l-[12px] border-[#f3ba2f] relative overflow-hidden group">
                <div class="absolute right-[-20px] top-[-20px] opacity-[0.03] group-hover:opacity-[0.07] transition-opacity"><i class="fa-solid fa-shield-halved text-[250px]"></i></div>
                <p class="text-[10px] font-black text-gray-500 uppercase tracking-[0.5em] mb-6">Total Node Liquidity</p>
                <h2 id="balance-main" class="text-7xl md:text-8xl font-black italic tracking-tighter mb-12">$0.00</h2>
                <div class="flex flex-wrap gap-4">
                    <button onclick="openAction('deposit')" class="px-10 py-5 bg-[#f3ba2f] text-black font-black rounded-2xl text-[10px] uppercase shadow-2xl hover:scale-105 transition">Add Assets</button>
                    <button onclick="openAction('withdraw')" class="px-10 py-5 bg-white/5 border border-white/10 font-black rounded-2xl text-[10px] uppercase hover:bg-white/10 transition">Withdraw</button>
                </div>
            </div>

            <div class="glass-panel p-10 rounded-[50px] flex flex-col justify-between">
                <div class="space-y-6">
                    <p class="text-[9px] font-black text-gray-500 uppercase tracking-widest">System Health</p>
                    <div id="sys-logs" class="font-mono text-[9px] text-green-500 space-y-2 opacity-60">
                        <div>> INITIALIZING QUANTUM...</div>
                        <div>> SYNCING WITH MAINNET...</div>
                        <div>> SECURITY_LAYER: ACTIVE</div>
                    </div>
                </div>
                <div class="mt-8 pt-8 border-t border-white/5">
                    <p class="text-[9px] font-black text-gray-500 uppercase mb-2">Network Latency</p>
                    <p class="text-xl font-black italic">1.24ms <span class="text-[8px] text-blue-400">OPTIMIZED</span></p>
                </div>
            </div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="nodes-grid"></div>

    </main>

    <div id="action-portal" class="fixed inset-0 z-[500] bg-black/95 backdrop-blur-3xl hidden flex items-center justify-center p-6">
        <div class="glass-panel w-full max-w-lg rounded-[60px] p-12 relative">
            <button onclick="closeAction()" class="absolute top-8 right-10 text-4xl opacity-50">&times;</button>
            
            <div id="dep-ui" class="hidden">
                <h3 class="text-3xl font-black italic mb-8 uppercase">Gateway</h3>
                <select id="net-sel" onchange="updateWallet()" class="w-full p-4 mb-6 text-xs font-bold">
                    <option value="TRC20">USDT (TRC20) - Fast</option>
                    <option value="ERC20">ETH (ERC20) - Secure</option>
                    <option value="BEP20">BNB (BEP20) - Smart Chain</option>
                </select>
                <div class="bg-yellow-500/5 p-6 rounded-3xl border border-yellow-500/20 mb-8 text-center">
                    <p class="text-[9px] font-black text-yellow-500 mb-2 uppercase">Official Receiving Address:</p>
                    <p id="wallet-addr" class="text-xs font-mono font-black break-all text-white">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount (USD)" class="w-full p-4 mb-4 text-xs font-black">
                <input type="text" id="dep-hash" placeholder="Transaction Hash ID" class="w-full p-4 mb-8 text-xs font-mono uppercase">
                <button onclick="submitDeposit()" class="w-full bg-[#f3ba2f] text-black font-black py-5 rounded-2xl shadow-xl uppercase text-xs tracking-widest">Verify Payout</button>
            </div>

            <div id="wit-ui" class="hidden text-center">
                <h3 class="text-3xl font-black italic mb-8 uppercase text-red-500">Withdraw</h3>
                <input type="text" id="wit-addr" placeholder="Destination Address" class="w-full p-4 mb-4 text-xs font-mono">
                <input type="number" id="wit-amt" placeholder="0.00" class="w-full p-6 mb-10 text-4xl font-black text-center">
                <button onclick="submitWithdraw()" class="w-full bg-white text-black font-black py-5 rounded-2xl shadow-xl uppercase text-xs">Request Liquidation</button>
            </div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 z-[600] bg-black hidden overflow-y-auto p-12">
        <div class="max-w-4xl mx-auto">
            <div class="flex justify-between items-center mb-12">
                <h2 class="text-4xl font-black italic text-[#f3ba2f] uppercase">Nexus Admin Terminal</h2>
                <button onclick="location.reload()" class="text-4xl">&times;</button>
            </div>
            <div id="admin-users" class="space-y-4"></div>
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
            appId: "1:341970060013:web:67374c0fd262b63bd342e4"
        };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);
        let userUID = localStorage.getItem('nexus_uid');

        // --- NODES RENDER ---
        const nodes = [
            {n: "Cyber", l: "Dubai", m: 15, y: 1.5}, {n: "Aegis", l: "London", m: 50, y: 2.2},
            {n: "Vortex", l: "Tokyo", m: 100, y: 3.5}, {n: "Titan", l: "Zurich", m: 500, y: 5.5},
            {n: "Nebula", l: "Singapore", m: 1000, y: 8.0}, {n: "Nova", l: "Toronto", m: 2500, y: 10.5},
            {n: "Apex", l: "Sydney", m: 5000, y: 14.0}, {n: "Omega", l: "Satellite", m: 10000, y: 20.0}
        ];

        document.getElementById('nodes-grid').innerHTML = nodes.map(node => `
            <div class="node-card glass-panel p-8 border border-white/5">
                <p class="text-[8px] font-black text-[#f3ba2f] uppercase tracking-widest mb-1">${node.n} NODE</p>
                <h4 class="text-xl font-black italic uppercase mb-6">${node.l}</h4>
                <div class="space-y-2 mb-8 text-[10px]">
                    <div class="flex justify-between font-bold opacity-40"><span>MIN ENTRY</span><span>$${node.m}</span></div>
                    <div class="flex justify-between font-black text-green-500 uppercase"><span>DAILY YIELD</span><span>+${node.y}%</span></div>
                </div>
                <button onclick="openAction('deposit')" class="w-full py-4 bg-white/5 border border-white/10 rounded-xl text-[9px] font-black uppercase hover:bg-[#f3ba2f] hover:text-black transition">Deploy</button>
            </div>
        `).join('');

        // --- SYSTEM CORE ---
        window.openAction = (t) => {
            document.getElementById('action-portal').classList.remove('hidden');
            document.getElementById('dep-ui').classList.toggle('hidden', t !== 'deposit');
            document.getElementById('wit-ui').classList.toggle('hidden', t !== 'withdraw');
        };
        window.closeAction = () => document.getElementById('action-portal').classList.add('hidden');
        window.toggleTheme = () => document.body.classList.toggle('light-mode');

        window.updateWallet = () => {
            const net = document.getElementById('net-sel').value;
            const ga = document.getElementById('wallet-addr');
            if(net === 'TRC20') ga.innerText = "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ";
            else if(net === 'ERC20') ga.innerText = "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355";
            else ga.innerText = "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355";
        };

        window.submitDeposit = async () => {
            const amt = document.getElementById('dep-amt').value;
            const hash = document.getElementById('dep-hash').value;
            if(!amt || !hash) return alert("Sweetie, fill all fields!");
            const tx = { type: 'DEPOSIT', amt: amt, hash: hash, date: new Date().toLocaleString(), status: 'PENDING' };
            const snap = await get(ref(db, `users/${userUID}`));
            let h = snap.val().history || []; h.unshift(tx);
            await update(ref(db, `users/${userUID}`), { history: h });
            alert("Protocol Broadcasted! Admin will verify soon.");
            closeAction();
        };

        window.submitWithdraw = async () => {
            const amt = parseFloat(document.getElementById('wit-amt').value);
            const snap = await get(ref(db, `users/${userUID}`));
            if(!amt || amt > snap.val().balance) return alert("Insufficient Liquidity!");
            const tx = { type: 'WITHDRAW', amt: amt, date: new Date().toLocaleString(), status: 'PENDING' };
            let h = snap.val().history || []; h.unshift(tx);
            await update(ref(db, `users/${userUID}`), { history: h });
            alert("Withdrawal Authorized. Security check in progress.");
            closeAction();
        };

        // --- AUTH & DATA SYNC ---
        if(!userUID) {
            const email = prompt("Enter Institutional Email:");
            if(email) {
                userUID = email.replace(/[.#$[\]]/g, "_");
                localStorage.setItem('nexus_uid', userUID);
                set(ref(db, `users/${userUID}`), { email: email, balance: 0, history: [] });
                location.reload();
            }
        } else {
            onValue(ref(db, `users/${userUID}`), (snap) => {
                if(snap.exists()) {
                    document.getElementById('balance-main').innerText = '$' + snap.val().balance.toLocaleString(undefined, {minimumFractionDigits:2});
                }
            });
        }

        // --- SECRET ADMIN ---
        let taps = 0;
        document.getElementById('master-logo').onclick = () => {
            taps++;
            if(taps === 4) {
                if(prompt("Admin Key:") === "coin786") loadAdmin();
                taps = 0;
            }
            setTimeout(() => taps = 0, 3000);
        };

        window.loadAdmin = () => {
            document.getElementById('admin-panel').classList.remove('hidden');
            onValue(ref(db, 'users'), (snap) => {
                const data = snap.val(); let html = "";
                for(let id in data) {
                    html += `<div class="glass-panel p-8 rounded-[30px] flex justify-between items-center mb-4">
                        <div><p class="text-[10px] font-bold text-gray-500">${data[id].email}</p><h4 class="text-2xl font-black italic">$${data[id].balance.toLocaleString()}</h4></div>
                        <button onclick="modBal('${id}')" class="bg-[#f3ba2f] text-black px-6 py-3 rounded-xl text-[10px] font-black">Edit Bal</button>
                    </div>`;
                }
                document.getElementById('admin-users').innerHTML = html;
            });
        };
        window.modBal = (id) => {
            const val = prompt("New balance for " + id);
            if(val) update(ref(db, `users/${id}`), { balance: parseFloat(val) });
        };

        // Live logs animation
        setInterval(() => {
            const logs = document.getElementById('sys-logs');
            const lines = ["> BLOCK_9928_VERIFIED", "> SYNCING_NODES...", "> ENCRYPTING_TX...", "> PEER_CONNECTED"];
            const div = document.createElement('div');
            div.innerText = lines[Math.floor(Math.random()*lines.length)];
            logs.appendChild(div);
            if(logs.childNodes.length > 5) logs.removeChild(logs.firstChild);
        }, 3000);
    </script>
</body>
</html>
