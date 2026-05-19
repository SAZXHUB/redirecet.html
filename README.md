<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>กำลังพาไป...</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@700;800&family=IBM+Plex+Mono:wght@300;400&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #08090d;
    --surface: #0f1117;
    --border: #1a1f2e;
    --accent: #00e5ff;
    --text: #e0e4f0;
    --muted: #454c60;
  }

  body {
    font-family: 'IBM Plex Mono', monospace;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    overflow: hidden;
  }

  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,229,255,0.025) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,229,255,0.025) 1px, transparent 1px);
    background-size: 48px 48px;
    pointer-events: none;
  }

  body::after {
    content: '';
    position: fixed;
    width: 600px;
    height: 600px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(0,229,255,0.07) 0%, transparent 70%);
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    pointer-events: none;
  }

  .container {
    position: relative;
    z-index: 10;
    width: 100%;
    max-width: 480px;
    padding: 24px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 24px;
    animation: fadeIn 0.4s ease both;
  }

  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(16px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* Spinner */
  .spinner-wrap {
    position: relative;
    width: 80px;
    height: 80px;
  }

  .spinner {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    border: 3px solid var(--border);
    border-top-color: var(--accent);
    animation: spin 0.8s linear infinite;
    box-shadow: 0 0 20px rgba(0,229,255,0.2);
  }

  @keyframes spin {
    to { transform: rotate(360deg); }
  }

  .spinner-icon {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 26px;
  }

  /* Card */
  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 28px 28px 24px;
    width: 100%;
    text-align: center;
    box-shadow: 0 0 60px rgba(0,0,0,0.5), 0 0 0 1px rgba(0,229,255,0.04);
  }

  .tag {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--accent);
    background: rgba(0,229,255,0.08);
    border: 1px solid rgba(0,229,255,0.15);
    padding: 4px 14px;
    border-radius: 20px;
    margin-bottom: 18px;
  }

  .headline {
    font-family: 'Syne', sans-serif;
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 18px;
    letter-spacing: -0.5px;
  }

  /* URL display */
  .url-box {
    background: rgba(0,229,255,0.05);
    border: 1px solid rgba(0,229,255,0.15);
    border-radius: 12px;
    padding: 14px 16px;
    text-align: left;
    margin-bottom: 20px;
  }

  .url-label {
    font-size: 9px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 6px;
  }

  .url-text {
    font-size: 13px;
    color: var(--accent);
    word-break: break-all;
    line-height: 1.6;
    font-weight: 400;
  }

  /* Thin loader bar at top of card */
  .bar-wrap {
    height: 2px;
    background: var(--border);
    border-radius: 2px;
    overflow: hidden;
    margin-bottom: 20px;
  }

  .bar-fill {
    height: 100%;
    width: 30%;
    background: var(--accent);
    border-radius: 2px;
    box-shadow: 0 0 10px rgba(0,229,255,0.7);
    animation: slide 1.2s ease-in-out infinite;
  }

  @keyframes slide {
    0%   { margin-left: -30%; }
    100% { margin-left: 100%; }
  }

  .status-text {
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 1px;
    animation: blink 1.4s ease infinite;
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.35; }
  }

  /* Error */
  .error-icon { font-size: 44px; margin-bottom: 14px; }
  .error-title {
    font-family: 'Syne', sans-serif;
    font-size: 18px;
    font-weight: 700;
    color: #ff6b6b;
    margin-bottom: 8px;
  }
  .error-sub { font-size: 12px; color: var(--muted); line-height: 1.6; }

  .footer {
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 1.5px;
  }
</style>
</head>
<body>

<div class="container">

  <div id="main-ui" style="width:100%;display:flex;flex-direction:column;align-items:center;gap:24px;">

    <div class="spinner-wrap">
      <div class="spinner"></div>
      <div class="spinner-icon">🔗</div>
    </div>

    <div class="card">
      <div class="tag">🌐 กำลังพาไปยัง</div>
      <div class="headline">ปลายทางของคุณ</div>

      <div class="url-box">
        <div class="url-label">destination url</div>
        <div class="url-text" id="dest-display">—</div>
      </div>

      <div class="bar-wrap">
        <div class="bar-fill"></div>
      </div>

      <div class="status-text" id="status-text">กำลังพาไป...</div>
    </div>

  </div>

  <div id="error-ui" style="display:none;width:100%;">
    <div class="card" style="text-align:center;">
      <div class="error-icon">⚠️</div>
      <div class="error-title">ไม่พบ URL ปลายทาง</div>
      <div class="error-sub">กรุณาตรวจสอบ QR Code<br>หรือลิ้งค์ที่ใช้เปิดหน้านี้</div>
    </div>
  </div>

  <div class="footer">SHARE HUB · sazxhub</div>

</div>

<script>
  function getParam() {
    const p = new URLSearchParams(window.location.search);
    return p.get('to') || p.get('url') || p.get('link') || p.get('u');
  }

  function normalizeUrl(u) {
    if (!u) return null;
    u = u.trim();
    if (/^https?:\/\//i.test(u)) return u;
    return 'https://' + u;
  }

  function init() {
    const raw = getParam();
    const dest = normalizeUrl(raw);

    if (!dest) {
      document.getElementById('main-ui').style.display = 'none';
      document.getElementById('error-ui').style.display = 'block';
      return;
    }

    document.getElementById('dest-display').textContent = dest;
    document.title = '→ ' + dest;

    // Redirect ทันทีเลย (0ms delay)
    window.location.replace(dest);
  }

  init();
</script>
</body>
</html>
