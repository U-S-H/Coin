<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GlobalInvest | Secure Dollar Trading</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #0b0e11; color: #eaecef; }
        .gold-gradient { background: linear-gradient(90deg, #f3ba2f 0%, #f0b90b 100%); }
        .card-bg { background-color: #1e2329; border: 1px solid #363c44; }
    </style>
</head>
<body class="font-sans">

    <nav class="flex items-center justify-between px-8 py-4 border-b border-gray-800">
        <div class="text-2xl font-bold text-[#f3ba2f]">GLOBAL<span class="text-white">INVEST</span></div>
        <div class="hidden md:flex space-x-6 text-sm font-medium">
            <a href="#" class="hover:text-[#f3ba2f]">Market</a>
            <a href="#" class="hover:text-[#f3ba2f]">Trade</a>
            <a href="#" class="hover:text-[#f3ba2f]">Portfolio</a>
        </div>
        <button class="gold-gradient text-black px-6 py-2 rounded font-bold text-sm">Get Started</button>
    </nav>

    <header class="text-center py-20 px-4">
        <h1 class="text-5xl md:text-6xl font-extrabold mb-6">Invest in <span class="text-[#f3ba2f]">USD</span> Globally</h1>
        <p class="text-gray-400 text-lg max-w-2xl mx-auto mb-8">
            The most secure platform to grow your wealth in Dollars. Start your journey with as little as $10.
        </p>
        <div class="flex justify-center space-x-4">
            <input type="text" placeholder="Email Address" class="bg-[#2b3139] px-4 py-3 rounded w-64 focus:outline-none border border-transparent focus:border-[#f3ba2f]">
            <button class="gold-gradient text-black px-8 py-3 rounded font-bold">Register Now</button>
        </div>
    </header>

    <main class="max-w-5xl mx-auto px-4 pb-20">
        <div class="card-bg rounded-xl p-6 shadow-2xl">
            <div class="flex justify-between items-center mb-6">
                <h2 class="text-xl font-bold">Live Markets</h2>
                <span class="text-[#f3ba2f] cursor-pointer">View More ></span>
            </div>
            
            <table class="w-full text-left">
                <thead class="text-gray-500 border-b border-gray-700">
                    <tr>
                        <th class="pb-4">Asset</th>
                        <th class="pb-4">Price</th>
                        <th class="pb-4">24h Change</th>
                        <th class="pb-4">Trend</th>
                    </tr>
                </thead>
                <tbody class="divide-y divide-gray-800">
                    <tr>
                        <td class="py-4 font-bold">USD / Gold</td>
                        <td class="py-4">$2,145.50</td>
                        <td class="py-4 text-green-500">+1.24%</td>
                        <td class="py-4 text-green-500">↗</td>
                    </tr>
                    <tr>
                        <td class="py-4 font-bold">Real Estate Index</td>
                        <td class="py-4">$542.10</td>
                        <td class="py-4 text-red-500">-0.45%</td>
                        <td class="py-4 text-red-500">↘</td>
                    </tr>
                    <tr>
                        <td class="py-4 font-bold">Global Tech Fund</td>
                        <td class="py-4">$128.90</td>
                        <td class="py-4 text-green-500">+3.10%</td>
                        <td class="py-4 text-green-500">↗</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </main>

    <footer class="text-center py-10 border-t border-gray-800 text-gray-500 text-sm">
        &copy; 2026 GlobalInvest Inc. All Rights Reserved. Secure & Encrypted.
    </footer>

</body>
</html>
