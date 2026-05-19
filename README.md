<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>กำลังพาไปยังปลายทาง...</title>
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

  /* Grid BG */
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

  /* Glow orb */
  body::after {
    content: '';
    position: fixed;
    width: 600px;
    height: 600px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(0,229,255,0.07) 0%, transparent 70%);
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    pointer-events: none;
  }

  .container {
    position: relative;
    z-index: 10;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 32px;
    padding: 24px;
    width: 100%;
    max-width: 520px;
    animation: fadeIn 0.6s ease both;
  }

  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* Ring timer */
  .ring-wrap {
    position: relative;
    width: 120px;
    height: 120px;
    flex-shrink: 0;
  }

  .ring-svg {
    width: 120px;
    height: 120px;
    transform: rotate(-90deg);
  }

  .ring-track {
    fill: none;
    stroke: var(--border);
    stroke-width: 4;
  }

  .ring-fill {
    fill: none;
    stroke: var(--accent);
    stroke-width: 4;
    stroke-linecap: round;
    stroke-dasharray: 314;
    stroke-dashoffset: 0;
    transition: stroke-dashoffset 1s linear;
    filter: drop-shadow(0 0 6px rgba(0,229,255,0.6));
  }

  .ring-number {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Syne', sans-serif;
    font-size: 42px;
    font-weight: 800;
    color: var(--accent);
    text-shadow: 0 0 24px rgba(0,229,255,0.5);
  }

  /* Card */
  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 28px 32px;
    width: 100%;
    text-align: center;
    box-shadow: 0 0 60px rgba(0,0,0,0.5), 0 0 0 1px rgba(0,229,255,0.05);
  }

  .tag {
    display: inline-block;
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--accent);
    background: rgba(0,229,255,0.08);
    border: 1px solid rgba(0,229,255,0.15);
    padding: 4px 14px;
    border-radius: 20px;
    margin-bottom: 16px;
  }

  .headline {
    font-family: 'Syne', sans-serif;
    font-size: 22px;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 6px;
    letter-spacing: -0.5px;
  }

  .sub {
    font-size: 12px;
    color: var(--muted);
    margin-bottom: 20px;
  }

  .dest-box {
    background: rgba(0,229,255,0.05);
    border: 1px solid rgba(0,229,255,0.15);
    border-radius: 10px;
    padding: 12px 16px;
    font-size: 12px;
    color: var(--accent);
    word-break: break-all;
    line-height: 1.5;
    text-align: left;
    display: flex;
    align-items: flex-start;
    gap: 8px;
    margin-bottom: 20px;
  }

  .dest-icon { flex-shrink: 0; margin-top: 1px; }
  .dest-url { flex: 1; }

  /* Progress bar */
  .progress-bar-wrap {
    height: 3px;
    background: var(--border);
    border-radius: 3px;
    overflow: hidden;
    margin-bottom: 20px;
  }

  .progress-bar-fill {
    height: 100%;
    background: var(--accent);
    border-radius: 3px;
    box-shadow: 0 0 8px rgba(0,229,255,0.6);
    width: 100%;
    transform-origin: left;
    animation: shrink linear both;
  }

  @keyframes shrink {
    from { transform: scaleX(1); }
    to { transform: scaleX(0); }
  }

  /* Buttons */
  .btn-now {
    display: block;
    width: 100%;
    padding: 13px;
    border-radius: 10px;
    background: var(--accent);
    color: #000;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 13px;
    font-weight: 500;
    letter-spacing: 1px;
    border: none;
    cursor: pointer;
    text-decoration: none;
    transition: background 0.2s, transform 0.15s;
  }

  .btn-now:hover {
    background: #33eaff;
    transform: translateY(-2px);
  }

  .btn-cancel {
    display: block;
    margin-top: 10px;
    font-size: 11px;
    color: var(--muted);
    text-align: center;
    cursor: pointer;
    letter-spacing: 0.5px;
    text-decoration: none;
    transition: color 0.2s;
  }

  .btn-cancel:hover { color: var(--text); }

  /* Error state */
  .error-state {
    text-align: center;
  }

  .error-icon { font-size: 48px; margin-bottom: 16px; }
  .error-title {
    font-family: 'Syne', sans-serif;
    font-size: 20px;
    font-weight: 700;
    color: #ff6b6b;
    margin-bottom: 8px;
  }
  .error-sub { font-size: 12px; color: var(--muted); }

  /* Footer */
  .footer {
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 1px;
    text-align: center;
  }

  /* Tick animation when done */
  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.4; }
  }

  .redirecting-text {
    font-size: 11px;
    color: var(--muted);
    margin-top: 14px;
    animation: pulse 1.2s ease infinite;
    letter-spacing: 1px;
  }
</style>
</head>
<body>
<div class="container" id="main-container">

  <!-- Main redirect UI -->
  <div id="redirect-ui" style="width:100%;display:flex;flex-direction:column;align-items:center;gap:28px;">

    <div class="ring-wrap">
      <svg class="ring-svg" viewBox="0 0 120 120">
        <circle class="ring-track" cx="60" cy="60" r="50"/>
        <circle class="ring-fill" id="ring" cx="60" cy="60" r="50"/>
      </svg>
      <div class="ring-number" id="counter">5</div>
    </div>

    <div class="card">
      <div class="tag">🔗 กำลังพาไปยัง</div>
      <div class="headline">ปลายทางของคุณ</div>
      <div class="sub" id="countdown-text">จะ redirect ใน <strong>5</strong> วินาที</div>

      <div class="dest-box">
        <span class="dest-icon">🌐</span>
        <span class="dest-url" id="dest-display">—</span>
      </div>

      <div class="progress-bar-wrap">
        <div class="progress-bar-fill" id="progress-bar"></div>
      </div>

      <a id="go-now-btn" href="#" class="btn-now" onclick="goNow()">→ ไปเลยทันที</a>
      <a href="javascript:void(0)" class="btn-cancel" onclick="cancelRedirect()">✕ ยกเลิก</a>

      <div class="redirecting-text" id="redir-text">กำลังนับถอยหลัง...</div>
    </div>

  </div>

  <!-- Error UI -->
  <div id="error-ui" style="display:none;">
    <div class="card error-state">
      <div class="error-icon">⚠️</div>
      <div class="error-title">ไม่พบ URL ปลายทาง</div>
      <div class="error-sub">กรุณาตรวจสอบ QR Code หรือลิ้งค์<br>ที่ใช้สร้างหน้านี้</div>
    </div>
  </div>

  <div class="footer">SHARE HUB · Redirect Service</div>

</div>

<script>
  const DURATION = 5; // seconds
  let countdown = DURATION;
  let timer = null;
  let cancelled = false;
  let destUrl = null;

  function getParam(name) {
    const params = new URLSearchParams(window.location.search);
    return params.get(name) || params.get('url') || params.get('link');
  }

  function normalizeUrl(u) {
    if (!u) return null;
    u = u.trim();
    if (/^https?:\/\//i.test(u)) return u;
    return 'https://' + u;
  }

  function init() {
    const raw = getParam('to') || getParam('url') || getParam('link') || getParam('u');
    destUrl = normalizeUrl(raw);

    if (!destUrl) {
      document.getElementById('redirect-ui').style.display = 'none';
      document.getElementById('error-ui').style.display = 'block';
      return;
    }

    // Show destination
    document.getElementById('dest-display').textContent = destUrl;
    document.getElementById('go-now-btn').href = destUrl;
    document.title = '→ ' + destUrl;

    // Start progress bar animation
    const bar = document.getElementById('progress-bar');
    bar.style.animationDuration = DURATION + 's';

    // Start ring animation
    setRing(DURATION, DURATION);

    // Start countdown
    updateCounter();
    timer = setInterval(tick, 1000);
  }

  function setRing(current, total) {
    const circumference = 314;
    const offset = circumference * (1 - current / total);
    document.getElementById('ring').style.strokeDashoffset = offset;
  }

  function tick() {
    countdown--;
    setRing(countdown, DURATION);
    updateCounter();
    if (countdown <= 0) {
      clearInterval(timer);
      goNow();
    }
  }

  function updateCounter() {
    document.getElementById('counter').textContent = countdown;
    document.getElementById('countdown-text').innerHTML =
      `จะ redirect ใน <strong>${countdown}</strong> วินาที`;
  }

  function goNow() {
    if (!destUrl || cancelled) return;
    document.getElementById('redir-text').textContent = '✓ กำลังพาไป...';
    document.getElementById('redir-text').style.color = 'var(--accent)';
    clearInterval(timer);
    window.location.href = destUrl;
  }

  function cancelRedirect() {
    cancelled = true;
    clearInterval(timer);
    document.getElementById('counter').textContent = '✕';
    document.getElementById('counter').style.fontSize = '28px';
    document.getElementById('ring').style.stroke = 'var(--muted)';
    document.getElementById('countdown-text').textContent = 'ยกเลิก redirect แล้ว';
    document.getElementById('redir-text').textContent = 'คุณสามารถกดปุ่ม "ไปเลยทันที" เมื่อพร้อม';
    document.getElementById('redir-text').style.animation = 'none';
    document.getElementById('progress-bar').style.animation = 'none';
    document.getElementById('progress-bar').style.transform = 'scaleX(0)';
  }

  init();
</script>
</body>
</html>
