<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS CORE | Web3 Digital Assets</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --bg: #020406; --card: #0d1117; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .glass-panel { background: rgba(13, 17, 23, 0.7); backdrop-filter: blur(25px); border: 1px solid rgba(255,255,255,0.06); }
        .wallet-btn { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.1); transition: 0.3s; }
        .wallet-btn:hover { background: rgba(243, 186, 47, 0.1); border-color: var(--gold); transform: translateY(-2px); }
        .node-box { background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.05); }
        .ping-dot { height: 6px; width: 6px; background: #10b981; border-radius: 50%; display: inline-block; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0% { opacity: 1; transform: scale(1); } 50% { opacity: 0.4; transform: scale(1.5); } 100% { opacity: 1; transform: scale(1); } }
        .hidden-section { display: none; }
        .crypto-gradient { background: linear-gradient(135deg, #f3ba2f 0%, #ff8c00 100%); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
    </style>
</head>
<body>

    <nav class="glass-panel sticky top-0 z-[100] px-6 py-4 flex items-center justify-between border-b border-white/5">
        <div class="flex items-center gap-3 cursor-pointer" onclick="location.reload()">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="crypto-gradient">Core</span></span>
        </div>
        <div id="auth-header">
            <button onclick="showSection('signup')" class="bg-white text-black px-6 py-2 rounded-full font-black text-xs hover:bg-[#f3ba2f] transition shadow-lg">CONNECT ACCESS</button>
        </div>
        <div id="user-header" class="hidden flex items-center gap-4">
            <div class="text-right leading-none"><p id="display-name" class="text-xs font-black text-[#f3ba2f] uppercase"></p><span class="text-[8px] text-gray-500 font-bold">SECURED NODE</span></div>
            <div class="w-10 h-10 rounded-full border border-yellow-500/30 flex items-center justify-center bg-gray-900">👤</div>
        </div>
    </nav>

    <section id="landing-section" class="section py-28 px-6 text-center animate__animated animate__fadeIn">
        <h1 class="text-6xl md:text-8xl font-black mb-6 italic tracking-tighter leading-none">INSTITUTIONAL<br><span class="crypto-gradient">LIQUIDITY.</span></h1>
        <p class="text-gray-500 max-w-xl mx-auto mb-10 text-sm font-bold uppercase tracking-[0.2em]">Next-Gen Wealth Management Protocol</p>
        <button onclick="showSection('signup')" class="bg-[#f3ba2f] text-black px-12 py-5 rounded-2xl font-black text-lg shadow-2xl hover:scale-105 transition">ENTER TERMINAL</button>
    </section>

    <section id="signup-section" class="section hidden-section flex justify-center py-20 animate__animated animate__zoomIn">
        <div class="glass-panel p-10 rounded-[40px] w-full max-w-md border border-yellow-500/20">
            <h2 class="text-3xl font-black mb-8 italic text-center">INITIALIZE NODE</h2>
            <div class="space-y-4">
                <input id="in-name" type="text" placeholder="Account Name" class="w-full bg-[#161a1e] p-4 rounded-xl border border-white/5 outline-none focus:border-[#f3ba2f]">
                <input type="email" placeholder="Secure Email" class="w-full bg-[#161a1e] p-4 rounded-xl border border-white/5 outline-none">
                <button onclick="handleAuth()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl shadow-yellow-500/10">CREATE PORTFOLIO</button>
            </div>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10 animate__animated animate__fadeIn">
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-10">
            <div class="lg:col-span-2 glass-panel p-10 rounded-[40px] border-l-4 border-[#f3ba2f]">
                <div class="flex justify-between items-start mb-6">
                    <div><p class="text-[10px] font-bold text-gray-500 uppercase tracking-widest">Available Balance</p>
                    <h2 id="balance-val" class="text-6xl font-black tracking-tighter italic">$12,500.00</h2></div>
                    <div class="bg-green-500/10 text-green-500 px-3 py-1 rounded-full text-[10px] font-black uppercase">Live Sync</div>
                </div>
                <div class="flex gap-4">
                    <button onclick="openModal('deposit')" class="flex-1 bg-[#f3ba2f] text-black py-4 rounded-2xl font-black text-xs uppercase">Add Assets</button>
                    <button onclick="openModal('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-4 rounded-2xl font-black text-xs uppercase hover:bg-white/10">Extract</button>
                </div>
            </div>

            <div class="glass-panel p-8 rounded-[40px] flex flex-col justify-center">
                <p class="text-[10px] font-bold text-gray-500 uppercase mb-4">Network Status</p>
                <div class="space-y-4">
                    <div class="flex justify-between items-center"><span class="text-xs text-gray-400">Mainnet Delay</span><span class="text-xs font-mono text-green-500">12ms</span></div>
                    <div class="flex justify-between items-center"><span class="text-xs text-gray-400">Staking APY</span><span class="text-xs font-mono text-[#f3ba2f]">24.2%</span></div>
                    <div class="flex justify-between items-center"><span class="text-xs text-gray-400">Security Audit</span><span class="text-[10px] font-black text-blue-500">VERIFIED</span></div>
                </div>
            </div>
        </div>

        <h3 class="font-black italic text-xs uppercase tracking-widest mb-6 text-gray-500">Infrastructure Nodes</h3>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-10">
            <div class="node-box p-5 rounded-2xl">
                <div class="flex justify-between mb-3"><span class="ping-dot"></span><span class="text-[9px] font-mono text-gray-600">LON-01</span></div>
                <p class="text-xs font-black uppercase">London Hub</p>
                <p class="text-[10px] text-green-500 font-mono mt-1">ACTIVE</p>
            </div>
            <div class="node-box p-5 rounded-2xl">
                <div class="flex justify-between mb-3"><span class="ping-dot"></span><span class="text-[9px] font-mono text-gray-600">NYC-04</span></div>
                <p class="text-xs font-black uppercase">New York</p>
                <p class="text-[10px] text-green-500 font-mono mt-1">ACTIVE</p>
            </div>
            <div class="node-box p-5 rounded-2xl">
                <div class="flex justify-between mb-3"><span class="ping-dot" style="background: #f59e0b;"></span><span class="text-[9px] font-mono text-gray-600">TKY-09</span></div>
                <p class="text-xs font-black uppercase">Tokyo Pool</p>
                <p class="text-[10px] text-yellow-500 font-mono mt-1">SYNCING...</p>
            </div>
            <div class="node-box p-5 rounded-2xl">
                <div class="flex justify-between mb-3"><span class="ping-dot"></span><span class="text-[9px] font-mono text-gray-600">DXB-02</span></div>
                <p class="text-xs font-black uppercase">Dubai Core</p>
                <p class="text-[10px] text-green-500 font-mono mt-1">ACTIVE</p>
            </div>
        </div>
    </section>

    <div id="deposit-modal" class="fixed inset-0 z-[200] bg-black/95 backdrop-blur-xl hidden flex items-center justify-center p-6">
        <div class="glass-panel w-full max-w-md rounded-[40px] p-10 animate__animated animate__fadeInUp border border-yellow-500/20">
            <div class="flex justify-between items-center mb-8">
                <h3 class="text-2xl font-black italic uppercase">Asset Gateway</h3>
                <button onclick="closeModals()" class="text-gray-500 text-3xl">&times;</button>
            </div>
            
            <p class="text-[10px] font-black text-gray-500 uppercase tracking-widest mb-4">Connect Secure Wallet</p>
            <div class="grid grid-cols-2 gap-4 mb-8">
                <button onclick="simulateConnect('MetaMask')" class="wallet-btn p-4 rounded-2xl flex flex-col items-center gap-2">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/3/36/MetaMask_Fox.svg" class="w-8 h-8">
                    <span class="text-[10px] font-black">METAMASK</span>
                </button>
                <button onclick="simulateConnect('Trust Wallet')" class="wallet-btn p-4 rounded-2xl flex flex-col items-center gap-2">
                    <img src="https://trustwallet.com/assets/images/media/assets/trust_platform.svg" class="w-8 h-8">
                    <span class="text-[10px] font-black">TRUST WALLET</span>
                </button>
                <button onclick="simulateConnect('Binance Pay')" class="wallet-btn p-4 rounded-2xl flex flex-col items-center gap-2">
                    <img src="https://cryptologos.cc/logos/binance-coin-bnb-logo.svg" class="w-8 h-8">
                    <span class="text-[10px] font-black">BINANCE PAY</span>
                </button>
                <button onclick="simulateConnect('WalletConnect')" class="wallet-btn p-4 rounded-2xl flex flex-col items-center gap-2">
                    <img src="https://raw.githubusercontent.com/WalletConnect/walletconnect-assets/master/Logo/Blue%20(Default)/Logo.svg" class="w-8 h-8">
                    <span class="text-[10px] font-black">ANY WALLET</span>
                </button>
            </div>

            <div class="space-y-4">
                <div class="bg-black/40 p-4 rounded-2xl border border-white/5">
                    <p class="text-[9px] text-gray-500 uppercase font-black mb-1">Manual USDT Address (TRC20)</p>
                    <p class="text-[11px] font-mono text-[#f3ba2f] break-all">TNV8pX9yR2qW23mXyZ99Vv2N8pQxR2</p>
                </div>
                <input id="dep-amt" type="number" placeholder="Enter Amount (USD)" class="w-full bg-[#161a1e] p-4 rounded-xl border border-white/5 text-sm font-black">
                <input id="dep-tid" type="text" placeholder="Transaction Hash (TID)" class="w-full bg-[#161a1e] p-4 rounded-xl border border-white/5 text-xs">
                <button onclick="submitDep()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-lg">VALIDATE ASSETS</button>
            </div>
        </div>
    </div>

    <div id="withdraw-modal" class="fixed inset-0 z-[200] bg-black/95 backdrop-blur-xl hidden flex items-center justify-center p-6">
        <div class="glass-panel w-full max-w-md rounded-[40px] p-10 animate__animated animate__fadeInDown border border-red-500/10">
            <h3 class="text-2xl font-black italic uppercase mb-8">Payout Request</h3>
            <div class="space-y-4">
                <input id="wit-name" type="text" placeholder="Beneficiary Name" class="w-full bg-[#161a1e] p-4 rounded-xl border border-white/5 text-sm">
                <input id="wit-acc" type="text" placeholder="Wallet Address / IBAN" class="w-full bg-[#161a1e] p-4 rounded-xl border border-white/5 text-xs font-mono">
                <input id="wit-amt" type="number" placeholder="Amount (USD)" class="w-full bg-[#161a1e] p-4 rounded-xl border border-white/5 text-lg font-black">
                <button onclick="submitWit()" class="w-full bg-white text-black font-black py-4 rounded-xl shadow-xl hover:bg-red-500 hover:text-white transition-all">EXTRACT LIQUIDITY</button>
            </div>
        </div>
    </div>

    <script>
        let balance = 12500.00;

        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0,0);
        }

        function handleAuth() {
            const name = document.getElementById('in-name').value || "Nexus User";
            document.getElementById('auth-header').classList.add('hidden');
            document.getElementById('user-header').classList.remove('hidden');
            document.getElementById('display-name').innerText = name;
            showSection('dashboard');
        }

        function openModal(id) { document.getElementById(id + '-modal').classList.remove('hidden'); }
        function closeModals() { document.querySelectorAll('[id$="-modal"]').forEach(m => m.classList.add('hidden')); }

        function simulateConnect(wallet) {
            alert(`Connecting to ${wallet} Extension... Please authorize via your mobile app.`);
        }

        function submitDep() {
            const amt = document.getElementById('dep-amt').value;
            if(!amt) return alert("Please specify the asset amount, sweetie!");
            alert("Protocol Initiated: Your transaction hash is being verified by our Global Nodes.");
            closeModals();
        }

        function submitWit() {
            const amt = parseFloat(document.getElementById('wit-amt').value);
            if(!amt || amt > balance) return alert("Insufficient Liquidity!");
            balance -= amt;
            document.getElementById('balance-val').innerText = '$' + balance.toLocaleString();
            alert("Settlement Finalized: Funds will be released following network confirmation.");
            closeModals();
        }
    </script>
</body>
</html>
