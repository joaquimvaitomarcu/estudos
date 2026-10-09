# estudos
serve para organizar seus estudos
```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Painel de Estudos & Tracker</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        brand: {
                            50: '#f0f7ff',
                            100: '#e0effe',
                            500: '#3b82f6',
                            600: '#2563eb',
                            700: '#1d4ed8',
                        }
                    }
                }
            }
        }
    </script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: transparent;
        }
        ::-webkit-scrollbar-thumb {
            background: rgba(156, 163, 175, 0.4);
            border-radius: 3px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: rgba(156, 163, 175, 0.7);
        }
    </style>
</head>
<body class="bg-gray-50 dark:bg-gray-900 text-gray-800 dark:text-gray-100 min-h-screen transition-colors duration-200">

    <!-- Navigation / Header -->
    <header class="bg-white dark:bg-gray-800 border-b border-gray-200 dark:border-gray-700 sticky top-0 z-30">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-16">
                <!-- Logo & Title -->
                <div class="flex items-center space-x-3">
                    <div class="p-2 bg-blue-600 rounded-lg text-white">
                        <i class="fa-solid fa-graduation-cap text-xl"></i>
                    </div>
                    <div>
                        <h1 class="text-lg font-bold text-gray-900 dark:text-white leading-tight">EstudoFlow</h1>
                        <p class="text-xs text-gray-500 dark:text-gray-400">Seu Organizador Pessoal de Estudos</p>
                    </div>
                </div>

                <!-- Theme Toggle & Stats Quick Glance -->
                <div class="flex items-center space-x-3 sm:space-x-4">
                    <div class="hidden sm:flex items-center space-x-2 bg-orange-50 dark:bg-orange-950/40 text-orange-600 dark:text-orange-400 px-3 py-1.5 rounded-full text-xs font-semibold border border-orange-200 dark:border-orange-800/50">
                        <i class="fa-solid fa-fire text-orange-500"></i>
                        <span id="streak-header-count">0 dias seguidos</span>
                    </div>

                    <button id="theme-toggle-btn" class="p-2 text-gray-500 hover:text-gray-700 dark:text-gray-400 dark:hover:text-gray-200 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-700 transition">
                        <i id="theme-toggle-dark-icon" class="fa-solid fa-moon text-lg hidden"></i>
                        <i id="theme-toggle-light-icon" class="fa-solid fa-sun text-lg text-yellow-400 hidden"></i>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content Container -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 space-y-8">

        <!-- SECTION 1: Top Dashboard Metrics -->
        <section class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
            <!-- Total Hours Card -->
            <div class="bg-white dark:bg-gray-800 p-5 rounded-xl border border-gray-200 dark:border-gray-700 shadow-sm flex items-center justify-between">
                <div>
                    <p class="text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Horas Estudadas</p>
                    <h3 id="stat-total-hours" class="text-2xl font-bold mt-1 text-gray-900 dark:text-white">0,0 h</h3>
                </div>
                <div class="p-3 bg-blue-100 dark:bg-blue-900/40 text-blue-600 dark:text-blue-400 rounded-lg">
                    <i class="fa-solid fa-clock text-xl"></i>
                </div>
            </div>

            <!-- Total Sessions Card -->
            <div class="bg-white dark:bg-gray-800 p-5 rounded-xl border border-gray-200 dark:border-gray-700 shadow-sm flex items-center justify-between">
                <div>
                    <p class="text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Sessões Concluídas</p>
                    <h3 id="stat-total-sessions" class="text-2xl font-bold mt-1 text-gray-900 dark:text-white">0</h3>
                </div>
                <div class="p-3 bg-emerald-100 dark:bg-emerald-900/40 text-emerald-600 dark:text-emerald-400 rounded-lg">
                    <i class="fa-solid fa-circle-check text-xl"></i>
                </div>
            </div>

            <!-- Streak Card -->
            <div class="bg-white dark:bg-gray-800 p-5 rounded-xl border border-gray-200 dark:border-gray-700 shadow-sm flex items-center justify-between">
                <div>
                    <p class="text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Sequência Atual</p>
                    <h3 id="stat-streak-days" class="text-2xl font-bold mt-1 text-gray-900 dark:text-white">0 dias</h3>
                </div>
                <div class="p-3 bg-orange-100 dark:bg-orange-900/40 text-orange-600 dark:text-orange-400 rounded-lg">
                    <i class="fa-solid fa-fire text-xl"></i>
                </div>
            </div>

            <!-- Active Pending Tasks -->
            <div class="bg-white dark:bg-gray-800 p-5 rounded-xl border border-gray-200 dark:border-gray-700 shadow-sm flex items-center justify-between">
                <div>
                    <p class="text-xs font-medium text-gray-500 dark:text-gray-400 uppercase tracking-wider">Tópicos Pendentes</p>
                    <h3 id="stat-pending-tasks" class="text-2xl font-bold mt-1 text-gray-900 dark:text-white">0</h3>
                </div>
                <div class="p-3 bg-purple-100 dark:bg-purple-900/40 text-purple-600 dark:text-purple-400 rounded-lg">
                    <i class="fa-solid fa-list-check text-xl"></i>
                </div>
            </div>
        </section>

        <!-- SECTION 2: Pomodoro & Interactive Timer -->
        <section class="bg-white dark:bg-gray-800 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm overflow-hidden p-6 sm:p-8">
            <div class="max-w-3xl mx-auto text-center">
                <div class="inline-flex items-center space-x-2 bg-blue-50 dark:bg-blue-900/30 text-blue-600 dark:text-blue-400 px-3 py-1 rounded-full text-xs font-semibold mb-4">
                    <i class="fa-solid fa-stopwatch"></i>
                    <span>Técnica Pomodoro</span>
                </div>

                <!-- Timer Mode Selector -->
                <div class="flex justify-center space-x-2 mb-6">
                    <button id="pomo-mode-work" onclick="setPomodoroMode('work')" class="px-4 py-2 text-xs sm:text-sm font-semibold rounded-lg transition-colors bg-blue-600 text-white shadow-sm">
                        Foco (25m)
                    </button>
                    <button id="pomo-mode-short" onclick="setPomodoroMode('short')" class="px-4 py-2 text-xs sm:text-sm font-semibold rounded-lg transition-colors bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300 hover:bg-gray-200 dark:hover:bg-gray-600">
                        Pausa Curta (5m)
                    </button>
                    <button id="pomo-mode-long" onclick="setPomodoroMode('long')" class="px-4 py-2 text-xs sm:text-sm font-semibold rounded-lg transition-colors bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300 hover:bg-gray-200 dark:hover:bg-gray-600">
                        Pausa Longa (15m)
                    </button>
                </div>

                <!-- Timer Display -->
                <div class="py-4">
                    <div id="pomo-timer-display" class="text-6xl sm:text-8xl font-black tracking-tight text-gray-900 dark:text-white font-mono">
                        25:00
                    </div>
                    <p id="pomo-status-label" class="text-sm font-medium text-gray-500 dark:text-gray-400 mt-2">
                        Hora de se concentrar nos estudos!
                    </p>
                </div>

                <!-- Timer Action Controls -->
                <div class="flex items-center justify-center space-x-4 mt-6">
                    <button id="pomo-start-btn" onclick="togglePomodoroTimer()" class="w-36 py-3.5 bg-blue-600 hover:bg-blue-700 text-white font-bold rounded-xl shadow-md transition transform active:scale-95 flex items-center justify-center space-x-2">
                        <i id="pomo-btn-icon" class="fa-solid fa-play"></i>
                        <span id="pomo-btn-text">Iniciar</span>
                    </button>
                    <button onclick="resetPomodoroTimer()" class="p-3.5 bg-gray-100 dark:bg-gray-700 hover:bg-gray-200 dark:hover:bg-gray-600 text-gray-700 dark:text-gray-200 font-bold rounded-xl transition">
                        <i class="fa-solid fa-rotate-left"></i>
                    </button>
                </div>
            </div>
        </section>

        <!-- SECTION 3: Study Logger Form + Breakdown Chart -->
        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            <!-- Left Side: Registration Form -->
            <section class="lg:col-span-1 bg-white dark:bg-gray-800 p-6 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm space-y-4">
                <div class="flex items-center space-x-2 border-b border-gray-100 dark:border-gray-700 pb-3">
                    <i class="fa-solid fa-pen-to-square text-blue-600 dark:text-blue-400"></i>
                    <h2 class="text-lg font-bold text-gray-900 dark:text-white">Registrar Sessão</h2>
                </div>

                <form id="study-session-form" onsubmit="handleSessionSubmit(event)" class="space-y-4">
                    <div>
                        <label class="block text-xs font-semibold text-gray-700 dark:text-gray-300 uppercase mb-1">Matéria / Disciplina</label>
                        <input type="text" id="session-subject" required placeholder="Ex: Matemática, História, Python..." class="w-full px-3 py-2 bg-gray-50 dark:bg-gray-700/50 border border-gray-300 dark:border-gray-600 rounded-lg text-sm text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 outline-none">
                    </div>

                    <div>
                        <label class="block text-xs font-semibold text-gray-700 dark:text-gray-300 uppercase mb-1">Assunto / Tópico</label>
                        <input type="text" id="session-topic" required placeholder="Ex: Equações do 2º Grau, Revolução Francesa..." class="w-full px-3 py-2 bg-gray-50 dark:bg-gray-700/50 border border-gray-300 dark:border-gray-600 rounded-lg text-sm text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 outline-none">
                    </div>

                    <div class="grid grid-cols-2 gap-3">
                        <div>
                            <label class="block text-xs font-semibold text-gray-700 dark:text-gray-300 uppercase mb-1">Tempo (min)</label>
                            <input type="number" id="session-duration" required min="1" max="1440" placeholder="Ex: 60" class="w-full px-3 py-2 bg-gray-50 dark:bg-gray-700/50 border border-gray-300 dark:border-gray-600 rounded-lg text-sm text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 outline-none">
                        </div>
                        <div>
                            <label class="block text-xs font-semibold text-gray-700 dark:text-gray-300 uppercase mb-1">Data</label>
                            <input type="date" id="session-date" required class="w-full px-3 py-2 bg-gray-50 dark:bg-gray-700/50 border border-gray-300 dark:border-gray-600 rounded-lg text-sm text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 outline-none">
                        </div>
                    </div>

                    <div>
                        <label class="block text-xs font-semibold text-gray-700 dark:text-gray-300 uppercase mb-1">Status do Tópico</label>
                        <select id="session-status" class="w-full px-3 py-2 bg-gray-50 dark:bg-gray-700/50 border border-gray-300 dark:border-gray-600 rounded-lg text-sm text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 outline-none">
                            <option value="Concluído">Concluído</option>
                            <option value="Em andamento">Em andamento</option>
                            <option value="Revisão Pendente">Revisão Pendente</option>
                        </select>
                    </div>

                    <button type="submit" class="w-full py-2.5 bg-blue-600 hover:bg-blue-700 text-white font-semibold rounded-lg text-sm shadow transition duration-150">
                        Salvar Sessão
                    </button>
                </form>
            </section>

            <!-- Right Side: Subject Breakdown Bars -->
            <section class="lg:col-span-2 bg-white dark:bg-gray-800 p-6 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm flex flex-col justify-between">
                <div>
                    <div class="flex items-center justify-between border-b border-gray-100 dark:border-gray-700 pb-3 mb-4">
                        <div class="flex items-center space-x-2">
                            <i class="fa-solid fa-chart-pie text-blue-600 dark:text-blue-400"></i>
                            <h2 class="text-lg font-bold text-gray-900 dark:text-white">Distribuição por Matéria</h2>
                        </div>
                        <span class="text-xs text-gray-500 dark:text-gray-400">Calculado por horas totais</span>
                    </div>

                    <!-- Progress bars container -->
                    <div id="subject-breakdown-list" class="space-y-4 max-h-[280px] overflow-y-auto pr-2">
                        <!-- Populated by JS -->
                    </div>
                </div>
                <div id="subject-empty-state" class="text-center py-8 text-gray-400 dark:text-gray-500">
                    <i class="fa-solid fa-chart-column text-4xl mb-2 opacity-50"></i>
                    <p class="text-sm">Nenhum estudo registrado ainda. Preencha o formulário para começar!</p>
                </div>
            </section>
        </div>

        <!-- SECTION 4: Study Planner / Kanban Board -->
        <section class="bg-white dark:bg-gray-800 p-6 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm space-y-6">
            <div class="flex flex-col sm:flex-row sm:items-center justify-between gap-4 border-b border-gray-100 dark:border-gray-700 pb-4">
                <div>
                    <h2 class="text-lg font-bold text-gray-900 dark:text-white flex items-center space-x-2">
                        <i class="fa-solid fa-bars-staggered text-blue-600 dark:text-blue-400"></i>
                        <span>Quadro de Tópicos e Tarefas</span>
                    </h2>
                    <p class="text-xs text-gray-500 dark:text-gray-400 mt-0.5">Planeje o que estudar a seguir ou mova seus conteúdos</p>
                </div>
                <!-- Quick Task Creation Trigger -->
                <form id="quick-task-form" onsubmit="handleAddTask(event)" class="flex items-center space-x-2">
                    <input type="text" id="new-task-title" required placeholder="Novo tópico de estudo..." class="px-3 py-1.5 bg-gray-50 dark:bg-gray-700/50 border border-gray-300 dark:border-gray-600 rounded-lg text-sm text-gray-900 dark:text-white focus:ring-2 focus:ring-blue-500 outline-none w-48 sm:w-64">
                    <select id="new-task-category" class="px-2 py-1.5 bg-gray-50 dark:bg-gray-700/50 border border-gray-300 dark:border-gray-600 rounded-lg text-xs text-gray-900 dark:text-white outline-none">
                        <option value="Geral">Geral</option>
                        <option value="Revisão">Revisão</option>
                        <option value="Exercícios">Exercícios</option>
                        <option value="Leitura">Leitura</option>
                    </select>
                    <button type="submit" class="px-3 py-1.5 bg-blue-600 hover:bg-blue-700 text-white font-medium text-sm rounded-lg shadow transition">
                        <i class="fa-solid fa-plus"></i>
                    </button>
                </form>
            </div>

            <!-- Kanban Columns -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <!-- Column 1: A Fazer -->
                <div class="bg-gray-50 dark:bg-gray-900/50 p-4 rounded-xl border border-gray-200 dark:border-gray-700/60">
                    <div class="flex items-center justify-between mb-3">
                        <span class="text-xs font-bold text-gray-600 dark:text-gray-300 uppercase tracking-wide flex items-center space-x-2">
                            <span class="w-2.5 h-2.5 rounded-full bg-amber-400"></span>
                            <span>A Fazer</span>
                        </span>
                        <span id="count-todo" class="text-xs font-semibold bg-gray-200 dark:bg-gray-700 px-2 py-0.5 rounded-full">0</span>
                    </div>
                    <div id="kanban-todo" class="space-y-2.5 min-h-[120px]">
                        <!-- Rendered by JS -->
                    </div>
                </div>

                <!-- Column 2: Em Andamento -->
                <div class="bg-gray-50 dark:bg-gray-900/50 p-4 rounded-xl border border-gray-200 dark:border-gray-700/60">
                    <div class="flex items-center justify-between mb-3">
                        <span class="text-xs font-bold text-gray-600 dark:text-gray-300 uppercase tracking-wide flex items-center space-x-2">
                            <span class="w-2.5 h-2.5 rounded-full bg-blue-500"></span>
                            <span>Em Andamento</span>
                        </span>
                        <span id="count-doing" class="text-xs font-semibold bg-gray-200 dark:bg-gray-700 px-2 py-0.5 rounded-full">0</span>
                    </div>
                    <div id="kanban-doing" class="space-y-2.5 min-h-[120px]">
                        <!-- Rendered by JS -->
                    </div>
                </div>

                <!-- Column 3: Concluído -->
                <div class="bg-gray-50 dark:bg-gray-900/50 p-4 rounded-xl border border-gray-200 dark:border-gray-700/60">
                    <div class="flex items-center justify-between mb-3">
                        <span class="text-xs font-bold text-gray-600 dark:text-gray-300 uppercase tracking-wide flex items-center space-x-2">
                            <span class="w-2.5 h-2.5 rounded-full bg-emerald-500"></span>
                            <span>Concluído</span>
                        </span>
                        <span id="count-done" class="text-xs font-semibold bg-gray-200 dark:bg-gray-700 px-2 py-0.5 rounded-full">0</span>
                    </div>
                    <div id="kanban-done" class="space-y-2.5 min-h-[120px]">
                        <!-- Rendered by JS -->
                    </div>
                </div>
            </div>
        </section>

        <!-- SECTION 5: Log Table / Recent Sessions -->
        <section class="bg-white dark:bg-gray-800 p-6 rounded-2xl border border-gray-200 dark:border-gray-700 shadow-sm space-y-4">
            <div class="flex items-center justify-between border-b border-gray-100 dark:border-gray-700 pb-3">
                <div class="flex items-center space-x-2">
                    <i class="fa-solid fa-list-ul text-blue-600 dark:text-blue-400"></i>
                    <h2 class="text-lg font-bold text-gray-900 dark:text-white">Histórico de Sessões</h2>
                </div>
                <span id="session-count-badge" class="text-xs font-semibold bg-blue-50 dark:bg-blue-900/40 text-blue-600 dark:text-blue-400 px-2.5 py-1 rounded-full">
                    0 registros
                </span>
            </div>

            <div class="overflow-x-auto">
                <table class="w-full text-left text-sm">
                    <thead>
                        <tr class="border-b border-gray-200 dark:border-gray-700 text-xs text-gray-500 dark:text-gray-400 uppercase">
                            <th class="pb-3 font-semibold">Data</th>
                            <th class="pb-3 font-semibold">Matéria</th>
                            <th class="pb-3 font-semibold">Assunto</th>
                            <th class="pb-3 font-semibold">Duração</th>
                            <th class="pb-3 font-semibold">Status</th>
                            <th class="pb-3 font-semibold text-right">Ação</th>
                        </tr>
                    </thead>
                    <tbody id="sessions-table-body" class="divide-y divide-gray-100 dark:divide-gray-700/60">
                        <!-- Populated by JS -->
                    </tbody>
                </table>
                <div id="sessions-empty-state" class="text-center py-8 text-gray-400 dark:text-gray-500">
                    Nenhum registro de estudo encontrado no histórico.
                </div>
            </div>
        </section>
    </main>

    <!-- Custom Notification Toast -->
    <div id="toast-container" class="fixed bottom-5 right-5 z-50 flex flex-col space-y-2 pointer-events-none"></div>

    <script>
        /* ==========================================================================
           STATE & LOCAL STORAGE INITIALIZATION
           ========================================================================== */
        const STORAGE_KEY_SESSIONS = 'estudoflow_sessions_v1';
        const STORAGE_KEY_TASKS = 'estudoflow_tasks_v1';
        const STORAGE_KEY_THEME = 'estudoflow_theme_v1';

        let sessions = JSON.parse(localStorage.getItem(STORAGE_KEY_SESSIONS)) || [];
        let tasks = JSON.parse(localStorage.getItem(STORAGE_KEY_TASKS)) || [
            { id: '1', title: 'Revisar conteúdo de Álgebra', category: 'Revisão', status: 'todo' },
            { id: '2', title: 'Resolver 10 exercícios de Gramática', category: 'Exercícios', status: 'doing' }
        ];

        /* ==========================================================================
           THEME SWITCHING (DARK/LIGHT MODE)
           ========================================================================== */
        function initTheme() {
            const savedTheme = localStorage.getItem(STORAGE_KEY_THEME);
            const systemPrefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
            
            if (savedTheme === 'dark' || (!savedTheme && systemPrefersDark)) {
                document.documentElement.classList.add('dark');
                document.getElementById('theme-toggle-light-icon').classList.remove('hidden');
            } else {
                document.documentElement.classList.remove('dark');
                document.getElementById('theme-toggle-dark-icon').classList.remove('hidden');
            }
        }

        document.getElementById('theme-toggle-btn').addEventListener('click', () => {
            const isDark = document.documentElement.classList.toggle('dark');
            localStorage.setItem(STORAGE_KEY_THEME, isDark ? 'dark' : 'light');
            
            document.getElementById('theme-toggle-dark-icon').classList.toggle('hidden', isDark);
            document.getElementById('theme-toggle-light-icon').classList.toggle('hidden', !isDark);
        });

        /* ==========================================================================
           POMODORO TIMER LOGIC & AUDIO
           ========================================================================== */
        let pomoMinutes = 25;
        let pomoSeconds = 0;
        let pomoTimerId = null;
        let pomoIsRunning = false;
        let currentPomoMode = 'work'; // 'work', 'short', 'long'

        const MODE_TIMES = {
            work: 25,
            short: 5,
            long: 15
        };

        function setPomodoroMode(mode) {
            if (pomoIsRunning) resetPomodoroTimer();
            currentPomoMode = mode;
            pomoMinutes = MODE_TIMES[mode];
            pomoSeconds = 0;

            // Highlight buttons
            ['work', 'short', 'long'].forEach(m => {
                const btn = document.getElementById(`pomo-mode-${m}`);
                if (m === mode) {
                    btn.className = "px-4 py-2 text-xs sm:text-sm font-semibold rounded-lg transition-colors bg-blue-600 text-white shadow-sm";
                } else {
                    btn.className = "px-4 py-2 text-xs sm:text-sm font-semibold rounded-lg transition-colors bg-gray-100 dark:bg-gray-700 text-gray-600 dark:text-gray-300 hover:bg-gray-200 dark:hover:bg-gray-600";
                }
            });

            const labels = {
                work: 'Hora de se concentrar nos estudos!',
                short: 'Descanse um pouco! Tome uma água.',
                long: 'Pausa mais longa. Relaxe e descanse a mente!'
            };
            document.getElementById('pomo-status-label').innerText = labels[mode];

            updateTimerDisplay();
        }

        function updateTimerDisplay() {
            const m = String(pomoMinutes).padStart(2, '0');
            const s = String(pomoSeconds).padStart(2, '0');
            document.getElementById('pomo-timer-display').innerText = `${m}:${s}`;
        }

        function togglePomodoroTimer() {
            if (pomoIsRunning) {
                // Pause
                clearInterval(pomoTimerId);
                pomoIsRunning = false;
                document.getElementById('pomo-btn-text').innerText = 'Continuar';
                document.getElementById('pomo-btn-icon').className = 'fa-solid fa-play';
            } else {
                // Start
                pomoIsRunning = true;
                document.getElementById('pomo-btn-text').innerText = 'Pausar';
                document.getElementById('pomo-btn-icon').className = 'fa-solid fa-pause';

                pomoTimerId = setInterval(() => {
                    if (pomoSeconds === 0) {
                        if (pomoMinutes === 0) {
                            clearInterval(pomoTimerId);
                            pomoIsRunning = false;
                            playTimerSound();
                            showNotification('Pomodoro Finalizado!', 'Seu tempo acabou.');
                            resetPomodoroTimer();
                            return;
                        }
                        pomoMinutes--;
                        pomoSeconds = 59;
                    } else {
                        pomoSeconds--;
                    }
                    updateTimerDisplay();
                }, 1000);
            }
        }

        function resetPomodoroTimer() {
            clearInterval(pomoTimerId);
            pomoIsRunning = false;
            pomoMinutes = MODE_TIMES[currentPomoMode];
            pomoSeconds = 0;
            document.getElementById('pomo-btn-text').innerText = 'Iniciar';
            document.getElementById('pomo-btn-icon').className = 'fa-solid fa-play';
            updateTimerDisplay();
        }

        function playTimerSound() {
            try {
                const ctx = new (window.AudioContext || window.webkitAudioContext)();
                const osc = ctx.createOscillator();
                const gain = ctx.createGain();
                osc.type = 'sine';
                osc.frequency.value = 587.33; // D5 note
                gain.gain.setValueAtTime(0.1, ctx.currentTime);
                osc.connect(gain);
                gain.connect(ctx.destination);
                osc.start();
                osc.stop(ctx.currentTime + 0.8);
            } catch (e) {
                console.log('Audio disabled or unsupported');
            }
        }

        /* ==========================================================================
           STUDY SESSIONS MANAGEMENT
           ========================================================================== */
        function handleSessionSubmit(e) {
            e.preventDefault();
            const subject = document.getElementById('session-subject').value.trim();
            const topic = document.getElementById('session-topic').value.trim();
            const durationMin = parseInt(document.getElementById('session-duration').value, 10);
            const date = document.getElementById('session-date').value;
            const status = document.getElementById('session-status').value;

            if (!subject || !topic || isNaN(durationMin) || !date) return;

            const newSession = {
                id: Date.now().toString(),
                subject,
                topic,
                durationMin,
                date,
                status
            };

            sessions.unshift(newSession);
            saveSessions();
            renderSessions();
            updateStats();

            // Reset form
            document.getElementById('study-session-form').reset();
            document.getElementById('session-date').valueAsDate = new Date();

            showNotification('Sessão Registrada!', `Estudo de ${subject} salvo com sucesso.`);
        }

        function deleteSession(id) {
            sessions = sessions.filter(s => s.id !== id);
            saveSessions();
            renderSessions();
            updateStats();
            showNotification('Removido', 'Registro excluído do histórico.');
        }

        function saveSessions() {
            localStorage.setItem(STORAGE_KEY_SESSIONS, JSON.stringify(sessions));
        }

        function renderSessions() {
            const tbody = document.getElementById('sessions-table-body');
            const emptyState = document.getElementById('sessions-empty-state');
            const countBadge = document.getElementById('session-count-badge');

            tbody.innerHTML = '';
            countBadge.innerText = `${sessions.length} registro${sessions.length !== 1 ? 's' : ''}`;

            if (sessions.length === 0) {
                emptyState.classList.remove('hidden');
                return;
            } else {
                emptyState.classList.add('hidden');
            }

            sessions.forEach(s => {
                const tr = document.createElement('tr');
                tr.className = "hover:bg-gray-50 dark:hover:bg-gray-700/30 transition-colors";

                const formattedDate = new Date(s.date + 'T00:00:00').toLocaleDateString('pt-BR');
                const hoursFormatted = (s.durationMin / 60).toFixed(1).replace('.', ',');

                let statusBadge = '';
                if (s.status === 'Concluído') {
                    statusBadge = '<span class="px-2 py-0.5 text-xs font-semibold bg-emerald-100 text-emerald-800 dark:bg-emerald-900/40 dark:text-emerald-400 rounded-full">Concluído</span>';
                } else if (s.status === 'Em andamento') {
                    statusBadge = '<span class="px-2 py-0.5 text-xs font-semibold bg-blue-100 text-blue-800 dark:bg-blue-900/40 dark:text-blue-400 rounded-full">Em andamento</span>';
                } else {
                    statusBadge = '<span class="px-2 py-0.5 text-xs font-semibold bg-amber-100 text-amber-800 dark:bg-amber-900/40 dark:text-amber-400 rounded-full">Revisão Pendente</span>';
                }

                tr.innerHTML = `
                    <td class="py-3 font-medium text-gray-900 dark:text-white">${formattedDate}</td>
                    <td class="py-3 font-semibold text-blue-600 dark:text-blue-400">${escapeHtml(s.subject)}</td>
                    <td class="py-3 text-gray-600 dark:text-gray-300">${escapeHtml(s.topic)}</td>
                    <td class="py-3 text-gray-600 dark:text-gray-300 font-mono">${s.durationMin} min (${hoursFormatted}h)</td>
                    <td class="py-3">${statusBadge}</td>
                    <td class="py-3 text-right">
                        <button onclick="deleteSession('${s.id}')" class="text-red-500 hover:text-red-700 dark:hover:text-red-400 p-1 transition" title="Excluir">
                            <i class="fa-solid fa-trash-can"></i>
                        </button>
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        /* ==========================================================================
           STATISTICS & SUBJECT BREAKDOWN
           ========================================================================== */
        function updateStats() {
            // 1. Total minutes & sessions
            const totalMinutes = sessions.reduce((acc, curr) => acc + curr.durationMin, 0);
            const totalHours = (totalMinutes / 60).toFixed(1).replace('.', ',');
            
            document.getElementById('stat-total-hours').innerText = `${totalHours} h`;
            document.getElementById('stat-total-sessions').innerText = sessions.length;

            // 2. Calculate streak
            const streak = calculateStreak();
            document.getElementById('stat-streak-days').innerText = `${streak} dia${streak !== 1 ? 's' : ''}`;
            document.getElementById('streak-header-count').innerText = `${streak} dia${streak !== 1 ? 's' : ''} seguidos`;

            // 3. Subject breakdown bars
            renderSubjectBreakdown(totalMinutes);
        }

        function calculateStreak() {
            if (sessions.length === 0) return 0;

            const dates = [...new Set(sessions.map(s => s.date))].sort().reverse();
            const todayStr = new Date().toISOString().split('T')[0];
            
            const yesterday = new Date();
            yesterday.setDate(yesterday.getDate() - 1);
            const yesterdayStr = yesterday.toISOString().split('T')[0];

            let currentStreak = 0;
            let checkDate = new Date();

            // Check if user studied today or yesterday to maintain active streak
            if (!dates.includes(todayStr) && !dates.includes(yesterdayStr)) {
                return 0;
            }

            if (dates.includes(todayStr)) {
                checkDate = new Date();
            } else {
                checkDate = yesterday;
            }

            while (true) {
                const dateStr = checkDate.toISOString().split('T')[0];
                if (dates.includes(dateStr)) {
                    currentStreak++;
                    checkDate.setDate(checkDate.getDate() - 1);
                } else {
                    break;
                }
            }

            return currentStreak;
        }

        function renderSubjectBreakdown(totalMinutes) {
            const listContainer = document.getElementById('subject-breakdown-list');
            const emptyState = document.getElementById('subject-empty-state');
            listContainer.innerHTML = '';

            if (sessions.length === 0 || totalMinutes === 0) {
                emptyState.classList.remove('hidden');
                return;
            } else {
                emptyState.classList.add('hidden');
            }

            // Group minutes by subject
            const subjectMap = {};
            sessions.forEach(s => {
                const subjKey = s.subject.trim();
                subjectMap[subjKey] = (subjectMap[subjKey] || 0) + s.durationMin;
            });

            // Sort subjects descending
            const sortedSubjects = Object.entries(subjectMap).sort((a, b) => b[1] - a[1]);

            // Colors palette
            const colors = [
                'bg-blue-500', 'bg-emerald-500', 'bg-purple-500', 
                'bg-amber-500', 'bg-indigo-500', 'bg-rose-500'
            ];

            sortedSubjects.forEach(([subject, minutes], idx) => {
                const percentage = Math.round((minutes / totalMinutes) * 100);
                const hours = (minutes / 60).toFixed(1).replace('.', ',');
                const color = colors[idx % colors.length];

                const item = document.createElement('div');
                item.className = 'space-y-1';
                item.innerHTML = `
                    <div class="flex justify-between text-xs font-medium">
                        <span class="text-gray-800 dark:text-gray-200 font-semibold">${escapeHtml(subject)}</span>
                        <span class="text-gray-500 dark:text-gray-400">${hours}h (${percentage}%)</span>
                    </div>
                    <div class="w-full h-2.5 bg-gray-100 dark:bg-gray-700 rounded-full overflow-hidden">
                        <div class="h-full ${color} rounded-full transition-all duration-500" style="width: ${percentage}%"></div>
                    </div>
                `;
                listContainer.appendChild(item);
            });
        }

        /* ==========================================================================
           KANBAN / TASK MANAGEMENT
           ========================================================================== */
        function handleAddTask(e) {
            e.preventDefault();
            const input = document.getElementById('new-task-title');
            const categorySelect = document.getElementById('new-task-category');
            const title = input.value.trim();

            if (!title) return;

            const newTask = {
                id: Date.now().toString(),
                title,
                category: categorySelect.value,
                status: 'todo'
            };

            tasks.push(newTask);
            saveTasks();
            renderTasks();

            input.value = '';
            showNotification('Tópico Adicionado', 'Nova tarefa criada no quadro.');
        }

        function moveTask(id, newStatus) {
            tasks = tasks.map(t => t.id === id ? { ...t, status: newStatus } : t);
            saveTasks();
            renderTasks();
        }

        function deleteTask(id) {
            tasks = tasks.filter(t => t.id !== id);
            saveTasks();
            renderTasks();
        }

        function saveTasks() {
            localStorage.setItem(STORAGE_KEY_TASKS, JSON.stringify(tasks));
        }

        function renderTasks() {
            const cols = {
                todo: document.getElementById('kanban-todo'),
                doing: document.getElementById('kanban-doing'),
                done: document.getElementById('kanban-done')
            };

            const counts = {
                todo: document.getElementById('count-todo'),
                doing: document.getElementById('count-doing'),
                done: document.getElementById('count-done')
            };

            // Clear
            Object.values(cols).forEach(c => c.innerHTML = '');

            const statusCounts = { todo: 0, doing: 0, done: 0 };

            tasks.forEach(task => {
                statusCounts[task.status]++;
                const card = document.createElement('div');
                card.className = "bg-white dark:bg-gray-800 p-3 rounded-lg border border-gray-200 dark:border-gray-700 shadow-sm space-y-2 text-xs group hover:border-blue-400 dark:hover:border-blue-500 transition";

                let catColor = 'bg-gray-100 text-gray-700 dark:bg-gray-700 dark:text-gray-300';
                if (task.category === 'Revisão') catColor = 'bg-purple-100 text-purple-700 dark:bg-purple-900/40 dark:text-purple-300';
                if (task.category === 'Exercícios') catColor = 'bg-blue-100 text-blue-700 dark:bg-blue-900/40 dark:text-blue-300';
                if (task.category === 'Leitura') catColor = 'bg-emerald-100 text-emerald-700 dark:bg-emerald-900/40 dark:text-emerald-300';

                card.innerHTML = `
                    <div class="flex items-start justify-between gap-2">
                        <span class="font-medium text-gray-800 dark:text-gray-100 leading-snug">${escapeHtml(task.title)}</span>
                        <button onclick="deleteTask('${task.id}')" class="text-gray-400 hover:text-red-500 transition opacity-0 group-hover:opacity-100">
                            <i class="fa-solid fa-xmark"></i>
                        </button>
                    </div>
                    <div class="flex items-center justify-between pt-1 border-t border-gray-100 dark:border-gray-700/50">
                        <span class="px-2 py-0.5 rounded-md font-semibold text-[10px] ${catColor}">${escapeHtml(task.category)}</span>
                        
                        <div class="flex items-center space-x-1">
                            ${task.status !== 'todo' ? `
                                <button onclick="moveTask('${task.id}', '${task.status === 'done' ? 'doing' : 'todo'}')" class="p-1 text-gray-400 hover:text-blue-600 dark:hover:text-blue-400" title="Mover para trás">
                                    <i class="fa-solid fa-arrow-left"></i>
                                </button>
                            ` : ''}
                            ${task.status !== 'done' ? `
                                <button onclick="moveTask('${task.id}', '${task.status === 'todo' ? 'doing' : 'done'}')" class="p-1 text-gray-400 hover:text-blue-600 dark:hover:text-blue-400" title="Avançar">
                                    <i class="fa-solid fa-arrow-right"></i>
                                </button>
                            ` : ''}
                        </div>
                    </div>
                `;

                if (cols[task.status]) {
                    cols[task.status].appendChild(card);
                }
            });

            // Update Counts
            counts.todo.innerText = statusCounts.todo;
            counts.doing.innerText = statusCounts.doing;
            counts.done.innerText = statusCounts.done;

            document.getElementById('stat-pending-tasks').innerText = statusCounts.todo + statusCounts.doing;
        }

        /* ==========================================================================
           UTILITIES & TOAST NOTIFICATIONS
           ========================================================================== */
        function showNotification(title, message) {
            const container = document.getElementById('toast-container');
            const toast = document.createElement('div');
            toast.className = "pointer-events-auto bg-gray-900 text-white dark:bg-white dark:text-gray-900 px-4 py-3 rounded-xl shadow-lg flex items-center space-x-3 transition transform duration-300 translate-y-2 opacity-0 text-xs";
            
            toast.innerHTML = `
                <i class="fa-solid fa-circle-check text-emerald-400 dark:text-emerald-600 text-sm"></i>
                <div>
                    <p class="font-bold">${escapeHtml(title)}</p>
                    <p class="opacity-80">${escapeHtml(message)}</p>
                </div>
            `;

            container.appendChild(toast);

            // Animate in
            setTimeout(() => {
                toast.classList.remove('translate-y-2', 'opacity-0');
            }, 10);

            // Animate out
            setTimeout(() => {
                toast.classList.add('opacity-0', 'translate-y-2');
                setTimeout(() => toast.remove(), 300);
            }, 3000);
        }

        function escapeHtml(str) {
            return str.replace(/[&<>"']/g, function(m) {
                return {
                    '&': '&amp;',
                    '<': '&lt;',
                    '>': '&gt;',
                    '"': '&quot;',
                    "'": '&#039;'
                }[m];
            });
        }

        /* ==========================================================================
           INITIALIZATION
           ========================================================================== */
        window.onload = function() {
            initTheme();
            document.getElementById('session-date').valueAsDate = new Date();
            renderSessions();
            renderTasks();
            updateStats();
        };
    </script>
</body>
</html>
```
