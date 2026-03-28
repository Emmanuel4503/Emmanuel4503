<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Emmanuel Oladipo — Software Engineer</title>

<!-- jQuery -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;800&display=swap" rel="stylesheet"/>

<style>
  /* ═══════════════════════════════════════════
     CSS CUSTOM PROPERTIES
  ═══════════════════════════════════════════ */
  :root {
    --primary:   #667eea;
    --mid:       #764ba2;
    --accent:    #f093fb;
    --teal:      #4ECDC4;
    --coral:     #FF6B6B;
    --bg:        #0D1117;
    --surface:   #161B22;
    --border:    rgba(102,126,234,0.25);
    --text:      #e6edf3;
    --muted:     #8b949e;
    --glow-blue: 0 0 20px rgba(102,126,234,0.6), 0 0 40px rgba(102,126,234,0.3);
    --glow-pink: 0 0 20px rgba(240,147,251,0.6), 0 0 40px rgba(240,147,251,0.3);
    --glow-teal: 0 0 20px rgba(78,205,196,0.6), 0 0 40px rgba(78,205,196,0.3);
    --font-head: 'Syne', sans-serif;
    --font-mono: 'Space Mono', monospace;
  }

  /* ═══════════════════════════════════════════
     RESET & BASE
  ═══════════════════════════════════════════ */
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-head);
    overflow-x: hidden;
    line-height: 1.6;
  }

  /* ═══════════════════════════════════════════
     ANIMATED BACKGROUND GRID
  ═══════════════════════════════════════════ */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(102,126,234,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(102,126,234,0.04) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  /* ═══════════════════════════════════════════
     HEADER WAVE
  ═══════════════════════════════════════════ */
  .header-wave {
    position: relative;
    text-align: center;
    padding: 80px 24px 60px;
    background: linear-gradient(135deg, #0a0e1a 0%, #0d1117 40%, #13072a 100%);
    overflow: hidden;
    opacity: 0; /* jQuery will fade in */
  }

  .header-wave::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse 80% 60% at 50% 0%, rgba(102,126,234,0.18) 0%, transparent 70%);
  }

  .header-orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(60px);
    opacity: 0.35;
    animation: drift 8s ease-in-out infinite alternate;
  }
  .header-orb.a { width: 300px; height: 300px; background: var(--primary); top: -80px; left: -60px; animation-delay: 0s; }
  .header-orb.b { width: 220px; height: 220px; background: var(--accent); top: -40px; right: -40px; animation-delay: -4s; }
  .header-orb.c { width: 160px; height: 160px; background: var(--teal); bottom: -20px; left: 40%; animation-delay: -2s; }

  @keyframes drift {
    from { transform: translate(0, 0) scale(1); }
    to   { transform: translate(20px, 15px) scale(1.08); }
  }

  .header-name {
    position: relative;
    font-size: clamp(2.4rem, 8vw, 5rem);
    font-weight: 800;
    background: linear-gradient(135deg, #fff 0%, var(--primary) 40%, var(--accent) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    letter-spacing: -1px;
    line-height: 1.1;
    margin-bottom: 16px;
  }

  .header-role {
    position: relative;
    font-family: var(--font-mono);
    font-size: clamp(0.7rem, 2.2vw, 1rem);
    color: var(--muted);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-bottom: 28px;
  }

  .header-badges {
    position: relative;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
  }

  /* ═══════════════════════════════════════════
     TYPING STRIP
  ═══════════════════════════════════════════ */
  .typing-strip {
    background: linear-gradient(90deg, transparent, rgba(102,126,234,0.08), transparent);
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    padding: 18px 24px;
    text-align: center;
    font-family: var(--font-mono);
    font-size: clamp(0.75rem, 2.5vw, 1rem);
    color: var(--primary);
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    opacity: 0;
  }

  .cursor-blink {
    display: inline-block;
    width: 2px;
    height: 1em;
    background: var(--accent);
    margin-left: 3px;
    vertical-align: text-bottom;
    animation: blink 1s step-end infinite;
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  /* ═══════════════════════════════════════════
     MAIN CONTAINER
  ═══════════════════════════════════════════ */
  .container {
    max-width: 960px;
    margin: 0 auto;
    padding: 0 24px 60px;
    position: relative;
    z-index: 1;
  }

  /* ═══════════════════════════════════════════
     SECTION DIVIDER
  ═══════════════════════════════════════════ */
  .section-divider {
    display: flex;
    align-items: center;
    gap: 14px;
    margin: 48px 0 28px;
    opacity: 0;
  }

  .section-divider .label {
    font-weight: 800;
    font-size: clamp(1rem, 3vw, 1.25rem);
    white-space: nowrap;
  }

  .section-divider .line {
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--border), transparent);
  }

  /* ═══════════════════════════════════════════
     ABOUT CARD
  ═══════════════════════════════════════════ */
  .about-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 24px 28px;
    font-family: var(--font-mono);
    font-size: clamp(0.72rem, 2vw, 0.88rem);
    line-height: 1.8;
    color: #b0c4de;
    position: relative;
    overflow: hidden;
    opacity: 0;
    transition: box-shadow 0.4s, border-color 0.4s;
  }

  .about-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 4px; height: 100%;
    background: linear-gradient(180deg, var(--primary), var(--accent));
    border-radius: 4px 0 0 4px;
  }

  .about-card:hover {
    border-color: rgba(102,126,234,0.5);
    box-shadow: var(--glow-blue);
  }

  .code-key   { color: var(--primary); }
  .code-str   { color: #a5d6ff; }
  .code-arr   { color: var(--accent); }
  .code-punct { color: var(--muted); }

  /* ═══════════════════════════════════════════
     BADGE GROUPS
  ═══════════════════════════════════════════ */
  .badge-group {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    justify-content: center;
    opacity: 0;
  }

  .badge {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 7px 14px;
    border-radius: 8px;
    font-family: var(--font-mono);
    font-size: clamp(0.62rem, 1.8vw, 0.75rem);
    font-weight: 700;
    border: 1px solid transparent;
    cursor: default;
    transition: transform 0.2s, box-shadow 0.3s, border-color 0.3s;
    white-space: nowrap;
  }

  .badge:hover {
    transform: translateY(-3px) scale(1.04);
  }

  /* Domain badges */
  .badge-domain { background: rgba(102,126,234,0.15); color: var(--primary); border-color: rgba(102,126,234,0.3); }
  .badge-domain:hover { box-shadow: var(--glow-blue); border-color: var(--primary); }

  /* Language badges — colour-coded */
  .b-html    { background: rgba(227,79,38,0.15);  color:#E34F26; border-color:rgba(227,79,38,0.3); }
  .b-css     { background: rgba(21,114,182,0.15); color:#1572B6; border-color:rgba(21,114,182,0.3); }
  .b-js      { background: rgba(247,223,30,0.15); color:#F7DF1E; border-color:rgba(247,223,30,0.3); }
  .b-next    { background: rgba(255,255,255,0.08); color:#fff;   border-color:rgba(255,255,255,0.15); }
  .b-react   { background: rgba(97,218,251,0.12); color:#61DAFB; border-color:rgba(97,218,251,0.3); }
  .b-flutter { background: rgba(2,86,155,0.18);   color:#02A9F4; border-color:rgba(2,86,155,0.3); }
  .b-node    { background: rgba(51,153,51,0.15);  color:#6CC24A; border-color:rgba(51,153,51,0.3); }
  .b-php     { background: rgba(119,107,180,0.18);color:#A97FDE; border-color:rgba(119,107,180,0.3); }
  .b-python  { background: rgba(55,118,171,0.18); color:#4FC3F7; border-color:rgba(55,118,171,0.3); }

  .b-html:hover    { box-shadow: 0 0 18px rgba(227,79,38,0.5); }
  .b-css:hover     { box-shadow: 0 0 18px rgba(21,114,182,0.5); }
  .b-js:hover      { box-shadow: 0 0 18px rgba(247,223,30,0.5); }
  .b-next:hover    { box-shadow: 0 0 18px rgba(255,255,255,0.2); }
  .b-react:hover   { box-shadow: 0 0 18px rgba(97,218,251,0.5); }
  .b-flutter:hover { box-shadow: 0 0 18px rgba(2,169,244,0.5); }
  .b-node:hover    { box-shadow: 0 0 18px rgba(108,194,74,0.5); }
  .b-php:hover     { box-shadow: 0 0 18px rgba(169,127,222,0.5); }
  .b-python:hover  { box-shadow: 0 0 18px rgba(79,195,247,0.5); }

  /* DB badges */
  .b-mysql  { background: rgba(68,121,161,0.18); color:#4479A1; border-color:rgba(68,121,161,0.3); }
  .b-mongo  { background: rgba(71,162,72,0.15);  color:#47A248; border-color:rgba(71,162,72,0.3); }
  .b-fire   { background: rgba(255,202,40,0.15); color:#FFCA28; border-color:rgba(255,202,40,0.3); }
  .b-mysql:hover  { box-shadow: 0 0 18px rgba(68,121,161,0.5); }
  .b-mongo:hover  { box-shadow: 0 0 18px rgba(71,162,72,0.5); }
  .b-fire:hover   { box-shadow: 0 0 18px rgba(255,202,40,0.5); }

  /* Tool badges */
  .b-tool { background: rgba(255,255,255,0.06); color: var(--muted); border-color: rgba(255,255,255,0.1); }
  .b-tool:hover { color: var(--text); border-color: rgba(255,255,255,0.25); box-shadow: 0 0 14px rgba(255,255,255,0.1); }

  /* ═══════════════════════════════════════════
     ACTIVITY GRAPH CARD
  ═══════════════════════════════════════════ */
  .graph-card {
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    opacity: 0;
    transition: box-shadow 0.4s, border-color 0.4s;
  }
  .graph-card:hover {
    border-color: rgba(240,147,251,0.4);
    box-shadow: var(--glow-pink);
  }
  .graph-card img { display: block; width: 100%; }

  /* ═══════════════════════════════════════════
     FOOTER WAVE
  ═══════════════════════════════════════════ */
  .footer-wave {
    margin-top: 60px;
    text-align: center;
    opacity: 0;
  }
  .footer-wave img { display: block; width: 100%; }

  /* ═══════════════════════════════════════════
     GLOW PULSE ANIMATION (jQuery adds class)
  ═══════════════════════════════════════════ */
  .glow-pulse {
    animation: glowLoop 3s ease-in-out infinite;
  }
  @keyframes glowLoop {
    0%,100% { box-shadow: 0 0 10px rgba(102,126,234,0.3); }
    50%      { box-shadow: 0 0 30px rgba(240,147,251,0.7), 0 0 60px rgba(102,126,234,0.4); }
  }

  /* ═══════════════════════════════════════════
     ┌─────────────────────────────────────────┐
     │        MEDIA QUERIES                    │
     │  — from largest to smallest             │
     └─────────────────────────────────────────┘
  ═══════════════════════════════════════════ */

  /* ── Tablet: ≤ 768px ── */
  @media (max-width: 768px) {
    .header-wave { padding: 60px 16px 48px; }

    .header-name { letter-spacing: -0.5px; }

    .container { padding: 0 16px 48px; }

    .section-divider { margin: 36px 0 20px; }

    .about-card { padding: 18px 20px; }

    .badge { padding: 6px 12px; }

    .header-orb.a { width: 180px; height: 180px; }
    .header-orb.b { width: 140px; height: 140px; }
    .header-orb.c { width: 100px; height: 100px; }
  }

  /* ── Large Phone: ≤ 480px ── */
  @media (max-width: 480px) {
    .header-wave { padding: 48px 12px 40px; }

    .header-role {
      font-size: 0.65rem;
      letter-spacing: 0.06em;
      word-break: break-word;
    }

    .header-badges { gap: 7px; }

    .typing-strip {
      font-size: 0.72rem;
      padding: 14px 12px;
      white-space: normal;
      text-align: left;
    }

    .container { padding: 0 12px 40px; }

    .section-divider .label { font-size: 0.92rem; }

    .about-card {
      padding: 14px 16px;
      font-size: 0.7rem;
    }

    .badge {
      padding: 5px 10px;
      font-size: 0.62rem;
      border-radius: 6px;
    }

    .badge-group { gap: 6px; }

    .header-orb.a { width: 120px; height: 120px; top: -40px; left: -30px; }
    .header-orb.b { width: 100px; height: 100px; top: -20px; right: -20px; }
    .header-orb.c { display: none; }
  }

  /* ── Small Phone: ≤ 360px ── */
  @media (max-width: 360px) {
    .header-wave { padding: 36px 10px 32px; }

    .header-name { letter-spacing: -0.2px; line-height: 1.15; }

    .header-role {
      font-size: 0.58rem;
      word-spacing: -1px;
    }

    .typing-strip { font-size: 0.65rem; padding: 12px 10px; }

    .container { padding: 0 10px 32px; }

    .about-card { padding: 12px 14px; font-size: 0.65rem; line-height: 1.7; }

    .badge { padding: 4px 9px; font-size: 0.58rem; }

    .section-divider { gap: 10px; margin: 28px 0 16px; }

    .section-divider .label { font-size: 0.85rem; }
  }

  /* ── Extra-Small: ≤ 320px ── */
  @media (max-width: 320px) {
    .header-name { font-size: 1.8rem; }

    .typing-strip { font-size: 0.6rem; }

    .about-card { font-size: 0.6rem; padding: 10px 12px; }

    .badge { font-size: 0.55rem; padding: 3px 8px; }

    .header-orb { display: none; }
  }
</style>
</head>
<body>

<!-- ═══ HEADER ═══ -->
<div class="header-wave" id="headerWave">
  <div class="header-orb a"></div>
  <div class="header-orb b"></div>
  <div class="header-orb c"></div>

  <h1 class="header-name">Emmanuel Oladipo</h1>
  <p class="header-role">Software Engineer &nbsp;|&nbsp; Full-Stack Developer &nbsp;|&nbsp; Mobile Architect</p>

  <div class="header-badges">
    <a href="https://www.google.com/maps/place/Ibadan,+Nigeria" target="_blank">
      <span class="badge b-tool">📍 Ibadan, Oyo State, Nigeria</span>
    </a>
    <a href="https://emmalink.netlify.app/" target="_blank">
      <span class="badge badge-domain">🌐 Portfolio</span>
    </a>
  </div>
</div>

<!-- ═══ TYPING STRIP ═══ -->
<div class="typing-strip" id="typingStrip">
  <span id="typedText"></span><span class="cursor-blink"></span>
</div>

<!-- ═══ MAIN ═══ -->
<div class="container">

  <!-- About -->
  <div class="section-divider" id="div1">
    <span class="label">🎯 About Me</span>
    <span class="line"></span>
  </div>

  <div class="about-card" id="aboutCard">
    <span class="code-key">const</span> <span style="color:var(--teal)">emmanuel</span> <span class="code-punct">= {</span><br/>
    &nbsp;&nbsp;<span class="code-key">role</span><span class="code-punct">:</span> <span class="code-str">"Software Engineer"</span><span class="code-punct">,</span><br/>
    &nbsp;&nbsp;<span class="code-key">location</span><span class="code-punct">:</span> <span class="code-str">"Ibadan, Nigeria"</span><span class="code-punct">,</span><br/>
    &nbsp;&nbsp;<span class="code-key">passion</span><span class="code-punct">:</span> <span class="code-str">"Building products that matter"</span><span class="code-punct">,</span><br/>
    &nbsp;&nbsp;<span class="code-key">currentFocus</span><span class="code-punct">:</span> <span class="code-arr">["AI Integration", "Cloud Architecture", "Mobile Excellence"]</span><span class="code-punct">,</span><br/>
    &nbsp;&nbsp;<span class="code-key">availableFor</span><span class="code-punct">:</span> <span class="code-str">"Freelance &amp; Collaboration"</span><br/>
    <span class="code-punct">};</span>
  </div>

  <!-- Development Domains -->
  <div class="section-divider" id="div2">
    <span class="label">🌐 Development Domains</span>
    <span class="line"></span>
  </div>

  <div class="badge-group" id="domainBadges">
    <span class="badge badge-domain">⚡ Front-End Development</span>
    <span class="badge badge-domain" style="background:rgba(118,75,162,0.18);color:#b07de0;border-color:rgba(118,75,162,0.35)">🔧 Back-End Web Development</span>
    <span class="badge badge-domain" style="background:rgba(240,147,251,0.12);color:var(--accent);border-color:rgba(240,147,251,0.3)">📱 Mobile Application Development</span>
  </div>

  <!-- Languages -->
  <div class="section-divider" id="div3">
    <span class="label">💻 Languages &amp; Frameworks</span>
    <span class="line"></span>
  </div>

  <div class="badge-group" id="langBadges">
    <span class="badge b-html">● HTML5</span>
    <span class="badge b-css">● CSS3</span>
    <span class="badge b-js">● JavaScript</span>
    <span class="badge b-next">▲ Next.js</span>
    <span class="badge b-react">⚛ React.js</span>
    <span class="badge b-flutter">◆ Flutter</span>
    <span class="badge b-node">⬡ Node.js</span>
    <span class="badge b-php">🐘 PHP</span>
    <span class="badge b-python">🐍 Python</span>
  </div>

  <!-- Databases -->
  <div class="section-divider" id="div4">
    <span class="label">🗄️ Databases &amp; Cloud</span>
    <span class="line"></span>
  </div>

  <div class="badge-group" id="dbBadges">
    <span class="badge b-mysql">🐬 MySQL</span>
    <span class="badge b-mongo">🍃 MongoDB</span>
    <span class="badge b-fire">🔥 Cloud Firestore</span>
  </div>

  <!-- Tools -->
  <div class="section-divider" id="div5">
    <span class="label">🔧 Tools &amp; More</span>
    <span class="line"></span>
  </div>

  <div class="badge-group" id="toolBadges">
    <span class="badge b-tool">VS Code</span>
    <span class="badge b-tool">Postman</span>
    <span class="badge b-tool">GitHub</span>
    <span class="badge b-tool">Notion</span>
    <span class="badge b-tool">Docker</span>
    <span class="badge b-tool">Figma</span>
    <span class="badge b-tool">AI / ML</span>
  </div>

  <!-- Activity Graph -->
  <div class="section-divider" id="div6">
    <span class="label">🌐 Activity Graph</span>
    <span class="line"></span>
  </div>

  <div class="graph-card" id="graphCard">
    <img
      src="https://github-readme-activity-graph.vercel.app/graph?username=Emmanuel4503&bg_color=0D1117&color=667eea&line=764ba2&point=f093fb&area=true&hide_border=true"
      alt="Activity Graph"
    />
  </div>

</div><!-- /container -->

<!-- ═══ FOOTER ═══ -->
<div class="footer-wave" id="footerWave">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:f093fb,50:764ba2,100:667eea&height=120&section=footer" alt="footer wave"/>
</div>

<!-- ═══════════════════════════════════════════
     jQuery ANIMATIONS
═══════════════════════════════════════════ -->
<script>
$(function () {

  /* ── 1. HEADER fade-in on load ── */
  $('#headerWave').delay(100).fadeTo(900, 1);

  /* ── 2. TYPING STRIP — typewriter cycling ── */
  const lines = [
    'Building Digital Experiences 🚀',
    'Crafting Scalable Solutions ⚡',
    'Mobile & Web Architect 📱',
    'Turning Ideas Into Reality ✨'
  ];
  let li = 0, ci = 0, erasing = false;

  $('#typingStrip').delay(600).fadeTo(500, 1);

  function typeLoop() {
    const target = lines[li];
    if (!erasing) {
      if (ci <= target.length) {
        $('#typedText').text(target.slice(0, ci++));
        setTimeout(typeLoop, 55);
      } else {
        setTimeout(() => { erasing = true; typeLoop(); }, 2000);
      }
    } else {
      if (ci > 0) {
        $('#typedText').text(target.slice(0, --ci));
        setTimeout(typeLoop, 28);
      } else {
        erasing = false;
        li = (li + 1) % lines.length;
        setTimeout(typeLoop, 400);
      }
    }
  }
  setTimeout(typeLoop, 800);

  /* ── 3. SCROLL-TRIGGERED stagger fade-in ── */
  const revealQueue = [
    '#div1', '#aboutCard',
    '#div2', '#domainBadges',
    '#div3', '#langBadges',
    '#div4', '#dbBadges',
    '#div5', '#toolBadges',
    '#div6', '#graphCard',
    '#footerWave'
  ];

  function checkReveal() {
    const wBottom = $(window).scrollTop() + $(window).height();
    revealQueue.forEach(function (sel, i) {
      const $el = $(sel);
      if ($el.length && parseFloat($el.css('opacity')) < 0.1) {
        const elTop = $el.offset().top;
        if (wBottom > elTop + 60) {
          $el.delay(i * 40).fadeTo(600, 1);
        }
      }
    });
  }

  $(window).on('scroll', checkReveal);
  setTimeout(checkReveal, 1200); // initial check

  /* ── 4. STAGGER badge entrance (scale + fade) ── */
  function staggerBadges(groupId, delay) {
    $(groupId + ' .badge').each(function (i) {
      const $b = $(this);
      $b.css({ opacity: 0, transform: 'translateY(12px) scale(0.88)' });
      setTimeout(function () {
        $b.animate({ opacity: 1 }, {
          duration: 380,
          step: function (now) {
            const y  = 12 * (1 - now);
            const sc = 0.88 + 0.12 * now;
            $(this).css('transform', 'translateY(' + y + 'px) scale(' + sc + ')');
          }
        });
      }, delay + i * 70);
    });
  }

  // Trigger badge stagger when section enters view
  const badgeGroups = {
    '#domainBadges': false,
    '#langBadges':   false,
    '#dbBadges':     false,
    '#toolBadges':   false
  };

  $(window).on('scroll.badges', function () {
    const wBottom = $(window).scrollTop() + $(window).height();
    $.each(badgeGroups, function (sel, done) {
      if (!done && $(sel).length) {
        const top = $(sel).offset().top;
        if (wBottom > top + 40) {
          badgeGroups[sel] = true;
          staggerBadges(sel, 80);
        }
      }
    });
  });
  setTimeout(function () { $(window).trigger('scroll.badges'); }, 1400);

  /* ── 5. GLOW PULSE on the about card ── */
  setTimeout(function () {
    $('#aboutCard').addClass('glow-pulse');
  }, 2500);

  /* ── 6. HEADER NAME rainbow shimmer ── */
  let hue = 220;
  setInterval(function () {
    hue = (hue + 0.6) % 360;
    // subtle hue-rotate keeps gradient fresh
    $('.header-name').css('filter', 'hue-rotate(' + (hue - 220) + 'deg)');
  }, 40);

  /* ── 7. Hover sparkle: random glow colour on badge touch ── */
  const glows = [
    '0 0 18px rgba(102,126,234,0.7)',
    '0 0 18px rgba(240,147,251,0.7)',
    '0 0 18px rgba(78,205,196,0.7)',
    '0 0 18px rgba(255,107,107,0.6)'
  ];
  $(document).on('mouseenter', '.badge', function () {
    const g = glows[Math.floor(Math.random() * glows.length)];
    $(this).stop(true).animate({ opacity: 1 }, 100).css('box-shadow', g);
  }).on('mouseleave', '.badge', function () {
    $(this).css('box-shadow', '');
  });

});
</script>
</body>
</html>
