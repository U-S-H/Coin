<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS CORE | Ultimate Web3 Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --bg: #010204; --glass: rgba(13, 17, 23, 0.9); }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .glass-panel { background: var(--glass); backdrop-filter: blur(30px); border: 1px solid rgba(255,255,255,0.06); }
        .crypto-glow { background: linear-gradient(90deg, #f3ba2f, #ffffff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .sidebar { transform: translateX(100%); transition: 0.4s cubic-bezier(0.4, 0, 0.2, 1); }
        .sidebar.active { transform: translateX(0); }
        .ping { height: 8px; width: 8px; border-radius: 50%; display: inline-block; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { opacity: 1; transform: scale(1); } 50% { opacity: 0.3; transform: scale(1.4); } 100% { opacity: 1; transform: scale(1); } }
        .hidden-section { display: none; }
        input { background: #0d1117 !important; border: 1px solid #21262d !important; color: white !important; outline: none !important; border-radius: 12px !important; }
        input:focus { border-color: var(--gold) !important; }
        .history-item { border-bottom: 1px solid rgba(255,255,255,0.03); }
        .vip-card { border: 1px solid rgba(255,255,255,0.05); transition: 0.3s; }
        .vip-card:hover { border-color: var(--gold); background: rgba(243, 186, 47, 0.05); }
    </style>
</head>
<body>

    <nav class="glass-panel sticky top-0 z-[100] px-6 py-4 flex items-center justify-between">
        <div class="flex items-center gap-3 cursor-pointer" onclick="checkAuth()">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl shadow-lg">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="crypto-glow">Core</span></span>
        </div>
        
        <div class="flex items-center gap-4">
            <div id="user-info" class="hidden text-right hidden sm:block">
                <p id="nav-name" class="text-[10px] font-black text-[#f3ba2f] uppercase"></p>
                <p class="text-[8px] text-green-500 font-bold">SECURED NODE</p>
            </div>
            <button onclick="toggleSidebar()" class="w-10 h-10 flex flex-col items-center justify-center gap-1.5 hover:opacity-70 transition">
                <div class="w-6 h-0.5 bg-white"></div>
                <div class="w-6 h-0.5 bg-white"></div>
                <div class="w-6 h-0.5 bg-white"></div>
            </button>
        </div>
    </nav>

    <div id="sidebar" class="sidebar fixed top-0 right-0 h-full w-full max-w-xs glass-panel z-[200] p-8 shadow-2xl">
        <div class="flex justify-between items-center mb-10">
            <h3 class="font-black italic uppercase text-lg">Menu</h3>
            <button onclick="toggleSidebar()" class="text-3xl">&times;</button>
        </div>
        <div class="space-y-6">
            <button onclick="showSection('dashboard'); toggleSidebar()" class="w-full text-left font-bold text-sm hover:text-[#f3ba2f] transition">🏠 DASHBOARD</button>
            <button onclick="openModal('deposit'); toggleSidebar()" class="w-full text-left font-bold text-sm hover:text-[#f3ba2f] transition">💰 DEPOSIT ASSETS</button>
            <button onclick="showPolicy('history'); toggleSidebar()" class="w-full text-left font-bold text-sm hover:text-[#f3ba2f] transition">📜 TRANSACTION HISTORY</button>
            <button onclick="showPolicy('company'); toggleSidebar()" class="w-full text-left font-bold text-sm hover:text-[#f3ba2f] transition">🏢 COMPANY DETAILS</button>
            <button onclick="showPolicy('privacy'); toggleSidebar()" class="w-full text-left font-bold text-sm hover:text-[#f3ba2f] transition">🛡️ PRIVACY POLICY</button>
            <hr class="border-white/5">
            <button onclick="logout()" class="w-full text-left font-black text-sm text-red-500 hover:scale-105 transition">🚪 LOGOUT TERMINAL</button>
        </div>
        <div class="absolute bottom-8 left-8">
            <p class="text-[10px] font-bold text-gray-600 uppercase tracking-widest italic">Nexus v2.4.0 Build</p>
        </div>
    </div>

    <section id="landing-section" class="section py-28 px-6 text-center animate__animated animate__fadeIn">
        <div class="inline-flex items-center gap-3 bg-white/5 border border-white/10 px-4 py-1 rounded-full mb-8">
            <span class="ping bg-green-500"></span><span class="text-[9px] font-black text-gray-500 uppercase tracking-[0.2em]">Global Network Verified</span>
        </div>
        <h1 class="text-7xl md:text-9xl font-black mb-8 italic leading-none tracking-tighter">THE <span class="crypto-glow">FUTURE</span><br>OF CAPITAL.</h1>
        <button onclick="showSection('signup')" class="bg-[#f3ba2f] text-black px-12 py-5 rounded-2xl font-black text-xl shadow-2xl hover:scale-105 transition">START MINING</button>
    </section>

    <section id="signup-section" class="section hidden-section flex justify-center py-24 px-6 animate__animated animate__zoomIn">
        <div class="glass-panel p-10 rounded-[40px] w-full max-w-md">
            <h2 class="text-3xl font-black mb-10 italic uppercase">Sync Identity</h2>
            <div class="space-y-4">
                <input id="reg-name" type="text" placeholder="Full Legal Name" class="w-full p-4">
                <input id="reg-email" type="email" placeholder="Institutional Email" class="w-full p-4">
                <button onclick="register()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl mt-4">INITIATE CONNECTION</button>
            </div>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10 animate__animated animate__fadeIn">
        
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <div class="lg:col-span-2 glass-panel p-10 rounded-[45px] border-l-8 border-[#f3ba2f]">
                <p class="text-[10px] font-black text-gray-500 uppercase tracking-[0.3em] mb-4">Secured Valuation</p>
                <h2 id="balance-val" class="text-6xl md:text-8xl font-black italic tracking-tighter mb-12">$0.00</h2>
                <div class="flex gap-4">
                    <button onclick="openModal('deposit')" class="flex-1 bg-[#f3ba2f] text-black py-4 rounded-2xl font-black text-xs uppercase shadow-lg hover:brightness-110">Deposit</button>
                    <button onclick="openModal('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-4 rounded-2xl font-black text-xs uppercase hover:bg-white/10">Withdraw</button>
                </div>
            </div>

            <div class="glass-panel p-8 rounded-[45px] flex flex-col justify-between">
                <p class="text-[10px] font-black text-gray-500 uppercase tracking-widest mb-4">Active Plan</p>
                <div class="space-y-4">
                    <div class="vip-card p-4 rounded-2xl bg-white/5">
                        <div class="flex justify-between items-center"><span class="text-xs font-black uppercase">Bronze Tier</span><span class="text-green-500 text-[10px] font-bold">5% Daily</span></div>
                    </div>
                    <div class="vip-card p-4 rounded-2xl opacity-40">
                        <div class="flex justify-between items-center"><span class="text-xs font-black uppercase">Gold Master</span><span class="text-yellow-500 text-[10px] font-bold">12% Daily</span></div>
                    </div>
                </div>
                <div class="mt-6"><p class="text-[9px] text-gray-600 font-bold uppercase tracking-widest italic">Profit starts every 24h</p></div>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mt-10">
            <div class="lg:col-span-2 glass-panel p-8 rounded-[40px]">
                <h4 class="text-xs font-black uppercase tracking-widest mb-6 flex items-center gap-2">
                    <span class="w-2 h-2 bg-[#f3ba2f] rounded-full"></span> Recent Terminal Activity
                </h4>
                <div id="history-container" class="space-y-4">
                    <p class="text-xs text-gray-600 italic">No recent transactions found in current session.</p>
                </div>
            </div>
            
            <div class="glass-panel p-8 rounded-[40px]">
                <h4 class="text-[10px] font-black uppercase tracking-widest mb-6 text-gray-500">Node Grid Status</h4>
                <div class="space-y-4">
                    <div class="flex justify-between text-[10px]"><span class="text-gray-400 italic">Node LON-01</span> <span class="text-green-500 font-bold">ACTIVE</span></div>
                    <div class="flex justify-between text-[10px]"><span class="text-gray-400 italic">Node HKG-05</span> <span class="text-green-500 font-bold">ACTIVE</span></div>
                    <div class="flex justify-between text-[10px]"><span class="text-gray-400 italic">Node DXB-02</span> <span class="text-yellow-500 font-bold">SYNCING</span></div>
                </div>
            </div>
        </div>
    </section>

    <div id="policy-modal" class="fixed inset-0 z-[300] bg-black/98 backdrop-blur-3xl hidden overflow-y-auto p-6">
        <div class="max-w-3xl mx-auto py-20">
            <div class="flex justify-between items-center mb-10">
                <h2 id="policy-title" class="text-4xl font-black italic uppercase"></h2>
                <button onclick="closePolicy()" class="text-5xl">&times;</button>
            </div>
            <div id="policy-content" class="text-gray-400 leading-relaxed space-y-6 text-sm italic">
                </div>
        </div>
    </div>

    <div id="deposit-modal" class="fixed inset-0 z-[300] bg-black/98 hidden flex items-center justify-center p-6">
        <div class="glass-panel w-full max-w-lg rounded-[50px] p-10 animate__animated animate__fadeInUp">
            <div class="flex justify-between items-center mb-8">
                <h3 class="text-2xl font-black italic uppercase">Deposit Asset</h3>
                <button onclick="closeModals()" class="text-gray-500 text-3xl">&times;</button>
            </div>
            <div class="bg-yellow-500/5 p-5 rounded-3xl border border-yellow-500/15 mb-6">
                <p class="text-[9px] font-black text-yellow-500 uppercase mb-2">USDT TRC20 Address:</p>
                <p id="trc-addr" class="text-[11px] font-mono font-bold break-all">TK9UpEWhrtHJMCXAjAmXJndadPZn6Ce2n1</p>
                <button onclick="copyAddr()" class="text-[8px] bg-white/5 px-2 py-1 mt-2 rounded-full uppercase hover:bg-white/10">Copy Address</button>
            </div>
            <div class="space-y-4">
                <input id="d-amt" type="number" placeholder="Enter Amount (USD)" class="w-full p-4">
                <input id="d-tid" type="text" placeholder="Transaction Hash (TID)" class="w-full p-4 text-[10px] font-mono">
                <button onclick="confirmDeposit()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl">SUBMIT VERIFICATION</button>
            </div>
        </div>
    </div>

    <div id="withdraw-modal" class="fixed inset-0 z-[300] bg-black/98 hidden flex items-center justify-center p-6">
        <div class="glass-panel w-full max-w-md rounded-[50px] p-10 animate__animated animate__fadeInDown">
            <h3 class="text-2xl font-black italic uppercase mb-8">Withdraw</h3>
            <div class="space-y-4">
                <input id="w-addr" type="text" placeholder="Receiver Address / IBAN" class="w-full p-4 text-[10px] font-mono">
                <input id="w-amt" type="number" placeholder="Amount (USD)" class="w-full p-4 text-2xl font-black text-center">
                <button onclick="confirmWithdraw()" class="w-full bg-white text-black font-black py-4 rounded-xl shadow-xl">AUTHORIZE PAYOUT</button>
            </div>
        </div>
    </div>

    <script>
        let userData = JSON.parse(localStorage.getItem('nexus_auth')) || null;
        let balance = parseFloat(localStorage.getItem('nexus_val')) || 42500.50;
        let history = JSON.parse(localStorage.getItem('nexus_history')) || [];

        function checkAuth() {
            if(userData) {
                showSection('dashboard');
                document.getElementById('user-info').classList.remove('hidden');
                document.getElementById('auth-nav').classList.add('hidden');
                document.getElementById('nav-name').innerText = userData.name;
                updateUI();
            } else {
                showSection('landing');
                document.getElementById('user-info').classList.add('hidden');
                document.getElementById('auth-nav').classList.remove('hidden');
            }
        }

        function register() {
            const name = document.getElementById('reg-name').value;
            if(!name) return alert("Sweetie, enter your name!");
            userData = { name: name };
            localStorage.setItem('nexus_auth', JSON.stringify(userData));
            localStorage.setItem('nexus_val', balance);
            checkAuth();
        }

        function logout() {
            localStorage.removeItem('nexus_auth');
            location.reload();
        }

        function toggleSidebar() { document.getElementById('sidebar').classList.toggle('active'); }
        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0,0);
        }

        function openModal(id) { document.getElementById(id + '-modal').classList.remove('hidden'); }
        function closeModals() { document.querySelectorAll('[id$="-modal"]').forEach(m => m.classList.add('hidden')); }

        function confirmDeposit() {
            const amt = document.getElementById('d-amt').value;
            if(!amt) return alert("Enter amount!");
            addHistory('Deposit', amt, 'PENDING');
            alert("Broadcasted: Your transfer is being audited by the blockchain nodes.");
            closeModals();
        }

        function confirmWithdraw() {
            const amt = parseFloat(document.getElementById('w-amt').value);
            if(!amt || amt > balance) return alert("Insufficient Liquidity!");
            balance -= amt;
            localStorage.setItem('nexus_val', balance);
            addHistory('Withdrawal', amt, 'SETTLED');
            updateUI();
            alert("Success: Assets released from institutional vault.");
            closeModals();
        }

        function addHistory(type, amt, status) {
            const date = new Date().toLocaleString();
            history.unshift({ type, amt, status, date });
            localStorage.setItem('nexus_history', JSON.stringify(history));
            updateUI();
        }

        function updateUI() {
            document.getElementById('balance-val').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
            const container = document.getElementById('history-container');
            if(history.length > 0) {
                container.innerHTML = history.slice(0, 5).map(item => `
                    <div class="history-item flex justify-between py-3">
                        <div><p class="text-[10px] font-black uppercase text-[#f3ba2f]">${item.type}</p><p class="text-[8px] text-gray-500">${item.date}</p></div>
                        <div class="text-right"><p class="text-xs font-mono">$${parseFloat(item.amt).toLocaleString()}</p><p class="text-[8px] font-bold ${item.status === 'PENDING' ? 'text-yellow-500' : 'text-green-500'}">${item.status}</p></div>
                    </div>
                `).join('');
            }
        }

        function copyAddr() {
            const addr = document.getElementById('trc-addr').innerText;
            navigator.clipboard.writeText(addr);
            alert("Copied to clipboard, sweetie!");
        }

        function showPolicy(type) {
            const modal = document.getElementById('policy-modal');
            const title = document.getElementById('policy-title');
            const content = document.getElementById('policy-content');
            modal.classList.remove('hidden');

            if(type === 'privacy') {
                title.innerText = "Privacy Protocol";
                content.innerHTML = "<p>Nexus Core uses AES-256 end-to-end encryption. Your data is stored on decentralized nodes and is never shared with third-party institutional entities. Our privacy standards comply with the 2026 Global Digital Asset Act.</p><p>By using this terminal, you consent to encrypted biometric logging for security purposes.</p>";
            } else if(type === 'company') {
                title.innerText = "Company Identity";
                content.innerHTML = "<p>Nexus Core Institutional is a global leader in Web3 liquidity and asset management. Founded in 2024, we bridge the gap between traditional finance and decentralized future.</p><p>Headquarters: Dubai Silicon Oasis, UAE | London Canary Wharf, UK.</p>";
            } else if(type === 'history') {
                title.innerText = "Full Ledger History";
                content.innerHTML = history.length > 0 ? history.map(item => `<div class='border-b border-white/5 py-4'><p class='font-black uppercase text-[#f3ba2f]'>${item.type}</p><p class='text-xs'>${item.date} | $${item.amt} | ${item.status}</p></div>`).join('') : "<p>No ledger entries found.</p>";
            }
        }

        function closePolicy() { document.getElementById('policy-modal').classList.add('hidden'); }

        window.onload = checkAuth;
    </script>
</body>
</html>
