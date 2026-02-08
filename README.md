<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KHBOTAI - Premium Digital Store</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Plus Jakarta Sans', sans-serif;
            background-color: #0f0f0f;
            color: #ffffff;
            min-height: 100vh;
        }
        .selection-btn {
            border: 1px solid #333;
            background: #ffffff;
            color: #000000;
            transition: all 0.2s;
        }
        .selection-btn.active {
            border-color: #ff6b00;
            background: rgba(255, 107, 0, 0.1);
            color: #ffffff;
        }
        .product-card {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            background-color: #1a1a1a;
            border: 1px solid #2a2a2a;
        }
        .product-card:hover {
            transform: translateY(-8px);
            border-color: #ff6b00;
            box-shadow: 0 10px 30px -10px rgba(255, 107, 0, 0.2);
        }
        .view-hidden { display: none; }
        
        .section-divider {
            border-top: 1px solid #2a2a2a;
            margin: 3rem 0;
            position: relative;
        }
        .section-divider span {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: #0f0f0f;
            padding: 0 1.5rem;
            color: #ff6b00;
            letter-spacing: 0.1em;
            text-transform: uppercase;
        }
        .kh-gradient-text {
            background: linear-gradient(90deg, #ffffff, #ff6b00);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
    </style>
</head>
<body class="p-4 md:p-8">

    <!-- KHBOTAI Header Section -->
    <div class="max-w-6xl mx-auto">
        <header class="flex flex-col md:flex-row justify-between items-center mb-12 py-6 gap-6 border-b border-white/5">
            <div onclick="showStore()" class="cursor-pointer flex items-center gap-3">
                <div class="w-10 h-10 bg-gradient-to-tr from-orange-600 to-orange-400 rounded-xl flex items-center justify-center font-black text-black text-xl shadow-lg shadow-orange-600/20">K</div>
                <h1 class="text-3xl font-extrabold tracking-tighter">KHBOTAI<span class="text-orange-500">.DEV</span></h1>
            </div>
            <nav class="flex gap-8 text-sm font-medium text-gray-400">
                <a href="javascript:void(0)" onclick="showStore()" class="hover:text-orange-500 transition-colors">Products</a>
                <a href="#" class="hover:text-orange-500 transition-colors">Pricing</a>
                <a href="#" class="hover:text-orange-500 transition-colors">Support</a>
                <a href="#" class="bg-white/5 hover:bg-white/10 text-white px-4 py-2 rounded-lg transition">Login</a>
            </nav>
        </header>
    </div>

    <!-- STOREFRONT VIEW -->
    <div id="storeView" class="max-w-6xl mx-auto">
        <div class="section-divider">
            <span class="text-xs font-bold">Premium Marketplace</span>
        </div>
        
        <div class="text-center mb-12">
            <h2 class="text-5xl font-black mb-4 kh-gradient-text">Unlock Premium Access</h2>
            <p class="text-gray-500 text-lg max-w-2xl mx-auto">High-quality digital subscriptions and tools delivered instantly to your inbox.</p>
        </div>

        <div id="productGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
            <!-- Products will be injected here -->
        </div>
    </div>

    <!-- PRODUCT DETAIL VIEW -->
    <div id="detailView" class="max-w-6xl mx-auto view-hidden">
        <!-- Breadcrumbs -->
        <nav class="text-sm text-gray-500 mb-8 flex items-center gap-2">
            <a href="javascript:void(0)" onclick="showStore()" class="hover:text-orange-500">Home</a> 
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
            <a href="#" class="hover:text-orange-500" id="detailCategory">Category</a> 
            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
            <span class="text-gray-300" id="detailCrumbName">Product</span>
        </nav>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 mb-16">
            <!-- Left: Product Image -->
            <div id="detailImageContainer" class="relative group rounded-2xl aspect-square flex items-center justify-center p-12 overflow-hidden shadow-2xl shadow-black">
                <!-- SVG Icon injected here -->
            </div>

            <!-- Right: Product Info -->
            <div class="flex flex-col">
                <div class="mb-2">
                    <span class="bg-orange-500/10 text-orange-500 text-[10px] font-bold px-2 py-1 rounded uppercase tracking-wider">Verified Service</span>
                </div>
                <h1 class="text-5xl font-black mb-2 tracking-tight" id="detailName">Product Name</h1>
                <p class="text-orange-500 text-2xl font-bold mb-8" id="detailPriceRange">$0.00</p>

                <div class="flex gap-4 mb-10">
                    <a href="#" class="flex-1 bg-gradient-to-r from-orange-500 to-orange-600 hover:scale-[1.02] text-white font-bold py-4 px-4 rounded-xl text-center transition shadow-lg shadow-orange-600/20">
                        Purchase via Telegram
                    </a>
                    <a href="#" class="flex-1 bg-white/5 hover:bg-white/10 text-white font-bold py-4 px-4 rounded-xl text-center transition border border-white/10">
                        Buy on WhatsApp
                    </a>
                </div>

                <div class="space-y-8 p-6 bg-white/5 rounded-2xl border border-white/5">
                    <div>
                        <label class="block text-xs font-bold text-gray-400 uppercase tracking-widest mb-3">License Type</label>
                        <button class="selection-btn active px-6 py-2 text-sm rounded-lg font-bold ring-2 ring-orange-500 ring-offset-2 ring-offset-[#1a1a1a]">Private Account</button>
                    </div>

                    <div>
                        <label class="block text-xs font-bold text-gray-400 uppercase tracking-widest mb-3">Subscription Term</label>
                        <div class="flex flex-wrap gap-3" id="durationContainer">
                            <!-- Buttons injected here -->
                        </div>
                    </div>
                </div>

                <div class="mt-10 grid grid-cols-2 gap-4">
                    <div class="flex items-center gap-3 text-sm text-gray-300">
                        <div class="w-8 h-8 rounded-full bg-green-500/10 flex items-center justify-center text-green-500">✓</div>
                        Instant Delivery
                    </div>
                    <div class="flex items-center gap-3 text-sm text-gray-300">
                        <div class="w-8 h-8 rounded-full bg-blue-500/10 flex items-center justify-center text-blue-500">🛡</div>
                        Full Warranty
                    </div>
                </div>

                <p class="text-4xl font-black text-orange-500 mt-12" id="displayPrice">$0.00</p>
            </div>
        </div>

        <!-- Detailed Description -->
        <div class="bg-white/5 rounded-3xl p-10 border border-white/5 mb-20">
            <h2 class="text-2xl font-bold mb-8 flex items-center gap-3">
                <span class="w-2 h-8 bg-orange-500 rounded-full"></span>
                Description & Terms
            </h2>
            <div class="prose prose-invert max-w-none text-gray-400 space-y-6">
                <p class="text-xl font-medium text-white">Before purchasing, please note the following conditions for the best experience.</p>
                <ul class="grid md:grid-cols-2 gap-4 list-none p-0">
                    <li class="bg-black/20 p-4 rounded-xl border border-white/5 flex items-start gap-3">
                        <span class="text-orange-500 font-bold">01.</span>
                        <span>Official subscription activated on your own personal email address.</span>
                    </li>
                    <li class="bg-black/20 p-4 rounded-xl border border-white/5 flex items-start gap-3">
                        <span class="text-orange-500 font-bold">02.</span>
                        <span>24/7 Priority support via Telegram and WhatsApp for all customers.</span>
                    </li>
                </ul>
            </div>
        </div>
    </div>

    <script>
        const products = [
            {
                id: 1,
                name: "Coursera Plus",
                category: "Learning",
                range: "$2.50 — $20.00",
                color: "bg-[#0056D2]",
                icon: `<svg viewBox="0 0 24 24" class="w-32 h-32 fill-white" xmlns="http://www.w3.org/2000/svg"><path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0zm-1.25 17.5h-2.5v-11h2.5v11zm5 0h-2.5v-6h2.5v6zm0-7.5h-2.5v-3.5h2.5v3.5z"/></svg>`,
                durations: [
                    { label: "1 Month", price: 2.50 },
                    { label: "6 Months", price: 12.00 },
                    { label: "1 Year", price: 20.00 }
                ]
            },
            {
                id: 2,
                name: "Netflix UHD",
                category: "Streaming",
                range: "$3.00 — $35.00",
                color: "bg-[#E50914]",
                icon: `<svg viewBox="0 0 24 24" class="w-32 h-32 fill-white" xmlns="http://www.w3.org/2000/svg"><path d="M6.5 2v20c1-.5 2.5-1 3.5-1s2.5.5 3.5 1V2c-1 .5-2.5 1-3.5 1s-2.5-.5-3.5-1z"/><path d="M17 2v20c1-.5 2.5-1 3.5-1V2c-1 .5-2.5 1-3.5 1z"/><path d="M3.5 2v20c1-.5 2.5-1 3.5-1V2c-1 .5-2.5 1-3.5 1z" opacity=".5"/></svg>`,
                durations: [
                    { label: "1 Month", price: 3.00 },
                    { label: "3 Months", price: 8.50 },
                    { label: "1 Year", price: 35.00 }
                ]
            },
            {
                id: 3,
                name: "Spotify Premium",
                category: "Music",
                range: "$1.50 — $15.00",
                color: "bg-[#1DB954]",
                icon: `<svg viewBox="0 0 24 24" class="w-32 h-32 fill-white" xmlns="http://www.w3.org/2000/svg"><path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0zm5.51 17.3c-.22.36-.68.48-1.05.25-2.81-1.72-6.35-2.1-10.52-1.15-.41.09-.82-.16-.91-.57-.09-.41.16-.82.57-.91 4.57-1.04 8.49-.6 11.66 1.34.37.22.49.68.25 1.04zm1.48-3.26c-.28.45-.87.59-1.32.32-3.22-1.98-8.12-2.55-11.93-1.4-.5.15-1.03-.13-1.18-.63-.15-.5.13-1.03.63-1.18 4.35-1.32 9.77-.67 13.48 1.61.45.27.59.86.32 1.3zm.13-3.4c-3.86-2.29-10.24-2.51-13.97-1.38-.59.18-1.22-.16-1.4-.75-.18-.59.16-1.22.75-1.4 4.29-1.3 11.33-1.04 15.78 1.6.53.31.71 1 .4 1.53-.31.53-1 .71-1.56.4z"/></svg>`,
                durations: [
                    { label: "1 Month", price: 1.50 },
                    { label: "6 Months", price: 8.00 },
                    { label: "1 Year", price: 15.00 }
                ]
            }
        ];

        let currentProduct = null;

        function renderStore() {
            const grid = document.getElementById('productGrid');
            grid.innerHTML = products.map(p => `
                <div onclick="showDetails(${p.id})" class="product-card p-6 rounded-2xl cursor-pointer group">
                    <div class="${p.color} aspect-[4/3] rounded-xl flex items-center justify-center mb-6 overflow-hidden relative">
                        <div class="absolute inset-0 bg-black/20 group-hover:bg-transparent transition-colors"></div>
                        ${p.icon.replace('w-32 h-32', 'w-20 h-20 group-hover:scale-110 transition-transform duration-500')}
                    </div>
                    <div class="flex flex-col gap-1">
                        <div class="flex justify-between items-center">
                            <h3 class="text-lg font-bold text-white">${p.name}</h3>
                            <span class="text-[10px] bg-white/5 text-gray-400 px-2 py-0.5 rounded uppercase font-bold tracking-widest">${p.category}</span>
                        </div>
                        <div class="flex justify-between items-baseline mt-2">
                            <p class="text-orange-500 font-black text-xl">${p.range.split('—')[0].trim()}</p>
                            <button class="text-xs text-gray-500 group-hover:text-white transition-colors">Details →</button>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        function showDetails(id) {
            currentProduct = products.find(p => p.id === id);
            
            document.getElementById('storeView').classList.add('view-hidden');
            document.getElementById('detailView').classList.remove('view-hidden');
            
            document.getElementById('detailName').innerText = currentProduct.name;
            document.getElementById('detailCrumbName').innerText = currentProduct.name;
            document.getElementById('detailCategory').innerText = currentProduct.category;
            document.getElementById('detailPriceRange').innerText = currentProduct.range;
            document.getElementById('detailImageContainer').className = `relative group rounded-2xl aspect-square flex items-center justify-center p-12 ${currentProduct.color} shadow-2xl`;
            document.getElementById('detailImageContainer').innerHTML = currentProduct.icon;

            const container = document.getElementById('durationContainer');
            container.innerHTML = currentProduct.durations.map((d, i) => `
                <button onclick="setDuration('${d.label}', ${d.price})" 
                        class="duration-btn selection-btn ${i === 0 ? 'active ring-2 ring-orange-500 ring-offset-2 ring-offset-[#1a1a1a]' : 'bg-white text-black'} px-5 py-2.5 text-xs rounded-lg font-bold">
                    ${d.label}
                </button>
            `).join('');

            setDuration(currentProduct.durations[0].label, currentProduct.durations[0].price);
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function showStore() {
            document.getElementById('storeView').classList.remove('view-hidden');
            document.getElementById('detailView').classList.add('view-hidden');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function setDuration(label, price) {
            document.getElementById('displayPrice').innerText = '$' + price.toFixed(2);

            const buttons = document.querySelectorAll('.duration-btn');
            buttons.forEach(btn => {
                if (btn.innerText.trim() === label) {
                    btn.classList.add('active', 'ring-2', 'ring-orange-500', 'ring-offset-2', 'ring-offset-[#1a1a1a]');
                    btn.classList.remove('bg-white', 'text-black');
                } else {
                    btn.classList.remove('active', 'ring-2', 'ring-orange-500', 'ring-offset-2', 'ring-offset-[#1a1a1a]');
                    btn.classList.add('bg-white', 'text-black');
                }
            });
        }

        function resetSelection() {
            if (currentProduct) setDuration(currentProduct.durations[0].label, currentProduct.durations[0].price);
        }

        renderStore();
    </script>
</body>
</html>
