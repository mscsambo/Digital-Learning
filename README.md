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
        
        <div class="flex flex-wrap gap-4 mb-4 text-sm font-medium">
            <div class="bg-indigo-50 text-indigo-700 px-4 py-2 rounded-lg border border-indigo-100">
                Words: <span id="wordCount">0</span>
            </div>
            <div class="bg-blue-50 text-blue-700 px-4 py-2 rounded-lg border border-blue-100">
                Characters: <span id="charCount">0</span>
            </div>
            <div id="readingTime" class="bg-gray-50 text-gray-600 px-4 py-2 rounded-lg border border-gray-100">
                Reading time: 0m
            </div>
        </div>

        <div class="mb-4">
            <label for="content" class="block text-gray-700 font-bold mb-2">Paste your text below:</label>
            <textarea id="content" rows="10" class="w-full p-4 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:outline-none text-gray-700" placeholder="Paste the content you want to analyze here..."></textarea>
        </div>
        
        <div class="flex flex-col md:flex-row items-center justify-between gap-4">
            <p class="text-xs text-gray-400 italic">* Minimum 50 words recommended for accuracy.</p>
            <button onclick="analyzeText()" id="checkBtn" class="w-full md:w-auto bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 px-10 rounded-full transition duration-300 shadow-lg transform hover:scale-105">
                Analyze Content
            </button>
        </div>

        <div id="results" class="hidden mt-12 border-t pt-8 animate-pulse">
            <h2 class="text-2xl font-bold text-center mb-8">Analysis Results</h2>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="bg-gray-50 p-6 rounded-lg text-center border">
                    <p class="text-gray-500 uppercase text-xs font-bold mb-2">AI Probability</p>
                    <div class="text-5xl font-extrabold" id="score">--</div>
                </div>
                <div class="bg-gray-50 p-6 rounded-lg text-center border">
                    <p class="text-gray-500 uppercase text-xs font-bold mb-2">Verdict</p>
                    <div class="text-2xl font-bold mt-2" id="verdict">Processing...</div>
                </div>
            </div>
        </div>
    </div>
</main>

<script>
    const textArea = document.getElementById('content');
    const wordCount = document.getElementById('wordCount');
    const charCount = document.getElementById('charCount');
    const readingTime = document.getElementById('readingTime');

    // --- Live Counter Logic ---
    textArea.addEventListener('input', () => {
        const text = textArea.value.trim();
        const words = text ? text.split(/\s+/).length : 0;
        const chars = text.length;
        
        wordCount.innerText = words;
        charCount.innerText = chars;
        readingTime.innerText = `Reading time: ${Math.ceil(words / 200)}m`;
    });

    // --- AI Detection Logic (Using Hugging Face API) ---
    async function analyzeText() {
        const text = textArea.value.trim();
        const btn = document.getElementById('checkBtn');
        const resultsDiv = document.getElementById('results');
        const scoreEl = document.getElementById('score');
        const verdictEl = document.getElementById('verdict');

        if (text.length < 100) {
            alert("Please enter at least 100 characters for a reliable result.");
            return;
        }

        btn.innerHTML = '<i class="fas fa-spinner fa-spin mr-2"></i> Scanning Models...';
        btn.disabled = true;
        resultsDiv.classList.remove('hidden');

        try {
            // Using the RoBERTa model which is great at detecting GPT/LLM text
            const response = await fetch("https://api-inference.huggingface.co/models/openai-community/roberta-base-openai-detector", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ inputs: text }),
            });

            const result = await response.json();
            
            // The model returns an array: [{label: "Fake", score: 0.99}, {label: "Real", score: 0.01}]
            const aiData = result[0].find(item => item.label === "Fake" || item.label === "LABEL_1");
            const aiScore = Math.round(aiData.score * 100);

            // Update UI
            resultsDiv.classList.remove('animate-pulse');
            scoreEl.innerText = aiScore + '%';
            
            if (aiScore > 70) {
                verdictEl.innerText = "Likely AI Generated";
                scoreEl.className = "text-5xl font-extrabold text-red-600";
            } else if (aiScore > 40) {
                verdictEl.innerText = "Possible AI/Human Mix";
                scoreEl.className = "text-5xl font-extrabold text-yellow-600";
            } else {
                verdictEl.innerText = "Likely Human Written";
                scoreEl.className = "text-5xl font-extrabold text-green-600";
            }

        } catch (error) {
            console.error("API Error:", error);
            alert("The detection engine is currently busy. Please try again in a moment.");
        } finally {
            btn.innerHTML = 'Analyze Content';
            btn.disabled = false;
        }
    }
</script>
</body>
</html>
