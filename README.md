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
          
