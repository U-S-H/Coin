<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        :root { --gold: #f3ba2f; --bg: #ffffff; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: var(--bg); color: #0f172a; margin: 0; overflow-x: hidden; }

        .glass-card { background: #fff; border: 1px solid rgba(0,0,0,0.05); border-radius: 28px; box-shadow: 0 10px 40px rgba(0,0,0,0.01); }
        .input-pro { background: #f8fafc; border: 2px solid transparent; border-radius: 18px; padding: 16px; width: 100%; font-weight: 700; outline: none; }
        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 900; padding: 18px; border-radius: 20px; width: 100%; text-transform: uppercase; letter-spacing: 1px; border: none; cursor: pointer; }
        
        .node-card { background: #fff; border: 1.5px solid #f1f5f9; border-radius: 24px; padding: 20px; transition: 0.3s; }
        .node-card:hover { border-color: var(--gold); transform: translateY(-5px); }

        .nav-item { cursor: pointer; font-size: 10px; font-weight: 800; color: #94a3b8; text-align: center; }
        .nav-item.active { color: #000; }
        .hidden { display: none !important; }
        
        .status-pending { background: #fef9c3; color: #a16207; }
        .status-approved { background: #dcfce7; color: #15803d; }
        .badge { padding: 4px 10px; border-radius: 100px; font-size: 8px; font-weight: 800; text-transform: uppercase; }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-16 h-16 bg-white text-black rounded-2xl flex items-center justify-center text-3xl font-black mb-4">N</div>
        <h1 class="text-white font-black italic text-xl uppercase tracking-widest">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="w-full max-w-sm space-y-10 text-center">
            <h2 class="text-3xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Username" class="input-pro text-center">
                <input type="password" id="l-pass" placeholder="Password" class="input-pro text-center">
                <button onclick="handleLogin()" class="btn-gold w-full">Authorize</button>
                <p onclick="toggleAuth(true)" class="text-[10px] font-black uppercase underline mt-4">Register New Node</p>
            </div>
            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Username" class="input-pro text-center">
                <input type="password" id="s-pass" placeholder="Password" class="input-pro text-center">
                <button onclick="handleSignup()" class="btn-gold w-full">Initialize</button>
                <p onclick="toggleAuth(false)" class="text-[10px] font-black uppercase underline mt-4">Back to Login</p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-28">
        <nav class="sticky top-0 bg-white/80 backdrop-blur-xl border-b p-5 flex justify-between items-center z-[500]">
            <div class="flex items-center gap-2">
                <div class="w-8 h-8 bg-black text-white rounded-lg flex items-center justify-center font-black text-xs">N</div>
                <span id="nav-user" class="font-black italic uppercase text-sm">USER</span>
            </div>
            <button onclick="logout()" class="text-slate-300"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-card p-10 bg-slate-900 text-white relative overflow-hidden">
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mb-2">Available Balance</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 flex justify-between">
                    <div><p class="text-[8px] font-black text-slate-500 uppercase">Total Profit</p><p id="profit-txt" class="text-lg font-black text-green-400">+$0.00</p></div>
                    <div class="text-right"><p class="text-[8px] font-black text-slate-500 uppercase">Sync Status</p><p class="text-xs font-black text-[#f3ba2f] italic">Active Node</p></div>
                </div>
            </div>

            <h3 class="font-black uppercase text-[10px] tracking-widest text-slate-400">Your Active Yields</h3>
            <div id="active-investments" class="space-y-4">
                <p class="text-center text-[10px] text-slate-300 py-4 italic">No active nodes found...</p>
            </div>
        </div>

        <div id="page-nodes" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Institutional Nodes</h3>
            <div id="nodes-grid" class="grid grid-cols-1 gap-4">
                </div>
        </div>

        <div id="page-history" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Transaction Ledger</h3>
            <div id="history-list" class="space-y-3"></div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-white border-t p-5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-house block text-lg mb-1"></i>Home</div>
            <div onclick="switchPage('nodes')" class="nav-item"><i class="fa-solid fa-server block text-lg mb-1"></i>Nodes</div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-receipt block text-lg mb-1"></i>Ledger</div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

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

        // NODE CONFIGURATION (15 Nodes)
        const nodesData = Array.from({length: 15}, (_, i) => ({
            id: i + 1,
            name: `Nexus Node-0${i+1}`,
            price: (i + 1) * 50, // 50, 100, 150...
            daily: ((i + 1) * 2.5).toFixed(2),
            days: 30
        }));

        window.onload = () => {
            renderNodes();
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const user = localStorage.getItem('nexus_user');
                if(user) showDashboard(user);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2000);
        };

        function renderNodes() {
            const container = document.getElementById('nodes-grid');
            container.innerHTML = nodesData.map(n => `
                <div class="node-card glass-card flex justify-between items-center">
                    <div>
                        <p class="text-[10px] font-black uppercase text-slate-400">${n.name}</p>
                        <h4 class="text-lg font-black italic">$${n.price}</h4>
                        <p class="text-[9px] font-bold text-green-500">Daily: $${n.daily} | ${n.days} Days</p>
                    </div>
                    <button onclick="buyNode(${n.id})" class="bg-black text-white px-6 py-3 rounded-xl text-[9px] font-black uppercase">Activate</button>
                </div>
            `).join('');
        }

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user');
            const node = nodesData.find(n => n.id === id);
            const snap = await get(ref(db, `users/${user}`));
            const balance = snap.val().balance || 0;

            if(balance < node.price) return alert("Insufficient Capital, sweetie!");

            const newBalance = balance - node.price;
            await set(ref(db, `users/${user}/balance`), newBalance);
            
            const invRef = push(ref(db, `users/${user}/investments`));
            await set(invRef, {
                ...node,
                startTime: Date.now(),
                status: 'active'
            });
            alert(`${node.name} Activated!`);
            switchPage('home');
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val();
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0);
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0);
                
                if(data.investments) {
                    let invHtml = "";
                    Object.values(data.investments).forEach(inv => {
                        const elapsed = Math.floor((Date.now() - inv.startTime) / 1000);
                        const remaining = (inv.days * 86400) - elapsed;
                        invHtml += `
                            <div class="glass-card p-5">
                                <div class="flex justify-between items-start mb-4">
                                    <p class="text-[9px] font-black uppercase">${inv.name}</p>
                                    <span class="badge status-approved">Yielding</span>
                                </div>
                                <div class="flex justify-between">
                                    <p class="text-[8px] font-black text-slate-400">REMAINING TIME</p>
                                    <p class="text-xs font-black italic text-[#f3ba2f]">${Math.max(0, Math.floor(remaining/3600))}h Left</p>
                                </div>
                            </div>
                        `;
                    });
                    document.getElementById('active-investments').innerHTML = invHtml;
                }
            });
        }

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Fill details!");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 100, profit: 0 }); // Free $100 for testing
            alert("Node ID Created!"); toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) {
                localStorage.setItem('nexus_user', u);
                showDashboard(u);
            } else alert("Invalid ID!");
        };

        window.switchPage = (p) => {
            ['home', 'nodes', 'history'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
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
