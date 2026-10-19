<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Captain Ruby's Grand Treasure Expedition — Coordinate Quest</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&family=Pirata+One&family=Quicksand:wght@500;700&display=swap" rel="stylesheet">
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --ocean-deep: #0c4a6e;
            --ocean-mid: #0284c7;
            --sand-light: #fef3c7;
            --sand-gold: #f59e0b;
            --jungle-green: #166534;
            --coral-rose: #be123c;
            --sunset-orange: #ea580c;
        }
        body {
            font-family: 'Quicksand', sans-serif;
            background: linear-gradient(135deg, var(--ocean-deep), #0f172a);
            color: #1e293b;
            user-select: none;
            -webkit-user-select: none;
        }
        .font-pirate {
            font-family: 'Pirata One', cursive;
            letter-spacing: 1.5px;
        }
        .font-heading {
            font-family: 'Fredoka', sans-serif;
        }
        /* Enhanced Parchment Map */
        .parchment-bg {
            background-color: #fef3c7;
            background-image: 
                radial-gradient(#fde68a 12%, transparent 13%),
                radial-gradient(#fcd34d 12%, transparent 13%);
            background-size: 50px 50px;
            background-position: 0 0, 25px 25px;
            box-shadow: inset 0 0 60px rgba(120, 53, 15, 0.25), 0 15px 35px -8px rgba(0,0,0,0.5);
            border: 14px solid #78350f;
            border-image: linear-gradient(to bottom right, #b45309, #451a03, #b45309) 1 1 1 1;
        }
        /* Wooden Button */
        .btn-wood {
            background: linear-gradient(180deg, #d97706 0%, #78350f 100%);
            border: 3px solid #451a03;
            color: #fef9c3;
            text-shadow: 2px 2px 0px rgba(0,0,0,0.6);
            box-shadow: 0 6px 0px #2d1204, 0 10px 15px rgba(0,0,0,0.4);
            transition: all 0.15s ease;
        }
        .btn-wood:hover:not(:disabled) {
            background: linear-gradient(180deg, #f59e0b 0%, #92400e 100%);
            transform: translateY(-2px);
            box-shadow: 0 8px 0px #2d1204, 0 12px 20px rgba(0,0,0,0.4);
        }
        .btn-wood:active:not(:disabled) {
            transform: translateY(4px);
            box-shadow: 0 2px 0px #2d1204, 0 4px 6px rgba(0,0,0,0.4);
        }
        .btn-wood:disabled {
            opacity: 0.55;
            cursor: not-allowed;
            filter: grayscale(0.5);
        }
        /* Gold Button */
        .btn-gold {
            background: linear-gradient(180deg, #fcd34d 0%, #b45309 100%);
            border: 3px solid #78350f;
            color: #451a03;
            text-shadow: 0px 1px 0px rgba(255,255,255,0.4);
            box-shadow: 0 6px 0px #78350f, 0 10px 15px rgba(0,0,0,0.3);
            transition: all 0.15s ease;
        }
        .btn-gold:hover:not(:disabled) {
            background: linear-gradient(180deg, #fef08a 0%, #f59e0b 100%);
            transform: translateY(-2px);
            box-shadow: 0 8px 0px #78350f, 0 12px 20px rgba(0,0,0,0.3);
        }
        .btn-gold:active:not(:disabled) {
            transform: translateY(4px);
            box-shadow: 0 2px 0px #78350f, 0 4px 6px rgba(0,0,0,0.3);
        }
        /* Difficulty Buttons */
        .btn-diff {
            transition: all 0.2s ease;
            border-width: 3px;
        }
        .btn-diff.active {
            transform: scale(1.05);
            box-shadow: 0 0 15px rgba(251, 191, 36, 0.6);
        }
        /* Animations */
        @keyframes pulseGlow {
            0%, 100% { transform: scale(1); filter: drop-shadow(0 0 6px rgba(234, 179, 8, 0.8)); }
            50% { transform: scale(1.15); filter: drop-shadow(0 0 18px rgba(234, 179, 8, 1)); }
        }
        .animate-pulse-glow {
            animation: pulseGlow 1.8s infinite ease-in-out;
        }
        @keyframes floatIdle {
            0%, 100% { transform: translateY(0px) rotate(0deg); }
            50% { transform: translateY(-10px) rotate(1.5deg); }
        }
        .animate-float {
            animation: floatIdle 3.5s ease-in-out infinite;
        }
        @keyframes chestOpen {
            0% { transform: scale(0.8) rotate(0deg); }
            50% { transform: scale(1.1) rotate(-3deg); }
            100% { transform: scale(1) rotate(0deg); }
        }
        .animate-chest {
            animation: chestOpen 0.8s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
        }
        @keyframes sparkle {
            0%, 100% { opacity: 0.3; transform: scale(0.8); }
            50% { opacity: 1; transform: scale(1.2); }
        }
        .sparkle {
            animation: sparkle 1.5s infinite;
        }
        /* Map Styling */
        .grid-line {
            stroke: #9a7b4f;
            stroke-width: 1.5;
            stroke-dasharray: 4, 3;
        }
        .axis-line {
            stroke: #4a2810;
            stroke-width: 3.5;
            stroke-linecap: round;
        }
        .map-interactive-object {
            cursor: pointer;
            transition: transform 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        .map-interactive-object:hover {
            transform: scale(1.25);
        }
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #fef3c7;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb {
            background: #b45309;
            border-radius: 4px;
        }
        /* Slow spin */
        @keyframes spin-slow {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }
        .animate-spin-slow {
            animation: spin-slow 8s linear infinite;
        }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center p-2 sm:p-4">
    <div id="game-app" class="w-full max-w-5xl bg-slate-800/90 rounded-3xl shadow-2xl overflow-hidden border-4 border-amber-500 flex flex-col min-h-[680px] relative">
        
        <!-- Top Navigation -->
        <header class="bg-gradient-to-r from-amber-950 via-amber-800 to-amber-950 px-4 py-3 border-b-4 border-amber-500 flex justify-between items-center text-amber-100 z-10">
            <div class="flex items-center space-x-3">
                <i class="fa-solid fa-compass-drafting text-amber-400 text-2xl animate-spin-slow"></i>
                <h1 class="font-pirate text-2xl sm:text-3xl tracking-wider text-amber-300">Captain Ruby's Expedition</h1>
            </div>
            <div id="progress-container" class="hidden flex items-center space-x-2 bg-amber-950/80 px-3 py-1.5 rounded-full border border-amber-600/60">
                <span class="text-xs sm:text-sm font-bold uppercase tracking-wider text-amber-400 mr-1">Progress:</span>
                <div class="flex space-x-1.5" id="progress-badges">
                    <!-- Badges inserted dynamically -->
                </div>
            </div>
            <div class="flex gap-2">
                <button id="btn-audio-toggle" onclick="toggleMute()" class="px-2.5 py-1.5 bg-amber-900/80 hover:bg-amber-800 rounded-lg border border-amber-500 text-amber-300 text-xs font-bold transition flex items-center gap-1.5">
                    <i id="audio-icon" class="fa-solid fa-volume-high text-sm"></i>
                    <span class="hidden sm:inline">Sound</span>
                </button>
            </div>
        </header>

        <main class="flex-1 flex flex-col relative overflow-hidden">
            <!-- WELCOME SCREEN -->
            <section id="screen-welcome" class="absolute inset-0 flex flex-col items-center justify-between p-4 sm:p-8 bg-cover bg-center text-center transition-all duration-500 z-10" style="background-image: radial-gradient(circle, rgba(12,74,110,0.6) 0%, rgba(15,23,42,0.9) 100%), url('https://images.unsplash.com/photo-1507525428034-b723cf961d3e?auto=format&fit=crop&w=1200&q=80');">
                <div class="mt-2 sm:mt-4 space-y-3 max-w-2xl">
                    <span class="px-4 py-1.5 bg-amber-500/20 text-amber-300 border border-amber-400/40 rounded-full text-xs sm:text-sm font-semibold tracking-wide uppercase backdrop-blur-md inline-block">
                        Year 4 Maths • Coordinate Adventure • 5 Levels
                    </span>
                    <h2 class="font-pirate text-3xl sm:text-5xl text-amber-300 drop-shadow-[0_4px_8px_rgba(0,0,0,0.9)]">
                        Captain Ruby's Grand Treasure Expedition
                    </h2>
                    <p class="text-sky-100 text-sm sm:text-lg font-medium drop-shadow-md">
                        Ahoy, Explorer! Navigate the mysterious islands using your coordinate skills. <br>
                        Unlock ancient relics, cross the Shark Channel, and claim the Crown Jewel!
                    </p>
                </div>

                <!-- Difficulty Selection -->
                <div class="w-full max-w-md bg-slate-900/60 p-4 rounded-2xl border border-amber-600/50 backdrop-blur-md">
                    <p class="text-amber-300 font-bold text-sm mb-3">Choose Your Challenge Level:</p>
                    <div class="grid grid-cols-3 gap-2">
                        <button onclick="setDifficulty('easy')" id="diff-easy" class="btn-diff bg-emerald-700 hover:bg-emerald-600 text-white py-2 px-3 rounded-xl font-heading text-sm border-emerald-400 active">
                            🌿 Easy<br><span class="text-xs opacity-80">Grid 0–5</span>
                        </button>
                        <button onclick="setDifficulty('medium')" id="diff-medium" class="btn-diff bg-amber-600 hover:bg-amber-500 text-white py-2 px-3 rounded-xl font-heading text-sm border-amber-300">
                            🏝️ Medium<br><span class="text-xs opacity-80">Grid 0–8</span>
                        </button>
                        <button onclick="setDifficulty('hard')" id="diff-hard" class="btn-diff bg-rose-700 hover:bg-rose-600 text-white py-2 px-3 rounded-xl font-heading text-sm border-rose-400">
                            👑 Hard<br><span class="text-xs opacity-80">Grid 0–10</span>
                        </button>
                    </div>
                </div>

                <!-- Captain Ruby -->
                <div class="my-2 flex flex-col items-center animate-float">
                    <div class="relative">
                        <div class="w-36 h-36 sm:w-44 sm:h-44 rounded-full bg-gradient-to-b from-amber-200 to-amber-500 border-4 border-amber-300 shadow-2xl flex items-center justify-center overflow-hidden">
                            <svg viewBox="0 0 120 120" class="w-full h-full">
                                <circle cx="60" cy="60" r="60" fill="#38bdf8"/>
                                <path d="M 20 50 Q 60 15 100 50 C 85 45 35 45 20 50 Z" fill="#1e293b" />
                                <path d="M 30 46 Q 60 22 90 46" stroke="#f59e0b" stroke-width="3" fill="none"/>
                                <circle cx="60" cy="34" r="5" fill="#f8fafc"/>
                                <path d="M 57 39 L 63 39 L 62 42 L 58 42 Z" fill="#f8fafc"/>
                                <path d="M 35 50 Q 20 70 30 90" stroke="#b45309" stroke-width="8" fill="none" stroke-linecap="round"/>
                                <path d="M 85 50 Q 100 70 90 90" stroke="#b45309" stroke-width="8" fill="none" stroke-linecap="round"/>
                                <circle cx="60" cy="62" r="26" fill="#fbcfe8"/>
                                <circle cx="50" cy="58" r="7" fill="#0f172a"/>
                                <line x1="25" y1="48" x2="75" y2="65" stroke="#0f172a" stroke-width="2.5"/>
                                <circle cx="70" cy="58" r="3" fill="#0f172a"/>
                                <path d="M 54 74 Q 62 82 72 74" stroke="#0f172a" stroke-width="3" fill="none" stroke-linecap="round"/>
                                <path d="M 34 86 L 60 110 L 86 86" fill="#991b1b"/>
                                <path d="M 44 92 L 60 100 L 76 92" fill="#b91c1c"/>
                            </svg>
                        </div>
                        <span class="absolute -bottom-2 -right-2 bg-amber-400 text-amber-950 font-bold text-xs px-3 py-1 rounded-full border-2 border-amber-900 shadow-lg">
                            Captain Ruby
                        </span>
                    </div>
                </div>

                <div class="mb-4 w-full max-w-xs">
                    <button id="btn-start" onclick="startAdventure()" class="btn-gold w-full py-4 text-2xl font-pirate tracking-wider rounded-2xl flex items-center justify-center gap-3">
                        <i class="fa-solid fa-compass text-amber-900 text-2xl"></i>
                        Set Sail!
                    </button>
                </div>
            </section>

            <!-- CHALLENGE SCREEN -->
            <section id="screen-challenge" class="hidden absolute inset-0 flex flex-col lg:flex-row p-3 sm:p-5 gap-4 bg-slate-900 overflow-y-auto">
                <div class="flex-1 flex flex-col items-center justify-center">
                    <div class="parchment-bg rounded-2xl p-2 sm:p-4 w-full aspect-square relative flex flex-col justify-between shadow-2xl max-w-lg">
                        <div class="absolute top-3 right-3 opacity-30 pointer-events-none w-14 h-14 sm:w-20 sm:h-20">
                            <svg viewBox="0 0 100 100">
                                <polygon points="50,5 60,40 95,50 60,60 50,95 40,60 5,50 40,40" fill="#78350f"/>
                                <polygon points="50,5 50,50 95,50 50,60 50,95 40,50 5,50 50,40" fill="#b45309"/>
                                <circle cx="50" cy="50" r="8" fill="#fef08a" stroke="#78350f" stroke-width="2"/>
                            </svg>
                        </div>
                        <div class="w-full h-full relative">
                            <svg id="treasure-map-svg" class="w-full h-full overflow-visible">
                                <defs>
                                    <filter id="glow" x="-20%" y="-20%" width="140%" height="140%">
                                        <feGaussianBlur stdDeviation="4" result="blur" />
                                        <feComposite in="SourceGraphic" in2="blur" operator="over" />
                                    </filter>
                                </defs>
                                <g id="map-dynamic">
                                    <!-- Map content generated by JS -->
                                </g>
                            </svg>
                        </div>
                    </div>
                </div>

                <div class="w-full lg:w-80 flex flex-col justify-between gap-3 bg-amber-950/60 p-4 rounded-2xl border-2 border-amber-700/80 backdrop-blur-md">
                    <div class="flex items-start gap-3 bg-amber-100 p-3.5 rounded-xl border-2 border-amber-800 shadow-md">
                        <div class="w-12 h-12 rounded-full bg-amber-400 border-2 border-amber-900 flex-shrink-0 flex items-center justify-center">
                            <i class="fa-solid fa-user-ninja text-amber-950 text-2xl"></i>
                        </div>
                        <div>
                            <h3 class="font-bold text-amber-950 text-sm">Captain Ruby says:</h3>
                            <p id="captain-clue-text" class="text-xs sm:text-sm text-amber-900 font-medium leading-snug mt-0.5">
                                Loading clue...
                            </p>
                        </div>
                    </div>

                    <div id="multiple-choice-box" class="hidden flex flex-col gap-2 my-1">
                        <p class="text-xs font-bold text-amber-300 uppercase tracking-wider">Select Coordinates:</p>
                        <div id="mc-options"><!-- Generated by JS --></div>
                    </div>

                    <div id="feedback-box" class="min-h-[100px] p-3 rounded-xl bg-slate-900/90 border border-amber-600/50 flex flex-col justify-center">
                        <div id="feedback-content" class="text-xs sm:text-sm text-slate-300">
                            <span class="text-amber-400 italic">Click objects on the map to explore!</span>
                        </div>
                    </div>

                    <div class="mt-auto pt-2">
                        <button id="btn-next-challenge" onclick="nextChallenge()" disabled class="btn-gold w-full py-3 text-lg font-pirate tracking-wider rounded-xl flex items-center justify-center gap-2">
                            <span id="btn-next-text">Next Challenge</span>
                            <i class="fa-solid fa-arrow-right text-sm"></i>
                        </button>
                    </div>
                </div>
            </section>

            <!-- VICTORY SCREEN -->
            <section id="screen-victory" class="hidden absolute inset-0 flex flex-col items-center justify-between p-4 sm:p-8 bg-cover bg-center text-center transition-all duration-500 z-20" style="background-image: radial-gradient(circle, rgba(25,118,210,0.5) 0%, rgba(15,23,42,0.95) 100%), url('https://images.unsplash.com/photo-1518709268805-4e9042af9f23?auto=format&fit=crop&w=1200&q=80');">
                <div class="mt-2 space-y-2 max-w-xl">
                    <span class="px-4 py-1 bg-yellow-500/30 text-yellow-300 border border-yellow-400 rounded-full text-xs font-bold uppercase tracking-widest">
                        Mission Complete!
                    </span>
                    <h2 class="font-pirate text-4xl sm:text-6xl text-amber-300 drop-shadow-[0_5px_10px_rgba(0,0,0,0.9)]">
                        Crown Jewel Unlocked!
                    </h2>
                    <p class="text-sky-200 text-sm">You mastered coordinates like a true captain — X first, then Y, every time!</p>
                </div>

                <div class="relative my-4 flex flex-col items-center">
                    <div class="absolute -top-12 text-yellow-300 text-3xl sparkle">✨</div>
                    <div class="absolute -bottom-6 -left-12 text-amber-400 text-2xl animate-bounce">🪙</div>
                    <div class="absolute -top-6 -right-12 text-yellow-200 text-3xl sparkle">💎</div>
                    
                    <div class="w-48 h-48 sm:w-56 sm:h-56 animate-chest">
                        <svg viewBox="0 0 200 200" class="w-full h-full drop-shadow-[0_15px_25px_rgba(234,179,8,0.4)]">
                            <circle cx="100" cy="110" r="70" fill="url(#goldGlow)" opacity="0.8"/>
                            <defs>
                                <radialGradient id="goldGlow" cx="50%" cy="50%" r="50%">
                                    <stop offset="0%" stop-color="#fef08a"/>
                                    <stop offset="100%" stop-color="#d97706" stop-opacity="0"/>
                                </radialGradient>
                            </defs>
                            <rect x="40" y="90" width="120" height="70" rx="8" fill="#78350f" stroke="#451a03" stroke-width="4"/>
                            <rect x="50" y="100" width="100" height="50" fill="#a16207"/>
                            <circle cx="70" cy="90" r="10" fill="#fbbf24"/>
                            <circle cx="90" cy="85" r="12" fill="#f59e0b"/>
                            <circle cx="110" cy="82" r="11" fill="#fef08a"/>
                            <circle cx="130" cy="88" r="9" fill="#fbbf24"/>
                            <circle cx="100" cy="92" r="14" fill="#f59e0b"/>
                            <polygon points="80,82 85,72 90,82 85,92" fill="#ef4444"/>
                            <polygon points="115,80 122,72 129,80 122,88" fill="#3b82f6"/>
                            <polygon points="98,75 104,65 110,75 104,85" fill="#10b981"/>
                            <polygon points="100,55 108,40 116,55 108,70" fill="#a855f7"/>
                            <g transform="translate(100, 70) rotate(-35) translate(-100, -70)">
                                <path d="M 36 70 Q 100 20 164 70 Z" fill="#854d0e" stroke="#451a03" stroke-width="4"/>
                                <rect x="40" y="62" width="120" height="10" fill="#f59e0b"/>
                            </g>
                            <rect x="92" y="110" width="16" height="20" rx="3" fill="#f59e0b" stroke="#78350f" stroke-width="2"/>
                            <circle cx="100" cy="118" r="3" fill="#451a03"/>
                        </svg>
                    </div>
                    
                    <div class="bg-amber-950/80 border-2 border-amber-500/80 px-6 py-3 rounded-2xl max-w-md shadow-xl backdrop-blur-md mt-2">
                        <p id="victory-explanation" class="text-amber-200 text-xs sm:text-sm font-medium">
                            Amazing work! You completed all 5 missions and mastered coordinates! 🎉
                        </p>
                    </div>
                </div>

                <div class="mb-4 w-full max-w-md flex flex-col sm:flex-row gap-3">
                    <button onclick="restartGame()" class="btn-gold flex-1 py-3 text-xl font-pirate tracking-wider rounded-xl flex items-center justify-center gap-2">
                        <i class="fa-solid fa-rotate-right"></i>
                        Play Again
                    </button>
                    <button onclick="returnToWelcome()" class="btn-wood flex-1 py-3 text-xl font-pirate tracking-wider rounded-xl flex items-center justify-center gap-2">
                        <i class="fa-solid fa-house"></i>
                        Home Screen
                    </button>
                </div>
            </section>
        </main>
    </div>

    <script>
        // ========== GAME STATE ==========
        const gameState = {
            difficulty: 'easy',
            gridMax: 5,
            cellSize: 80,
            currentChallenge: 1,
            totalChallenges: 5,
            isAnsweredCorrectly: false,
            soundEnabled: true,
            objects: {},
            challenges: []
        };

        // ========== DIFFICULTY SETUP ==========
        function setDifficulty(level) {
            ['easy', 'medium', 'hard'].forEach(l => {
                const btn = document.getElementById(`diff-${l}`);
                btn.classList.remove('active', 'ring-2', 'ring-amber-300');
            });
            document.getElementById(`diff-${level}`).classList.add('active', 'ring-2', 'ring-amber-300');
            gameState.difficulty = level;
            gameState.gridMax = level === 'easy' ? 5 : level === 'medium' ? 8 : 10;
            gameState.cellSize = 400 / gameState.gridMax;
        }
        setDifficulty('easy');

        // ========== BUILD CHALLENGES ==========
        function buildChallenges() {
            const G = gameState.gridMax;
            gameState.objects = {
                'Palm Tree': { x: 1, y: 1, id: 'obj-palm', icon: 'palm' },
                'Compass': { x: 2, y: G-1, id: 'obj-compass', icon: 'compass' },
                'Golden Key': { x: Math.floor(G/2), y: Math.floor(G/2), id: 'obj-key', icon: 'key' },
                'Sailboat': { x: G-1, y: 1, id: 'obj-boat', icon: 'boat' },
                'Ancient Stele': { x: 1, y: G-2, id: 'obj-stele', icon: 'stele' },
                'Coral Cave': { x: G-2, y: G-2, id: 'obj-cave', icon: 'cave' },
                'Treasure Chest': { x: G, y: G-1, id: 'obj-chest', icon: 'chest' }
            };

            const mid = Math.floor(G/2);
            gameState.challenges = [
                {
                    id: 1,
                    title: 'Find the Key',
                    clue: `First, find the Golden Key at coordinates (${mid}, ${mid}) — the heart of the island!`,
                    target: 'Golden Key',
                    correctX: mid,
                    correctY: mid,
                    type: 'click'
                },
                {
                    id: 2,
                    title: 'Read the Compass',
                    clue: `Where is the Compass located? It sits high on the northern cliffs. Choose the correct coordinates.`,
                    target: 'Compass',
                    correctX: 2,
                    correctY: G-1,
                    type: 'choice'
                },
                {
                    id: 3,
                    title: 'Cross the Shark Channel',
                    clue: `Start at the Palm Tree (1,1). Move right to match the Sailboat's X-position at ${G}. Then sail up to the same Y as the Ancient Stele. Where do you land?`,
                    target: 'Coral Cave',
                    correctX: G-2,
                    correctY: G-2,
                    type: 'click',
                    explain: `From Palm Tree (1,1):<br>→ Right to Sailboat X = ${G} → adjust to ${G-2}<br>→ Up to Stele Y = ${G-2}<br>Destination = <strong>(${G-2}, ${G-2})</strong> — the Coral Cave!`
                },
                {
                    id: 4,
                    title: 'Follow the Map Lines',
                    clue: `From the Golden Key (${mid}, ${mid}): move right 3 units, then up 2 units. Which landmark do you reach?`,
                    target: 'Ancient Stele',
                    correctX: mid + 3,
                    correctY: mid + 2,
                    type: 'click',
                    explain: `(${mid} + 3, ${mid} + 2) = <strong>(${mid+3}, ${mid+2})</strong> — the Ancient Stele!`
                },
                {
                    id: 5,
                    title: 'The Crown Jewel',
                    clue: `Final treasure! Start at Sailboat (${G}, 1). Move left 0 units and up ${G-2} units. Click the Crown Jewel location!`,
                    target: 'Treasure Chest',
                    correctX: G,
                    correctY: G-1,
                    type: 'click',
                    explain: `X stays ${G}, Y = 1 + ${G-2} = ${G-1}<br>Treasure at <strong>(${G}, ${G-1})</strong> — well done, Captain!`
                }
            ];
            gameState.totalChallenges = gameState.challenges.length;
        }

        // ========== AUDIO ==========
        const AudioContext = window.AudioContext || window.webkitAudioContext;
        let audioCtx = null;
        function initAudio() { if (!audioCtx) audioCtx = new AudioContext(); }
        function playSound(type) {
            if (!gameState.soundEnabled) return;
            initAudio();
            if (audioCtx.state === 'suspended') audioCtx.resume();
            const osc = audioCtx.createOscillator();
            const gain = audioCtx.createGain();
            osc.connect(gain); gain.connect(audioCtx.destination);
            const now = audioCtx.currentTime;
            if (type === 'correct') {
                osc.type = 'triangle';
                osc.frequency.setValueAtTime(523.25, now);
                osc.frequency.setValueAtTime(659.25, now + 0.1);
                osc.frequency.setValueAtTime(783.99, now + 0.2);
                osc.frequency.setValueAtTime(1046.50, now + 0.3);
                gain.gain.setValueAtTime(0.2, now);
                gain.gain.exponentialRampToValueAtTime(0.001, now + 0.6);
                osc.start(now); osc.stop(now + 0.6);
            } else if (type === 'wrong') {
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(200, now);
                osc.frequency.linearRampToValueAtTime(110, now + 0.3);
                gain.gain.setValueAtTime(0.2, now);
                gain.gain.exponentialRampToValueAtTime(0.001, now + 0.4);
                osc.start(now); osc.stop(now + 0.4);
            } else if (type === 'click') {
                osc.type = 'sine';
                osc.frequency.setValueAtTime(440, now);
                gain.gain.setValueAtTime(0.08, now);
                gain.gain.exponentialRampToValueAtTime(0.001, now + 0.06);
                osc.start(now); osc.stop(now + 0.06);
            } else if (type === 'victory') {
                osc.type = 'triangle';
                [440, 554.37, 659.25, 880, 1046.5].forEach((f, i) => {
                    osc.frequency.setValueAtTime(f, now + i * 0.15);
                });
                gain.gain.setValueAtTime(0.25, now);
                gain.gain.exponentialRampToValueAtTime(0.001, now + 1.5);
                osc.start(now); osc.stop(now + 1.5);
            }
        }
        function toggleMute() {
            gameState.soundEnabled = !gameState.soundEnabled;
            document.getElementById('audio-icon').className = 
                gameState.soundEnabled ? 'fa-solid fa-volume-high text-sm' : 'fa-solid fa-volume-xmark text-sm';
            playSound('click');
        }

        // ========== NAVIGATION ==========
        function startAdventure() {
            playSound('click');
            buildChallenges();
            document.getElementById('screen-welcome').classList.add('hidden');
            document.getElementById('screen-challenge').classList.remove('hidden');
            document.getElementById('progress-container').classList.remove('hidden');
            loadChallenge(1);
        }
        function returnToWelcome() {
            playSound('click');
            ['screen-victory','screen-challenge'].forEach(id=>document.getElementById(id).classList.add('hidden'));
            document.getElementById('progress-container').classList.add('hidden');
            document.getElementById('screen-welcome').classList.remove('hidden');
        }
        function restartGame() {
            playSound('click');
            document.getElementById('screen-victory').classList.add('hidden');
            buildChallenges();
            loadChallenge(1);
        }

        // ========== MAP DRAWING ==========
        function buildMapSVG() {
            const G = gameState.gridMax;
            const S = gameState.cellSize;
            const originX = 50;
            const originY = 450;
            const totalW = originX + G * S + 40;
            const totalH = originY + 60;
            let html = `
                <svg viewBox="0 0 ${totalW} ${totalH}" class="w-full h-full overflow-visible">
                    <defs>
                        <filter id="glow" x="-20%" y="-20%" width="140%" height="140%">
                            <feGaussianBlur stdDeviation="4" result="blur"/>
                            <feComposite in="SourceGraphic" in2="blur" operator="over"/>
                        </filter>
                    </defs>
                    <path d="M 30,80 Q 80,20 ${G*40},40 T ${G*70},80 Q ${G*90},200 ${G*80},380 T ${G*50},460 Q ${G*20},460 30,320 T 30,80 Z" fill="#e2c993" opacity="0.5"/>
                    <g id="grid-lines">
                        <line x1="${originX}" y1="${originY}" x2="${originX + G*S}" y2="${originY}" class="axis-line"/>
                        <line x1="${originX}" y1="${originY}" x2="${originX}" y2="${originY - G*S}" class="axis-line"/>
            `;
            for (let i = 1; i <= G; i++) {
                html += `<line x1="${originX + i*S}" y1="${originY}" x2="${originX + i*S}" y2="${originY - G*S}" class="grid-line"/>`;
                html += `<line x1="${originX}" y1="${originY - i*S}" x2="${originX + G*S}" y2="${originY - i*S}" class="grid-line"/>`;
            }
            html += `</g><g id="axis-labels" font-family="'Fredoka', sans-serif" font-weight="bold" fill="#3a1c07">`;
            for (let i = 0; i <= G; i++) {
                html += `<text x="${originX + i*S}" y="${originY + 30}" text-anchor="middle" font-size="16">${i}</text>`;
                html += `<text x="${originX - 20}" y="${originY - i*S + 6}" text-anchor="end" font-size="16">${i}</text>`;
            }
            html += `<text x="${originX + G*S/2}" y="${originY + 50}" text-anchor="middle" font-size="18" fill="#78350f">X-axis</text>`;
            html += `<text x="15" y="${originY - G*S/2}" text-anchor="middle" font-size="18" fill="#78350f" transform="rotate(-90 15 ${originY - G*S/2})">Y-axis</text>`;
            html += `<circle cx="${originX}" cy="${originY}" r="5" fill="#78350f"/></g>`;

            // Helper: SVG coords from math (x,y)
            function pt(x,y) {
                return [originX + x*S, originY - y*S];
            }

            // Draw objects
            for (const [name, obj] of Object.entries(gameState.objects)) {
                const [px, py] = pt(obj.x, obj.y);
                html += `<g id="${obj.id}" class="map-interactive-object" onclick="handleObjectClick('${name}',${obj.x},${obj.y})" transform="translate(${px},${py})">
                    <path d="M-18,-18 L18,18 M18,-18 L-18,18" stroke="${obj.icon==='chest'?'#b45309':'#7f1d1d'}" stroke-width="${obj.icon==='chest'?'8':'5'}" stroke-linecap="round"/>
                    ${obj.icon==='chest'?'<path d="M-15,-15 L15,15 M15,-15 L-15,15" stroke="#fbbf24" stroke-width="5" stroke-linecap="round"/>':''}
                    <g transform="translate(0,-22) scale(0.85)">`;
                switch(obj.icon) {
                    case 'palm':
                        html += `<path d="M-4,20 Q2,0 8,-20" stroke="#78350f" stroke-width="7" fill="none" stroke-linecap="round"/>
                            <path d="M8,-20 Q-15,-35 -30,-20 Q-10,-10 8,-20 Z" fill="#15803d"/>
                            <path d="M8,-20 Q25,-40 40,-25 Q20,-10 8,-20 Z" fill="#16a34a"/>
                            <path d="M8,-20 Q-5,-45 5,-50 Q12,-25 8,-20 Z" fill="#22c55e"/>`;
                        break;
                    case 'compass':
                        html += `<circle cx="0" cy="0" r="20" fill="#fef08a" stroke="#854d0e" stroke-width="3"/>
                            <polygon points="0,-14 4,-2 0,0" fill="#dc2626"/>
                            <polygon points="0,14 4,2 0,0" fill="#475569"/>
                            <polygon points="-14,0 -2,-4 0,0" fill="#475569"/>
                            <polygon points="14,0 2,4 0,0" fill="#475569"/>`;
                        break;
                    case 'key':
                        html += `<circle cx="-12" cy="0" r="10" fill="none" stroke="#d97706" stroke-width="4"/>
                            <path d="M-2,0 L18,0 M10,0 L10,6 M15,0 L15,6" stroke="#d97706" stroke-width="4" stroke-linecap="round"/>`;
                        break;
                    case 'boat':
                        html += `<path d="M-22,5 C-15,20 15,20 22,5 Z" fill="#78350f" stroke="#451a03" stroke-width="2"/>
                            <line x1="0" y1="5" x2="0" y2="-20" stroke="#451a03" stroke-width="3"/>
                            <path d="M2,-18 L16,-8 L2,-2 Z" fill="#f8fafc"/>`;
                        break;
                    case 'stele':
                        html += `<path d="M-12,-25 L-12,15 L12,15 L12,-25 L0,-35 Z" fill="#94a3b8" stroke="#4b5563" stroke-width="2"/>
                            <text x="0" y="-5" text-anchor="middle" font-size="12" fill="#374151">☉</text>`;
                        break;
                    case 'cave':
                        html += `<ellipse cx="0" cy="0" rx="22" ry="16" fill="#1f2937" stroke="#78350f" stroke-width="3"/>
                            <ellipse cx="0" cy="0" rx="12" ry="9" fill="#020617"/>
                            <path d="M-8,-5 Q0,-12 8,-5" stroke="#fbbf24" stroke-width="2" fill="none"/>`;
                        break;
                    case 'chest':
                        html += `<rect x="-16" y="-6" width="32" height="22" rx="3" fill="#854d0e" stroke="#451a03" stroke-width="2"/>
                            <path d="M-16,-6 Q0,-18 16,-6 Z" fill="#a16207" stroke="#451a03" stroke-width="2"/>
                            <rect x="-4" y="-2" width="8" height="8" rx="1" fill="#f59e0b"/>
                            <circle cx="0" cy="2" r="1.5" fill="#451a03"/>`;
                        break;
                }
                html += `</g></g>`;
            }
            html += `<g id="path-overlay"></g></svg>`;
            document.getElementById('map-dynamic').innerHTML = html;
        }

        // ========== CHALLENGE LOADER ==========
        function loadChallenge(num) {
            gameState.currentChallenge = num;
            gameState.isAnsweredCorrectly = false;
            const ch = gameState.challenges[num-1];
            document.getElementById('btn-next-challenge').disabled = true;
            document.getElementById('path-overlay').innerHTML = '';
            document.getElementById('path-overlay').setAttribute('opacity','0');
            Object.values(gameState.objects).forEach(o=>{
                const el = document.getElementById(o.id);
                if(el) el.classList.remove('animate-pulse-glow');
            });

            // Progress badges
            let badgesHtml = '';
            for(let i=1; i<=gameState.totalChallenges; i++) {
                if(i<num) badgesHtml += `<div class="w-7 h-7 rounded-full flex items-center justify-center bg-emerald-600 text-white border border-emerald-400"><i class="fa-solid fa-check text-xs"></i></div>`;
                else if(i===num) badgesHtml += `<div class="w-7 h-7 rounded-full flex items-center justify-center bg-amber-400 text-amber-950 border-2 border-amber-300 shadow-md font-bold text-xs">${i}</div>`;
                else badgesHtml += `<div class="w-7 h-7 rounded-full flex items-center justify-center bg-slate-700 text-slate-400 border border-slate-600 font-bold text-xs">${i}</div>`;
            }
            document.getElementById('progress-badges').innerHTML = badgesHtml;

            document.getElementById('captain-clue-text').innerHTML = ch.clue;
            document.getElementById('btn-next-text').innerText = num === gameState.totalChallenges ? 'Claim Jewel!' : 'Next Challenge';
            document.getElementById('feedback-content').innerHTML = `<span class="text-amber-400 italic">Click the correct object on the map!</span>`;

            const mcBox = document.getElementById('multiple-choice-box');
            if(ch.type === 'choice') {
                mcBox.classList.remove('hidden');
                const opts = [
                    {label: 'A', x:ch.c
