<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Financial Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --bg: #f8fafc; --text: #0f172a; }
        body { background-color: var(--bg); color: var(--text); font-family: 'Inter', sans-serif; overflow-x: hidden; }
        
        .glass-card { background: white; border: 1px solid rgba(0,0,0,0.05); box-shadow: 0 10px 40px rgba(0,0,0,0.02); border-radius: 40px; }
        .sidebar { position: fixed; top: 0; left: -320px; width: 300px; height: 100%; background: white; z-index: 1000; transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); box-shadow: 25px 0 60px rgba(0,0,0,0.05); }
        .sidebar.active { left: 0; }
        .overlay { position: fixed; inset: 0; background: rgba(0,0,0,0.15); backdrop-filter: blur(4px); z-index: 900; display: none; }
        .overlay.active { display: block; }
        
        .status-pending { color: #f59e0b; background: #fffbeb; padding: 4px 10px; border-radius: 20px; font-size: 9px; font-weight: 900; }
        .status-approved { color: #10b981; background: #ecfdf5; padding: 4px 10px; border-radius: 20px; font-size: 9px; font-weight: 900; }
        .status-rejected { color: #ef4444; background: #fef2f2; padding: 4px 10px; border-radius: 20px; font-size: 9px; font-weight: 900; }

        .progress-bar { height: 4px; background: #f1f5f9; border-radius: 10px; overflow: hidden; }
        .progress-fill { height: 100%; background: var(--gold); width: 0%; transition: 1s; }
        
        input, select { background: #f8fafc !important; border: 1px solid #e2e8f0 !important; border-radius: 15px; padding: 12px; width: 100%; font-size: 13px; font-weight: 600; }
        #scan-line { position: fixed; top: 0; width: 100%; height: 2px; background: var(--gold); z-index: 1100; animation: scan 6s infinite linear; opacity: 0.2; }
        @keyframes scan { 0% { top: 0; } 100% { top: 100%; } }
    </style>
</head>
<body>

    <div id="scan-line"></div>
    <div class="overlay" id="overlay" onclick="toggleSidebar()"></div>

    <div class="sidebar p-8 flex flex-col justify-between" id="sidebar">
        <div class="space-y-10">
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 bg-black rounded-xl flex items-center justify-center text-white font-black">N</div>
                <h2 class="font-black italic uppercase text-lg tracking-tighter">Terminal</h2>
            </div>
            <nav class="space-y-6">
                <div class="flex items-center gap-4 text-sm font-bold text-slate-400 hover:text-black cursor-pointer" onclick="toggleSidebar()"><i class="fa-solid fa-house"></i> Home Dashboard</div>
                <div class="flex items-center gap-4 text-sm font-bold text-slate-400 hover:text-black cursor-pointer" onclick="scrollToElement('history-sec')"><i class="fa-solid fa-receipt"></i> Operations Log</div>
                <div class="flex items-center gap-4 text-sm font-bold text-slate-400 hover:text-black cursor-pointer" onclick="showLegal('privacy')"><i class="fa-solid fa-user-shield"></i> Privacy Policy</div>
                <div class="flex items-center gap-4 text-sm font-bold text-slate-400 hover:text-black cursor-pointer" onclick="showLegal('about')"><i class="fa-solid fa-building"></i> Company Details</div>
            </nav>
        </div>
        <button onclick="logout()" class="w-full py-4 bg-red-50 text-red-600 rounded-2xl font-black text-[10px] uppercase tracking-widest hover:bg-red-600 hover:text-white transition">Terminate Session</button>
    </div>

    <nav class="sticky top-0 bg-white/80 backdrop-blur-md px-8 py-5 flex justify-between items-center z-[800] border-b border-slate-100">
        <div class="flex items-center gap-5">
            <i class="fa-solid fa-bars-staggered cursor-pointer text-xl" onclick="toggleSidebar()"></i>
            <div id="master-logo" class="cursor-pointer">
                <h1 class="text-xl font-black italic uppercase leading-none">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
                <p class="text-[7px] font-black text-slate-400 tracking-[0.4em] uppercase mt-1">Institutional v5.1</p>
            </div>
        </div>
        <div class="flex items-center gap-4">
            <div id="sync-timer" class="text-[10px] font-black bg-slate-100 px-3 py-1.5 rounded-full text-slate-500">SYNCING...</div>
        </div>
    </nav>

    <main class="container mx-auto px-6 py-10 space-y-12">
        
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <div class="lg:col-span-2 glass-card p-12 relative overflow-hidden bg-gradient-to-br from-white to-slate-50">
                <p class="text-[10px] font-black text-slate-400 uppercase tracking-widest mb-4">Secured Equity Value (USD)</p>
                <h2 id="balance-main" class="text-7xl md:text-8xl font-black italic tracking-tighter mb-12">$0.00</h2>
                <div class="flex flex-wrap gap-4">
                    <button onclick="openModal('deposit')" class="px-10 py-5 bg-[#f3ba2f] text-black font-black rounded-2xl text-[10px] uppercase shadow-xl shadow-yellow-500/20 hover:scale-105 transition">Add Assets</button>
                    <button onclick="openModal('withdraw')" class="px-10 py-5 bg-slate-100 text-slate-500 font-black rounded-2xl text-[10px] uppercase hover:bg-slate-200 transition">Liquidate</button>
                </div>
            </div>
            
            <div class="glass-card p-10 flex flex-col justify-between">
                <div>
                    <p class="text-[10px] font-black text-slate-400 uppercase mb-6">Yield Metrics</p>
                    <div class="space-y-4">
                        <div class="flex justify-between text-xs font-bold"><span>Daily Yield</span><span class="text-green-500">+$0.00</span></div>
                        <div class="flex justify-between text-xs font-bold"><span>Total Profit</span><span class="text-blue-500">$0.00</span></div>
                    </div>
                </div>
                <div class="pt-8 border-t border-slate-50">
                    <div class="flex justify-between text-[9px] font-black text-slate-300 mb-2 uppercase"><span>Cluster Load</span><span id="load-pct">65%</span></div>
                    <div class="progress-bar"><div class="progress-fill" id="load-fill"></div></div>
                </div>
            </div>
        </div>

        <div class="text-center space-y-2">
            <h3 class="text-xs font-black text-slate-300 uppercase tracking-[0.5em]">Global Hardware Nodes</h3>
        </div>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="nodes-grid"></div>

        <div id="history-sec" class="glass-card p-10">
            <div class="flex justify-between items-center mb-8">
                <h4 class="text-sm font-black italic uppercase">System Transaction Log</h4>
                <div class="flex gap-2">
                    <div class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
                    <span class="text-[9px] font-bold text-slate-400 uppercase">Live Audit</span>
                </div>
            </div>
            <div class="overflow-x-auto">
                <table class="w-full text-left">
                    <thead class="text-[10px] font-black text-slate-300 uppercase border-b border-slate-50">
                        <tr><th class="pb-4">Date</th><th class="pb-4">Operation</th><th class="pb-4">Asset Value</th><th class="pb-4">Verification</th></tr>
                    </thead>
                    <tbody id="history-rows" class="text-xs font-bold"></tbody>
                </table>
            </div>
        </div>
    </main>

    <div id="modal-portal" class="fixed inset-0 z-[1000] bg-white/95 backdrop-blur-2xl hidden flex items-center justify-center p-6">
        <div class="w-full max-w-lg glass-card p-12 relative">
            <button onclick="closeModal()" class="absolute top-8 right-10 text-4xl font-thin">&times;</button>
            <div id="deposit-ui" class="hidden">
                <h3 class="text-3xl font-black italic uppercase mb-8">Deposit</h3>
                <select id="dep-net" class="mb-4"><option value="TRC20">USDT (TRC20)</option><option value="BEP20">USDT (BEP20)</option></select>
                <div class="bg-slate-50 p-6 rounded-3xl mb-8 text-center border border-slate-100">
                    <p class="text-[8px] font-black text-slate-400 uppercase mb-2">Receiver Address:</p>
                    <p id="addr-text" class="text-[11px] font-mono font-black break-all">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
                </div>
                <input type="number" id="dep-amt" placeholder="Amount (USD)" class="mb-4">
                <input type="text" id="dep-hash" placeholder="Transaction Hash ID" class="mb-8">
                <button onclick="submitTX('DEPOSIT')" class="w-full bg-black text-white font-black py-5 rounded-2xl uppercase text-[10px] tracking-widest">Verify Transfer</button>
            </div>
            <div id="withdraw-ui" class="hidden text-center">
                <h3 class="text-3xl font-black italic uppercase mb-8 text-red-500">Withdraw</h3>
                <input type="text" id="wit-addr" placeholder="Wallet Address" class="mb-4">
                <input type="number" id="wit-amt" placeholder="0.00" class="mb-10 text-4xl text-center font-black">
                <button onclick="submitTX('WITHDRAW')" class="w-full bg-red-600 text-white font-black py-5 rounded-2xl uppercase text-[10px]">Request Extraction</button>
            </div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 z-[2000] bg-white hidden overflow-y-auto p-10">
        <div class="max-w-4xl mx-auto">
            <div class="flex justify-between items-center mb-12">
                <h2 class="text-3xl font-black italic uppercase">Nexus Admin Terminal</h2>
                <button onclick="location.reload()" class="text-4xl">&times;</button>
            </div>
            <div id="admin-list" class="space-y-4"></div>
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

        // UI Helpers
        window.toggleSidebar = () => { document.getElementById('sidebar').classList.toggle('active'); document.getElementById('overlay').classList.toggle('active'); };
        window.openModal = (t) => { document.getElementById('modal-portal').classList.remove('hidden'); document.getElementById('deposit-ui').classList.toggle('hidden', t!=='deposit'); document.getElementById('withdraw-ui').classList.toggle('hidden', t!=='withdraw'); };
        window.closeModal = () => document.getElementById('modal-portal').classList.add('hidden');
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.scrollToElement = (id) => { document.getElementById(id).scrollIntoView({behavior:'smooth'}); toggleSidebar(); };

        // Node Configuration
        const nodes = [
            {n:"Aegis", l:"Dubai", p:1.5, d:"24/30"}, {n:"Vortex", l:"Zurich", p:2.8, d:"12/30"},
            {n:"Titan", l:"Tokyo", p:4.5, d:"08/30"}, {n:"Apex", l:"London", p:8.2, d:"02/30"}
        ];
        document.getElementById('nodes-grid').innerHTML = nodes.map(node => `
            <div class="glass-card p-8 hover:border-[#f3ba2f] transition-all">
                <div class="flex justify-between items-center mb-6"><span class="text-[9px] font-black text-slate-300 uppercase">${node.n} Node</span><i class="fa-solid fa-bolt text-yellow-400"></i></div>
                <h4 class="text-xl font-black italic uppercase mb-1">${node.l}</h4>
                <p class="text-[10px] font-bold text-green-500 mb-8">+${node.p}% Daily Yield</p>
                <div class="flex justify-between text-[9px] font-black uppercase border-t border-slate-50 pt-4">
                    <span class="text-slate-400">Cycle Remaining</span><span>${node.d} Days</span>
                </div>
            </div>
        `).join('');

        // Master Logic
        if(!userUID) {
            const email = prompt("Institutional Email Required:");
            if(email) {
                userUID = email.replace(/[.#$[\]]/g, "_");
                localStorage.setItem('nexus_uid', userUID);
                set(ref(db, `users/${userUID}`), { email: email, balance: 0, history: [] }).then(()=>location.reload());
            }
        } else {
            onValue(ref(db, `users/${userUID}`), (snap) => {
                const d = snap.val();
                if(d) {
                    document.getElementById('balance-main').innerText = '$' + (d.balance || 0).toLocaleString(undefined, {minimumFractionDigits:2});
                    const hRows = document.getElementById('history-rows');
                    hRows.innerHTML = d.history ? d.history.map(tx => `
                        <tr class="border-b border-slate-50">
                            <td class="py-5 text-slate-400 text-[10px]">${tx.date}</td>
                            <td class="py-5 uppercase text-[10px]">${tx.type}</td>
                            <td class="py-5">$${tx.amt}</td>
                            <td class="py-5"><span class="status-${tx.status.toLowerCase()}">${tx.status}</span></td>
                        </tr>
                    `).join('') : `<tr><td colspan="4" class="py-10 text-center text-slate-300 uppercase">No Operations Logged</td></tr>`;
                }
            });
        }

        window.submitTX = async (type) => {
            const amt = type === 'DEPOSIT' ? document.getElementById('dep-amt').value : document.getElementById('wit-amt').value;
            if(!amt || amt <= 0) return alert("Invalid Amount!");
            const tx = { type, amt, date: new Date().toLocaleString(), status: 'PENDING' };
            const snap = await get(ref(db, `users/${userUID}`));
            let h = snap.val().history || []; h.unshift(tx);
            await update(ref(db, `users/${userUID}`), { history: h });
            alert("Protocol Broadcasted. Awaiting Verification.");
            closeModal();
        };

        // Admin Terminal
        let taps = 0;
        document.getElementById('master-logo').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Security Key:") === "coin786") showAdmin(); taps=0; }
            setTimeout(()=>taps=0, 2000);
        };
        function showAdmin() {
            document.getElementById('admin-panel').classList.remove('hidden');
            onValue(ref(db, 'users'), (snap) => {
                const users = snap.val(); let html = "";
                for(let id in users) {
                    html += `<div class="glass-card p-8 flex justify-between items-center mb-4">
                        <div><p class="text-[10px] font-black text-slate-400">${users[id].email}</p><h4 class="text-2xl font-black italic">$${users[id].balance}</h4></div>
                        <div class="flex gap-2">
                            <button onclick="editBal('${id}')" class="bg-black text-white px-5 py-2 rounded-xl text-[10px] font-bold">Balance</button>
                            <button onclick="approveTX('${id}')" class="bg-green-500 text-white px-5 py-2 rounded-xl text-[10px] font-bold">Approve Log</button>
                        </div>
                    </div>`;
                }
                document.getElementById('admin-list').innerHTML = html;
            });
        }
        window.editBal = (id) => { const v = prompt("New Balance:"); if(v) update(ref(db, `users/${id}`), {balance: parseFloat(v)}); };
        window.approveTX = async (id) => {
            const snap = await get(ref(db, `users/${id}`));
            const history = snap.val().history;
            if(history && history[0]) {
                history[0].status = "APPROVED";
                update(ref(db, `users/${id}`), { history: history });
                alert("Log Entry Verified!");
            }
        };

        // Timer Sync
        setInterval(() => {
            const now = new Date();
            document.getElementById('sync-timer').innerText = `SYNC: ${now.getHours()}:${now.getMinutes()}:${now.getSeconds()}`;
            document.getElementById('load-fill').style.width = Math.floor(Math.random()*40 + 60) + "%";
        }, 1000);
    </script>
</body>
</html>
