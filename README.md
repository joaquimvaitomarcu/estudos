<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Painel de Estudos</title>
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
            --emerald: #10b981;
            --amber: #f59e0b;
            --rose: #f43f5e;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
        }

        body {
            background-color: var(--bg-body);
            color: var(--text-main);
            padding: 16px;
            padding-bottom: 40px;
        }

        .container {
            max-width: 440px;
            margin: 0 auto;
            display: flex;
            flex-direction: column;
            gap: 16px;
        }

        header {
            background-color: var(--army-green);
            color: #ffffff;
            padding: 16px 20px;
            border-radius: 24px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 12px rgba(0,0,0,0.3);
        }

        header h1 {
            font-size: 1rem;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .card {
            background-color: var(--bg-card);
            border: 1px solid var(--border-color);
            border-radius: 24px;
            padding: 20px;
            display: flex;
            flex-direction: column;
            gap: 14px;
        }

        .card-title {
            font-size: 0.75rem;
            font-weight: 600;
            color: var(--text-sub);
            text-transform: uppercase;
            letter-spacing: 0.05em;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
        }

        .stat-box {
            padding: 14px;
            border-radius: 16px;
            text-align: center;
            border: 1px solid rgba(16, 185, 129, 0.2);
            background-color: rgba(16, 185, 129, 0.08);
        }

        .stat-val {
            display: block;
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--emerald);
        }

        .stat-lbl {
            font-size: 0.75rem;
            color: var(--text-sub);
        }

        .timer-display {
            font-size: 3.25rem;
            font-weight: 800;
            font-family: monospace;
            color: var(--emerald);
            text-align: center;
            margin: 8px 0;
        }

        .input-field {
            width: 100%;
            padding: 12px 14px;
            background-color: var(--input-bg);
            color: var(--text-main);
            border: 1px solid var(--border-color);
            border-radius: 16px;
            font-size: 0.875rem;
            outline: none;
        }

        .input-field:focus {
            border-color: var(--emerald);
        }

        .btn {
            border: none;
            padding: 12px 16px;
            border-radius: 16px;
            font-weight: 600;
            font-size: 0.875rem;
            cursor: pointer;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            transition: opacity 0.15s, transform 0.1s;
        }

        .btn:active {
            transform: scale(0.97);
        }

        .btn-army {
            background-color: var(--army-green);
            color: #ffffff;
        }

        .btn-emerald {
            background-color: var(--emerald);
            color: #ffffff;
        }

        .btn-amber {
            background-color: var(--amber);
            color: #ffffff;
        }

        .btn-icon {
            background-color: var(--input-bg);
            color: var(--text-main);
            border: 1px solid var(--border-color);
        }

        .flex-gap {
            display: flex;
            gap: 8px;
        }

        .progress-bar-bg {
            width: 100%;
            height: 8px;
            background-color: rgba(0,0,0,0.4);
            border-radius: 999px;
            overflow: hidden;
        }

        .progress-bar-fill {
            height: 100%;
            background-color: var(--emerald);
            width: 0%;
            transition: width 0.3s;
        }

        .log-item, .task-item {
            padding: 12px 14px;
            background-color: var(--input-bg);
            border: 1px solid var(--border-color);
            border-radius: 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 0.8125rem;
        }

        .hidden { display: none !important; }
    </style>
</head>
<body>

    <div class="container">
        <!-- Header -->
        <header>
            <h1><i class="fa-solid fa-graduation-cap"></i> Meu Painel de Estudos</h1>
        </header>

        <!-- Progresso -->
        <section class="card">
            <div class="card-title"><i class="fa-solid fa-chart-line" style="color:var(--emerald)"></i> Progresso Geral</div>
            <div class="grid-2">
                <div class="stat-box">
                    <span class="stat-val" id="statHours">0h</span>
                    <span class="stat-lbl">Tempo Estudado</span>
                </div>
                <div class="stat-box" style="border-color:rgba(245,158,11,0.2); background:rgba(245,158,11,0.08);">
                    <span class="stat-val" id="statStreak" style="color:var(--amber)">0 🔥</span>
                    <span class="stat-lbl">Sequência (Dias)</span>
                </div>
            </div>
            <div>
                <div style="display:flex; justify-content:space-between; font-size:0.75rem; margin-bottom:6px;">
                    <span style="color:var(--text-sub)">Meta de Tópicos</span>
                    <span id="progressPercent" style="color:var(--emerald); font-weight:700">0%</span>
                </div>
                <div class="progress-bar-bg">
                    <div id="progressBar" class="progress-bar-fill"></div>
                </div>
            </div>
        </section>

        <!-- Divisão por Matéria -->
        <section class="card">
            <div class="card-title"><i class="fa-solid fa-chart-pie" style="color:var(--emerald)"></i> Divisão por Matéria</div>
            <div id="subjectPercentages" style="display:flex; flex-direction:column; gap:10px;">
                <p style="font-size:0.75rem; color:var(--text-sub); font-style:italic;">Nenhum registo ainda.</p>
            </div>
        </section>

        <!-- Cronómetro de Estudo -->
        <section class="card" style="text-align:center;">
            <div class="card-title" style="justify-content:center;"><i class="fa-solid fa-stopwatch" style="color:var(--emerald)"></i> Cronómetro de Estudo</div>
            
            <div style="display:flex; flex-direction:column; gap:8px; text-align:left;">
                <input type="text" id="timerSubject" placeholder="Matéria (ex: Matemática)" class="input-field">
                <input type="text" id="timerTopic" placeholder="Assunto (ex: Trigonometria)" class="input-field">
            </div>

            <div class="timer-display" id="timerDisplay">25:00</div>

            <div class="flex-gap" style="justify-content:center;">
                <button id="startBtn" class="btn btn-army"><i class="fa-solid fa-play"></i> Iniciar</button>
                <button id="pauseBtn" class="btn btn-amber hidden"><i class="fa-solid fa-pause"></i> Pausar</button>
                <button id="finishBtn" class="btn btn-emerald"><i class="fa-solid fa-check"></i> Salvar</button>
                <button id="resetBtn" class="btn btn-icon"><i class="fa-solid fa-rotate-left"></i></button>
            </div>
        </section>

        <!-- Registo Manual -->
        <section class="card">
            <div class="card-title"><i class="fa-solid fa-plus-circle" style="color:var(--emerald)"></i> Registo Manual</div>
            <form id="studyForm" style="display:flex; flex-direction:column; gap:10px;">
                <input type="text" id="subjectInput" placeholder="Matéria (ex: História)" required class="input-field">
                <input type="text" id="topicInput" placeholder="Assunto (ex: Brasil Colônia)" required class="input-field">
                <input type="number" id="minutesInput" placeholder="Tempo (minutos)" min="1" required class="input-field">
                <button type="submit" class="btn btn-army"><i class="fa-solid fa-floppy-disk"></i> Salvar Sessão</button>
            </form>
        </section>

        <!-- Tópicos a Estudar -->
        <section class="card">
            <div class="card-title"><i class="fa-solid fa-list-check" style="color:var(--emerald)"></i> Tópicos a Estudar</div>
            <form id="taskForm" class="flex-gap">
                <input type="text" id="taskInput" placeholder="Novo tópico..." required class="input-field">
                <button type="submit" class="btn btn-army"><i class="fa-solid fa-plus"></i></button>
            </form>
            <div id="taskList" style="display:flex; flex-direction:column; gap:8px;"></div>
        </section>

        <!-- Histórico -->
        <section class="card">
            <div style="display:flex; justify-between; align-items:center;">
                <div class="card-title"><i class="fa-solid fa-history" style="color:var(--emerald)"></i> Histórico Recente</div>
                <button id="clearLogsBtn" style="background:none; border:none; color:var(--rose); font-size:0.75rem; cursor:pointer;">Limpar</button>
            </div>
            <div id="logsList" style="display:flex; flex-direction:column; gap:8px;"></div>
        </section>
    </div>

    <script>
        window.addEventListener('DOMContentLoaded', function() {
            var timer = null;
            var timeLeft = 25 * 60;
            var elapsedTimeSeconds = 0;
            var isRunning = false;

            var display = document.getElementById('timerDisplay');
            var startBtn = document.getElementById('startBtn');
            var pauseBtn = document.getElementById('pauseBtn');
            var resetBtn = document.getElementById('resetBtn');
            var finishBtn = document.getElementById('finishBtn');

            function updateDisplay() {
                var m = Math.floor(timeLeft / 60);
                var s = timeLeft % 60;
                display.textContent = (m < 10 ? '0' + m : m) + ':' + (s < 10 ? '0' + s : s);
            }

            startBtn.addEventListener('click', function() {
                if (!isRunning) {
                    isRunning = true;
                    startBtn.classList.add('hidden');
                    pauseBtn.classList.remove('hidden');
                    timer = setInterval(function() {
                        if (timeLeft > 0) {
                            timeLeft--;
                            elapsedTimeSeconds++;
                            updateDisplay();
                        } else {
                            clearInterval(timer);
                            isRunning = false;
                            alert('Tempo finalizado!');
                            saveTimerSession();
                        }
                    }, 1000);
                }
            });

            pauseBtn.addEventListener('click', function() {
                clearInterval(timer);
                isRunning = false;
                pauseBtn.classList.add('hidden');
                startBtn.classList.remove('hidden');
            });

            resetBtn.addEventListener('click', function() {
                clearInterval(timer);
                isRunning = false;
                timeLeft = 25 * 60;
                elapsedTimeSeconds = 0;
                updateDisplay();
                pauseBtn.classList.add('hidden');
                startBtn.classList.remove('hidden');
            });

            finishBtn.addEventListener('click', function() {
                if (elapsedTimeSeconds < 5) {
                    alert('Deves estudar pelo menos alguns segundos para salvar.');
                    return;
                }
                saveTimerSession();
            });

            function saveTimerSession() {
                var subj = document.getElementById('timerSubject').value.trim() || 'Geral';
                var top = document.getElementById('timerTopic').value.trim() || 'Estudo com Cronómetro';
                var mins = Math.max(1, Math.round(elapsedTimeSeconds / 60));
                
                saveLog(subj, top, mins);
                
                clearInterval(timer);
                isRunning = false;
                timeLeft = 25 * 60;
                elapsedTimeSeconds = 0;
                updateDisplay();
                pauseBtn.classList.add('hidden');
                startBtn.classList.remove('hidden');
                document.getElementById('timerSubject').value = '';
                document.getElementById('timerTopic').value = '';
            }

            function saveLog(subj, top, mins) {
                var logs = JSON.parse(localStorage.getItem('studyLogs') || '[]');
                logs.unshift({ subject: subj, topic: top, minutes: mins });
                localStorage.setItem('studyLogs', JSON.stringify(logs));
                loadData();
            }

            function loadData() {
                var logs = JSON.parse(localStorage.getItem('studyLogs') || '[]');
                var logsList = document.getElementById('logsList');
                var subjectPercentages = document.getElementById('subjectPercentages');
                logsList.innerHTML = '';
                
                var totalMin = 0;
                var totals = {};

                logs.forEach(function(l) {
                    var m = parseInt(l.minutes) || 0;
                    totalMin += m;
                    var k = l.subject.toLowerCase();
                    if (!totals[k]) totals[k] = { name: l.subject, minutes: 0 };
                    totals[k].minutes += m;

                    var item = document.createElement('div');
                    item.className = 'log-item';
                    item.innerHTML = '<div><strong style="color:var(--emerald); display:block;">' + escapeHtml(l.subject) + '</strong><span style="color:var(--text-sub);">' + escapeHtml(l.topic) + '</span></div><span style="font-weight:700; color:var(--emerald);">' + l.minutes + ' min</span>';
                    logsList.appendChild(item);
                });

                if (logs.length === 0) {
                    logsList.innerHTML = '<p style="font-size:0.75rem; color:var(--text-sub); font-style:italic;">Nenhum registo.</p>';
                }

                document.getElementById('statHours').textContent = (totalMin / 60).toFixed(1) + 'h';
                document.getElementById('statStreak').textContent = (logs.length > 0 ? 1 : 0) + ' 🔥';

                // Porcentagens
                subjectPercentages.innerHTML = '';
                if (totalMin === 0) {
                    subjectPercentages.innerHTML = '<p style="font-size:0.75rem; color:var(--text-sub); font-style:italic;">Nenhum registo.</p>';
                } else {
                    Object.values(totals).forEach(function(s) {
                        var pct = Math.round((s.minutes / totalMin) * 100);
                        var div = document.createElement('div');
                        div.innerHTML = '<div style="display:flex; justify-content:space-between; font-size:0.75rem; margin-bottom:4px;"><span style="font-weight:600;">' + escapeHtml(s.name) + '</span><span style="color:var(--emerald); font-weight:700;">' + pct + '%</span></div><div class="progress-bar-bg"><div class="progress-bar-fill" style="width:' + pct + '%"></div></div>';
                        subjectPercentages.appendChild(div);
                    });
                }
            }

            document.getElementById('studyForm').addEventListener('submit', function(e) {
                e.preventDefault();
                var subj = document.getElementById('subjectInput').value.trim();
                var top = document.getElementById('topicInput').value.trim();
                var mins = document.getElementById('minutesInput').value.trim();
                saveLog(subj, top, mins);
                this.reset();
            });

            document.getElementById('clearLogsBtn').addEventListener('click', function() {
                if (confirm('Apagar todo o histórico?')) {
                    localStorage.removeItem('studyLogs');
                    loadData();
                }
            });

            // Tarefas
            function loadTasks() {
                var tasks = JSON.parse(localStorage.getItem('studyTasks') || '[]');
                var taskList = document.getElementById('taskList');
                taskList.innerHTML = '';
                var done = 0;

                tasks.forEach(function(t, i) {
                    if (t.done) done++;
                    var item = document.createElement('div');
                    item.className = 'task-item';
                    item.innerHTML = '<span style="' + (t.done ? 'text-decoration:line-through; opacity:0.5;' : '') + '">' + escapeHtml(t.title) + '</span><div style="display:flex; gap:8px;"><button onclick="toggleTask(' + i + ')" style="background:none; border:none; color:var(--emerald); cursor:pointer;"><i class="fa-solid fa-check"></i></button><button onclick="deleteTask(' + i + ')" style="background:none; border:none; color:var(--rose); cursor:pointer;"><i class="fa-solid fa-trash"></i></button></div>';
                    taskList.appendChild(item);
                });

                var pct = tasks.length > 0 ? Math.round((done / tasks.length) * 100) : 0;
                document.getElementById('progressPercent').textContent = pct + '%';
                document.getElementById('progressBar').style.width = pct + '%';
            }

            document.getElementById('taskForm').addEventListener('submit', function(e) {
                e.preventDefault();
                var title = document.getElementById('taskInput').value.trim();
                if (!title) return;
                var tasks = JSON.parse(localStorage.getItem('studyTasks') || '[]');
                tasks.push({ title: title, done: false });
                localStorage.setItem('studyTasks', JSON.stringify(tasks));
                document.getElementById('taskInput').value = '';
                loadTasks();
            });

            window.toggleTask = function(i) {
                var tasks = JSON.parse(localStorage.getItem('studyTasks') || '[]');
                tasks[i].done = !tasks[i].done;
                localStorage.setItem('studyTasks', JSON.stringify(tasks));
                loadTasks();
            };

            window.deleteTask = function(i) {
                var tasks = JSON.parse(localStorage.getItem('studyTasks') || '[]');
                tasks.splice(i, 1);
                localStorage.setItem('studyTasks', JSON.stringify(tasks));
                loadTasks();
            };

            function escapeHtml(t) {
                var d = document.createElement('div');
                d.innerText = t;
