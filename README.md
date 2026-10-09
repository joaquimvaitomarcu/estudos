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
            --bg-body: #0f172a;
            --bg-card: #1e293b;
            --text-main: #f8fafc;
            --text-sub: #94a3b8;
            --border-color: #334155;
            --input-bg: #0f172a;
        }
        .light-mode {
            --bg-body: #f8fafc;
            --bg-card: #ffffff;
            --text-main: #0f172a;
            --text-sub: #64748b;
            --border-color: #e2e8f0;
            --input-bg: #f1f5f9;
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
            border-radius: 1.25rem;
        }
        .input-field {
            background-color: var(--input-bg);
            color: var(--text-main);
            border: 1px solid var(--border-color);
            border-radius: 0.875rem;
        }
        .subtext {
            color: var(--text-sub);
        }
    </style>
</head>
<body class="min-h-screen pb-10">

    <!-- Cabeçalho limpo e sem travar a tela -->
    <header class="bg-indigo-600 text-white px-5 py-4 shadow-md flex justify-between items-center rounded-b-2xl mb-5">
        <h1 class="text-base font-bold flex items-center gap-2">
            <i class="fa-solid fa-graduation-cap text-lg"></i> Meu Painel de Estudos
        </h1>
        <button id="themeToggle" class="p-2 rounded-xl bg-indigo-700/60 hover:bg-indigo-700 transition active:scale-95">
            <i class="fa-solid fa-sun text-amber-300 text-base" id="themeIcon"></i>
        </button>
    </header>

    <main class="max-w-md mx-auto px-4 space-y-4">

        <!-- 1. ESTATÍSTICAS -->
        <section class="card p-4 shadow-sm">
            <h2 class="text-xs font-semibold subtext uppercase tracking-wider mb-3 flex items-center gap-2">
                <i class="fa-solid fa-chart-line text-indigo-400"></i> Progresso
            </h2>
            <div class="grid grid-cols-2 gap-3">
                <div class="p-3 rounded-2xl bg-indigo-500/10 text-center border border-indigo-500/20">
                    <span class="block text-2xl font-bold text-indigo-400" id="statHours">0h</span>
                    <span class="text-xs subtext">Tempo Estudado</span>
                </div>
                <div class="p-3 rounded-2xl bg-amber-500/10 text-center border border-amber-500/20">
                    <span class="block text-2xl font-bold text-amber-400" id="statStreak">0 🔥</span>
                    <span class="text-xs subtext">Sequência (Dias)</span>
                </div>
            </div>
        </section>

        <!-- 2. POMODORO -->
        <section class="card p-5 shadow-sm text-center">
            <h2 class="text-xs font-semibold subtext uppercase tracking-wider mb-1 flex items-center justify-center gap-2">
                <i class="fa-solid fa-clock text-indigo-400"></i> Cronômetro Pomodoro
            </h2>
            <p id="timerStatus" class="text-xs font-semibold text-indigo-400 mb-2">MODO FOCO</p>
            
            <div class="text-5xl font-extrabold my-3 font-mono text-indigo-400 tracking-tight" id="timerDisplay">25:00</div>

            <div class="flex justify-center gap-2 mb-4">
                <button id="startBtn" class="bg-indigo-600 hover:bg-indigo-700 text-white font-semibold px-6 py-2.5 rounded-xl transition flex items-center gap-2 shadow-sm active:scale-95">
                    <i class="fa-solid fa-play text-xs"></i> Iniciar
                </button>
                <button id="pauseBtn" class="bg-amber-500 hover:bg-amber-600 text-white font-semibold px-6 py-2.5 rounded-xl transition hidden flex items-center gap-2 shadow-sm active:scale-95">
                    <i class="fa-solid fa-pause text-xs"></i> Pausar
                </button>
                <button id="resetBtn" class="input-field px-4 py-2.5 rounded-xl transition active:scale-95">
                    <i class="fa-solid fa-rotate-left text-xs"></i>
                </button>
            </div>

            <div class="grid grid-cols-3 gap-2 text-xs">
                <button id="modePomodoro" class="py-2 bg-indigo-600 text-white font-semibold rounded-xl">Foco (25m)</button>
                <button id="modeShort" class="py-2 input-field rounded-xl font-medium">Pausa (5m)</button>
                <button id="modeLong" class="py-2 input-field rounded-xl font-medium">Pausa (15m)</button>
            </div>
        </section>

        <!-- 3. REGISTRO DE SESSÃO -->
        <section class="card p-4 shadow-sm">
            <h2 class="text-xs font-semibold subtext uppercase tracking-wider mb-3 flex items-center gap-2">
                <i class="fa-solid fa-plus-circle text-indigo-400"></i> Registrar Estudo
            </h2>
            <form id="studyForm" class="space-y-2.5">
                <input type="text" id="subjectInput" placeholder="Matéria (ex: Física)" required class="w-full p-3 input-field text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500">
                <input type="text" id="topicInput" placeholder="Assunto (ex: Leis de Newton)" required class="w-full p-3 input-field text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500">
                <input type="number" id="minutesInput" placeholder="Tempo dedicado (minutos)" min="1" required class="w-full p-3 input-field text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500">
                <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-semibold p-3 rounded-xl transition flex justify-center items-center gap-2 text-sm shadow-sm active:scale-95">
                    <i class="fa-solid fa-floppy-disk"></i> Salvar Sessão
                </button>
            </form>
        </section>

        <!-- 4. QUADRO DE TAREFAS -->
        <section class="card p-4 shadow-sm">
            <h2 class="text-xs font-semibold subtext uppercase tracking-wider mb-3 flex items-center gap-2">
                <i class="fa-solid fa-list-check text-indigo-400"></i> Tópicos a Estudar
            </h2>
            <form id="taskForm" class="flex gap-2 mb-3">
                <input type="text" id="taskInput" placeholder="Nova tarefa ou tópico..." required class="flex-1 p-2.5 input-field text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500">
                <button type="submit" class="bg-indigo-600 hover:bg-indigo-700 text-white px-4 rounded-xl text-sm font-semibold transition active:scale-95">
                    <i class="fa-solid fa-plus"></i>
                </button>
            </form>
            <div id="taskList" class="space-y-2 max-h-48 overflow-y-auto">
                <!-- Tarefas entram aqui -->
            </div>
        </section>

        <!-- 5. HISTÓRICO RECENTE -->
        <section class="card p-4 shadow-sm">
            <div class="flex justify-between items-center mb-3">
                <h2 class="text-xs font-semibold subtext uppercase tracking-wider flex items-center gap-2">
                    <i class="fa-solid fa-history text-indigo-400"></i> Histórico Recente
                </h2>
                <button id="clearLogsBtn" class="text-xs text-rose-400 hover:underline">Limpar</button>
            </div>
            <div id="logsList" class="space-y-2 max-h-52 overflow-y-auto">
                <!-- Histórico entra aqui -->
            </div>
        </section>

    </main>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // --- TEMA ESCURO / CLARO ---
            const themeToggle = document.getElementById('themeToggle');
            const themeIcon = document.getElementById('themeIcon');
            
            if (localStorage.getItem('theme') === 'light') {
                document.body.classList.add('light-mode');
                themeIcon.className = 'fa-solid fa-moon text-slate-100 text-base';
            }

            themeToggle.addEventListener('click', () => {
                document.body.classList.toggle('light-mode');
                const isLight = document.body.classList.contains('light-mode');
                localStorage.setItem('theme', isLight ? 'light' : 'dark');
                themeIcon.className = isLight ? 'fa-solid fa-moon text-slate-100 text-base' : 'fa-solid fa-sun text-amber-300 text-base';
            });

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
                statusText.textContent = title.toUpperCase();
                updateDisplay();
                
                pauseBtn.classList.add('hidden');
                startBtn.classList.remove('hidden');

                [modePomodoro, modeShort, modeLong].forEach(btn => {
                    btn.className = "py-2 input-field rounded-xl font-medium";
                });
                activeBtn.className = "py-2 bg-indigo-600 text-white font-semibold rounded-xl";
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

            // --- REGISTRO DE SESSÕES & HISTÓRICO ---
            const studyForm = document.getElementById('studyForm');
            const logsList = document.getElementById('logsList');
            const clearLogsBtn = document.getElementById('clearLogsBtn');

            function loadData() {
                const logs = JSON.parse(localStorage.getItem('studyLogs') || '[]');
                logsList.innerHTML = '';
                
                let totalMin = 0;
                logs.forEach((log) => {
                    totalMin += parseInt(log.minutes) || 0;
                    const item = document.createElement('div');
                    item.className = 'p-3 rounded-xl input-field flex justify-between items-center text-xs';
                    item.innerHTML = `
                        <div>
                            <strong class="text-indigo-400 block text-sm">${escapeHtml(log.subject)}</strong>
                            <span class="subtext">${escapeHtml(log.topic)}</span>
                        </div>
                        <span class="font-bold px-2.5 py-1 rounded-lg bg-indigo-500/10 text-indigo-400">${log.minutes} min</span>
                    `;
                    logsList.appendChild(item);
                });

                if (logs.length === 0) {
                    logsList.innerHTML = '<p class="text-xs subtext italic">Nenhuma sessão registrada.</p>';
                }

                document.getElementById('statHours').textContent = `${(totalMin / 60).toFixed(1)}h`;
                document.getElementById('statStreak').textContent = `${logs.length > 0 ? 1 : 0} 🔥`;
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

                const logs = JSON.parse(localStorage.getItem('studyLogs') || '[]');
                logs.unshift({ subject, topic, minutes, date: new Date().toLocaleDateString() });
                localStorage.setItem('studyLogs', JSON.stringify(logs));

                studyForm.reset();
                loadData();
            });

            clearLogsBtn.addEventListener('click', () => {
                if (confirm('Apagar todo o histórico?')) {
                    localStorage.removeItem('studyLogs');
                    loadData();
                }
            });

            // --- TAREFAS (TO-DO) ---
            const taskForm = document.getElementById('taskForm');
            const taskInput = document.getElementById('taskInput');
            const taskList = document.getElementById('taskList');

            function loadTasks() {
                const tasks = JSON.parse(localStorage.getItem('studyTasks') || '[]');
                taskList.innerHTML = '';

                tasks.forEach((task, index) => {
                    const item = document.createElement('div');
                    item.className = 'p-2.5 rounded-xl input-field flex items-center justify-between text-xs';
                    item.innerHTML = `
                        <span class="${task.done ? 'line-through opacity-50' : ''}">${escapeHtml(task.title)}</span>
                        <div class="flex gap-2">
                            <button onclick="toggleTask(${index})" class="text-emerald-400 p-1"><i class="fa-solid fa-check"></i></button>
                            <button onclick="deleteTask(${index})" class="text-rose-400 p-1"><i class="fa-solid fa-trash"></i></button>
                        </div>
                    `;
                    taskList.appendChild(item);
                });

                if (tasks.length === 0) {
                    taskList.innerHTML = '<p class="text-xs subtext italic">Nenhuma tarefa pendente.</p>';
                }
            }

            taskForm.addEventListener('submit', (e) => {
                e.preventDefault();
                const title = taskInput.value.trim();
                if (!title) return;

                const tasks = JSON.parse(localStorage.getItem('studyTasks') || '[]');
                tasks.push({ title, done: false });
                localStorage.setItem('studyTasks', JSON.stringify(tasks));

                taskInput.value = '';
                loadTasks();
            });

            window.toggleTask = (index) => {
                const tasks = JSON.parse(localStorage.getItem('studyTasks') || '[]');
                tasks[index].done = !tasks[index].done;
                localStorage.setItem('studyTasks', JSON.stringify(tasks));
                loadTasks();
            };

            window.deleteTask = (index) => {
                const tasks = JSON.parse(localStorage.getItem('studyTasks') || '[]');
                tasks.splice(index, 1);
                localStorage.setItem('studyTasks', JSON.stringify(tasks));
                loadTasks();
            };

            // Inicialização
            updateDisplay();
            loadData();
            loadTasks();
        });
    </script>
</body>
</html>
