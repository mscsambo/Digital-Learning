<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NexGen Digital Store</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #1a1a1a;
            color: #ffffff;
            min-height: 100vh;
        }
        .selection-btn {
            border: 1px solid #444;
            background: #ffffff;
            color: #000000;
            transition: all 0.2s;
        }
        .selection-btn.active {
            border-color: #f59e0b;
            background: rgba(245, 158, 11, 0.2);
            color: #ffffff;
        }
        .product-card {
            transition: transform 0.3s ease, border-color 0.3s ease;
            background-color: #252525;
            border: 1px solid #333;
        }
        .product-card:hover {
            transform: translateY(-5px);
            border-color: #f59e0b;
        }
        .view-hidden { display: none; }
        
        /* Matching the reference layout styling */
        .page-title-border {
            border-bottom: 1px solid #333;
            margin-bottom: 2rem;
            padding-bottom: 0.5rem;
        }
        .section-divider {
            border-top: 1px solid #333;
            margin: 2rem 0;
            position: relative;
        }
        .section-divider span {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: #1a1a1a;
            padding: 0 1rem;
        }
    </style>
</head>
<body class="p-4 md:p-8">

    <!-- Header Section -->
    <div class="max-w-6xl mx-auto">
        <h2 class="text-2xl font-bold page-title-border">Digital-Learning</h2>
        
        <header class="flex justify-between items-center mb-12">
            <div onclick="showStore()" class="cursor-pointer flex items-center gap-2 border-b-2 border-white pb-1">
                <div class="w-8 h-8 bg-orange-500 rounded flex items-center justify-center font-bold text-black text-xs">N</div>
                <h1 class="text-2xl font-bold tracking-tight">NEXGEN<span class="text-orange-500">STORE</span></h1>
            </div>
            <nav class="hidden md:flex gap-6 text-sm text-gray-400">
                <a href="javascript:void(0)" onclick="showStore()" class="hover:text-white transition">All Products</a>
                <a href="#" class="hover:text-white transition">Support</a>
                <a href="#" class="hover:text-white transition">My Orders</a>
            </nav>
        </header>
    </div>

    <!-- STOREFRONT VIEW -->
    <div id="storeView" class="max-w-6xl mx-auto">
        <div class="section-divider">
            <span class="text-xl font-bold">Premium Subscriptions</span>
        </div>
        
        <div class="text-center mb-10">
            <p class="text-gray-500 text-sm">Instant access to the world's best digital services at unbeatable prices.</p>
        </div>

        <div id="productGrid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
            <!-- Products will be injected here -->
        </div>
    </div>

    <!-- PRODUCT DETAIL VIEW -->
    <div id="detailView" class="max-w-6xl mx-auto view-hidden">
        <!-- Breadcrumbs -->
        <nav class="text-sm text-gray-500 mb-6">
            <a href="javascript:void(0)" onclick="showStore()" class="hover:text-gray-300">Home</a> / 
            <a href="#" class="hover:text-gray-300" id="detailCategory">Online Courses</a> / 
            <span id="detailCrumbName">Coursera</span>
        </nav>

        <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 mb-12">
            <!-- Left: Product Image -->
            <div id="detailImageContainer" class="relative group rounded-sm aspect-video flex items-center justify-center p-12">
                <!-- SVG Icon injected here -->
            </div>

            <!-- Right: Product Info -->
            <div class="flex flex-col">
                <h1 class="text-4xl font-bold mb-2" id="detailName">Coursera</h1>
                <p class="text-orange-400 text-xl font-semibold mb-6" id="detailPriceRange">$2.50 — $20.00</p>

                <div class="flex gap-4 mb-8">
                    <a href="#" class="flex-1 bg-orange-400 hover:bg-orange-500 text-white font-bold py-3 px-4 rounded text-center transition shadow-lg shadow-orange-900/20">
                        Buy on Telegram
                    </a>
                    <a href="#" class="flex-1 bg-[#d97706] hover:bg-orange-600 text-white font-bold py-3 px-4 rounded text-center transition">
                        Buy on WhatsApp
                    </a>
                </div>

                <p class="text-xs text-gray-400 italic mb-6">*Select Plans, Duration, and Others Type below to calculate the price.</p>

                <div class="space-y-6">
                    <div>
                        <label class="block text-sm font-bold mb-2">Account Type : <span class="font-normal text-gray-400">Personal (Private)</span></label>
                        <button class="selection-btn active px-4 py-2 text-sm rounded outline-none ring-1 ring-orange-500">Personal (Private)</button>
                    </div>

                    <div>
                        <label class="block text-sm font-bold mb-2">Plan : <span class="font-normal text-gray-400" id="detailPlanName">Plus</span></label>
                        <button class="selection-btn active px-4 py-2 text-sm rounded outline-none ring-1 ring-orange-500" id="detailPlanBtn">Plus</button>
                    </div>

                    <div>
                        <label class="block text-sm font-bold mb-2">Duration : <span class="font-normal text-gray-400" id="durationLabel">1 Month</span></label>
                        <div class="flex gap-2" id="durationContainer">
                            <!-- Buttons injected here -->
                        </div>
                        <button onclick="resetSelection()" class="text-xs text-orange-400 mt-2 underline">Clear</button>
                    </div>
                </div>

                <ul class="mt-8 space-y-2 text-sm text-gray-200">
                    <li class="flex items-center gap-2"><span class="text-blue-400">☑</span> Account access on your email.</li>
                    <li class="flex items-center gap-2"><span class="text-blue-400">☑</span> Non-Renewable.</li>
                    <li class="flex items-center gap-2"><span class="text-blue-400">☑</span> Full-time warranty.</li>
                    <li class="flex items-center gap-2"><span class="text-blue-400">☑</span> 100% genuine access to Coursera.</li>
                    <li class="flex items-center gap-2"><span class="text-blue-400">☑</span> Instant delivery.</li>
                </ul>

                <p class="text-3xl font-bold text-orange-400 mt-8" id="displayPrice">$0.00</p>
                
                <div class="mt-6 text-xs text-gray-500 space-y-1">
                    <p>SKU: N/A</p>
                    <p>Categories: <span class="text-orange-400">Online Courses, All time Popular, Learning Support</span></p>
                </div>
            </div>
        </div>

        <!-- Description Box -->
        <div class="border border-gray-700 rounded p-8 mb-20">
            <h2 class="text-3xl font-bold mb-6">Description</h2>
            <div class="space-y-4">
                <h3 class="text-2xl font-bold">## Before placing an order, please get in touch with us.</h3>
                <ul class="space-y-2 text-gray-300 ml-4 list-disc">
                    <li>Get a Coursera subscription at an affordable price.</li>
                    <li>100% genuine access to Coursera.</li>
                </ul>
            </div>
        </div>
    </div>

    <script>
        const products = [
            {
                id: 1,
                name: "Coursera",
                category: "Online Courses",
                range: "$2.50 — $20.00",
                color: "bg-blue-600",
                plan: "Plus",
                icon: `<svg viewBox="0 0 24 24" class="w-32 h-32 fill-white" xmlns="http://www.w3.org/2000/svg"><path d="M2.5 16.5C2.5 16.5 5 13.5 12 13.5C19 13.5 21.5 16.5 21.5 16.5V19.5C21.5 19.5 19 16.5 12 16.5C5 16.5 2.5 19.5 2.5 19.5V16.5Z"/><path d="M2.5 10.5C2.5 10.5 5 7.5 12 7.5C19 7.5 21.5 10.5 21.5 10.5V13.5C21.5 13.5 19 10.5 12 10.5C5 10.5 2.5 13.5 2.5 13.5V10.5Z"/><path d="M2.5 4.5C2.5 4.5 5 1.5 12 1.5C19 1.5 21.5 4.5 21.5 4.5V7.5C21.5 7.5 19 4.5 12 4.5C5 4.5 2.5 7.5 2.5 7.5V4.5Z"/></svg>`,
                durations: [
                    { label: "1 Month", price: 2.50 },
                    { label: "6 Month", price: 12.00 },
                    { label: "1 Year", price: 20.00 }
                ]
            },
            {
                id: 2,
                name: "Netflix",
                category: "Streaming",
                range: "$3.00 — $35.00",
                color: "bg-red-600",
                plan: "Premium 4K",
                icon: `<svg viewBox="0 0 24 24" class="w-32 h-32 fill-white" xmlns="http://www.w3.org/2000/svg"><path d="M6.5 2v20c1-.5 2.5-1 3.5-1s2.5.5 3.5 1V2c-1 .5-2.5 1-3.5 1s-2.5-.5-3.5-1z"/><path d="M17 2v20c1-.5 2.5-1 3.5-1V2c-1 .5-2.5 1-3.5 1z"/><path d="M3.5 2v20c1-.5 2.5-1 3.5-1V2c-1 .5-2.5 1-3.5 1z" opacity=".5"/></svg>`,
                durations: [
                    { label: "1 Month", price: 3.00 },
                    { label: "3 Month", price: 8.50 },
                    { label: "1 Year", price: 35.00 }
                ]
            },
            {
                id: 3,
                name: "Spotify",
                category: "Music",
                range: "$1.50 — $15.00",
                color: "bg-green-600",
                plan: "Premium Family",
                icon: `<svg viewBox="0 0 24 24" class="w-32 h-32 fill-white" xmlns="http://www.w3.org/2000/svg"><path d="M12 0C5.373 0 0 5.373 0 12s5.373 12 12 12 12-5.373 12-12S18.627 0 12 0zm5.51 17.3c-.22.36-.68.48-1.05.25-2.81-1.72-6.35-2.1-10.52-1.15-.41.09-.82-.16-.91-.57-.09-.41.16-.82.57-.91 4.57-1.04 8.49-.6 11.66 1.34.37.22.49.68.25 1.04zm1.48-3.26c-.28.45-.87.59-1.32.32-3.22-1.98-8.12-2.55-11.93-1.4-.5.15-1.03-.13-1.18-.63-.15-.5.13-1.03.63-1.18 4.35-1.32 9.77-.67 13.48 1.61.45.27.59.86.32 1.3zm.13-3.4c-3.86-2.29-10.24-2.51-13.97-1.38-.59.18-1.22-.16-1.4-.75-.18-.59.16-1.22.75-1.4 4.29-1.3 11.33-1.04 15.78 1.6.53.31.71 1 .4 1.53-.31.53-1 .71-1.56.4z"/></svg>`,
                durations: [
                    { label: "1 Month", price: 1.50 },
                    { label: "6 Month", price: 8.00 },
                    { label: "1 Year", price: 15.00 }
                ]
            }
        ];

        let currentProduct = null;

        function renderStore() {
            const grid = document.getElementById('productGrid');
            grid.innerHTML = products.map(p => `
                <div onclick="showDetails(${p.id})" class="product-card p-6 rounded-lg cursor-pointer">
                    <div class="${p.color} aspect-video rounded-md flex items-center justify-center mb-6 overflow-hidden">
                        ${p.icon.replace('w-32 h-32', 'w-16 h-16')}
                    </div>
                    <div class="flex justify-between items-end">
                        <h3 class="text-md font-bold text-gray-200">${p.name}</h3>
                        <p class="text-orange-500 font-bold text-sm">${p.range.split('—')[0].trim()}</p>
                    </div>
                </div>
            `).join('');
        }

        function showDetails(id) {
            currentProduct = products.find(p => p.id === id);
            
            document.getElementById('storeView').classList.add('view-hidden');
            document.getElementById('detailView').classList.remove('view-hidden');
            
            // Populate Details
            document.getElementById('detailName').innerText = currentProduct.name;
            document.getElementById('detailCrumbName').innerText = currentProduct.name;
            document.getElementById('detailCategory').innerText = currentProduct.category;
            document.getElementById('detailPriceRange').innerText = currentProduct.range;
            document.getElementById('detailPlanName').innerText = currentProduct.plan;
            document.getElementById('detailPlanBtn').innerText = currentProduct.plan;
            document.getElementById('detailImageContainer').className = `relative group rounded-sm aspect-video flex items-center justify-center p-12 ${currentProduct.color}`;
            document.getElementById('detailImageContainer').innerHTML = currentProduct.icon;

            // Render Duration Buttons
            const container = document.getElementById('durationContainer');
            container.innerHTML = currentProduct.durations.map((d, i) => `
                <button onclick="setDuration('${d.label}', ${d.price})" 
                        class="duration-btn selection-btn ${i === 0 ? 'active outline-none ring-1 ring-orange-500' : ''} px-6 py-2 text-sm rounded">
                    ${d.label}
                </button>
            `).join('');

            // Set Initial Price
            setDuration(currentProduct.durations[0].label, currentProduct.durations[0].price);
            window.scrollTo(0, 0);
        }

        function showStore() {
            document.getElementById('storeView').classList.remove('view-hidden');
            document.getElementById('detailView').classList.add('view-hidden');
        }

        function setDuration(label, price) {
            document.getElementById('durationLabel').innerText = label;
            document.getElementById('displayPrice').innerText = '$' + price.toFixed(2);

            const buttons = document.querySelectorAll('.duration-btn');
            buttons.forEach(btn => {
                if (btn.innerText.trim() === label) {
                    btn.classList.add('active', 'outline-none', 'ring-1', 'ring-orange-500');
                    btn.classList.remove('bg-white', 'text-black');
                } else {
                    btn.classList.remove('active', 'outline-none', 'ring-1', 'ring-orange-500');
                    btn.classList.add('bg-white', 'text-black');
                }
            });
        }

        function resetSelection() {
            if (currentProduct) {
                setDuration(currentProduct.durations[0].label, currentProduct.durations[0].price);
            }
        }

        // Initialize
        renderStore();
    </script>
</body>
</html>
