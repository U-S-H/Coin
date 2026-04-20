<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Complete Ecosystem</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        body { background: #f8fafc; color: #000; font-family: 'Plus Jakarta Sans', sans-serif; }
        p, h1, h2, h3, h4, span, b { color: #000 !important; font-weight: 700; }
        .text-white { color: #fff !important; }
        .glass-card { background: #fff !important; border-radius: 30px; border: 1px solid #e2e8f0; box-shadow: 0 10px 30px rgba(0,0,0,0.05); }
        .mining-card { background: #0f172a !important; border-radius: 35px; position: relative; overflow: hidden; }
        .node-card { background: #fff !important; border-radius: 30px; border: 1px solid #e2e8f0; overflow: hidden; display: flex; flex-direction: column; margin-bottom: 25px; text-align: center; }
        .node-img { width: 100%; height: 180px; object-fit: cover; }
        .btn-center { background: #2563eb !important; color: #fff !important; padding: 16px; border-radius: 20px; font-size: 11px; font-weight: 800; text-transform: uppercase; width: 80%; margin: 0 auto 25px auto; display: block; }
        nav { background: #fff !important; border-top: 1px solid #e2e8f0; height: 85px; }
        .nav-link { color: #94a3b8 !important; font-size: 9px; font-weight: 800; text-align: center; }
        .nav-link.active { color: #2563eb !important; }
        .input-prime { background: #f1f5f9 !important; color: #000 !important; border: 2px solid #e2e8f0 !important; border-radius: 18px; padding: 15px; width: 100%; }
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 99999; display: flex; align-items: center; justify-content: center; }
    </style>
</head>
<body>

    <div id="preloader"><div class="w-10 h-10 border-4 border-blue-600 border-t-transparent rounded-full animate-spin"></div></div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="w-full max-w-sm space-y-8">
            <div class="text-center"><h1 class="text-5xl font-black italic">NEXUS<span class="text-blue-600">.</span></h1></div>
            <div id="login-box" class="glass-card p-8 space-y-5">
                <input type="text" id="l-user" placeholder="Account ID" class="input-prime">
                <input type="password" id="l-pass" placeholder="Security PIN" class="input-prime">
                <button onclick="login()" class="btn-center !w-full !m-0 !bg-black">Access Terminal</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] text-blue-600 uppercase cursor-pointer">Create Account</p>
            </div>
            <div id="signup-box" class="glass-card p-8 space-y-5 hidden">
                <input type="text" id="s-user" placeholder="Choose ID" class="input-prime">
                <input type="password" id="s-pass" placeholder="Create PIN" class="input-prime">
                <button onclick="signup()" class="btn-center !w-full !m-0 !bg-black">Register</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-slate-400 uppercase cursor-pointer">Back</p>
            </div>
        </div>
    </div>

    <div id="main-view" class="hidden pb-32">
        <header class="p-5 bg-white sticky top-0 z-50 border-b flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div id="logo-trigger" class="w-12 h-12 bg-black text-white rounded-2xl flex items-center justify-center font-black">N</div>
                <div><p id="display-name" class="text-xs uppercase">---</p><span id="kyc-badge" class="text-[8px] px-2 py-0.5 rounded bg-amber-100">PENDING</span></div>
            </div>
            <button onclick="logout()" class="w-10 h-10 bg-slate-100 rounded-xl flex items-center justify-center text-slate-400"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="tab-home" class="p-6 space-y-6">
            <div class="mining-card p-8 text-white">
                <p class="text-[9px] text-slate-400 uppercase tracking-widest">Total Liquidity</p>
                <h2 id="ui-bal" class="text-4xl font-black mt-2 text-white !important">$0.00</h2>
                <div class="h-20 mt-4"><canvas id="hashChart"></canvas></div>
                <div class="mt-6 pt-6 border-t border-white/10 flex justify-between">
                    <div><p class="text-[8px] text-slate-500 uppercase">Yield</p><p id="ui-prof" class="text-lg text-emerald-400">+$0.00</p></div>
                    <div class="text-right"><p class="text-[8px] text-slate-500 uppercase">Shield</p><p id="anti-phish" class="text-xs text-blue-400">NX-0000</p></div>
                </div>
            </div>

            <div class="grid grid-cols-2 gap-3">
                <button onclick="nav('legal')" class="bg-white p-4 rounded-2xl text-[9px] uppercase border shadow-sm">About Company</button>
                <button onclick="nav('legal')" class="bg-white p-4 rounded-2xl text-[9px] uppercase border shadow-sm">Privacy Policy</button>
            </div>

            <h3 class="text-[10px] text-slate-400 uppercase tracking-[4px] ml-1">My Node History</h3>
            <div id="active-list" class="space-y-3"></div>
        </main>

        <main id="tab-nodes" class="p-6 hidden">
            <h3 class="text-lg font-black uppercase mb-6">Cloud Infrastructure</h3>
            <div id="nodes-container" class="space-y-6"></div>
        </main>

        <main id="tab-vault" class="p-6 space-y-6 hidden">
            <div class="glass-card p-6 space-y-4">
                <h3 class="text-xs text-blue-600 uppercase">Capital Deposit</h3>
                <select id="d-asset" class="input-prime" onchange="updAddr()"><option value="">Select Asset</option><option value="TRX">TRX (Tron)</option><option value="USDT">USDT (TRC20)</option></select>
                <div id="d-panel" class="hidden space-y-4">
                    <p id="addr-txt" class="text-[9px] font-mono text-blue-600 p-4 bg-blue-50 rounded-xl break-all text-center"></p>
                    <input type="number" id="d-amt" placeholder="Amount ($)" class="input-prime">
                    <input type="text" placeholder="Transaction Hash" class="input-prime">
                    <button onclick="alert('Audit Sent')" class="btn-center !w-full !m-0 !bg-black">Submit Audit</button>
                </div>
            </div>
            <div class="glass-card p-6 space-y-4 border-t-8 border-black">
                <h3 class="text-xs text-slate-500 uppercase">Profit Withdrawal</h3>
                <input type="number" placeholder="Amount ($)" class="input-prime">
                <input type="text" placeholder="Wallet Address" class="input-prime">
                <button onclick="alert('Processing...')" class="btn-center !w-full !m-0">Request Payout</button>
            </div>
        </main>

        <main id="tab-legal" class="p-6 hidden space-y-8">
            <div><h4 class="text-blue-600 text-xs mb-2 uppercase">About Nexus Omni</h4><p class="text-xs text-slate-600 leading-loose">We provide institutional-grade cloud mining infrastructure since 2021. Our protocol ensures 99.9% uptime for digital asset generation.</p></div>
            <div><h4 class="text-blue-600 text-xs mb-2 uppercase">Privacy & Security</h4><p class="text-xs text-slate-600 leading-loose">All data is encrypted via AES-256 protocols. We do not share user identities with third-party auditors.</p></div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 flex justify-around items-center px-4 z-[1000]">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-home text-xl mb-1"></i><br>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-microchip text-xl mb-1"></i><br>NODES</div>
            <div onclick="nav('vault')" class="nav-link"><i class="fa-solid fa-vault text-xl mb-1"></i><br>VAULT</div>
            <div onclick="nav('legal')" class="nav-link"><i class="fa-solid fa-file-shield text-xl mb-1"></i><br>LEGAL</div>
        </nav>
    </div>

    <div id="adm-panel" class="fixed inset-0 bg-white z-[10001] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b pb-4"><h2 class="text-xl font-black text-blue-600">MASTER ADMIN</h2><button onclick="document.getElementById('adm-panel').classList.add('hidden')" class="text-2xl">&times;</button></div>
        <div id="adm-users" class="space-y-4"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        const nodeData = Array.from({length: 10}, (_, i) => ({ id: i, name: `Quantum Node v${i+1}`, price: 100+(i*400), yield: 15+(i*35), img: `https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400&q=80&sig=${i}` }));

        window.onload = () => {
            initChart(); renderNodes();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1000);
            if(localStorage.getItem('nx_usr')) startSession(localStorage.getItem('nx_usr'));
        };

        function initChart() {
            const ctx = document.getElementById('hashChart').getContext('2d');
            new Chart(ctx, { type: 'line', data: { labels: ['','','','','','',''], datasets: [{ data: [30, 55, 40, 75, 50, 90, 65], borderColor: '#3b82f6', tension: 0.4, borderWidth: 2, pointRadius: 0 }]}, options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false }}, scales: { x: { display: false }, y: { display: false }}}});
        }

        window.renderNodes = () => {
            document.getElementById('nodes-container').innerHTML = nodeData.map(n => `
                <div class="node-card">
                    <img src="${n.img}" class="node-img">
                    <div class="p-6">
                        <h4 class="uppercase text-sm mb-1">${n.name}</h4>
                        <p class="text-emerald-600 text-[10px] mb-4">Daily Yield: $${n.yield}</p>
                        <p class="text-2xl font-black mb-5">$${n.price}</p>
                        <button onclick="buy('${n.id}', ${n.price}, '${n.name}')" class="btn-center">Activate Node</button>
                    </div>
                </div>`).join('');
        };

        window.login = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Access Denied");
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
                document.getElementById('kyc-badge').innerText = d.kyc === 'Verified' ? 'VERIFIED' : 'PENDING';
                document.getElementById('kyc-badge').className = `text-[8px] px-2 py-0.5 rounded ${d.kyc === 'Verified' ? 'bg-emerald-100 text-emerald-700' : 'bg-amber-100 text-amber-700'}`;
                const nodes = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-list').innerHTML = nodes.map(([k, v]) => `<div class="glass-card p-4 flex justify-between items-center border-l-4 border-blue-600"><p class="text-[10px] uppercase">${v.name}</p><span class="text-[8px] text-slate-400">ACTIVE</span></div>`).join('') || '<p class="text-center text-[9px] text-slate-400 py-4 uppercase">No History Found</p>';
            });
        }

        window.buy = async (id, price, name) => {
            const uid = localStorage.getItem('nx_usr'), s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < price) return alert("Insufficient Balance");
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - price });
            await push(ref(db, `users/${uid}/nodes`), { name, time: Date.now() });
            alert("Deployment Successful!"); nav('home');
        };

        // ADMIN TRIGGER (4 Clicks on Logo)
        let taps = 0; document.getElementById('logo-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Key:") === "coin786") { document.getElementById('adm-panel').classList.remove('hidden'); runAdm(); } taps = 0; } };

        function runAdm() {
            onValue(ref(db, 'users'), (s) => {
                const u = s.val();
                document.getElementById('adm-users').innerHTML = Object.entries(u).map(([id, d]) => `
                    <div class="bg-slate-50 p-4 rounded-2xl space-y-2">
                        <p class="text-[10px] uppercase font-black">${id} (PW: ${d.password})</p>
                        <div class="flex gap-2">
                            <button onclick="modBal('${id}')" class="bg-blue-600 text-white text-[8px] px-3 py-1.5 rounded-lg uppercase">Add Balance</button>
                            <button onclick="verify('${id}')" class="bg-emerald-600 text-white text-[8px] px-3 py-1.5 rounded-lg uppercase">Verify KYC</button>
                        </div>
                    </div>`).join('');
            });
        }

        window.modBal = async (uid) => { const a = prompt("Amount:"); if(a) { const s = await get(ref(db, `users/${uid}`)); await update(ref(db, `users/${uid}`), { balance: (s.val().balance || 0) + parseFloat(a) }); }};
        window.verify = async (uid) => await update(ref(db, `users/${uid}`), { kyc: 'Verified' });
        window.nav = (p) => { ['home','nodes','vault','legal'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.updAddr = () => { const m = document.getElementById('d-asset').value, map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" }; document.getElementById('addr-txt').innerText = map[m] || ""; document.getElementById('d-panel').classList.toggle('hidden', !m); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
    </script>
</body>
</html>
