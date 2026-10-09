<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Painel de Estudos</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
        }
    </script>
    <!-- FontAwesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body class="bg-slate-50 text-slate-800 dark:bg-slate-900 dark:text-slate-100 min-h-screen transition-colors duration-200">
    <div id="app" class="min-h-screen flex flex-col">
        <!-- Header -->
        <header class="bg-indigo-600 dark:bg-slate-800 text-white p-4 shadow-md flex justify-between items-center">
            <h1 class="text-xl font-bold flex items-center gap-2">
                <i class="fa-solid fa-graduation-cap"></i> Painel de Estudos
            </h1>
            <button id="themeToggle" class="p-2 rounded-lg hover:bg-indigo-700 dark:hover:bg-slate-700 transition">
                <i class="fa-solid fa-moon text-lg" id="themeIcon"></i>
            </button>
        </header>

        <!-- Conteúdo Principal -->
        <main class="flex-1 p-4 md:p-8 max-w-6xl w-full mx-auto grid grid-cols-1 md:grid-cols-3 gap-6">
            
            <!-- Sessão Pomodoro -->
            <section class="bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 flex flex-col items-center justify-between">
                <div class="w-full text-center">
                    <h2 class="text-lg font-semibold mb-2 text-slate-700 dark:text-slate-200 flex items-center justify-center gap-2">
                        <i class="fa-solid fa-clock text-indigo-500"></i> Temporizador
                    </h2>
                    <p id="timerStatus" class="text-xs text-slate-500 dark:text-slate-400 font-medium uppercase tracking-wider mb-4">Modo Foco</p>
                    
                    <div class="text-6xl font-extrabold text-indigo-600 dark:text-indigo-400 my-4 font-mono" id="timerDisplay">25:00</div>
                    
                    <div class="flex justify-center gap-3 mb-6">
                        <button id="startBtn" class="bg-indigo-600 hover:bg-indigo-700 text-white px-6 py-2.5 rounded-xl font-medium transition flex items-center gap-2 shadow-sm">
                            <i class="fa-solid fa-play"></i> Iniciar
                        </button>
                        <button id="pauseBtn" class="bg-amber-500 hover:bg-amber-600 text-white px-6 py-2.5 rounded-xl font-medium transition hidden flex items-center gap-2 shadow-sm">
                            <i class="fa-solid fa-pause"></i> Pausar
                        </button>
                        <button id="resetBtn" class="bg-slate-100 dark:bg-slate-700 hover:bg-slate-200 dark:hover:bg-slate-600 text-slate-600 dark:text-slate-300 px-4 py-2.5 rounded-xl transition">
                            <i class="fa-solid fa-rotate-left"></i>
                        </button>
                    </div>
                </div>

                <div class="flex gap-2 text-xs font-medium w-full justify-center">
                    <button id="modePomodoro" class="px-3 py-1.5 bg-indigo-100 text-indigo-700 dark:bg-indigo-900/60 dark:text-indigo-300 rounded-lg transition">Foco (25m)</button>
                    <button id="modeShort" class="px-3 py-1.5 bg-slate-100 text-slate-600 dark:bg-slate-700 dark:text-slate-300 rounded-lg transition">Pausa (5m)</button>
                    <button id="modeLong" class="px-3 py-1.5 bg-slate-100 text-slate-600 dark:bg-slate-700 dark:text-slate-300 rounded-lg transition">Pausa (15m)</button>
                </div>
            </section>

            <!-- Registro e Histórico -->
            <section class="md:col-span-2 bg-white dark:bg-slate-800 p-6 rounded-2xl shadow-sm border border-slate-200 dark:border-slate-700 flex flex-col justify-between">
                <div>
                    <h2 class="text-lg font-semibold mb-4 text-slate-700 dark:text-slate-200 flex items-center gap-2">
                        <i class="fa-solid fa-plus-circle text-indigo-500"></i> Registrar Estudo
                    </h2>
                    <form id="studyForm" class="grid grid-cols-1 sm:grid-cols-3 gap-3 mb-6">
                        <input type="text" id="subjectInput" placeholder="Matéria (ex: Física)" required class="p-3 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-800 dark:text-slate-100 text-sm">
                        <input type="text" id="topicInput" placeholder="Assunto (ex: Cinemática)" required class="p-3 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-800 dark:text-slate-100 text-sm">
                        <input type="number" id="minutesInput" placeholder="Tempo (min)" min="1" required class="p-3 bg-slate-50 dark:bg-slate-900 border border-slate-200 dark:border-slate-700 rounded-xl focus:outline-none focus:ring-2 focus:ring-indigo-500 text-slate-800 dark:text-slate-100 text-sm">
                        <button type="submit" class="sm:col-span-3 bg-indigo-600 hover:bg-indigo-700 text-white font-medium p-3 rounded-xl transition flex items-center justify-center gap-2 text-sm shadow-sm">
                            <i class="fa-solid fa-floppy-disk"></i> Salvar Sessão
                        </button>
                    </form>

                    <h3 class="text-md font-semibold mb-3 text-slate-700 dark:text-slate-200 flex items-center gap-2">
                        <i class="fa-solid fa-list-check text-indigo-500"></i> Histórico Recente
                    </h3>
                    <div id="logsList" class="space-y-2 max-h-52 overflow-y-auto pr-1">
                        <!-- Logs dinâmicos aparecem aqui -->
                    </div>
                </div>

                <!-- Botão de Limpar -->
                <div class="mt-4 pt-4 border-t border-slate-100 dark:border-slate-700/50 flex justify-end">
                    <button id="clearLogsBtn" class="text-xs text-rose-500 hover:text-rose-700 dark:hover:text-rose-400 flex items-center gap-1 transition">
                        <i class="fa-solid fa-trash-can"></i> Limpar histórico
                    </button>
                </div>
            </section>
        </main>
    </div>

    <!-- Script com todas as funções tratadas -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // --- TEMPORIZADOR POMODORO ---
            let timer = null;
            let currentModeTime = 25 * 60;
            let timeLeft = currentModeTime;
            let isRunning = false;

            const display = document.getElementById('timerDisplay');
            const statusText = document.getElementById('timerStatus');
            const startBtn = document.getElementById('startBtn');
            const pauseBtn = document.getElementById('pauseBtn');
            const resetBtn = document.getElementById('resetBtn');

            const modePomodoro = document.getElementById('modePomodoro');
            const modeShort = document.getElementById('modeShort');
            const modeLong = document.getElementById('modeLong');

            function updateDisplay() {
                const minutes = Math.floor(timeLeft / 60);
                const seconds = timeLeft % 60;
                display.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            }

            function setMode(seconds, title, activeBtn) {
                clearInterval(timer);
                isRunning = false;
                currentModeTime = seconds;
                timeLeft = seconds;
                statusText.textContent = title;
                updateDisplay();
                
                pauseBtn.classList.add('hidden');
                startBtn.classList.remove('hidden');

                [modePomodoro, modeShort, modeLong].forEach(btn => {
                    btn.className = "px-3 py-1.5 bg-slate-100 text-slate-600 dark:bg-slate-700 dark:text-slate-300 rounded-lg transition";
                });
                activeBtn.className = "px-3 py-1.5 bg-indigo-100 text-indigo-700 dark:bg-indigo-900/60 dark:text-indigo-300 rounded-lg transition font-semibold";
            }

            modePomodoro.addEventListener('click', () => setMode(25 * 60, 'Modo Foco', modePomodoro));
            modeShort.addEventListener('click', () => setMode(5 * 60, 'Pausa Curta', modeShort));
            modeLong.addEventListener('click', () => setMode(15 * 60, 'Pausa Longa', modeLong));

            startBtn.addEventListener('click', () => {
                if (!isRunning) {
                    isRunning = true;
                    startBtn.classList.add('hidden');
                    pauseBtn.classList.remove('hidden');
                    
                    timer = setInterval(() => {
                        if (timeLeft > 0) {
                            timeLeft--;
                            updateDisplay();
                        } else {
                            clearInterval(timer);
                            isRunning = false;
                            alert('Tempo concluído!');
                            startBtn.classList.remove('hidden');
                            pauseBtn.classList.add('hidden');
                        }
                    }, 1000);
                }
            });

            pauseBtn.addEventListener('click', () => {
                clearInterval(timer);
                isRunning = false;
                pauseBtn.classList.add('hidden');
                startBtn.classList.remove('hidden');
            });

            resetBtn.addEventListener('click', () => {
                clearInterval(timer);
                isRunning = false;
                timeLeft = currentModeTime;
                updateDisplay();
                pauseBtn.classList.add('hidden');
                startBtn.classList.remove('hidden');
            });

            // --- TEMA ESCURO / CLARO ---
            const themeToggle = document.getElementById('themeToggle');
            const themeIcon = document.getElementById('themeIcon');

            themeToggle.addEventListener('click', () => {
                document.documentElement.classList.toggle('dark');
                const isDark = document.documentElement.classList.contains('dark');
                themeIcon.className = isDark ? 'fa-solid fa-sun text-amber-400' : 'fa-solid fa-moon text-lg';
            });

            // --- REGISTRO DE ESTUDOS E LOCALSTORAGE ---
            const studyForm = document.getElementById('studyForm');
            const logsList = document.getElementById('logsList');
            const clearLogsBtn = document.getElementById('clearLogsBtn');

            function loadLogs() {
                const logs = JSON.parse(localStorage.getItem('studyLogs') || '[]');
                logsList.innerHTML = '';
                
                if (logs.length === 0) {
                    logsList.innerHTML = '<p class="text-sm text-slate-400 italic py-2">Nenhum registro encontrado.</p>';
                    return;
                }

                logs.forEach((log) => {
                    const item = document.createElement('div');
                    item.className = 'p-3 bg-slate-50 dark:bg-slate-900 rounded-xl flex justify-between items-center text-sm border border-slate-100 dark:border-slate-700/50';
                    item.innerHTML = `
                        <div>
                            <span class="font-semibold text-indigo-600 dark:text-indigo-400">${escapeHtml(log.subject)}</span> 
                            <span class="text-slate-400 dark:text-slate-500">•</span> 
                            <span class="text-slate-700 dark:text-slate-300">${escapeHtml(log.topic)}</span>
                        </div>
                        <span class="bg-indigo-50 dark:bg-indigo-950/60 text-indigo-600 dark:text-indigo-300 px-2.5 py-1 rounded-lg text-xs font-semibold">${log.minutes} min</span>
                    `;
                    logsList.appendChild(item);
                });
            }

            function escapeHtml(text) {
                const div = document.createElement('div');
                div.innerText = text;
                return div.innerHTML;
            }

            studyForm.addEventListener('submit', (e) => {
                e.preventDefault();
                const subject = document.getElementById('subjectInput').value.trim();
                const topic = document.getElementById('topicInput').value.trim();
                const minutes = document.getElementById('minutesInput').value.trim();

                if (!subject || !topic || !minutes) return;

                const logs = JSON.parse(localStorage.getItem('studyLogs') || '[]');
                logs.unshift({ subject, topic, minutes, date: new Date().toLocaleDateString() });
                localStorage.setItem('studyLogs', JSON.stringify(logs));

                studyForm.reset();
                loadLogs();
            });

            clearLogsBtn.addEventListener('click', () => {
                if (confirm('Deseja realmente apagar todo o seu histórico de estudos?')) {
                    localStorage.removeItem('studyLogs');
                    loadLogs();
                }
            });

            // Inicializar a exibição
            updateDisplay();
            loadLogs();
        });
    </script>
</body>
</html>
