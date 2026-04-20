<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Elite Dashboard</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --accent: #6366f1; --bg: #fdfdfd; }
        body { background-color: var(--bg); color: #1e293b; font-family: 'Plus Jakarta Sans', sans-serif; overflow-x: hidden; }
        
        .modern-card { background: white; border: 1px solid rgba(0,0,0,0.04); border-radius: 32px; box-shadow: 0 20px 40px rgba(0,0,0,0.02); transition: 0.3s; }
        .modern-card:hover { transform: translateY(-5px); box-shadow: 0 30px 60px rgba(0,0,0,0.05); }
        
        .sidebar { position: fixed; top: 0; left: -320px; width: 300px; height: 100%; background: white; z-index: 1000; transition: 0.4s; border-right: 1px solid #f1f5f9; }
        .sidebar.active { left: 0; }
        .overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.1); backdrop-filter: blur(8px); z-index: 900; display: none; }
        .overlay.active { display: block; }

        .status-pill { padding: 4px 12px; border-radius: 100px; font-size: 10px; font-weight: 800; text-transform: uppercase; }
        .pending { background: #fff7ed; color: #f97316; }
        .approved { background: #f0fdf4; color: #22c55e; }
        
        .gradient-btn { background: linear-gradient(135deg, #f3ba2f 0%, #ffdb4d 100%); color: #000; font-weight: 800; transition: 0.3s; }
        .gradient-btn:hover { opacity: 0.9; transform: scale(1.02); }

        #scan-anim { position: fixed; top: 0; width: 100%; height: 3px; background: var(--gold); z-index: 1500; animation: scan 8s infinite; opacity: 0.4; }
        @keyframes scan { 0% { top: 0; } 100% { top: 100%; } }
    </style>
</head>
<body>

    <div id="scan-anim"></div>
    <div class="overlay" id="overlay" onclick="toggleSidebar()"></div>

    <aside class="sidebar p-8 flex flex-col justify-between" id="sidebar">
        <div>
            <div class="flex items-center gap-3 mb-12">
                <div class="w-10 h-10 bg-black rounded-2xl flex items-center justify-center text-white font-black">N</div>
                <h2 class="font-black italic text-xl uppercase tracking-tighter">Nexus</h2>
            </div>
            <nav class="space-y-4">
                <div class="p-4 rounded-2xl bg-slate-50 text-slate-900 font-bold flex items-center gap-4 cursor-pointer">
                    <i class="fa-solid fa-grid-2"></i> Dashboard
                </div>
                <div onclick="scrollToId('nodes-sec')" class="p-4 rounded-2xl text-slate-400 font-bold flex items-center gap-4 cursor-pointer hover:bg-slate-50 hover:text-black">
                    <i class="fa-solid fa-microchip"></i> Mining Nodes
                </div>
                <div onclick="scrollToId('history-sec')" class="p-4 rounded-2xl text-slate-400 font-bold flex items-center gap-4 cursor-pointer hover:bg-slate-50 hover:text-black">
                    <i class="fa-solid fa-receipt"></i> Transaction Log
                </div>
            </nav>
        </div>
        <button onclick="logout()" class="w-full py-4 bg-red-50 text-red-500 rounded-2xl font-black text-xs uppercase hover:bg-red-500 hover:text-white transition">Terminate</button>
    </aside>

    <nav class="sticky top-0 bg-white/70 backdrop-blur-xl z-[800] border-b border-slate-100 px-8 py-5 flex justify-between items-center">
        <div class="flex items-center gap-6">
            <i class="fa-solid fa-bars-staggered text-xl cursor-pointer" onclick="toggleSidebar()"></i>
            <div id="logo" class="cursor-pointer">
                <h1 class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
            </div>
        </div>
        <div class="flex items-center gap-4">
            <span id="user-display" class="hidden md:block text-[10px] font-black text-slate-400 uppercase tracking-widest">User_Term_01</span>
            <div class="w-10 h-10 bg-slate-100 rounded-full flex items-center justify-center font-black">U</div>
        </div>
    </nav>

    <main class="container mx-auto px-6 py-10 space-y-10">
        
        <div class="grid grid-cols-1 lg:grid-cols-4 gap-6">
            <div class="lg:col-span-2 modern-card p-10 bg-gradient-to-br from-white to-slate-50 border-l-[10px] border-[#f3ba2f]">
                <p class="text-[10px] font-black text-slate-400 uppercase tracking-[0.4em] mb-4">Total Net Equity</p>
                <h2 id="main-balance" class="text-6xl md:text-7xl font-black italic tracking-tighter mb-10 text-slate-900">$0.00</h2>
                <div class="flex gap-4">
                    <button onclick="openAction('dep')" class="gradient-btn px-8 py-4 rounded-2xl text-[10px] uppercase tracking-widest">Add Assets</button>
                    <button onclick="openAction('wit')" class="bg-slate-100 px-8 py-4 rounded-2xl text-[10px] font-black uppercase text-slate-400 hover:bg-slate-200">Withdraw</button>
                </div>
            </div>

            <div class="modern-card p-8 flex flex-col justify-between">
                <div>
                    <p class="text-[10px] font-black text-slate-400 uppercase mb-4">Total Yield</p>
                    <h3 id="total-profit" class="text-3xl font-black italic text-green-500">+$0.00</h3>
                </div>
                <div class="pt-6 border-t border-slate-50">
                    <div class="flex justify-between text-[9px] font-black text-slate-300 uppercase"><span>Market Status</span><span class="text-blue-500">Volatile</span></div>
                </div>
            </div>

            <div class="modern-card p-8 bg-slate-900 text-white flex flex-col justify-between">
                <div>
                    <p class="text-[10px] font-black text-slate-500 uppercase mb-4">Daily Bonus</p>
                    <h3 class="text-2xl font-black italic text-[#f3ba2f]">Ready</h3>
                </div>
                <button onclick="claimBonus()" class="w-full py-3 bg-white/10 rounded-xl text-[9px] font-black uppercase tracking-widest hover:bg-[#f3ba2f] hover:text-black transition">Claim Now</button>
            </div>
        </div>

        <div id="nodes-sec" class="space-y-6">
            <h3 class="text-center text-xs font-black text-slate-300 uppercase tracking-[0.6em]">Active Mining Clusters</h3>
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="nodes-grid"></div>
        </div>

        <div id="history-sec" class="modern-card p-10 overflow-hidden">
            <div class="flex justify-between items-center mb-8">
                <h4 class="text-sm font-black italic uppercase">Institutional Ledger</h4>
                <div class="text-[9px] font-bold text-slate-300 uppercase">Live Blockchain Sync <i class="fa-solid fa-rotate animate-spin ml-2"></i></div>
            </div>
            <div class="overflow-x-auto">
                <table class="w-full text-left">
                    <thead class="text-[10px] font-black text-slate-300 uppercase border-b border-slate-50">
                        <tr><th class="pb-4">Timestamp</th><th class="pb-4">Operation</th><th class="pb-4">Value</th><th class="pb-4">Status</th></tr>
                    </thead>
                    <tbody id="history-table" class="text-xs font-bold"></tbody>
                </table>
            </div>
        </div>

    </main>

    <footer class="bg-white border-t border-slate-100 pt-20 pb-10 px-8">
        <div class="container mx-auto grid grid-cols-1 md:grid-cols-4 gap-12 text-center md:text-left">
            <div class="col-span-1 md:col-span-2">
                <h2 class="text-xl font-black italic uppercase mb-4">Nexus Infinity <span class="text-[#f3ba2f]">Group</span></h2>
                <p class="text-xs text-slate-400 max-w-sm mx-auto md:mx-0">Licensed and regulated by GFCA (Global Financial Conduct Authority). Registered Address: Level 42, The Shard, London, UK.</p>
            </div>
            <div class="space-y-4">
                <h4 class="text-[10px] font-black text-slate-900 uppercase">Compliance</h4>
                <div class="flex flex-col gap-2 text-xs text-slate-400 font-medium">
                    <span class="hover:text-black cursor-pointer" onclick="showLegal('privacy')">Privacy Policy</span>
                    <span class="hover:text-black cursor-pointer" onclick="showLegal('terms')">Terms of Service</span>
                </div>
            </div>
            <div class="space-y-4">
                <h4 class="text-[10px] font-black text-slate-900 uppercase">Support</h4>
                <p class="text-xs text-slate-400">admin@nexus-infinity.pro</p>
                <div class="flex justify-center md:justify-start gap-4 grayscale opacity-30">
                    <i class="fa-brands fa-cc-visa text-xl"></i>
                    <i class="fa-brands fa-cc-mastercard text-xl"></i>
                </div>
            </div>
        </div>
        <div class="text-center mt-16 pt-8 border-t border-slate-50">
            <p class="text-[9px] font-black text-slate-200 uppercase tracking-[0.5em]">&copy; 2026 Nexus Infinity Institutional Terminal</p>
        </div>
    </footer>

    <div id="action-modal" class="fixed inset-0 z-[1000] bg-white/95 backdrop-blur-xl hidden flex items-center justify-center p-6">
        <div class="w-full max-w-md modern-card p-10 relative">
            <button onclick="closeAction()" class="absolute top-6 right-8 text-4xl font-thin">&times;</button>
            
            <div id="dep-ui" class="hidden">
                <h3 class="text-3xl font-black italic uppercase mb-8">Deposit</h3>
                <select id="dep-net" class="w-full p-4 mb-4 bg-slate-50 border-none rounded-2xl font-bold text-xs">
                    <option value="TRC20">USDT (TRC20)</option>
                    <option value="BEP20">USDT (BEP20)</option>
                </select>
                <div class="p-6 bg-slate-50 rounded-3xl mb-8 text-center border border-slate-100">
                    <p class="text-[8px] font-black text-slate-400 uppercase mb-2">Receiver Address:</p>
                    <p class="text-[10px] font-mono font-black break-all">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount (USD)" class="w-full p-4 mb-4 bg-slate-50 border-none rounded-2xl text-xs font-bold">
                <input type="text" id="dep-hash" placeholder="Transaction Hash" class="w-full p-4 mb-8 bg-slate-50 border-none rounded-2xl text-xs font-bold">
                <button onclick="handleTX('DEPOSIT')" class="w-full py-5 gradient-btn rounded-2xl text-[10px] uppercase">Verify Transfer</button>
            </div>

            <div id="wit-ui" class="hidden">
                <h3 class="text-3xl font-black italic uppercase mb-8 text-red-500">Withdraw</h3>
                <input type="text" id="wit-addr" placeholder="Destination Address" class="w-full p-4 mb-4 bg-slate-50 border-none rounded-2xl text-xs font-bold">
                <input type="number" id="wit-amt" placeholder="0.00" class="w-full p-8 mb-8 bg-slate-50 border-none rounded-3xl text-4xl text-center font-black">
                <button onclick="handleTX('WITHDRAW')" class="w-full py-5 bg-black text-white rounded-2xl text-[10px] font-black uppercase">Request Liquidation</button>
            </div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 z-[2000] bg-white hidden overflow-y-auto p-12">
        <div class="max-w-4xl mx-auto">
            <div class="flex justify-between items-center mb-12">
                <h2 class="text-3xl font-black italic uppercase">Nexus Admin Terminal</h2>
                <button onclick="location.reload()" class="text-4xl">&times;</button>
            </div>
            <div id="admin-users" class="space-y-4"></div>
        </div>
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
        let userUID = localStorage.getItem('nexus_uid');

        // UI Logic
        window.toggleSidebar = () => { document.getElementById('sidebar').classList.toggle('active'); document.getElementById('overlay').classList.toggle('active'); };
        window.scrollToId = (id) => { document.getElementById(id).scrollIntoView({behavior:'smooth'}); toggleSidebar(); };
        window.openAction = (t) => { document.getElementById('action-modal').classList.remove('hidden'); document.getElementById('dep-ui').classList.toggle('hidden', t!=='dep'); document.getElementById('wit-ui').classList.toggle('hidden', t!=='wit'); };
        window.closeAction = () => document.getElementById('action-modal').classList.add('hidden');
        window.logout = () => { localStorage.clear(); location.reload(); };

        // Nodes Data
        const nodes = [
            {n: "Titan", l: "Dubai", y: 1.5, p: 45}, {n: "Vortex", l: "London", y: 2.8, p: 20},
            {n: "Apex", l: "Tokyo", y: 5.2, p: 75}, {n: "Aegis", l: "Zurich", y: 8.5, p: 10}
        ];
        document.getElementById('nodes-grid').innerHTML = nodes.map(node => `
            <div class="modern-card p-8">
                <div class="flex justify-between items-center mb-6">
                    <span class="text-[9px] font-black text-slate-300 uppercase">${node.n}_CLUSTER</span>
                    <i class="fa-solid fa-bolt text-yellow-400"></i>
                </div>
                <h4 class="text-xl font-black italic uppercase mb-2">${node.l}</h4>
                <p class="text-[10px] font-black text-green-500 mb-8">+${node.y}% Daily Yield</p>
                <div class="h-1 w-full bg-slate-100 rounded-full overflow-hidden">
                    <div class="h-full bg-[#f3ba2f]" style="width: ${node.p}%"></div>
                </div>
            </div>
        `).join('');

        // Master Logic
        if(!userUID) {
            const email = prompt("Enter Terminal Email:");
            if(email) {
                userUID = email.replace(/[.#$[\]]/g, "_");
                localStorage.setItem('nexus_uid', userUID);
                set(ref(db, `users/${userUID}`), { email: email, balance: 0, profit: 0, history: [] }).then(()=>location.reload());
            }
        } else {
            document.getElementById('user-display').innerText = userUID;
            onValue(ref(db, `users/${userUID}`), (snap) => {
                const d = snap.val();
                if(d) {
                    document.getElementById('main-balance').innerText = '$' + (d.balance || 0).toLocaleString();
                    document.getElementById('total-profit').innerText = '+$' + (d.profit || 0).toLocaleString();
                    const table = document.getElementById('history-table');
                    table.innerHTML = d.history ? d.history.map(tx => `
                        <tr class="border-b border-slate-50">
                            <td class="py-5 text-slate-400 text-[10px]">${tx.date}</td>
                            <td class="py-5 uppercase text-[10px]">${tx.type}</td>
                            <td class="py-5">$${tx.amt}</td>
                            <td class="py-5"><span class="status-pill ${tx.status.toLowerCase()}">${tx.status}</span></td>
                        </tr>
                    `).join('') : `<tr><td colspan="4" class="py-10 text-center text-slate-200">NO LOGS FOUND</td></tr>`;
                }
            });
        }

        window.handleTX = async (type) => {
            const amt = type === 'DEPOSIT' ? document.getElementById('dep-amt').value : document.getElementById('wit-amt').value;
            if(!amt || amt <= 0) return alert("Enter valid amount!");
            const tx = { type, amt, date: new Date().toLocaleString(), status: 'PENDING' };
            const snap = await get(ref(db, `users/${userUID}`));
            let h = snap.val().history || []; h.unshift(tx);
            await update(ref(db, `users/${userUID}`), { history: h });
            alert("Transaction Broadcasted to Blockchain!");
            closeAction();
        };

        window.claimBonus = () => {
            alert("Daily Bonus System Syncing... Check back in 24h, sweetie!");
        };

        // ADMIN TERMINAL
        let taps = 0;
        document.getElementById('logo').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Auth Key:") === "coin786") showAdmin(); taps=0; }
            setTimeout(()=>taps=0, 3000);
        };
        function showAdmin() {
            document.getElementById('admin-panel').classList.remove('hidden');
            onValue(ref(db, 'users'), (snap) => {
                const data = snap.val(); let html = "";
                for(let id in data) {
                    html += `<div class="modern-card p-6 flex justify-between items-center mb-4">
                        <div><p class="text-[10px] font-black text-slate-400">${data[id].email}</p><h4 class="text-xl font-black italic">$${data[id].balance}</h4></div>
                        <div class="flex gap-2">
                            <button onclick="modVal('${id}', 'balance')" class="bg-black text-white px-4 py-2 rounded-xl text-[10px]">Bal</button>
                            <button onclick="modVal('${id}', 'profit')" class="bg-green-500 text-white px-4 py-2 rounded-xl text-[10px]">Profit</button>
                            <button onclick="approve('${id}')" class="bg-blue-500 text-white px-4 py-2 rounded-xl text-[10px]">Approve</button>
                        </div>
                    </div>`;
                }
                document.getElementById('admin-users').innerHTML = html;
            });
        }
        window.modVal = (id, field) => { const v = prompt(`New ${field}:`); if(v) update(ref(db, `users/${id}`), {[field]: parseFloat(v)}); };
        window.approve = async (id) => {
            const snap = await get(ref(db, `users/${id}`));
            const h = snap.val().history;
            if(h && h[0]) { h[0].status = "APPROVED"; update(ref(db, `users/${id}`), {history: h}); alert("Approved!"); }
        };
    </script>
</body>
</html>
