<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nexus Invest | Global Premium Dashboard</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --primary: #f3ba2f; --bg: #05070a; --card: #0f1217; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .glass { background: rgba(15, 18, 23, 0.7); backdrop-filter: blur(12px); border: 1px solid rgba(255,255,255,0.05); }
        .gold-btn { background: linear-gradient(135deg, #f3ba2f 0%, #f0b90b 100%); transition: 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275); }
        .gold-btn:hover { transform: translateY(-2px); box-shadow: 0 10px 20px rgba(243, 186, 47, 0.2); }
        .hidden-section { display: none; }
        .status-dot { height: 8px; width: 8px; border-radius: 50%; display: inline-block; animation: pulse 2s infinite; }
        @keyframes pulse { 0% { transform: scale(0.9); opacity: 1; } 70% { transform: scale(1.5); opacity: 0; } 100% { transform: scale(0.9); opacity: 0; } }
        input::-webkit-outer-spin-button, input::-webkit-inner-spin-button { -webkit-appearance: none; margin: 0; }
    </style>
</head>
<body>

    <nav class="glass sticky top-0 z-50 flex items-center justify-between px-6 py-4">
        <div class="flex items-center gap-2 cursor-pointer" onclick="location.reload()">
            <div class="w-8 h-8 bg-[#f3ba2f] rounded-lg flex items-center justify-center font-black text-black">N</div>
            <span class="text-xl font-bold tracking-tighter uppercase">Nexus<span class="text-[#f3ba2f]">Invest</span></span>
        </div>
        <div id="auth-zone" class="flex gap-4">
            <button onclick="showSection('login')" class="text-gray-400 hover:text-white text-sm font-medium">Log In</button>
            <button onclick="showSection('signup')" class="gold-btn text-black px-6 py-2 rounded-full font-bold text-sm">Join Now</button>
        </div>
        <div id="user-zone" class="hidden flex items-center gap-4">
            <div class="text-right">
                <p id="user-name" class="text-sm font-bold text-[#f3ba2f]"></p>
                <p class="text-[10px] text-gray-500">Premium Member</p>
            </div>
            <div class="w-10 h-10 rounded-full bg-gradient-to-tr from-[#f3ba2f] to-yellow-600 p-[2px]">
                <div class="w-full h-full rounded-full bg-black flex items-center justify-center font-bold">U</div>
            </div>
        </div>
    </nav>

    <main id="landing-section" class="section container mx-auto px-6 py-20 text-center animate__animated animate__fadeIn">
        <h1 class="text-6xl md:text-8xl font-black mb-8 leading-tight">Trade Smarter.<br><span class="text-[#f3ba2f]">Invest Globally.</span></h1>
        <p class="text-gray-500 text-lg md:text-xl max-w-3xl mx-auto mb-12">The elite platform for dollar-denominated assets. Access real-time markets with institutional-grade security.</p>
        <div class="flex flex-wrap justify-center gap-6">
            <button onclick="showSection('signup')" class="gold-btn text-black px-10 py-4 rounded-full font-black text-lg">Open Account</button>
            <div class="flex items-center gap-3 text-gray-400">
                <span class="status-dot bg-green-500"></span> 2,401 Traders Online
            </div>
        </div>
    </main>

    <section id="login-section" class="section hidden-section flex justify-center py-20 animate__animated animate__zoomIn">
        <div class="glass p-10 rounded-3xl w-full max-w-md shadow-2xl">
            <h2 class="text-3xl font-black mb-8">Welcome Back</h2>
            <input type="email" placeholder="Email" class="w-full bg-[#161a1e] p-4 rounded-xl mb-4 border border-gray-800 outline-none focus:border-[#f3ba2f]">
            <input type="password" placeholder="Password" class="w-full bg-[#161a1e] p-4 rounded-xl mb-6 border border-gray-800 outline-none">
            <button onclick="handleAuth('Investor')" class="w-full gold-btn text-black font-black py-4 rounded-xl">LOGIN</button>
        </div>
    </section>

    <section id="signup-section" class="section hidden-section flex justify-center py-20 animate__animated animate__zoomIn">
        <div class="glass p-10 rounded-3xl w-full max-w-md shadow-2xl">
            <h2 class="text-3xl font-black mb-8">Start Journey</h2>
            <input id="in-name" type="text" placeholder="Full Name" class="w-full bg-[#161a1e] p-4 rounded-xl mb-4 border border-gray-800 outline-none focus:border-[#f3ba2f]">
            <input type="email" placeholder="Email" class="w-full bg-[#161a1e] p-4 rounded-xl mb-4 border border-gray-800 outline-none">
            <input type="password" placeholder="Password" class="w-full bg-[#161a1e] p-4 rounded-xl mb-6 border border-gray-800 outline-none">
            <button onclick="handleAuth()" class="w-full gold-btn text-black font-black py-4 rounded-xl">CREATE ACCOUNT</button>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10 animate__animated animate__fadeInUp">
        <div class="grid grid-cols-1 lg:grid-cols-4 gap-8">
            
            <div class="lg:col-span-1 space-y-6">
                <div class="glass p-8 rounded-3xl relative overflow-hidden">
                    <p class="text-xs text-gray-500 uppercase tracking-widest mb-2 font-bold">Total Net Worth</p>
                    <h2 id="balance-val" class="text-4xl font-black tracking-tighter mb-6">$12,500.00</h2>
                    <div class="flex gap-2">
                        <button onclick="openModal('deposit')" class="flex-1 gold-btn text-black py-3 rounded-xl font-bold text-xs">DEPOSIT</button>
                        <button onclick="openModal('withdraw')" class="flex-1 bg-white/5 hover:bg-white/10 py-3 rounded-xl font-bold text-xs">WITHDRAW</button>
                    </div>
                </div>
                
                <div class="glass p-6 rounded-3xl">
                    <h4 class="text-sm font-bold mb-4">Market Status</h4>
                    <div class="space-y-4">
                        <div class="flex justify-between items-center">
                            <span class="text-gray-400 text-xs">Wall Street</span>
                            <span class="text-green-500 text-xs font-bold uppercase">Open</span>
                        </div>
                        <div class="flex justify-between items-center">
                            <span class="text-gray-400 text-xs">Crypto Market</span>
                            <span class="text-green-500 text-xs font-bold uppercase tracking-tighter">24/7 Active</span>
                        </div>
                    </div>
                </div>
            </div>

            <div class="lg:col-span-3 space-y-8">
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="glass p-6 rounded-3xl border-l-4 border-[#f3ba2f]">
                        <p class="text-xs text-gray-500">Bitcoin / USD</p>
                        <p id="p-btc" class="text-xl font-bold mt-1 tracking-tighter">$67,421.10</p>
                    </div>
                    <div class="glass p-6 rounded-3xl border-l-4 border-blue-500">
                        <p class="text-xs text-gray-500">Nasdaq 100</p>
                        <p id="p-nas" class="text-xl font-bold mt-1 tracking-tighter">$18,240.50</p>
                    </div>
                    <div class="glass p-6 rounded-3xl border-l-4 border-green-500">
                        <p class="text-xs text-gray-500">US Dollar Index</p>
                        <p class="text-xl font-bold mt-1 tracking-tighter">104.12</p>
                    </div>
                </div>

                <div class="glass rounded-3xl overflow-hidden">
                    <div class="p-6 border-b border-gray-800 flex justify-between items-center">
                        <h3 class="font-black uppercase tracking-widest text-sm">Active Markets</h3>
                        <div class="text-[10px] bg-green-500/20 text-green-500 px-2 py-1 rounded">REAL-TIME DATA</div>
                    </div>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left">
                            <thead class="bg-white/5 text-[10px] text-gray-500 uppercase">
                                <tr>
                                    <th class="p-6">Asset Name</th>
                                    <th class="p-6">Price</th>
                                    <th class="p-6">24h Performance</th>
                                    <th class="p-6 text-right">Action</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-gray-900">
                                <tr class="hover:bg-white/5 transition">
                                    <td class="p-6 flex items-center gap-3"><div class="w-8 h-8 rounded-full bg-yellow-500/20 flex items-center justify-center font-bold text-xs">₿</div> Bitcoin</td>
                                    <td class="p-6 font-mono font-bold">$67,421.10</td>
                                    <td class="p-6 text-green-500 font-bold">+2.41%</td>
                                    <td class="p-6 text-right"><button class="bg-[#f3ba2f] text-black text-[10px] font-black px-4 py-1 rounded-full">TRADE</button></td>
                                </tr>
                                <tr class="hover:bg-white/5 transition">
                                    <td class="p-6 flex items-center gap-3"><div class="w-8 h-8 rounded-full bg-blue-500/20 flex items-center justify-center font-bold text-xs">Ξ</div> Ethereum</td>
                                    <td class="p-6 font-mono font-bold">$3,842.50</td>
                                    <td class="p-6 text-red-500 font-bold">-0.12%</td>
                                    <td class="p-6 text-right"><button class="bg-[#f3ba2f] text-black text-[10px] font-black px-4 py-1 rounded-full">TRADE</button></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <div id="trans-modal" class="fixed inset-0 z-[100] bg-black/80 backdrop-blur-sm hidden flex items-center justify-center p-6">
        <div class="glass w-full max-w-md rounded-3xl p-8 animate__animated animate__fadeInDown">
            <div class="flex justify-between items-center mb-8">
                <h3 id="modal-title" class="text-2xl font-black uppercase tracking-tight">Deposit Funds</h3>
                <button onclick="closeModal()" class="text-gray-500 hover:text-white text-2xl">&times;</button>
            </div>
            
            <div class="space-y-6">
                <div>
                    <label class="text-[10px] uppercase text-gray-500 font-bold">Select Method</label>
                    <select class="w-full bg-[#161a1e] p-4 rounded-xl border border-gray-800 outline-none focus:border-[#f3ba2f] mt-2">
                        <option>USDT (TRC20)</option>
                        <option>Bank Transfer (Swift)</option>
                        <option>Credit/Debit Card</option>
                        <option>PayPal / Payoneer</option>
                    </select>
                </div>
                <div>
                    <label class="text-[10px] uppercase text-gray-500 font-bold">Amount (USD)</label>
                    <input id="trans-amount" type="number" placeholder="0.00" class="w-full bg-[#161a1e] p-4 rounded-xl border border-gray-800 outline-none focus:border-[#f3ba2f] mt-2 text-2xl font-bold">
                </div>
                <button onclick="executeTransaction()" id="modal-btn" class="w-full gold-btn text-black font-black py-4 rounded-2xl">CONFIRM DEPOSIT</button>
            </div>
        </div>
    </div>

    <script>
        let balance = 12500;
        let activeMode = 'deposit';

        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0,0);
        }

        function handleAuth(manualName) {
            const name = manualName || document.getElementById('in-name').value || "Elite Trader";
            document.getElementById('auth-zone').classList.add('hidden');
            document.getElementById('user-zone').classList.remove('hidden');
            document.getElementById('user-name').innerText = name;
            document.getElementById('user-name-span').innerText = name;
            showSection('dashboard');
        }

        function openModal(mode) {
            activeMode = mode;
            document.getElementById('modal-title').innerText = mode === 'deposit' ? 'Deposit Funds' : 'Withdraw Funds';
            document.getElementById('modal-btn').innerText = mode === 'deposit' ? 'CONFIRM DEPOSIT' : 'REQUEST WITHDRAWAL';
            document.getElementById('trans-modal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('trans-modal').classList.add('hidden');
        }

        function executeTransaction() {
            const amt = parseFloat(document.getElementById('trans-amount').value);
            if(!amt || amt <= 0) return alert("Please enter a valid amount.");
            
            if(activeMode === 'withdraw' && amt > balance) return alert("Insufficient balance!");

            balance = activeMode === 'deposit' ? balance + amt : balance - amt;
            document.getElementById('balance-val').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
            
            alert(`${activeMode.toUpperCase()} of $${amt} processed successfully!`);
            closeModal();
            document.getElementById('trans-amount').value = '';
        }

        // Live Price Animation
        setInterval(() => {
            const btc = 67000 + (Math.random() * 800);
            const nas = 18000 + (Math.random() * 300);
            document.getElementById('p-btc').innerText = '$' + btc.toLocaleString(undefined, {minimumFractionDigits: 2});
            document.getElementById('p-nas').innerText = '$' + nas.toLocaleString(undefined, {minimumFractionDigits: 2});
        }, 2000);
    </script>
</body>
</html>
