<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS INFINITY | Master Hub</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;500;700;800&family=Syncopate:wght@700&display=swap');
        :root { --neon-pink: #ff00ff; --neon-blue: #00d4ff; --glass: rgba(255, 255, 255, 0.05); }
        body { background: #050505; color: #f8f9fa; font-family: 'Plus Jakarta Sans', sans-serif; margin: 0; }
        .glass-card { background: var(--glass); backdrop-filter: blur(25px); border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 30px; }
        .input-hub { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.1); border-radius: 20px; padding: 18px; color: white; width: 100%; outline: none; transition: 0.3s; }
        .input-hub:focus { border-color: var(--neon-pink); box-shadow: 0 0 15px rgba(255, 0, 255, 0.1); }
        .btn-neon { background: linear-gradient(135deg, #ff00ff, #ff003c); border-radius: 20px; padding: 18px; font-weight: 800; text-transform: uppercase; letter-spacing: 1px; transition: 0.3s; width: 100%; }
        .btn-neon:hover { transform: scale(1.02); filter: brightness(1.2); }
        .nav-item { color: #555; transition: 0.3s; cursor: pointer; text-align: center; font-size: 9px; font-weight: 800; }
        .nav-active { color: var(--neon-pink); text-shadow: 0 0 10px var(--neon-pink); }
        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div id="dashboard" class="pb-32">
        <header class="p-6 flex justify-between items-center sticky top-0 bg-[#050505]/80 backdrop-blur-xl z-50 border-b border-white/5">
            <div class="flex items-center gap-3">
                <div id="admin-trigger" class="w-10 h-10 bg-white/5 rounded-xl flex items-center justify-center font-black border border-white/10 italic">N</div>
                <div><p id="nav-user" class="text-xs font-black uppercase text-pink-500 leading-none">...</p><p class="text-[7px] text-green-500 font-black uppercase tracking-widest mt-1">● Secure Connection</p></div>
            </div>
            <button onclick="logout()" class="text-zinc-600"><i class="fa-solid fa-power-off text-xl"></i></button>
        </header>

        <main id="page-vault" class="p-6 space-y-8">
            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xl font-black italic text-pink-500 uppercase tracking-tighter">Capital Injection</h3>
                
                <div class="grid gap-3">
                    <div class="bg-white/5 p-4 rounded-2xl border border-white/5">
                        <div class="flex justify-between items-center mb-1"><span class="text-[8px] font-black text-zinc-500 uppercase">Binance (USDT-TRC20)</span><i class="fa-brands fa-bitcoin text-yellow-500"></i></div>
                        <p class="text-[10px] font-bold select-all break-all text-pink-400">TAvfQQ18hXHdVCHbExV4yUPvQ4XkNgfKsJ</p>
                    </div>
                    <div class="bg-white/5 p-4 rounded-2xl border border-white/5">
                        <div class="flex justify-between items-center mb-1"><span class="text-[8px] font-black text-zinc-500 uppercase">Trust Wallet (BNB-BEP20)</span><i class="fa-solid fa-shield-halved text-blue-500"></i></div>
                        <p class="text-[10px] font-bold select-all break-all text-blue-400">0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</p>
                    </div>
                    <div class="bg-white/5 p-4 rounded-2xl border border-white/5">
                        <div class="flex justify-between items-center mb-1"><span class="text-[8px] font-black text-zinc-500 uppercase">MetaMask (ETH-ERC20)</span><i class="fa-solid fa-fox text-orange-500"></i></div>
                        <p class="text-[10px] font-bold select-all break-all text-orange-400">0xD9359EADE5F5bACA51fb7da043767Bc0685bC355</p>
                    </div>
                </div>

                <div class="space-y-4 pt-4 border-t border-white/5">
                    <select id="dep-method" class="input-hub bg-zinc-950">
                        <option value="Binance (USDT)">Binance Pay</option>
                        <option value="Trust Wallet (BNB)">Trust Wallet</option>
                        <option value="MetaMask (ETH)">MetaMask</option>
                    </select>
                    <input type="number" id="dep-amt" placeholder="Amount to Inject ($)" class="input-hub">
                    <input type="text" id="dep-tid" placeholder="Transaction Hash / TID" class="input-hub">
                    <div class="relative">
                        <p class="text-[8px] font-black text-zinc-500 uppercase mb-2 ml-2">Upload Transfer Signature</p>
                        <input type="file" id="dep-proof" accept="image/*" class="text-[10px] block w-full file:mr-4 file:py-2 file:px-4 file:rounded-full file:bg-pink-500/10 file:text-pink-500 file:border-0">
                    </div>
                    <img id="preview-img" class="mt-4 w-full h-40 rounded-2xl border border-white/10 object-cover hidden">
                    <button onclick="submitDeposit()" class="btn-neon">Initialize Protocol</button>
                </div>
            </div>

            <div class="glass-card p-8 space-y-6">
                <h3 class="text-xl font-black italic uppercase tracking-tighter">Capital Payout</h3>
                <div class="space-y-4">
                    <select id="w-method" class="input-hub bg-zinc-950">
                        <option value="Binance Pay">Binance Pay ID</option>
                        <option value="Trust Wallet">Trust Wallet (Multi-Coin)</option>
                        <option value="MetaMask">MetaMask Wallet</option>
                        <option value="OKX">OKX Terminal</option>
                        <option value="Coinbase">Coinbase Pro</option>
                    </select>
                    <input type="text" id="w-addr" placeholder="Destination Address / ID" class="input-hub">
                    <input type="number" id="w-amt" placeholder="Payout Amount ($)" class="input-hub">
                    <p class="text-[8px] text-zinc-500 font-bold uppercase text-center italic">Service Fee: 0% Institutional Coverage</p>
                    <button onclick="submitWith()" class="btn-neon !bg-zinc-800">Queue Distribution</button>
                </div>
            </div>
        </main>

        <nav class="fixed bottom-0 left-0 right-0 p-6 bg-black/60 backdrop-blur-2xl border-t border-white/5 flex justify-around items-center z-[100]">
            <div class="nav-item"><i class="fa-solid fa-house-signal text-xl"></i><p>CORE</p></div>
            <div class="nav-item nav-active"><i class="fa-solid fa-vault text-xl"></i><p>VAULT</p></div>
            <div class="nav-item"><i class="fa-solid fa-list-ul text-xl"></i><p>LOGS</p></div>
        </nav>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, push } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = { apiKey: "AIzaSyDaOGSlBjS7_pQX9ELAytXVF4jvWK_lzB0", authDomain: "live-54fb4.firebaseapp.com", databaseURL: "https://live-54fb4-default-rtdb.firebaseio.com", projectId: "live-54fb4", storageBucket: "live-54fb4.firebasestorage.app", messagingSenderId: "781910562842", appId: "1:781910562842:web:07a887f860d30fd17d99a3" };
        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // Base64 Implementation for Modern Image Handling
        document.getElementById('dep-proof').onchange = (e) => {
            const reader = new FileReader();
            reader.readAsDataURL(e.target.files[0]);
            reader.onload = () => {
                document.getElementById('preview-img').src = reader.result;
                document.getElementById('preview-img').classList.remove('hidden');
            };
        };

        window.submitDeposit = async () => {
            const user = localStorage.getItem('nexus_user') || 'DemoUser';
            const amt = document.getElementById('dep-amt').value;
            const tid = document.getElementById('dep-tid').value;
            const method = document.getElementById('dep-method').value;
            const proof = document.getElementById('preview-img').src;

            if(!amt || !tid || !proof) return alert("Security Check: Missing Protocol Data!");

            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, tid, method, proof, status: 'pending', date: new Date().toLocaleString(), type: 'Deposit', hKey: hRef.key };
            
            await set(hRef, entry);
            await set(ref(db, `admin/requests/${hRef.key}`), entry); // Admin Unlimited Power System
            alert("Capital Injection Logged. Waiting for Institutional Clearance.");
        };

        window.submitWith = async () => {
            const user = localStorage.getItem('nexus_user') || 'DemoUser';
            const addr = document.getElementById('w-addr').value;
            const amt = document.getElementById('w-amt').value;
            const method = document.getElementById('w-method').value;

            if(!amt || !addr) return alert("Details Required for Payout!");

            const hRef = push(ref(db, `users/${user}/history`));
            const entry = { user, amount: amt, address: addr, method, status: 'pending', date: new Date().toLocaleString(), type: 'Withdrawal', hKey: hRef.key };
            
            await set(hRef, entry);
            await set(ref(db, `admin/requests/${hRef.key}`), entry);
            alert("Payout Distribution Queued for Audit.");
        };
    </script>
</body>
</html>
