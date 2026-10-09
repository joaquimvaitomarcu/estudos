<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Painel de Estudos</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --bg-body: #0d110e;
            --bg-card: #182017;
            --text-main: #f1f5f2;
            --text-sub: #8a9a86;
            --border-color: #2a3828;
            --input-bg: #111710;
            --army-green: #4a5d3f;
            --army-accent: #6b875b;
        }
        .light-mode {
            --bg-body: #f4f6f4;
            --bg-card: #ffffff;
            --text-main: #1b2419;
            --text-sub: #52634d;
            --border-color: #d2ded0;
            --input-bg: #e9eee8;
            --army-green: #3b4b32;
            --army-accent: #4a5d3f;
        }
        body {
            background-color: var(--bg-body);
            color: var(--text-main);
            transition: background-color 0.2s, color 0.2s;
            font-family: system-ui, -apple-system, sans-serif;
        }
        .card {
            background-color: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 1.75rem;
        }
        .input-field {
            background-color: var(--input-bg);
            color: var(--text-main);
            border: 1px solid var(--border-color);
            border-radius: 1.25rem;
        }
        .subtext {
            color: var(--text-sub);
        }
        .btn-army {
            background-color: var(--army-green);
            color: #ffffff;
        }
        .btn-army:hover {
            background-color: var(--army-accent);
        }
    </style>
</head>
<body class="min-h-screen pb-10">

    <!-- Header Flutuante -->
    <div class="px-4 pt-4 max-w-md mx-auto">
        <header class="btn-army text-white px-5 py-4 shadow-lg flex justify-between items-center rounded-3xl">
            <h1 class="text-base font-bold flex items-center gap-2">
                <i class="fa-solid fa-graduation-cap text-xl"></i> Meu Painel de Estudos
            </h1>
            <button id="themeToggle" type="button" class="p-2.5 rounded-2xl bg-black/30 hover:bg-black/40 transition active:scale-95">
                <i class="fa-solid fa-sun text-amber-300 text-base" id="themeIcon"></i>
            </button>
        </header>
    </div>

    <main class="max-w-md mx-auto p-4 space-y-4">

        <!-- ESTATÍSTICAS E META -->
        <section class="card p-5 shadow-sm space-y-4">
            <h2 class="text-xs font-semibold subtext uppercase tracking-wider flex items-center gap-2">
                <i class="fa-solid fa-chart-line text-emerald-500"></i> Progresso Geral
            </h2>
            
            <div class="grid grid-cols-2 gap-3">
                <div class="p-3.5 rounded-2xl bg-emerald-500/10 text-center border border-emerald-500/20">
                    <span class="block text-2xl font-bold text-emerald-400" id="statHours">0h</span>
                    <span class="text-xs subtext font-medium">Tempo Estudado</span>
                </div>
                <div class="p-3.5 rounded-2xl bg-amber-500/10 text-center border border-amber-500/20">
                    <span class="block text-2xl font-bold text-amber-400" id="statStreak">0 🔥</span>
                    <span class="text-xs subtext font-medium">Sequência (Dias)</span>
                </div>
            </div>

            <!-- Meta de Tarefas Concluídas -->
            <div class="p-4 rounded-2xl bg-black/20 border border-white/5 space-y-2">
                <div class="flex justify-between items-center text-xs font-semibold">
                    <span class="subtext flex items-center gap-1.5">
                        <i class="fa-solid fa-circle-check text-emerald-400"></i> Meta de Tópicos
                    </span>
                    <span class="text-emerald-400 text-sm font-bold" id="progressPercent">0%</span>
                </div>
                <div class="w-full bg-black/40 h-2.5 rounded-full overflow-hidden p-0.5 border border-white/5">
                    <div id="progressBar" class="bg-gradient-to-r from-emerald-600 to-emerald-400 h-full rounded-full transition-all duration-500 w-0"></div>
                </div>
            </div>
        </section>

        <!-- PORCENTAGEM DE ESTUDO POR MATÉRIA -->
        <section class="card p-5 shadow-sm space-y-3">
            <h2 class="text-xs font-semibold subtext uppercase tracking-wider flex items-center gap-2">
                <i class="fa-solid fa-chart-pie text-emerald-500"></i> Divisão por Matéria
            </h2>
            <div id="subjectPercentages" class="space-y-3">
                <p class="text-xs subtext italic">Registre sessões para ver a porcentagem por matéria.</p>
            </div>
        </section>

        <!-- CRONÔMETRO DE ESTUDO -->
        <section class="card p-5 shadow-sm text-center space-y-3">
            <h2 class="text-xs font-semibold subtext uppercase tracking-wider flex items-center justify-center gap-2">
                <i class="fa-solid fa-stopwatch text-emerald-500"></i> Cronômetro de Estudo
            </h2>

            <div class="space-y-2 text-left">
                <input type="text" id="timerSubject" placeholder="Matéria (ex: Matemática)" class="w-full p-3 input-field text-xs focus:outline-none focus:ring-2 focus:ring-emerald-500">
                <input type="text" id="timerTopic" placeholder="Assunto (ex: Trigonometria)" class="w-full p-3 input-field text-xs focus:outline-none focus:ring-2 focus:ring-emerald-500">
            </div>

            <p id="timerStatus" class="text-xs font-semibold text-emerald-400 pt-1">MODO FOCO</p>
            
            <div class="text-5xl font-extrabold my-2 font-mono text-emerald-400 tracking-tight" id="timerDisplay">25:00</div>

            <div class="flex justify-center gap-2 mb-2">
                <button id="startBtn" type="button" class="btn-army font-semibold px-5 py-3 rounded-2xl transition flex items-center gap-2 shadow-md active:scale-95 text-xs">
                    <i class="fa-solid fa-play"></i> Iniciar
                </button>
                <button id="pauseBtn" type="button" class="bg-amber-600 hover:bg-amber-700 text-white font-semibold px-5 py-3 rounded-2xl transition hidden flex items-center gap-2 shadow-md active:scale-95 text-xs">
                    <i class="fa-solid fa-pause"></i> Pausar
                </button>
                <button id="finishBtn" type="button" class="bg-emerald-600 hover:bg-emerald-700 text-white font-semibold px-4 py-3 rounded-2xl transition flex items-center gap-1.5 shadow-md active:scale-95 text-xs">
                    <i class="fa-solid fa-check"></i> Salvar
                </button>
                <button id="resetBtn" type="button" class="input-field px-4 py-3 rounded-2xl transition active:scale-95 text-xs">
                    <i class="fa-solid fa-rotate-left"></i>
                </button>
            </div>

            <div class="grid grid-cols-3 gap-2 text-xs pt-1">
                <button id="modePomodoro" type="button" class="py-2.5 btn-army font-semibold rounded-2xl">Foco (25m)</button>
                <button id="modeShort" type="button" class="py-2.5 input-field rounded-2xl font-medium">Pausa (5m)</button>
                <button id="modeLong" type="button" class="py-2.5 input-field rounded-2xl font-medium">Pausa (15m)</button>
            </div>
        </section>

        <!-- REGISTRO MANUAL DE SESSÃO -->
        <section class="card p-5 shadow-sm">
            <h2 class="text-xs font-semibold subtext uppercase tracking-wider mb-3 flex items-center gap-2">
                <i class="fa-solid fa-plus-circle text-emerald-500"></i> Registro Manual
            </h2>
            <form id="studyForm" class="space-y-3">
                <input type="text" id="subjectInput" placeholder="Matéria (ex: História)" required class="w-full p-3.5 input-field text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                <input type="text" id="topicInput" placeholder="Assunto (ex: Brasil Colônia)" required class="w-full p-3.5 input-field text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                <input type="number" id="minutesInput" placeholder="Tempo dedicado (minutos)" min="1" required class="w-full p-3.5 input-field text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                <button type="submit" class="w-full btn-army font-semibold p-3.5 rounded-2xl transition flex justify-center items-center gap-2 text-sm shadow-md active:scale-95">
                    <i class="fa-solid fa-floppy-disk"></i> Salvar Sessão
                </button>
            </form>
        </section>

        <!-- QUADRO DE TAREFAS -->
        <section class="card p-5 shadow-sm">
            <h2 class="text-xs font-semibold subtext uppercase tracking-wider mb-3 flex items-center gap-2">
                <i class="fa-solid fa-list-check text-emerald-500"></i> Tópicos a Estudar
            </h2>
            <form id="taskForm" class="flex items-center gap-2 mb-3 w-full">
                <input type="text" id="taskInput" placeholder="Novo tópico..." required class="flex-1 min-w-0 p-3 input-field text-sm focus:outline-none focus:ring-2 focus:ring-emerald-500">
                <button type="submit" class="btn-army px-4 py-3 rounded-2xl text-sm font-semibold transition active:scale-95 flex-shrink-0">
                    <i class="fa-solid fa-plus"></i>
                </button>
            </form>
            <div id="taskList" class="space-y-2 max-h-48 overflow-y-auto">
                <p class="text-xs subtext italic">Nenhuma tarefa pendente.</p>
            </div>
        </section>

        <!-- HISTÓRICO RECENTE -->
        <section class="card p-5 shadow-sm">
            <div class="flex justify-between items-center mb-3">
                <h2 class="text-xs font-semibold subtext uppercase tracking-wider flex items-center gap-2">
                    <i class="fa-solid fa-history text-emerald-500"></i> Histórico Recente
                </h2>
                <button id="clearLogsBtn" type="button" class="text-xs text-rose-400 hover:underline">Limpar</button>
            </div>
            <div id="logsList" class="space-y-2 max-h-52 overflow-y-auto">
                <p class="text-xs subtext italic">Nenhuma sessão registrada.</p>
            </div>
        </section>

    </main>

    <script>
        (function() {
            // --- TEMA ESCURO / CLARO ---
            const themeToggle = document.getElementById('themeToggle');
            const themeIcon = document.getElementById('themeIcon');
            
            if (localStorage.getItem('theme') === 'light') {
                document.body.classList.add('light-mode');
                if (themeIcon) themeIcon.className = 'fa-solid fa-moon text-slate-100 text-base';
            }

            if (themeToggle) {
                themeToggle.addEventListener('click', () => {
                    document.body.classList.toggle('light-mode');
                    const isLight = document.body.classList.contains('light-mode');
                    localStorage.setItem('theme', isLight ? 'light' : 'dark');
                    if (themeIcon) {
                        themeIcon.className = isLight ? 'fa-solid fa-moon text-slate-100 text-base' : 'fa-solid fa-sun text-amber-300 text-base';
                    }
                });
            }

            // --- CRONÔMETRO DE ESTUDO ---
            let timer = null;
            let currentModeTime = 25 * 60;
            let timeLeft = currentModeTime;
            let elapsedTimeSeconds = 0;
            let isRunning = false;

            const display = document.getElementById('timerDisplay');
            const statusText = document.getElementById('timerStatus');
            const startBtn = document.getElementById('startBtn');
            const pauseBtn = document.getElementById('pauseBtn');
            const resetBtn = document.getElementById('resetBtn');
            const finishBtn = document.getElementById('finishBtn');

            const timerSubject = document.getElementById('timerSubject');
            const timerTopic = document.getElementById('timerTopic');

            const modePomodoro = document.getElementById('modePomodoro');
            const modeShort = document.getElementById('modeShort');
            const modeLong = document.getElementById('modeLong');

            function updateDisplay() {
                if (!display) return;
                const minutes = Math.floor(timeLeft / 60);
                const seconds = timeLeft % 60;
                display.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            }

            function setMode(seconds, title, activeBtn) {
                clearInterval(timer);
                isRunning = false;
                currentModeTime = seconds;
                timeLeft = seconds;
                elapsedTimeSeconds = 0;
                if (statusText) statusText.textContent = title.toUpperCase();
                updateDisplay();
                
                if (pauseBtn) pauseBtn.classList.add('hidden');
                if (startBtn) startBtn.classList.remove('hidden');

                [modePomodoro, modeShort, modeLong].forEach(btn => {
                    if (btn) btn.className = "py-2.5 input-field rounded-2xl font-medium";
                });
                if (activeBtn) activeBtn.className = "py-2.5 btn-army font-semibold rounded-2xl";
            }

            if (modePomodoro) modePomodoro.addEventListener('click', () => setMode(25 * 60, 'Modo Foco', modePomodoro));
            if (modeShort) modeShort.addEventListener('click', () => setMode(5 * 60, 'Pausa Curta', modeShort));
            if (modeLong) modeLong.addEventListener('click', () => setMode(15 * 60, 'Pausa Longa', modeLong));

            if (startBtn) {
                startBtn.addEventListener('click', () => {
                    if (!isRunning) {
                        isRunning = true;
                        startBtn.classList.add('hidden');
                        if (pauseBtn) pauseBtn.classList.remove('hidden');
                        
                        timer = setInterval(() => {
                            if (timeLeft > 0) {
                                timeLeft--;
                                elapsedTimeSeconds++;
                                updateDisplay();
                            } else {
                                clearInterval(timer);
                                isRunning = false;
                                alert('Tempo concluído!');
                                saveTimerSession();
                                startBtn.classList.remove('hidden');
                                if (pauseBtn) pauseBtn.classList.add('hidden');
                            }
                        }, 1000);
                    }
                });
            }

            if (pauseBtn) {
                pauseBtn.addEventListener('click', () => {
                    clearInterval(timer);
                    isRunning = false;
                    pauseBtn.classList.add('hidden');
                    if (startBtn) startBtn.classList.remove('hidden');
                });
            }

            if (resetBtn) {
                resetBtn.addEventListener('click', () => {
                    clearInterval(timer);
                    isRunning = false;
                    timeLeft = currentModeTime;
                    elapsedTimeSeconds = 0;
                    updateDisplay();
                    if (pauseBtn) pauseBtn.classList.add('hidden');
                    if (startBtn) startBtn.classList.remove('hidden');
                });
            }

            if (finishBtn) {
                finishBtn.addEventListener('click', () => {
                    if (elapsedTimeSeconds < 10) {
                        alert('Estude ao menos alguns segundos para salvar a sessão!');
                        return;
                    }
                    saveTimerSession();
                });
            }

            function saveTimerSession() {
                const subject = (timerSubject && timerSubject.value.trim()) ? timerSubject.value.trim() : 'Estudo Geral';
                const topic = (timerTopic && timerTopic.value.trim()) ? timerTopic.value.trim() : 'Sessão com Cronômetro';
                const minutes = Math.max(1, Math.round(elapsedTimeSeconds / 60));

                saveStudyLog(subject, topic, minutes);

                clearInterval(timer);
                isRunning = false;
                timeLeft = currentModeTime;
                elapsedTimeSeconds = 0;
                updateDisplay();
                if (pauseBtn) pauseBtn.classList.add('hidden');
                if (startBtn) startBtn.classList.remove('hidden');

                if (timerSubject) timerSubject.value = '';
                if (timerTopic) timerTopic.value = '';
            }

            // --- REGISTRO DE DADOS E NAVEGAÇÃO ---
            const studyForm = document.getElementById('studyForm');
            const logsList = document.getElementById('logsList');
            const subjectPercentages = document.getElementById('subjectPercentages');
            const clearLogsBtn = document.getElementById('clearLogsBtn');

            function saveStudyLog(subject, topic, minutes) {
                const logs = JSON.parse(localStorage.getItem('studyLogs') || '[]');
                logs.unshift({ subject, topic, minutes, date: new Date().toLocaleDateString() });
                localStorage.setItem('studyLogs', JSON.stringify(logs));
                loadData();
            }

            function loadData() {
                const logs = JSON.parse(localStorage.getItem('studyLogs') || '[]');
                if (!logsList) return;
                logsList.innerHTML = '';
                
                let totalMin = 0;
                const subjectTotals = {};

                logs.forEach((log) => {
                    const min = parseInt(log.minutes) || 0;
                    totalMin += min;

                    const subjKey = log.subject.trim().toLowerCase();
                    const subjDisplayName = log.subject.trim();

                    if (!subjectTotals[subjKey]) {
                        subjectTotals[subjKey] = { name: subjDisplayName, minutes: 0 };
                    }
                    subjectTotals[subjKey].minutes += min;

                    const item = document.createElement('div');
                    item.className = 'p-3.5 rounded-2xl input-field flex justify-between items-center text-xs';
                    item.innerHTML = `
                        <div>
                            <strong class="text-emerald-400 block text-sm">${escapeHtml(log.subject)}</strong>
                            <span class="subtext">${escapeHtml(log.topic)}</span>
                        </div>
                        <span class="font-bold px-3 py-1 rounded-xl bg-emerald-500/10 text-emerald-400">${log.minutes} min</span>
                    `;
                    logsList.appendChild(item);
                });

                if (logs.length === 0) {
                    logsList.innerHTML = '<p class="text-xs subtext italic">Nenhuma sessão registrada.</p>';
                }

                const statHours = document.getElementById('statHours');
                const statStreak = document.getElementById('statStreak');
                if (statHours) statHours.textContent = `${(totalMin / 60).toFixed(1)}h`;
                if (statStreak) statStreak.textContent = `${logs.length > 0 ? 1 : 0} 🔥`;

                renderSubjectPercentages(subjectTotals, totalMin);
            }

            functio
