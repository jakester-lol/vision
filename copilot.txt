<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>OCIA Terminal Boot</title>

<style>
    body {
        margin: 0;
        background: #000;
        color: #00ff9c;
        font-family: "Consolas", "Courier New", monospace;
        font-size: 14px;
        overflow: hidden;
    }

    .terminal {
        padding: 15px;
        white-space: pre-wrap;
        line-height: 1.4;
    }

    .green { color: #00ff9c; }
    .yellow { color: #f1c40f; }
    .red { color: #ff4c4c; }
    .cyan { color: #4cc3ff; }
    .white { color: #e0e0e0; }

    .signature {
        color: #00ff9c;
        text-align: center;
        margin-top: 20px;
        font-size: 13px;
        display: none;
    }
</style>
</head>
<body>

<div id="terminal" class="terminal"></div>

<div id="signature" class="signature">
<pre>
   ██████╗  ██████╗ ██╗ █████╗ 
  ██╔═══██╗██╔════╝ ██║██╔══██╗
  ██║   ██║██║      ██║███████║
  ██║   ██║██║   ██╗██║██╔══██║
  ╚██████╔╝╚██████╔╝██║██║  ██║
   ╚═════╝  ╚═════╝ ╚═╝╚═╝  ╚═╝

 Ohio Criminal Investigation Association
</pre>
</div>

<script>
const terminal = document.getElementById("terminal");
const signature = document.getElementById("signature");

// Boot log lines
const bootLines = [
    { text: "OCIA Secure Terminal v3.14.07\n", cls: "cyan" },
    { text: "Copyright (C) 2004-2026 OCIA Systems\n\n", cls: "white" },
    { text: "[INIT] Initializing kernel modules...\n", cls: "green" },
    { text: "[LOAD] Loading core drivers...........OK\n", cls: "green" },
    { text: "[LOAD] Loading encryption services....OK\n", cls: "green" },
    { text: "[LOAD] Mounting secure volume.........OK\n\n", cls: "green" },

    { text: "[ASSET] Loading asset pack: UI_CORE_01\n", cls: "yellow" },
    { text: "[ERROR] Asset validation failed. Retrying...\n\n", cls: "red" },

    { text: "[ASSET] Loading asset pack: UI_CORE_01\n", cls: "yellow" },
    { text: "[ERROR] CRC mismatch detected. Retrying...\n\n", cls: "red" },

    { text: "[ASSET] Loading asset pack: UI_CORE_01\n", cls: "yellow" },
    { text: "[ERROR] Timeout while accessing resource. Retrying...\n\n", cls: "red" },

    { text: "[ASSET] Loading asset pack: UI_CORE_01\n", cls: "yellow" },
    { text: "[SUCCESS] Asset pack verified and loaded.\n\n", cls: "green" },

    { text: "[NET] Establishing secure uplink........OK\n", cls: "green" },
    { text: "[AUTH] Authenticating terminal ID.......OK\n", cls: "green" },
    { text: "[SYS] Applying policy rules..............OK\n\n", cls: "green" },

    { text: "[BOOT] Finalizing system startup...\n", cls: "cyan" },
    { text: "[BOOT] OCIA Terminal ready.\n\n", cls: "green" }
];

// Function to print line
function printLine(line) {
    const span = document.createElement("span");
    span.className = line.cls;
    span.textContent = line.text;
    terminal.appendChild(span);
    window.scrollTo(0, document.body.scrollHeight);
}

// Function to simulate boot with random delays
function startBoot(index = 0) {
    if (index >= bootLines.length) {
        // All lines done, show signature
        signature.style.display = "block";
        setTimeout(() => {
            window.location.href = "management.html";
        }, 3000); // redirect after 3 seconds
        return;
    }

    printLine(bootLines[index]);

    // Random delay between 150ms and 900ms per line
    const randomDelay = Math.floor(Math.random() * 750) + 150;
    setTimeout(() => startBoot(index + 1), randomDelay);
}

// Start boot sequence
startBoot();
</script>

</body>
</html>


<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Unified Investigation Utilities</title>

<!-- Bootstrap -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

<!-- Font Awesome -->
<link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">

<style>
    body {
        background: #9fa3a7;
        font-family: Tahoma, "Segoe UI", sans-serif;
        margin: 0;
        padding: 0;
    }

    /* Old Windows / CAD window frame */
    .window {
        width: 700px;
        margin: 40px auto;
        border: 2px solid #3a3a3a;
        background: #c9c9c9;
        box-shadow:
            inset 1px 1px 0 #ffffff,
            inset -1px -1px 0 #707070,
            4px 4px 0 #4a4a4a;
    }

    /* Top title bar */
    .title-bar {
        background: linear-gradient(#5b5b5b, #2f2f2f);
        color: #eaeaea;
        padding: 6px 10px;
        font-size: 13px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        border-bottom: 2px solid #1f1f1f;
    }

    .title-bar .controls i {
        margin-left: 8px;
        color: #d0d0d0;
        cursor: default;
    }

    /* Inner content */
    .content {
        background: #efefef;
        padding: 10px;
        border: 2px solid #7b7b7b;
        box-shadow:
            inset 2px 2px 0 #ffffff,
            inset -2px -2px 0 #8a8a8a;
    }

    /* File list container */
    .file-container {
        background: #ffffff;
        border: 1px solid #6b6b6b;
        box-shadow:
            inset 1px 1px 0 #ffffff,
            inset -1px -1px 0 #9a9a9a;
        padding: 5px;
    }

    /* File row */
    .file-item {
        display: flex;
        align-items: center;
        padding: 5px 8px;
        text-decoration: none;
        color: #000;
        font-size: 13px;
        border: 1px solid transparent;
    }

    .file-item:hover {
        background: #cdd9e5;
        border: 1px dotted #000;
    }

    .file-icon {
        width: 22px;
        text-align: center;
        margin-right: 6px;
        color: #1f1f1f;
    }

    /* Bottom status bar */
    .status-bar {
        background: #bdbdbd;
        border-top: 2px solid #7b7b7b;
        padding: 4px 8px;
        font-size: 11px;
        color: #2b2b2b;
        box-shadow:
            inset 1px 1px 0 #ffffff,
            inset -1px -1px 0 #7a7a7a;
    }
</style>
</head>

<body>
<img src="ocia-logo.png" alt="OCIA Logo" style="position:fixed;top:10px;right:10px;width:220px;height:auto;z-index:9999;">
<div class="window">
    <div class="title-bar">
        <span>Ohio Criminal Investigation Association – Unified Investigation Utilities</span>
        <div class="controls">
            <i class="fa-solid fa-window-minimize"></i>
            <i class="fa-regular fa-square"></i>
            <i class="fa-solid fa-xmark"></i>
        </div>
    </div>

    <div class="content">
        <div class="file-container">

            <a href="oshp.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>oshp_documents.txt</div>
            </a>

            <a href="lcso.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>lcso_documents.txt</div>
            </a>

            <a href="opd.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>opd_documents.txt</div>
            </a>

            <a href="warrants.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>warrants.txt</div>
            </a>

            <a href="active_cases.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>active_cases.txt</div>
            </a>

            <a href="evidence.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>evidence.txt</div>
            </a>

            <a href="inactive_cases.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>inactive_cases.txt</div>
            </a>

            <a href="booting.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>management.exe</div>
            </a>

        </div>
    </div>

    <div class="status-bar">
        System Status: CONNECTED | Terminal ID: OCIA-UNIT-04 | Access Level: STANDARD
    </div>
</div>

</body>
</html>


<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Unified Investigation Utilities</title>

<!-- Bootstrap -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">

<!-- Font Awesome -->
<link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" rel="stylesheet">

<style>
    body {
        background: #9fa3a7;
        font-family: Tahoma, "Segoe UI", sans-serif;
        margin: 0;
        padding: 0;
    }

    /* Old Windows / CAD window frame */
    .window {
        width: 700px;
        margin: 40px auto;
        border: 2px solid #3a3a3a;
        background: #c9c9c9;
        box-shadow:
            inset 1px 1px 0 #ffffff,
            inset -1px -1px 0 #707070,
            4px 4px 0 #4a4a4a;
    }

    /* Top title bar */
    .title-bar {
        background: linear-gradient(#5b5b5b, #2f2f2f);
        color: #eaeaea;
        padding: 6px 10px;
        font-size: 13px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        border-bottom: 2px solid #1f1f1f;
    }

    .alt-title-bar {
        background: linear-gradient(#4075b9, #234a77);
        color: #eaeaea;
        padding: 6px 10px;
        font-size: 13px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        border-bottom: 2px solid #1f1f1f;
    }

    .title-bar .controls i {
        margin-left: 8px;
        color: #d0d0d0;
        cursor: default;
    }

    /* Inner content */
    .content {
        background: #efefef;
        padding: 10px;
        border: 2px solid #7b7b7b;
        box-shadow:
            inset 2px 2px 0 #ffffff,
            inset -2px -2px 0 #8a8a8a;
    }

    /* File list container */
    .file-container {
        background: #ffffff;
        border: 1px solid #6b6b6b;
        box-shadow:
            inset 1px 1px 0 #ffffff,
            inset -1px -1px 0 #9a9a9a;
        padding: 5px;
    }

    /* File row */
    .file-item {
        display: flex;
        align-items: center;
        padding: 5px 8px;
        text-decoration: none;
        color: #000;
        font-size: 13px;
        border: 1px solid transparent;
    }

    .file-item:hover {
        background: #cdd9e5;
        border: 1px dotted #000;
    }

    .file-icon {
        width: 22px;
        text-align: center;
        margin-right: 6px;
        color: #1f1f1f;
    }

    /* Bottom status bar */
    .status-bar {
        background: #bdbdbd;
        border-top: 2px solid #7b7b7b;
        padding: 4px 8px;
        font-size: 11px;
        color: #2b2b2b;
        box-shadow:
            inset 1px 1px 0 #ffffff,
            inset -1px -1px 0 #7a7a7a;
    }

    .closer:hover{
        background-color:red;
    }
</style>
</head>

<body>

<div class="window">
    <div class="title-bar">
        <span>Ohio Criminal Investigation Association – Unified Investigation Utilities</span>
        <div class="controls">
            <i class="fa-solid fa-window-minimize"></i>
            <i class="fa-regular fa-square"></i>
            <i class="fa-solid fa-xmark"></i>
        </div>
    </div>

    <div class="content">
        <div class="file-container">

            <a href="oshp.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>oshp_documents.txt</div>
            </a>

            <a href="lcso.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>lcso_documents.txt</div>
            </a>

            <a href="opd.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>opd_documents.txt</div>
            </a>

            <a href="warrants.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>warrants.txt</div>
            </a>

            <a href="active_cases.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>active_cases.txt</div>
            </a>

            <a href="evidence.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>evidence.txt</div>
            </a>

            <a href="inactive_cases.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>inactive_cases.txt</div>
            </a>

            <a href="management.html" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>management.txt</div>
            </a>

        </div>
    </div>

    <div class="status-bar">
        System Status: IDLE_TABBED_OUT | Terminal ID: OCIA-UNIT-04 | Access Level: STANDARD
    </div>
</div>

<div class="window">
    <div class="alt-title-bar">
        <span>Ohio Criminal Investigation Association – LCSO Documents</span>
        <div class="controls">
            <i class="fa-solid fa-window-minimize"></i>
            <i class="fa-regular fa-square"></i>
            <i onclick="window.location=('index.html')" class="fa-solid fa-xmark closer"></i>
        </div>
    </div>

    <div class="content">
        <div class="file-container">

            <a href="link" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>standard_operating.docx</div>
            </a>

            <a href="link" class="file-item">
                <div class="file-icon"><i class="fa-solid fa-file-lines"></i></div>
                <div>main_database.docx</div>
            </a>

        </div>
    </div>

    <div class="status-bar">
        System Status: CONNECTED | Terminal ID: OCIA-UNIT-04 | Access Level: STANDARD
    </div>
</div>

</body>
</html>


Understanding these pages and their styles, please make these styles on this webpage:

<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Server Name's CAD/MDT</title>
    <link rel="preconnect" href="https://cdn.jsdelivr.net">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css" rel="stylesheet">
    <link href="assets/css/style.css" rel="stylesheet">
  </head>
  <body class="auth-shell">
    <main class="auth-hero">
      <section class="auth-card reveal">
        <p class="eyebrow">Roleplay CAD / MDT</p>
        <h1 data-server-name>Empty Field</h1>
        <p class="lead" data-server-description>Empty Field</p>
        <div class="auth-actions">
          <a class="btn btn-primary" href="login.html"><i class="bi bi-box-arrow-in-right"></i> Sign in</a>
          <a class="btn btn-ghost" href="register.html"><i class="bi bi-person-plus"></i> Create account</a>
          <a class="btn btn-ghost" href="documentation.html"><i class="bi bi-file-earmark-text"></i> Documentation</a>
        </div>
      </section>
    </main>
    <footer class="powered-footer"><span class="powered-badge"><i class="bi bi-shield-check"></i> Powered by <strong>TrojanGFX</strong></span></footer>
    <script type="module" src="assets/js/auth-boot.js"></script>
<script type="module" src="assets/js/branding.js"></script>
<script src="assets/js/interactions.js"></script>
    <script type="module" src="assets/js/branding.js"></script>
    <script src="assets/js/interactions.js"></script>
    <script type="module" src="assets/js/redirect-if-authenticated.js"></script>
  </body>
</html>

<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Login</title>
    <link rel="preconnect" href="https://cdn.jsdelivr.net">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css" rel="stylesheet">
    <link href="assets/css/style.css" rel="stylesheet">
  </head>
  <body class="auth-shell">
    <main class="auth-hero compact">
      <form id="loginForm" class="auth-card reveal">
        <a class="mini-link" href="index.html"><i class="bi bi-arrow-left"></i> Home</a>
        <h1>Login</h1>
        <p class="lead"><span data-server-name>Server Name</span> CAD/MDT</p>
        <div id="authMessage" class="form-alert" role="alert" aria-live="polite" hidden></div>
        <label>Email<input required type="email" name="email" autocomplete="email" placeholder="you@example.com"></label>
        <label>Password<input required type="password" name="password" autocomplete="current-password" placeholder="••••••••"></label>
        <button class="btn btn-primary full" type="submit"><i class="bi bi-box-arrow-in-right"></i> Enter portal</button>
        <p class="muted center">Need access? <a href="register.html">Create an account</a></p>
      </form>
    </main>
    <footer class="powered-footer"><span class="powered-badge"><i class="bi bi-shield-check"></i> Powered by <strong>TrojanGFX</strong></span></footer>
    <div id="toastHost" class="toast-host"></div>
    <script type="module" src="assets/js/auth.js"></script>
    <script type="module" src="assets/js/branding.js"></script>
    <script src="assets/js/interactions.js"></script>
  </body>
</html>

<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Portal | Server Name</title>
    <link rel="preconnect" href="https://cdn.jsdelivr.net">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.css" rel="stylesheet">
    <link href="assets/css/style.css" rel="stylesheet">
  </head>
  <body class="portal-shell">
    <aside class="sidebar" id="sidebar">
      <a class="sidebar-brand" href="#dashboard" data-route="dashboard"><i class="bi bi-shield-shaded"></i><span>Server Name</span></a>
      <nav id="sidebarNav" class="side-nav"></nav>
      <div class="sidebar-powered"><span class="powered-badge"><i class="bi bi-shield-check"></i> Powered by <strong>TrojanGFX</strong></span></div>
      <button class="side-collapse" id="collapseSidebar" title="Toggle sidebar"><i class="bi bi-layout-sidebar-inset"></i></button>
    </aside>

    <section class="portal-frame">
      <header class="topbar">
        <button class="icon-btn mobile-only" id="mobileMenu" title="Menu"><i class="bi bi-list"></i></button>
        <div class="global-search"><i class="bi bi-search"></i><input id="globalSearch" placeholder="Search records, calls, units, people..."></div>
        <select id="roleSwitcher" class="role-switcher" title="Active role"></select>
        <a class="icon-btn" href="https://cad.trojan-gfx.com/documentation.php" title="Documentation"><i class="bi bi-file-earmark-text"></i></a>
        <button class="icon-btn" id="quickActionBtn" title="Quick action"><i class="bi bi-lightning-charge"></i></button>
        <button class="icon-btn" id="notificationsBtn" title="Notifications"><i class="bi bi-bell"></i><span id="notificationDot" class="pulse-dot"></span></button>
        <div class="profile-menu">
          <button class="profile-chip" id="profileBtn"><i class="bi bi-person-circle"></i><span id="profileName">Loading</span></button>
          <div class="dropdown" id="profileDropdown">
            <button data-open-modal="permissionsModal"><i class="bi bi-key"></i> Redeem permission code</button>
            <button data-route="settings"><i class="bi bi-sliders"></i> Settings</button>
            <button id="logoutBtn"><i class="bi bi-box-arrow-right"></i> Logout</button>
          </div>
        </div>
      </header>

      <main class="content">
        <section class="page-head reveal">
          <div>
            <p class="eyebrow" id="pageEyebrow">Unified operations</p>
            <h1 id="pageTitle">Dashboard</h1>
          </div>
          <div class="head-actions">
            <button class="btn btn-ghost" data-open-modal="permissionsModal"><i class="bi bi-key"></i> Redeem code</button>
            <button class="btn btn-primary" data-open-modal="quickModal"><i class="bi bi-plus-lg"></i> Quick create</button>
          </div>
        </section>
        <section id="app" class="app-region"></section>
      </main>
    </section>

    <div id="modalLayer" class="modal-layer" aria-hidden="true">
      <div class="modal-card">
        <button class="modal-close" data-close-modal title="Close"><i class="bi bi-x-lg"></i></button>
        <div id="modalContent"></div>
      </div>
    </div>
    <div id="toastHost" class="toast-host"></div>
    <script type="module" src="assets/js/portal.js"></script>
    <script src="assets/js/interactions.js"></script>
  </body>
</html>


style.css
:root{
  color-scheme:dark;
  --bg:#1e1f22;
  --panel:#2b2d31;
  --panel-strong:#313338;
  --line:rgba(255,255,255,.08);
  --line-strong:rgba(255,255,255,.16);
  --text:#f2f3f5;
  --muted:#b5bac1;
  --soft:#949ba4;
  --blue:#5865f2;
  --green:#3ba55d;
  --yellow:#faa81a;
  --red:#ed4245;
  --purple:#9b59ff;
  --orange:#f47b3f;
  --shadow:0 10px 30px rgba(0,0,0,.25);
  --radius: 10px;
  --fast: 120ms ease;
  --smooth: 120ms ease;
  font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
}

* { box-sizing: border-box; }
html { scroll-behavior: smooth; }
body {
  margin: 0;
  min-height: 100vh;
  background: var(--bg);
  color: var(--text);
  overflow-x: hidden;
}

a { color: var(--text); text-decoration: none; }
.bi { color: currentColor; }
button, input, select, textarea { font: inherit; }
button { cursor: pointer; }
input, select, textarea {
  width: 100%;
  color: var(--text);
  background: #1a1b1e !important;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  padding: .84rem .95rem;
  outline: none;
  transition: border-color var(--fast), background var(--fast);
}
input:focus, select:focus, textarea:focus {
  border-color: var(--line-strong);
  background: #2f96ff;
  box-shadow: 0 0 0 3px rgba(184, 220, 255, .22);
}
textarea { min-height: 104px; resize: vertical; }
::placeholder { color: rgba(255, 255, 255, .72); }
label { display: grid; gap: .42rem; color: var(--text); font-size: .88rem; }
.form-alert {
  border: 1px solid var(--red);
  border-left: 5px solid var(--red);
  border-radius: var(--radius);
  background: var(--red);
  color: var(--text);
  padding: .82rem .95rem;
  line-height: 1.45;
}
.form-alert.success {
  border-left-color: var(--green);
  border-color: var(--green);
  background: var(--green);
  color: var(--text);
}

.auth-shell { display: grid; place-items: center; padding: 24px; background: var(--bg); }
.auth-hero { width: min(860px, 100%); min-height: calc(100vh - 48px); display: grid; place-items: center; }
.auth-hero.compact { width: min(520px, 100%); }
.auth-card, .glass-card {
  position: relative;
  overflow: hidden;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: var(--panel);
  box-shadow: var(--shadow);
}
.auth-card {
  width: 100%;
  padding: clamp(24px, 4vw, 36px);
  display: grid;
  gap: 16px;
}
.auth-card::before, .glass-card::before { display: none; }
.brand-mark, .product-mark { display: none; }
h1, h2, h3, p { margin: 0; }
h1 { font-size: clamp(2rem, 5vw, 3.2rem); line-height: 1.05; letter-spacing: 0; }
.compact h1 { font-size: clamp(1.9rem, 5vw, 2.6rem); }
.lead { max-width: 680px; color: var(--text); font-size: .98rem; line-height: 1.55; }
.eyebrow { color: var(--text); text-transform: uppercase; letter-spacing: .16em; font-size: .72rem; font-weight: 800; }
.muted { color: var(--muted); }
.center { text-align: center; }
.mini-link { color: var(--text); display: inline-flex; align-items: center; gap: .45rem; width: fit-content; }
.auth-actions, .head-actions, .row-actions { display: flex; gap: 12px; flex-wrap: wrap; align-items: center; }
.btn {
  min-height: 42px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: .58rem;
  border: 1px solid transparent;
  border-radius: var(--radius);
  padding: .76rem 1rem;
  color: var(--text);
  font-weight: 800;
  transition: border-color var(--fast), background var(--fast);
}
.btn:hover { border-color: var(--line-strong); }
.btn-primary { background: #004fcf; color: var(--text); border-color: var(--line-strong); }
.btn-danger { background: var(--red); color: var(--text); border-color: var(--red); }
.btn-ghost { background: #1b87ff; border-color: var(--line); color: var(--text); }
.btn.full { width: 100%; }
.feature-grid { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 10px; margin-top: 10px; }
.feature-grid span {
  display: flex;
  align-items: center;
  gap: .55rem;
  padding: .9rem;
  color: var(--soft);
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
}

.powered-footer {
  position: fixed;
  left: 18px;
  right: 18px;
  bottom: 14px;
  display: flex;
  justify-content: center;
  z-index: 40;
  pointer-events: none;
}
.powered-badge {
  min-width: min(420px, calc(100vw - 36px));
  min-height: 38px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: .5rem;
  border: 1px solid var(--line-strong);
  border-radius: 999px;
  background: #1b87ff;
  color: var(--text);
  padding: .42rem 1.15rem;
  font-size: .78rem;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: .06em;
}
.powered-badge i { font-size: .98rem; }
.powered-badge strong { color: var(--text); }

.portal-shell { display: grid; grid-template-columns: 280px 1fr; min-height: 100vh; transition: grid-template-columns var(--smooth); }
.portal-shell.sidebar-collapsed { grid-template-columns: 92px 1fr; }
.sidebar {
  position: sticky;
  top: 0;
  height: 100vh;
  padding: 18px;
  border-right: 1px solid var(--line);
  background: #006bf5;
  transition: width var(--smooth), transform var(--smooth);
  z-index: 20;
}
.sidebar.is-collapsed { width: 92px; padding-inline: 14px; }
.sidebar.is-collapsed .sidebar-brand span,
.sidebar.is-collapsed .sidebar-powered,
.sidebar.is-collapsed .nav-item span,
.sidebar.is-collapsed .nav-item .bi-lock { display: none; }
.sidebar.is-collapsed .sidebar-brand,
.sidebar.is-collapsed .nav-item { justify-content: center; }
.sidebar.is-collapsed .nav-item { padding-inline: .55rem; }
.sidebar.is-collapsed .side-collapse { left: 14px; right: 14px; }
.sidebar-brand {
  height: 54px;
  display: flex;
  align-items: center;
  gap: .72rem;
  color: var(--text);
  font-size: 1.05rem;
  font-weight: 900;
  flex-wrap: wrap;
}
.sidebar-brand i { color: var(--text); font-size: 1.5rem; }
.sidebar-powered {
  position: absolute;
  left: 14px;
  right: 14px;
  bottom: 72px;
  display: flex;
  justify-content: center;
}
.sidebar-powered .powered-badge {
  min-width: 0;
  width: 100%;
  padding-inline: .7rem;
  font-size: .62rem;
}
.side-nav { display: grid; gap: 6px; margin-top: 18px; }
.nav-item {
  display: flex;
  align-items: center;
  gap: .72rem;
  min-height: 44px;
  padding: .7rem .8rem;
  color: var(--text);
  border: 1px solid transparent;
  border-radius: var(--radius);
  background: transparent;
  transition: background var(--fast), color var(--fast), border-color var(--fast);
}
.nav-item:hover, .nav-item.active { color: var(--text); background: #2f96ff; border-color: var(--line-strong); }
.nav-item.locked { opacity: .42; }
.status-grid { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 10px; }
.status-btn {
  min-height: 74px;
  display: grid;
  align-content: center;
  justify-items: start;
  gap: 4px;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
  color: var(--text);
  padding: .8rem;
  transition: background var(--fast), border-color var(--fast);
}
.status-btn:hover { background: #2f96ff; border-color: var(--line-strong); }
.status-btn strong { font-size: .92rem; }
.status-btn span { color: var(--text); font-size: .78rem; }
.status-btn.panic { background: var(--red); border-color: var(--red); color: var(--text); }
.side-collapse { position: absolute; bottom: 18px; left: 18px; right: 18px; }
.side-collapse, .icon-btn, .modal-close {
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
  color: var(--text);
  min-width: 42px;
  height: 42px;
  display: grid;
  place-items: center;
  transition: background var(--fast), border-color var(--fast);
}
.side-collapse:hover, .icon-btn:hover, .modal-close:hover { background: #2f96ff; border-color: var(--line-strong); }
.portal-frame { min-width: 0; }
.topbar {
  position: sticky;
  top: 0;
  z-index: 15;
  display: flex;
  align-items: center;
  gap: 12px;
  min-height: 76px;
  padding: 16px 22px;
  border-bottom: 1px solid var(--line);
  background: #006bf5;
  color: var(--text);
}
.global-search {
  flex: 1;
  min-width: 160px;
  display: flex;
  align-items: center;
  gap: .7rem;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
  padding: 0 .85rem;
}
.global-search input { border: 0; background: transparent; box-shadow: none; }
.role-switcher { width: min(220px, 28vw); }
.profile-menu { position: relative; }
.profile-chip {
  display: flex;
  align-items: center;
  gap: .6rem;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
  color: var(--text);
  padding: .62rem .8rem;
}
.dropdown {
  display: none;
  position: absolute;
  top: calc(100% + 10px);
  right: 0;
  width: 240px;
  padding: 8px;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: var(--panel-strong);
  box-shadow: var(--shadow);
}
.dropdown.open { display: grid; }
.dropdown button {
  border: 0;
  background: transparent;
  color: var(--soft);
  padding: .78rem;
  text-align: left;
  border-radius: var(--radius);
}
.dropdown button:hover { background: #2f96ff; color: var(--text); }
.pulse-dot {
  width: 8px;
  height: 8px;
  border-radius: 999px;
  background: var(--red);
  position: absolute;
  margin: -16px 0 0 18px;
  box-shadow: none;
}
.content { padding: clamp(18px, 3vw, 34px); }
.page-head {
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 22px;
}
.page-head h1 { font-size: clamp(1.6rem, 3vw, 2.4rem); }
.app-region { display: grid; gap: 18px; }
.grid { display: grid; gap: 16px; }
.grid.cols-2 { grid-template-columns: repeat(2, minmax(0, 1fr)); }
.grid.cols-3 { grid-template-columns: repeat(3, minmax(0, 1fr)); }
.grid.cols-4 { grid-template-columns: repeat(4, minmax(0, 1fr)); }
.glass-card {
  padding: 18px;
  transition: border-color var(--fast);
}
.glass-card:hover { border-color: var(--line-strong); }
.stat-card { min-height: 112px; display: grid; align-content: space-between; }
.stat-top { display: flex; justify-content: space-between; align-items: center; gap: 12px; }
.stat-icon { color: var(--text) !important; font-size: 1.4rem; }
.stat-value { font-size: 1.65rem; font-weight: 900; }
.stat-label { color: var(--text); }
.table-wrap { overflow: auto; border: 1px solid var(--line); border-radius: var(--radius); }
table { width: 100%; border-collapse: collapse; min-width: 720px; }
th, td { padding: .72rem .82rem; border-bottom: 1px solid var(--line); text-align: left; color: var(--text); }
th { color: var(--text); font-size: .74rem; text-transform: uppercase; letter-spacing: .08em; background: #0063dd; }
tr:hover td { background: #2490ff; }
.badge {
  display: inline-flex;
  align-items: center;
  gap: .35rem;
  border-radius: 999px;
  padding: .28rem .56rem;
  font-size: .76rem;
  font-weight: 900;
  border: 1px solid var(--line);
}
.badge.green { color: var(--text); background: var(--green); border-color: var(--green); }
.badge.blue { color: var(--text); background: #004fcb; border-color: #004fcb; }
.badge.yellow { color: var(--text); background: var(--yellow); border-color: var(--yellow); }
.badge.red { color: var(--text); background: var(--red); border-color: var(--red); }
.badge.purple { color: var(--text); background: var(--purple); border-color: var(--purple); }
.badge.gray { color: var(--text); background: #3b98ff; border-color: #3b98ff; }
.form-grid { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 14px; }
.form-grid .wide { grid-column: 1 / -1; }
.toolbar { display: flex; gap: 10px; align-items: center; justify-content: space-between; flex-wrap: wrap; margin-bottom: 14px; }
.timeline { display: grid; gap: 12px; }
.timeline-item {
  display: grid;
  grid-template-columns: 34px 1fr;
  gap: 10px;
  color: var(--text);
}
.timeline-dot {
  width: 28px;
  height: 28px;
  display: grid;
  place-items: center;
  border-radius: 999px;
  background: #2f96ff;
  color: var(--text);
  border: 1px solid var(--line);
}
.empty-state {
  min-height: 160px;
  display: grid;
  place-items: center;
  text-align: center;
  color: var(--text);
  border: 1px dashed var(--line-strong);
  border-radius: var(--radius);
}
.empty-state i { display: block; font-size: 2rem; color: var(--text); margin-bottom: 8px; }
.skeleton {
  min-height: 80px;
  border-radius: var(--radius);
  background: #1b87ff;
}
.modal-layer {
  display: none;
  position: fixed;
  inset: 0;
  z-index: 60;
  place-items: center;
  padding: 22px;
  background: rgba(0, 42, 115, .62);
  backdrop-filter: none;
}
.modal-layer.open { display: grid; }
.modal-card {
  width: min(760px, 100%);
  max-height: min(760px, calc(100vh - 44px));
  overflow: auto;
  position: relative;
  padding: 24px;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: var(--panel-strong);
  box-shadow: var(--shadow);
  animation: none;
}
.modal-close { position: absolute; top: 14px; right: 14px; }
.toast-host {
  position: fixed;
  right: 18px;
  bottom: 18px;
  display: grid;
  gap: 10px;
  z-index: 80;
}
.toast {
  min-width: min(360px, calc(100vw - 36px));
  display: flex;
  align-items: flex-start;
  gap: .75rem;
  padding: .9rem;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: var(--panel-strong);
  box-shadow: var(--shadow);
  animation: none;
}
.toast i { color: var(--text); }
.panic-popup {
  position: fixed;
  inset: 0;
  z-index: 95;
  display: grid;
  place-items: start center;
  padding: 22px;
  pointer-events: none;
  background: rgba(13, 29, 49, .28);
  animation: none;
}
.panic-popup-card {
  pointer-events: auto;
  width: min(720px, 100%);
  display: grid;
  grid-template-columns: 54px 1fr 42px;
  gap: 16px;
  align-items: center;
  margin-top: 44px;
  padding: 18px;
  border: 1px solid rgba(255, 93, 115, .56);
  border-radius: var(--radius);
  background: var(--red);
  box-shadow: none;
  animation: none;
}
.panic-popup-card > i {
  width: 54px;
  height: 54px;
  display: grid;
  place-items: center;
  border-radius: var(--radius);
  color: var(--text);
  font-size: 2rem;
  background: #b90f1f;
}
.panic-popup-card h2 { font-size: clamp(1.7rem, 4vw, 3rem); }
.announcement-popup {
  position: fixed;
  inset: 0;
  z-index: 94;
  display: grid;
  place-items: center;
  padding: 22px;
  pointer-events: none;
  background: rgba(0, 42, 115, .52);
  backdrop-filter: none;
  animation: none;
}
.announcement-popup-card {
  pointer-events: auto;
  width: min(760px, 100%);
  display: grid;
  grid-template-columns: 54px 1fr 42px;
  gap: 16px;
  align-items: center;
  padding: 20px;
  border: 1px solid rgba(255, 209, 102, .46);
  border-radius: var(--radius);
  background: var(--yellow);
  box-shadow: none;
  animation: none;
}
.announcement-popup-card > i {
  width: 54px;
  height: 54px;
  display: grid;
  place-items: center;
  border-radius: var(--radius);
  color: var(--text);
  font-size: 2rem;
  background: #c69200;
}
.announcement-popup-card h2 { font-size: clamp(1.6rem, 4vw, 3rem); }
.map-list {
  display: grid;
  gap: 10px;
  min-height: 420px;
  padding: 14px;
  background:
    linear-gradient(#3c9cff 1px, transparent 1px),
    linear-gradient(90deg, #3c9cff 1px, transparent 1px),
    #1b87ff;
  background-size: 28px 28px;
  border: 1px solid var(--line);
  border-radius: var(--radius);
}
.map-pin {
  align-self: start;
  max-width: 460px;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  padding: 12px;
  background: #1b87ff;
  box-shadow: none;
}
.mobile-only { display: none; }

.reveal { animation: none; }

.landing-shell {
  min-height: 100vh;
  background: var(--bg);
  color: var(--text);
}
.landing-topbar {
  position: sticky;
  top: 0;
  z-index: 35;
  min-height: 76px;
  display: flex;
  align-items: center;
  gap: 18px;
  padding: 14px clamp(18px, 4vw, 44px);
  border-bottom: 1px solid var(--line);
  background: #006bf5;
}
.landing-brand {
  display: inline-flex;
  align-items: center;
  gap: .7rem;
  font-size: 1.12rem;
  font-weight: 900;
  white-space: nowrap;
}
.landing-brand i { font-size: 1.5rem; }
.landing-nav {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
  flex-wrap: wrap;
}
.landing-nav a {
  min-height: 36px;
  display: inline-flex;
  align-items: center;
  border: 1px solid transparent;
  border-radius: var(--radius);
  padding: .48rem .7rem;
  font-size: .9rem;
  font-weight: 800;
}
.landing-nav a:hover { background: #2f96ff; border-color: var(--line-strong); }
.landing-actions {
  display: flex;
  align-items: center;
  gap: 10px;
  flex-wrap: wrap;
  justify-content: flex-end;
}
.landing-main {
  width: min(1200px, calc(100% - 36px));
  margin: 0 auto;
  display: grid;
  gap: 28px;
  padding: clamp(28px, 5vw, 64px) 0 56px;
}
.landing-hero {
  min-height: calc(100vh - 150px);
  display: grid;
  grid-template-columns: minmax(0, .9fr) minmax(420px, 1.1fr);
  gap: clamp(22px, 4vw, 46px);
  align-items: center;
}
.landing-hero-copy {
  display: grid;
  gap: 18px;
}
.landing-hero h1 {
  font-size: clamp(3rem, 8vw, 6.4rem);
  max-width: 760px;
}
.landing-subtitle {
  max-width: 680px;
  color: var(--text);
  font-size: clamp(1rem, 1.6vw, 1.22rem);
  line-height: 1.58;
}
.landing-preview {
  margin: 0;
  min-height: 520px;
  overflow: hidden;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #0b79ff;
}
.preview-topbar {
  min-height: 54px;
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 0 16px;
  border-bottom: 1px solid var(--line);
  background: #006bf5;
}
.preview-topbar span {
  width: 11px;
  height: 11px;
  border-radius: 999px;
  background: #ffffff;
  opacity: .74;
}
.preview-topbar strong {
  margin-left: 10px;
  font-size: .9rem;
}
.preview-body {
  display: grid;
  grid-template-columns: 190px 1fr;
  min-height: 466px;
}
.preview-body aside {
  display: grid;
  align-content: start;
  gap: 8px;
  padding: 18px;
  border-right: 1px solid var(--line);
  background: #006bf5;
}
.preview-body aside b { margin-bottom: 12px; }
.preview-body aside span {
  min-height: 38px;
  display: flex;
  align-items: center;
  gap: 9px;
  border: 1px solid transparent;
  border-radius: var(--radius);
  padding: .52rem .62rem;
  font-size: .86rem;
}
.preview-body aside span.active,
.preview-body aside span:hover {
  background: #2f96ff;
  border-color: var(--line-strong);
}
.preview-body section {
  display: grid;
  align-content: start;
  gap: 16px;
  padding: 18px;
}
.preview-stat-row {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 12px;
}
.preview-stat-row article,
.preview-board div {
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
  padding: 16px;
}
.preview-stat-row small {
  display: block;
  margin-bottom: 10px;
  font-weight: 800;
}
.preview-stat-row strong {
  font-size: 2rem;
}
.preview-board {
  display: grid;
  gap: 12px;
}
.preview-board div {
  min-height: 150px;
  display: grid;
  align-content: center;
  gap: 10px;
}
.preview-board p,
.preview-board span {
  line-height: 1.45;
}
.preview-board span {
  color: var(--text);
  font-size: .9rem;
}
.landing-band,
.landing-split,
.landing-demo {
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #0b79ff;
  padding: clamp(22px, 4vw, 36px);
}
.landing-section-head {
  display: grid;
  gap: 12px;
  margin-bottom: 20px;
}
.landing-section-head h2,
.landing-split h2,
.landing-demo h2 {
  font-size: clamp(1.8rem, 4vw, 3rem);
}
.landing-card-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 14px;
}
.landing-card-grid article {
  min-height: 190px;
  display: grid;
  align-content: start;
  gap: 12px;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
  padding: 18px;
}
.landing-card-grid i {
  font-size: 1.6rem;
}
.landing-card-grid p,
.landing-checks span {
  line-height: 1.5;
}
.landing-split {
  display: grid;
  grid-template-columns: minmax(0, .82fr) minmax(0, 1.18fr);
  gap: 22px;
  align-items: center;
}
.landing-split > div {
  display: grid;
  gap: 16px;
}
.landing-checks {
  display: grid;
  gap: 10px;
}
.landing-checks span {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
  padding: 12px;
  font-weight: 800;
}
.landing-screenshot {
  margin: 0;
}
.landing-screenshot img {
  display: block;
  width: 100%;
  height: auto;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #006bf5;
}
.landing-demo {
  display: grid;
  grid-template-columns: minmax(0, .82fr) minmax(360px, 1fr);
  gap: 20px;
  align-items: start;
}
.landing-demo > div {
  display: grid;
  gap: 12px;
}
.landing-demo-form {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 14px;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
  padding: 18px;
}
.landing-demo-form .wide {
  grid-column: 1 / -1;
}
.landing-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  padding: 0 clamp(18px, 4vw, 44px) 22px;
  flex-wrap: wrap;
}
.landing-footer div {
  display: flex;
  gap: 14px;
  flex-wrap: wrap;
  font-weight: 800;
}

.docs-shell {
  min-height: 100vh;
  background: var(--bg);
  color: var(--text);
}
.docs-topbar {
  position: sticky;
  top: 0;
  z-index: 30;
  display: flex;
  align-items: center;
  gap: 14px;
  min-height: 76px;
  padding: 14px clamp(18px, 4vw, 42px);
  border-bottom: 1px solid var(--line);
  background: #006bf5;
}
.docs-brand {
  display: inline-flex;
  align-items: center;
  gap: .72rem;
  color: var(--text);
  font-weight: 900;
  white-space: nowrap;
}
.docs-brand i { font-size: 1.45rem; }
.docs-nav {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
  flex-wrap: wrap;
}
.docs-nav a {
  min-height: 36px;
  display: inline-flex;
  align-items: center;
  border: 1px solid transparent;
  border-radius: var(--radius);
  padding: .48rem .7rem;
  font-size: .88rem;
}
.docs-nav a:hover { background: #2f96ff; border-color: var(--line-strong); }
.docs-portal-link { white-space: nowrap; }
.docs-main {
  width: min(1180px, calc(100% - 36px));
  margin: 0 auto;
  padding: clamp(28px, 5vw, 64px) 0 72px;
  display: grid;
  gap: 28px;
}
.docs-hero {
  min-height: 320px;
  display: grid;
  align-content: center;
  gap: 16px;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #0b79ff;
  padding: clamp(24px, 5vw, 54px);
}
.docs-hero h1 { max-width: 800px; }
.docs-index {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 12px;
}
.docs-index a {
  min-height: 86px;
  display: flex;
  align-items: center;
  gap: 12px;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
  padding: 16px;
  font-weight: 900;
}
.docs-index a:hover { border-color: var(--line-strong); background: #2f96ff; }
.docs-index i { font-size: 1.35rem; }
.docs-section {
  display: grid;
  grid-template-columns: minmax(0, .88fr) minmax(0, 1.12fr);
  gap: 20px;
  align-items: stretch;
}
.docs-section-alt { grid-template-columns: minmax(0, 1.12fr) minmax(0, .88fr); }
.docs-section-copy,
.docs-grid-section {
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #0b79ff;
  padding: clamp(20px, 3vw, 30px);
}
.docs-section-copy {
  display: grid;
  align-content: start;
  gap: 16px;
}
.docs-section-copy h2,
.docs-grid-section h2 {
  font-size: clamp(1.6rem, 3vw, 2.25rem);
}
.docs-section-copy p,
.docs-grid-section p,
.docs-task-grid p,
.docs-role-grid p {
  line-height: 1.55;
}
.docs-steps {
  margin: 0;
  padding-left: 1.25rem;
  display: grid;
  gap: 10px;
  line-height: 1.5;
}
.docs-steps li { padding-left: .25rem; }
kbd,
code {
  border: 1px solid var(--line);
  border-radius: 7px;
  background: #1b87ff;
  color: var(--text);
  padding: .12rem .36rem;
  font-weight: 800;
}
.docs-shot {
  margin: 0;
  display: grid;
  gap: 10px;
  align-content: start;
}
.docs-shot img {
  width: 100%;
  height: auto;
  display: block;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #006bf5;
}
.docs-shot figcaption {
  color: var(--text);
  font-size: .88rem;
  line-height: 1.4;
}
.docs-note {
  display: grid;
  grid-template-columns: 30px 1fr;
  gap: 10px;
  align-items: start;
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
  padding: 14px;
  line-height: 1.45;
}
.docs-note i {
  width: 30px;
  height: 30px;
  display: grid;
  place-items: center;
  border-radius: 999px;
  background: #004fcf;
}
.docs-table-wrap {
  overflow: auto;
  border: 1px solid var(--line);
  border-radius: var(--radius);
}
.docs-table { min-width: 620px; }
.docs-grid-section {
  display: grid;
  gap: 18px;
}
.docs-role-grid,
.docs-task-grid {
  display: grid;
  gap: 14px;
}
.docs-role-grid { grid-template-columns: repeat(5, minmax(0, 1fr)); }
.docs-task-grid { grid-template-columns: repeat(3, minmax(0, 1fr)); }
.docs-role-grid article,
.docs-task-grid article {
  border: 1px solid var(--line);
  border-radius: var(--radius);
  background: #1b87ff;
  padding: 16px;
}
.docs-role-grid i {
  font-size: 1.5rem;
  display: inline-block;
  margin-bottom: 12px;
}
.docs-role-grid h3,
.docs-task-grid h3 {
  margin-bottom: 8px;
}
.docs-footer {
  display: flex;
  justify-content: center;
  padding: 0 18px 22px;
}

.click-ripple {
  position: fixed;
  z-index: 2147483647;
  width: 12px;
  height: 12px;
  left: 0;
  top: 0;
  border: 2px solid rgba(255, 255, 255, .95);
  background: rgba(255, 255, 255, .18);
  border-radius: 999px;
  pointer-events: none;
  transform: translate(-50%, -50%) scale(.25);
  animation: clickRipple 620ms ease-out forwards;
  mix-blend-mode: screen;
}

@keyframes clickRipple {
  to {
    opacity: 0;
    transform: translate(-50%, -50%) scale(9);
  }
}

@media (max-width: 1100px) {
  .grid.cols-4 { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .grid.cols-3 { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .status-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .landing-hero,
  .landing-split { grid-template-columns: 1fr; }
  .landing-hero { min-height: 0; }
  .landing-card-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .docs-index { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .docs-section,
  .docs-section-alt { grid-template-columns: 1fr; }
  .docs-role-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .docs-task-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .docs-section-alt .docs-shot { order: 2; }
}
@media (max-width: 820px) {
  .portal-shell { grid-template-columns: 1fr; }
  .portal-shell.sidebar-collapsed { grid-template-columns: 1fr; }
  .sidebar { position: fixed; transform: translateX(-104%); width: 280px; }
  .sidebar.open { transform: translateX(0); }
  .mobile-only { display: grid; }
  .topbar { flex-wrap: wrap; }
  .global-search { order: 5; flex-basis: 100%; }
  .role-switcher { width: auto; flex: 1; }
  .page-head { align-items: stretch; flex-direction: column; }
  .grid.cols-2, .grid.cols-3, .grid.cols-4, .form-grid, .feature-grid { grid-template-columns: 1fr; }
  .status-grid { grid-template-columns: 1fr; }
  .landing-topbar { align-items: stretch; flex-direction: column; }
  .landing-nav { justify-content: flex-start; }
  .landing-actions { justify-content: stretch; }
  .landing-actions .btn,
  .landing-demo .btn { width: 100%; }
  .landing-preview { min-height: 0; }
  .preview-body { grid-template-columns: 1fr; }
  .preview-body aside { border-right: 0; border-bottom: 1px solid var(--line); }
  .preview-stat-row,
  .landing-card-grid { grid-template-columns: 1fr; }
  .landing-demo,
  .landing-demo-form { grid-template-columns: 1fr; }
  .docs-topbar { align-items: stretch; flex-direction: column; }
  .docs-nav { justify-content: flex-start; }
  .docs-portal-link { width: 100%; }
  .docs-index,
  .docs-role-grid,
  .docs-task-grid { grid-template-columns: 1fr; }
}
body,.auth-shell,.landing-shell,.docs-shell{
  background:var(--bg)!important;
  color:var(--text)!important;
}

.auth-card,.glass-card,.modal-card,.landing-band,.landing-split,
.landing-demo,.docs-section-copy,.docs-grid-section,
.landing-preview{
  background:rgba(43,45,49,.96)!important;
  border-color:var(--line)!important;
  backdrop-filter:blur(16px);
  box-shadow:var(--shadow);
}

.sidebar,.topbar,.landing-topbar,.docs-topbar,.preview-topbar,
.preview-body aside{
  background:#18191c!important;
  border-color:var(--line)!important;
}

input,select,textarea,.global-search,.profile-chip{
  background:#1a1b1e!important;
  border:1px solid #3f4147!important;
  color:var(--text)!important;
}

input:focus,select:focus,textarea:focus{
  border-color:var(--blue)!important;
  box-shadow:0 0 0 3px rgba(88,101,242,.25)!important;
}

.btn-primary{
  background:var(--blue)!important;
  border-color:var(--blue)!important;
  color:#fff!important;
}
.btn-primary:hover{background:#6974f5!important;}

.btn-ghost,.icon-btn,.side-collapse{
  background:#3a3d44!important;
  border-color:var(--line)!important;
}
.btn-ghost:hover,.icon-btn:hover,.side-collapse:hover{
  background:#454850!important;
}

.nav-item.active{
  background:rgba(88,101,242,.18)!important;
}
.nav-item:hover{
  background:rgba(255,255,255,.05)!important;
}

.dropdown,.toast,.powered-badge{
  background:#2b2d31!important;
  border-color:var(--line)!important;
}

th{background:#232428!important;}
tr:hover td{background:rgba(255,255,255,.03)!important;}

.modal-layer{
  background:rgba(0,0,0,.55)!important;
  backdrop-filter:blur(8px);
}

.click-ripple{
  border-color:rgba(88,101,242,.9)!important;
  background:rgba(88,101,242,.15)!important;
}

body::before{
 content:"";
 position:fixed;
 inset:0;
 pointer-events:none;
 background:
 radial-gradient(circle at top,rgba(88,101,242,.08),transparent 50%),
 radial-gradient(circle at bottom right,rgba(255,255,255,.02),transparent 40%);
}

/* =========================
   OCIA BOOT SYSTEM LAYER
========================= */

.boot-shell {
  background: #000 !important;
  color: #00ff9c;
  font-family: "Consolas", "Courier New", monospace;
  overflow: hidden;
}

.boot-terminal {
  padding: 18px;
  white-space: pre-wrap;
  font-size: 13px;
  line-height: 1.4;
}

.boot-line {
  color: #00ff9c;
  text-shadow: 0 0 8px rgba(0,255,156,.25);
}

.boot-complete {
  height: 100vh;
  display: grid;
  place-items: center;
}

.boot-complete.hidden {
  display: none;
}

.boot-card {
  text-align: center;
  padding: 32px;
  border: 1px solid rgba(0,255,156,.25);
  background: rgba(0,0,0,.7);
  box-shadow: 0 0 40px rgba(0,255,156,.08);
}

.boot-logo {
  color: #00ff9c;
  font-size: 12px;
  line-height: 1.2;
}

.boot-warning {
  color: rgba(255,255,255,.6);
  font-size: 12px;
  margin: 12px 0 20px;
}

.boot-launch {
  background: #00ff9c !important;
  color: #000 !important;
  font-weight: 900;
  border: none !important;
}

.boot-launch:hover {
  background: #00cc7a !important;
}

/* =========================================================
   OCIA TERMINAL BOOT (FULL AUTHENTIC REBUILD)
   Based on original booting.html system
========================================================= */

.boot-shell {
  background: #000 !important;
  color: #00ff9c !important;
  font-family: "Consolas", "Courier New", monospace !important;
  overflow: hidden;
  height: 100vh;
}

/* Terminal area */
.boot-terminal {
  padding: 16px;
  white-space: pre-wrap;
  line-height: 1.45;
  font-size: 14px;
}

/* Each line = authentic terminal styling */
.boot-line {
  display: block;
  animation: bootFlicker 120ms linear;
}

@keyframes bootFlicker {
  0% { opacity: 0.4; }
  100% { opacity: 1; }
}

/* Color system EXACTLY like your original */
.boot-green { color: #00ff9c; }
.boot-yellow { color: #f1c40f; }
.boot-red { color: #ff4c4c; }
.boot-cyan { color: #4cc3ff; }
.boot-white { color: #e0e0e0; }

/* Fake CRT glow */
.boot-shell::before {
  content: "";
  position: fixed;
  inset: 0;
  pointer-events: none;
  background:
    repeating-linear-gradient(
      to bottom,
      rgba(255,255,255,0.02),
      rgba(255,255,255,0.02) 1px,
      transparent 2px,
      transparent 4px
    );
  mix-blend-mode: overlay;
  opacity: .35;
}

/* Scanline drift */
.boot-shell::after {
  content: "";
  position: fixed;
  inset: 0;
  pointer-events: none;
  background: radial-gradient(circle at center, rgba(0,255,156,.06), transparent 60%);
}

/* Signature block (your OCIA ASCII logo) */
.boot-signature {
  display: none;
  margin-top: 20px;
  color: #00ff9c;
  text-align: center;
  font-size: 13px;
}

.boot-signature pre {
  line-height: 1.1;
}

/* Launch card */
.boot-launch-screen {
  display: none;
  height: 100vh;
  place-items: center;
}

.boot-launch-card {
  border: 1px solid rgba(0,255,156,.25);
  background: rgba(0,0,0,.75);
  padding: 32px;
  box-shadow: 0 0 60px rgba(0,255,156,.08);
  text-align: center;
}

.boot-launch-title {
  color: #00ff9c;
  letter-spacing: .2em;
  font-weight: 800;
  margin-bottom: 10px;
}

.boot-launch-sub {
  color: rgba(255,255,255,.65);
  font-size: 12px;
  margin-bottom: 20px;
}

.boot-launch-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 10px 18px;
  border: 1px solid #00ff9c;
  background: transparent;
  color: #00ff9c;
  font-weight: 900;
  text-transform: uppercase;
  cursor: pointer;
}

.boot-launch-btn:hover {
  background: rgba(0,255,156,.08);
}
