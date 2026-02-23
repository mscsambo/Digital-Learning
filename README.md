
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Sentinel | Professional AI Content Detector</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mammoth/1.6.0/mammoth.browser.min.js"></script>

    <script>
        // Dark Mode Initialization
        if (localStorage.theme === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
            document.documentElement.classList.add('dark');
        } else {
            document.documentElement.classList.remove('dark');
        }
    </script>

    <style>
        .gradient-bg { background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%); }
        .dark .gradient-bg { background: linear-gradient(135deg, #1e1b4b 0%, #4338ca 100%); }
        .loading-pulse { animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite; }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: .5; } }
    </style>
</head>
<body class="bg-gray-50 dark:bg-gray-900 text-gray-900 dark:text-gray-100 transition-colors duration-300 min-h-screen">

    <div class="fixed top-4 right-4 z-50">
        <button onclick="toggleDarkMode()" class="p-3 rounded-full bg-white dark:bg-gray-800 shadow-xl border border-gray-200 dark:border-gray-700">
            <i id="theme-icon" class="fas fa-moon text-indigo-600 dark:text-yellow-400"></i>
        </button>
    </div>

    <header class="gradient-bg py-16 px-4 text-center text-white shadow-lg">
        <h1 class="text-4xl md:text-5xl font-extrabold mb-4">AI Sentinel</h1>
        <p class="text-lg opacity-90 max-w-2xl mx-auto">Verify text authenticity. Detect content from ChatGPT, Gemini, Claude, and more using deep-learning models.</p>
    </header>

    <main class="max-w-4xl mx-auto -mt-12 px-4 pb-12">
        <div class="bg-white dark:bg-gray-800 rounded-2xl shadow-2xl p-6 md:p-10 border border-gray-100 dark:border-gray-700">
            
            <div class="mb-8">
                <label class="block text-sm font-bold mb-3 uppercase tracking-wider text-gray-500 dark:text-gray-400">Import Document</label>
                <label class="flex flex-col items-center justify-center w-full h-32 border-2 border-dashed border-gray-300 dark:border-gray-600 rounded-xl cursor-pointer bg-gray-50 dark:bg-gray-700/50 hover:bg-indigo-50 dark:hover:bg-gray-700 transition">
                    <div class="flex flex-col items-center justify-center pt-5 pb-6">
                        <i class="fas fa-file-upload text-3xl text-indigo-400 mb-2"></i>
                        <p class="text-sm">Click to upload <span class="font-bold text-indigo-500">PDF, DOCX, or TXT</span></p>
                    </div>
                    <input id="fileUpload" type="file" class="hidden" accept=".pdf,.docx,.txt" />
                </label>
            </div>

            <div class="flex flex-wrap gap-3 mb-4">
                <div class="px-4 py-2 bg-indigo-50 dark:bg-indigo-900/30 text-indigo-600 dark:text-indigo-300 rounded-lg text-xs font-bold border border-indigo-100 dark:border-indigo-800">
                    WORDS: <span id="wordCount">0</span>
                </div>
                <div class="px-4 py-2 bg-blue-50 dark:bg-blue-900/30 text-blue-600 dark:text-blue-300 rounded-lg text-xs font-bold border border-blue-100 dark:border-blue-800">
                    CHARS: <span id="charCount">0</span>
                </div>
                <div class="px-4 py-2 bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300 rounded-lg text-xs font-bold">
                    READ TIME: <span id="readingTime">0</span>s
                </div>
            </div>

            <textarea id="content" rows="10" class="w-full p-5 border border-gray-200 dark:border-gray-600 rounded-xl focus:ring-4 focus:ring-indigo-500/20 focus:outline-none dark:bg-gray-900 dark:text-white transition" placeholder="Paste your content here for analysis..."></textarea>

            <button onclick="analyzeText()" id="checkBtn" class="w-full mt-6 bg-indigo-600 hover:bg-indigo-700 text-white font-black py-4 rounded-xl transition-all transform hover:scale-[1.01] shadow-xl text-lg">
                ANALYZE CONTENT
            </button>

            <div id="results" class="hidden mt-12 border-t dark:border-gray-700 pt-10">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <div class="bg-gray-50 dark:bg-gray-900/50 p-8 rounded-2xl text-center border border-gray-100 dark:border-gray-800">
                        <p class="text-gray-400 uppercase text-xs font-black mb-2">AI Probability</p>
                        <div class="text-6xl font-black" id="score">0%</div>
                    </div>
                    <div class="flex flex-col justify-center items-center p-8 bg-gray-50 dark:bg-gray-900/50 rounded-2xl border border-gray-100 dark:border-gray-800">
                        <p class="text-gray-400 uppercase text-xs font-black mb-2">Verdict</p>
                        <div class="text-2xl font-bold mb-4 text-center" id="verdict">Checking...</div>
                        <button onclick="downloadReport()" class="text-sm bg-gray-800 hover:bg-black text-white px-6 py-2 rounded-lg transition flex items-center gap-2">
                            <i class="fas fa-download"></i> PDF Report
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <div class="mt-12 bg-white dark:bg-gray-800 rounded-2xl shadow-lg p-6 border border-gray-100 dark:border-gray-700">
            <div class="flex items-center justify-between mb-6">
                <h3 class="font-black text-xl text-gray-800 dark:text-white uppercase tracking-tighter">Scan History</h3>
                <button onclick="clearHistory()" class="text-xs font-bold text-red-500 hover:text-red-700 uppercase">Clear All</button>
            </div>
            <div id="historyList" class="space-y-4">
                <p class="text-center text-gray-400 py-4 italic" id="emptyHistory">Your recent scans will appear here.</p>
            </div>
        </div>
    </main>

    <footer class="text-center py-10 text-gray-400 text-xs uppercase tracking-widest">
        &copy; 2026 AI Sentinel &bull; Secure AI Detection
    </footer>

    <script>
        const API_KEY = "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";
        const textArea = document.getElementById('content');
        
        // --- 1. DARK MODE LOGIC ---
        function toggleDarkMode() {
            const html = document.documentElement;
            const icon = document.getElementById('theme-icon');
            if (html.classList.contains('dark')) {
                html.classList.remove('dark');
                localStorage.theme = 'light';
                icon.classList.replace('fa-sun', 'fa-moon');
            } else {
                html.classList.add('dark');
                localStorage.theme = 'dark';
                icon.classList.replace('fa-moon', 'fa-sun');
            }
        }

        // --- 2. COUNTER LOGIC ---
        textArea.addEventListener('input', () => {
            const text = textArea.value.trim();
            const words = text ? text.split(/\s+/).length : 0;
            document.getElementById('wordCount').innerText = words;
            document.getElementById('charCount').innerText = text.length;
            document.getElementById('readingTime').innerText = Math.max(1, Math.round((words / 200) * 60));
        });

        // --- 3. FILE UPLOAD LOGIC ---
        document.getElementById('fileUpload').addEventListener('change', async function(e) {
            const file = e.target.files[0];
            if (!file) return;
            
            if (file.type === "text/plain") {
                const reader = new FileReader();
                reader.onload = (e) => { textArea.value = e.target.result; textArea.dispatchEvent(new Event('input')); };
                reader.readAsText(file);
            } else if (file.type === "application/pdf") {
                const arrayBuffer = await file.arrayBuffer();
                const pdfJS = window['pdfjs-dist/build/pdf'];
                pdfJS.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.worker.min.js';
                const pdf = await pdfJS.getDocument(arrayBuffer).promise;
                let fullText = "";
                for (let i = 1; i <= pdf.numPages; i++) {
                    const page = await pdf.getPage(i);
                    const content = await page.getTextContent();
                    fullText += content.items.map(item => item.str).join(" ") + " ";
                }
                textArea.value = fullText; textArea.dispatchEvent(new Event('input'));
            } else if (file.name.endsWith('.docx')) {
                const arrayBuffer = await file.arrayBuffer();
                mammoth.extractRawText({ arrayBuffer }).then(res => { 
                    textArea.value = res.value; textArea.dispatchEvent(new Event('input')); 
                });
            }
        });

        // --- 4. AI DETECTION & HISTORY ---
        async function analyzeText() {
            const text = textArea.value.trim();
            if (text.length < 50) return alert("Please enter at least 50 characters.");

            const btn = document.getElementById('checkBtn');
            const results = document.getElementById('results');
            
            btn.disabled = true;
            btn.innerHTML = '<i class="fas fa-circle-notch fa-spin mr-2"></i> Analyzing...';
            results.classList.remove('hidden');
            results.classList.add('loading-pulse');

            try {
                const response = await fetch("https://api-inference.huggingface.co/models/openai-community/roberta-base-openai-detector", {
                    method: "POST",
                    headers: { "Content-Type": "application/json", "Authorization": `Bearer ${API_KEY}` },
                    body: JSON.stringify({ inputs: text }),
                });

                const data = await response.json();
                
                // Handle warming up
                if (data.error && data.estimated_time) {
                    btn.innerHTML = `<i class="fas fa-clock mr-2"></i> Engine Warming (${Math.round(data.estimated_time)}s)`;
                    setTimeout(analyzeText, 5000);
                    return;
                }

                const aiScore = Math.round(data[0].find(i => i.label === "LABEL_1" || i.label === "Fake").score * 100);
                
                updateUI(aiScore);
                addToHistory(text, aiScore);

            } catch (err) {
                alert("The engine is currently busy. Please try again in a few seconds.");
            } finally {
                btn.disabled = false;
                btn.innerHTML = 'ANALYZE CONTENT';
                results.classList.remove('loading-pulse');
            }
        }

        function updateUI(score) {
            const scoreEl = document.getElementById('score');
            const verdictEl = document.getElementById('verdict');
            scoreEl.innerText = score + '%';
            
            if (score > 70) {
                scoreEl.className = "text-6xl font-black text-red-600";
                verdictEl.innerText = "Highly Likely AI Generated";
            } else if (score > 40) {
                scoreEl.className = "text-6xl font-black text-yellow-500";
                verdictEl.innerText = "Possible AI/Human Hybrid";
            } else {
                scoreEl.className = "text-6xl font-black text-green-600";
                verdictEl.innerText = "Likely Human Written";
            }
        }

        function addToHistory(text, score) {
            let history = JSON.parse(localStorage.getItem('sentinelHistory') || '[]');
            history.unshift({ id: Date.now(), preview: text.substring(0, 50) + "...", score, date: new Date().toLocaleTimeString() });
            history = history.slice(0, 5);
            localStorage.setItem('sentinelHistory', JSON.stringify(history));
            renderHistory();
        }

        function renderHistory() {
            const history = JSON.parse(localStorage.getItem('sentinelHistory') || '[]');
            const list = document.getElementById('historyList');
            const empty = document.getElementById('emptyHistory');
            
            if (history.length === 0) { empty.className = "block"; list.innerHTML = ''; return; }
            empty.className = "hidden";
            list.innerHTML = history.map(item => `
                <div class="flex items-center justify-between p-4 bg-gray-50 dark:bg-gray-900 rounded-xl border border-gray-100 dark:border-gray-700">
                    <div><p class="text-sm font-bold">${item.preview}</p><p class="text-xs text-gray-400">${item.date}</p></div>
                    <div class="font-black ${item.score > 70 ? 'text-red-500' : 'text-green-500'}">${item.score}% AI</div>
                </div>
            `).join('');
        }

        function clearHistory() { localStorage.removeItem('sentinelHistory'); renderHistory(); }

        // --- 5. PDF REPORT GEN ---
        function downloadReport() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            const text = textArea.value;
            const score = document.getElementById('score').innerText;
            const verdict = document.getElementById('verdict').innerText;

            doc.setFontSize(22); doc.setTextColor(79, 70, 229);
            doc.text("AI Sentinel Report", 20, 20);
            doc.setFontSize(10); doc.setTextColor(150);
            doc.text(`Date: ${new Date().toLocaleString()}`, 20, 30);
            
            doc.setFontSize(16); doc.setTextColor(0);
            doc.text(`Result: ${verdict} (${score})`, 20, 50);
            
            doc.setFontSize(10);
            const lines = doc.splitTextToSize(text.substring(0, 2000), 170);
            doc.text(lines, 20, 70);
            
            doc.save("AI-Sentinel-Report.pdf");
        }

        window.onload = () => {
            renderHistory();
            if (document.documentElement.classList.contains('dark')) {
                document.getElementById('theme-icon').classList.replace('fa-moon', 'fa-sun');
            }
        };
    </script>
</body>
</html>
