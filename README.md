<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GlobalInvest | Simulator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #0b0e11; color: #eaecef; transition: all 0.3s ease; }
        .gold-gradient { background: linear-gradient(90deg, #f3ba2f 0%, #f0b90b 100%); }
        .card-bg { background-color: #1e2329; border: 1px solid #363c44; }
        .hidden-section { display: none; }
    </style>
</head>
<body class="font-sans">

    <nav class="flex items-center justify-between px-8 py-4 border-b border-gray-800">
        <div class="text-2xl font-bold text-[#f3ba2f] cursor-pointer" onclick="showSection('landing')">GLOBAL<span class="text-white">INVEST</span></div>
        <div id="nav-links" class="hidden md:flex space-x-6 text-sm font-medium">
            <a href="#" class="hover:text-[#f3ba2f]">Market</a>
            <a href="#" class="hover:text-[#f3ba2f]">Trade</a>
        </div>
        <div id="auth-buttons">
            <button onclick="showSection('login')" class="text-gray-400 mr-4 hover:text-white">Login</button>
            <button onclick="showSection('signup')" class="gold-gradient text-black px-6 py-2 rounded font-bold text-sm">Join Now</button>
        </div>
        <div id="user-profile" class="hidden-section flex items-center">
            <span id="display-name" class="mr-4 text-[#f3ba2f] font-bold"></span>
            <button onclick="logout()" class="text-xs bg-red-600 px-2 py-1 rounded text-white">Logout</button>
        </div>
    </nav>

    <div id="landing-section" class="section">
        <header class="text-center py-20 px-4">
            <h1 class="text-5xl md:text-6xl font-extrabold mb-6">Invest in <span class="text-[#f3ba2f]">USD</span></h1>
            <p class="text-gray-400 text-lg max-w-2xl mx-auto mb-8">World's most advanced investment simulator.</p>
            <button onclick="showSection('signup')" class="gold-gradient text-black px-10 py-4 rounded font-bold text-lg">Create Free Account</button>
        </header>
    </div>

    <div id="signup-section" class="section hidden-section flex justify-center py-20">
        <div class="card-bg p-8 rounded-xl w-96">
            <h2 class="text-2xl font-bold mb-6 text-center text-[#f3ba2f]">Create Account</h2>
            <input id="signup-name" type="text" placeholder="Full Name" class="w-full bg-[#2b3139] p-3 rounded mb-4 border border-gray-700 focus:border-[#f3ba2f] outline-none">
            <input id="signup-email" type="email" placeholder="Email Address" class="w-full bg-[#2b3139] p-3 rounded mb-4 border border-gray-700 focus:border-[#f3ba2f] outline-none">
            <input type="password" placeholder="Password" class="w-full bg-[#2b3139] p-3 rounded mb-6 border border-gray-700 focus:border-[#f3ba2f] outline-none">
            <button onclick="handleAuth('signup')" class="w-full gold-gradient text-black font-bold py-3 rounded">Sign Up</button>
        </div>
    </div>

    <div id="login-section" class="section hidden-section flex justify-center py-20">
        <div class="card-bg p-8 rounded-xl w-96">
            <h2 class="text-2xl font-bold mb-6 text-center text-[#f3ba2f]">Login</h2>
            <input id="login-email" type="email" placeholder="Email" class="w-full bg-[#2b3139] p-3 rounded mb-4 border border-gray-700 focus:border-[#f3ba2f] outline-none">
            <input type="password" placeholder="Password" class="w-full bg-[#2b3139] p-3 rounded mb-6 border border-gray-700 focus:border-[#f3ba2f] outline-none">
            <button onclick="handleAuth('login')" class="w-full gold-gradient text-black font-bold py-3 rounded">Login</button>
        </div>
    </div>

    <div id="dashboard-section" class="section hidden-section px-8 py-10">
        <h2 class="text-3xl font-bold mb-8">Welcome Back, <span id="user-name-span" class="text-[#f3ba2f]">User</span>!</h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
            <div class="card-bg p-6 rounded-xl">
                <p class="text-gray-400 text-sm">Total Balance</p>
                <h3 class="text-4xl font-bold mt-2 text-green-500">$5,420.00</h3>
            </div>
            <div class="card-bg p-6 rounded-xl border-l-4 border-yellow-500">
                <p class="text-gray-400 text-sm">Active Investments</p>
                <h3 class="text-4xl font-bold mt-2">$1,200.00</h3>
            </div>
            <div class="card-bg p-6 rounded-xl">
                <p class="text-gray-400 text-sm">Profit (24h)</p>
                <h3 class="text-4xl font-bold mt-2 text-green-400">+$124.50</h3>
            </div>
        </div>
    </div>

    <script>
        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.section').forEach(section => {
                section.classList.add('hidden-section');
            });
            // Show target section
            document.getElementById(sectionId + '-section').classList.remove('hidden-section');
        }

        function handleAuth(type) {
            let name = "Investor";
            if(type === 'signup') {
                name = document.getElementById('signup-name').value || "New Member";
            } else {
                name = "Investor"; // Simulated login
            }

            // UI Changes
            document.getElementById('auth-buttons').classList.add('hidden-section');
            document.getElementById('user-profile').classList.remove('hidden-section');
            document.getElementById('display-name').innerText = name;
            document.getElementById('user-name-span').innerText = name;

            showSection('dashboard');
            alert(type.toUpperCase() + " Successful! (Simulation Mode)");
        }

        function logout() {
            document.getElementById('auth-buttons').classList.remove('hidden-section');
            document.getElementById('user-profile').classList.add('hidden-section');
            showSection('landing');
        }
    </script>
</body>
</html>
