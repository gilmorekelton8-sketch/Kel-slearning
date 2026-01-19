<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>kel'slearning.hub</title>
    <style>
        /* --- CORE THEME --- */
        :root {
            --bg: #0f0f13;
            --card-bg: #1a1a24;
            --primary: #6c5ce7;
            --accent: #00cec9;
            --text: #ffffff;
            --font-main: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            --font-dyslexic: 'Comic Sans MS', 'Chalkboard SE', sans-serif;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            font-family: var(--font-main);
            margin: 0;
            display: flex;
            flex-direction: column;
            min-height: 100vh;
            cursor: default;
            overflow-x: hidden;
            transition: font-size 0.3s ease;
        }

        /* DYSLEXIA FONT MODE */
        body.dyslexia-mode { font-family: var(--font-dyslexic) !important; letter-spacing: 1px; }

        /* TEXT SIZES */
        body.text-small { font-size: 14px; }
        body.text-medium { font-size: 16px; }
        body.text-large { font-size: 20px; }

        /* PARTICLES & SCANS */
        #particles-js { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: -1; background: radial-gradient(circle at center, #1b1b2f 0%, #0f0f13 100%); }
        .scanlines { display: none; position: fixed; top: 0; left: 0; width: 100vw; height: 100vh; background: linear-gradient(to bottom, rgba(255,255,255,0), rgba(255,255,255,0) 50%, rgba(0,0,0,0.2) 50%, rgba(0,0,0,0.2)); background-size: 100% 4px; z-index: 9999; pointer-events: none; animation: scrollLines 10s linear infinite; }
        @keyframes scrollLines { from {background-position: 0 0;} to {background-position: 0 100%;} }

        /* FAKE ADDRESS BAR (NEW) */
        .system-address-bar {
            background: #000;
            padding: 8px 15px;
            display: flex;
            align-items: center;
            gap: 15px;
            border-bottom: 1px solid #333;
            font-family: monospace;
            font-size: 12px;
            z-index: 200;
        }
        .window-controls { display: flex; gap: 6px; }
        .win-dot { width: 10px; height: 10px; border-radius: 50%; background: #555; }
        .win-dot.red { background: #ff5f56; }
        .win-dot.yellow { background: #ffbd2e; }
        .win-dot.green { background: #27c93f; }
        
        .fake-url-box {
            background: #1a1a20;
            color: var(--accent);
            padding: 4px 15px;
            border-radius: 15px;
            flex: 1;
            display: flex;
            align-items: center;
            border: 1px solid #333;
        }
        .lock-icon { margin-right: 8px; font-size: 10px; }

        /* NEWS TICKER */
        .news-ticker {
            background: var(--primary); color: white; padding: 5px 0; overflow: hidden; white-space: nowrap; font-size: 0.9rem; font-weight: bold; border-bottom: 2px solid var(--accent);
        }
        .news-content { display: inline-block; animation: marquee 20s linear infinite; padding-left: 100%; }
        @keyframes marquee { 0% { transform: translate(0, 0); } 100% { transform: translate(-100%, 0); } }

        /* HEADER */
        header {
            background: rgba(24, 24, 37, 0.9); padding: 15px 40px; border-bottom: 3px solid var(--primary); display: flex; justify-content: space-between; align-items: center; box-shadow: 0 0 20px rgba(0,0,0, 0.5); position: relative; z-index: 100; backdrop-filter: blur(10px);
        }
        .logo { font-size: 26px; font-weight: 800; letter-spacing: 2px; text-transform: uppercase; text-shadow: 0 0 10px var(--primary); animation: pulseLogo 3s infinite; }
        .logo span { color: var(--primary); }
        .logo span.blue { color: var(--accent); }
        @keyframes pulseLogo { 0% { text-shadow: 0 0 10px var(--primary); } 50% { text-shadow: 0 0 25px var(--primary), 0 0 5px white; } 100% { text-shadow: 0 0 10px var(--primary); } }

        nav { display: flex; gap: 10px; align-items: center; }

        /* NAV BUTTONS */
        .nav-btn {
            background: rgba(0,0,0,0.3); border: 2px solid var(--accent); color: var(--accent); padding: 8px 18px; cursor: pointer; font-weight: bold; border-radius: 20px; transition: 0.3s;
        }
        .nav-btn:hover { background: var(--accent); color: #000; box-shadow: 0 0 20px var(--accent); transform: scale(1.05); }
        .login-btn { background: var(--primary); border-color: var(--primary); color: white; }
        
        /* SPECIAL HEADER BUTTONS */
        .credits-btn { border-color: #ffd32a; color: #ffd32a; }
        .credits-btn:hover { background: #ffd32a; color: black; box-shadow: 0 0 20px #ffd32a; }
        
        .menu-btn { background: transparent; border: none; color: white; font-size: 2rem; cursor: pointer; padding: 0 10px; transition: 0.3s; }
        .menu-btn:hover { color: var(--accent); transform: rotate(90deg); }

        /* DROPDOWN MENU */
        #dropdown-menu {
            display: none; position: absolute; top: 80px; right: 20px; background: rgba(26, 26, 36, 0.98); border: 1px solid var(--accent); border-radius: 10px; width: 240px; flex-direction: column; box-shadow: 0 0 30px rgba(0,206,201, 0.2); overflow: hidden; backdrop-filter: blur(5px); z-index: 200;
        }
        #dropdown-menu button { background: transparent; border: none; color: white; padding: 15px; text-align: left; cursor: pointer; border-bottom: 1px solid #333; transition: 0.2s; font-size: 0.95rem; }
        #dropdown-menu button:hover { background: var(--primary); padding-left: 20px; }
        .upload-play-btn { color: #00ff41 !important; font-weight: bold; }
        .upload-play-btn:hover { background: #00ff41 !important; color: black !important; }

        /* MAIN CONTENT */
        main { flex: 1; padding: 40px; max-width: 1200px; margin: 0 auto; width: 100%; box-sizing: border-box; z-index: 10; }

        .hero { text-align: center; margin-bottom: 50px; }
        .hero h1 { font-size: 3.5rem; margin: 0 0 10px 0; background: linear-gradient(to right, var(--primary), var(--accent)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .hero p { color: #ccc; font-size: 1.3rem; min-height: 1.5em; }
        .typing-cursor::after { content: '|'; animation: blink 1s infinite; }
        @keyframes blink { 50% { opacity: 0; } }

        /* GAME GRID */
        .game-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 30px; }
        .game-card {
            background: rgba(26, 26, 36, 0.8); border-radius: 15px; padding: 30px; text-align: center; border: 1px solid #444; transition: 0.4s; cursor: pointer; position: relative; overflow: hidden; backdrop-filter: blur(5px);
        }
        .game-card:hover { transform: translateY(-10px) scale(1.02); border-color: var(--primary); box-shadow: 0 15px 40px rgba(108, 92, 231, 0.3); }
        .game-icon { font-size: 50px; margin-bottom: 20px; display: block; filter: drop-shadow(0 0 10px rgba(255,255,255,0.3)); }
        .game-title { font-size: 1.4rem; font-weight: bold; margin-bottom: 10px; display: block; }
        .game-desc { color: #888; margin-bottom: 20px; display: block; font-size: 0.9rem; }
        .play-btn { background: linear-gradient(45deg, var(--primary), #8e44ad); color: white; border: none; padding: 10px 25px; border-radius: 25px; font-weight: bold; cursor: pointer; transition: 0.2s; }

        /* GAME WINDOW */
        #game-window { display: none; background: var(--card-bg); border-radius: 20px; padding: 40px; text-align: center; border: 2px solid var(--accent); box-shadow: 0 0 100px rgba(0,206,201, 0.2); position: relative; min-height: 500px; }
        .close-game { background: #ff4757; border: none; color: white; padding: 8px 20px; border-radius: 5px; cursor: pointer; position: absolute; top: 20px; right: 20px; font-weight: bold; z-index: 10; }

        /* SIMULATED CHAT */
        #chat-box {
            position: fixed; bottom: 20px; right: 20px; width: 300px; background: rgba(0,0,0,0.9); border: 1px solid var(--primary); border-radius: 10px; z-index: 500; display: flex; flex-direction: column; overflow: hidden; box-shadow: 0 0 20px rgba(0,0,0,0.8); transition: 0.3s; height: 40px; 
        }
        #chat-header { padding: 10px; background: var(--primary); cursor: pointer; font-weight: bold; display: flex; justify-content: space-between; }
        #chat-content { flex: 1; padding: 10px; overflow-y: auto; height: 250px; display: none; font-size: 0.9rem; }
        #chat-input-area { padding: 10px; border-top: 1px solid #333; display: none; }
        #chat-input { width: 70%; padding: 5px; background: #222; border: 1px solid #444; color: white; }
        #send-chat { width: 25%; background: var(--accent); border: none; cursor: pointer; color: black; font-weight: bold; }
        .chat-msg { margin-bottom: 8px; }
        .chat-user { color: var(--accent); font-weight: bold; }

        /* IFRAME */
        iframe.uploaded-game-frame { width: 100%; height: 600px; border: none; background: white; border-radius: 10px; }

        /* MODALS */
        .modal-overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.8); z-index: 1000; justify-content: center; align-items: center; backdrop-filter: blur(8px); }
        .modal-box { background: rgba(26, 26, 36, 0.95); padding: 30px; border-radius: 15px; width: 90%; max-width: 500px; border: 1px solid var(--primary); box-shadow: 0 0 50px rgba(108, 92, 231, 0.4); text-align: center; animation: modalPop 0.3s forwards; max-height: 90vh; overflow-y: auto; }
        @keyframes modalPop { from{transform: scale(0.8); opacity:0;} to {transform: scale(1); opacity:1;} }
        
        .modal-input { width: 100%; padding: 12px; margin: 10px 0; background: #0b0b0e; border: 1px solid #444; color: white; border-radius: 5px; box-sizing: border-box; outline: none; }
        .modal-btn { width: 100%; padding: 12px; background: var(--primary); color: white; border: none; border-radius: 5px; font-weight: bold; cursor: pointer; margin-top: 10px; }
        .modal-btn.secondary { background: #333; }
        
        /* AUTH TABS */
        .auth-tabs { display: flex; justify-content: space-around; margin-bottom: 20px; border-bottom: 1px solid #444; }
        .auth-tab { background: none; border: none; color: #888; font-size: 1.1rem; cursor: pointer; padding-bottom: 10px; font-weight: bold; }
        .auth-tab.active { color: var(--accent); border-bottom: 2px solid var(--accent); }

        /* SETTINGS SPECIFIC STYLES */
        .setting-group { border: 1px solid #333; padding: 15px; border-radius: 10px; margin-bottom: 15px; text-align: left; }
        .setting-group h3 { margin-top: 0; color: var(--accent); border-bottom: 1px solid #444; padding-bottom: 5px; font-size: 1rem; }
        .setting-row { display: flex; justify-content: space-between; align-items: center; margin: 10px 0; color: #ccc; }
        
        /* SLIDERS */
        input[type=range] { width: 100px; accent-color: var(--accent); }

        /* TOGGLE SWITCH (Pure CSS) */
        .switch { position: relative; display: inline-block; width: 40px; height: 20px; }
        .switch input { opacity: 0; width: 0; height: 0; }
        .slider { position: absolute; cursor: pointer; top: 0; left: 0; right: 0; bottom: 0; background-color: #333; transition: .4s; border-radius: 20px; }
        .slider:before { position: absolute; content: ""; height: 14px; width: 14px; left: 3px; bottom: 3px; background-color: white; transition: .4s; border-radius: 50%; }
        input:checked + .slider { background-color: var(--accent); }
        input:checked + .slider:before { transform: translateX(20px); }

        /* CREDITS SPECIAL STYLE */
        #credits-text { font-size: 2rem; font-weight: bold; background: linear-gradient(to right, #ffd32a, #ff9f43); -webkit-background-clip: text; -webkit-text-fill-color: transparent; animation: glow 2s infinite alternate; }
        @keyframes glow { from { text-shadow: 0 0 10px rgba(255, 211, 42, 0.5); } to { text-shadow: 0 0 30px rgba(255, 211, 42, 0.8); } }

        /* CLICK SPARKLE */
        .sparkle { position: absolute; width: 10px; height: 10px; background: var(--accent); border-radius: 50%; pointer-events: none; animation: pop 0.6s ease-out forwards; z-index: 9999; }
        @keyframes pop { 0% {transform: scale(1); opacity: 1;} 100% {transform: scale(3); opacity: 0;} }
        
        footer { text-align: center; padding: 20px; color: #555; font-size: 0.8rem; margin-top: auto; }
        
        /* INTERNAL GAMES CSS */
        .math-problem { font-size: 4rem; font-weight: bold; margin: 30px 0; }
        
        /* UPDATED MEMORY GRID FOR 16 CARDS */
        .memory-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; max-width: 500px; margin: 0 auto; }
        .mem-card { background: var(--primary); height: 80px; border-radius: 8px; cursor: pointer; display: flex; align-items: center; justify-content: center; font-size: 2rem; color: transparent; transition: 0.3s; transform-style: preserve-3d; }
        .mem-card.flipped { background: white; color: black; transform: rotateY(180deg); }
        
        /* TIC TAC TOE RAINBOW */
        .ttt-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; max-width: 300px; margin: 20px auto; }
        .ttt-cell { background: #222; height: 90px; border-radius: 10px; cursor: pointer; font-size: 3.5rem; display: flex; align-items: center; justify-content: center; font-weight: bold; border: 2px solid #333; }
        
        /* RAINBOW ANIMATION */
        @keyframes rainbowAnim { 0% {background-position: 0% 50%;} 50% {background-position: 100% 50%;} 100% {background-position: 0% 50%;} }
        .rainbow-text {
            background: linear-gradient(270deg, #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #8b00ff);
            background-size: 400% 400%;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: rainbowAnim 4s ease infinite;
        }

    </style>
</head>
<body>

<input type="file" id="play-game-input" accept=".html,.htm" style="display: none;" onchange="handleGameFileLoad(this)">

<canvas id="particles-js"></canvas>
<div class="scanlines" id="crt-overlay"></div>

<div class="system-address-bar">
    <div class="window-controls">
        <div class="win-dot red"></div>
        <div class="win-dot yellow"></div>
        <div class="win-dot green"></div>
    </div>
    <div class="fake-url-box">
        <span class="lock-icon">🔒</span> https://kel'slearning.hub
    </div>
    <div style="color:#666;">Guest Mode</div>
</div>

<div class="news-ticker">
    <div class="news-content">
        📢 NEW: Secure Login Added | 🎮 Upload custom games in menu | 🏆 Leader: Kelton (9999 pts) | 💡 Settings upgraded | 🚀 Learning V3.8 Live
    </div>
</div>

<header>
    <div class="logo">KEL'S <span class="blue">LEARNING</span></div>
    <nav>
        <button class="nav-btn" onclick="showHome()">HOME</button>
        <button class="nav-btn" onclick="openAbout()">ABOUT US</button>
        <button class="nav-btn credits-btn" onclick="openCredits()">CREDITS</button>
        
        <button class="nav-btn login-btn" id="nav-auth-btn" onclick="openAuthModal()">LOGIN</button>
        <button class="nav-btn" onclick="openSettings()">⚙️</button>
        <button class="menu-btn" onclick="toggleMenu()">☰</button>
    </nav>
    
    <div id="dropdown-menu">
        <button class="upload-play-btn" onclick="triggerPlayUpload()">🎮 Upload & Play</button>
        <button onclick="openUploadModal()">📂 Cloud Storage</button>
        <button onclick="openAccountModal()">👤 Account Info</button>
        <button onclick="openBugModal()">🐞 Report Bugs</button>
        <button onclick="window.open('https://chatgpt.com', '_blank')">🤖 AI Assistant</button>
    </div>
</header>

<main id="main-content">
    <div id="home-view">
        <div class="hero">
            <h1>LEVEL UP YOUR BRAIN</h1>
            <p id="hero-text" class="typing-cursor">Initializing Audio Systems...</p>
        </div>
        <div class="game-grid">
            <div class="game-card" onclick="startMathGame()">
                <span class="game-icon">🧮</span>
                <span class="game-title">Math Blaster</span>
                <span class="game-desc">Calculate fast or crash!</span>
                <button class="play-btn">PLAY NOW</button>
            </div>
            
            <div class="game-card" onclick="startMemoryGame()">
                <span class="game-icon">🧠</span>
                <span class="game-title">Memory Matrix</span>
                <span class="game-desc">Hack the mainframe.</span>
                <button class="play-btn">PLAY NOW</button>
            </div>

            <div class="game-card" onclick="startTicTacToe()">
                <span class="game-icon">⭕❌</span>
                <span class="game-title">Tic-Tac-Toe</span>
                <span class="game-desc">Classic Strategy Duel</span>
                <button class="play-btn">PLAY NOW</button>
            </div>

            <div class="game-card" onclick="window.open('https://eaglecraft.pages.dev/', '_blank')">
                <span class="game-icon">⛏️</span>
                <span class="game-title">Minecraft</span>
                <span class="game-desc">Eaglecraft Web</span>
                <button class="play-btn">PLAY EXTERNAL</button>
            </div>

            <div class="game-card" onclick="window.open('https://voxiom.io/', '_blank')">
                <span class="game-icon">🔫</span>
                <span class="game-title">Voxiom.io</span>
                <span class="game-desc">Voxel Shooter</span>
                <button class="play-btn">PLAY EXTERNAL</button>
            </div>
        </div>
    </div>

    <div id="game-window">
        <button class="close-game" onclick="showHome()">EXIT GAME</button>
        <div id="game-content"></div>
    </div>
</main>

<div id="chat-box">
    <div id="chat-header" onclick="toggleChat()">
        <span>💬 Global Chat (3 Online)</span>
        <span id="chat-toggle-icon">▲</span>
    </div>
    <div id="chat-content">
        <div class="chat-msg"><span class="chat-user">System:</span> Welcome to the Hub!</div>
        <div class="chat-msg"><span class="chat-user">Bot_Alpha:</span> Anyone want to play Math Blaster?</div>
    </div>
    <div id="chat-input-area">
        <input type="text" id="chat-input" placeholder="Type message...">
        <button id="send-chat" onclick="sendMsg()">SEND</button>
    </div>
</div>

<div class="modal-overlay" id="settings-modal">
    <div class="modal-box">
        <h2>SYSTEM SETTINGS</h2>
        
        <div class="setting-group">
            <h3>🎨 Appearance</h3>
            <div style="display:flex; gap:10px; margin-bottom:10px;">
                <div style="width:30px; height:30px; border-radius:50%; background:#6c5ce7; cursor:pointer; border:2px solid white;" onclick="setTheme('#6c5ce7', '#00cec9')"></div>
                <div style="width:30px; height:30px; border-radius:50%; background:#ff4757; cursor:pointer; border:2px solid white;" onclick="setTheme('#ff4757', '#ffa502')"></div>
                <div style="width:30px; height:30px; border-radius:50%; background:#00ff41; cursor:pointer; border:2px solid white;" onclick="setTheme('#00ff41', '#008f11')"></div>
            </div>
            <div class="setting-row">
                <span>Retro CRT Mode</span>
                <label class="switch"><input type="checkbox" onchange="toggleCRT()"><span class="slider"></span></label>
            </div>
        </div>

        <div class="setting-group">
            <h3>👁️ Accessibility</h3>
            <div class="setting-row">
                <span>Text Size</span>
                <input type="range" min="1" max="3" value="2" onchange="changeTextSize(this.value)">
            </div>
            <div class="setting-row">
                <span>Dyslexia Friendly Font</span>
                <label class="switch"><input type="checkbox" onchange="toggleDyslexia()"><span class="slider"></span></label>
            </div>
        </div>

        <div class="setting-group">
            <h3>🔊 Audio</h3>
            <div class="setting-row">
                <span>Master Volume</span>
                <input type="range" min="0" max="100" value="50" id="vol-slider">
            </div>
            <div class="setting-row">
                <span>Sound Effects (SFX)</span>
                <label class="switch"><input type="checkbox" checked id="sfx-toggle"><span class="slider"></span></label>
            </div>
        </div>

        <div class="setting-group">
            <h3>🛠️ System</h3>
            <div class="setting-row">
                <span>Parental Controls</span>
                <label class="switch"><input type="checkbox"><span class="slider"></span></label>
            </div>
            <button onclick="alert('Cache Cleared!');" style="width:100%; background:#333; border:1px solid #555; padding:5px; color:#aaa; cursor:pointer;">CLEAR CACHE</button>
        </div>

        <button class="modal-btn secondary" onclick="closeModal('settings-modal')">SAVE & CLOSE</button>
    </div>
</div>

<div class="modal-overlay" id="credits-modal">
    <div class="modal-box" style="border-color: #ffd32a; box-shadow: 0 0 50px rgba(255, 211, 42, 0.3);">
        <h2>DEVELOPMENT CREDITS</h2>
        <br>
        <p>This learning platform was architected by:</p>
        <div id="credits-text">From: Kelton.Gilmore</div>
        <br>
        <p style="color:#aaa; font-size:0.9rem;">Lead Developer & Designer</p>
        <button class="modal-btn" style="background:#ffd32a; color:black;" onclick="closeModal('credits-modal')">CLOSE</button>
    </div>
</div>

<div class="modal-overlay" id="about-modal">
    <div class="modal-box">
        <h2>ABOUT US</h2>
        <p>Welcome to <strong>Kel's Learning</strong>.</p>
        <p style="text-align:left; color:#ccc; line-height:1.6;">
            We are dedicated to fusing high-performance gaming with educational content. 
            Our mission is to make learning math, memory, and strategy as addictive as your favorite video games.
            <br><br>
            <strong>Version:</strong> 3.8 (Hub ID Update)<br>
            <strong>Location:</strong> Global Server<br>
            <strong>Motto:</strong> "Play Smart."
        </p>
        <button class="modal-btn secondary" onclick="closeModal('about-modal')">CLOSE</button>
    </div>
</div>

<div class="modal-overlay" id="auth-modal">
    <div class="modal-box">
        <h2 id="auth-title">PLAYER ACCESS</h2>
        
        <div class="auth-tabs">
            <button class="auth-tab active" id="tab-login" onclick="switchAuthMode('login')">LOGIN</button>
            <button class="auth-tab" id="tab-signup" onclick="switchAuthMode('signup')">SIGN UP</button>
        </div>

        <div id="auth-container">
            <input type="email" id="auth-email" class="modal-input" placeholder="Enter Gmail Address (@gmail.com)">
            
            <input type="text" id="auth-user" class="modal-input" placeholder="Create Username" style="display:none;">
            
            <input type="password" id="auth-pass" class="modal-input" placeholder="Password">
            
            <button class="modal-btn" id="auth-submit-btn" onclick="handleAuthSubmit()">LOGIN</button>
        </div>

        <div id="logged-in-view" style="display:none;">
            <p>Welcome back, <span id="logged-user-display" style="color:var(--accent); font-weight:bold;">User</span>.</p>
            <button class="modal-btn" style="background:#ff4757" onclick="logout()">LOGOUT</button>
        </div>

        <button class="modal-btn secondary" onclick="closeModal('auth-modal')">CLOSE</button>
    </div>
</div>

<div class="modal-overlay" id="upload-modal">
    <div class="modal-box">
        <h2>CLOUD STORAGE</h2>
        <button class="modal-btn" onclick="document.getElementById('cloud-input').click()">SELECT FILE</button>
        <input type="file" id="cloud-input" style="display:none">
        <div id="file-list" style="margin-top:15px; color:#aaa;">No files.</div>
        <button class="modal-btn secondary" onclick="closeModal('upload-modal')">CLOSE</button>
    </div>
</div>

<div class="modal-overlay" id="account-modal">
    <div class="modal-box">
        <h2>ACCOUNT SETTINGS</h2>
        <p>Current User: <span id="acc-name" style="color:var(--accent); font-weight:bold;">Guest</span></p>
        
        <hr style="border:0; border-top:1px solid #333; margin:20px 0;">
        
        <h3 style="margin:0 0 10px 0; color:#ccc; font-size:1rem;">Update Credentials</h3>
        <p style="font-size:0.8rem; color:#888;">Leave blank if you don't want to change it.</p>
        
        <input type="text" id="update-user" class="modal-input" placeholder="New Username">
        <input type="password" id="update-pass" class="modal-input" placeholder="New Password">
        
        <button class="modal-btn" onclick="updateAccountInfo()">SAVE CHANGES</button>
        <button class="modal-btn secondary" onclick="closeModal('account-modal')">CLOSE</button>
    </div>
</div>

<div class="modal-overlay" id="bug-modal"><div class="modal-box"><h2>REPORT BUG</h2><input class="modal-input" placeholder="Issue"><button class="modal-btn" onclick="alert('Sent!');closeModal('bug-modal')">SEND</button><button class="modal-btn secondary" onclick="closeModal('bug-modal')">CLOSE</button></div></div>

<footer>&copy; 2026 Kel's Learning | Designed for Gamers</footer>

<script>
    /* =========================================
       NEW: SOUND EFFECTS ENGINE
       ========================================= */
    const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    
    function playClickSound() {
        if(!document.getElementById('sfx-toggle').checked) return;
        if(audioCtx.state === 'suspended') audioCtx.resume();

        const osc = audioCtx.createOscillator();
        const gainNode = audioCtx.createGain();
        
        osc.type = 'sine';
        osc.frequency.setValueAtTime(800, audioCtx.currentTime);
        osc.frequency.exponentialRampToValueAtTime(300, audioCtx.currentTime + 0.1);
        
        const vol = document.getElementById('vol-slider').value / 100;
        gainNode.gain.setValueAtTime(vol * 0.1, audioCtx.currentTime);
        gainNode.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.1);

        osc.connect(gainNode);
        gainNode.connect(audioCtx.destination);
        
        osc.start();
        osc.stop(audioCtx.currentTime + 0.1);
    }

    document.addEventListener('click', (e) => {
        if(e.target.tagName === 'BUTTON' || e.target.closest('.game-card') || e.target.tagName === 'A') {
            playClickSound();
        }
    });

    /* =========================================
       NEW: GMAIL AUTHENTICATION & DATABASE
       ========================================= */
    
    let isSignupMode = false;
    
    // Load users from browser memory (local database simulation)
    const getSavedUsers = () => JSON.parse(localStorage.getItem('kels_user_db')) || [];
    
    function switchAuthMode(mode) {
        isSignupMode = (mode === 'signup');
        
        // Visual toggle of tabs
        document.getElementById('tab-login').classList.toggle('active', !isSignupMode);
        document.getElementById('tab-signup').classList.toggle('active', isSignupMode);
        
        // Show/Hide Username field
        document.getElementById('auth-user').style.display = isSignupMode ? 'block' : 'none';
        
        // Change Button Text
        document.getElementById('auth-submit-btn').innerText = isSignupMode ? 'CREATE ACCOUNT' : 'LOGIN';
    }

    function handleAuthSubmit() {
        const email = document.getElementById('auth-email').value.toLowerCase().trim();
        const pass = document.getElementById('auth-pass').value;
        const username = document.getElementById('auth-user').value.trim();
        
        // 1. Validation: Must be Gmail
        if (!email.endsWith('@gmail.com')) {
            alert("❌ Error: You must use a valid @gmail.com address.");
            return;
        }

        if (pass.length < 3) {
            alert("❌ Error: Password is too short.");
            return;
        }

        const users = getSavedUsers();

        if (isSignupMode) {
            // SIGN UP LOGIC
            if (!username) { alert("❌ Error: Username required."); return; }
            
            // Check if email already exists
            const existing = users.find(u => u.email === email);
            if (existing) {
                alert("❌ This Gmail is already registered. Please Login.");
                return;
            }

            // Save new user
            users.push({ email: email, pass: pass, username: username });
            localStorage.setItem('kels_user_db', JSON.stringify(users));
            alert("✅ Account Created! Logging you in...");
            
            // Log them in immediately
            loginUser(username);

        } else {
            // LOGIN LOGIC
            const user = users.find(u => u.email === email && u.pass === pass);
            
            if (user) {
                alert("✅ Welcome back, " + user.username + "!");
                loginUser(user.username);
            } else {
                alert("❌ Login Failed: Wrong email or password.");
            }
        }
    }

    function loginUser(name) {
        localStorage.setItem('kels_current_user', name);
        updateUIForLogin(name);
        closeModal('auth-modal');
    }

    function updateUIForLogin(name) {
        document.getElementById('nav-auth-btn').innerText = name;
        document.getElementById('nav-auth-btn').classList.add('upload-play-btn'); // Turn green
        document.getElementById('acc-name').innerText = name;
        
        // Update modal view
        document.getElementById('auth-container').style.display = 'none';
        document.getElementById('logged-in-view').style.display = 'block';
        document.getElementById('logged-user-display').innerText = name;
        document.querySelector('.auth-tabs').style.display = 'none';
    }

    function logout() {
        localStorage.removeItem('kels_current_user');
        location.reload();
    }

    // Check login on load
    const savedUser = localStorage.getItem('kels_current_user');
    if (savedUser) {
        updateUIForLogin(savedUser);
    }

    /* =========================================
       NEW: ACCOUNT UPDATE FUNCTION
       ========================================= */
    function updateAccountInfo() {
        const currentUser = localStorage.getItem('kels_current_user');
        
        if(!currentUser) {
            alert("❌ You must be logged in to change settings.");
            return;
        }
        
        const newName = document.getElementById('update-user').value.trim();
        const newPass = document.getElementById('update-pass').value.trim();
        
        if(!newName && !newPass) {
            alert("⚠️ Please enter a new username or password.");
            return;
        }
        
        const users = getSavedUsers();
        const userIndex = users.findIndex(u => u.username === currentUser);
        
        if(userIndex > -1) {
            // Update Username
            if(newName) {
                // Check if taken
                if(users.some(u => u.username === newName)) {
                    alert("❌ Username already taken!");
                    return;
                }
                users[userIndex].username = newName;
                localStorage.setItem('kels_current_user', newName);
                updateUIForLogin(newName);
            }
            
            // Update Password
            if(newPass) {
                if(newPass.length < 3) { alert("❌ Password too short."); return; }
                users[userIndex].pass = newPass;
            }
            
            localStorage.setItem('kels_user_db', JSON.stringify(users));
            alert("✅ Account credentials updated successfully!");
            
            // Clear inputs
            document.getElementById('update-user').value = '';
            document.getElementById('update-pass').value = '';
            closeModal('account-modal');
        }
    }


    /* =========================================
       STANDARD UI FUNCTIONS
       ========================================= */
    function openCredits() { document.getElementById('credits-modal').style.display='flex'; }
    function openAbout() { document.getElementById('about-modal').style.display='flex'; }
    
    function changeTextSize(val) {
        document.body.classList.remove('text-small', 'text-medium', 'text-large');
        if(val == '1') document.body.classList.add('text-small');
        if(val == '2') document.body.classList.add('text-medium');
        if(val == '3') document.body.classList.add('text-large');
    }

    function toggleDyslexia() { document.body.classList.toggle('dyslexia-mode'); }
    function triggerPlayUpload() { document.getElementById('play-game-input').click(); toggleMenu(); }
    
    function handleGameFileLoad(input) {
        const file = input.files[0];
        if (file && (file.name.endsWith('.html') || file.name.endsWith('.htm'))) {
            const objectURL = URL.createObjectURL(file);
            document.getElementById('home-view').style.display = 'none';
            document.getElementById('game-window').style.display = 'block';
            document.getElementById('game-content').innerHTML = `<h2>Playing: ${file.name}</h2><iframe class="uploaded-game-frame" src="${objectURL}"></iframe>`;
        } else { alert("Please select an .html file."); }
    }

    let chatOpen = false;
    function toggleChat() {
        chatOpen = !chatOpen;
        const box = document.getElementById('chat-box');
        document.getElementById('chat-content').style.display = chatOpen ? 'block' : 'none';
        document.getElementById('chat-input-area').style.display = chatOpen ? 'flex' : 'none';
        box.style.height = chatOpen ? '350px' : '40px';
        document.getElementById('chat-toggle-icon').innerText = chatOpen ? '▼' : '▲';
    }
    function sendMsg() {
        const val = document.getElementById('chat-input').value;
        if(val) {
            const user = localStorage.getItem('kels_current_user') || "Guest";
            document.getElementById('chat-content').innerHTML += `<div class="chat-msg"><span class="chat-user">${user}:</span> ${val}</div>`;
            document.getElementById('chat-input').value = "";
            playClickSound(); 
        }
    }

    // Visuals
    const canvas = document.getElementById('particles-js');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth; canvas.height = window.innerHeight;
    let particles = [];
    class Particle {
        constructor() { this.x=Math.random()*canvas.width; this.y=Math.random()*canvas.height; this.size=Math.random()*2; this.vx=Math.random()-0.5; this.vy=Math.random()-0.5; }
        update() { this.x+=this.vx; this.y+=this.vy; if(this.x<0||this.x>canvas.width)this.vx*=-1; if(this.y<0||this.y>canvas.height)this.vy*=-1; }
        draw() { ctx.fillStyle='rgba(108, 92, 231, 0.5)'; ctx.beginPath(); ctx.arc(this.x,this.y,this.size,0,Math.PI*2); ctx.fill(); }
    }
    for(let i=0;i<50;i++) particles.push(new Particle());
    function animate() { ctx.clearRect(0,0,canvas.width,canvas.height); particles.forEach(p=>{p.update();p.draw()}); requestAnimationFrame(animate); }
    animate();

    document.addEventListener('click', (e)=>{
        const s = document.createElement('div'); s.classList.add('sparkle');
        s.style.left=e.pageX+'px'; s.style.top=e.pageY+'px'; document.body.appendChild(s);
        setTimeout(()=>s.remove(),600);
    });

    function showHome() { document.getElementById('home-view').style.display='block'; document.getElementById('game-window').style.display='none'; }
    function toggleMenu() { const m=document.getElementById('dropdown-menu'); m.style.display = m.style.display==='flex'?'none':'flex'; }
    function closeModal(id) { document.getElementById(id).style.display='none'; }
    function openSettings() { document.getElementById('settings-modal').style.display='flex'; }
    function openUploadModal() { document.getElementById('upload-modal').style.display='flex'; }
    function openAccountModal() { document.getElementById('account-modal').style.display='flex'; }
    function openBugModal() { document.getElementById('bug-modal').style.display='flex'; }
    
    // Open Auth Modal Logic
    function openAuthModal() { 
        const user = localStorage.getItem('kels_current_user');
        if(user) {
             // Already logged in
             document.getElementById('auth-container').style.display = 'none';
             document.querySelector('.auth-tabs').style.display = 'none';
             document.getElementById('logged-in-view').style.display = 'block';
        } else {
            // Not logged in
            document.getElementById('auth-container').style.display = 'block';
            document.querySelector('.auth-tabs').style.display = 'flex';
            document.getElementById('logged-in-view').style.display = 'none';
            switchAuthMode('login'); // Default to login
        }
        document.getElementById('auth-modal').style.display='flex'; 
    }

    let crt = false;
    function toggleCRT() { crt=!crt; document.getElementById('crt-overlay').style.display=crt?'block':'none'; }
    function setTheme(p, a) { document.documentElement.style.setProperty('--primary', p); document.documentElement.style.setProperty('--accent', a); }

    // Games
    const gc = document.getElementById('game-content');
    
    function startMathGame() {
        document.getElementById('home-view').style.display='none'; document.getElementById('game-window').style.display='block';
        let n1=Math.floor(Math.random()*20), n2=Math.floor(Math.random()*20);
        gc.innerHTML = `<div class="math-problem">${n1} + ${n2} = ?</div><input id="ans" class="modal-input" style="width:100px;text-align:center;">`;
        document.getElementById('ans').focus();
        document.getElementById('ans').onkeypress = (e) => { if(e.key=='Enter') { if(e.target.value == n1+n2) { alert("CORRECT!"); playClickSound(); } else alert("WRONG!"); startMathGame(); }};
    }
    
    // --- UPDATED TIC TAC TOE WITH RAINBOW TEXT ---
    function startTicTacToe() {
        document.getElementById('home-view').style.display='none'; document.getElementById('game-window').style.display='block';
        gc.innerHTML = `<h2>Tic Tac Toe</h2><div class="ttt-grid" id="ttt"></div>`;
        let b=['','','','','','','','',''], p='X';
        const render = () => { 
            document.getElementById('ttt').innerHTML = b.map((c,i)=>
                `<div class="ttt-cell" onclick="move(${i})"><span class="${c ? 'rainbow-text' : ''}">${c}</span></div>`
            ).join(''); 
        };
        window.move = (i) => { if(!b[i]){ b[i]=p; p=p=='X'?'O':'X'; playClickSound(); render(); } };
        render();
    }
    
    // --- UPDATED MEMORY GAME WITH MORE CARDS (16 Total) ---
    function startMemoryGame() {
        document.getElementById('home-view').style.display='none'; document.getElementById('game-window').style.display='block';
        gc.innerHTML = `<h2>Memory Matrix (Expert Mode)</h2><div class="memory-grid" id="mem"></div>`;
        
        // Extended items array for 16 cards (8 pairs)
        let items = ['A','A','B','B','C','C','D','D','E','E','F','F','G','G','H','H'].sort(()=>Math.random()-0.5);
        
        document.getElementById('mem').innerHTML = items.map((x,i)=>`<div class="mem-card" id="m${i}" onclick="mflip(${i},'${x}')">${x}</div>`).join('');
    }
    
    let picked = [];
    window.mflip = (i,v) => {
        let el = document.getElementById('m'+i);
        if(el.classList.contains('flipped') || picked.length>1) return;
        playClickSound();
        el.classList.add('flipped'); el.style.color='black';
        picked.push({i,v});
        if(picked.length==2) {
            setTimeout(()=>{
                if(picked[0].v != picked[1].v) {
                    document.getElementById('m'+picked[0].i).classList.remove('flipped'); document.getElementById('m'+picked[0].i).style.color='transparent';
                    document.getElementById('m'+picked[1].i).classList.remove('flipped'); document.getElementById('m'+picked[1].i).style.color='transparent';
                }
                picked = [];
            }, 800);
        }
    }

    // Hero Text Animation
    let txt = "Initializing Audio Systems... Access Granted.";
    let i = 0;
    document.getElementById("hero-text").innerHTML = "";
    function typeWriter() {
        if (i < txt.length) {
            document.getElementById("hero-text").innerHTML += txt.charAt(i);
            i++;
            setTimeout(typeWriter, 50);
        }
    }
    typeWriter();

</script>
</body>
</html>
