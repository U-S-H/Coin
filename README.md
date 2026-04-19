<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nexus Capital | Global Institutional Grade</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --primary: #f3ba2f; --bg: #030508; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; }
        .glass-card { background: rgba(18, 22, 28, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.05); transition: 0.4s; }
        .glass-card:hover { border-color: var(--primary); transform: translateY(-5px); }
        .gold-btn { background: linear-gradient(135deg, #f3ba2f 0%, #d49e00 100%); color: #000; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; }
        .hidden-section { display: none; }
        .profit-up { color: #00ff88; text-shadow: 0 0 10px rgba(0,255,136,0.3); }
        .sidebar-active { border-right: 3px solid var(--primary); background: rgba(243, 186, 47, 0.05); }
    </style>
</head>
<body>

    <div class="flex min-h-screen">
        
        <aside id="sidebar" class="hidden md:flex w-64 border-r border-gray-900 flex-col p-6 sticky top-0 h-screen bg-[#030508]">
            <div class="flex items-center gap-2 mb-10">
                <div class="w-8 h-8 bg-[#f3ba2f] rounded-lg flex items-center justify-center text-black font-black">N</div>
                <span class="font-black text-xl tracking-tighter italic">NEXUS</span>
            </div>
            <nav class="space-y-4 flex-1">
                <a href="#" class="flex items-center gap-3 p-3 rounded-xl sidebar-active text-sm"><span>🏠</span> Dashboard</a>
                <a href="#" class="flex items-center gap-3 p-3 rounded-xl text-gray-500 hover:text-white transition text-sm"><span>📈</span> Trade Markets</a>
                <a href="#" class="flex items-center gap-3 p-3 rounded-xl text-gray-500 hover:text-white transition text-sm"><span>💎</span> Staking Plans</a>
                <a href="#" class="flex items-center gap-3 p-3 rounded-xl text-gray-500 hover:text-white transition text-sm"><span>👥</span> Affiliates</a>
                <a href="#" onclick="openSupport()" class="flex items-center gap-3 p-3 rounded-xl text-gray-500 hover:text-white transition text-sm"><span>🎧</span> Support</a>
            </nav>
            <div class="mt-auto p-4 glass-card rounded-2xl">
                <p class="text-[10px] text-gray-500 uppercase font-bold">Server Status</p>
                <p class="text-[10px] text-green-500 font-bold">● Global Nodes Active</p>
            </div>
        </aside>

        <main class="flex-1 overflow-y-auto">
            
            <nav class="flex items-center justify-between px-8 py-6 sticky top-0 bg-[#030508]/80 backdrop-blur-xl z-50">
                <h2 id="page-title" class="text-lg font-black uppercase tracking-widest text-gray-400">Overview</h2>
                <div id="user-info" class="hidden flex items-center gap-4">
                    <div class="flex flex-col items-end">
                        <span id="user-name" class="font-bold text-sm text-[#f3ba2f]"></span>
                        <span class="text-[9px] bg-white/10 px-2 py-0.5 rounded text-gray-300">IP: 182.164.x.x</span>
                    </div>
                    <button onclick="location.reload()" class="w-10 h-10 rounded-full bg-gray-900 border border-gray-800 flex items-center justify-center">🚪</button>
                </div>
                <div id="auth-buttons">
                    <button onclick="showSection('signup')" class="gold-btn px-6 py-2 rounded-full text-xs">Access Account</button>
                </div>
            </nav>

            <div id="landing-section" class="section p-12 text-center animate__animated animate__fadeIn">
                <h1 class="text-7xl font-black mb-6">World Wide <br><span class="text-[#f3ba2f]">Dollar</span> Liquidity.</h1>
                <p class="text-gray-500 max-w-xl mx-auto mb-10">Nexus Capital provides institutional grade investment tools for retail traders worldwide.</p>
                <div class="flex justify-center gap-4">
                    <button onclick="showSection('signup')" class="gold-btn px-10 py-4 rounded-2xl">Start Investing</button>
                </div>
            </div>

            <section id="signup-section" class="section hidden-section p-12 flex justify-center animate__animated animate__zoomIn">
                <div class="glass-card p-10 rounded-3xl w-full max-w-md">
                    <h2 class="text-3xl font-black mb-6">Verify Identity</h2>
                    <input id="in-name" type="text" placeholder="Your Name" class="w-full bg-[#0a0c10] p-4 rounded-xl mb-4 border border-gray-800 outline-none focus:border-[#f3ba2f]">
                    <input type="email" placeholder="Email Address" class="w-full bg-[#0a0c10] p-4 rounded-xl mb-6 border border-gray-800 outline-none">
                    <button onclick="handleAuth()" class="w-full gold-btn py-4 rounded-xl">Initialize</button>
                </div>
            </section>

            <section id="dashboard-section" class="section hidden-section p-8 animate__animated animate__fadeInUp">
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-6 mb-8">
                    <div class="glass-card p-8 rounded-[32px] col-span-2">
                        <p class="text-xs font-bold text-gray-500 mb-2 uppercase tracking-widest">Available Liquidity</p>
                        <div class="flex items-baseline gap-4">
                            <h2 id="balance-val" class="text-5xl font-black tracking-tighter italic">$12,500.00</h2>
                            <span id="profit-tick" class="text-xs font-bold profit-up">+0.00%</span>
                        </div>
                        <div class="flex gap-3 mt-8">
                            <button onclick="openModal('Deposit')" class="gold-btn px-8 py-3 rounded-xl text-xs">Add Funds</button>
                            <button onclick="openModal('Withdraw')" class="bg-white/5 px-8 py-3 rounded-xl text-xs font-bold hover:bg-white/10 transition">Extract</button>
                        </div>
                    </div>
                    <div class="glass-card p-8 rounded-[32px] flex flex-col justify-center">
                        <p class="text-xs font-bold text-gray-500 mb-4 uppercase">Asset Distribution</p>
                        <div class="space-y-3">
                            <div class="flex justify-between text-sm"><span class="text-gray-400">Bitcoin</span><span id="btc-val">0.024 BTC</span></div>
                            <div class="flex justify-between text-sm"><span class="text-gray-400">Ethereum</span><span id="eth-val">0.45 ETH</span></div>
                            <div class="w-full bg-gray-900 h-1.5 rounded-full mt-4 overflow-hidden">
                                <div class="bg-[#f3ba2f] h-full" style="width: 70%"></div>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                    <div class="lg:col-span-2 glass-card rounded-[32px] overflow-hidden">
                        <div class="p-6 border-b border-gray-900 flex justify-between items-center">
                            <h3 class="font-black text-xs uppercase tracking-widest">Terminal Feed</h3>
                            <span class="text-[10px] text-gray-500 font-mono">UTC: 2026-04-19</span>
                        </div>
                        <div class="p-6 space-y-4 font-mono text-[11px]" id="terminal-feed">
                            <p class="text-green-500 text-xs tracking-tighter">>>> Nexus Global Node Connected...</p>
                            <p class="text-gray-500 tracking-tighter">>>> API handshake successful (0.4ms)...</p>
                        </div>
                    </div>

                    <div class="glass-card p-6 rounded-[32px]">
                        <h3 class="font-black text-xs uppercase tracking-widest mb-6">Concierge Support</h3>
                        <textarea id="support-msg" placeholder="Message to account manager..." class="w-full bg-[#0a0c10] border border-gray-800 rounded-2xl p-4 text-xs outline-none focus:border-[#f3ba2f] h-32"></textarea>
                        <button onclick="sendSupport()" class="w-full mt-4 bg-white text-black py-3 rounded-xl text-xs font-black">SEND TICKET</button>
                    </div>
                </div>
            </section>
        </main>
    </div>

    <div id="trans-modal" class="fixed inset-0 z-[100] bg-black/95 backdrop-blur-xl hidden flex items-center justify-center p-6">
        <div class="glass-card w-full max-w-sm rounded-[40px] p-10 animate__animated animate__fadeInDown">
            <h3 id="modal-title" class="text-2xl font-black mb-8 italic uppercase tracking-tighter">Deposit</h3>
            <input id="trans-amount" type="number" placeholder="0.00 USD" class="w-full bg-transparent text-4xl font-black border-b-2 border-gray-800 outline-none focus:border-[#f3ba2f] pb-4 mb-10 text-center">
            <button onclick="confirmTrans()" class="gold-btn w-full py-4 rounded-2xl">Confirm Execution</button>
            <button onclick="closeModal()" class="w-full mt-4 text-gray-500 text-xs font-bold">CANCEL</button>
        </div>
    </div>

    <script>
        let balance = 12500.00;
        let mode = '';

        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            if(id === 'dashboard') document.getElementById('page-title').innerText = 'Institutional Terminal';
        }

        function handleAuth() {
            const name = document.getElementById('in-name').value || "Nexus Member";
            document.getElementById('auth-buttons').classList.add('hidden');
            document.getElementById('user-info').classList.remove('hidden');
            document.getElementById('user-name').innerText = name;
            showSection('dashboard');
            startLiveTicker();
        }

        function startLiveTicker() {
            setInterval(() => {
                let change = (Math.random() * 0.05).toFixed(4);
                balance += parseFloat(change);
                document.getElementById('balance-val').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
                document.getElementById('profit-tick').innerText = `+${(Math.random()*2).toFixed(2)}%`;
                
                // Update BTC/ETH ratio
                document.getElementById('btc-val').innerText = (balance * 0.00000037).toFixed(6) + " BTC";
                document.getElementById('eth-val').innerText = (balance * 0.000036).toFixed(4) + " ETH";
            }, 4000);
        }

        function openModal(m) { mode = m; document.getElementById('modal-title').innerText = m; document.getElementById('trans-modal').classList.remove('hidden'); }
        function closeModal() { document.getElementById('trans-modal').classList.add('hidden'); }

        function confirmTrans() {
            const val = parseFloat(document.getElementById('trans-amount').value);
            if(!val) return;
            balance = mode === 'Deposit' ? balance + val : balance - val;
            document.getElementById('balance-val').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
            
            const feed = document.getElementById('terminal-feed');
            feed.innerHTML += `<p class="text-green-500 tracking-tighter">>>> [SUCCESS] ${mode} of $${val} confirmed by network.</p>`;
            
            closeModal();
            document.getElementById('trans-amount').value = '';
        }

        function sendSupport() {
            const msg = document.getElementById('support-msg').value;
            if(!msg) return;
            alert("Ticket Opened: Your account manager will contact you shortly via encrypted mail.");
            document.getElementById('support-msg').value = '';
        }
    </script>
</body>
</html>
