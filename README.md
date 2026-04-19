<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nexus Capital | Elite Global Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --dark: #05070a; --glass: rgba(15, 18, 23, 0.9); }
        body { background-color: var(--dark); color: #ffffff; font-family: 'Inter', sans-serif; }
        .glass-ui { background: var(--glass); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.08); }
        .gold-glow { border: 1px solid var(--gold) !important; box-shadow: 0 0 15px rgba(243, 186, 47, 0.1); }
        .hidden-section { display: none; }
        .gradient-text { background: linear-gradient(90deg, #f3ba2f, #ffffff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        input, select { background: #161a1e !important; border: 1px solid #2b3139 !important; color: white !important; outline: none !important; }
        input:focus { border-color: var(--gold) !important; }
    </style>
</head>
<body class="overflow-x-hidden">

    <nav class="glass-ui sticky top-0 z-[100] px-8 py-4 flex items-center justify-between">
        <div class="flex items-center gap-2 cursor-pointer" onclick="location.reload()">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="text-[#f3ba2f]">Capital</span></span>
        </div>
        <div id="auth-buttons" class="flex gap-6 items-center">
            <button onclick="showSection('signup')" class="bg-[#f3ba2f] text-black px-8 py-2 rounded-full font-black text-xs hover:scale-105 transition">GET STARTED</button>
        </div>
        <div id="user-nav" class="hidden flex items-center gap-4">
            <div class="text-right"><p id="user-display" class="text-sm font-bold text-[#f3ba2f]"></p><p class="text-[9px] text-green-500 font-bold uppercase">Pro Trader</p></div>
            <div class="w-10 h-10 rounded-full bg-gradient-to-tr from-yellow-500 to-black p-[1px]"><div class="w-full h-full bg-black rounded-full flex items-center justify-center">👤</div></div>
        </div>
    </nav>

    <section id="landing-section" class="section py-32 px-6 text-center animate__animated animate__fadeIn">
        <h1 class="text-6xl md:text-8xl font-black mb-8 italic uppercase leading-none">Global <span class="gradient-text">Dollar</span><br>Settlement.</h1>
        <p class="text-gray-500 max-w-2xl mx-auto mb-10 text-lg uppercase tracking-widest font-bold">The institutional standard for 2026</p>
        <button onclick="showSection('signup')" class="bg-[#f3ba2f] text-black px-12 py-5 rounded-2xl font-black text-xl shadow-2xl">OPEN SECURE ACCOUNT</button>
    </section>

    <section id="signup-section" class="section hidden-section flex justify-center py-20 px-6 animate__animated animate__zoomIn">
        <div class="glass-ui p-10 rounded-[40px] w-full max-w-md border border-gray-800">
            <h2 class="text-3xl font-black mb-6 italic">JOIN THE ELITE</h2>
            <div class="space-y-4">
                <input id="in-name" type="text" placeholder="Full Name" class="w-full p-4 rounded-2xl">
                <input type="email" placeholder="Email Address" class="w-full p-4 rounded-2xl">
                <input type="password" placeholder="Create Password" class="w-full p-4 rounded-2xl">
                <button onclick="handleAuth()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-2xl shadow-lg">INITIALIZE ACCOUNT</button>
            </div>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10 animate__animated animate__fadeIn">
        
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-10">
            <div class="glass-ui p-8 rounded-[40px] gold-glow relative overflow-hidden">
                <p class="text-xs font-bold text-gray-500 uppercase tracking-widest mb-2">Total Managed Balance</p>
                <h2 id="balance-val" class="text-5xl font-black italic tracking-tighter">$15,400.00</h2>
                <div class="flex gap-4 mt-8">
                    <button onclick="openModal('deposit')" class="flex-1 bg-green-500 text-black py-3 rounded-xl font-bold text-xs uppercase">Deposit</button>
                    <button onclick="openModal('withdraw')" class="flex-1 bg-white/5 border border-white/10 py-3 rounded-xl font-bold text-xs uppercase hover:bg-white/10 transition">Withdraw</button>
                </div>
            </div>
            
            <div class="glass-ui p-8 rounded-[40px] flex flex-col justify-center border-l-4 border-blue-500">
                <p class="text-[10px] font-bold text-gray-500 uppercase mb-2 italic">Profit Forecast (24h)</p>
                <h3 class="text-3xl font-black text-blue-500">+$214.50</h3>
                <div class="mt-4 bg-white/5 h-2 rounded-full overflow-hidden"><div class="bg-blue-500 h-full" style="width: 65%"></div></div>
            </div>

            <div class="glass-ui p-8 rounded-[40px] flex flex-col justify-center border-l-4 border-[#f3ba2f]">
                <p class="text-[10px] font-bold text-gray-500 uppercase mb-2 italic">Account Tier</p>
                <h3 class="text-3xl font-black text-[#f3ba2f] uppercase italic">Diamond Pro</h3>
                <p class="text-[10px] text-gray-600 mt-2">Maximum withdrawal limit active</p>
            </div>
        </div>

        <div class="glass-ui rounded-[40px] overflow-hidden animate__animated animate__fadeInUp">
            <div class="p-8 border-b border-white/5 flex justify-between items-center">
                <h3 class="font-black italic uppercase text-sm tracking-widest text-gray-400">Ledger / Recent Transactions</h3>
                <span class="text-[10px] bg-green-500/20 text-green-500 px-3 py-1 rounded-full font-bold">SYSTEM ACTIVE</span>
            </div>
            <div class="overflow-x-auto">
                <table class="w-full text-left text-sm">
                    <thead class="bg-white/5 text-[10px] font-bold text-gray-500 uppercase">
                        <tr><th class="p-6">Type</th><th class="p-6">Method</th><th class="p-6">Amount</th><th class="p-6">TID / Proof</th><th class="p-6">Status</th></tr>
                    </thead>
                    <tbody id="ledger-body" class="divide-y divide-white/5">
                        </tbody>
                </table>
            </div>
        </div>
    </section>

    <div id="deposit-modal" class="fixed inset-0 z-[200] bg-black/95 backdrop-blur-xl hidden flex items-center justify-center p-6">
        <div class="glass-ui w-full max-w-md rounded-[40px] p-10 animate__animated animate__fadeInDown">
            <div class="flex justify-between items-center mb-8">
                <h3 class="text-2xl font-black italic uppercase">Initialize Deposit</h3>
                <button onclick="closeModals()" class="text-gray-500 text-3xl">&times;</button>
            </div>
            <div class="space-y-6">
                <div><label class="text-[10px] font-bold text-gray-500 uppercase">Select Gateway</label>
                    <select id="dep-method" class="w-full p-4 rounded-2xl mt-2 text-sm">
                        <option value="USDT (TRC20)">USDT (TRC20 Wallet)</option>
                        <option value="Bitcoin">Bitcoin (BTC)</option>
                        <option value="Binance Pay">Binance Pay (ID)</option>
                        <option value="Bank Transfer">International Bank Wire</option>
                    </select>
                </div>
                <div><label class="text-[10px] font-bold text-gray-500 uppercase">Amount (USD)</label>
                    <input id="dep-amount" type="number" placeholder="Min $50.00" class="w-full p-4 rounded-2xl mt-2 text-xl font-black">
                </div>
                <div><label class="text-[10px] font-bold text-gray-500 uppercase">Transaction ID (TID)</label>
                    <input id="dep-tid" type="text" placeholder="Paste TID here" class="w-full p-4 rounded-2xl mt-2 text-xs">
                </div>
                <div><label class="text-[10px] font-bold text-gray-500 uppercase">Upload Proof (Screenshot)</label>
                    <input type="file" id="dep-proof" accept="image/*" class="w-full p-3 rounded-2xl mt-2 text-[10px] bg-white/5">
                </div>
                <button onclick="submitDeposit()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-2xl shadow-xl">SUBMIT PROOF</button>
            </div>
        </div>
    </div>

    <div id="withdraw-modal" class="fixed inset-0 z-[200] bg-black/95 backdrop-blur-xl hidden flex items-center justify-center p-6">
        <div class="glass-ui w-full max-w-md rounded-[40px] p-10 animate__animated animate__fadeInUp">
            <div class="flex justify-between items-center mb-8">
                <h3 class="text-2xl font-black italic uppercase">Request Payout</h3>
                <button onclick="closeModals()" class="text-gray-500 text-3xl">&times;</button>
            </div>
            <div class="space-y-5">
                <select id="wit-method" class="w-full p-4 rounded-2xl text-sm">
                    <option value="Crypto Wallet">Crypto Wallet (USDT/BTC)</option>
                    <option value="Local Bank">Local Bank Account</option>
                </select>
                <input id="wit-name" type="text" placeholder="Account Holder Name" class="w-full p-4 rounded-2xl text-sm">
                <input id="wit-number" type="text" placeholder="Account Number / Wallet Address" class="w-full p-4 rounded-2xl text-sm">
                <input id="wit-amount" type="number" placeholder="Withdrawal Amount" class="w-full p-4 rounded-2xl text-xl font-black">
                <button onclick="submitWithdraw()" class="w-full bg-white text-black font-black py-4 rounded-2xl shadow-xl">INITIATE PAYOUT</button>
            </div>
        </div>
    </div>

    <script>
        let balance = 15400.00;
        let proofBase64 = "";

        // File to Base64 Converter
        document.getElementById('dep-proof').addEventListener('change', function(e) {
            const file = e.target.files[0];
            const reader = new FileReader();
            reader.onloadend = () => { proofBase64 = reader.result; };
            reader.readAsDataURL(file);
        });

        function showSection(id) {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById(id + '-section').classList.remove('hidden-section');
            window.scrollTo(0,0);
        }

        function handleAuth() {
            const name = document.getElementById('in-name').value || "Elite User";
            document.getElementById('auth-buttons').classList.add('hidden');
            document.getElementById('user-nav').classList.remove('hidden');
            document.getElementById('user-display').innerText = name;
            showSection('dashboard');
            addLedgerRow('Welcome Bonus', 'System', 100.00, 'N/A', 'Completed', 'text-green-500');
        }

        function openModal(type) {
            document.getElementById(type + '-modal').classList.remove('hidden');
        }

        function closeModals() {
            document.getElementById('deposit-modal').classList.add('hidden');
            document.getElementById('withdraw-modal').classList.add('hidden');
        }

        function submitDeposit() {
            const amt = document.getElementById('dep-amount').value;
            const tid = document.getElementById('dep-tid').value;
            const method = document.getElementById('dep-method').value;
            
            if(!amt || !tid || !proofBase64) return alert("Please fill all fields and upload proof, sweetie!");

            addLedgerRow('Deposit', method, amt, tid, 'Pending Audit', 'text-yellow-500');
            closeModals();
            alert("Deposit submitted! Our team will verify the Base64 proof and TID within 24h.");
        }

        function submitWithdraw() {
            const amt = parseFloat(document.getElementById('wit-amount').value);
            const name = document.getElementById('wit-name').value;
            const acc = document.getElementById('wit-number').value;
            const method = document.getElementById('wit-method').value;

            if(!amt || !name || !acc) return alert("All fields are required for withdrawal!");
            if(amt > balance) return alert("Insufficient balance!");

            balance -= amt;
            document.getElementById('balance-val').innerText = '$' + balance.toLocaleString(undefined, {minimumFractionDigits: 2});
            
            addLedgerRow('Withdraw', method, amt, acc.substring(0,6)+'...', 'Processing', 'text-blue-500');
            closeModals();
            alert("Withdrawal request sent successfully, sweetie!");
        }

        function addLedgerRow(type, method, amt, tid, status, colorClass) {
            const tbody = document.getElementById('ledger-body');
            const row = `
                <tr class="hover:bg-white/5 transition">
                    <td class="p-6 font-bold uppercase text-[10px]">${type}</td>
                    <td class="p-6 text-gray-400 text-xs">${method}</td>
                    <td class="p-6 font-black ${type==='Deposit' || type==='Welcome Bonus' ? 'text-green-500' : 'text-red-500'}">$${parseFloat(amt).toLocaleString()}</td>
                    <td class="p-6 font-mono text-[9px] text-gray-500">${tid}</td>
                    <td class="p-6"><span class="px-3 py-1 rounded-full bg-white/5 font-bold text-[9px] ${colorClass}">${status}</span></td>
                </tr>
            `;
            tbody.innerHTML = row + tbody.innerHTML;
        }
    </script>
</body>
</html>
