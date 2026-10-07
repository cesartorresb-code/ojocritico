<!DOCTYPE html>
<html lang="es" class="h-full bg-slate-900 text-slate-100">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LenguaQuest 6° - El Gran Taller de las Palabras</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600;700&family=Outfit:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- Canvas Confetti Library -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.9.2/dist/confetti.browser.min.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Outfit', 'sans-serif'],
                        display: ['Fredoka', 'cursive']
                    },
                    colors: {
                        brand: {
                            50: '#f0f9ff',
                            100: '#e0f2fe',
                            400: '#38bdf8',
                            500: '#0284c7',
                            600: '#0369a1',
                            700: '#075985',
                        },
                        gram: {
                            sustantivo: '#3b82f6', // Blue
                            adjetivo: '#10b981',   // Emerald
                            adverbio: '#8b5cf6',   // Purple
                            preposicion: '#f59e0b',// Amber
                            conector: '#ec4899'    // Pink
                        }
                    }
                }
            }
        }
    </script>

    <style>
        .font-display { font-family: 'Fredoka', cursive; }
        
        @keyframes pulse-subtle {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.03); }
        }
        .animate-pulse-subtle { animation: pulse-subtle 2s infinite ease-in-out; }

        .glass-panel {
            background: rgba(30, 41, 59, 0.7);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        /* Printable styles for official report */
        @media print {
            body { background: white !important; color: black !important; }
            .no-print { display: none !important; }
            .print-only { display: block !important; }
            .report-card { border: 2px solid #000 !important; color: black !important; background: white !important; box-shadow: none !important; }
        }
        .print-only { display: none; }
    </style>
</head>
<body class="h-full flex flex-col font-sans bg-slate-950 text-slate-100 selection:bg-brand-500 selection:text-white">

    <!-- TOP HEADER -->
    <header class="no-print sticky top-0 z-40 glass-panel border-b border-slate-800 px-4 py-3">
        <div class="max-w-7xl mx-auto flex flex-wrap justify-between items-center gap-3">
            <!-- Game Title & Badge -->
            <div class="flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-indigo-500 via-purple-500 to-pink-500 flex items-center justify-center text-white text-xl shadow-lg shadow-purple-500/20">
                    <i class="fa-solid fa-feather-pointed"></i>
                </div>
                <div>
                    <h1 class="font-display text-xl font-bold bg-gradient-to-r from-sky-400 via-purple-300 to-pink-400 bg-clip-text text-transparent">
                        LenguaQuest <span class="text-xs px-2 py-0.5 rounded-full bg-slate-800 text-sky-400 border border-sky-500/30">6° Primaria</span>
                    </h1>
                    <p class="text-xs text-slate-400 font-medium hidden sm:block">Campo Formativo: Lenguajes • Taller de Redacción</p>
                </div>
            </div>

            <!-- Student Profile Summary & Navigation Buttons -->
            <div class="flex items-center gap-2 sm:gap-4">
                <!-- XP & Stars pill -->
                <div class="flex items-center gap-3 bg-slate-900/80 border border-slate-800 rounded-full px-3 py-1.5 text-xs sm:text-sm">
                    <div class="flex items-center gap-1.5 text-amber-400 font-bold" title="Puntos XP">
                        <i class="fa-solid fa-star"></i>
                        <span id="header-xp">0</span> XP
                    </div>
                    <div class="w-px h-4 bg-slate-700"></div>
                    <div class="flex items-center gap-1.5 text-sky-400 font-bold" title="Nivel actual">
                        <i class="fa-solid fa-trophy"></i>
                        <span>Nvl <span id="header-level">1</span></span>
                    </div>
                </div>

                <!-- Navigation Tabs -->
                <div class="flex items-center gap-1 bg-slate-900 p-1 rounded-xl border border-slate-800 text-xs">
                    <button onclick="switchTab('adventure')" id="tab-adventure" class="nav-btn active px-3 py-1.5 rounded-lg font-medium transition flex items-center gap-1.5 bg-brand-600 text-white shadow">
                        <i class="fa-solid fa-map-location-dot"></i> <span class="hidden md:inline">Misiones</span>
                    </button>
                    <button onclick="switchTab('express')" id="tab-express" class="nav-btn px-3 py-1.5 rounded-lg font-medium transition text-slate-400 hover:text-white flex items-center gap-1.5">
                        <i class="fa-solid fa-bolt text-amber-400"></i> <span class="hidden md:inline">Modo 30s</span>
                    </button>
                    <button onclick="switchTab('profile')" id="tab-profile" class="nav-btn px-3 py-1.5 rounded-lg font-medium transition text-slate-400 hover:text-white flex items-center gap-1.5">
                        <i class="fa-solid fa-id-card"></i> <span class="hidden md:inline">Perfil</span>
                    </button>
                    <button onclick="switchTab('teacher')" id="tab-teacher" class="nav-btn px-3 py-1.5 rounded-lg font-medium transition text-emerald-400 hover:text-emerald-300 hover:bg-slate-800 flex items-center gap-1.5">
                        <i class="fa-solid fa-chalkboard-user"></i> <span class="hidden md:inline">Docente</span>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- MAIN CONTAINER -->
    <main class="flex-1 max-w-7xl w-full mx-auto p-4 md:p-6 overflow-y-auto">

        <!-- Sync / Storage Alert Bar -->
        <div id="sync-banner" class="no-print mb-4 p-3 rounded-xl bg-slate-900/90 border border-slate-800 text-xs flex items-center justify-between text-slate-300">
            <div class="flex items-center gap-2">
                <span id="sync-icon" class="w-2.5 h-2.5 rounded-full bg-emerald-500 inline-block animate-ping"></span>
                <span id="sync-text">Modo local activado. Tus avances se guardan en el dispositivo y se sincronizarán en la nube al conectar.</span>
            </div>
            <button onclick="openRegistrationModal()" class="text-sky-400 hover:underline font-bold flex items-center gap-1">
                <i class="fa-solid fa-user-pen"></i> Cambiar Alumno
            </button>
        </div>

        <!-- ================= TAB 1: MISIONES DE CONSTRUCCIÓN DE TEXTOS ================= -->
        <section id="view-adventure" class="tab-view space-y-6">
            <!-- Grammatical Cheat-sheet Quick Reference -->
            <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-5 gap-2 text-xs">
                <div class="p-2.5 rounded-xl bg-blue-950/40 border border-blue-500/30 flex items-center gap-2">
                    <span class="w-3 h-3 rounded-full bg-gram-sustantivo shrink-0"></span>
                    <div>
                        <p class="font-bold text-blue-300">Sustantivo</p>
                        <p class="text-[10px] text-slate-400">Nombra objetos, seres, ideas</p>
                    </div>
                </div>
                <div class="p-2.5 rounded-xl bg-emerald-950/40 border border-emerald-500/30 flex items-center gap-2">
                    <span class="w-3 h-3 rounded-full bg-gram-adjetivo shrink-0"></span>
                    <div>
                        <p class="font-bold text-emerald-300">Adjetivo</p>
                        <p class="text-[10px] text-slate-400">Describe o califica</p>
                    </div>
                </div>
                <div class="p-2.5 rounded-xl bg-purple-950/40 border border-purple-500/30 flex items-center gap-2">
                    <span class="w-3 h-3 rounded-full bg-gram-adverbio shrink-0"></span>
                    <div>
                        <p class="font-bold text-purple-300">Adverbio y Tipos</p>
                        <p class="text-[10px] text-slate-400">Modo, tiempo, lugar, etc.</p>
                    </div>
                </div>
                <div class="p-2.5 rounded-xl bg-amber-950/40 border border-amber-500/30 flex items-center gap-2">
                    <span class="w-3 h-3 rounded-full bg-gram-preposicion shrink-0"></span>
                    <div>
                        <p class="font-bold text-amber-300">Preposición</p>
                        <p class="text-[10px] text-slate-400">Enlaza palabras (a, de, en...)</p>
                    </div>
                </div>
                <div class="p-2.5 rounded-xl bg-pink-950/40 border border-pink-500/30 flex items-center gap-2 col-span-2 sm:col-span-1">
                    <span class="w-3 h-3 rounded-full bg-gram-conector shrink-0"></span>
                    <div>
                        <p class="font-bold text-pink-300">Conector</p>
                        <p class="text-[10px] text-slate-400">Une oraciones e ideas</p>
                    </div>
                </div>
            </div>

            <!-- Level Selector Dashboard -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
                <!-- Level Selector Sidebar -->
                <div class="glass-panel p-5 rounded-2xl border border-slate-800 space-y-4">
                    <h2 class="font-display text-lg font-bold text-slate-100 flex items-center gap-2">
                        <i class="fa-solid fa-map text-amber-400"></i> Ruta de Aprendizaje 6°
                    </h2>
                    <p class="text-xs text-slate-400">Completa cada nivel para construir un párrafo complejo y descriptivo digno de sexto grado.</p>
                    
                    <div class="space-y-3" id="levels-list">
                        <!-- Rendered dynamically -->
                    </div>
                </div>

                <!-- Active Mission Workspace -->
                <div class="lg:col-span-2 glass-panel p-6 rounded-2xl border border-slate-800 flex flex-col justify-between space-y-6" id="mission-workspace">
                    <!-- Dynamic Mission Screen -->
                </div>
            </div>
        </section>

        <!-- ================= TAB 2: MODO EXPRÉS 30 SEGUNDOS ================= -->
        <section id="view-express" class="tab-view hidden space-y-6">
            <div class="max-w-2xl mx-auto glass-panel p-6 sm:p-8 rounded-3xl border border-amber-500/30 text-center space-y-6 relative overflow-hidden">
                <!-- Decorative Glow -->
                <div class="absolute -top-10 -right-10 w-40 h-40 bg-amber-500/10 rounded-full blur-3xl pointer-events-none"></div>

                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-amber-500/20 text-amber-300 text-xs font-bold border border-amber-500/30">
                    <i class="fa-solid fa-stopwatch animate-bounce"></i> Desafío de Velocidad Gramatical
                </div>

                <h2 class="font-display text-2xl sm:text-3xl font-bold">Modo Express 30s</h2>
                <p class="text-slate-300 text-sm max-w-lg mx-auto">
                    Lee la oración, observa la palabra <span class="bg-amber-400/20 text-amber-300 px-1.5 py-0.5 rounded font-bold border border-amber-400/40">resaltada</span> y clasifícala lo más rápido posible. ¿Será un <b>Adverbio</b>, un <b>Conector</b> o una <b>Preposición</b>?
                </p>

                <!-- Express Mini Game Display Box -->
                <div id="express-start-card" class="py-6 space-y-4">
                    <div class="bg-slate-900/80 p-6 rounded-2xl border border-slate-800 flex flex-col items-center gap-3">
                        <i class="fa-solid fa-bolt-lightning text-5xl text-amber-400 animate-pulse"></i>
                        <p class="text-xs text-slate-400">Récord Actual: <span id="express-high-score" class="text-amber-400 font-bold">0</span> puntos</p>
                    </div>
                    <button onclick="startExpressGame()" class="w-full sm:w-auto px-8 py-3.5 bg-gradient-to-r from-amber-500 to-orange-600 hover:from-amber-400 hover:to-orange-500 text-slate-950 font-display font-bold text-lg rounded-2xl shadow-lg shadow-amber-500/20 transition transform active:scale-95">
                        <i class="fa-solid fa-play mr-2"></i> ¡Comenzar Desafío!
                    </button>
                </div>

                <!-- Express Active Gameplay Screen -->
                <div id="express-game-card" class="hidden space-y-6">
                    <!-- Timer & Score Header -->
                    <div class="flex items-center justify-between bg-slate-900 px-4 py-3 rounded-2xl border border-slate-800">
                        <div class="flex items-center gap-2">
                            <i class="fa-solid fa-clock text-amber-400 text-lg"></i>
                            <span id="express-timer" class="font-display text-2xl font-bold text-amber-400">30</span>
                            <span class="text-xs text-slate-400">seg</span>
                        </div>
                        <div class="flex items-center gap-2">
                            <span class="text-xs text-slate-400">Puntaje:</span>
                            <span id="express-score" class="font-display text-2xl font-bold text-emerald-400">0</span>
                        </div>
                    </div>

                    <!-- Sentence Box -->
                    <div class="min-h-[120px] bg-slate-900 p-6 rounded-2xl border border-slate-800 flex items-center justify-center text-lg sm:text-xl font-medium leading-relaxed text-slate-200" id="express-sentence-box">
                        <!-- Dynamic sentence inserted here -->
                    </div>

                    <!-- Choice Buttons -->
                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-3" id="express-options">
                        <button onclick="answerExpress('Adverbio')" class="p-4 rounded-xl bg-purple-900/40 border border-purple-500/50 hover:bg-purple-600 hover:text-white transition font-display font-bold text-purple-300 flex flex-col items-center gap-1 active:scale-95">
                            <i class="fa-solid fa-sliders"></i>
                            <span>Adverbio</span>
                        </button>
                        <button onclick="answerExpress('Conector')" class="p-4 rounded-xl bg-pink-900/40 border border-pink-500/50 hover:bg-pink-600 hover:text-white transition font-display font-bold text-pink-300 flex flex-col items-center gap-1 active:scale-95">
                            <i class="fa-solid fa-link"></i>
                            <span>Conector</span>
                        </button>
                        <button onclick="answerExpress('Preposición')" class="p-4 rounded-xl bg-amber-900/40 border border-amber-500/50 hover:bg-amber-600 hover:text-white transition font-display font-bold text-amber-300 flex flex-col items-center gap-1 active:scale-95">
                            <i class="fa-solid fa-right-to-bracket"></i>
                            <span>Preposición</span>
                        </button>
                    </div>
                </div>
            </div>
        </section>

        <!-- ================= TAB 3: PERFIL DE ALUMNO Y LOGROS ================= -->
        <section id="view-profile" class="tab-view hidden space-y-6">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                <!-- Profile Card -->
                <div class="glass-panel p-6 rounded-2xl border border-slate-800 space-y-4 text-center">
                    <div class="relative w-24 h-24 mx-auto">
                        <div class="w-full h-full rounded-2xl bg-gradient-to-tr from-sky-500 to-indigo-600 flex items-center justify-center text-4xl text-white font-bold shadow-lg shadow-sky-500/20" id="profile-avatar-icon">
                            <i class="fa-solid fa-user-astronaut"></i>
                        </div>
                        <button onclick="openRegistrationModal()" class="absolute -bottom-1 -right-1 bg-slate-800 border border-slate-700 text-sky-400 p-2 rounded-xl text-xs hover:bg-slate-700" title="Editar Perfil">
                            <i class="fa-solid fa-pen"></i>
                        </button>
                    </div>

                    <div>
                        <h2 class="font-display text-xl font-bold text-white" id="profile-name-display">Alumno Desconocido</h2>
                        <p class="text-xs text-slate-400" id="profile-details-display">6° Grado • Grupo "A"</p>
                        <p class="text-xs text-sky-400 font-semibold mt-1" id="profile-school-display">Escuela Primaria Oficial</p>
                    </div>

                    <div class="pt-4 border-t border-slate-800 grid grid-cols-2 gap-2 text-xs">
                        <div class="bg-slate-900 p-3 rounded-xl border border-slate-800">
                            <p class="text-slate-400">Total XP</p>
                            <p class="font-display text-lg font-bold text-amber-400" id="profile-xp-val">0</p>
                        </div>
                        <div class="bg-slate-900 p-3 rounded-xl border border-slate-800">
                            <p class="text-slate-400">Nivel</p>
                            <p class="font-display text-lg font-bold text-sky-400" id="profile-level-val">1</p>
                        </div>
                    </div>
                </div>

                <!-- Badges & Achievements Grid -->
                <div class="md:col-span-2 glass-panel p-6 rounded-2xl border border-slate-800 space-y-4">
                    <h3 class="font-display text-lg font-bold text-white flex items-center gap-2">
                        <i class="fa-solid fa-award text-amber-400"></i> Insignias Gramaticales Obtenidas
                    </h3>
                    <div class="grid grid-cols-2 sm:grid-cols-3 gap-4" id="badges-grid">
                        <!-- Badges rendered by JS -->
                    </div>
                </div>
            </div>

            <!-- Learning History Log -->
            <div class="glass-panel p-6 rounded-2xl border border-slate-800 space-y-4">
                <h3 class="font-display text-lg font-bold text-white flex items-center gap-2">
                    <i class="fa-solid fa-clock-rotate-left text-sky-400"></i> Historial de Actividades Recientes
                </h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-xs text-left text-slate-300">
                        <thead class="bg-slate-900 text-slate-400 uppercase text-[10px]">
                            <tr>
                                <th class="p-3">Fecha y Hora</th>
                                <th class="p-3">Misión / Modo</th>
                                <th class="p-3">Puntaje</th>
                                <th class="p-3">Estado</th>
                            </tr>
                        </thead>
                        <tbody id="history-table-body" class="divide-y divide-slate-800">
                            <!-- Populated dynamically -->
                        </tbody>
                    </table>
                </div>
            </div>
        </section>

        <!-- ================= TAB 4: ZONA DOCENTE Y REPORTE OFICIAL ================= -->
        <section id="view-teacher" class="tab-view hidden space-y-6">
            <div class="glass-panel p-6 rounded-2xl border border-emerald-500/30 space-y-6">
                <div class="flex flex-wrap justify-between items-center gap-4 border-b border-slate-800 pb-4">
                    <div>
                        <h2 class="font-display text-xl font-bold text-emerald-400 flex items-center gap-2">
                            <i class="fa-solid fa-file-invoice text-2xl"></i> Panel del Docente y Reportes Formativos
                        </h2>
                        <p class="text-xs text-slate-400">Genera la evidencia impreso-digital de evaluación continua para la NEM / Campo Formativo Lenguajes.</p>
                    </div>
                    <button onclick="printOfficialReport()" class="px-5 py-2.5 bg-emerald-600 hover:bg-emerald-500 text-white rounded-xl font-bold text-xs flex items-center gap-2 shadow-lg shadow-emerald-600/20 transition">
                        <i class="fa-solid fa-print"></i> Generar / Imprimir Reporte PDF
                    </button>
                </div>

                <!-- Printable Official Assessment Report Sheet (Formatted for SEP/Lenguajes) -->
                <div class="report-card bg-white text-slate-900 p-6 sm:p-8 rounded-2xl shadow-2xl border border-slate-300 space-y-6 font-sans">
                    <!-- Report Header -->
                    <div class="border-b-2 border-slate-900 pb-4 flex justify-between items-start gap-4">
                        <div>
                            <h3 class="text-xl font-bold text-slate-900 uppercase tracking-wide">Reporte de Evaluación Formativa</h3>
                            <p class="text-xs font-semibold text-slate-600">Campo Formativo: Lenguajes • 6° Grado de Educación Primaria</p>
                            <p class="text-xs text-slate-500">Contenido: Análisis y uso de adverbios, conectores, preposiciones, adjetivos y sustantivos en la redacción.</p>
                        </div>
                        <div class="text-right">
                            <span class="inline-block px-3 py-1 bg-slate-900 text-white text-xs font-bold rounded">
                                EVIDENCIA OFICIAL
                            </span>
                            <p class="text-[10px] text-slate-500 mt-1" id="report-date">Fecha: 00/00/0000</p>
                        </div>
                    </div>

                    <!-- Student & Teacher Metadata Grid -->
                    <div class="grid grid-cols-2 sm:grid-cols-4 gap-4 text-xs bg-slate-100 p-4 rounded-xl border border-slate-300">
                        <div>
                            <span class="text-slate-500 block font-semibold text-[10px] uppercase">Nombre del Alumno</span>
                            <span id="rep-student-name" class="font-bold text-slate-900">--</span>
                        </div>
                        <div>
                            <span class="text-slate-500 block font-semibold text-[10px] uppercase">Grado y Grupo</span>
                            <span id="rep-student-grade" class="font-bold text-slate-900">6° --</span>
                        </div>
                        <div>
                            <span class="text-slate-500 block font-semibold text-[10px] uppercase">Escuela Primaria</span>
                            <span id="rep-school-name" class="font-bold text-slate-900">--</span>
                        </div>
                        <div>
                            <span class="text-slate-500 block font-semibold text-[10px] uppercase">Nivel de Dominio</span>
                            <span id="rep-level-mastery" class="font-bold text-emerald-700">En Desarrollo</span>
                        </div>
                    </div>

                    <!-- Competency Matrix / Table -->
                    <div class="space-y-2">
                        <h4 class="font-bold text-xs uppercase text-slate-800 tracking-wider">Procesos de Desarrollo de Aprendizaje (PDA) Evaluados</h4>
                        <table class="w-full text-xs text-left border-collapse border border-slate-300">
                            <thead>
                                <tr class="bg-slate-200 text-slate-800">
                                    <th class="p-2 border border-slate-300 font-bold">Indicador / PDA Lenguajes 6°</th>
                                    <th class="p-2 border border-slate-300 font-bold w-32 text-center">Estatus</th>
                                    <th class="p-2 border border-slate-300 font-bold w-24 text-center">Puntaje</th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-slate-300">
                                <tr>
                                    <td class="p-2 border border-slate-300">1. Identifica y emplea adverbios de tiempo, lugar, modo y cantidad para enriquecer oraciones.</td>
                                    <td class="p-2 border border-slate-300 text-center font-bold text-emerald-600" id="rep-pda-1">Consolidado</td>
                                    <td class="p-2 border border-slate-300 text-center font-mono font-bold" id="rep-score-1">100%</td>
                                </tr>
                                <tr>
                                    <td class="p-2 border border-slate-300">2. Emplea sustantivos y adjetivos calificativos para detallar descripciones complejas.</td>
                                    <td class="p-2 border border-slate-300 text-center font-bold text-emerald-600" id="rep-pda-2">Consolidado</td>
                                    <td class="p-2 border border-slate-300 text-center font-mono font-bold" id="rep-score-2">100%</td>
                                </tr>
                                <tr>
                                    <td class="p-2 border border-slate-300">3. Utiliza preposiciones y conectores temporales/causales para dar cohesión al texto.</td>
                                    <td class="p-2 border border-slate-300 text-center font-bold text-emerald-600" id="rep-pda-3">En Proceso</td>
                                    <td class="p-2 border border-slate-300 text-center font-mono font-bold" id="rep-score-3">80%</td>
                                </tr>
                                <tr>
                                    <td class="p-2 border border-slate-300">4. Agilidad en la identificación contextual de elementos gramaticales (Modo Express).</td>
                                    <td class="p-2 border border-slate-300 text-center font-bold text-sky-600" id="rep-pda-4">Destacado</td>
                                    <td class="p-2 border border-slate-300 text-center font-mono font-bold" id="rep-score-4">0 pts</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>

                    <!-- Teacher Signatures & Observations -->
                    <div class="grid grid-cols-2 gap-8 pt-8">
                        <div class="border-t border-slate-400 text-center pt-2">
                            <p class="text-xs font-bold text-slate-800">Firma del Docente / Asesor</p>
                            <p class="text-[10px] text-slate-500">Evaluación Continua - Campo Lenguajes</p>
                        </div>
                        <div class="border-t border-slate-400 text-center pt-2">
                            <p class="text-xs font-bold text-slate-800">Sello o Validación Escolar</p>
                            <p class="text-[10px] text-slate-500">Escuela Primaria Oficial</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

    </main>

    <!-- USER REGISTRATION / PROFILE MODAL -->
    <div id="modal-register" class="fixed inset-0 z-50 bg-slate-950/80 backdrop-blur-sm hidden flex items-center justify-center p-4">
        <div class="glass-panel p-6 sm:p-8 rounded-3xl border border-slate-700 max-w-md w-full space-y-5 relative shadow-2xl">
            <button onclick="closeRegistrationModal()" class="absolute top-4 right-4 text-slate-400 hover:text-white">
                <i class="fa-solid fa-xmark text-xl"></i>
            </button>

            <div class="text-center space-y-1">
                <div class="w-12 h-12 bg-sky-500/20 text-sky-400 rounded-2xl flex items-center justify-center mx-auto text-2xl border border-sky-500/30">
                    <i class="fa-solid fa-user-plus"></i>
                </div>
                <h3 class="font-display text-2xl font-bold text-white">Registro de Estudiante</h3>
                <p class="text-xs text-slate-400">Guarda tu progreso para descargar tus evidencias gramaticales.</p>
            </div>

            <form onsubmit="handleRegistrationSubmit(event)" class="space-y-4 text-xs">
                <div>
                    <label class="block font-bold text-slate-300 mb-1">Nombre Completo del Alumno</label>
                    <input type="text" id="input-student-name" required placeholder="Ej. Sofía Hernández Pérez" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2.5 text-white focus:outline-none focus:border-sky-500">
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block font-bold text-slate-300 mb-1">Grado</label>
                        <select id="input-student-grade" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2.5 text-white focus:outline-none focus:border-sky-500">
                            <option value="6° Primaria">6° Primaria</option>
                        </select>
                    </div>
                    <div>
                        <label class="block font-bold text-slate-300 mb-1">Grupo</label>
                        <input type="text" id="input-student-group" required placeholder="Ej. A / B" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2.5 text-white focus:outline-none focus:border-sky-500">
                    </div>
                </div>
                <div>
                    <label class="block font-bold text-slate-300 mb-1">Nombre de la Escuela Primaria</label>
                    <input type="text" id="input-school-name" required placeholder="Ej. Benito Juárez" class="w-full bg-slate-900 border border-slate-700 rounded-xl px-3 py-2.5 text-white focus:outline-none focus:border-sky-500">
                </div>

                <button type="submit" class="w-full py-3 bg-gradient-to-r from-sky-500 to-indigo-600 hover:from-sky-400 hover:to-indigo-500 text-white font-display font-bold text-sm rounded-xl shadow-lg shadow-sky-500/20 transition">
                    <i class="fa-solid fa-floppy-disk mr-1"></i> Guardar y Comenzar
                </button>
            </form>
        </div>
    </div>

    <!-- FIREBASE & CORE GAME LOGIC MODULE -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, doc, setDoc, getDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Firebase Initialization with mandatory environment parameters check
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'lenguaquest-6gr';
        let db = null;
        let auth = null;
        let user = null;

        if (typeof __firebase_config !== 'undefined') {
            try {
                const firebaseConfig = JSON.parse(__firebase_config);
                const app = initializeApp(firebaseConfig);
                auth = getAuth(app);
                db = getFirestore(app);

                // Authentication Rule implementation
                const initAuth = async () => {
                    if (typeof __initial_auth_token !== 'undefined' && __initial_auth_token) {
                        await signInWithCustomToken(auth, __initial_auth_token);
                    } else {
                        await signInAnonymously(auth);
                    }
                };
                initAuth();

                onAuthStateChanged(auth, (u) => {
                    user = u;
                    if (user) {
                        console.log("Firebase Auth Connected:", user.uid);
                        document.getElementById('sync-icon').className = "w-2.5 h-2.5 rounded-full bg-emerald-500 inline-block";
                        document.getElementById('sync-text').innerText = "Sincronizado con la nube (Firebase activo) + Copia en dispositivo.";
                    }
                });
            } catch (err) {
                console.warn("Firebase initialization skipped or failed. Using localStorage backup:", err);
            }
        }

        // Global Sync Function called when student saves progress
        window.saveStudentDataCloud = async function(data) {
            // Always update LocalStorage
            localStorage.setItem('lenguaquest_student', JSON.stringify(data));

            // Firestore sync adhering strictly to RULE 1 path structure
            if (db && user) {
                try {
                    const docRef = doc(db, 'artifacts', appId, 'users', user.uid, 'profile', 'data');
                    await setDoc(docRef, data, { merge: true });
                    console.log("Data successfully synced to Firestore!");
                } catch (e) {
                    console.error("Firestore sync error:", e);
                }
            }
        };

        window.loadStudentDataCloud = async function() {
            let local = localStorage.getItem('lenguaquest_student');
            if (local) {
                return JSON.parse(local);
            }
            if (db && user) {
                try {
                    const docRef = doc(db, 'artifacts', appId, 'users', user.uid, 'profile', 'data');
                    const snap = await getDoc(docRef);
                    if (snap.exists()) {
                        return snap.data();
                    }
                } catch (e) {
                    console.error("Error loading Firestore data:", e);
                }
            }
            return null;
        };
    </script>

    <script>
        // APP STATE
        let studentState = {
            name: 'Alumno de 6°',
            grade: '6° Primaria',
            group: 'A',
            school: 'Escuela Primaria Lic. Benito Juárez',
            xp: 0,
            level: 1,
            completedLevels: [],
            badges: [],
            expressHighScore: 0,
            history: []
        };

        // GRAMMAR LEVELS (6° Primaria - Campo Formativo Lenguajes)
        const GAME_LEVELS = [
            {
                id: 1,
                title: "Nivel 1: Sustantivos y Adjetivos",
                subtitle: "Enriqueciendo las ideas básicas",
                icon: "fa-cubes",
                color: "blue",
                description: "Partiendo de una oración simple, amplíala agregando sustantivos precisos y adjetivos calificativos impactantes.",
                baseSentence: "El perro corrió por el campo.",
                taskPrompt: "Transforma la oración simple eligiendo el conjunto de Sustantivos y Adjetivos que le den mayor belleza y detalle descriptivo:",
                options: [
                    {
                        text: "El voraz perro corrió por el campo.",
                        feedback: "Falta enriquecer más sustantivos con adjetivos calificativos.",
                        correct: false
                    },
                    {
                        text: "El majestuoso sabueso azabache corrió alegremente por el frondoso campo silvestre.",
                        feedback: "¡Excelente! Has enriquecido el sujeto y el escenario con sustantivos específicos y adjetivos precisos.",
                        correct: true
                    },
                    {
                        text: "El perro feo corrió por el campo grande.",
                        feedback: "Aunque usaste adjetivos, son demasiado básicos para sexto grado.",
                        correct: false
                    }
                ],
                badge: "Maestro del Detalle"
            },
            {
                id: 2,
                title: "Nivel 2: La Cueva de los Adverbios",
                subtitle: "Clasificación de Adverbios (Tiempo, Lugar, Modo, Cantidad)",
                icon: "fa-sliders",
                color: "purple",
                description: "Los adverbios modifican al verbo diciendo cómo, cuándo, dónde o cuánto ocurre la acción.",
                baseSentence: "El investigador analizó las pistas.",
                taskPrompt: "Agrega adverbios de MODO (rápidamente) y TIEMPO (ayer) para darle precisión temporal y procedimental al verbo 'analizó':",
                options: [
                    {
                        text: "Ayer, el astuto investigador analizó cuidadosamente las pistas del misterioso caso.",
                        feedback: "¡Perfecto! 'Ayer' es adverbio de tiempo y 'cuidadosamente' de modo.",
                        correct: true
                    },
                    {
                        text: "El investigador analizó las pistas allá en la casa.",
                        feedback: "Aquí solo usaste adverbios de lugar ('allá'), pero el reto pedía tiempo y modo.",
                        correct: false
                    },
                    {
                        text: "El investigador analizó muchas pistas.",
                        feedback: "'Muchas' califica la cantidad, falta precisar el modo y el tiempo.",
                        correct: false
                    }
                ],
                badge: "Cazador de Adverbios"
            },
            {
                id: 3,
                title: "Nivel 3: El Puente de las Preposiciones",
                subtitle: "A, ante, bajo, con, contra, de, desde, en, entre, hacia...",
                icon: "fa-bridge",
                color: "amber",
                description: "Las preposiciones son enlaces fundamentales que relacionan sustantivos y conceptos en el texto.",
                baseSentence: "El tren avanzó la niebla la estación final.",
                taskPrompt: "Selecciona las preposiciones correctas para unir los elementos de la oración de manera coherente:",
                options: [
                    {
                        text: "El tren avanzó por la niebla con la estación final.",
                        feedback: "La preposición 'con' no encaja adecuadamente con la dirección del trayecto.",
                        correct: false
                    },
                    {
                        text: "El tren avanzó a través de la densa niebla hacia la estación final.",
                        feedback: "¡Extraordinario! 'A través de' y 'hacia' marcan perfectamente el paso y destino.",
                        correct: true
                    },
                    {
                        text: "El tren avanzó en la niebla sin la estación final.",
                        feedback: "'Sin' cambia de forma ilógica el significado del trayecto.",
                        correct: false
                    }
                ],
                badge: "Guía de Preposiciones"
            },
            {
                id: 4,
                title: "Nivel 4: La Torre de los Conectores",
                subtitle: "Uniendo ideas (Sin embargo, Por lo tanto, Además, Ya que)",
                icon: "fa-link",
                color: "pink",
                description: "Los conectores lógicos otorgan fluidez y jerarquía a los párrafos amplios.",
                baseSentence: "Llovió intensamente todo el día. Los exploradores continuaron su camino sin rendirse.",
                taskPrompt: "Elige el conector adversativo o de oposición idóneo para transformar dos oraciones simples en un solo enunciado cohesivo:",
                options: [
                    {
                        text: "Llovió intensamente todo el día, por consiguiente, los exploradores continuaron su camino.",
                        feedback: "'Por consiguiente' expresa consecuencia directa, no contraste o valentía.",
                        correct: false
                    },
                    {
                        text: "Llovió intensamente todo el día; no obstante, los intrépidos exploradores continuaron con determinación su largo camino.",
                        feedback: "¡Formidable! 'No obstante' contrapone la lluvia difícil con el esfuerzo de avanzar.",
                        correct: true
                    },
                    {
                        text: "Llovió intensamente todo el día además los exploradores continuaron su camino.",
                        feedback: "Falta un conector de oposición y la puntuación es débil.",
                        correct: false
                    }
                ],
                badge: "Arquitecto Textual"
            },
            {
                id: 5,
                title: "Nivel 5: La Gran Obra Maestra (Nivel 6°)",
                subtitle: "Construcción completa de texto descriptivo y argumentativo",
                icon: "fa-scroll",
                color: "emerald",
                description: "Combina sustantivos precisos, adjetivos, adverbios clasificables, preposiciones y conectores en un texto amplio.",
                baseSentence: "Texto básico inicial: 'Los científicos descubrieron una cueva. Tenía pinturas. Era muy importante.'",
                taskPrompt: "Selecciona el texto ampliado que demuestra un nivel de redacción avanzado propio de sexto grado:",
                options: [
                    {
                        text: "Ayer, en una remota región montañosa, los científicos descubrieron pacientemente una misteriosa cueva ancestral. Esta cueva albergaba fascinantes pinturas rupestres en sus frías paredes; por lo tanto, este hallazgo representa un avance extraordinario para la arqueología moderna.",
                        feedback: "¡IMPRESIONANTE! Has logrado un texto rico en adjetivos, adverbios de tiempo y modo, preposiciones y un conector consecutivo perfecto.",
                        correct: true
                    },
                    {
                        text: "Los científicos fueron a la cueva rápido y vieron pinturas viejas porque era importante.",
                        feedback: "El vocabulario sigue siendo plano e impropio de un texto complejo de 6° grado.",
                        correct: false
                    }
                ],
                badge: "Gran Escritor 6° Primaria"
            }
        ];

        // EXPRESS MODE DATA BANK (30s Timed Challenge)
        const EXPRESS_QUESTIONS = [
            { text: "El detective caminó <span class='underline text-purple-400 font-bold'>lentamente</span> hacia la escena.", answer: "Adverbio", hint: "Modifica al verbo caminó (Adverbio de modo)" },
            { text: "Estudiamos mucho para el examen, <span class='underline text-pink-400 font-bold'>sin embargo</span>, las preguntas eran complejas.", answer: "Conector", hint: "Une dos oraciones contrastantes (Conector adversativo)" },
            { text: "El regalo está guardado <span class='underline text-amber-400 font-bold'>bajo</span> la mesa de centro.", answer: "Preposición", hint: "Indica ubicación o relación espacial (Preposición)" },
            { text: "<span class='underline text-purple-400 font-bold'>Mañana</span> entregaremos el proyecto de investigación.", answer: "Adverbio", hint: "Indica tiempo en que ocurre la acción (Adverbio de tiempo)" },
            { text: "Corrieron con entusiasmo <span class='underline text-amber-400 font-bold'>hasta</span> llegar a la meta.", answer: "Preposición", hint: "Indica límite espacial o temporal (Preposición)" },
            { text: "Llegaron temprano, <span class='underline text-pink-400 font-bold'>por lo tanto</span>, alcanzaron los mejores lugares.", answer: "Conector", hint: "Muestra una consecuencia directa (Conector consecutivo)" },
            { text: "El automóvil avanzaba <span class='underline text-purple-400 font-bold'>muy</span> rápido en la autopista.", answer: "Adverbio", hint: "Modifica a otro adverbio aumentando intensidad (Adverbio de cantidad)" }
        ];

        // Web Audio Synthesizer sound generator
        function playSound(type) {
            try {
                const ctx = new (window.AudioContext || window.webkitAudioContext)();
                const osc = ctx.createOscillator();
                const gain = ctx.createGain();
                osc.connect(gain);
                gain.connect(ctx.destination);

                if (type === 'success') {
                    osc.frequency.setValueAtTime(440, ctx.currentTime);
                    osc.frequency.exponentialRampToValueAtTime(880, ctx.currentTime + 0.3);
                    gain.gain.setValueAtTime(0.2, ctx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.3);
                    osc.start();
                    osc.stop(ctx.currentTime + 0.3);
                } else if (type === 'error') {
                    osc.type = 'sawtooth';
                    osc.frequency.setValueAtTime(220, ctx.currentTime);
                    osc.frequency.exponentialRampToValueAtTime(110, ctx.currentTime + 0.25);
                    gain.gain.setValueAtTime(0.2, ctx.currentTime);
                    gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.25);
                    osc.start();
                    osc.stop(ctx.currentTime + 0.25);
                }
            } catch (e) {
                // Silently ignore if audio isn't permitted by browser policy
            }
        }

        // Trigger Canvas Confetti integration
        function triggerConfetti() {
            if (typeof confetti === 'function') {
                confetti({
                    particleCount: 100,
                    spread: 70,
                    origin: { y: 0.6 }
                });
            }
        }

        // Switch Active App Tab
        window.switchTab = function(tabName) {
            document.querySelectorAll('.tab-view').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.nav-btn').forEach(el => {
                el.classList.remove('bg-brand-600', 'text-white', 'shadow');
                el.classList.add('text-slate-400');
            });

            const activeView = document.getElementById(`view-${tabName}`);
            const activeTabBtn = document.getElementById(`tab-${tabName}`);

            if (activeView) activeView.classList.remove('hidden');
            if (activeTabBtn) {
                activeTabBtn.classList.add('bg-brand-600', 'text-white', 'shadow');
                activeTabBtn.classList.remove('text-slate-400');
            }

            if (tabName === 'profile') renderProfileTab();
            if (tabName === 'teacher') renderTeacherTab();
        };

        // Render Level Selector List in Adventure View
        function renderLevelsList() {
            const container = document.getElementById('levels-list');
            if (!container) return;

            container.innerHTML = GAME_LEVELS.map(lvl => {
                const isCompleted = studentState.completedLevels.includes(lvl.id);
                const isCurrent = studentState.level === lvl.id;
                
                return `
                    <div onclick="selectLevel(${lvl.id})" class="p-3.5 rounded-xl border transition cursor-pointer flex items-center justify-between ${
                        isCurrent 
                            ? 'bg-slate-800 border-sky-500 shadow-lg shadow-sky-500/10 ring-1 ring-sky-500' 
                            : isCompleted 
                                ? 'bg-slate-900/80 border-emerald-500/40 opacity-90' 
                                : 'bg-slate-900/50 border-slate-800 hover:border-slate-700'
                    }">
                        <div class="flex items-center gap-3">
                            <div class="w-9 h-9 rounded-lg flex items-center justify-center text-sm ${
                                isCompleted ? 'bg-emerald-500/20 text-emerald-400' : 'bg-slate-800 text-sky-400'
                            }">
                                <i class="fa-solid ${isCompleted ? 'fa-check-double' : lvl.icon}"></i>
                            </div>
                            <div>
                                <h4 class="font-bold text-xs text-white">${lvl.title}</h4>
                                <p class="text-[10px] text-slate-400">${lvl.subtitle}</p>
                            </div>
                        </div>
                        ${isCompleted ? '<span class="text-[10px] bg-emerald-500/20 text-emerald-400 px-2 py-0.5 rounded-full font-bold">Completado</span>' : ''}
                    </div>
                `;
            }).join('');
        }

        // Select and render mission workspace
        window.selectLevel = function(lvlId) {
            studentState.level = lvlId;
            renderLevelsList();
            const levelData = GAME_LEVELS.find(l => l.id === lvlId);
            const workspace = document.getElementById('mission-workspace');

            workspace.innerHTML = `
                <!-- Mission Title & Prompt -->
                <div class="space-y-3">
                    <div class="flex items-center justify-between">
                        <span class="text-xs font-bold px-3 py-1 rounded-full bg-${levelData.color}-500/20 text-${levelData.color}-400 border border-${levelData.color}-500/30">
                            ${levelData.title}
                        </span>
                        <span class="text-xs text-slate-400">Recompensa: +50 XP & Insignia</span>
                    </div>

                    <h3 class="font-display text-xl sm:text-2xl font-bold text-white">${levelData.subtitle}</h3>
                    <p class="text-xs sm:text-sm text-slate-300">${levelData.description}</p>
                </div>

                <!-- Sentence Preview Box -->
                <div class="bg-slate-900/90 p-5 rounded-xl border border-slate-800 space-y-2">
                    <span class="text-[10px] uppercase font-bold text-slate-400 tracking-wider">Texto Base Inicial:</span>
                    <p class="font-mono text-sm sm:text-base text-amber-300">"${levelData.baseSentence}"</p>
                </div>

                <!-- Interactive Question / Option Picker -->
                <div class="space-y-3">
                    <p class="text-xs font-bold text-slate-200">${levelData.taskPrompt}</p>
                    <div class="space-y-2.5">
                        ${levelData.options.map((opt, idx) => `
                            <button onclick="submitAnswer(${levelData.id}, ${idx})" class="w-full text-left p-4 rounded-xl bg-slate-900 border border-slate-800 hover:border-sky-500/50 hover:bg-slate-800/80 transition text-xs sm:text-sm text-slate-200 flex items-start gap-3 group">
                                <span class="w-6 h-6 rounded-full bg-slate-800 group-hover:bg-sky-500 group-hover:text-white flex items-center justify-center text-xs font-bold shrink-0 transition">
                                    ${String.fromCharCode(65 + idx)}
                                </span>
                                <span>${opt.text}</span>
                            </button>
                        `).join('')}
                    </div>
                </div>

                <div id="feedback-box" class="hidden p-4 rounded-xl text-xs space-y-2"></div>
            `;
        };

        // Process Student Mission Answer
        window.submitAnswer = function(lvlId, optionIndex) {
            const levelData = GAME_LEVELS.find(l => l.id === lvlId);
            const selectedOpt = levelData.options[optionIndex];
            const feedbackBox = document.getElementById('feedback-box');

            feedbackBox.classList.remove('hidden', 'bg-emerald-950/80', 'border-emerald-500/50', 'text-emerald-200', 'bg-rose-950/80', 'border-rose-500/50', 'text-rose-200');

            if (selectedOpt.correct) {
                playSound('success');
                triggerConfetti();

                feedbackBox.classList.add('bg-emerald-950/80', 'border', 'border-emerald-500/50', 'text-emerald-200');
                feedbackBox.innerHTML = `
                    <div class="flex items-center gap-2 font-bold text-sm">
                        <i class="fa-solid fa-circle-check text-emerald-400 text-lg"></i>
                        <span>¡Respuesta Correcta!</span>
                    </div>
                    <p>${selectedOpt.feedback}</p>
                `;

                // Update Level & XP Progression
                if (!studentState.completedLevels.includes(lvlId)) {
                    studentState.completedLevels.push(lvlId);
                    studentState.xp += 50;
                    if (!studentState.badges.includes(levelData.badge)) {
                        studentState.badges.push(levelData.badge);
                    }
                }

                // Record learning history
                studentState.history.unshift({
                    date: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
                    activity: levelData.title,
                    score: "50 XP",
                    status: "Completado"
                });

                updateHeaderStats();
                renderLevelsList();
                saveState();

            } else {
                playSound('error');
                feedbackBox.classList.add('bg-rose-950/80', 'border', 'border-rose-500/50', 'text-rose-200');
                feedbackBox.innerHTML = `
                    <div class="flex items-center gap-2 font-bold text-sm">
                        <i class="fa-solid fa-circle-xmark text-rose-400 text-lg"></i>
                        <span>Sigue intentándolo</span>
                    </div>
                    <p>${selectedOpt.feedback}</p>
                `;
            }
        };

        let expressTimer = null;
        let expressTimeLeft = 30;
        let expressCurrentScore = 0;
        let expressCurrentQ = null;

        window.startExpressGame = function() {
            document.getElementById('express-start-card').classList.add('hidden');
            document.getElementById('express-game-card').classList.remove('hidden');

            expressTimeLeft = 30;
            expressCurrentScore = 0;
            document.getElementById('express-score').innerText = expressCurrentScore;
            document.getElementById('express-timer').innerText = expressTimeLeft;

            nextExpressQuestion();

            if (expressTimer) clearInterval(expressTimer);
            expressTimer = setInterval(() => {
                expressTimeLeft--;
                document.getElementById('express-timer').innerText = expressTimeLeft;

                if (expressTimeLeft <= 0) {
                    clearInterval(expressTimer);
                    endExpressGame();
                }
            }, 1000);
        };

        function nextExpressQuestion() {
            const randomIdx = Math.floor(Math.random() * EXPRESS_QUESTIONS.length);
            expressCurrentQ = EXPRESS_QUESTIONS[randomIdx];
            document.getElementById('express-sentence-box').innerHTML = expressCurrentQ.text;
        }

        window.answerExpress = function(selectedType) {
            if (selectedType === expressCurrentQ.answer) {
                playSound('success');
                expressCurrentScore += 10;
                document.getElementById('express-score').innerText = expressCurrentScore;
            } else {
                playSound('error');
            }
            nextExpressQuestion();
        };

        function endExpressGame() {
            playSound('success');
            triggerConfetti();

            if (expressCurrentScore > studentState.expressHighScore) {
                studentState.expressHighScore = expressCurrentScore;
            }

            studentState.xp += expressCurrentScore;
            studentState.history.unshift({
                date: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
                activity: "Modo Express 30s",
                score: `${expressCurrentScore} pts`,
                status: "Finalizado"
            });

            updateHeaderStats();
            saveState();

            document.getElementById('express-game-card').classList.add('hidden');
            document.getElementById('express-start-card').classList.remove('hidden');
            document.getElementById('express-high-score').innerText = studentState.expressHighScore;

            alert(`¡Tiempo Agotado! Lograste ${expressCurrentScore} puntos en la prueba rápida de velocidad gramatical.`);
        }

        // Profile Modal Actions
        window.openRegistrationModal = function() {
            document.getElementById('input-student-name').value = studentState.name || '';
            document.getElementById('input-student-group').value = studentState.group || 'A';
            document.getElementById('input-school-name').value = studentState.school || '';
            document.getElementById('modal-register').classList.remove('hidden');
        };

        window.closeRegistrationModal = function() {
            document.getElementById('modal-register').classList.add('hidden');
        };

        window.handleRegistrationSubmit = function(e) {
            e.preventDefault();
            studentState.name = document.getElementById('input-student-name').value;
            studentState.group = document.getElementById('input-student-group').value;
            studentState.school = document.getElementById('input-school-name').value;

            saveState();
            closeRegistrationModal();
            renderProfileTab();
            renderTeacherTab();
            triggerConfetti();
        };

        // Render Profile View Data
        function renderProfileTab() {
            document.getElementById('profile-name-display').innerText = studentState.name || "Alumno Desconocido";
            document.getElementById('profile-details-display').innerText = `${studentState.grade} • Grupo "${studentState.group}"`;
            document.getElementById('profile-school-display').innerText = studentState.school;
            document.getElementById('profile-xp-val').innerText = studentState.xp;
            document.getElementById('profile-level-val').innerText = studentState.completedLevels.length + 1;

            // Render badges grid
            const badgesGrid = document.getElementById('badges-grid');
            const allBadges = [
                { name: "Maestro del Detalle", desc: "Uso de adjetivos y sustantivos" },
                { name: "Cazador de Adverbios", desc: "Dominio de clases de adverbios" },
                { name: "Guía de Preposiciones", desc: "Relaciones sintácticas claras" },
                { name: "Arquitecto Textual", desc: "Uso de conectores lógicos" },
                { name: "Gran Escritor 6° Primaria", desc: "Redacción compleja de párrafos" }
            ];

            badgesGrid.innerHTML = allBadges.map(b => {
                const unlocked = studentState.badges.includes(b.name);
                return `
                    <div class="p-4 rounded-xl border text-center space-y-2 ${
                        unlocked ? 'bg-amber-500/10 border-amber-500/40 text-amber-300' : 'bg-slate-900/40 border-slate-800 text-slate-500'
                    }">
                        <div class="w-10 h-10 rounded-full mx-auto flex items-center justify-center text-lg ${
                            unlocked ? 'bg-amber-500 text-slate-950 font-bold' : 'bg-slate-800 text-slate-600'
                        }">
                            <i class="fa-solid fa-award"></i>
                        </div>
                        <div>
                            <p class="font-bold text-xs">${b.name}</p>
                            <p class="text-[10px] opacity-80">${b.desc}</p>
                        </div>
                    </div>
                `;
            }).join('');

            // History Log Table
            const historyBody = document.getElementById('history-table-body');
            if (studentState.history.length === 0) {
                historyBody.innerHTML = `<tr><td colspan="4" class="p-3 text-center text-slate-500">Sin historial registrado aún.</td></tr>`;
            } else {
                historyBody.innerHTML = studentState.history.map(item => `
                    <tr class="hover:bg-slate-800/40">
                        <td class="p-3">${item.date}</td>
                        <td class="p-3 font-semibold text-slate-200">${item.activity}</td>
                        <td class="p-3 text-amber-400 font-bold">${item.score}</td>
                        <td class="p-3"><span class="px-2 py-0.5 rounded bg-emerald-500/20 text-emerald-400 font-bold">${item.status}</span></td>
                    </tr>
                `).join('');
            }
        }

        // Render Teacher Evaluation Official Report Sheet
        function renderTeacherTab() {
            document.getElementById('report-date').innerText = `Fecha: ${new Date().toLocaleDateString('es-MX')}`;
            document.getElementById('rep-student-name').innerText = studentState.name;
            document.getElementById('rep-student-grade').innerText = `${studentState.grade} - Grupo "${studentState.group}"`;
            document.getElementById('rep-school-name').innerText = studentState.school;

            const progressPct = Math.round((studentState.completedLevels.length / GAME_LEVELS.length) * 100);
            document.getElementById('rep-level-mastery').innerText = progressPct >= 80 ? 'Destacado' : progressPct >= 40 ? 'Satisfactorio' : 'En Desarrollo';

            document.getElementById('rep-score-1').innerText = studentState.completedLevels.includes(2) ? '100%' : '50%';
            document.getElementById('rep-score-2').innerText = studentState.completedLevels.includes(1) ? '100%' : '50%';
            document.getElementById('rep-score-3').innerText = studentState.completedLevels.includes(3) && studentState.completedLevels.includes(4) ? '100%' : '60%';
            document.getElementById('rep-score-4').innerText = `${studentState.expressHighScore} pts`;
        }

        window.printOfficialReport = function() {
            window.print();
        };

        function updateHeaderStats() {
            document.getElementById('header-xp').innerText = studentState.xp;
            document.getElementById('header-level').innerText = studentState.completedLevels.length + 1;
        }

        function saveState() {
            if (window.saveStudentDataCloud) {
                window.saveStudentDataCloud(studentState);
            }
        }

        // App Initialization on Load
        window.onload = async function() {
            if (window.loadStudentDataCloud) {
                const loaded = await window.loadStudentDataCloud();
                if (loaded) {
                    studentState = { ...studentState, ...loaded };
                }
            }
            updateHeaderStats();
            renderLevelsList();
            selectLevel(1);
            document.getElementById('express-high-score').innerText = studentState.expressHighScore || 0;
        };
    </script>
</body>
</html>
