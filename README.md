<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Sentinel | AI Content Detector</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        .gradient-bg {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }
    </style>
</head>
<body class="bg-gray-50 font-sans leading-normal tracking-normal">

    <nav class="flex items-center justify-between flex-wrap p-6 bg-white shadow-sm">
        <div class="flex items-center flex-shrink-0 text-gray-800 mr-6">
            <span class="font-bold text-xl tracking-tight text-indigo-600"><i class="fas fa-robot mr-2"></i>AI Sentinel</span>
        </div>
        <div class="block lg:hidden">
            <button class="flex items-center px-3 py-2 border rounded text-gray-500 border-gray-400 hover:text-gray-800 hover:border-indigo-500">
                <svg class="fill-current h-3 w-3" viewBox="0 0 20 20"><title>Menu</title><path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"/></svg>
            </button>
        </div>
        <div class="w-full block flex-grow lg:flex lg:items-center lg:w-auto">
            <div class="text-sm lg:flex-grow text-right">
                <a href="#" class="block mt-4 lg:inline-block lg:mt-0 text-gray-600 hover:text-indigo-600 mr-4">How it works</a>
                <a href="#" class="block mt-4 lg:inline-block lg:mt-0 text-gray-600 hover:text-indigo-600 mr-4">API</a>
                <a href="#" class="inline-block text-sm px-4 py-2 leading-none border rounded text-indigo-600 border-indigo-600 hover:border-transparent hover:text-white hover:bg-indigo-600 mt-4 lg:mt-0">Premium</a>
            </div>
        </div>
    </nav>

    <header class="gradient-bg py-16 px-4 text-center text-white">
        <h1 class="text-4xl md:text-5xl font-bold mb-4">AI Content Detector</h1>
        <p class="text-xl opacity-90">Verify if text was written by ChatGPT, Gemini, Claude, or a Human.</p>
    </header>

    <main class="max-w-4xl mx-auto -mt-10 px-4 pb-12">
        <div class="bg-white rounded-xl shadow-2xl p-6 md:p-8">
            <div class="mb-4">
                <label for="content" class="block text-gray-700 font-bold mb-2">Paste your text below (minimum 50 words recommended):</label>
                <textarea id="content" rows="10" class="w-full p-4 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:outline-none text-gray-700" placeholder="Paste the content you want to analyze here..."></textarea>
            </div>
            
            <div class="flex flex-col md:flex-row items-center justify-between gap-4">
                <div class="text-sm text-gray-500">
                    Character count: <span id="charCount">0</span>
                </div>
                <button onclick="analyzeText()" id="checkBtn" class="w-full md:w-auto bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 px-10 rounded-full transition duration-300 shadow-lg transform hover:scale-105">
                    Analyze Text
                </button>
            </div>

            <div id="results" class="hidden mt-12 border-t pt-8">
                <h2 class="text-2xl font-bold text-center mb-8">Analysis Results</h2>
                <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                    <div class="bg-gray-50 p-6 rounded-lg text-center border">
                        <p class="text-gray-500 uppercase text-xs font-bold tracking-widest mb-2">AI Probability</p>
                        <div class="text-5xl font-extrabold text-indigo-600" id="score">0%</div>
                    </div>
                    <div class="bg-gray-50 p-6 rounded-lg text-center border">
                        <p class="text-gray-500 uppercase text-xs font-bold tracking-widest mb-2">Verdict</p>
                        <div class="text-2xl font-bold mt-2" id="verdict">Likely Human</div>
                    </div>
                    <div class="bg-gray-50 p-6 rounded-lg text-center border">
                        <p class="text-gray-500 uppercase text-xs font-bold tracking-widest mb-2">Models Scanned</p>
                        <div class="flex justify-center gap-2 mt-2 text-indigo-400">
                            <i class="fas fa-brain" title="GPT-4"></i>
                            <i class="fas fa-bolt" title="Gemini"></i>
                            <i class="fas fa-feather" title="Claude"></i>
                        </div>
                        <p class="text-xs text-gray-400 mt-2">Multi-model consensus</p>
                    </div>
                </div>
            </div>
        </div>

        <section class="mt-16 grid grid-cols-1 md:grid-cols-3 gap-8 text-center">
            <div>
                <div class="bg-indigo-100 w-12 h-12 rounded-full flex items-center justify-center mx-auto mb-4">
                    <i class="fas fa-check text-indigo-600"></i>
                </div>
                <h3 class="font-bold text-lg">99% Accuracy</h3>
                <p class="text-gray-600 text-sm">Trained on billions of tokens from LLMs and human writers.</p>
            </div>
            <div>
                <div class="bg-indigo-100 w-12 h-12 rounded-full flex items-center justify-center mx-auto mb-4">
                    <i class="fas fa-shield-alt text-indigo-600"></i>
                </div>
                <h3 class="font-bold text-lg">Privacy First</h3>
                <p class="text-gray-600 text-sm">We don't store your content or use it for training data.</p>
            </div>
            <div>
                <div class="bg-indigo-100 w-12 h-12 rounded-full flex items-center justify-center mx-auto mb-4">
                    <i class="fas fa-infinity text-indigo-600"></i>
                </div>
                <h3 class="font-bold text-lg">Unlimited Checks</h3>
                <p class="text-gray-600 text-sm">Our free tier allows for extensive daily checking.</p>
            </div>
        </section>
    </main>

    <footer class="bg-white border-t py-8 text-center text-gray-500 text-sm">
        &copy; 2026 AI Sentinel Inc. All rights reserved.
    </footer>

    <script>
        // Simple UI Logic
        const textArea = document.getElementById('content');
        const charCount = document.getElementById('charCount');

        textArea.addEventListener('input', () => {
            charCount.innerText = textArea.value.length;
        });

        function analyzeText() {
            const text = textArea.value.trim();
            const btn = document.getElementById('checkBtn');
            const resultsDiv = document.getElementById('results');

            if (text.length < 20) {
                alert("Please enter more text for an accurate analysis.");
                return;
            }

            // UI Feedback: Loading state
            btn.innerHTML = '<i class="fas fa-circle-notch fa-spin mr-2"></i> Analyzing...';
            btn.disabled = true;

            // Simulate an API call delay
            setTimeout(() => {
                // For demonstration, we'll generate a random "AI" score
                // In a real app, you'd send 'text' to an API here.
                const randomScore = Math.floor(Math.random() * 100);
                
                resultsDiv.classList.remove('hidden');
                document.getElementById('score').innerText = randomScore + '%';
                
                const verdict = document.getElementById('verdict');
                if(randomScore > 70) {
                    verdict.innerText = "Highly Likely AI";
                    verdict.className = "text-2xl font-bold mt-2 text-red-600";
                } else if (randomScore > 40) {
                    verdict.innerText = "Mixed Content";
                    verdict.className = "text-2xl font-bold mt-2 text-yellow-600";
                } else {
                    verdict.innerText = "Likely Human";
                    verdict.className = "text-2xl font-bold mt-2 text-green-600";
                }

                btn.innerHTML = 'Analyze Text';
                btn.disabled = false;
                
                // Scroll to results
                resultsDiv.scrollIntoView({ behavior: 'smooth' });
            }, 1500);
        }
    </script>
</body>
</html>
