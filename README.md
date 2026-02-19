<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="theme-color" content="#0B3D2E">
    <meta name="background-color" content="#0A0E27">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="AgentPro">
    <meta name="mobile-web-app-capable" content="yes">
    <meta name="application-name" content="AgentPro Football">
    <meta name="msapplication-TileColor" content="#0B3D2E">
    <meta name="msapplication-tap-highlight" content="no">
    
    <title>AgentPro Football - Gestion d'Agents Sportifs</title>
    
    <!-- Favicon -->
    <link rel="icon" type="image/svg+xml" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect width='100' height='100' rx='20' fill='%230B3D2E'/><circle cx='50' cy='50' r='35' fill='%23CCFF00'/><path d='M50 20 L55 40 L75 40 L60 55 L65 75 L50 60 L35 75 L40 55 L25 40 L45 40 Z' fill='%230B3D2E'/></svg>">
    <link rel="apple-touch-icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 180 180'><rect width='180' height='180' rx='40' fill='%230B3D2E'/><circle cx='90' cy='90' r='60' fill='%23CCFF00'/><circle cx='90' cy='90' r='25' fill='none' stroke='%230B3D2E' stroke-width='8'/><path d='M90 30 L90 50 M90 130 L90 150 M30 90 L50 90 M130 90 L150 90' stroke='%230B3D2E' stroke-width='8' stroke-linecap='round'/></svg>">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        * {
            -webkit-tap-highlight-color: transparent;
            -webkit-touch-callout: none;
            touch-action: manipulation;
            box-sizing: border-box;
        }
        
        html {
            scroll-behavior: smooth;
        }
        
        body {
            background: linear-gradient(135deg, #0A0E27 0%, #151B3B 50%, #0B3D2E 100%);
            min-height: 100vh;
            font-family: 'Inter', sans-serif;
            overscroll-behavior-y: none;
            -webkit-overflow-scrolling: touch;
            color: white;
            margin: 0;
            padding: 0;
        }
        
        button, input, select, textarea {
            touch-action: manipulation;
            font-family: inherit;
        }
        
        .glass-panel {
            background: rgba(21, 27, 59, 0.85);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .neon-border {
            box-shadow: 0 0 20px rgba(204, 255, 0, 0.3), inset 0 0 20px rgba(204, 255, 0, 0.1);
        }
        
        .pitch-pattern {
            background-image: 
                linear-gradient(rgba(11, 61, 46, 0.3) 1px, transparent 1px),
                linear-gradient(90deg, rgba(11, 61, 46, 0.3) 1px, transparent 1px);
            background-size: 40px 40px;
        }
        
        .player-card {
            transition: transform 0.2s ease, box-shadow 0.2s ease;
            will-change: transform;
        }
        
        .player-card:active {
            transform: scale(0.98);
        }
        
        /* Mobile optimizations */
        @media (max-width: 768px) {
            .hide-mobile {
                display: none !important;
            }
            
            .mobile-full {
                width: 100vw;
                margin-left: -1rem;
                margin-right: -1rem;
                border-radius: 0;
            }
            
            .bottom-nav {
                position: fixed;
                bottom: 0;
                left: 0;
                right: 0;
                z-index: 50;
                padding-bottom: env(safe-area-inset-bottom, 0px);
            }
            
            .content-pb {
                padding-bottom: calc(80px + env(safe-area-inset-bottom, 0px));
            }
        }
        
        @media (min-width: 769px) {
            .bottom-nav {
                display: none;
            }
            .content-pb {
                padding-bottom: 2rem;
            }
        }
        
        @keyframes slideUp {
            from { transform: translateY(20px); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .animate-slide-up {
            animation: slideUp 0.3s ease-out;
        }
        
        .animate-fade-in {
            animation: fadeIn 0.2s ease-out;
        }
        
        .haptic:active {
            transform: scale(0.95);
        }
        
        .install-prompt {
            position: fixed;
            bottom: 100px;
            left: 50%;
            transform: translateX(-50%) translateY(200px);
            z-index: 60;
            transition: transform 0.3s ease;
            max-width: 90vw;
        }
        
        .install-prompt.show {
            transform: translateX(-50%) translateY(0);
        }
        
        .offline-bar {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            background: #ef4444;
            color: white;
            text-align: center;
            padding: 8px;
            z-index: 100;
            transform: translateY(-100%);
            transition: transform 0.3s;
            font-size: 14px;
        }
        
        .offline-bar.show {
            transform: translateY(0);
        }
        
        .swipe-container {
            touch-action: pan-y;
            overflow-x: hidden;
        }
        
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        
        ::-webkit-scrollbar-track {
            background: rgba(255,255,255,0.05);
        }
        
        ::-webkit-scrollbar-thumb {
            background: rgba(204, 255, 0, 0.3);
            border-radius: 3px;
        }
        
        .no-select {
            user-select: none;
            -webkit-user-select: none;
        }
        
        .skeleton {
            background: linear-gradient(90deg, rgba(255,255,255,0.05) 25%, rgba(255,255,255,0.1) 50%, rgba(255,255,255,0.05) 75%);
            background-size: 200% 100%;
            animation: shimmer 1.5s infinite;
        }
        
        @keyframes shimmer {
            0% { background-position: 200% 0; }
            100% { background-position: -200% 0; }
        }
        
        .safe-area-top {
            padding-top: env(safe-area-inset-top, 0px);
        }
        
        /* Custom colors */
        .text-neon-lime { color: #CCFF00; }
        .bg-neon-lime { background-color: #CCFF00; }
        .text-neon-cyan { color: #00F0FF; }
        .bg-neon-cyan { background-color: #00F0FF; }
        .text-deep-navy { color: #0A0E27; }
        .bg-deep-navy { background-color: #0A0E27; }
        .text-accent-gold { color: #FFD700; }
        .bg-accent-gold { background-color: #FFD700; }
        .border-neon-lime { border-color: #CCFF00; }
        .border-neon-cyan { border-color: #00F0FF; }
        
        .font-display { font-family: 'Space Grotesk', sans-serif; }
        
        /* Modal animations */
        .modal-enter {
            transform: translateY(100%);
        }
        .modal-enter-active {
            transform: translateY(0);
            transition: transform 0.3s ease-out;
        }
        .modal-exit {
            transform: translateY(0);
        }
        .modal-exit-active {
            transform: translateY(100%);
            transition: transform 0.3s ease-in;
        }
        
        /* Pull to refresh */
        .ptr-indicator {
            position: fixed;
            top: -60px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 40;
            transition: top 0.3s;
        }
        
        .ptr-loading {
            top: 20px !important;
        }
    </style>
    
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        display: ['Space Grotesk', 'sans-serif'],
                    },
                    colors: {
                        'pitch-green': '#0B3D2E',
                        'pitch-light': '#1A5F4A',
                        'neon-lime': '#CCFF00',
                        'neon-cyan': '#00F0FF',
                        'deep-navy': '#0A0E27',
                        'card-dark': '#151B3B',
                        'accent-gold': '#FFD700'
                    }
                }
            }
        }
    </script>
</head>
<body class="no-select">

    <!-- Offline Indicator -->
    <div id="offlineBar" class="offline-bar">
        <i class="fas fa-wifi-slash mr-2"></i> Mode hors ligne - Données synchronisées localement
    </div>

    <!-- Pull to Refresh Indicator -->
    <div id="ptrIndicator" class="ptr-indicator glass-panel rounded-full p-3 shadow-xl">
        <i class="fas fa-sync-alt animate-spin text-neon-lime text-xl"></i>
    </div>

    <!-- Top Navigation -->
    <nav class="fixed w-full z-50 glass-panel border-b border-white/10 safe-area-top">
        <div class="max-w-7xl mx-auto px-4 h-16 flex items-center justify-between">
            <div class="flex items-center gap-3 cursor-pointer" onclick="showDashboard()">
                <div class="w-10 h-10 rounded-full bg-gradient-to-br from-[#CCFF00] to-[#00F0FF] flex items-center justify-center shadow-lg">
                    <i class="fas fa-futbol text-deep-navy text-xl"></i>
                </div>
                <div>
                    <h1 class="font-display font-bold text-xl tracking-tight text-white">AGENT<span class="text-[#CCFF00]">PRO</span></h1>
                    <p class="text-[10px] text-gray-400 tracking-wider">FOOTBALL MANAGEMENT</p>
                </div>
            </div>
            
            <div class="flex items-center gap-3">
                <button onclick="toggleSync()" class="w-10 h-10 rounded-full bg-white/10 flex items-center justify-center relative active:scale-95 transition-transform" id="syncBtn">
                    <i class="fas fa-sync-alt text-sm text-white" id="syncIcon"></i>
                    <span id="syncBadge" class="absolute -top-1 -right-1 w-4 h-4 bg-[#CCFF00] rounded-full text-[10px] text-[#0A0E27] font-bold flex items-center justify-center hidden">3</span>
                </button>
                <button onclick="showProfile()" class="w-10 h-10 rounded-full bg-gradient-to-r from-[#00F0FF] to-blue-500 flex items-center justify-center active:scale-95 transition-transform">
                    <i class="fas fa-user text-sm text-white"></i>
                </button>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <main class="pt-20 px-4 max-w-7xl mx-auto content-pb swipe-container min-h-screen" id="mainContent">
        
        <!-- Dashboard Section -->
        <section id="dashboard" class="section-content space-y-6 animate-fade-in">
            <!-- Quick Stats Grid -->
            <div class="grid grid-cols-2 gap-3">
                <div class="glass-panel rounded-xl p-4 relative overflow-hidden active:scale-95 transition-transform cursor-pointer" onclick="showSection('finances')">
                    <div class="absolute -right-4 -top-4 w-20 h-20 bg-[#CCFF00]/20 rounded-full blur-2xl"></div>
                    <p class="text-gray-400 text-xs mb-1 uppercase tracking-wider">Portfolio</p>
                    <h3 class="text-xl font-bold text-white" id="totalValue">€127.5M</h3>
                    <p class="text-[#CCFF00] text-xs mt-1 flex items-center gap-1">
                        <i class="fas fa-arrow-up text-[10px]"></i> 12.5%
                    </p>
                </div>
                
                <div class="glass-panel rounded-xl p-4 relative overflow-hidden active:scale-95 transition-transform cursor-pointer" onclick="showSection('transfers')">
                    <div class="absolute -right-4 -top-4 w-20 h-20 bg-[#00F0FF]/20 rounded-full blur-2xl"></div>
                    <p class="text-gray-400 text-xs mb-1 uppercase tracking-wider">Actifs</p>
                    <h3 class="text-xl font-bold text-white">5</h3>
                    <p class="text-[#00F0FF] text-xs mt-1">3 en négociation</p>
                </div>
            </div>

            <!-- Action Buttons -->
            <div class="grid grid-cols-4 gap-2">
                <button onclick="quickAction('scan')" class="glass-panel rounded-xl p-3 flex flex-col items-center gap-1 active:scale-95 transition-transform haptic">
                    <div class="w-10 h-10 rounded-full bg-[#CCFF00]/20 flex items-center justify-center mb-1">
                        <i class="fas fa-qrcode text-[#CCFF00]"></i>
                    </div>
                    <span class="text-[10px] text-gray-300">Scanner</span>
                </button>
                <button onclick="quickAction('call')" class="glass-panel rounded-xl p-3 flex flex-col items-center gap-1 active:scale-95 transition-transform haptic">
                    <div class="w-10 h-10 rounded-full bg-[#00F0FF]/20 flex items-center justify-center mb-1">
                        <i class="fas fa-phone text-[#00F0FF]"></i>
                    </div>
                    <span class="text-[10px] text-gray-300">Appeler</span>
                </button>
                <button onclick="openModal('addPlayer')" class="glass-panel rounded-xl p-3 flex flex-col items-center gap-1 active:scale-95 transition-transform haptic">
                    <div class="w-10 h-10 rounded-full bg-[#FFD700]/20 flex items-center justify-center mb-1">
                        <i class="fas fa-plus text-[#FFD700]"></i>
                    </div>
                    <span class="text-[10px] text-gray-300">Ajouter</span>
                </button>
                <button onclick="quickAction('share')" class="glass-panel rounded-xl p-3 flex flex-col items-center gap-1 active:scale-95 transition-transform haptic">
                    <div class="w-10 h-10 rounded-full bg-purple-500/20 flex items-center justify-center mb-1">
                        <i class="fas fa-share-alt text-purple-400"></i>
                    </div>
                    <span class="text-[10px] text-gray-300">Partager</span>
                </button>
            </div>

            <!-- Priority Players Carousel -->
            <div>
                <div class="flex justify-between items-center mb-3">
                    <h3 class="font-bold text-lg text-white">Priorités du jour</h3>
                    <button onclick="showSection('players')" class="text-[#CCFF00] text-xs hover:underline">Voir tout</button>
                </div>
                <div class="flex gap-4 overflow-x-auto pb-4 snap-x snap-mandatory scrollbar-hide" id="priorityCarousel" style="scrollbar-width: none; -ms-overflow-style: none;">
                    <!-- Generated by JS -->
                </div>
            </div>

            <!-- Market Trend Mini -->
            <div class="glass-panel rounded-xl p-4">
                <div class="flex justify-between items-center mb-3">
                    <h3 class="font-bold text-white">Tendance Marché</h3>
                    <span class="text-xs text-gray-400">24h</span>
                </div>
                <div class="h-24 flex items-end gap-1" id="miniChart">
                    <!-- Bars generated by JS -->
                </div>
            </div>

            <!-- Upcoming Events -->
            <div class="glass-panel rounded-xl p-4">
                <h3 class="font-bold mb-3 text-white">Échéances proches</h3>
                <div class="space-y-3" id="upcomingEvents">
                    <!-- Generated by JS -->
                </div>
            </div>
        </section>

        <!-- Players Section -->
        <section id="players" class="section-content hidden space-y-4 animate-slide-up">
            <div class="flex items-center gap-3 mb-4">
                <button onclick="showDashboard()" class="w-10 h-10 rounded-full glass-panel flex items-center justify-center active:scale-95 transition-transform">
                    <i class="fas fa-arrow-left text-white"></i>
                </button>
                <h2 class="text-2xl font-bold text-white">Mes Joueurs</h2>
            </div>

            <div class="relative">
                <i class="fas fa-search absolute left-4 top-1/2 transform -translate-y-1/2 text-gray-400"></i>
                <input type="text" placeholder="Rechercher un joueur..." class="w-full glass-panel rounded-xl pl-12 pr-4 py-3 bg-[#0A0E27]/50 border border-white/10 focus:border-[#CCFF00] outline-none text-white placeholder-gray-500" onkeyup="filterPlayers(this.value)">
            </div>

            <div class="flex gap-2 overflow-x-auto pb-2" id="positionFilters" style="scrollbar-width: none;">
                <button class="px-4 py-2 rounded-full bg-[#CCFF00] text-[#0A0E27] font-bold text-sm whitespace-nowrap active:scale-95 transition-transform">Tous</button>
                <button class="px-4 py-2 rounded-full glass-panel text-sm whitespace-nowrap text-gray-300 active:scale-95 transition-transform" onclick="filterByPosition('GK')">Gardiens</button>
                <button class="px-4 py-2 rounded-full glass-panel text-sm whitespace-nowrap text-gray-300 active:scale-95 transition-transform" onclick="filterByPosition('DEF')">Défenseurs</button>
                <button class="px-4 py-2 rounded-full glass-panel text-sm whitespace-nowrap text-gray-300 active:scale-95 transition-transform" onclick="filterByPosition('MID')">Milieux</button>
                <button class="px-4 py-2 rounded-full glass-panel text-sm whitespace-nowrap text-gray-300 active:scale-95 transition-transform" onclick="filterByPosition('FWD')">Attaquants</button>
            </div>

            <div class="grid grid-cols-1 gap-3" id="playersList">
                <!-- Generated by JS -->
            </div>
        </section>

        <!-- Transfers Section -->
        <section id="transfers" class="section-content hidden space-y-4 animate-slide-up">
            <div class="flex items-center gap-3 mb-4">
                <button onclick="showDashboard()" class="w-10 h-10 rounded-full glass-panel flex items-center justify-center active:scale-95 transition-transform">
                    <i class="fas fa-arrow-left text-white"></i>
                </button>
                <h2 class="text-2xl font-bold text-white">Transferts</h2>
            </div>

            <div class="glass-panel rounded-xl p-1 flex text-sm bg-[#0A0E27]/30">
                <button class="flex-1 py-2 rounded-lg bg-white/10 font-medium text-white">Actifs</button>
                <button class="flex-1 py-2 rounded-lg text-gray-400 hover:text-white transition-colors">Historique</button>
                <button class="flex-1 py-2 rounded-lg text-gray-400 hover:text-white transition-colors">Prospects</button>
            </div>

            <div class="space-y-3" id="transfersList">
                <!-- Generated by JS -->
            </div>
        </section>

        <!-- Contracts Section -->
        <section id="contracts" class="section-content hidden space-y-4 animate-slide-up">
            <div class="flex items-center gap-3 mb-4">
                <button onclick="showDashboard()" class="w-10 h-10 rounded-full glass-panel flex items-center justify-cente# index.html
