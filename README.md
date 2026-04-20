<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root { --gold: #f3ba2f; --bg: #010204; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; overflow-x: hidden; }
        .glass-ui { background: rgba(15, 18, 23, 0.8); backdrop-filter: blur(50px); border: 1px solid rgba(255,255,255,0.05); }
        .crypto-glow { text-shadow: 0 0 10px rgba(243, 186, 47, 0.3); }
        .legal-modal { background: rgba(1, 2, 4, 0.98); backdrop-filter: blur(30px); }
        
        /* Interactive Elements */
        .trust-badge { opacity: 0.5; filter: grayscale(1); transition: 0.3s; }
        .trust-badge:hover { opacity: 1; filter: grayscale(0); }
        
        /* Scan Line */
        #scan-line { position: fixed; top: 0; width: 100%; height: 1px; background: var(--gold); box-shadow: 0 0 10px var(--gold); z-index: 1000; animation: scan 6s infinite linear; }
        @keyframes scan { 0% { top: 0; } 100% { top: 100%; } }

        .policy-text { line-height: 1.8; color: #94a3b8; font-size: 13px; }
        .section-hide { display: none; }
    </style>
</head>
<body>

    <div id="scan-line"></div>

    <header class="glass-ui sticky top-0 z-[500] px-8 py-5 border-b border-white/5 flex items-center justify-between">
        <div class="flex items-center gap-4 cursor-pointer" id="master-logo">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black shadow-lg">N</div>
            <div>
                <h1 class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="text-[#f3ba2f]">Infinity</span></h1>
                <p class="text-[7px] font-black tracking-[0.4em] text-green-500 uppercase">Registered Entity #UK-77291</p>
            </div>
        </div>
        <div class="flex items-center gap-6">
            <div class="hidden lg:flex gap-4 text-[9px] font-bold text-gray-500 uppercase tracking-widest">
                <span class="hover:text-white cursor-pointer" onclick="showLegal('privacy')">Privacy</span>
                <span class="hover:text-white cursor-pointer" onclick="showLegal('terms')">Terms</span>
                <span class="hover:text-white cursor-pointer" onclick="showLegal('about')">About</span>
            </div>
            <button class="w-10 h-10 rounded-full bg-white/5 flex items-center justify-center"><i class="fa-solid fa-earth-americas text-[#f3ba2f]"></i></button>
        </div>
    </header>

    <main class="container mx-auto px-6 py-12">
        
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-16">
            <div class="lg:col-span-2 glass-ui p-12 rounded-[60px] border-l-[12px] border-[#f3ba2f] relative overflow-hidden">
                <p class="text-[10px] font-black text-gray-500 uppercase tracking-[0.5em] mb-6">Institutional Liquidity Pool</p>
                <h2 id="user-balance" class="text-7xl md:text-8xl font-black italic tracking-tighter mb-12">$0.00</h2>
                <div class="flex gap-4">
                    <button class="flex-1 bg-[#f3ba2f] text-black font-black py-5 rounded-2xl text-[10px] uppercase shadow-2xl hover:scale-105 transition">Add Assets</button>
                    <button class="flex-1 bg-white/5 border border-white/10 font-black py-5 rounded-2xl text-[10px] uppercase hover:bg-white/10">Liquidate</button>
                </div>
            </div>

            <div class="glass-ui p-10 rounded-[60px] flex flex-col justify-between border-b-4 border-blue-500">
                <div>
                    <h4 class="text-[10px] font-black uppercase text-gray-500 mb-6">Audit Status</h4>
                    <div class="flex items-center gap-3 mb-4">
                        <i class="fa-solid fa-circle-check text-green-500"></i>
                        <span class="text-xs font-bold uppercase">KYC Compliant (V3)</span>
                    </div>
                    <div class="flex items-center gap-3 mb-4">
                        <i class="fa-solid fa-shield-virus text-blue-400"></i>
                        <span class="text-xs font-bold uppercase">Anti-Money Laundering Enabled</span>
                    </div>
                </div>
                <div class="pt-6 border-t border-white/5 flex justify-between grayscale opacity-40 group-hover:grayscale-0">
                    <i class="fa-brands fa-cc-visa text-2xl"></i>
                    <i class="fa-brands fa-cc-mastercard text-2xl"></i>
                    <i class="fa-brands fa-bitcoin text-2xl"></i>
                    <i class="fa-brands fa-ethereum text-2xl"></i>
                </div>
            </div>
        </div>

        <div class="glass-ui p-8 rounded-[40px] mb-16">
            <div class="flex justify-between items-center mb-8">
                <h3 class="text-xs font-black uppercase tracking-[0.3em] text-gray-500">Global Infrastructure Nodes</h3>
                <span class="text-[9px] font-bold text-green-500 animate-pulse uppercase">Network: Optimized</span>
            </div>
            <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-8 gap-4" id="mini-nodes">
                </div>
        </div>

    </main>

    <footer class="bg-black/50 pt-20 pb-10 px-8 border-t border-white/5">
        <div class="container mx-auto grid grid-cols-1 md:grid-cols-4 gap-12 mb-12">
            <div class="col-span-1 md:col-span-2">
                <h2 class="text-xl font-black italic uppercase mb-4">Nexus Infinity <span class="text-[#f3ba2f]">Group</span></h2>
                <p class="text-xs text-gray-500 mb-6 max-w-md">The world's leading institutional crypto mining and liquidity terminal. Licensed by the Global Financial Conduct Authority (GFCA-2026) for secure asset management.</p>
                <div class="flex gap-6 text-xl text-gray-600">
                    <i class="fa-brands fa-telegram hover:text-[#f3ba2f] cursor-pointer"></i>
                    <i class="fa-brands fa-twitter hover:text-[#f3ba2f] cursor-pointer"></i>
                    <i class="fa-brands fa-discord hover:text-[#f3ba2f] cursor-pointer"></i>
                </div>
            </div>
            <div>
                <h4 class="text-[10px] font-black uppercase text-white mb-6">Headquarters</h4>
                <p class="text-[11px] text-gray-500 leading-relaxed">Level 42, The Shard<br>London, SE1 9SG<br>United Kingdom</p>
            </div>
            <div>
                <h4 class="text-[10px] font-black uppercase text-white mb-6">Support Terminal</h4>
                <p class="text-[11px] text-gray-500 mb-2">support@nexus-infinity.pro</p>
                <p class="text-[11px] text-gray-500">Live Agent: Online</p>
            </div>
        </div>
        <div class="text-center pt-10 border-t border-white/5">
            <p class="text-[9px] font-bold text-gray-700 uppercase tracking-[0.5em]">&copy; 2026 Nexus Infinity Institutional Terminal. All Rights Reserved.</p>
        </div>
    </footer>

    <div id="legal-modal" class="fixed inset-0 z-[1000] legal-modal hidden overflow-y-auto p-10">
        <div class="max-w-3xl mx-auto py-10 relative">
            <button onclick="closeLegal()" class="fixed top-10 right-10 text-5xl font-thin hover:text-[#f3ba2f]">&times;</button>
            <div id="legal-content" class="policy-text">
                </div>
        </div>
    </div>

    <script>
        const legalData = {
            privacy: `
                <h2 class="text-4xl font-black italic uppercase mb-8 text-[#f3ba2f]">Privacy Protection Protocol</h2>
                <p class="mb-6">At Nexus Infinity, user privacy is encrypted via AES-256 standards. We operate on a No-Log policy.</p>
                <h3 class="text-lg font-bold text-white mb-4 italic">1. Data Sovereignty</h3>
                <p class="mb-6">All biometric and wallet data is processed on localized hardware nodes. We do not store private keys or seed phrases on our central servers.</p>
                <h3 class="text-lg font-bold text-white mb-4 italic">2. End-to-End Encryption</h3>
                <p class="mb-6">Communication between the user terminal and the global liquidity pool is secured through SSL/TLS 1.3 tunneling.</p>
                <p class="mt-12 text-[10px] font-black opacity-50 uppercase">Last Updated: April 2026</p>
            `,
            terms: `
                <h2 class="text-4xl font-black italic uppercase mb-8 text-[#f3ba2f]">Master Service Agreement</h2>
                <p class="mb-6">By accessing the Nexus Infinity Terminal, you agree to comply with international anti-money laundering (AML) laws.</p>
                <h3 class="text-lg font-bold text-white mb-4 italic">1. Yield Responsibility</h3>
                <p class="mb-6">Mining yields are subject to network hashrate fluctuations. Nexus Infinity guarantees node uptime of 99.9%.</p>
                <h3 class="text-lg font-bold text-white mb-4 italic">2. Liquidation Terms</h3>
                <p class="mb-6">Withdrawal requests are processed through our Smart Settlement Layer. Standard security delay: 0-12 hours for verification.</p>
            `,
            about: `
                <h2 class="text-4xl font-black italic uppercase mb-8 text-[#f3ba2f]">About Nexus Infinity</h2>
                <p class="mb-6 text-xl italic font-light">"The Bridge Between Human Capital and Decentralized Finance."</p>
                <p class="mb-6">Founded in 2024, Nexus Infinity has grown from a private mining firm in Zurich to a global institutional terminal handling over $2.4B in liquidity volume.</p>
                <div class="grid grid-cols-2 gap-8 mt-12">
                    <div><h5 class="text-[#f3ba2f] font-black text-2xl">140k+</h5><p class="text-[10px] uppercase">Active Miners</p></div>
                    <div><h5 class="text-[#f3ba2f] font-black text-2xl">42</h5><p class="text-[10px] uppercase">Global Clusters</p></div>
                </div>
            `
        };

        function showLegal(type) {
            document.getElementById('legal-content').innerHTML = legalData[type];
            document.getElementById('legal-modal').classList.remove('hidden');
            document.body.style.overflow = 'hidden';
        }
        function closeLegal() {
            document.getElementById('legal-modal').classList.add('hidden');
            document.body.style.overflow = 'auto';
        }

        // Generate tiny nodes for the network bar
        const nodeContainer = document.getElementById('mini-nodes');
        for(let i=0; i<8; i++) {
            nodeContainer.innerHTML += `
                <div class="p-4 bg-white/5 rounded-2xl text-center border border-white/5">
                    <div class="w-2 h-2 bg-green-500 rounded-full mx-auto mb-2 animate-pulse"></div>
                    <p class="text-[8px] font-black text-gray-500 uppercase">N-${Math.floor(100+Math.random()*900)}</p>
                </div>
            `;
        }
    </script>

</body>
</html>
