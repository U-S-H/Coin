<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>NEXUS OMNI | Ultimate Master Edition</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap');
        
        body { background: #f8fafc; color: #000; font-family: 'Plus Jakarta Sans', sans-serif; scroll-behavior: smooth; }
        p, h1, h2, h3, h4, span, b, label { color: #000 !important; font-weight: 700; }
        .text-white, .btn-prime, .mining-card *, .nav-link.active * { color: #fff !important; }
        
        /* Modern Glass UI */
        .glass-card { background: rgba(255, 255, 255, 0.98) !important; border-radius: 35px; border: 1px solid #e2e8f0; box-shadow: 0 15px 40px rgba(0,0,0,0.04); }
        .mining-card { background: linear-gradient(135deg, #0f172a 0%, #1e293b 100%) !important; border-radius: 45px; box-shadow: 0 25px 60px rgba(15,23,42,0.25); }
        
        /* Infrastructure Nodes */
        .node-card { background: #fff !important; border-radius: 35px; overflow: hidden; border: 1px solid #e2e8f0; margin-bottom: 30px; transition: 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        .node-card:active { transform: scale(0.97); }
        .node-img { width: 100%; height: 210px; object-fit: cover; filter: brightness(0.9); }
        
        /* Global Inputs & Buttons */
        .btn-prime { background: #2563eb !important; padding: 18px; border-radius: 22px; font-size: 11px; font-weight: 800; text-transform: uppercase; letter-spacing: 2px; width: 85%; margin: 0 auto; display: block; border: none; cursor: pointer; transition: 0.3s; }
        .input-prime { background: #f1f5f9 !important; border: 2px solid #e2e8f0 !important; border-radius: 20px; padding: 18px; width: 100%; font-weight: 700; font-size: 14px; transition: 0.3s; }
        .input-prime:focus { border-color: #2563eb !important; background: #fff !important; outline: none; }

        /* Navigation */
        nav { background: rgba(255, 255, 255, 0.9) !important; backdrop-filter: blur(15px); border-top: 1px solid #e2e8f0; height: 95px; }
        .nav-link { color: #94a3b8 !important; font-size: 9px; font-weight: 800; text-align: center; }
        .nav-link.active { color: #2563eb !important; }

        #preloader { position: fixed; inset: 0; background: #fff; z-index: 99999; display: flex; align-items: center; justify-content: center; }
        .badge { font-size: 8px; padding: 4px 12px; border-radius: 10px; text-transform: uppercase; letter-spacing: 1px; }
        .faq-item { border-bottom: 1px solid #f1f5f9; padding: 20px 0; }
        .proof-preview { width: 100%; height: 150px; border-radius: 20px; object-fit: cover; margin-top: 10px; border: 2px solid #e2e8f0; display: none; }
    </style>
</head>
<body>

    <div id="preloader"><div class="w-14 h-14 border-[5px] border-blue-600 border-t-transparent rounded-full animate-spin"></div></div>

    <div id="main-view" class="hidden pb-40">
        <header class="p-6 bg-white/80 backdrop-blur-md sticky top-0 z-50 border-b flex justify-between items-center">
            <div class="flex items-center gap-4">
                <div id="logo-trigger" class="w-14 h-14 bg-black text-white rounded-3xl flex items-center justify-center text-2xl font-black shadow-xl">N</div>
                <div><p id="display-name" class="text-sm font-black uppercase">---</p><span id="kyc-badge" class="badge bg-amber-100 text-amber-600">Pending Audit</span></div>
            </div>
            <button onclick="logout()" class="w-12 h-12 bg-slate-100 rounded-2xl flex items-center justify-center text-slate-400"><i class="fa-solid fa-power-off text-lg"></i></button>
        </header>

        <main id="tab-home" class="p-6 space-y-8">
            <div class="mining-card p-10">
                <p class="text-[10px] text-slate-400 uppercase tracking-[4px]">Verified Capital</p>
                <h2 id="ui-bal" class="text-5xl font-black mt-3 text-white !important tracking-tighter">$0.00</h2>
                <div class="h-28 mt-6"><canvas id="hashChart"></canvas></div>
            </div>

            <div class="glass-card p-8 space-y-5">
                <h3 class="text-xs font-black uppercase text-blue-600 tracking-widest">Protocol Verification</h3>
                <input type="file" id="kyc-file" class="hidden" accept="image/*" onchange="processKYC(this)">
                <button onclick="document.getElementById('kyc-file').click()" class="w-full py-4 bg-slate-900 text-white rounded-2xl text-[10px] font-black uppercase shadow-2xl">Submit Base64 Document</button>
            </div>

            <h3 class="text-[11px] text-slate-400 uppercase tracking-[6px] ml-1">Asset Logs</h3>
            <div id="tx-history" class="space-y-4"></div>
        </main>

        <main id="tab-nodes" class="p-6 hidden">
            <h3 class="text-xl font-black uppercase mb-8 tracking-tighter">Mining Infrastructure</h3>
            <div id="nodes-container" class="space-y-8"></div>
        </main>

        <main id="tab-vault" class="p-6 space-y-8 hidden">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xs font-black uppercase text-blue-600 tracking-widest">Deposit Gateway</h3>
                <p class="text-[10px] text-slate-400">Min Deposit: $100</p>
                <select id="d-method" class="input-prime" onchange="showGate()">
                    <option value="">Select Gateway</option>
                    <option value="Binance">Binance (USDT)</option>
                    <option value="Trust">Trust Wallet (TRX/USDT)</option>
                    <option value="MetaMask">MetaMask (ETH/BNB)</option>
                </select>
                <div id="d-panel" class="hidden space-y-5">
                    <div class="p-6 bg-blue-50 rounded-3xl border-2 border-dashed border-blue-200">
                        <p id="d-addr" class="text-[10px] font-mono break-all text-center text-blue-600 font-black"></p>
                    </div>
                    <input type="number" id="d-amt" placeholder="Amount ($)" class="input-prime">
                    <input type="text" id="d-tid" placeholder="Transaction ID (TID)" class="input-prime">
                    <input type="file" id="d-proof" class="hidden" accept="image/*" onchange="prevProof(this)">
                    <button onclick="document.getElementById('d-proof').click()" class="w-full py-4 bg-slate-100 rounded-2xl text-[10px] font-black uppercase">Upload Proof Image</button>
                    <img id="proof-img" class="proof-preview">
                    <button onclick="logTransaction('Deposit')" class="btn-prime !w-full !m-0 !bg-slate-900">Confirm Deposit</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6 border-t-[12px] border-slate-900">
                <h3 class="text-xs font-black uppercase text-slate-400 tracking-widest">Withdrawal System</h3>
                <p class="text-[10px] text-slate-400">Min Withdraw: $50</p>
                <select id="w-method" class="input-prime">
                    <option value="Binance">Binance</option>
                    <option value="OKX">OKX</option>
                    <option value="Trust">Trust Wallet</option>
                    <option value="MetaMask">MetaMask</option>
                    <option value="Coinbase">Coinbase</option>
                    <option value="Bybit">Bybit</option>
                </select>
                <input type="number" id="w-amt" placeholder="Amount ($)" class="input-prime">
                <input type="text" id="w-acc" placeholder="Account Number / Wallet" class="input-prime">
                <input type="text" id="w-user" placeholder="Account Username" class="input-prime">
                <button onclick="logTransaction('Withdraw')" class="btn-prime !w-full !m-0">Initialize Withdrawal</button>
            </div>
        </main>

        <main id="tab-legal" class="p-6 hidden space-y-8">
            <div class="glass-card p-8">
                <h4 class="text-blue-600 text-[10px] mb-4 uppercase tracking-widest">Company History</h4>
                <p class="text-xs text-slate-600 leading-loose">Nexus Omni Global (Seychelles #8812) operates decentralized high-hashrate nodes since 2024. Our mission is to democratize institutional mining power.</p>
            </div>
            <div class="glass-card p-8">
                <h4 class="text-blue-600 text-[10px] mb-4 uppercase tracking-widest">Global FAQ</h4>
                <div class="faq-item"><p class="text-[11px]">Minimum deposit?</p><p class="text-[10px] text-slate-400 font-medium mt-2">Access starts at $150 per node.</p></div>
                <div class="faq-item border-none"><p class="text-[11px]">How long for withdrawal?</p><p class="text-[10px] text-slate-400 font-medium mt-2">Usually 1-6 hours after audit.</p></div>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 flex justify-around items-center px-4 z-[1000]">
            <div onclick="nav('home')" class="nav-link active"><i class="fa-solid fa-house-chimney text-2xl mb-1"></i><br>HOME</div>
            <div onclick="nav('nodes')" class="nav-link"><i class="fa-solid fa-microchip text-2xl mb-1"></i><br>NODES</div>
            <div onclick="nav('vault')" class="nav-link"><i class="fa-solid fa-vault text-2xl mb-1"></i><br>VAULT</div>
            <div onclick="nav('legal')" class="nav-link"><i class="fa-solid fa-file-shield text-2xl mb-1"></i><br>INFO</div>
        </nav>
    </div>

    <div id="adm-panel" class="fixed inset-0 bg-white z-[10001] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10 border-b-4 pb-6"><h2 class="text-2xl font-black text-blue-600 uppercase tracking-tighter">MASTER OVERRIDE</h2><button onclick="document.getElementById('adm-panel').classList.add('hidden')" class="text-5xl text-slate-300">&times;</button></div>
        <div id="adm-users" class="space-y-8"></div>
    </div>

    <div id="auth-view" class="min-h-screen flex items-center justify-center p-8 bg-slate-50">
        <div class="max-w-sm w-full space-y-12">
            <div class="text-center"><h1 class="text-7xl font-black italic tracking-tighter">NEXUS<span class="text-blue-600">.</span></h1></div>
            <div id="login-box" class="glass-card p-10 space-y-6">
                <input type="text" id="l-user" placeholder="Account ID" class="input-prime">
                <input type="password" id="l-pass" placeholder="PIN" class="input-prime">
                <button onclick="login()" class="btn-prime !w-full !m-0 !bg-slate-900 shadow-2xl">Login</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] font-black text-blue-600 uppercase cursor-pointer">Register</p>
            </div>
            <div id="signup-box" class="glass-card p-10 space-y-6 hidden">
                <input type="text" id="s-user" placeholder="Choose ID" class="input-prime">
                <input type="password" id="s-pass" placeholder="Security PIN" class="input-prime">
                <button onclick="signup()" class="btn-prime !w-full !m-0 !bg-slate-900">Sign Up</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] font-black text-slate-400 uppercase cursor-pointer">Back</p>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const config = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(config);
        const db = getDatabase(app);

        let proofBase64 = "";

        const nodeLib = Array.from({length: 20}, (_, i) => ({
            id: i, name: i < 15 ? `Sovereign G-${i+1}` : `Omni Master v${i-14}`,
            price: i < 15 ? 150 + (i * 350) : 6000 + (i * 1500),
            yield: i < 15 ? 12 + (i * 30) : 800 + (i * 300),
            img: `https://images.unsplash.com/photo-${['1518770660439-4636190af475','1550751827-4bd374c3f58b','1639762681485-074b7f938ba0','1640343136701-d051ff221245','1639762681057-32c9a2d572e4','1620712946848-016ce8a03972','1607799279861-4dd421837ad1','1451187580459-43490279c0fa','1558494949-ef010cbdcc51','1517077304055-6e89a38289c8','1563986768609-322da13575f3','1535223289827-42f1e9919769','1519389950473-47ba0277781c','1461749280684-dccba630e2f6','1498050108023-c5249f4df085','1504384308090-c894fdcc538d','1526374965328-7f61d4dc18c5','1614064641938-3bbee52942c7','1581091226825-a6a2a5aee158','1581092160562-40aa08e78837'][i]}?w=600&q=80`
        }));

        window.onload = () => {
            initChart(); renderNodes();
            setTimeout(() => document.getElementById('preloader').style.display='none', 1500);
            if(localStorage.getItem('nx_usr')) startSession(localStorage.getItem('nx_usr'));
        };

        window.prevProof = (i) => {
            const r = new FileReader(); r.onload = (e) => {
                proofBase64 = e.target.result; const p = document.getElementById('proof-img');
                p.src = proofBase64; p.style.display = 'block';
            }; r.readAsDataURL(i.files[0]);
        };

        window.showGate = () => {
            const m = document.getElementById('d-method').value;
            const map = { "Binance": "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ", "Trust": "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76", "MetaMask": "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355" };
            document.getElementById('d-addr').innerText = map[m] || "";
            document.getElementById('d-panel').classList.toggle('hidden', !m);
        };

        window.logTransaction = async (type) => {
            const uid = localStorage.getItem('nx_usr');
            if (type === 'Deposit') {
                const amt = parseFloat(document.getElementById('d-amt').value);
                const tid = document.getElementById('d-tid').value;
                if(amt < 100) return alert("Min Deposit $100");
                if(!tid || !proofBase64) return alert("Enter TID & Upload Proof");
                await push(ref(db, `users/${uid}/transactions`), { type, amount: amt, tid, proof: proofBase64, status: 'Pending', time: Date.now() });
            } else {
                const amt = parseFloat(document.getElementById('w-amt').value);
                const acc = document.getElementById('w-acc').value;
                const usr = document.getElementById('w-user').value;
                const snap = await get(ref(db, `users/${uid}`));
                if(amt < 50) return alert("Min Withdrawal $50");
                if(snap.val().balance < amt) return alert("Insufficient Balance");
                if(!acc || !usr) return alert("Fill all fields");
                await push(ref(db, `users/${uid}/transactions`), { type, amount: amt, account: acc, username: usr, status: 'Pending', time: Date.now() });
            }
            alert("Request broadcasted!"); location.reload();
        };

        window.processKYC = (input) => {
            const r = new FileReader(); r.onload = async (e) => {
                const uid = localStorage.getItem('nx_usr');
                await update(ref(db, `users/${uid}`), { kycData: e.target.result, kyc: 'Under Audit' });
                alert("Identity string encoded. Manual audit initiated.");
            }; r.readAsDataURL(input.files[0]);
        };

        window.login = async () => {
            const u = document.getElementById('l-user').value.trim(), p = document.getElementById('l-pass').value;
            const s = await get(ref(db, `users/${u}`));
            if(s.exists() && s.val().password === p) { localStorage.setItem('nx_usr', u); startSession(u); } else alert("Access Error");
        };

        window.signup = async () => {
            const u = document.getElementById('s-user').value.trim(), p = document.getElementById('s-pass').value;
            if(u && p) { await set(ref(db, `users/${u}`), { username: u, password: p, balance: 0, kyc: 'Unverified' }); toggleAuth(false); }
        };

        function startSession(uid) {
            document.getElementById('auth-view').classList.add('hidden');
            document.getElementById('main-view').classList.remove('hidden');
            document.getElementById('display-name').innerText = uid;
            onValue(ref(db, `users/${uid}`), (snap) => {
                const d = snap.val(); if(!d) return;
                document.getElementById('ui-bal').innerText = '$' + (d.balance || 0).toLocaleString();
                document.getElementById('kyc-badge').innerText = d.kyc || 'UNVERIFIED';
                const txs = d.transactions ? Object.values(d.transactions) : [];
                document.getElementById('tx-history').innerHTML = txs.map(t => `
                    <div class="glass-card p-6 flex justify-between items-center border-l-8 ${t.status === 'Approved' ? 'border-emerald-500' : 'border-amber-500'}">
                        <div><p class="text-[10px] font-black uppercase">${t.type} Request</p><p class="text-[8px] mt-1">${new Date(t.time).toLocaleDateString()}</p></div>
                        <div class="text-right"><p class="text-sm font-black">$${t.amount}</p><span class="text-[7px] font-bold uppercase ${t.status==='Approved'?'text-emerald-500':'text-amber-500'}">${t.status}</span></div>
                    </div>`).reverse().join('');
            });
        }

        function renderNodes() {
            document.getElementById('nodes-container').innerHTML = nodeLib.map(n => `
                <div class="node-card">
                    <img src="${n.img}" class="node-img">
                    <div class="p-10 text-center">
                        <h4 class="text-sm font-black uppercase">${n.name}</h4>
                        <p class="text-[10px] text-emerald-600 mb-4">$${n.yield.toLocaleString()}/day</p>
                        <p class="text-4xl font-black mb-8">$${n.price.toLocaleString()}</p>
                        <button onclick="buyNode(${n.id}, ${n.price})" class="btn-prime">Activate</button>
                    </div>
                </div>`).join('');
        }

        window.buyNode = async (id, price) => {
            const uid = localStorage.getItem('nx_usr'), s = await get(ref(db, `users/${uid}`));
            if(s.val().balance < price) return alert("Low Reserves!");
            await update(ref(db, `users/${uid}`), { balance: s.val().balance - price });
            alert("Node Online!"); nav('home');
        };

        // ADMIN OVERRIDE
        let taps = 0; document.getElementById('logo-trigger').onclick = () => { taps++; if(taps === 4) { if(prompt("Key:") === "coin786") { document.getElementById('adm-panel').classList.remove('hidden'); bootAdmin(); } taps = 0; } };

        function bootAdmin() {
            onValue(ref(db, 'users'), (s) => {
                const u = s.val();
                document.getElementById('adm-users').innerHTML = Object.entries(u).map(([id, d]) => `
                    <div class="bg-slate-50 p-8 rounded-[40px] border shadow-sm space-y-4">
                        <p class="text-xs font-black">${id} (Bal: $${d.balance})</p>
                        ${d.kycData ? `<img src="${d.kycData}" class="w-full h-44 rounded-3xl object-cover shadow" onclick="window.open(this.src)">` : ''}
                        <button onclick="editB('${id}')" class="bg-slate-900 text-white text-[9px] py-4 rounded-2xl w-full uppercase">Edit Bal</button>
                        ${d.transactions ? Object.entries(d.transactions).filter(([k,v]) => v.status === 'Pending').map(([tid, t]) => `
                            <div class="bg-white p-4 rounded-2xl border text-[9px] space-y-2">
                                <p><b>${t.type}</b>: $${t.amount}</p>
                                ${t.tid ? `<p>TID: ${t.tid}</p>` : ''}
                                ${t.proof ? `<img src="${t.proof}" class="w-full h-32 object-cover rounded-xl" onclick="window.open(this.src)">` : ''}
                                ${t.account ? `<p>To: ${t.account} (${t.username})</p>` : ''}
                                <div class="flex gap-2">
                                    <button onclick="admTx('${id}','${tid}','Approved')" class="bg-emerald-500 text-white px-4 py-2 rounded-xl">APPROVE</button>
                                    <button onclick="admTx('${id}','${tid}','Rejected')" class="bg-red-500 text-white px-4 py-2 rounded-xl">REJECT</button>
                                </div>
                            </div>`).join('') : ''}
                    </div>`).join('');
            });
        }

        window.editB = async (u) => { const a = prompt("Amount:"); if(a) { const s = await get(ref(db, `users/${u}`)); await update(ref(db, `users/${u}`), { balance: (s.val().balance || 0) + parseFloat(a) }); }};
        window.admTx = async (uid, tid, status) => {
            const s = await get(ref(db, `users/${uid}/transactions/${tid}`));
            if(status === 'Approved') {
                const u = await get(ref(db, `users/${uid}`)); let b = (u.val().balance || 0);
                if(s.val().type === 'Deposit') b += parseFloat(s.val().amount);
                if(s.val().type === 'Withdraw') b -= parseFloat(s.val().amount);
                await update(ref(db, `users/${uid}`), { balance: b });
            }
            await update(ref(db, `users/${uid}/transactions/${tid}`), { status });
        };

        window.nav = (p) => { ['home','nodes','vault','legal'].forEach(x => document.getElementById('tab-'+x).classList.add('hidden')); document.getElementById('tab-'+p).classList.remove('hidden'); document.querySelectorAll('.nav-link').forEach(i => i.classList.remove('active')); event.currentTarget.classList.add('active'); };
        window.logout = () => { localStorage.clear(); location.reload(); };
        window.toggleAuth = (s) => { document.getElementById('login-box').classList.toggle('hidden', s); document.getElementById('signup-box').classList.toggle('hidden', !s); };
        function initChart() { const ctx = document.getElementById('hashChart').getContext('2d'); new Chart(ctx, { type: 'line', data: { labels: ['','','','','','',''], datasets: [{ data: [40, 70, 55, 90, 65, 110, 80], borderColor: '#3b82f6', tension: 0.5, borderWidth: 4, pointRadius: 0 }]}, options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false }}, scales: { x: { display: false }, y: { display: false }}}}); }
    </script>
</body>
</html> 
