<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS CORE | Institutional Mining Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --bg: #010204; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .glass { background: rgba(15, 18, 23, 0.9); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.06); }
        .sidebar { transform: translateX(100%); transition: 0.5s cubic-bezier(0.4, 0, 0.2, 1); }
        .sidebar.active { transform: translateX(0); }
        .crypto-text { background: linear-gradient(90deg, #f3ba2f, #ffffff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .hidden-section { display: none; }
        input { background: #0d1117 !important; border: 1px solid #21262d !important; color: white !important; outline: none !important; border-radius: 12px; }
        .node-card { transition: all 0.3s ease; border: 1px solid rgba(255,255,255,0.03); }
        .node-card:hover { border-color: var(--gold); transform: translateY(-5px); box-shadow: 0 10px 30px rgba(243, 186, 47, 0.1); }
        .ping { height: 6px; width: 6px; border-radius: 50%; background: #10b981; display: inline-block; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.3; } 100% { opacity: 1; } }
        ::-webkit-scrollbar { width: 5px; }
        ::-webkit-scrollbar-thumb { background: var(--gold); border-radius: 10px; }
    </style>
</head>
<body>

    <nav class="glass sticky top-0 z-[100] px-6 py-4 flex items-center justify-between border-b border-white/5">
        <div class="flex items-center gap-3 cursor-pointer" onclick="location.reload()">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl shadow-lg">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="crypto-text">Core</span></span>
        </div>
        <div class="flex items-center gap-4">
            <div id="user-tag" class="hidden text-right hidden sm:block">
                <p id="user-name-display" class="text-[10px] font-black text-[#f3ba2f] uppercase"></p>
                <p class="text-[7px] text-green-500 font-bold tracking-[0.3em]">SECURE NODE</p>
            </div>
            <button onclick="toggleMenu()" class="w-10 h-10 flex flex-col items-center justify-center gap-1.5 glass rounded-full">
                <div class="w-5 h-0.5 bg-white"></div>
                <div class="w-5 h-0.5 bg-white"></div>
                <div class="w-5 h-0.5 bg-white"></div>
            </button>
        </div>
    </nav>

    <div id="sidebar-menu" class="sidebar fixed top-0 right-0 h-full w-full max-w-xs glass z-[200] p-10 shadow-2xl">
        <div class="flex justify-between items-center mb-12">
            <h3 class="font-black italic uppercase tracking-widest text-sm">Institutional Menu</h3>
            <button onclick="toggleMenu()" class="text-4xl text-gray-500">&times;</button>
        </div>
        <div class="space-y-6">
            <button onclick="showSection('dashboard'); toggleMenu()" class="w-full text-left font-bold text-xs hover:text-[#f3ba2f] transition tracking-widest uppercase">🏠 Dashboard</button>
            <button onclick="showPolicy('history'); toggleMenu()" class="w-full text-left font-bold text-xs hover:text-[#f3ba2f] transition tracking-widest uppercase">📜 Ledger History</button>
            <button onclick="showPolicy('company'); toggleMenu()" class="w-full text-left font-bold text-xs hover:text-[#f3ba2f] transition tracking-widest uppercase">🏢 Company Info</button>
            <button onclick="showPolicy('privacy'); toggleMenu()" class="w-full text-left font-bold text-xs hover:text-[#f3ba2f] transition tracking-widest uppercase">🛡️ Privacy Protocol</button>
            <div class="pt-10"><button onclick="logout()" class="w-full text-left font-black text-xs text-red-500 tracking-widest uppercase">🚪 Terminate Session</button></div>
        </div>
    </div>

    <section id="landing-section" class="section py-32 px-6 text-center animate__animated animate__fadeIn">
        <div class="inline-flex items-center gap-3 bg-white/5 border border-white/10 px-5 py-2 rounded-full mb-10">
            <span class="ping"></span><span class="text-[8px] font-black text-gray-500 uppercase tracking-[0.3em]">Quantum Shield v4.2 Active</span>
        </div>
        <h1 class="text-6xl md:text-9xl font-black mb-8 italic tracking-tighter leading-none uppercase">Nexus<br><span class="crypto-text">Mining.</span></h1>
        <p class="text-gray-400 max-w-lg mx-auto mb-12 text-xs font-bold uppercase tracking-[0.5em]">Global Decentralized Payouts</p>
        <button onclick="showSection('auth')" class="bg-[#f3ba2f] text-black px-12 py-5 rounded-2xl font-black text-xl shadow-2xl hover:scale-105 transition">ENTER HUB</button>
    </section>

    <section id="auth-section" class="section hidden-section flex justify-center py-24 px-6 animate__animated animate__zoomIn">
        <div class="glass p-10 rounded-[40px] w-full max-w-md">
            <h2 class="text-2xl font-black mb-8 italic uppercase tracking-tighter">Initialize Node</h2>
            <div class="space-y-4">
                <input id="reg-name" type="text" placeholder="Full Legal Name" class="w-full p-4 text-xs">
                <input id="reg-email" type="email" placeholder="Institutional Email" class="w-full p-4 text-xs">
                <button onclick="login()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl mt-4 uppercase text-[10px] tracking-widest">Connect</button>
            </div>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10 animate__animated animate__fadeIn">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-12">
            <div class="lg:col-span-2 glass p-10 rounded-[45px] border-l-[12px] border-[#f3ba2f]">
                <p class="text-[10px] font-black text-gray-500 uppercase tracking-widest mb-4">Node Balance (USD)</p>
                <h2 id="balance-display" class="text-6xl md:text-8xl font-black italic tracking-tighter mb-12">$0.00</h2>
                <div class="flex gap-4">
                    <button onclick="openModal('deposit')" class="flex-1 bg-[#f3ba2f] text-black py-5 rounded-2xl font-black text-xs uppercase shadow-xl hover:brightness-110">Deposit</button>
                    <button onclick="openModal('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-5 rounded-2xl font-black text-xs uppercase hover:bg-white/10">Withdraw</button>
                </div>
            </div>
            <div class="glass p-8 rounded-[45px] flex flex-col justify-center space-y-6">
                <div><p class="text-[9px] font-black text-gray-500 uppercase">Mining Power</p><h3 class="text-3xl font-black text-[#f3ba2f]">1.24 TH/s</h3></div>
                <div><p class="text-[9px] font-black text-gray-500 uppercase">Uptime</p><h3 class="text-3xl font-black text-green-500 uppercase italic">99.9%</h3></div>
            </div>
        </div>

        <h3 class="text-sm font-black italic uppercase mb-8 tracking-[0.3em] text-gray-500">Global Mining Clusters</h3>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6 mb-16">
            <script>
                const nodeData = [
                    {n: "Alpha", l: "Dubai, UAE", m: 15, y: 1.5},
                    {n: "Beta", l: "London, UK", m: 50, y: 2.2},
                    {n: "Gamma", l: "Singapore", m: 100, y: 3.0},
                    {n: "Delta", l: "Frankfurt, DE", m: 250, y: 3.8},
                    {n: "Epsilon", l: "Tokyo, JP", m: 500, y: 4.5},
                    {n: "Zeta", l: "Zurich, CH", m: 800, y: 5.5},
                    {n: "Eta", l: "Toronto, CA", m: 1200, y: 6.8},
                    {n: "Theta", l: "Sydney, AU", m: 2000, y: 8.2},
                    {n: "Iota", l: "Stockholm, SE", m: 3500, y: 10.5},
                    {n: "Kappa", l: "Hong Kong", m: 5000, y: 12.0},
                    {n: "Lambda", l: "Reykjavik, IS", m: 7500, y: 15.0},
                    {n: "Omega", l: "Starlink Sat", m: 10000, y: 20.0}
                ];

                document.write(nodeData.map(node => `
                    <div class="node-card glass p-8 rounded-[35px] relative overflow-hidden group">
                        <div class="flex justify-between items-start mb-6">
                            <div>
                                <p class="text-[8px] font-black text-[#f3ba2f] uppercase tracking-widest mb-1">Node ${node.n}</p>
                                <h4 class="text-lg font-black italic uppercase text-white">${node.l}</h4>
                            </div>
                            <span class="ping"></span>
                        </div>
                        <div class="space-y-3 mb-8">
                            <div class="flex justify-between text-[10px]"><span class="text-gray-500 font-bold uppercase">Entry:</span><span class="font-black text-white">$${node.m}</span></div>
                            <div class="flex justify-between text-[10px]"><span class="text-gray-500 font-bold uppercase">Daily Profit:</span><span class="font-black text-green-500">$${(node.m * node.y / 100).toFixed(2)}</span></div>
                            <div class="flex justify-between text-[10px]"><span class="text-gray-500 font-bold uppercase">30D Total:</span><span class="font-black text-[#f3ba2f]">$${(node.m * node.y / 100 * 30).toFixed(2)}</span></div>
                        </div>
                        <div class="bg-white/5 rounded-xl p-3 mb-6 text-center">
                            <p class="text-[8px] font-black text-gray-500 uppercase mb-1">Next Payout In</p>
                            <p class="text-xs font-mono font-black text-white countdown">23:59:59</p>
                        </div>
                        <button onclick="openModal('deposit')" class="w-full py-4 bg-white/5 rounded-2xl text-[9px] font-black uppercase tracking-[0.2em] group-hover:bg-[#f3ba2f] group-hover:text-black transition duration-500">Activate Node</button>
                    </div>
                `).join(''));
            </script>
        </div>

        <div class="glass p-10 rounded-[50px] max-w-4xl mx-auto">
            <h4 class="text-xs font-black uppercase tracking-widest mb-10 flex items-center gap-3">
                <span class="w-2 h-2 bg-[#f3ba2f] rounded-full"></span> Live Terminal Ledger
            </h4>
            <div id="history-box" class="space-y-6">
                <p class="text-xs text-gray-600 italic">Decrypting ledger activity...</p>
            </div>
        </div>
    </section>

    <div id="deposit-modal" class="fixed inset-0 z-[300] bg-black/98 backdrop-blur-3xl hidden flex items-center justify-center p-6">
        <div class="glass w-full max-w-lg rounded-[50px] p-10 animate__animated animate__fadeInUp">
            <div class="flex justify-between items-center mb-8">
                <h3 class="text-2xl font-black italic uppercase">Funding</h3>
                <button onclick="closeModals()" class="text-gray-500 text-4xl">&times;</button>
            </div>
            <div class="flex gap-2 mb-8 overflow-x-auto pb-2">
                <button onclick="setGate('BINANCE')" class="bg-white/5 px-6 py-2 rounded-full text-[9px] font-black border border-white/10 hover:border-[#f3ba2f] transition">BINANCE (TRC20)</button>
                <button onclick="setGate('METAMASK')" class="bg-white/5 px-6 py-2 rounded-full text-[9px] font-black border border-white/10 hover:border-[#f3ba2f] transition">METAMASK (ETH)</button>
                <button onclick="setGate('TRUST')" class="bg-white/5 px-6 py-2 rounded-full text-[9px] font-black border border-white/10 hover:border-[#f3ba2f] transition">TRUST (TRX)</button>
            </div>
            <div class="bg-yellow-500/5 p-6 rounded-3xl border border-yellow-500/20 mb-8">
                <p id="gate-name" class="text-[9px] font-black text-yellow-500 mb-2 uppercase tracking-widest">Binance USDT (TRC20):</p>
                <p id="gate-addr" class="text-[11px] font-mono font-bold break-all text-white">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
            </div>
            <div class="space-y-4">
                <input id="d-amt" type="number" placeholder="Deposit Amount (USD)" class="w-full p-4 font-black text-sm">
                <input id="d-hash" type="text" placeholder="TX Hash / Transaction ID" class="w-full p-4 text-[10px] font-mono uppercase">
                <button onclick="confirmDep()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl uppercase text-[10px] tracking-widest">Submit Verification</button>
            </div>
        </div>
    </div>

    <div id="withdraw-modal" class="fixed inset-0 z-[300] bg-black/98 hidden flex items-center justify-center p-6">
        <div class="glass w-full max-w-md rounded-[50px] p-10 animate__animated animate__fadeInDown">
            <h3 class="text-2xl font-black italic mb-8 uppercase text-red-500">Liquidate</h3>
            <input id="w-addr" type="text" placeholder="Withdrawal Wallet Address" class="w-full p-4 mb-4 text-xs font-mono">
            <input id="w-amt" type="number" placeholder="Amount (USD)" class="w-full p-6 mb-8 text-3xl font-black text-center">
            <button onclick="confirmWit()" class="w-full bg-white text-black font-black py-4 rounded-xl shadow-xl uppercase text-[10px] tracking-widest">Authorize Extract</button>
        </div>
    </div>

    <div id="policy-modal" class="fixed inset-0 z-[400] bg-black/98 hidden overflow-y-auto p-10">
        <div class="max-w-2xl mx-auto">
            <div class="flex justify-between items-center mb-10">
                <h2 id="policy-title" class="text-3xl font-black italic uppercase"></h2>
                <button onclick="closePolicy()" class="text-5xl">&times;</button>
            </div>
            <div id="policy-body" class="text-gray-400 space-y-6 italic leading-relaxed text-sm"></div>
        </div>
    </div>

    <script>
        let user = JSON.parse(localStorage.getItem('nexus_user')) || null;
        let balance = parseFloat(localStorage.getItem('nexus_bal')) || 12450.75;
        let history = JSON.parse(localStorage.getItem('nexus_history')) || [];

        function checkAuth() {
            if(user) {
                showSection('dashboard');
                document.getElementById('user-tag').classList.remove('hidden');
                document.getElementById('user-name-display').innerText = user.name;
                updateUI();
                startCountdown();
                generateLiveActivity();
            } else {
                showSection('landing');
            }
        }

        function login() {
            const n = document.getElementById('reg-name').value;
            if(!n) return alert("Security Trace: Please enter legal name, sweetie!");
            user = { name: n };
            localStorage.setItem('nexus_user', JSON.stringify(user));
            localStorage.setItem('nexus_bal', balance);
            checkAuth();
        }

        function logout() { localStorage.clear(); location.reload(); }
        function toggleMenu() { document.getElementById('sidebar-menu').classList.toggle('active'); }
        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0,0);
        }

        function openModal(id) { document.getElementById(id + '-modal').classList.remove('hidden'); }
        function closeModals() { document.querySelectorAll('[id$="-modal"]').forEach(m => m.classList.add('hidden')); }

        function setGate(type) {
            const gn = document.getElementById('gate-name');
            const ga = document.getElementById('gate-addr');
            if(type === 'BINANCE') { gn.innerText = "Binance USDT (TRC20):"; ga.innerText = "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ"; }
            else if(type === 'METAMASK') { gn.innerText = "MetaMask (ETH / ERC20):"; ga.innerText = "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355"; }
            else { gn.innerText = "Trust Wallet (TRX / TRC20):"; ga.innerText = "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76"; }
        }

        function confirmDep() {
            const a = document.getElementById('d-amt').value;
            if(!a) return alert("Specify amount!");
            history.unshift({ type: 'DEPOSIT', amt: a, date: new Date().toLocaleString(), status: 'PENDING' });
            localStorage.setItem('nexus_history', JSON.stringify(history));
            alert("Protocol Broadcasted: Verifying assets on mainnet nodes...");
            updateUI(); closeModals();
        }

        function confirmWit() {
            const a = parseFloat(document.getElementById('w-amt').value);
            if(!a || a > balance) return alert("Liquidity Error: Insufficient funds!");
            balance -= a;
            localStorage.setItem('nexus_bal', balance);
            history.unshift({ type: 'WITHDRAW', amt: a, date: new Date().toLocaleString(), status: 'SETTLED' });
            localStorage.setItem('nexus_history', JSON.stringify(history));
            alert("Authorization Granted: Payout dispatched.");
            updateUI(); closeModals();
        }

        function updateUI() {
            document.getElementById('balance-display').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
            const box = document.getElementById('history-box');
            if(history.length > 0) {
                box.innerHTML = history.slice(0, 5).map(i => `
                    <div class="flex justify-between border-b border-white/5 py-5 px-2 hover:bg-white/5 transition rounded-2xl">
                        <div><p class="text-[9px] font-black text-[#f3ba2f] tracking-widest">${i.type}</p><p class="text-[8px] text-gray-600 font-bold italic mt-1">${i.date}</p></div>
                        <div class="text-right"><p class="text-xs font-mono font-black">$${parseFloat(i.amt).toLocaleString()}</p><p class="text-[8px] font-black ${i.status === 'PENDING' ? 'text-yellow-500' : 'text-green-500'} mt-1">${i.status}</p></div>
                    </div>
                `).join('');
            }
        }

        function startCountdown() {
            setInterval(() => {
                document.querySelectorAll('.countdown').forEach(el => {
                    let time = el.innerText.split(':');
                    let h = parseInt(time[0]), m = parseInt(time[1]), s = parseInt(time[2]);
                    if (s > 0) s--; else { s = 59; if (m > 0) m--; else { m = 59; if (h > 0) h--; else h = 23; } }
                    el.innerText = `${String(h).padStart(2, '0')}:${String(m).padStart(2, '0')}:${String(s).padStart(2, '0')}`;
                });
            }, 1000);
        }

        function generateLiveActivity() {
            const names = ["0x4e2...","0x91d...","0x77b...","User_882","Institutional_X"];
            setInterval(() => {
                if(history.length < 10) {
                    const randomName = names[Math.floor(Math.random()*names.length)];
                    const randomAmt = (Math.random() * 5000 + 100).toFixed(2);
                    console.log(`Node Pulse: ${randomName} active.`);
                }
            }, 5000);
        }

        function showPolicy(type) {
            const modal = document.getElementById('policy-modal');
            const title = document.getElementById('policy-title');
            const body = document.getElementById('policy-body');
            modal.classList.remove('hidden');
            if(type === 'privacy') {
                title.innerText = "Privacy Protocol";
                body.innerHTML = "<p>Nexus Terminal uses end-to-end AES-256 encryption. We do not store biometric or private key data on centralized nodes.</p>";
            } else if(type === 'company') {
                title.innerText = "Nexus Institutional";
                body.innerHTML = "<p>Global leaders in high-frequency mining liquidity since 2024. Operating 142 clusters across 12 countries.</p>";
            } else {
                title.innerText = "Encrypted Ledger";
                body.innerHTML = history.length > 0 ? history.map(i => `<div class='py-4 border-b border-white/5 text-xs font-mono'><span class='text-[#f3ba2f]'>${i.date}</span> | ${i.type} | $${i.amt}</div>`).join('') : "No data.";
            }
        }

        function closePolicy() { document.getElementById('policy-modal').classList.add('hidden'); }
        window.onload = checkAuth;
    </script>
</body>
</html>
