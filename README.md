<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Portfolio — Creative Freelancer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;700;800&family=DM+Sans:ital,wght@0,300;0,400;1,300&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0a0a0a;
    --bg2: #111111;
    --bg3: #1a1a1a;
    --accent: #e8ff47;
    --accent2: #ff6b35;
    --text: #f0ede6;
    --muted: #6b6860;
    --border: rgba(240,237,230,0.08);
    --font-display: 'Syne', sans-serif;
    --font-body: 'DM Sans', sans-serif;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-body);
    font-weight: 300;
    line-height: 1.7;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 10px; height: 10px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed; pointer-events: none; z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s ease, width 0.2s, height 0.2s, background 0.2s;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid rgba(232,255,71,0.4);
    border-radius: 50%;
    position: fixed; pointer-events: none; z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.15s ease, width 0.2s, height 0.2s;
  }
  body:has(a:hover) .cursor, body:has(button:hover) .cursor { width: 16px; height: 16px; background: var(--accent2); }
  body:has(a:hover) .cursor-ring, body:has(button:hover) .cursor-ring { width: 52px; height: 52px; }

  /* Nav */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; justify-content: space-between; align-items: center;
    padding: 28px 60px;
    background: linear-gradient(to bottom, rgba(10,10,10,0.95), transparent);
    backdrop-filter: blur(0px);
  }
  .nav-logo {
    font-family: var(--font-display);
    font-weight: 800;
    font-size: 20px;
    letter-spacing: -0.5px;
    color: var(--text);
    text-decoration: none;
  }
  .nav-logo span { color: var(--accent); }
  .nav-links { display: flex; gap: 40px; list-style: none; }
  .nav-links a {
    font-size: 13px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--muted);
    text-decoration: none;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--text); }
  .nav-cta {
    background: var(--accent);
    color: #0a0a0a;
    font-family: var(--font-display);
    font-weight: 700;
    font-size: 13px;
    letter-spacing: 0.05em;
    padding: 10px 24px;
    border: none;
    cursor: none;
    text-decoration: none;
    transition: background 0.2s, transform 0.15s;
  }
  .nav-cta:hover { background: var(--accent2); transform: translateY(-1px); }

  /* Hero */
  #hero {
    min-height: 100vh;
    display: flex; flex-direction: column; justify-content: flex-end;
    padding: 0 60px 80px;
    position: relative;
    overflow: hidden;
  }
  .hero-bg-text {
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    font-family: var(--font-display);
    font-weight: 800;
    font-size: clamp(100px, 18vw, 280px);
    color: rgba(240,237,230,0.03);
    white-space: nowrap;
    user-select: none;
    pointer-events: none;
    letter-spacing: -0.05em;
  }
  .hero-eyebrow {
    font-size: 12px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 24px;
    display: flex; align-items: center; gap: 12px;
  }
  .hero-eyebrow::before {
    content: '';
    display: block; width: 32px; height: 1px;
    background: var(--accent);
  }
  .hero-title {
    font-family: var(--font-display);
    font-weight: 800;
    font-size: clamp(52px, 8vw, 110px);
    line-height: 0.92;
    letter-spacing: -0.04em;
    margin-bottom: 40px;
  }
  .hero-title .line2 { color: var(--accent); display: block; }
  .hero-title .line3 { opacity: 0.25; display: block; }
  .hero-bottom {
    display: flex; justify-content: space-between; align-items: flex-end;
    border-top: 1px solid var(--border);
    padding-top: 32px;
    margin-top: 60px;
  }
  .hero-desc {
    max-width: 360px;
    font-size: 15px;
    color: var(--muted);
    line-height: 1.8;
  }
  .hero-stats { display: flex; gap: 48px; }
  .stat-num {
    font-family: var(--font-display);
    font-size: 36px;
    font-weight: 800;
    color: var(--text);
    display: block;
    line-height: 1;
  }
  .stat-label { font-size: 12px; color: var(--muted); letter-spacing: 0.1em; text-transform: uppercase; margin-top: 4px; }
  .scroll-indicator {
    position: absolute;
    right: 60px; bottom: 80px;
    writing-mode: vertical-rl;
    font-size: 11px;
    letter-spacing: 0.2em;
    color: var(--muted);
    text-transform: uppercase;
    display: flex; align-items: center; gap: 12px;
  }
  .scroll-indicator::after {
    content: '';
    display: block; width: 1px; height: 48px;
    background: var(--border);
    animation: scrollPulse 1.8s ease-in-out infinite;
  }
  @keyframes scrollPulse { 0%,100%{opacity:0.3} 50%{opacity:1} }

  /* Marquee */
  .marquee-wrap {
    overflow: hidden;
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    padding: 18px 0;
    background: var(--bg2);
  }
  .marquee-track {
    display: flex; gap: 0;
    animation: marquee 20s linear infinite;
    width: max-content;
  }
  .marquee-track span {
    font-family: var(--font-display);
    font-size: 13px;
    font-weight: 700;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--muted);
    padding: 0 40px;
    white-space: nowrap;
  }
  .marquee-track span.accent { color: var(--accent); }
  @keyframes marquee { from{transform:translateX(0)} to{transform:translateX(-50%)} }

  /* Section commons */
  section { padding: 120px 60px; }
  .section-label {
    font-size: 11px;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 20px;
    display: flex; align-items: center; gap: 12px;
  }
  .section-label::before { content:''; display:block; width:24px; height:1px; background:var(--accent); }
  .section-title {
    font-family: var(--font-display);
    font-weight: 800;
    font-size: clamp(36px, 5vw, 64px);
    letter-spacing: -0.03em;
    line-height: 1;
  }

  /* About */
  #about { background: var(--bg2); }
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    margin-top: 60px;
    align-items: start;
  }
  .about-img-wrap {
    position: relative;
    aspect-ratio: 4/5;
    background: var(--bg3);
    overflow: hidden;
  }
  .about-img-placeholder {
    width: 100%; height: 100%;
    display: flex; align-items: center; justify-content: center;
    background: linear-gradient(135deg, var(--bg3) 0%, #222 100%);
    position: relative;
    overflow: hidden;
  }
  .about-img-placeholder::before {
    content: '';
    position: absolute; inset: 0;
    background: repeating-linear-gradient(
      45deg,
      transparent,
      transparent 24px,
      rgba(255,255,255,0.02) 24px,
      rgba(255,255,255,0.02) 25px
    );
  }
  .about-img-initials {
    font-family: var(--font-display);
    font-size: 80px;
    font-weight: 800;
    color: rgba(240,237,230,0.08);
    z-index: 1;
  }
  .about-img-tag {
    position: absolute; bottom: 24px; left: 24px;
    background: var(--accent);
    color: #0a0a0a;
    font-family: var(--font-display);
    font-size: 12px;
    font-weight: 700;
    padding: 8px 16px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }
  .about-content {}
  .about-bio {
    font-size: 17px;
    line-height: 1.9;
    color: rgba(240,237,230,0.7);
    margin-bottom: 40px;
  }
  .skills-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-bottom: 40px;
  }
  .skill-item {
    display: flex; align-items: center; gap: 10px;
    font-size: 14px; color: var(--muted);
    letter-spacing: 0.05em;
  }
  .skill-item::before {
    content: '▸';
    color: var(--accent);
    font-size: 10px;
  }
  .about-cta {
    display: inline-flex; align-items: center; gap: 12px;
    font-family: var(--font-display);
    font-weight: 700;
    font-size: 14px;
    color: var(--text);
    text-decoration: none;
    border-bottom: 1px solid var(--accent);
    padding-bottom: 4px;
    transition: color 0.2s, gap 0.2s;
  }
  .about-cta:hover { color: var(--accent); gap: 20px; }

  /* Work */
  #work { background: var(--bg); }
  .work-header {
    display: flex; justify-content: space-between; align-items: flex-end;
    margin-bottom: 60px;
  }
  .work-filter {
    display: flex; gap: 4px;
  }
  .filter-btn {
    background: none;
    border: 1px solid var(--border);
    color: var(--muted);
    font-family: var(--font-body);
    font-size: 12px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 8px 20px;
    cursor: none;
    transition: all 0.2s;
  }
  .filter-btn.active, .filter-btn:hover {
    background: var(--accent);
    color: #0a0a0a;
    border-color: var(--accent);
  }
  .projects-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2px;
  }
  .project-card {
    position: relative;
    background: var(--bg3);
    overflow: hidden;
    aspect-ratio: 4/3;
    cursor: none;
    group: true;
  }
  .project-card:first-child { grid-column: span 2; aspect-ratio: 21/9; }
  .project-bg {
    width: 100%; height: 100%;
    transition: transform 0.5s ease;
    display: flex; align-items: center; justify-content: center;
    font-size: 100px;
    color: rgba(255,255,255,0.04);
    font-family: var(--font-display);
    font-weight: 800;
  }
  .project-card:hover .project-bg { transform: scale(1.04); }
  .project-bg.g1 { background: linear-gradient(135deg, #1a1a2e, #16213e); }
  .project-bg.g2 { background: linear-gradient(135deg, #1a1a1a, #2d1515); }
  .project-bg.g3 { background: linear-gradient(135deg, #0f1a0f, #1a2a1a); }
  .project-bg.g4 { background: linear-gradient(135deg, #1a1528, #0a0a1a); }
  .project-bg.g5 { background: linear-gradient(135deg, #1a1510, #2a2010); }
  .project-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(to top, rgba(10,10,10,0.95) 0%, transparent 60%);
    display: flex; flex-direction: column; justify-content: flex-end;
    padding: 32px;
    opacity: 0;
    transition: opacity 0.3s;
  }
  .project-card:hover .project-overlay { opacity: 1; }
  .project-always {
    position: absolute; bottom: 0; left: 0; right: 0;
    padding: 24px 32px;
    background: linear-gradient(to top, rgba(10,10,10,0.85), transparent);
  }
  .project-tag {
    font-size: 11px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 6px;
  }
  .project-name {
    font-family: var(--font-display);
    font-weight: 700;
    font-size: 22px;
    letter-spacing: -0.02em;
  }
  .project-desc {
    font-size: 13px;
    color: rgba(240,237,230,0.6);
    line-height: 1.6;
    margin-top: 8px;
  }
  .project-link {
    display: inline-flex; align-items: center; gap: 8px;
    color: var(--accent);
    font-family: var(--font-display);
    font-size: 13px;
    font-weight: 700;
    text-decoration: none;
    margin-top: 16px;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  /* Services */
  #services { background: var(--bg2); }
  .services-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    margin-top: 60px;
  }
  .service-card {
    background: var(--bg3);
    padding: 40px 36px;
    border: 1px solid transparent;
    transition: border-color 0.3s, background 0.3s;
    cursor: none;
  }
  .service-card:hover {
    border-color: var(--accent);
    background: rgba(232,255,71,0.03);
  }
  .service-num {
    font-family: var(--font-display);
    font-size: 13px;
    font-weight: 800;
    color: var(--accent);
    letter-spacing: 0.1em;
    margin-bottom: 28px;
  }
  .service-icon {
    font-size: 32px;
    margin-bottom: 20px;
    display: block;
  }
  .service-name {
    font-family: var(--font-display);
    font-size: 22px;
    font-weight: 700;
    letter-spacing: -0.02em;
    margin-bottom: 12px;
  }
  .service-desc { font-size: 14px; color: var(--muted); line-height: 1.8; }

  /* Testimonials */
  #testimonials { background: var(--bg); overflow: hidden; }
  .testimonials-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2px;
    margin-top: 60px;
  }
  .testimonial-card {
    background: var(--bg2);
    padding: 40px;
    border: 1px solid var(--border);
  }
  .testimonial-quote {
    font-size: 13px;
    color: var(--accent);
    margin-bottom: 20px;
    letter-spacing: 0.1em;
  }
  .testimonial-text {
    font-size: 16px;
    line-height: 1.9;
    color: rgba(240,237,230,0.75);
    margin-bottom: 28px;
    font-style: italic;
  }
  .testimonial-author { display: flex; align-items: center; gap: 14px; }
  .author-avatar {
    width: 44px; height: 44px;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-family: var(--font-display);
    font-weight: 800;
    font-size: 16px;
    flex-shrink: 0;
  }
  .av1 { background: rgba(232,255,71,0.12); color: var(--accent); }
  .av2 { background: rgba(255,107,53,0.12); color: var(--accent2); }
  .av3 { background: rgba(100,150,255,0.12); color: #6496ff; }
  .av4 { background: rgba(150,100,255,0.12); color: #9664ff; }
  .author-name { font-family: var(--font-display); font-weight: 700; font-size: 15px; }
  .author-role { font-size: 12px; color: var(--muted); margin-top: 2px; }

  /* Contact */
  #contact {
    background: var(--bg);
    text-align: center;
    display: flex; flex-direction: column; align-items: center;
    padding: 140px 60px;
  }
  .contact-pre {
    font-size: 12px; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--accent); margin-bottom: 24px;
  }
  .contact-big {
    font-family: var(--font-display);
    font-weight: 800;
    font-size: clamp(48px, 8vw, 100px);
    letter-spacing: -0.04em;
    line-height: 0.9;
    margin-bottom: 48px;
  }
  .contact-big em { font-style: normal; color: var(--accent); }
  .contact-email {
    font-family: var(--font-display);
    font-size: clamp(18px, 2.5vw, 28px);
    font-weight: 700;
    color: var(--text);
    text-decoration: none;
    border-bottom: 1px solid var(--border);
    padding-bottom: 8px;
    letter-spacing: -0.02em;
    transition: color 0.2s, border-color 0.2s;
    margin-bottom: 48px;
    display: block;
  }
  .contact-email:hover { color: var(--accent); border-color: var(--accent); }
  .contact-socials { display: flex; gap: 24px; }
  .social-link {
    width: 44px; height: 44px;
    border: 1px solid var(--border);
    display: flex; align-items: center; justify-content: center;
    color: var(--muted);
    text-decoration: none;
    font-size: 14px;
    font-weight: 700;
    letter-spacing: 0.05em;
    transition: all 0.2s;
  }
  .social-link:hover { border-color: var(--accent); color: var(--accent); }

  /* Footer */
  footer {
    background: var(--bg);
    border-top: 1px solid var(--border);
    padding: 28px 60px;
    display: flex; justify-content: space-between; align-items: center;
    font-size: 12px;
    color: var(--muted);
  }
  .footer-logo {
    font-family: var(--font-display);
    font-weight: 800;
    font-size: 16px;
    color: var(--text);
    letter-spacing: -0.02em;
  }
  .footer-logo span { color: var(--accent); }

  /* Animations */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<nav>
  <a href="#hero" class="nav-logo">KIM<span>.</span>J</a>
  <ul class="nav-links">
    <li><a href="#about">About</a></li>
    <li><a href="#work">Work</a></li>
    <li><a href="#services">Services</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
  <a href="#contact" class="nav-cta">Hire Me</a>
</nav>

<!-- Hero -->
<section id="hero">
  <div class="hero-bg-text">CREATE</div>
  <div class="hero-eyebrow">Available for projects · 2025</div>
  <h1 class="hero-title">
    Creative<br>
    <span class="line2">Freelancer</span>
    <span class="line3">& Creator</span>
  </h1>
  <div class="hero-bottom">
    <p class="hero-desc">
      브랜드의 이야기를 시각으로 번역하는 크리에이터.<br>
      아이디어를 현실로 만드는 일에 집중합니다.
    </p>
    <div class="hero-stats">
      <div>
        <span class="stat-num">80+</span>
        <span class="stat-label">Projects Done</span>
      </div>
      <div>
        <span class="stat-num">5yr</span>
        <span class="stat-label">Experience</span>
      </div>
      <div>
        <span class="stat-num">40+</span>
        <span class="stat-label">Happy Clients</span>
      </div>
    </div>
  </div>
  <div class="scroll-indicator">Scroll</div>
</section>

<!-- Marquee -->
<div class="marquee-wrap">
  <div class="marquee-track">
    <span>Brand Identity</span><span class="accent">✦</span>
    <span>Motion Design</span><span class="accent">✦</span>
    <span>Web Design</span><span class="accent">✦</span>
    <span>Visual Storytelling</span><span class="accent">✦</span>
    <span>UI/UX</span><span class="accent">✦</span>
    <span>Content Creation</span><span class="accent">✦</span>
    <span>Photography</span><span class="accent">✦</span>
    <span>Brand Identity</span><span class="accent">✦</span>
    <span>Motion Design</span><span class="accent">✦</span>
    <span>Web Design</span><span class="accent">✦</span>
    <span>Visual Storytelling</span><span class="accent">✦</span>
    <span>UI/UX</span><span class="accent">✦</span>
    <span>Content Creation</span><span class="accent">✦</span>
    <span>Photography</span><span class="accent">✦</span>
  </div>
</div>

<!-- About -->
<section id="about">
  <div class="about-grid">
    <div class="about-img-wrap reveal">
      <div class="about-img-placeholder">
        <span class="about-img-initials">KJ</span>
      </div>
      <div class="about-img-tag">Based in Seoul</div>
    </div>
    <div class="about-content reveal">
      <div class="section-label">About Me</div>
      <h2 class="section-title" style="margin-bottom:32px">I make ideas<br>come alive.</h2>
      <p class="about-bio">
        안녕하세요, 저는 브랜드 정체성과 디지털 경험을 만드는 프리랜서 크리에이터입니다. 서울을 기반으로 글로벌 클라이언트와 협업하며, 단순한 디자인을 넘어 기억에 남는 경험을 만드는 것을 추구합니다.
      </p>
      <div class="skills-list">
        <span class="skill-item">Brand Identity</span>
        <span class="skill-item">Motion Graphics</span>
        <span class="skill-item">Web Design</span>
        <span class="skill-item">Photography</span>
        <span class="skill-item">Content Strategy</span>
        <span class="skill-item">Video Editing</span>
        <span class="skill-item">Social Media</span>
        <span class="skill-item">Illustration</span>
      </div>
      <a href="#contact" class="about-cta">함께 프로젝트 시작하기 →</a>
    </div>
  </div>
</section>

<!-- Work -->
<section id="work">
  <div class="work-header reveal">
    <div>
      <div class="section-label">Selected Work</div>
      <h2 class="section-title">Projects</h2>
    </div>
    <div class="work-filter">
      <button class="filter-btn active">All</button>
      <button class="filter-btn">Branding</button>
      <button class="filter-btn">Web</button>
      <button class="filter-btn">Motion</button>
    </div>
  </div>

  <div class="projects-grid reveal">
    <div class="project-card">
      <div class="project-bg g1">01</div>
      <div class="project-always">
        <div class="project-tag">Branding · Identity</div>
        <div class="project-name">NOVO Coffee Roasters</div>
      </div>
      <div class="project-overlay">
        <div class="project-desc">스페셜티 커피 브랜드의 전체 브랜드 아이덴티티 구축. 로고, 패키지, 웹사이트까지 일관된 세계관 설계.</div>
        <a href="#" class="project-link">View Project ↗</a>
      </div>
    </div>

    <div class="project-card">
      <div class="project-bg g2">02</div>
      <div class="project-always">
        <div class="project-tag">Web · UI/UX</div>
        <div class="project-name">Flux Studio</div>
      </div>
      <div class="project-overlay">
        <div class="project-desc">크리에이티브 에이전시의 포트폴리오 웹사이트 기획 및 디자인. 애니메이션 중심의 인터랙티브 경험.</div>
        <a href="#" class="project-link">View Project ↗</a>
      </div>
    </div>

    <div class="project-card">
      <div class="project-bg g3">03</div>
      <div class="project-always">
        <div class="project-tag">Motion · Content</div>
        <div class="project-name">Minimal Stories</div>
      </div>
      <div class="project-overlay">
        <div class="project-desc">SNS 채널을 위한 모션 콘텐츠 시리즈. 브랜드 스토리를 움직임으로 전달하는 숏폼 영상 제작.</div>
        <a href="#" class="project-link">View Project ↗</a>
      </div>
    </div>

    <div class="project-card">
      <div class="project-bg g4">04</div>
      <div class="project-always">
        <div class="project-tag">Photo · Art Direction</div>
        <div class="project-name">Arthaus Gallery</div>
      </div>
      <div class="project-overlay">
        <div class="project-desc">갤러리 아트 디렉션 및 전시 홍보 콘텐츠 전반. 공간을 화면으로 번역하는 비주얼 언어 구축.</div>
        <a href="#" class="project-link">View Project ↗</a>
      </div>
    </div>

    <div class="project-card">
      <div class="project-bg g5">05</div>
      <div class="project-always">
        <div class="project-tag">Branding · Web</div>
        <div class="project-name">Green Cycles</div>
      </div>
      <div class="project-overlay">
        <div class="project-desc">지속가능 라이프스타일 브랜드의 리브랜딩 프로젝트. 친환경 가치를 모던하게 시각화.</div>
        <a href="#" class="project-link">View Project ↗</a>
      </div>
    </div>
  </div>
</section>

<!-- Services -->
<section id="services">
  <div class="reveal">
    <div class="section-label">What I Do</div>
    <h2 class="section-title">Services</h2>
  </div>
  <div class="services-grid reveal">
    <div class="service-card">
      <div class="service-num">01</div>
      <span class="service-icon">◈</span>
      <div class="service-name">Brand Identity</div>
      <p class="service-desc">로고 디자인부터 브랜드 가이드라인, 패키지 디자인까지. 브랜드의 첫인상과 지속적인 인식을 설계합니다.</p>
    </div>
    <div class="service-card">
      <div class="service-num">02</div>
      <span class="service-icon">◐</span>
      <div class="service-name">Web & UI Design</div>
      <p class="service-desc">사용자 경험을 중심에 놓은 웹사이트 및 앱 UI 디자인. 기능과 미학이 균형 잡힌 디지털 공간을 만듭니다.</p>
    </div>
    <div class="service-card">
      <div class="service-num">03</div>
      <span class="service-icon">▷</span>
      <div class="service-name">Motion & Video</div>
      <p class="service-desc">브랜드 모션 그래픽, SNS 콘텐츠, 숏폼 영상까지. 움직임으로 이야기를 전달하는 콘텐츠를 제작합니다.</p>
    </div>
    <div class="service-card">
      <div class="service-num">04</div>
      <span class="service-icon">⬡</span>
      <div class="service-name">Content Strategy</div>
      <p class="service-desc">소셜미디어 콘텐츠 기획 및 제작. 브랜드 보이스를 일관되게 유지하면서 타겟 오디언스와 소통하는 전략.</p>
    </div>
    <div class="service-card">
      <div class="service-num">05</div>
      <span class="service-icon">◎</span>
      <div class="service-name">Photography</div>
      <p class="service-desc">제품, 라이프스타일, 브랜드 포토그래피. 브랜드의 무드와 스타일을 담은 비주얼 콘텐츠를 촬영합니다.</p>
    </div>
    <div class="service-card">
      <div class="service-num">06</div>
      <span class="service-icon">✦</span>
      <div class="service-name">Art Direction</div>
      <p class="service-desc">캠페인 전체의 비주얼 방향 설정. 아이디어 단계부터 최종 결과물까지 일관된 크리에이티브 리더십 제공.</p>
    </div>
  </div>
</section>

<!-- Testimonials -->
<section id="testimonials">
  <div class="reveal">
    <div class="section-label">Client Reviews</div>
    <h2 class="section-title">What they say</h2>
  </div>
  <div class="testimonials-grid reveal">
    <div class="testimonial-card">
      <div class="testimonial-quote">★★★★★</div>
      <p class="testimonial-text">"브랜드가 원하는 방향을 정확히 이해하고, 기대 이상의 결과물을 내주셨어요. 단순 디자인이 아닌 브랜드 스토리를 함께 만들어주는 파트너입니다."</p>
      <div class="testimonial-author">
        <div class="author-avatar av1">LH</div>
        <div>
          <div class="author-name">이현주</div>
          <div class="author-role">CEO, NOVO Coffee Roasters</div>
        </div>
      </div>
    </div>
    <div class="testimonial-card">
      <div class="testimonial-quote">★★★★★</div>
      <p class="testimonial-text">"커뮤니케이션이 명확하고, 마감을 항상 지켜주세요. 결과물 퀄리티는 물론 작업 과정 자체가 즐거웠습니다. 다음 프로젝트도 함께하고 싶습니다."</p>
      <div class="testimonial-author">
        <div class="author-avatar av2">PJ</div>
        <div>
          <div class="author-name">박진수</div>
          <div class="author-role">Co-founder, Flux Studio</div>
        </div>
      </div>
    </div>
    <div class="testimonial-card">
      <div class="testimonial-quote">★★★★★</div>
      <p class="testimonial-text">"우리 브랜드의 정체성을 완전히 새롭게 만들어주셨어요. 처음에는 막막했던 리브랜딩이 작업을 통해 명확한 방향성을 갖게 되었습니다."</p>
      <div class="testimonial-author">
        <div class="author-avatar av3">KM</div>
        <div>
          <div class="author-name">김민지</div>
          <div class="author-role">Brand Manager, Green Cycles</div>
        </div>
      </div>
    </div>
    <div class="testimonial-card">
      <div class="testimonial-quote">★★★★★</div>
      <p class="testimonial-text">"SNS 콘텐츠 방향을 잡지 못하고 있었는데, 전략부터 실제 제작까지 원스톱으로 해결해주셨어요. 팔로워가 3개월 만에 2배 이상 늘었습니다."</p>
      <div class="testimonial-author">
        <div class="author-avatar av4">SO</div>
        <div>
          <div class="author-name">서지원</div>
          <div class="author-role">Director, Arthaus Gallery</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Contact -->
<section id="contact">
  <div class="contact-pre reveal">Let's Work Together</div>
  <h2 class="contact-big reveal">Got a project<br>in <em>mind?</em></h2>
  <a href="mailto:hello@kimj.studio" class="contact-email reveal">hello@kimj.studio</a>
  <div class="contact-socials reveal">
    <a href="#" class="social-link">IG</a>
    <a href="#" class="social-link">BE</a>
    <a href="#" class="social-link">LI</a>
    <a href="#" class="social-link">YT</a>
  </div>
</section>

<footer>
  <span class="footer-logo">KIM<span>.</span>J</span>
  <span>© 2025 Kim J Studio. All rights reserved.</span>
  <span>Seoul, South Korea</span>
</footer>

<script>
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; cursor.style.left = mx + 'px'; cursor.style.top = my + 'px'; });
  function animRing() { rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12; ring.style.left = rx + 'px'; ring.style.top = ry + 'px'; requestAnimationFrame(animRing); }
  animRing();

  const obs = new IntersectionObserver((entries) => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), e.target.dataset.delay || 0);
      }
    });
  }, { threshold: 0.1 });
  document.querySelectorAll('.reveal').forEach((el, i) => {
    el.dataset.delay = (i % 3) * 100;
    obs.observe(el);
  });

  document.querySelectorAll('.filter-btn').forEach(btn => {
    btn.addEventListener('click', () => {
      document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
    });
  });
</script>
</body>
</html>
