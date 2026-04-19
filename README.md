<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS ELITE | Web3 Asset Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --bg: #010204; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .glass-panel { background: rgba(13, 17, 23, 0.8); backdrop-filter: blur(30px); border: 1px solid rgba(255,255,255,0.07); }
        .wallet-btn { background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.08); transition: 0.3s; cursor: pointer; }
        .wallet-btn:hover { border-color: var(--gold); background: rgba(243, 186, 47, 0.08); transform: translateY(-3px); }
        .ping-dot { height: 8px; width: 8px; border-radius: 50%; display: inline-block; animation: pulse 1.8s infinite; }
        @keyframes pulse { 0% { opacity: 1; transform: scale(1); } 50% { opacity: 0.3; transform: scale(1.4); } 100% { opacity: 1; transform: scale(1); } }
        .hidden-section { display: none; }
        .crypto-text { background: linear-gradient(90deg, #f3ba2f, #ffffff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        input { background: #0d1117 !important; border: 1px solid #21262d !important; color: white !important; outline: none !important; }
        input:focus { border-color: var(--gold) !important; }
    </style>
</head>
<body>

    <nav class="glass-panel sticky top-0 z-[100] px-8 py-5 flex items-center justify-between">
        <div class="flex items-center gap-3 cursor-pointer" onclick="checkAuth()">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="crypto-text">Elite</span></span>
        </div>
        <div id="auth-nav">
            <button onclick="showSection('signup')" class="bg-white text-black px-8 py-2.5 rounded-full font-black text-xs hover:scale-105 transition shadow-lg">CONNECT HUB</button>
        </div>
        <div id="user-nav" class="hidden flex items-center gap-4">
            <div class="text-right leading-none"><p id="nav-user-name" class="text-xs font-black text-[#f3ba2f] uppercase"></p><span class="text-[8px] text-green-500 font-bold tracking-widest">ENCRYPTED</span></div>
            <button onclick="logout()" class="w-10 h-10 rounded-full border border-red-500/20 bg-red-500/5 flex items-center justify-center text-sm">🚪</button>
        </div>
    </nav>

    <section id="landing-section" class="section py-32 px-6 text-center animate__animated animate__fadeIn">
        <div class="inline-flex items-center gap-3 bg-white/5 border border-white/10 px-5 py-2 rounded-full mb-10">
            <span class="ping-dot bg-green-500"></span><span class="text-[10px] font-black text-gray-400 uppercase tracking-[0.2em]">Institutional Network: Active</span>
        </div>
        <h1 class="text-7xl md:text-9xl font-black mb-8 italic leading-none tracking-tighter uppercase">Global <span class="crypto-text">Wealth</span><br>Settlement.</h1>
        <p class="text-gray-500 max-w-xl mx-auto mb-12 text-sm font-bold uppercase tracking-[0.4em]">The 2026 Standard for Digital Assets</p>
        <button onclick="showSection('signup')" class="bg-[#f3ba2f] text-black px-14 py-6 rounded-2xl font-black text-xl shadow-2xl hover:scale-105 transition">INITIATE ACCESS</button>
    </section>

    <section id="signup-section" class="section hidden-section flex justify-center py-24 px-6 animate__animated animate__zoomIn">
        <div class="glass-panel p-12 rounded-[45px] w-full max-w-md border border-yellow-500/20">
            <h2 class="text-3xl font-black mb-2 italic">CREATE NODE</h2>
            <p class="text-[10px] text-gray-500 mb-10 tracking-widest">PROTECTED BY AES-256 BIT ENCRYPTION</p>
            <div class="space-y-4">
                <input id="reg-name" type="text" placeholder="Legal Full Name" class="w-full p-4 rounded-2xl">
                <input id="reg-email" type="email" placeholder="Institutional Email" class="w-full p-4 rounded-2xl">
                <button onclick="register()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-2xl shadow-xl mt-4 uppercase text-sm">Authorize Session</button>
            </div>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10 animate__animated animate__fadeIn">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <div class="lg:col-span-2 glass-panel p-12 rounded-[50px] border-l-8 border-[#f3ba2f] relative overflow-hidden">
                <p class="text-[11px] font-black text-gray-500 uppercase tracking-widest mb-4">Current Asset Valuation</p>
                <h2 id="total-balance" class="text-6xl md:text-8xl font-black italic tracking-tighter mb-12">$0.00</h2>
                <div class="flex gap-5">
                    <button onclick="openModal('deposit')" class="flex-1 bg-[#f3ba2f] text-black py-5 rounded-3xl font-black text-xs uppercase shadow-xl">Deposit Assets</button>
                    <button onclick="openModal('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-5 rounded-3xl font-black text-xs uppercase hover:bg-white/10 transition">Withdraw</button>
                </div>
            </div>
            <div class="glass-panel p-10 rounded-[50px] flex flex-col justify-center gap-6">
                <div><p class="text-[10px] font-bold text-gray-500 uppercase mb-1">Global Node Rank</p><h3 class="text-3xl font-black text-[#f3ba2f]">#12,042</h3></div>
                <div><p class="text-[10px] font-bold text-gray-500 uppercase mb-1">Security Tier</p><h3 class="text-3xl font-black text-green-500">TITANIUM</h3></div>
                <div><p class="text-[10px] font-bold text-gray-500 uppercase mb-1">APY Yield</p><h3 class="text-3xl font-black text-blue-500">18.4%</h3></div>
            </div>
        </div>
    </section>

    <div id="deposit-modal" class="fixed inset-0 z-[200] bg-black/98 backdrop-blur-3xl hidden flex items-center justify-center p-6">
        <div class="glass-panel w-full max-w-xl rounded-[50px] p-12 animate__animated animate__fadeInUp border border-yellow-500/20">
            <div class="flex justify-between items-center mb-10">
                <h3 class="text-3xl font-black italic uppercase">Asset Gateway</h3>
                <button onclick="closeModals()" class="text-gray-500 text-4xl">&times;</button>
            </div>
            
            <p class="text-[10px] font-black text-gray-500 uppercase tracking-[0.3em] mb-6 text-center">Multi-Wallet Protocol</p>
            <div class="grid grid-cols-2 sm:grid-cols-3 gap-4 mb-10">
                <div onclick="setGateway('USDT')" class="wallet-btn p-5 rounded-3xl flex flex-col items-center gap-3">
                    <img src="https://cryptologos.cc/logos/tether-usdt-logo.svg" class="w-10 h-10">
                    <span class="text-[9px] font-black uppercase">Tron TRC20</span>
                </div>
                <div onclick="setGateway('METAMASK')" class="wallet-btn p-5 rounded-3xl flex flex-col items-center gap-3">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/3/36/MetaMask_Fox.svg" class="w-10 h-10">
                    <span class="text-[9px] font-black uppercase">MetaMask</span>
                </div>
                <div onclick="setGateway('TRUST')" class="wallet-btn p-5 rounded-3xl flex flex-col items-center gap-3">
                    <img src="https://trustwallet.com/assets/images/media/assets/trust_platform.svg" class="w-10 h-10">
                    <span class="text-[9px] font-black uppercase">Trust Wallet</span>
                </div>
            </div>

            <div id="deposit-form" class="space-y-5">
                <div class="bg-yellow-500/5 p-5 rounded-3xl border border-yellow-500/20">
                    <p id="gw-label" class="text-[9px] font-black text-yellow-500 uppercase mb-2">Primary TRC20 Address:</p>
                    <p id="gw-address" class="text-[11px] font-mono break-all font-bold tracking-tighter text-white">TK9UpEWhrtHJMCXAjAmXJndadPZn6Ce2n1</p>
                </div>
                <input id="d-amt" type="number" placeholder="Enter Amount (USD)" class="w-full p-5 rounded-2xl text-lg font-black">
                <input id="d-tid" type="text" placeholder="Transaction Hash / TID" class="w-full p-5 rounded-2xl text-xs font-mono">
                <button onclick="confirmDep()" class="w-full bg-[#f3ba2f] text-black font-black py-5 rounded-2xl shadow-xl uppercase text-sm tracking-widest">Verify Transfer</button>
            </div>
        </div>
    </div>

    <div id="withdraw-modal" class="fixed inset-0 z-[200] bg-black/98 hidden flex items-center justify-center p-6">
        <div class="glass-panel w-full max-w-md rounded-[50px] p-12 animate__animated animate__fadeInUp">
            <h3 class="text-3xl font-black italic uppercase mb-10 text-red-500">Liquidation</h3>
            <div class="space-y-5">
                <input id="w-name" type="text" placeholder="Beneficiary Name" class="w-full p-5 rounded-2xl">
                <input id="w-addr" type="text" placeholder="Destination Wallet Address" class="w-full p-5 rounded-2xl text-xs font-mono">
                <input id="w-amt" type="number" placeholder="Amount (USD)" class="w-full p-5 rounded-2xl text-2xl font-black">
                <button onclick="confirmWit()" class="w-full bg-white text-black font-black py-5 rounded-2xl shadow-xl uppercase">Extract Funds</button>
            </div>
        </div>
    </div>

    <script>
        let session = JSON.parse(localStorage.getItem('nexus_user')) || null;
        let balance = parseFloat(localStorage.getItem('nexus_bal')) || 25400.50;

        function checkAuth() {
            if(session) {
                showSection('dashboard');
                document.getElementById('auth-nav').classList.add('hidden');
                document.getElementById('user-nav').classList.remove('hidden');
                document.getElementById('nav-user-name').innerText = session.name;
                updateUI();
            } else {
                showSection('landing');
                document.getElementById('auth-nav').classList.remove('hidden');
                document.getElementById('user-nav').classList.add('hidden');
            }
        }

        function register() {
            const name = document.getElementById('reg-name').value;
            if(!name) return alert("Please specify node name, sweetie!");
            session = { name: name };
            localStorage.setItem('nexus_user', JSON.stringify(session));
            localStorage.setItem('nexus_bal', balance);
            checkAuth();
        }

        function logout() {
            localStorage.removeItem('nexus_user');
            location.reload();
        }

        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0,0);
        }

        function setGateway(type) {
            const label = document.getElementById('gw-label');
            const addr = document.getElementById('gw-address');
            if(type === 'USDT') {
                label.innerText = "Primary TRC20 Address:";
                addr.innerText = "TK9UpEWhrtHJMCXAjAmXJndadPZn6Ce2n1";
            } else if(type === 'METAMASK') {
                label.innerText = "MetaMask Web3 Hub:";
                addr.innerText = "0x742d35Cc6634C0532925a3b844Bc454e4438f44e";
            } else {
                label.innerText = "Trust Wallet Core:";
                addr.innerText = "bnb1grpf0955u0800ed873as9jzrsh96vxy0";
            }
        }

        function openModal(id) { document.getElementById(id + '-modal').classList.remove('hidden'); }
        function closeModals() { document.querySelectorAll('[id$="-modal"]').forEach(m => m.classList.add('hidden')); }

        function confirmDep() {
            if(!document.getElementById('d-amt').value || !document.getElementById('d-tid').value) return alert("Security audit failed: Fill all fields, sweetie!");
            alert("Verification Protocol: Your assets are being analyzed by our Global Nodes.");
            closeModals();
        }

        function confirmWit() {
            const amt = parseFloat(document.getElementById('w-amt').value);
            if(!amt || amt > balance) return alert("Liquidity Error: Insufficient balance!");
            balance -= amt;
            localStorage.setItem('nexus_bal', balance);
            updateUI();
            alert("Settlement Successful: Funds dispatched to network.");
            closeModals();
        }

        function updateUI() {
            document.getElementById('total-balance').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
        }

        window.onload = checkAuth;
    </script>
</body>
</html>
