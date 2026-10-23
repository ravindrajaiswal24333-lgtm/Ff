# Ff<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <!-- Disables pinch-zooming and locks viewport to mobile dimensions -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover" />
  
  <!-- Hides browser address bar on iOS & Android -->
  <meta name="mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <meta name="theme-color" content="#000000" />

  <title>Free Fire Mobile</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Teko:wght@600;700&display=swap" rel="stylesheet">

  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      user-select: none;
      -webkit-user-select: none;
      touch-action: none;
      -webkit-touch-callout: none;
    }

    html, body {
      width: 100%;
      height: 100%;
      height: 100dvh;
      background: #000;
      overflow: hidden;
      position: fixed;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    }

    /* Edge-to-edge Fullscreen Game Frame */
    #mobileGameFrame {
      width: 100vw;
      height: 100dvh;
      border: none;
      display: block;
      background: #000;
    }

    /* Floating Notch-Safe Quick Settings Pill */
    #mobileMenuBtn {
      position: fixed;
      top: env(safe-area-inset-top, 8px);
      right: env(safe-area-inset-right, 12px);
      z-index: 9999;
      background: rgba(10, 12, 16, 0.85);
      border: 1px solid rgba(255, 184, 0, 0.6);
      color: #ffb800;
      padding: 5px 12px;
      border-radius: 20px;
      font-size: 0.75rem;
      font-weight: bold;
      letter-spacing: 0.5px;
      backdrop-filter: blur(8px);
    }

    /* Slide-out Mobile Tool Drawer */
    #mobileDrawer {
      position: fixed;
      top: 0;
      right: -260px;
      width: 240px;
      height: 100dvh;
      background: rgba(12, 15, 20, 0.95);
      border-left: 2px solid #ffb800;
      z-index: 10000;
      display: flex;
      flex-direction: column;
      padding: 20px;
      gap: 12px;
      transition: right 0.25s ease-out;
      backdrop-filter: blur(12px);
      color: #fff;
    }

    #mobileDrawer.active {
      right: 0;
    }

    .drawer-header {
      font-family: 'Teko', sans-serif;
      font-size: 1.5rem;
      color: #ffb800;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid #222;
      padding-bottom: 6px;
    }

    .drawer-btn {
      background: #1c222c;
      color: #fff;
      border: 1px solid #333d4b;
      padding: 10px;
      font-weight: 700;
      font-size: 0.85rem;
      border-radius: 6px;
      text-transform: uppercase;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
    }

    .drawer-btn:active {
      background: #ffb800;
      color: #000;
    }

    /* Forced Landscape Warning Screen */
    #landscapeAlert {
      display: none;
      position: fixed;
      inset: 0;
      background: #0a0c10;
      z-index: 99999;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 24px;
    }

    .rotate-icon {
      font-size: 3rem;
      margin-bottom: 15px;
      animation: spinPhone 2s infinite ease-in-out;
    }

    @keyframes spinPhone {
      0% { transform: rotate(0deg); }
      50% { transform: rotate(-90deg); }
      100% { transform: rotate(0deg); }
    }

    #landscapeAlert h2 {
      font-family: 'Teko', sans-serif;
      font-size: 2rem;
      color: #ffb800;
      letter-spacing: 1px;
    }

    #landscapeAlert p {
      color: #94a3b8;
      font-size: 0.85rem;
      margin-top: 6px;
      max-width: 260px;
    }

    /* Shows warning if phone is held upright in portrait */
    @media (orientation: portrait) {
      #landscapeAlert {
        display: flex;
      }
    }
  </style>
</head>
<body>

  <!-- Rotate Alert (Appears when phone is held vertically) -->
  <div id="landscapeAlert">
    <div class="rotate-icon">📱</div>
    <h2>ROTATE YOUR PHONE</h2>
    <p>Please rotate your device horizontally (landscape) to activate full-screen touch controls.</p>
  </div>

  <!-- Floating Settings Pill -->
  <div id="mobileMenuBtn" onclick="toggleDrawer()">
    ⚙ MENU
  </div>

  <!-- Touch Settings Drawer -->
  <div id="mobileDrawer">
    <div class="drawer-header">
      <span>SETTINGS</span>
      <span onclick="toggleDrawer()" style="cursor: pointer; font-size: 1.2rem;">✕</span>
    </div>
    <button class="drawer-btn" onclick="goFullscreen()">⛶ Fullscreen</button>
    <button class="drawer-btn" onclick="reloadStream()">🔄 Reload Game</button>
  </div>

  <!-- Real Free Fire Mobile Touch Stream -->
  <iframe 
    id="mobileGameFrame" 
    src="https://now.gg/play/garena-international-i-private-limited/2785/free-fire-battlegrounds" 
    allow="autoplay; fullscreen; pointer-lock; gamepad; microphone"
    scrolling="no">
  </iframe>

  <script>
    function toggleDrawer() {
      document.getElementById('mobileDrawer').classList.toggle('active');
    }

    function reloadStream() {
      const frame = document.getElementById('mobileGameFrame');
      frame.src = frame.src;
      toggleDrawer();
    }

    function goFullscreen() {
      const el = document.documentElement;
      if (el.requestFullscreen) {
        el.requestFullscreen();
      } else if (el.webkitRequestFullscreen) {
        el.webkitRequestFullscreen();
      }
      toggleDrawer();
    }
  </script>
</body>
</html>
