<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GlobalInvest Pro | Ultimate Simulator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #0b0e11; color: #eaecef; overflow-x: hidden; }
        .gold-gradient { background: linear-gradient(90deg, #f3ba2f 0%, #f0b90b 100%); }
        .card-bg { background-color: #1e2329; border: 1px solid #363c44; transition: 0.3s; }
        .card-bg:hover { border-color: #f3ba2f; }
        .hidden-section { display: none; }
        .chart-placeholder { background: linear-gradient(180deg, #1e2329 0%, #0b0e11 100%); height: 200px; position: relative; }
        .pulse { animation: pulse-animation 2s infinite; }
        @keyframes pulse-animation { 0% { opacity: 1; } 50% { opacity: 0.5; } 100% { opacity: 1; } }
    </style>
</head>
<body class="font-sans">

    <nav class="flex items-center justify-between px-6 py-4 border-b border-gray-800 sticky top-0 bg-[#0b0e11] z-50">
        <div class="text-2xl font-bold text-[#f3ba2f] cursor-pointer" onclick="showSection('landing')">GLOBAL<span class="text-white">INVEST</span></div>
        <div id="auth-buttons">
            <button onclick="showSection('login')" class="text-gray-400 mr-4 hover:text-white">Login</button>
            <button onclick="showSection('signup')" class="gold-gradient text-black px-5 py-2 rounded-lg font-bold text-sm shadow-lg shadow-yellow-500/20">Sign Up</button>
        </div>
        <div id="user-profile" class="hidden-section flex items-center">
            <div class="flex flex-col items-end mr-4">
                <span id="display-name" class="text-[#f3ba2f] font-bold text-sm"></span>
                <span class="text-[10px] text-green-500 uppercase tracking-widest">Verified</span>
            </div>
            <button onclick="logout()" class="bg-gray-800 p-2 rounded-full hover:bg-red-900 transition"><img src="https://img.icons8.com/ios-glyphs/20/ffffff/logout-rounded.png"/></button>
        </div>
    </nav>

    <section id="landing-section" class="section text-center py-24 px-4">
        <div class="inline-block bg-yellow-500/10 text-[#f3ba2f] px-4 py-1 rounded-full text-xs font-bold mb-6 border border-yellow-500/20">NEW: 2026 WORLDWIDE TRADING ACTIVE</div>
        <h1 class="text-5xl md:text-7xl font-extrabold mb-6 tracking-tight">Invest Dollars <br><span class="text-[#f3ba2f]">Without Borders</span></h1>
        <p class="text-gray-400 text-lg max-w-2xl mx-auto mb-10 leading-relaxed">Experience the world's most powerful investment simulator. Trade Stocks, Crypto, and Forex in real-time USD markets.</p>
        <button onclick="showSection('signup')" class="gold-gradient text-black px-12 py-4 rounded-xl font-black text-lg hover:scale-105 transition-transform shadow-xl shadow-yellow-500/30">START TRADING NOW</button>
    </section>

    <section id="signup-section" class="section hidden-section flex justify-center py-20 px-4">
        <div class="card-bg p-10 rounded-2xl w-full max-w-md shadow-2xl">
            <h2 class="text-3xl font-bold mb-2">Create Account</h2>
            <p class="text-gray-500 mb-8">Join thousands of global investors.</p>
            <input id="signup-name" type="text" placeholder="Full Name" class="w-full bg-[#2b3139] p-4 rounded-xl mb-4 border border-gray-700 outline-none focus:border-[#f3ba2f]">
            <input type="email" placeholder="Email Address" class="w-full bg-[#2b3139] p-4 rounded-xl mb-4 border border-gray-700 outline-none">
            <input type="password" placeholder="Password" class="w-full bg-[#2b3139] p-4 rounded-xl mb-6 border border-gray-700 outline-none">
            <button onclick="handleAuth('signup')" class="w-full gold-gradient text-black font-black py-4 rounded-xl shadow-lg">CREATE ACCOUNT</button>
        </div>
    </section>

    <section id="login-section" class="section hidden-section flex justify-center py-20 px-4">
        <div class="card-bg p-10 rounded-2xl w-full max-w-md shadow-2xl">
            <h2 class="text-3xl font-bold mb-2">Welcome Back</h2>
            <p class="text-gray-500 mb-8">Login to manage your portfolio.</p>
            <input id="login-email" type="email" placeholder="Email" class="w-full bg-[#2b3139] p-4 rounded-xl mb-4 border border-gray-700 outline-none">
            <input type="password" placeholder="Password" class="w-full bg-[#2b3139] p-4 rounded-xl mb-6 border border-gray-700 outline-none text-white">
            <button onclick="handleAuth('login')" class="w-full gold-gradient text-black font-black py-4 rounded-xl shadow-lg">LOGIN</button>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section px-6 md:px-12 py-10">
        <div class="flex flex-col md:flex-row justify-between items-start md:items-center mb-10">
            <div>
                <h2 class="text-3xl font-black">Dashboard</h2>
                <p class="text-gray-500">Good to see you, <span id="user-name-span" class="text-[#f3ba2f]"></span></p>
            </div>
            <div class="flex gap-3 mt-4 md:mt-0">
                <button onclick="updateBalance(500)" class="bg-green-600/20 text-green-500 border border-green-600/50 px-4 py-2 rounded-lg font-bold text-xs">+ DEPOSIT $</button>
                <button onclick="updateBalance(-500)" class="bg-gray-800 text-gray-400 px-4 py-2 rounded-lg font-bold text-xs">WITHDRAW</button>
            </div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-10">
            <div class="card-bg p-6 rounded-2xl relative overflow-hidden">
                <p class="text-gray-400 text-xs font-bold uppercase tracking-wider">Total Portfolio Balance</p>
                <h3 id="main-balance" class="text-4xl font-black mt-2 text-white">$10,000.00</h3>
                <div class="absolute bottom-0 left-0 h-1 bg-[#f3ba2f] w-full"></div>
            </div>
            <div class="card-bg p-6 rounded-2xl">
                <p class="text-gray-400 text-xs font-bold uppercase tracking-wider">24h Profit / Loss</p>
                <h3 class="text-4xl font-black mt-2 text-green-500">+$842.10 <span class="text-sm font-normal">(+8.4%)</span></h3>
            </div>
            <div class="card-bg p-6 rounded-2xl">
                <p class="text-gray-400 text-xs font-bold uppercase tracking-wider">Total Assets Managed</p>
                <h3 class="text-4xl font-black mt-2">12 <span class="text-sm font-normal text-gray-500">Items</span></h3>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <div class="lg:col-span-2 card-bg rounded-2xl overflow-hidden">
                <div class="p-6 border-b border-gray-800 flex justify-between items-center">
                    <h4 class="font-bold">Live Global Market</h4>
                    <span class="flex items-center text-[10px] text-green-500"><span class="w-2 h-2 bg-green-500 rounded-full mr-2 pulse"></span> LIVE STREAMING</span>
                </div>
                <div class="overflow-x-auto">
                    <table class="w-full text-left">
                        <thead class="text-gray-500 text-xs uppercase bg-[#161a1e]">
                            <tr>
                                <th class="p-4 text-white">Asset</th>
                                <th class="p-4">Price (USD)</th>
                                <th class="p-4">Change</th>
                                <th class="p-4 text-center">Trade</th>
                            </tr>
                        </thead>
                        <tbody id="market-body" class="divide-y divide-gray-800 text-sm">
                            </tbody>
                    </table>
                </div>
            </div>

            <div class="card-bg rounded-2xl p-6">
                <h4 class="font-bold mb-6">Recent Activity</h4>
                <div class="space-y-6">
                    <div class="flex gap-4">
                        <div class="w-10 h-10 bg-green-500/20 rounded-full flex items-center justify-center text-green-500">↑</div>
                        <div>
                            <p class="text-sm font-bold">Bitcoin Buy Order</p>
                            <p class="text-[10px] text-gray-500">2 minutes ago • Executed</p>
                        </div>
                    </div>
                    <div class="flex gap-4">
                        <div class="w-10 h-10 bg-[#f3ba2f]/20 rounded-full flex items-center justify-center text-[#f3ba2f]">$</div>
                        <div>
                            <p class="text-sm font-bold">Bonus Reward Received</p>
                            <p class="text-[10px] text-gray-500">5 hours ago • System</p>
                        </div>
                    </div>
                </div>
                <div class="mt-10 p-4 bg-[#f3ba2f] rounded-xl text-black">
                    <p class="font-black text-sm uppercase">Global Tip:</p>
                    <p class="text-xs leading-tight mt-1">Diversify your portfolio by investing in both Crypto and Forex to reduce risk.</p>
                </div>
            </div>
        </div>
    </section>

    <footer class="text-center py-12 text-gray-600 text-[10px] uppercase tracking-widest border-t border-gray-900 mt-10">
        &copy; 2026 GLOBALINVEST PLATFORM • SECURED BY END-TO-END ENCRYPTION • WORLDWIDE ACCESS
    </footer>

    <script>
        let balance = 10000;
        const assets = [
            { name: 'Bitcoin', symbol: 'BTC', price: 64230, change: '+2.4%', color: 'text-green-500' },
            { name: 'Ethereum', symbol: 'ETH', price: 3450, change: '-1.1%', color: 'text-red-500' },
            { name: 'Tesla Inc.', symbol: 'TSLA', price: 182.40, change: '+5.7%', color: 'text-green-500' },
            { name: 'Gold Index', symbol: 'XAU', price: 2150, change: '+0.2%', color: 'text-green-500' }
        ];

        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0, 0);
        }

        function handleAuth(type) {
            const name = document.getElementById('signup-name').value || "Global Trader";
            document.getElementById('auth-buttons').classList.add('hidden-section');
            document.getElementById('user-profile').classList.remove('hidden-section');
            document.getElementById('display-name').innerText = name;
            document.getElementById('user-name-span').innerText = name;
            showSection('dashboard');
            populateMarket();
        }

        function logout() {
            location.reload();
        }

        function populateMarket() {
            const body = document.getElementById('market-body');
            body.innerHTML = '';
            assets.forEach(asset => {
                body.innerHTML += `
                    <tr class="hover:bg-[#2b3139] transition cursor-pointer">
                        <td class="p-4 font-bold text-white">${asset.name} <span class="text-gray-500 text-[10px] ml-2">${asset.symbol}</span></td>
                        <td class="p-4 font-mono">$${asset.price.toLocaleString()}</td>
                        <td class="p-4 ${asset.color} font-bold">${asset.change}</td>
                        <td class="p-4 text-center"><button class="bg-[#2b3139] px-3 py-1 rounded text-xs border border-gray-700 hover:border-[#f3ba2f]">Buy</button></td>
                    </tr>
                `;
            });
        }

        function updateBalance(amt) {
            balance += amt;
            document.getElementById('main-balance').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
            if(amt > 0) alert("Simulation: $"+amt+" deposited successfully!");
        }

        // Price Animation
        setInterval(() => {
            const prices = document.querySelectorAll('.font-mono');
            prices.forEach(p => {
                let current = parseFloat(p.innerText.replace('$', '').replace(',', ''));
                let change = (Math.random() - 0.5) * 10;
                p.innerText = '$' + (current + change).toLocaleString(undefined, {minimumFractionDigits: 2});
            });
        }, 3000);
    </script>
</body>
</html>
