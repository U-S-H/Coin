<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Ultimate Production</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        body { background: #f8fafc; color: #000; font-family: 'Plus Jakarta Sans', sans-serif; }
        .glass-card { background: #fff !important; border-radius: 30px; border: 1px solid #e2e8f0; box-shadow: 0 10px 30px rgba(0,0,0,0.05); }
        .mining-card { background: #0f172a !important; border-radius: 35px; color: white !important; }
        .node-card { background: #fff !important; border-radius: 25px; border: 1px solid #e2e8f0; overflow: hidden; margin-bottom: 20px; text-align: center; padding-bottom: 20px; }
        .btn-center { background: #2563eb !important; color: #fff !important; padding: 14px; border-radius: 18px; font-size: 10px; font-weight: 800; text-transform: uppercase; width: 85%; margin: 0 auto; display: block; }
        .input-prime { background: #f1f5f9 !important; color: #000 !important; border: 2px solid #e2e8f0 !important; border-radius: 15px; padding: 14px; width: 100%; font-weight: 700; }
        nav { background: #fff !important; border-top: 1px solid #e2e8f0; height: 85px; z-index: 1000; }
        .nav-link { color: #94a3b8 !important; font-size: 9px; font-weight: 800; text-align: center; }
        .nav-link.active { color: #2563eb !important; }
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 99999; display: flex; align-items: center; justify-content: center; }
        .badge { font-size: 8px; font-weight: 900; padding: 4px 10px; border-radius: 8px; text-transform: uppercase; }
    </style>
</head>
<body>

    <div id="preloader"><div class="w-10 h-10 border-4 border-blue-600 border-t-transparent rounded-full animate-spin"></div></div>

    <div id="main-view" class="pb-32 hidden">
        <header class="p-5 bg-white sticky top-0 z-50 border-b flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div id="logo-trigger" class="w-12 h-12 bg-black text-white rounded-2xl flex items-center justify-center font-black">N</div>
                <div><p id="display-name" class="text-xs uppercase">---</p><span id="kyc-status" class="badge bg-amber-100 text-amber-600">Pending KYC</span></div>
            </div>
            <button onclick="logout()" class="w-10 h-10 bg-slate-100 rounded-xl flex items-center justify-center text-slate-400"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="tab-home" class="p-6 space-y-6">
            <div class="mining-card p-8">
                <p class="text-[9px] text-slate-400 uppercase tracking-widest font-bold">Current Portfolio</p>
                <h2 id="ui-bal" class="text-4xl font-black mt-2 text-white !important">$0.00</h2>
                <div class="h-24 mt-4"><canvas id="hashChart"></canvas></div>
                <div class="mt-6 pt-6 border-t border-white/10 flex justify-between">
                    <div><p class="text-[8px] text-slate-500 uppercase">Yield</p><p id="ui-prof" class="text-lg text-emerald-400 font-bold">+$0.00</p></div>
                    <div class="text-right"><p class="text-[8px] text-slate-500 uppercase">Shield Code</p><p id="anti-phish" class="text-xs text-blue-300 font-bold">NX-0000</p></div>
                </div>
            </div>

            <div class="glass-card p-6 space-y-4">
                <h4 class="text-xs uppercase text-blue-600">KYC Verification</h4>
                <p class="text-[10px] text-slate-500">Upload ID card to enable high-volume withdrawals.</p>
                <input type="file" id="kyc-file" accept="image/*" class="hidden" onchange="uploadKYC(this)">
                <button onclick="document.getElementById('kyc-file').click()" class="bg-slate-900 text-white w-full py-3 rounded-xl text-[10px] font-bold">UPLOAD DOCUMENT (BASE64)</button>
            </div>

            <h3 class="text-[10px] text-slate-400 uppercase tracking-[4px] ml-1">My Active Nodes</h3>
            <div id="active-list" class="space-y-3"></div>
        </main>

        <main id="tab-nodes" class="p-6 hidden">
            <h3 class="text-lg font-black uppercase mb-6">Omni Infra Nodes</h3>
            <div id="nodes-container" class="grid grid-cols-1 gap-6"></div>
        </main>

        <main id="tab-vault" class="p-6 space-y-8 hidden">
            <div class="glass-card p-6 space-y-4">
                <h3 class="text-xs text-blue-600 uppercase font-black">Capital Injection</h3>
                <select id="d-method" class="input-prime" onchange="showDeposit()">
                    <option value="">Select Deposit Gateway</option>
                    <option value="TRX">TRX (Trust Wallet)</option>
                    <option value="ETH">ETH (MetaMask)</option>
                    <option value="USDT">USDT TRC20 (Binance)</option>
                </select>
                <div id="d-area" class="hidden space-y-4">
                    <div class="p-4 bg-slate-50 rounded-2xl border-2 border-dashed border-slate-200">
                        <p id="d-addr" class="text-[10px] font-mono break-all text-center text-blue-600 font-bold"></p>
                    </div>
                    <input type="number" id="d-amt" placeholder="Amount ($)" class="input-prime">
                    <button onclick="alert('Transaction under audit...')" class="btn-center !w-full !m-0 !bg-black">Confirm Payment</button>
                </div>
            </div>

            <div class="glass-card p-6 space-y-4 border-t-8 border-slate-900">
                <h3 class="text-xs text-slate-500 uppercase font-black">Extraction System</h3>
                <select id="w-method" class="input-prime">
                    <option value="Binance">Binance Exchange</option>
                    <option value="OKX">OKX Terminal</option>
                    <option value="Bybit">Bybit Global</option>
                    <option value="Trust">Trust Wallet</option>
                </select>
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-prime">
                <input type="text" id="w-acc" placeholder="Destination Address / Account ID" class="input-prime">
                <button onclick="alert('Withdrawal Request Sent')" class="btn-center !w-full !m-0">Initialize Payout</button>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 flex justify-around items-center px-4">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-home text-2xl mb-1"></i><br>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-microchip text-2xl mb-1"></i><br>NODES</div>
            <div onclick="nav('vault')" class="nav-link"><i class="fa-solid fa-wallet text-2xl mb-1"></i><br>VAULT</div>
            <div onclick="nav('adm')" class="nav-link"><i class="fa-solid fa-user-shield text-2xl mb-1"></i><br>ADMIN</div>
        </nav>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="w-full max-w-sm space-y-8">
            <div class="text-center"><h1 class="text-5xl font-black italic">NEXUS<span class="text-blue-600">.</span></h1></div>
            <div id="login-box" class="glass-card p-8 space-y-5">
                <input type="text" id="l-user" placeholder="Account ID" class="input-prime">
                <input type="password" id="l-pass" placeholder="PIN" class="input-prime">
                <button onclick="login()" class="btn-center !w-full !m-0 !bg-black">Sign In</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] text-blue-600 uppercase font-bold cursor-pointer">Register Profile</p>
            </div>
            <div id="signup-box" class="glass-card p-8 space-y-5 hidden">
                <input type="text" id="s-user" placeholder="Choose ID" class="input-prime">
                <input type="password" id="s-pass" placeholder="New PIN" class="input-prime">
                <button onclick="signup()" class="btn-center !w-full !m-0 !bg-black">Initialize</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-slate-400 uppercase font-bold cursor-pointer">Back</p>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        // NODE DATA (15 Retail + 5 Elite = 20)
        const nodes = Array.from({length: 20}, (_, i) => ({
            id: i, name: i < 15 ? `Standard Node G-${i+1}` : `Elite Sovereign S-${i-14}`,
            price: i < 15 ? 100 + (i * 200) : 5000 + (i * 1000),
            yield: i < 15 ? 10 + (i * 15) : 800 + (i * 200)
        }));

        window.onload = () => {
            initChart(); renderNodes();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1000);
            if(localStorage.getItem('nx_usr')) startSession(localStorage.getItem('nx_usr'));
        };

        function renderNodes() {
            document.getElementById('nodes-container').innerHTML = nodes.map(n => `
                <div class="node-card">
                    <div class="h-32 bg-slate-100 flex items-center justify-center"><i class="fa-solid fa-microchip text-4xl text-blue-200"></i></div>
                    <div class="p-5">
                        <h4 class="font-black text-xs uppercase mb-1">${n.name}</h4>
                        <p class="text-[10px] text-emerald-600 font-bold mb-4">Daily Yield: $${n.yield}</p>
                        <p class="text-2xl font-black mb-5">$${n.price}</p>
                        <button onclick="buyNode(${n.id}, ${n.price}, '${n.name}')" class="btn-center">Activate Node</button>
                    </div>
                </div>`).join('');
        }

        window.showDeposit = () => {
            const m = document.getElementById('d-method').value;
            const addrs = {
                "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76",
                "ETH": "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355",
                "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ"
            };
            document.getElementById('d-addr').innerText = addrs[m] || "";
            document.getElementById('d-area').classList.toggle('hidden', !m);
        };

        window.uploadKYC = (input) => {
            const reader = new FileReader();
            reader.onload = async (e) => {
                const uid = localStorage.getItem('nx_usr');
                await update(ref(db, `users/${uid}`), { kycData: e.target.result, kyc: 'Reviewing' });
                alert("KYC Document uploaded in Base64. Admin will review.");
            };
            reader.readAsDataURL(input.files[0]);
        };

        window.login = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Error");
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
                document.getElementById('kyc-status').innerText = d.kyc || 'Pending KYC';
                document.getElementById('kyc-status').className = `badge ${d.kyc === 'Verified' ? 'bg-emerald-100 text-emerald-600' : 'bg-amber-100 text-amber-600'}`;
            });
        }

        window.buyNode = async (id, price, name) => {
            const uid = localStorage.getItem('nx_usr'), s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < price) return alert("Low Capital");
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - price });
            await push(ref(db, `users/${uid}/active_nodes`), { name, date: Date.now() });
            alert("Node Online!"); nav('home');
        };

        window.nav = (p) => { ['home','nodes','vault'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        function initChart() { const ctx = document.getElementById('hashChart').getContext('2d'); new Chart(ctx, { type: 'line', data: { labels: ['','','','','','',''], datasets: [{ data: [40, 60, 45, 80, 55, 90, 70], borderColor: '#3b82f6', tension: 0.4, borderWidth: 3, pointRadius: 0 }]}, options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false }}, scales: { x: { display: false }, y: { display: false }}}}); }
    </script>
</body>
</html>
