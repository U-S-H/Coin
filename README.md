<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS CORE | Institutional Web3 Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --bg: #020406; --card: #0d1117; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .glass-panel { background: rgba(13, 17, 23, 0.75); backdrop-filter: blur(25px); border: 1px solid rgba(255,255,255,0.06); }
        .wallet-btn { background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.08); transition: 0.3s; cursor: pointer; }
        .wallet-btn:hover { border-color: var(--gold); background: rgba(243, 186, 47, 0.05); transform: translateY(-3px); }
        .ping-dot { height: 8px; width: 8px; border-radius: 50%; display: inline-block; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0% { opacity: 1; transform: scale(1); } 50% { opacity: 0.3; transform: scale(1.3); } 100% { opacity: 1; transform: scale(1); } }
        .hidden-section { display: none; }
        .crypto-gradient { background: linear-gradient(90deg, #f3ba2f, #ffaa00); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        input, select { background: #161a1e !important; border: 1px solid #2b3139 !important; color: white !important; outline: none !important; }
        input:focus { border-color: var(--gold) !important; }
    </style>
</head>
<body>

    <nav class="glass-panel sticky top-0 z-[100] px-8 py-4 flex items-center justify-between border-b border-white/5">
        <div class="flex items-center gap-3 cursor-pointer" onclick="checkAuth()">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl shadow-lg shadow-yellow-500/20">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="crypto-gradient">Core</span></span>
        </div>
        
        <div id="auth-nav" class="flex gap-4">
            <button onclick="showSection('signup')" class="bg-white text-black px-6 py-2 rounded-full font-black text-xs hover:bg-[#f3ba2f] transition shadow-lg">CONNECT</button>
        </div>

        <div id="user-nav" class="hidden flex items-center gap-4">
            <div class="text-right leading-none">
                <p id="user-display-name" class="text-xs font-black text-[#f3ba2f] uppercase tracking-widest"></p>
                <span class="text-[8px] text-green-500 font-bold">NODE: ONLINE</span>
            </div>
            <button onclick="logout()" class="w-10 h-10 rounded-full border border-red-500/30 flex items-center justify-center bg-gray-900 text-sm hover:bg-red-500/10">🚪</button>
        </div>
    </nav>

    <section id="landing-section" class="section py-28 px-6 text-center animate__animated animate__fadeIn">
        <div class="inline-flex items-center gap-3 bg-white/5 border border-white/10 px-4 py-1.5 rounded-full mb-8">
            <span class="ping-dot bg-green-500"></span>
            <span class="text-[10px] font-bold text-gray-400 uppercase tracking-widest">Quantum Ledger Active: 2026 Edition</span>
        </div>
        <h1 class="text-7xl md:text-9xl font-black mb-8 italic tracking-tighter leading-none">THE <span class="crypto-gradient">ELITE</span><br>TERMINAL.</h1>
        <p class="text-gray-500 max-w-xl mx-auto mb-12 text-sm font-bold uppercase tracking-[0.3em]">Institutional Grade Digital Asset Management</p>
        <button onclick="showSection('signup')" class="bg-[#f3ba2f] text-black px-12 py-5 rounded-2xl font-black text-xl shadow-2xl hover:scale-105 transition">INITIALIZE SESSION</button>
    </section>

    <section id="signup-section" class="section hidden-section flex justify-center py-20 px-6 animate__animated animate__zoomIn">
        <div class="glass-panel p-12 rounded-[40px] w-full max-w-md border border-yellow-500/20">
            <h2 class="text-3xl font-black mb-2 italic uppercase">Join Network</h2>
            <p class="text-[10px] text-gray-500 mb-8 tracking-widest">SECURE BIOMETRIC ENCRYPTION ACTIVE</p>
            <div class="space-y-4">
                <input id="auth-username" type="text" placeholder="Full Legal Name" class="w-full p-4 rounded-xl">
                <input id="auth-email" type="email" placeholder="Institutional Email" class="w-full p-4 rounded-xl">
                <button onclick="performSignup()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl">AUTHORIZE PORTFOLIO</button>
                <p class="text-center text-[10px] text-gray-600 mt-4 italic">By joining, you agree to 2026 Global Asset Terms.</p>
            </div>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10 animate__animated animate__fadeIn">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-10">
            <div class="lg:col-span-2 glass-panel p-10 rounded-[40px] border-l-8 border-[#f3ba2f]">
                <p class="text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-2">Total Managed Liquidity</p>
                <h2 id="balance-val" class="text-6xl md:text-7xl font-black tracking-tighter italic mb-10">$0.00</h2>
                <div class="flex gap-4">
                    <button onclick="openModal('deposit')" class="flex-1 bg-[#f3ba2f] text-black py-4 rounded-2xl font-black text-xs uppercase shadow-lg">Add Assets</button>
                    <button onclick="openModal('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-4 rounded-2xl font-black text-xs uppercase hover:bg-white/10">Extract</button>
                </div>
            </div>

            <div class="glass-panel p-8 rounded-[40px] flex flex-col justify-center">
                <h4 class="text-[10px] font-black text-gray-500 uppercase mb-6 tracking-widest">Infrastructure Status</h4>
                <div class="space-y-4">
                    <div class="flex justify-between items-center"><span class="text-xs text-gray-400">Node Latency</span><span class="text-xs font-mono text-green-500">~14ms</span></div>
                    <div class="flex justify-between items-center"><span class="text-xs text-gray-400">Validator Nodes</span><span class="text-xs font-mono">21 Active</span></div>
                    <div class="flex justify-between items-center"><span class="text-xs text-gray-400">Secure Protocol</span><span class="text-[9px] font-black text-blue-500 uppercase tracking-tighter">Quantum Guard v2</span></div>
                </div>
            </div>
        </div>

        <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
            <div class="glass-panel p-6 rounded-3xl text-center border-b-2 border-green-500">
                <span class="ping-dot bg-green-500 mb-2"></span>
                <p class="text-[10px] font-black uppercase text-gray-400">HKG-Node</p>
            </div>
            <div class="glass-panel p-6 rounded-3xl text-center border-b-2 border-green-500">
                <span class="ping-dot bg-green-500 mb-2"></span>
                <p class="text-[10px] font-black uppercase text-gray-400">DXB-Node</p>
            </div>
            <div class="glass-panel p-6 rounded-3xl text-center border-b-2 border-yellow-500">
                <span class="ping-dot bg-yellow-500 mb-2"></span>
                <p class="text-[10px] font-black uppercase text-gray-400">NYC-Node</p>
            </div>
            <div class="glass-panel p-6 rounded-3xl text-center border-b-2 border-green-500">
                <span class="ping-dot bg-green-500 mb-2"></span>
                <p class="text-[10px] font-black uppercase text-gray-400">LON-Node</p>
            </div>
        </div>
    </section>

    <div id="deposit-modal" class="fixed inset-0 z-[200] bg-black/98 backdrop-blur-3xl hidden flex items-center justify-center p-6">
        <div class="glass-panel w-full max-w-lg rounded-[40px] p-10 animate__animated animate__fadeInUp border border-yellow-500/20">
            <div class="flex justify-between items-center mb-8">
                <h3 class="text-2xl font-black italic uppercase">Asset Gateway</h3>
                <button onclick="closeModals()" class="text-gray-500 text-3xl">&times;</button>
            </div>
            
            <div class="grid grid-cols-2 sm:grid-cols-3 gap-4 mb-8">
                <button onclick="walletSim('MetaMask')" class="wallet-btn p-4 rounded-2xl flex flex-col items-center gap-2">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/3/36/MetaMask_Fox.svg" class="w-8 h-8">
                    <span class="text-[9px] font-black tracking-widest">METAMASK</span>
                </button>
                <button onclick="walletSim('Trust Wallet')" class="wallet-btn p-4 rounded-2xl flex flex-col items-center gap-2">
                    <img src="https://trustwallet.com/assets/images/media/assets/trust_platform.svg" class="w-8 h-8">
                    <span class="text-[9px] font-black tracking-widest">TRUST</span>
                </button>
                <button onclick="walletSim('Binance Pay')" class="wallet-btn p-4 rounded-2xl flex flex-col items-center gap-2">
                    <img src="https://cryptologos.cc/logos/binance-coin-bnb-logo.svg" class="w-8 h-8">
                    <span class="text-[9px] font-black tracking-widest">BINANCE</span>
                </button>
            </div>

            <div class="space-y-4">
                <div class="bg-yellow-500/5 p-4 rounded-2xl border border-yellow-500/20">
                    <p class="text-[9px] font-black text-yellow-500 uppercase mb-2">Company USDT Address (TRC20)</p>
                    <p class="text-[10px] font-mono break-all font-bold tracking-tighter">TLy2n1R7xP9qW23mXyZ99Vv2N8pQxR2</p>
                </div>
                <input id="dep-amt" type="number" placeholder="Deposit Amount (USD)" class="w-full p-4 rounded-xl">
                <input id="dep-hash" type="text" placeholder="Transaction Hash / TID" class="w-full p-4 rounded-xl text-xs">
                <button onclick="submitDep()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl">SUBMIT PROOF</button>
            </div>
        </div>
    </div>

    <div id="withdraw-modal" class="fixed inset-0 z-[200] bg-black/98 hidden flex items-center justify-center p-6">
        <div class="glass-panel w-full max-w-md rounded-[40px] p-10 animate__animated animate__fadeInUp">
            <h3 class="text-2xl font-black italic uppercase mb-8">Payout Request</h3>
            <div class="space-y-4">
                <input id="wit-name" type="text" placeholder="Account Holder Name" class="w-full p-4 rounded-xl text-sm">
                <input id="wit-addr" type="text" placeholder="Wallet Address / IBAN" class="w-full p-4 rounded-xl text-xs font-mono">
                <input id="wit-amt" type="number" placeholder="Extract Amount (USD)" class="w-full p-4 rounded-xl text-xl font-black">
                <button onclick="submitWit()" class="w-full bg-white text-black font-black py-4 rounded-xl shadow-xl">INITIATE WITHDRAWAL</button>
            </div>
        </div>
    </div>

    <script>
        // CORE AUTH LOGIC (LOCAL STORAGE)
        let userSession = JSON.parse(localStorage.getItem('nexus_session')) || null;
        let balance = parseFloat(localStorage.getItem('nexus_balance')) || 12500.00;

        function checkAuth() {
            if(userSession) {
                showSection('dashboard');
                document.getElementById('auth-nav').classList.add('hidden');
                document.getElementById('user-nav').classList.remove('hidden');
                document.getElementById('user-display-name').innerText = userSession.name;
                updateBalanceUI();
            } else {
                showSection('landing');
                document.getElementById('auth-nav').classList.remove('hidden');
                document.getElementById('user-nav').classList.add('hidden');
            }
        }

        function performSignup() {
            const name = document.getElementById('auth-username').value;
            const email = document.getElementById('auth-email').value;
            if(!name || !email) return alert("Please provide credentials, sweetie!");

            userSession = { name: name, email: email };
            localStorage.setItem('nexus_session', JSON.stringify(userSession));
            localStorage.setItem('nexus_balance', balance);
            
            checkAuth();
        }

        function logout() {
            localStorage.removeItem('nexus_session');
            userSession = null;
            location.reload();
        }

        // NAVIGATION LOGIC
        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0,0);
        }

        // TRANSACTION LOGIC
        function openModal(id) { document.getElementById(id + '-modal').classList.remove('hidden'); }
        function closeModals() { document.querySelectorAll('[id$="-modal"]').forEach(m => m.classList.add('hidden')); }

        function walletSim(wallet) {
            alert(`Initializing hand-shake with ${wallet} Extension... Please authorize the request on your device.`);
        }

        function submitDep() {
            const amt = document.getElementById('dep-amt').value;
            const hash = document.getElementById('dep-hash').value;
            if(!amt || !hash) return alert("All fields are mandatory for audit, sweetie!");
            alert("Verification Started: Our nodes are validating your transaction on the blockchain.");
            closeModals();
        }

        function submitWit() {
            const amt = parseFloat(document.getElementById('wit-amt').value);
            if(!amt || amt > balance) return alert("Insufficient Liquidity!");
            balance -= amt;
            localStorage.setItem('nexus_balance', balance);
            updateBalanceUI();
            alert("Extraction Success: Settlement will be processed within institutional hours.");
            closeModals();
        }

        function updateBalanceUI() {
            document.getElementById('balance-val').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
        }

        // Initialize on Load
        window.onload = checkAuth;
    </script>
</body>
</html>
