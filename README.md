<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS CORE | Institutional Asset Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --bg: #010204; --glass: rgba(15, 18, 23, 0.85); }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .glass-card { background: var(--glass); backdrop-filter: blur(30px); border: 1px solid rgba(255,255,255,0.06); }
        .crypto-glow { background: linear-gradient(90deg, #f3ba2f, #ffffff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .ping { height: 8px; width: 8px; background: #10b981; border-radius: 50%; display: inline-block; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { opacity: 1; transform: scale(1); } 50% { opacity: 0.3; transform: scale(1.5); } 100% { opacity: 1; transform: scale(1); } }
        .hidden-section { display: none; }
        input, select { background: #0d1117 !important; border: 1px solid #21262d !important; color: white !important; border-radius: 12px !important; outline: none !important; }
        input:focus { border-color: var(--gold) !important; box-shadow: 0 0 10px rgba(243, 186, 47, 0.1); }
        .market-ticker { white-space: nowrap; animation: ticker 30s linear infinite; }
        @keyframes ticker { 0% { transform: translateX(100%); } 100% { transform: translateX(-100%); } }
    </style>
</head>
<body>

    <div class="bg-[#f3ba2f]/10 border-b border-white/5 py-2 overflow-hidden">
        <div class="market-ticker flex gap-10 text-[10px] font-black uppercase tracking-widest text-[#f3ba2f]">
            <span>BTC: $68,241.50 <span class="text-green-500">▲ 2.4%</span></span>
            <span>ETH: $3,412.10 <span class="text-red-500">▼ 0.8%</span></span>
            <span>USDT: $1.00 <span class="text-blue-500">STABLE</span></span>
            <span>BNB: $582.00 <span class="text-green-500">▲ 1.1%</span></span>
            <span>SOL: $142.30 <span class="text-green-500">▲ 5.6%</span></span>
        </div>
    </div>

    <nav class="glass-card sticky top-0 z-[100] px-8 py-5 flex items-center justify-between border-b border-white/5">
        <div class="flex items-center gap-3 cursor-pointer" onclick="checkAuth()">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl shadow-lg">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="crypto-glow">Core</span></span>
        </div>
        <div id="auth-nav">
            <button onclick="showSection('signup')" class="bg-white text-black px-8 py-2.5 rounded-full font-black text-xs hover:bg-[#f3ba2f] transition shadow-lg">ACCESS TERMINAL</button>
        </div>
        <div id="user-nav" class="hidden flex items-center gap-5">
            <div class="text-right"><p id="display-name" class="text-[10px] font-black text-[#f3ba2f] uppercase"></p><p class="text-[8px] text-gray-500 font-bold">VERIFIED NODE</p></div>
            <button onclick="logout()" class="w-10 h-10 rounded-full border border-red-500/20 bg-red-500/5 flex items-center justify-center text-sm">🚪</button>
        </div>
    </nav>

    <section id="landing-section" class="section py-32 px-6 text-center animate__animated animate__fadeIn">
        <div class="inline-flex items-center gap-3 bg-white/5 border border-white/10 px-5 py-1.5 rounded-full mb-8">
            <span class="ping"></span> <span class="text-[10px] font-black text-gray-400 uppercase tracking-widest">Quantum Guard v2.0 Active</span>
        </div>
        <h1 class="text-7xl md:text-9xl font-black mb-8 italic tracking-tighter leading-none">SECURE<br><span class="crypto-glow">LIQUIDITY.</span></h1>
        <p class="text-gray-500 max-w-xl mx-auto mb-12 text-sm font-bold uppercase tracking-[0.4em]">The New Standard for Institutional Assets</p>
        <button onclick="showSection('signup')" class="bg-[#f3ba2f] text-black px-14 py-6 rounded-2xl font-black text-xl shadow-2xl hover:scale-105 transition">ENTER HUB</button>
    </section>

    <section id="signup-section" class="section hidden-section flex justify-center py-24 px-6 animate__animated animate__zoomIn">
        <div class="glass-card p-12 rounded-[40px] w-full max-w-md border border-yellow-500/20">
            <h2 class="text-3xl font-black mb-10 italic uppercase tracking-tighter">Initialize Node</h2>
            <div class="space-y-4">
                <input id="in-name" type="text" placeholder="Full Legal Name" class="w-full p-4">
                <input id="in-email" type="email" placeholder="Institutional Email" class="w-full p-4">
                <button onclick="performSignup()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl mt-4 text-xs uppercase">Connect to Mainnet</button>
            </div>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10 animate__animated animate__fadeIn">
        
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-10">
            <div class="lg:col-span-2 glass-card p-10 rounded-[50px] border-l-8 border-[#f3ba2f]">
                <p class="text-[10px] font-black text-gray-500 uppercase tracking-widest mb-2">Portfolio Valuation</p>
                <h2 id="balance-val" class="text-6xl md:text-8xl font-black italic tracking-tighter">$0.00</h2>
                <div class="flex gap-4 mt-12">
                    <button onclick="openModal('deposit')" class="flex-1 bg-[#f3ba2f] text-black py-4 rounded-2xl font-black text-xs uppercase shadow-xl">Deposit</button>
                    <button onclick="openModal('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-4 rounded-2xl font-black text-xs uppercase hover:bg-white/10 transition">Extract</button>
                </div>
            </div>
            <div class="glass-card p-10 rounded-[50px] space-y-8 flex flex-col justify-center">
                <div><p class="text-[9px] font-black text-gray-500 uppercase">Loyalty Points</p><h3 class="text-3xl font-black text-blue-500">2,450 XP</h3></div>
                <div><p class="text-[9px] font-black text-gray-500 uppercase">APY Multiplier</p><h3 class="text-3xl font-black text-green-500">1.5x</h3></div>
                <div><p class="text-[9px] font-black text-gray-500 uppercase">Referral Link</p><p class="text-[10px] font-mono text-[#f3ba2f] mt-2 underline cursor-pointer">nexus.core/ref?7721</p></div>
            </div>
        </div>

        <h4 class="font-black text-[10px] uppercase tracking-[0.3em] mb-6 text-gray-600">Network Infrastructure</h4>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
            <div class="glass-card p-6 rounded-3xl border-b border-green-500/50">
                <span class="ping"></span><p class="text-[10px] font-black mt-2 uppercase">Node HK-1</p>
                <p class="text-[9px] text-gray-500 font-mono italic">Status: Syncing</p>
            </div>
            <div class="glass-card p-6 rounded-3xl border-b border-green-500/50">
                <span class="ping"></span><p class="text-[10px] font-black mt-2 uppercase">Node DXB-7</p>
                <p class="text-[9px] text-gray-500 font-mono italic">Status: Stable</p>
            </div>
            <div class="glass-card p-6 rounded-3xl border-b border-yellow-500/50">
                <span class="ping" style="background:#f3ba2f"></span><p class="text-[10px] font-black mt-2 uppercase">Node NYC-4</p>
                <p class="text-[9px] text-gray-500 font-mono italic">Status: Busy</p>
            </div>
            <div class="glass-card p-6 rounded-3xl border-b border-green-500/50">
                <span class="ping"></span><p class="text-[10px] font-black mt-2 uppercase">Node LON-2</p>
                <p class="text-[9px] text-gray-500 font-mono italic">Status: Stable</p>
            </div>
        </div>
    </section>

    <div id="deposit-modal" class="fixed inset-0 z-[200] bg-black/98 backdrop-blur-3xl hidden flex items-center justify-center p-6">
        <div class="glass-card w-full max-w-lg rounded-[50px] p-12 animate__animated animate__fadeInUp border border-yellow-500/20">
            <div class="flex justify-between items-center mb-10">
                <h3 class="text-3xl font-black italic uppercase">Asset Input</h3>
                <button onclick="closeModals()" class="text-gray-500 text-4xl">&times;</button>
            </div>
            
            <div class="space-y-6">
                <div class="grid grid-cols-3 gap-3">
                    <button onclick="setGate('TRC20')" class="bg-white/5 p-4 rounded-2xl text-[9px] font-black hover:border-[#f3ba2f] border border-transparent">TRC20</button>
                    <button onclick="setGate('ERC20')" class="bg-white/5 p-4 rounded-2xl text-[9px] font-black hover:border-[#f3ba2f] border border-transparent">ERC20</button>
                    <button onclick="setGate('BEP20')" class="bg-white/5 p-4 rounded-2xl text-[9px] font-black hover:border-[#f3ba2f] border border-transparent">BEP20</button>
                </div>
                
                <div class="bg-yellow-500/5 p-6 rounded-3xl border border-yellow-500/20">
                    <p id="gate-label" class="text-[9px] font-black text-yellow-500 uppercase mb-2 italic">USDT (TRC20) Wallet:</p>
                    <p id="gate-addr" class="text-[11px] font-mono break-all font-bold tracking-tighter text-white">TK9UpEWhrtHJMCXAjAmXJndadPZn6Ce2n1</p>
                </div>

                <input id="d-amt" type="number" placeholder="Enter Amount (USD)" class="w-full p-5 text-lg font-black">
                <input id="d-tid" type="text" placeholder="Transaction Hash / TID" class="w-full p-5 text-[10px] font-mono uppercase">
                <button onclick="submitDep()" class="w-full bg-[#f3ba2f] text-black font-black py-5 rounded-2xl shadow-xl uppercase text-xs">Verify Liquidity</button>
            </div>
        </div>
    </div>

    <div id="withdraw-modal" class="fixed inset-0 z-[200] bg-black/98 hidden flex items-center justify-center p-6">
        <div class="glass-card w-full max-w-md rounded-[50px] p-12 animate__animated animate__fadeInDown">
            <h3 class="text-3xl font-black italic uppercase mb-10">Extract</h3>
            <div class="space-y-5">
                <input id="w-name" type="text" placeholder="Beneficiary Account Name" class="w-full p-5">
                <input id="w-addr" type="text" placeholder="Wallet Address / IBAN" class="w-full p-5 text-[10px] font-mono">
                <input id="w-amt" type="number" placeholder="Amount (USD)" class="w-full p-5 text-2xl font-black">
                <button onclick="submitWit()" class="w-full bg-white text-black font-black py-5 rounded-2xl uppercase shadow-xl">Confirm Extraction</button>
            </div>
        </div>
    </div>

    <script>
        let userData = JSON.parse(localStorage.getItem('nexus_session')) || null;
        let balance = parseFloat(localStorage.getItem('nexus_balance')) || 52400.75;

        function checkAuth() {
            if(userData) {
                showSection('dashboard');
                document.getElementById('auth-nav').classList.add('hidden');
                document.getElementById('user-nav').classList.remove('hidden');
                document.getElementById('display-name').innerText = userData.name;
                updateBalanceUI();
            } else {
                showSection('landing');
                document.getElementById('auth-nav').classList.remove('hidden');
                document.getElementById('user-nav').classList.add('hidden');
            }
        }

        function performSignup() {
            const name = document.getElementById('in-name').value;
            if(!name) return alert("Security: Node name required, sweetie!");
            userData = { name: name };
            localStorage.setItem('nexus_session', JSON.stringify(userData));
            localStorage.setItem('nexus_balance', balance);
            checkAuth();
        }

        function logout() {
            localStorage.removeItem('nexus_session');
            location.reload();
        }

        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0,0);
        }

        function setGate(net) {
            const lbl = document.getElementById('gate-label');
            const adr = document.getElementById('gate-addr');
            if(net === 'TRC20') { lbl.innerText = "USDT (TRC20) Wallet:"; adr.innerText = "TK9UpEWhrtHJMCXAjAmXJndadPZn6Ce2n1"; }
            else if(net === 'ERC20') { lbl.innerText = "USDT (ERC20) Wallet:"; adr.innerText = "0x742d35Cc6634C0532925a3b844Bc454e4438f44e"; }
            else { lbl.innerText = "USDT (BEP20) Wallet:"; adr.innerText = "0xTK9UpEWhrtHJMCXAjAmXJndadPZn6Ce2n1"; }
        }

        function openModal(id) { document.getElementById(id + '-modal').classList.remove('hidden'); }
        function closeModals() { document.querySelectorAll('[id$="-modal"]').forEach(m => m.classList.add('hidden')); }

        function submitDep() {
            if(!document.getElementById('d-amt').value || !document.getElementById('d-tid').value) return alert("Error: Missing verification details!");
            alert("Broadcasted: Your transaction hash is being audited by the Nexus Network.");
            closeModals();
        }

        function submitWit() {
            const amt = parseFloat(document.getElementById('w-amt').value);
            if(!amt || amt > balance) return alert("Liquidity Error: Insufficient funds!");
            balance -= amt;
            localStorage.setItem('nexus_balance', balance);
            updateBalanceUI();
            alert("Settled: Assets have been released from the institutional vault.");
            closeModals();
        }

        function updateBalanceUI() {
            document.getElementById('balance-val').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
        }

        window.onload = checkAuth;
    </script>
</body>
</html>
