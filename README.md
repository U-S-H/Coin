<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS PRO | Ultimate Institutional Suite</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --dark: #020406; --card: #0b0e11; }
        body { background-color: var(--dark); color: #ffffff; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .glass { background: rgba(11, 14, 17, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.05); }
        .gold-glow { box-shadow: 0 0 20px rgba(243, 186, 47, 0.15); border: 1px solid var(--gold) !important; }
        .nav-link:hover { color: var(--gold); border-bottom: 2px solid var(--gold); }
        .hidden-section { display: none; }
        .crypto-card { transition: 0.3s; cursor: pointer; border-radius: 20px; }
        .crypto-card:hover { background: rgba(255,255,255,0.03); transform: translateY(-5px); }
        input::-webkit-outer-spin-button, input::-webkit-inner-spin-button { -webkit-appearance: none; }
    </style>
</head>
<body>

    <div class="w-full bg-[#161a1e] py-1 border-b border-gray-800 flex overflow-hidden whitespace-nowrap">
        <div class="flex animate-[scroll_20s_linear_infinite] gap-10 text-[10px] font-bold text-gray-400">
            <span>BTC/USD <span class="text-green-500">$67,842.10 ↑</span></span>
            <span>ETH/USD <span class="text-red-500">$3,421.50 ↓</span></span>
            <span>BNB/USD <span class="text-green-500">$592.12 ↑</span></span>
            <span>GOLD/USD <span class="text-yellow-500">$2,142.10 ↑</span></span>
            <span>CRUDE OIL <span class="text-red-500">$84.20 ↓</span></span>
            <span>BTC/USD <span class="text-green-500">$67,842.10 ↑</span></span>
        </div>
    </div>

    <nav class="glass sticky top-0 z-[100] px-6 py-4 flex items-center justify-between border-b border-gray-800">
        <div class="flex items-center gap-10">
            <div class="flex items-center gap-2 cursor-pointer" onclick="location.reload()">
                <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl">N</div>
                <span class="text-xl font-black tracking-tighter uppercase italic">Nexus<span class="text-[#f3ba2f]">Pro</span></span>
            </div>
            <div class="hidden lg:flex gap-6 text-[11px] font-bold text-gray-400 uppercase tracking-widest">
                <a href="#" class="nav-link">Spot</a>
                <a href="#" class="nav-link">Futures</a>
                <a href="#" class="nav-link">P2P</a>
                <a href="#" class="nav-link">Academy</a>
            </div>
        </div>
        <div id="auth-box" class="flex gap-4 items-center">
            <button onclick="showSection('login')" class="text-xs font-bold text-gray-400 hover:text-white">Sign In</button>
            <button onclick="showSection('signup')" class="bg-[#f3ba2f] text-black px-6 py-2 rounded-lg font-black text-xs">JOIN ELITE</button>
        </div>
        <div id="user-box" class="hidden flex items-center gap-4">
            <div class="bg-gray-800 px-4 py-1.5 rounded-full border border-gray-700">
                <span id="bal-top" class="text-xs font-black text-[#f3ba2f]">$0.00</span>
            </div>
            <button onclick="showSection('dashboard')" class="w-10 h-10 rounded-full border-2 border-[#f3ba2f] flex items-center justify-center font-bold">U</button>
        </div>
    </nav>

    <section id="landing-section" class="section py-24 px-6 text-center animate__animated animate__fadeIn">
        <div class="inline-flex items-center gap-2 bg-white/5 border border-white/10 px-4 py-1.5 rounded-full mb-8">
            <span class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></span>
            <span class="text-[10px] font-bold tracking-widest text-gray-400 uppercase">Institutional Liquidity Provider 2026</span>
        </div>
        <h1 class="text-6xl md:text-9xl font-black tracking-tighter mb-8 italic">THE FUTURE OF<br><span class="text-[#f3ba2f]">GLOBAL WEALTH.</span></h1>
        <p class="text-gray-500 max-w-2xl mx-auto mb-12 text-lg">Nexus Pro is the world’s leading digital asset ecosystem for professional investors. Zero-latency trading, worldwide dollar settlement.</p>
        <button onclick="showSection('signup')" class="bg-[#f3ba2f] text-black px-12 py-5 rounded-2xl font-black text-xl hover:scale-105 transition-all shadow-2xl shadow-yellow-500/20">START YOUR EMPIRE</button>
    </section>

    <section id="signup-section" class="section hidden-section flex justify-center py-20 animate__animated animate__zoomIn">
        <div class="glass p-12 rounded-[40px] w-full max-w-md border border-gray-800">
            <h2 class="text-4xl font-black mb-2 italic uppercase">Register</h2>
            <p class="text-gray-500 text-xs mb-8 tracking-widest uppercase">Securing your financial freedom</p>
            <div class="space-y-4">
                <input id="in-name" type="text" placeholder="Full Name" class="w-full bg-white/5 p-4 rounded-xl border border-white/10 outline-none focus:border-[#f3ba2f] transition">
                <input type="email" placeholder="Institutional Email" class="w-full bg-white/5 p-4 rounded-xl border border-white/10 outline-none">
                <input type="password" placeholder="Password" class="w-full bg-white/5 p-4 rounded-xl border border-white/10 outline-none">
                <div class="flex items-center gap-2 p-2"><input type="checkbox" checked><span class="text-[10px] text-gray-500">I agree to the 2026 Global Asset Policy.</span></div>
                <button onclick="handleAuth()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-lg">CREATE ACCOUNT</button>
            </div>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section px-8 py-10 animate__animated animate__fadeIn">
        
        <div class="grid grid-cols-1 lg:grid-cols-4 gap-6 mb-10">
            <div class="lg:col-span-1 glass p-8 rounded-[32px] gold-glow relative overflow-hidden">
                <p class="text-[10px] font-black text-[#f3ba2f] uppercase tracking-widest mb-4">Master Balance</p>
                <h2 id="balance-val" class="text-4xl font-black tracking-tighter mb-8">$15,400.00</h2>
                <div class="flex gap-3">
                    <button onclick="openModal('Deposit')" class="flex-1 bg-[#f3ba2f] text-black py-3 rounded-xl font-black text-[10px]">DEPOSIT</button>
                    <button onclick="openModal('Withdraw')" class="flex-1 bg-white/5 hover:bg-white/10 py-3 rounded-xl font-black text-[10px]">WITHDRAW</button>
                </div>
            </div>

            <div class="glass p-8 rounded-[32px] flex flex-col justify-center bg-gradient-to-br from-green-500/5 to-transparent">
                <p class="text-xs text-gray-500 font-bold mb-1">Staking Rewards</p>
                <h3 class="text-3xl font-black text-green-500">+$142.10</h3>
                <p class="text-[10px] text-gray-600 mt-2 italic">Earned from ETH Liquidity Pool</p>
            </div>
            <div class="glass p-8 rounded-[32px] flex flex-col justify-center bg-gradient-to-br from-blue-500/5 to-transparent">
                <p class="text-xs text-gray-500 font-bold mb-1">Affiliate Rank</p>
                <h3 class="text-3xl font-black text-blue-500 uppercase">Diamond</h3>
                <p class="text-[10px] text-gray-600 mt-2 italic">Next Reward: $500.00 (72%)</p>
            </div>
            <div class="glass p-8 rounded-[32px] flex flex-col justify-center">
                <p class="text-xs text-gray-500 font-bold mb-1">Live Trading View</p>
                <div class="w-full bg-gray-900 h-10 rounded-lg flex items-center justify-center border border-white/5">
                    <span class="text-[10px] font-mono animate-pulse text-yellow-500">Connecting to AWS-Central...</span>
                </div>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <div class="lg:col-span-2 glass rounded-[32px] overflow-hidden">
                <div class="p-6 border-b border-gray-800 flex justify-between items-center bg-white/5">
                    <h4 class="font-black text-xs uppercase tracking-widest">Advanced Spot Terminal</h4>
                    <div class="flex gap-4">
                        <span class="text-[10px] text-green-500 font-bold">API STABLE</span>
                        <span class="text-[10px] text-gray-500 font-mono">NODE: TYO-21</span>
                    </div>
                </div>
                <div class="p-10 h-64 relative bg-[#0d1014] flex flex-col justify-end">
                    <div class="flex items-end gap-2 h-full items-end pb-4">
                        <div class="bg-red-500/50 w-full rounded-t" style="height: 40%"></div>
                        <div class="bg-green-500/50 w-full rounded-t" style="height: 60%"></div>
                        <div class="bg-green-500/50 w-full rounded-t" style="height: 85%"></div>
                        <div class="bg-red-500/50 w-full rounded-t" style="height: 30%"></div>
                        <div class="bg-green-500/50 w-full rounded-t" style="height: 55%"></div>
                        <div class="bg-green-500/50 w-full rounded-t" style="height: 95%"></div>
                    </div>
                    <div class="absolute top-10 left-10"><h5 class="text-3xl font-black text-white/10 uppercase italic">BTC / USD CHART</h5></div>
                </div>
                <div class="p-6">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div class="crypto-card p-4 border border-white/5 flex justify-between items-center">
                            <div><p class="text-[10px] font-bold text-gray-500">BTC</p><p class="font-black">Bitcoin</p></div>
                            <div class="text-right font-mono text-green-500 font-bold"><p>$67,230</p><p class="text-[10px]">+2.1%</p></div>
                        </div>
                        <div class="crypto-card p-4 border border-white/5 flex justify-between items-center">
                            <div><p class="text-[10px] font-bold text-gray-500">ETH</p><p class="font-black">Ethereum</p></div>
                            <div class="text-right font-mono text-red-500 font-bold"><p>$3,420</p><p class="text-[10px]">-0.4%</p></div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="space-y-6">
                <div class="glass p-6 rounded-[32px] border-l-4 border-[#f3ba2f]">
                    <h4 class="font-black text-xs uppercase mb-4">P2P Express Buy</h4>
                    <input type="number" placeholder="Enter Amount USD" class="w-full bg-white/5 p-3 rounded-xl border border-white/10 text-sm mb-4 outline-none focus:border-[#f3ba2f]">
                    <div class="flex gap-2">
                        <button class="flex-1 bg-white/5 py-2 rounded-lg text-[10px] font-black border border-white/10">USDT</button>
                        <button class="flex-1 bg-white/5 py-2 rounded-lg text-[10px] font-black border border-white/10">BTC</button>
                    </div>
                    <button class="w-full mt-4 gold-btn text-black font-black py-3 rounded-xl text-xs">FIND OFFERS</button>
                </div>

                <div class="glass p-6 rounded-[32px]">
                    <h4 class="font-black text-xs uppercase mb-4 text-gray-400 tracking-widest">Security Protocol</h4>
                    <div class="space-y-4">
                        <div class="flex justify-between items-center"><span class="text-[10px] text-gray-500">2FA Status</span><span class="text-[10px] font-black text-green-500 uppercase">Active</span></div>
                        <div class="flex justify-between items-center"><span class="text-[10px] text-gray-500">Cold Storage</span><span class="text-[10px] font-black text-[#f3ba2f] uppercase">Enabled</span></div>
                        <div class="flex justify-between items-center"><span class="text-[10px] text-gray-500">Audit Source</span><span class="text-[10px] font-black uppercase">CertiK 2026</span></div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <div id="trans-modal" class="fixed inset-0 z-[200] bg-black/95 backdrop-blur-xl hidden flex items-center justify-center p-6">
        <div class="glass w-full max-w-sm rounded-[40px] p-10 animate__animated animate__fadeInUp">
            <h3 id="modal-title" class="text-3xl font-black italic mb-8 uppercase tracking-tighter">EXECUTE</h3>
            <div class="space-y-6">
                <input id="trans-amt" type="number" placeholder="0.00 USD" class="w-full bg-transparent border-b-2 border-gray-800 text-4xl font-black text-center outline-none focus:border-[#f3ba2f] pb-4">
                <select class="w-full bg-white/5 p-4 rounded-xl border border-white/10 text-xs font-bold outline-none">
                    <option>USDT (Global Network)</option>
                    <option>Bitcoin Wallet</option>
                    <option>Swift Bank Wire</option>
                    <option>Nexus Card Balance</option>
                </select>
                <button onclick="confirmTrans()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-2xl shadow-xl shadow-yellow-500/20">CONFIRM EXECUTION</button>
                <button onclick="closeModal()" class="w-full text-xs font-bold text-gray-600 tracking-widest uppercase">Abort</button>
            </div>
        </div>
    </div>

    <script>
        let balance = 15400.00;
        let mode = '';

        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0,0);
        }

        function handleAuth() {
            const name = document.getElementById('in-name').value || "Elite Member";
            document.getElementById('auth-box').classList.add('hidden');
            document.getElementById('user-box').classList.remove('hidden');
            document.getElementById('bal-top').innerText = '$' + balance.toLocaleString();
            showSection('dashboard');
            startGlobalTicker();
        }

        function openModal(m) { mode = m; document.getElementById('modal-title').innerText = m; document.getElementById('trans-modal').classList.remove('hidden'); }
        function closeModal() { document.getElementById('trans-modal').classList.add('hidden'); }

        function confirmTrans() {
            const val = parseFloat(document.getElementById('trans-amt').value);
            if(!val) return;
            balance = mode === 'Deposit' ? balance + val : balance - val;
            updateUI();
            closeModal();
            alert(`Network Success: ${mode} of $${val} confirmed by global validator nodes.`);
        }

        function updateUI() {
            document.getElementById('balance-val').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
            document.getElementById('bal-top').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
        }

        function startGlobalTicker() {
            setInterval(() => {
                let p = (Math.random() * 0.02);
                balance += p;
                updateUI();
            }, 5000);
        }

        // Ticker Scroll CSS Injection
        const style = document.createElement('style');
        style.textContent = `@keyframes scroll { 0% { transform: translateX(0); } 100% { transform: translateX(-50%); } }`;
        document.head.append(style);
    </script>
</body>
</html>
