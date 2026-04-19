<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NEXUS CORE | Institutional Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css" rel="stylesheet">
    <style>
        :root { --gold: #f3ba2f; --bg: #010204; }
        body { background-color: var(--bg); color: #ffffff; font-family: 'Inter', sans-serif; }
        .glass { background: rgba(15, 18, 23, 0.9); backdrop-filter: blur(20px); border: 1px solid rgba(255,255,255,0.06); }
        .crypto-text { background: linear-gradient(90deg, #f3ba2f, #ffffff); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .hidden-section { display: none; }
        .node-card { border: 1px solid rgba(255,255,255,0.03); transition: 0.3s; }
        .node-card:hover { border-color: var(--gold); transform: translateY(-5px); }
        .ping { height: 6px; width: 6px; border-radius: 50%; background: #10b981; display: inline-block; animation: pulse 2s infinite; }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: 0.3; } }
    </style>
</head>
<body>

    <nav class="glass sticky top-0 z-[100] px-6 py-4 flex items-center justify-between border-b border-white/5">
        <div class="flex items-center gap-3 cursor-pointer" id="master-logo">
            <div class="w-10 h-10 bg-[#f3ba2f] rounded-xl flex items-center justify-center font-black text-black text-xl shadow-lg">N</div>
            <span class="text-xl font-black italic tracking-tighter uppercase">Nexus<span class="crypto-text">Core</span></span>
        </div>
        
        <div id="user-tag" class="hidden text-right">
            <p id="user-name-display" class="text-[10px] font-black text-[#f3ba2f] uppercase"></p>
            <p class="text-[7px] text-green-500 font-bold tracking-[0.2em]">NODE: ACTIVE</p>
        </div>
    </nav>

    <section id="admin-section" class="section hidden-section p-10 animate__animated animate__fadeIn">
        <div class="max-w-4xl mx-auto glass p-10 rounded-[40px] border-2 border-red-500/20">
            <h2 class="text-4xl font-black text-red-500 mb-8 italic uppercase">Control Terminal</h2>
            <div id="admin-users-list" class="space-y-4">
                <p class="text-gray-500 italic">Fetching global node data...</p>
            </div>
            <button onclick="location.reload()" class="mt-10 text-xs font-bold text-gray-500 uppercase tracking-widest hover:text-white">Exit Admin</button>
        </div>
    </section>

    <section id="auth-section" class="section flex justify-center py-24 px-6">
        <div class="glass p-10 rounded-[40px] w-full max-w-md border border-white/5">
            <h2 class="text-2xl font-black mb-8 italic uppercase tracking-tighter">Initialize Session</h2>
            <input id="reg-email" type="email" placeholder="Institutional Email" class="w-full p-4 mb-4 bg-black/50 border border-white/10 rounded-xl text-xs">
            <button onclick="loginUser()" class="w-full bg-[#f3ba2f] text-black font-black py-4 rounded-xl shadow-xl uppercase text-[10px] tracking-widest">Connect Network</button>
        </div>
    </section>

    <section id="dashboard-section" class="section hidden-section container mx-auto px-6 py-10">
        <div class="glass p-10 rounded-[45px] border-l-[12px] border-[#f3ba2f] mb-12">
            <p class="text-[10px] font-black text-gray-500 uppercase tracking-widest mb-4">Total Assets (USD)</p>
            <h2 id="balance-display" class="text-6xl md:text-8xl font-black italic tracking-tighter">$0.00</h2>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="node-container"></div>
    </section>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, set, get, update, onValue } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        const firebaseConfig = {
            apiKey: "AIzaSyBEqvT7AYCTZg1Bb6zEDtJn71QrYopX73M",
            authDomain: "coin-07.firebaseapp.com",
            databaseURL: "https://coin-07-default-rtdb.firebaseio.com",
            projectId: "coin-07",
            storageBucket: "coin-07.firebasestorage.app",
            messagingSenderId: "341970060013",
            appId: "1:341970060013:web:67374c0fd262b63bd342e4"
        };

        const app = initializeApp(firebaseConfig);
        const db = getDatabase(app);

        // --- SECRET KEY LOGIC ---
        let logoTaps = 0;
        document.getElementById('master-logo').addEventListener('click', () => {
            logoTaps++;
            if(logoTaps === 4) {
                const secret = prompt("Enter Administration Key:");
                if(secret === "coin786") {
                    showAdminPanel();
                } else {
                    alert("Unauthorized Access Attempt!");
                }
                logoTaps = 0;
            }
            setTimeout(() => { logoTaps = 0; }, 3000); // Reset taps after 3s
        });

        // --- AUTH & DATABASE ---
        window.loginUser = async () => {
            const email = document.getElementById('reg-email').value;
            if(!email) return alert("Email required, sweetie!");
            const userId = email.replace(/[.#$[\]]/g, "_");
            
            const userRef = ref(db, 'users/' + userId);
            const snap = await get(userRef);
            
            if(!snap.exists()) {
                await set(userRef, { email: email, balance: 0, history: [] });
            }
            
            localStorage.setItem('nexus_uid', userId);
            location.reload();
        };

        // --- SHOW ADMIN ---
        async function showAdminPanel() {
            document.querySelectorAll('.section').forEach(s => s.classList.add('hidden-section'));
            document.getElementById('admin-section').classList.remove('hidden-section');
            
            const usersRef = ref(db, 'users');
            onValue(usersRef, (snapshot) => {
                const data = snapshot.val();
                let html = "";
                for(let id in data) {
                    html += `
                        <div class="glass p-4 rounded-2xl flex justify-between items-center border border-white/5">
                            <div><p class="text-[10px] font-bold text-gray-400">${data[id].email}</p><p class="text-xl font-black italic">$${data[id].balance}</p></div>
                            <button onclick="updateUserBalance('${id}')" class="bg-[#f3ba2f] text-black px-4 py-2 rounded-lg text-[10px] font-black uppercase">Edit</button>
                        </div>`;
                }
                document.getElementById('admin-users-list').innerHTML = html;
            });
        }

        // Global functions for buttons
        window.updateUserBalance = (id) => {
            const newBal = prompt("Enter New Balance for " + id);
            if(newBal !== null) {
                update(ref(db, 'users/' + id), { balance: parseFloat(newBal) });
            }
        };

        // On Load Check
        const savedId = localStorage.getItem('nexus_uid');
        if(savedId) {
            document.getElementById('auth-section').classList.add('hidden-section');
            document.getElementById('dashboard-section').classList.remove('hidden-section');
            document.getElementById('user-tag').classList.remove('hidden');
            
            onValue(ref(db, 'users/' + savedId), (snap) => {
                if(snap.exists()) {
                    document.getElementById('balance-display').innerText = '$' + snap.val().balance.toLocaleString();
                    document.getElementById('user-name-display').innerText = snap.val().email.split('@')[0];
                }
            });
        }
    </script>
</body>
</html>
