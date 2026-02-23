<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Sentinel | Professional Content Detector</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.4.120/pdf.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mammoth/1.6.0/mammoth.browser.min.js"></script>

    <style>
        .gradient-bg { background: linear-gradient(135deg, #4f46e5 0%, #7c3aed 100%); }
        .loading-pulse { animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite; }
        @keyframes pulse { 0%, 100% { opacity: 1; } 50% { opacity: .5; } }
    </style>
</head>
<body class="bg-gray-50 text-gray-900 font-sans min-h-screen">

    <header class="gradient-bg py-16 px-4 text-center text-white shadow-lg">
        <h1 class="text-4xl md:text-5xl font-extrabold mb-4 uppercase tracking-tighter">AI Sentinel</h1>
        <p class="text-lg opacity-90 max-w-2xl mx-auto font-light">Verify authenticity instantly using on-device machine learning.</p>
    </header>

    <main class="max-w-4xl mx-auto -mt-12 px-4 pb-12">
        <div class="bg-white rounded-2xl shadow-2xl p-6 md:p-10 border border-gray-100">
            
            <div class="mb-8">
                <label class="block text-sm font-bold mb-3 uppercase tracking-wider text-gray-400">Import Document</label>
                <label class="flex flex-col items-center justify-center w-full h-32 border-2 border-dashed border-gray-200 rounded-xl cursor-pointer bg-gray-50 hover:bg-indigo-50 transition">
                    <div class="flex flex-col items-center justify-center pt-5 pb-6">
                        <i class="fas fa-file-upload text-3xl text-indigo-400 mb-2"></i>
                        <p class="text-sm">Click to upload <span class="font-bold text-indigo-600">PDF, DOCX, or TXT</span></p>
                    </div>
                    <input id="fileUpload" type="file" class="hidden" accept=".pdf,.docx,.txt" />
                </label>
            </div>

            <div class="flex flex-wrap gap-3 mb-4">
                <div class="px-4 py-2 bg-indigo-50 text-indigo-600 rounded-lg text-xs font-bold border border-indigo-100 uppercase">
                    Words: <span id="wordCount">0</span>
                </div>
                <div class="px-4 py-2 bg-blue-50 text-blue-600 rounded-lg text-xs font-bold border border-blue-100 uppercase">
                    Characters: <span id="charCount">0</span>
                </div>
                <div class="px-4 py-2 bg-gray-100 text-gray-600 rounded-lg text-xs font-bold uppercase">
                    Read Time: <span id="readingTime">0</span>s
                </div>
            </div>

            <textarea id="content" rows="10" class="w-full p-5 border border-gray-200 rounded-xl focus:ring-4 focus:ring-indigo-500/20 focus:outline-none transition text-lg" placeholder="Paste your content here for analysis..."></textarea>

            <div id="setupLoader" class="mt-6 mb-2 hidden">
                <div class="flex justify-between mb-1">
                    <span class="text-xs font-bold text-indigo-600 uppercase">Downloading AI Engine...</span>
                    <span id="progressPercent" class="text-xs font-bold text-indigo-600">0%</span>
                </div>
                <div class="w-full bg-gray-100 rounded-full h-2">
                    <div id="progressBar" class="bg-indigo-600 h-2 rounded-full transition-all duration-300" style="width: 0%"></div>
                </div>
            </div>

            <button onclick="analyzeText()" id="checkBtn" class="w-full mt-4 bg-indigo-600 hover:bg-indigo-700 text-white font-black py-5 rounded-xl transition-all transform hover:scale-[1.01] shadow-xl text-lg uppercase tracking-widest">
                Analyze Content
            </button>

            <div id="results" class="hidden mt-12 border-t pt-10">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                    <div class="bg-gray-50 p-8 rounded-2xl text-center border border-gray-100">
                        <p class="text-gray-400 uppercase text-xs font-black mb-2">AI Probability</p>
                        <div class="text-6xl font-black" id="score">0%</div>
                    </div>
                    <div class="flex flex-col justify-center items-center p-8 bg-gray-50 rounded-2xl border border-gray-100">
                        <p class="text-gray-400 uppercase text-xs font-black mb-2">Verdict</p>
                        <div class="text-2xl font-bold mb-4 text-center" id="verdict">Checking...</div>
                        <button onclick="downloadReport()" class="text-sm bg-gray-800 hover:bg-black text-white px-6 py-2 rounded-lg transition flex items-center gap-2">
                            <i class="fas fa-file-pdf"></i> Download PDF Report
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <div class="mt-12 bg-white rounded-2xl shadow-lg p-6 border border-gray-100">
            <div class="flex items-center justify-between mb-6">
                <h3 class="font-black text-xl text-gray-800 uppercase tracking-tighter">Recent Scans</h3>
                <button onclick="clearHistory()" class="text-xs font-bold text-red-500 hover:text-red-700 uppercase">Clear All</button>
            </div>
            <div id="historyList" class="space-y-4 text-center">
                <p class="text-gray-400 py-4 italic" id="emptyHistory">No recent scans yet.</p>
            </div>
        </div>
    </main>

    <footer class="text-center py-10 text-gray-400 text-xs uppercase tracking-widest">
        &copy; 2026 AI Sentinel &bull; Privacy-First AI Detection
    </footer>

    <script type="module">
        import { pipeline, env } from 'https://cdn.jsdelivr.net/npm/@xenova/transformers@2.17.2';
        
        env.allowLocalModels = false;
        let detectorPipe = null;
        const textArea = document.getElementById('content');

        // --- 1. INITIALIZE ON-DEVICE ENGINE ---
        async function initModel() {
            const loader = document.getElementById('setupLoader');
            const progressBar = document.getElementById('progressBar');
            const progressPercent = document.getElementById('progressPercent');
            const btn = document.getElementById('checkBtn');

            loader.classList.remove('hidden');
            btn.disabled = true;

            try {
                detectorPipe = await pipeline('text-classification', 'Xenova/roberta-base-openai-detector', {
                    progress_callback: (data) => {
                        if (data.status === 'progress') {
                            const p = Math.round(data.progress);
                            progressBar.style.width = `${p}%`;
                            progressPercent.innerText = `${p}%`;
                        }
                        if (data.status === 'ready') {
                            loader.classList.add('hidden');
                            btn.disabled = false;
                            btn.innerHTML = 'ANALYZE CONTENT';
                        }
                    }
                });
            } catch (err) {
                console.error(err);
                btn.innerHTML = "Error Loading Engine";
            }
        }
        initModel();

        // --- 2. ANALYZE LOGIC ---
        window.analyzeText = async function() {
            const text = textArea.value.trim();
            if (text.length < 50) return alert("Please enter at least 50 characters.");
            if (!detectorPipe) return alert("Engine is still loading...");

            const btn = document.getElementById('checkBtn');
            const results = document.getElementById('results');
            
            btn.disabled = true;
            btn.innerHTML = '<i class="fas fa-brain fa-spin mr-2"></i> Locally Processing...';
            results.classList.remove('hidden');
            results.classList.add('loading-pulse');

            try {
                const output = await detectorPipe(text);
                const prediction = output[0];
                let aiScore = prediction.label === 'Fake' ? Math.round(prediction.score * 100) : Math.round((1 - prediction.score) * 100);

                updateUI(aiScore);
                addToHistory(text, aiScore);
            } catch (err) {
                alert("Processing error. Please refresh.");
            } finally {
                btn.disabled = false;
                btn.innerHTML = 'ANALYZE CONTENT';
                results.classList.remove('loading-pulse');
            }
        };

        // --- 3. UI & FILE HANDLERS ---
        textArea.addEventListener('input', () => {
            const text = textArea.value.trim();
            const words = text ? text.split(/\s+/).length : 0;
            document.getElementById('wordCount').innerText = words;
            document.getElementById('charCount').innerText = text.length;
            document.getElementById('readingTime').innerText = Math.max(1, Math.round((words / 200) * 60));
        });

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

        function updateUI(score) {
            const scoreEl = document.getElementById('score');
            const verdictEl = document.getElementById('verdict');
            scoreEl.innerText = score + '%';
            if (score > 70) { scoreEl.className = "text-6xl font-black text-red-600"; verdictEl.innerText = "Highly Likely AI"; }
            else if (score > 40) { scoreEl.className = "text-6xl font-black text-yellow-500"; verdictEl.innerText = "Possible Hybrid"; }
            else { scoreEl.className = "text-6xl font-black text-green-600"; verdictEl.innerText = "Likely Human"; }
        }

        function addToHistory(text, score) {
            let history = JSON.parse(localStorage.getItem('sentinelHistory') || '[]');
            history.unshift({ preview: text.substring(0, 45) + "...", score, date: new Date().toLocaleTimeString() });
            localStorage.setItem('sentinelHistory', JSON.stringify(history.slice(0, 5)));
            renderHistory();
        }

        window.renderHistory = function() {
            const history = JSON.parse(localStorage.getItem('sentinelHistory') || '[]');
            const list = document.getElementById('historyList');
            const empty = document.getElementById('emptyHistory');
            if (history.length === 0) { empty.style.display = 'block'; list.innerHTML = ''; return; }
            empty.style.display = 'none';
            list.innerHTML = history.map(item => `
                <div class="flex items-center justify-between p-4 bg-gray-50 rounded-xl border border-gray-100">
                    <div class="text-left"><p class="text-sm font-bold">${item.preview}</p><p class="text-xs text-gray-400">${item.date}</p></div>
                    <div class="font-black ${item.score > 70 ? 'text-red-500' : 'text-green-500'}">${item.score}% AI</div>
                </div>
            `).join('');
        };

        window.clearHistory = function() { localStorage.removeItem('sentinelHistory'); renderHistory(); };

        window.downloadReport = function() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            doc.setFontSize(22); doc.setTextColor(79, 70, 229);
            doc.text("AI Sentinel Report", 20, 20);
            doc.setFontSize(14); doc.setTextColor(0);
            doc.text(`Verdict: ${document.getElementById('verdict').innerText}`, 20, 40);
            doc.text(`Score: ${document.getElementById('score').innerText}`, 20, 50);
            const lines = doc.splitTextToSize(textArea.value.substring(0, 2000), 170);
            doc.setFontSize(10); doc.text(lines, 20, 70);
            doc.save("Report.pdf");
        };

        renderHistory();
    </script>
</body>
</html>
