<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nexus Invest | Worldwide Premium</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --primary: #f3ba2f; --bg: #05070a; --card: #0f1217; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; }
        .glass { background: rgba(15, 18, 23, 0.75); backdrop-filter: blur(15px); border: 1px solid rgba(255,255,255,0.08); }
        .gold-btn { background: linear-gradient(135deg, #f3ba2f 0%, #f0b90b 100%); transition: 0.3s; }
        .gold-btn:hover { transform: scale(1.02); box-shadow: 0 0 20px rgba(243, 186, 47, 0.3); }
        .hidden-section { display: none; }
        .status-dot { height: 8px; width: 8px; border-radius: 50%; display: inline-block; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { opacity: 1; } 50% { opacity: 0.3; } 100% { opacity: 1; } }
    </style>
</head>
<body>

    <nav class="glass sticky top-0 z-50 flex items-center justify-between px-6 py-4">
        <div class="flex items-center gap-2 cursor-pointer" onclick="location.reload()">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl shadow-lg">N</div>
            <span class="text-xl font-bold tracking-tighter">NEXUS<span class="text-[#f3ba2f]">CAPITAL</span></span>
        </div>
        <div id="auth-zone" class="flex gap-4">
            <button onclick="showSection('login')" class="text-gray-400 hover:text-white text-sm font-bold">Login</button>
            <button onclick="showSection('signup')" class="gold-btn text-black px-6 py-2 rounded-full font-bold text-sm">Get Started</button>
        </div>
        <div id="user-zone" class="hidden flex items-center gap-4">
            <div class="text-right">
                <p id="user-name" class="text-sm font-bold text-[#f3ba2f]"></p>
                <p id="kyc-status" class="text-[9px] text-red-500 font-bold uppercase">KYC Unverified</p>
            </div>
            <button onclick="showSection('dashboard')" class="w-10 h-10 rounded-full bg-gray-800 border border-gray-700 flex items-center justify-center">👤</button>
        </div>
    </nav>

    <main id="landing-section" class="section container mx-auto px-6 py-24 text-center animate__animated animate__fadeIn">
        <h1 class="text-6xl md:text-8xl font-black mb-8">Invest in <span class="text-[#f3ba2f]">Dollars</span><br>Anywhere.</h1>
        <p class="text-gray-500 text-lg max-w-2xl mx-auto mb-12">The global standard for digital asset investment. Secure, fast, and transparent.</p>
        <button onclick="showSection('signup')" class="gold-btn text-black px-12 py-5 rounded-full font-black text-xl shadow-2xl">Start Earning Now</button>
    </main>

    <section id="signup-section" class="section hidden-section flex justify-center py-20 px-4 animate__animated animate__zoomIn">
        <div class="glass p-10 rounded-3xl w-full max-w-md">
            <h2 class="text-3xl font-black mb-6">Create Account</h2>
            <input id="in-name" type="text" placeholder="Full Name" class="w-full bg-[#161a1e] p-4 rounded-xl mb-4 border border-gray-800 outline-none focus:border-[#f3ba2f]">
            <input type="email" placeholder="Email" class="w-full bg-[#161a1e] p-4 rounded-xl mb-4 border border-gray-800 outline-none">
            <input type="password" placeholder="Password" class="w-full bg-[#161a1e] p-4 rounded-xl mb-6 border border-gray-800 outline-none">
            <button onclick="handleAuth()" class="w-full gold-btn text-black font-black py-4 rounded-xl">REGISTER</button>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10 animate__animated animate__fadeInUp">
        
        <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-10">
            <div class="glass p-6 rounded-3xl relative overflow-hidden">
                <p class="text-[10px] text-gray-500 font-bold uppercase mb-1">Main Balance</p>
                <h2 id="balance-val" class="text-3xl font-black">$12,500.00</h2>
                <div class="flex gap-2 mt-4">
                    <button onclick="openModal('deposit')" class="text-[10px] bg-green-500/20 text-green-500 px-3 py-1 rounded-lg font-bold">DEPOSIT</button>
                    <button onclick="openModal('withdraw')" class="text-[10px] bg-red-500/20 text-red-500 px-3 py-1 rounded-lg font-bold">WITHDRAW</button>
                </div>
            </div>
            <div class="glass p-6 rounded-3xl">
                <p class="text-[10px] text-gray-500 font-bold uppercase mb-1">Total Profits</p>
                <h2 class="text-3xl font-black text-green-500">+$2,410.50</h2>
            </div>
            <div class="glass p-6 rounded-3xl">
                <p class="text-[10px] text-gray-500 font-bold uppercase mb-1">Active Plans</p>
                <h2 id="active-plans-count" class="text-3xl font-black text-[#f3ba2f]">0</h2>
            </div>
            <div class="glass p-6 rounded-3xl">
                <p class="text-[10px] text-gray-500 font-bold uppercase mb-1">Referral Earnings</p>
                <h2 class="text-3xl font-black">$120.00</h2>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            
            <div class="lg:col-span-2 space-y-6">
                <h3 class="text-xl font-black uppercase tracking-widest">Investment Plans</h3>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div class="glass p-6 rounded-2xl border-t-4 border-blue-500">
                        <h4 class="font-bold">Basic Plan</h4>
                        <p class="text-2xl font-black my-2">5% <span class="text-xs text-gray-500">/ Monthly</span></p>
                        <p class="text-[10px] text-gray-400 mb-4">Min: $100 | Max: $1,000</p>
                        <button onclick="buyPlan('Basic')" class="w-full bg-white/5 hover:bg-white/10 py-2 rounded-lg text-xs font-bold transition">INVEST NOW</button>
                    </div>
                    <div class="glass p-6 rounded-2xl border-t-4 border-[#f3ba2f]">
                        <h4 class="font-bold text-[#f3ba2f]">Gold Plan</h4>
                        <p class="text-2xl font-black my-2">12% <span class="text-xs text-gray-500">/ Monthly</span></p>
                        <p class="text-[10px] text-gray-400 mb-4">Min: $1,500 | Max: $10,000</p>
                        <button onclick="buyPlan('Gold')" class="w-full gold-btn text-black py-2 rounded-lg text-xs font-bold">INVEST NOW</button>
                    </div>
                    <div class="glass p-6 rounded-2xl border-t-4 border-purple-500">
                        <h4 class="font-bold">Platinum</h4>
                        <p class="text-2xl font-black my-2">25% <span class="text-xs text-gray-500">/ Monthly</span></p>
                        <p class="text-[10px] text-gray-400 mb-4">Min: $15,000 | Max: Unlimited</p>
                        <button onclick="buyPlan('Platinum')" class="w-full bg-white/5 hover:bg-white/10 py-2 rounded-lg text-xs font-bold transition">INVEST NOW</button>
                    </div>
                </div>

                <div class="glass rounded-3xl overflow-hidden mt-10">
                    <div class="p-6 border-b border-gray-800"><h3 class="font-bold text-sm uppercase">Recent Transactions</h3></div>
                    <table class="w-full text-left text-xs">
                        <thead class="bg-white/5 text-gray-500">
                            <tr><th class="p-4">Type</th><th class="p-4">Amount</th><th class="p-4">Status</th><th class="p-4">Date</th></tr>
                        </thead>
                        <tbody id="trans-history" class="divide-y divide-gray-900">
                            <tr><td class="p-4">Welcome Bonus</td><td class="p-4 text-green-500">+$50.00</td><td class="p-4 uppercase font-bold text-[9px]">Completed</td><td class="p-4 text-gray-500">2026-04-19</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <div class="space-y-6">
                <div class="glass p-6 rounded-3xl bg-red-500/5 border-red-500/20">
                    <h4 class="font-bold text-sm mb-2">Account Verification</h4>
                    <p class="text-[11px] text-gray-400 mb-4">Verify your identity to increase withdrawal limits.</p>
                    <button onclick="alert('KYC System: Please upload ID Card photo.')" class="w-full border border-red-500/50 text-red-500 py-2 rounded-xl text-[10px] font-bold hover:bg-red-500 hover:text-white transition">VERIFY KYC</button>
                </div>

                <div class="glass p-6 rounded-3xl">
                    <h4 class="font-bold text-sm mb-2">Referral Program</h4>
                    <p class="text-[11px] text-gray-400 mb-4">Get 10% of your friend's first deposit.</p>
                    <div class="flex gap-2">
                        <input type="text" value="nexus.inv/u7821" readonly class="flex-1 bg-black/40 p-2 rounded-lg text-[10px] border border-gray-800 outline-none">
                        <button onclick="alert('Link Copied!')" class="bg-[#f3ba2f] text-black px-3 rounded-lg text-[10px] font-bold">COPY</button>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <div id="trans-modal" class="fixed inset-0 z-[100] bg-black/90 backdrop-blur-md hidden flex items-center justify-center p-6">
        <div class="glass w-full max-w-sm rounded-3xl p-8 animate__animated animate__fadeInDown">
            <div class="flex justify-between items-center mb-6">
                <h3 id="modal-title" class="text-xl font-black uppercase">Deposit</h3>
                <button onclick="closeModal()" class="text-gray-500 text-2xl">&times;</button>
            </div>
            <select class="w-full bg-[#161a1e] p-4 rounded-xl border border-gray-800 outline-none mb-4 text-sm">
                <option>USDT (TRC20)</option>
                <option>Bitcoin (BTC)</option>
                <option>Local Bank</option>
            </select>
            <input id="trans-amount" type="number" placeholder="Amount in USD" class="w-full bg-[#161a1e] p-4 rounded-xl border border-gray-800 outline-none mb-6 text-xl font-bold">
            <button onclick="executeTransaction()" id="modal-btn" class="w-full gold-btn text-black font-black py-4 rounded-xl">CONFIRM</button>
        </div>
    </div>

    <script>
        let balance = 12500;
        let activePlans = 0;
        let activeMode = 'deposit';

        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0,0);
        }

        function handleAuth() {
            const name = document.getElementById('in-name').value || "Global Trader";
            document.getElementById('auth-zone').classList.add('hidden');
            document.getElementById('user-zone').classList.remove('hidden');
            document.getElementById('user-name').innerText = name;
            showSection('dashboard');
        }

        function openModal(mode) {
            activeMode = mode;
            document.getElementById('modal-title').innerText = mode;
            document.getElementById('trans-modal').classList.remove('hidden');
        }

        function closeModal() { document.getElementById('trans-modal').classList.add('hidden'); }

        function executeTransaction() {
            const amt = parseFloat(document.getElementById('trans-amount').value);
            if(!amt || amt <= 0) return;
            
            if(activeMode === 'withdraw' && amt > balance) return alert("Insufficient Balance!");

            balance = activeMode === 'deposit' ? balance + amt : balance - amt;
            updateUI();
            addTransaction(activeMode, amt);
            closeModal();
            alert(activeMode.toUpperCase() + " Successful!");
        }

        function buyPlan(plan) {
            alert("Success: You have subscribed to the " + plan + " Plan! Profit will start in 24h.");
            activePlans++;
            updateUI();
        }

        function addTransaction(type, amt) {
            const tbody = document.getElementById('trans-history');
            const row = `<tr><td class="p-4">${type}</td><td class="p-4 ${type==='deposit'?'text-green-500':'text-red-500'}">${type==='deposit'?'+':'-'}$${amt}</td><td class="p-4 uppercase font-bold text-[9px]">Completed</td><td class="p-4 text-gray-500">Today</td></tr>`;
            tbody.innerHTML = row + tbody.innerHTML;
        }

        function updateUI() {
            document.getElementById('balance-val').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
            document.getElementById('active-plans-count').innerText = activePlans;
        }
    </script>
</body>
</html>
