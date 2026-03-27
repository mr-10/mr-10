<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>RAKIB — Android Developer</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600;700&display=swap');

  :root {
    --neon-blue: #00F0FF;
    --neon-purple: #BC13FE;
    --neon-pink: #FF006E;
    --neon-green: #00FF88;
    --bg: #030305;
    --surface: #080810;
    --surface2: #0D0D1A;
    --text: #E0E0E0;
    --text-dim: #888;
    --glow-blue: 0 0 20px #00F0FF, 0 0 40px #00F0FF44;
    --glow-purple: 0 0 20px #BC13FE, 0 0 40px #BC13FE44;
    --glow-pink: 0 0 20px #FF006E, 0 0 40px #FF006E44;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Rajdhani', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    position: fixed;
    width: 12px; height: 12px;
    background: var(--neon-blue);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, background 0.2s;
    box-shadow: var(--glow-blue);
  }
  .cursor-ring {
    position: fixed;
    width: 36px; height: 36px;
    border: 1px solid var(--neon-blue);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.15s ease-out, width 0.2s, height 0.2s;
    opacity: 0.6;
  }

  /* SCAN LINE OVERLAY */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,240,255,0.015) 2px,
      rgba(0,240,255,0.015) 4px
    );
    pointer-events: none;
    z-index: 1000;
  }

  /* GRID BG */
  .grid-bg {
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,240,255,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,240,255,0.04) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
    z-index: 0;
    animation: gridDrift 20s linear infinite;
  }
  @keyframes gridDrift {
    from { transform: translateY(0); }
    to { transform: translateY(60px); }
  }

  /* NAV */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 500;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px 40px;
    background: linear-gradient(180deg, rgba(3,3,5,0.95) 0%, transparent 100%);
    border-bottom: 1px solid rgba(0,240,255,0.1);
    backdrop-filter: blur(10px);
  }

  .nav-logo {
    font-family: 'Orbitron', monospace;
    font-size: 1.2rem;
    font-weight: 900;
    color: var(--neon-blue);
    text-shadow: var(--glow-blue);
    letter-spacing: 4px;
  }

  .nav-links {
    display: flex;
    gap: 32px;
    list-style: none;
  }
  .nav-links a {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.75rem;
    color: var(--text-dim);
    text-decoration: none;
    letter-spacing: 2px;
    transition: color 0.2s, text-shadow 0.2s;
  }
  .nav-links a:hover {
    color: var(--neon-blue);
    text-shadow: var(--glow-blue);
  }

  /* HERO */
  #hero {
    position: relative;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1;
    overflow: hidden;
  }

  .hero-content {
    text-align: center;
    z-index: 2;
    position: relative;
  }

  .hero-tag {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.75rem;
    color: var(--neon-purple);
    letter-spacing: 4px;
    margin-bottom: 20px;
    opacity: 0;
    animation: fadeUp 0.8s 0.2s forwards;
  }

  .hero-name {
    font-family: 'Orbitron', monospace;
    font-size: clamp(3.5rem, 10vw, 8rem);
    font-weight: 900;
    line-height: 0.9;
    letter-spacing: -2px;
    margin-bottom: 16px;
    opacity: 0;
    animation: fadeUp 0.8s 0.4s forwards;
  }

  .hero-name .line1 {
    display: block;
    color: transparent;
    -webkit-text-stroke: 1px var(--neon-blue);
    text-shadow: none;
  }
  .hero-name .line2 {
    display: block;
    color: var(--neon-blue);
    text-shadow: var(--glow-blue);
  }

  .hero-title {
    font-family: 'Rajdhani', sans-serif;
    font-size: clamp(1rem, 3vw, 1.5rem);
    font-weight: 300;
    color: var(--text-dim);
    letter-spacing: 6px;
    text-transform: uppercase;
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeUp 0.8s 0.6s forwards;
  }

  .hero-title span {
    color: var(--neon-pink);
    font-weight: 600;
  }

  .hero-cta {
    display: inline-flex;
    gap: 16px;
    opacity: 0;
    animation: fadeUp 0.8s 0.8s forwards;
  }

  .btn {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.8rem;
    letter-spacing: 2px;
    padding: 14px 32px;
    text-decoration: none;
    border-radius: 4px;
    transition: all 0.3s;
    cursor: none;
  }

  .btn-primary {
    background: var(--neon-blue);
    color: #000;
    border: 1px solid var(--neon-blue);
    box-shadow: var(--glow-blue);
  }
  .btn-primary:hover {
    background: transparent;
    color: var(--neon-blue);
    box-shadow: var(--glow-blue), inset 0 0 20px rgba(0,240,255,0.1);
  }

  .btn-secondary {
    background: transparent;
    color: var(--neon-purple);
    border: 1px solid var(--neon-purple);
  }
  .btn-secondary:hover {
    background: rgba(188,19,254,0.1);
    box-shadow: var(--glow-purple);
  }

  /* FLOATING 3D ELEMENTS */
  .float-element {
    position: absolute;
    pointer-events: none;
    animation: float3d 6s ease-in-out infinite;
  }
  @keyframes float3d {
    0%, 100% { transform: translateY(0) rotateX(0deg) rotateZ(0deg); }
    33% { transform: translateY(-20px) rotateX(5deg) rotateZ(2deg); }
    66% { transform: translateY(-10px) rotateX(-3deg) rotateZ(-1deg); }
  }

  .hex {
    width: 120px; height: 120px;
    clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
    animation-delay: var(--delay);
  }
  .hex-1 { top: 15%; left: 8%; background: rgba(0,240,255,0.05); border: 1px solid rgba(0,240,255,0.2); --delay: 0s; animation-duration: 7s; }
  .hex-2 { top: 60%; right: 6%; background: rgba(188,19,254,0.05); border: 1px solid rgba(188,19,254,0.2); --delay: -2s; animation-duration: 9s; width: 80px; height: 80px; }
  .hex-3 { bottom: 20%; left: 15%; background: rgba(255,0,110,0.05); border: 1px solid rgba(255,0,110,0.2); --delay: -4s; animation-duration: 8s; width: 60px; height: 60px; }
  .hex-4 { top: 30%; right: 12%; background: rgba(0,255,136,0.05); border: 1px solid rgba(0,255,136,0.2); --delay: -1s; animation-duration: 6s; width: 90px; height: 90px; }

  .ring {
    border-radius: 50%;
    border: 1px solid;
    position: absolute;
    animation: ringPulse 4s ease-in-out infinite;
    animation-delay: var(--delay);
  }
  @keyframes ringPulse {
    0%, 100% { transform: scale(1); opacity: 0.3; }
    50% { transform: scale(1.1); opacity: 0.8; }
  }
  .ring-1 { width: 300px; height: 300px; top: 10%; right: -50px; border-color: rgba(0,240,255,0.15); --delay: 0s; }
  .ring-2 { width: 200px; height: 200px; bottom: 15%; left: -30px; border-color: rgba(188,19,254,0.15); --delay: -2s; }

  /* SECTIONS */
  section {
    position: relative;
    z-index: 1;
    padding: 100px 40px;
    max-width: 1100px;
    margin: 0 auto;
  }

  .section-header {
    display: flex;
    align-items: center;
    gap: 20px;
    margin-bottom: 60px;
  }

  .section-number {
    font-family: 'Orbitron', monospace;
    font-size: 0.7rem;
    color: var(--neon-purple);
    letter-spacing: 3px;
  }

  .section-title {
    font-family: 'Orbitron', monospace;
    font-size: clamp(1.5rem, 4vw, 2.5rem);
    font-weight: 700;
    color: var(--text);
    letter-spacing: 2px;
  }

  .section-line {
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, rgba(0,240,255,0.4), transparent);
  }

  /* ABOUT */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 48px;
    align-items: center;
  }

  .about-text p {
    font-size: 1.1rem;
    line-height: 1.9;
    color: var(--text-dim);
    margin-bottom: 20px;
  }
  .about-text p strong {
    color: var(--neon-blue);
    font-weight: 600;
  }

  .about-stats {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }

  .stat-card {
    background: var(--surface);
    border: 1px solid rgba(0,240,255,0.1);
    border-radius: 12px;
    padding: 24px;
    text-align: center;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }
  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--neon-blue), var(--neon-purple));
  }
  .stat-card:hover {
    border-color: rgba(0,240,255,0.4);
    box-shadow: 0 0 30px rgba(0,240,255,0.1);
    transform: translateY(-4px);
  }

  .stat-number {
    font-family: 'Orbitron', monospace;
    font-size: 2rem;
    font-weight: 900;
    color: var(--neon-blue);
    text-shadow: var(--glow-blue);
    display: block;
  }
  .stat-label {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.7rem;
    color: var(--text-dim);
    letter-spacing: 2px;
    margin-top: 4px;
  }

  /* PROJECTS */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 24px;
  }

  .project-card {
    background: var(--surface);
    border: 1px solid rgba(0,240,255,0.08);
    border-radius: 16px;
    padding: 32px;
    transition: all 0.4s cubic-bezier(0.23, 1, 0.32, 1);
    position: relative;
    overflow: hidden;
    cursor: none;
    transform-style: preserve-3d;
  }

  .project-card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba(0,240,255,0.04), rgba(188,19,254,0.04));
    opacity: 0;
    transition: opacity 0.3s;
  }
  .project-card:hover::before { opacity: 1; }

  .project-card:hover {
    border-color: rgba(0,240,255,0.3);
    box-shadow:
      0 20px 60px rgba(0,0,0,0.5),
      0 0 30px rgba(0,240,255,0.08),
      inset 0 1px 0 rgba(255,255,255,0.05);
    transform: translateY(-8px) rotateX(2deg);
  }

  .project-accent {
    position: absolute;
    top: 0; right: 0;
    width: 80px; height: 80px;
    background: radial-gradient(circle, var(--accent-color) 0%, transparent 70%);
    opacity: 0.15;
    border-radius: 50%;
    transform: translate(20px, -20px);
  }

  .project-icon {
    font-size: 2rem;
    margin-bottom: 16px;
    display: block;
  }

  .project-name {
    font-family: 'Orbitron', monospace;
    font-size: 1rem;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 8px;
    letter-spacing: 1px;
  }

  .project-desc {
    font-size: 0.95rem;
    color: var(--text-dim);
    line-height: 1.7;
    margin-bottom: 20px;
  }

  .project-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 24px;
  }

  .tag {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.65rem;
    padding: 4px 10px;
    border-radius: 4px;
    letter-spacing: 1px;
    border: 1px solid;
  }
  .tag-blue { color: var(--neon-blue); border-color: rgba(0,240,255,0.3); background: rgba(0,240,255,0.05); }
  .tag-purple { color: var(--neon-purple); border-color: rgba(188,19,254,0.3); background: rgba(188,19,254,0.05); }
  .tag-pink { color: var(--neon-pink); border-color: rgba(255,0,110,0.3); background: rgba(255,0,110,0.05); }
  .tag-green { color: var(--neon-green); border-color: rgba(0,255,136,0.3); background: rgba(0,255,136,0.05); }

  .project-link {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.7rem;
    color: var(--neon-blue);
    text-decoration: none;
    letter-spacing: 2px;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    transition: gap 0.2s, text-shadow 0.2s;
  }
  .project-link:hover {
    gap: 14px;
    text-shadow: var(--glow-blue);
  }
  .project-link::after { content: '→'; }

  /* STACK */
  .stack-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    gap: 16px;
  }

  .stack-item {
    background: var(--surface);
    border: 1px solid rgba(0,240,255,0.08);
    border-radius: 12px;
    padding: 20px;
    text-align: center;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }
  .stack-item:hover {
    border-color: var(--item-color);
    box-shadow: 0 0 20px color-mix(in srgb, var(--item-color) 20%, transparent);
    transform: translateY(-4px);
  }

  .stack-icon { font-size: 1.8rem; display: block; margin-bottom: 10px; }
  .stack-name {
    font-family: 'Orbitron', monospace;
    font-size: 0.7rem;
    font-weight: 700;
    letter-spacing: 1px;
    color: var(--item-color, var(--text));
  }
  .stack-sub {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.6rem;
    color: var(--text-dim);
    margin-top: 4px;
    letter-spacing: 1px;
  }

  /* TIMELINE */
  .timeline { position: relative; padding-left: 40px; }
  .timeline::before {
    content: '';
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 1px;
    background: linear-gradient(180deg, var(--neon-blue), var(--neon-purple), transparent);
  }

  .timeline-item {
    position: relative;
    margin-bottom: 48px;
    opacity: 0;
    transform: translateX(-20px);
    animation: slideIn 0.6s forwards;
    animation-delay: var(--delay);
  }
  @keyframes slideIn {
    to { opacity: 1; transform: translateX(0); }
  }

  .timeline-dot {
    position: absolute;
    left: -44px; top: 4px;
    width: 10px; height: 10px;
    border-radius: 50%;
    background: var(--neon-blue);
    box-shadow: var(--glow-blue);
    border: 2px solid var(--bg);
  }

  .timeline-date {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.7rem;
    color: var(--neon-purple);
    letter-spacing: 2px;
    margin-bottom: 8px;
  }

  .timeline-title {
    font-family: 'Orbitron', monospace;
    font-size: 1rem;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 8px;
    letter-spacing: 1px;
  }

  .timeline-desc {
    font-size: 0.95rem;
    color: var(--text-dim);
    line-height: 1.7;
  }

  /* CONTACT */
  .contact-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 48px;
    align-items: start;
  }

  .contact-intro {
    font-size: 1.1rem;
    color: var(--text-dim);
    line-height: 1.9;
    margin-bottom: 32px;
  }
  .contact-intro strong { color: var(--neon-blue); }

  .contact-links { display: flex; flex-direction: column; gap: 16px; }

  .contact-link {
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 18px 24px;
    background: var(--surface);
    border: 1px solid rgba(0,240,255,0.08);
    border-radius: 12px;
    text-decoration: none;
    transition: all 0.3s;
    cursor: none;
  }
  .contact-link:hover {
    border-color: var(--link-color);
    box-shadow: 0 0 20px color-mix(in srgb, var(--link-color) 20%, transparent);
    transform: translateX(8px);
  }

  .contact-link-icon { font-size: 1.3rem; }
  .contact-link-text {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.8rem;
    color: var(--text-dim);
    letter-spacing: 1px;
  }
  .contact-link:hover .contact-link-text { color: var(--link-color); }

  /* TERMINAL CONTACT FORM */
  .terminal {
    background: var(--surface2);
    border: 1px solid rgba(0,240,255,0.15);
    border-radius: 16px;
    overflow: hidden;
  }

  .terminal-bar {
    background: rgba(0,240,255,0.05);
    padding: 12px 20px;
    display: flex;
    align-items: center;
    gap: 8px;
    border-bottom: 1px solid rgba(0,240,255,0.1);
  }

  .dot { width: 10px; height: 10px; border-radius: 50%; }
  .dot-red { background: #FF006E; }
  .dot-yellow { background: #FFCC00; }
  .dot-green { background: #00FF88; }

  .terminal-title {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.7rem;
    color: var(--text-dim);
    margin-left: 8px;
    letter-spacing: 2px;
  }

  .terminal-body { padding: 24px; }

  .terminal-line {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.85rem;
    color: var(--text-dim);
    margin-bottom: 16px;
    line-height: 1.6;
  }
  .terminal-line .prompt { color: var(--neon-green); margin-right: 8px; }
  .terminal-line .cmd { color: var(--neon-blue); }
  .terminal-line .output { color: var(--text-dim); padding-left: 20px; display: block; }
  .terminal-line .highlight { color: var(--neon-purple); }

  .cursor-blink {
    display: inline-block;
    width: 8px; height: 14px;
    background: var(--neon-blue);
    animation: blink 1s step-end infinite;
    vertical-align: middle;
    margin-left: 2px;
  }
  @keyframes blink { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }

  /* FOOTER */
  footer {
    position: relative;
    z-index: 1;
    border-top: 1px solid rgba(0,240,255,0.08);
    padding: 40px;
    text-align: center;
  }

  .footer-logo {
    font-family: 'Orbitron', monospace;
    font-size: 1rem;
    font-weight: 900;
    color: var(--neon-blue);
    letter-spacing: 6px;
    text-shadow: var(--glow-blue);
    margin-bottom: 12px;
  }

  .footer-copy {
    font-family: 'Share Tech Mono', monospace;
    font-size: 0.7rem;
    color: var(--text-dim);
    letter-spacing: 2px;
  }
  .footer-copy span { color: var(--neon-pink); }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .reveal {
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 0.8s, transform 0.8s;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* GLITCH EFFECT */
  .glitch {
    position: relative;
  }
  .glitch::before, .glitch::after {
    content: attr(data-text);
    position: absolute;
    inset: 0;
    font-family: inherit;
    font-size: inherit;
    font-weight: inherit;
    letter-spacing: inherit;
  }
  .glitch::before {
    color: var(--neon-pink);
    animation: glitch1 3s infinite;
    clip-path: polygon(0 0, 100% 0, 100% 40%, 0 40%);
  }
  .glitch::after {
    color: var(--neon-blue);
    animation: glitch2 3s infinite;
    clip-path: polygon(0 60%, 100% 60%, 100% 100%, 0 100%);
  }
  @keyframes glitch1 {
    0%, 90%, 100% { transform: none; opacity: 0; }
    92% { transform: translateX(-3px); opacity: 0.8; }
    94% { transform: translateX(3px); opacity: 0.8; }
    96% { transform: translateX(-2px); opacity: 0.8; }
  }
  @keyframes glitch2 {
    0%, 90%, 100% { transform: none; opacity: 0; }
    93% { transform: translateX(3px); opacity: 0.8; }
    95% { transform: translateX(-3px); opacity: 0.8; }
    97% { transform: translateX(2px); opacity: 0.8; }
  }

  /* RESPONSIVE */
  @media (max-width: 768px) {
    nav { padding: 16px 20px; }
    .nav-links { display: none; }
    section { padding: 80px 20px; }
    .about-grid, .contact-grid { grid-template-columns: 1fr; }
    .hero-name { font-size: 3rem; }
    .hero-cta { flex-direction: column; align-items: center; }
    .stack-grid { grid-template-columns: repeat(3, 1fr); }
  }
</style>
</head>
<body>

<!-- CURSOR -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- GRID BG -->
<div class="grid-bg"></div>

<!-- NAV -->
<nav>
  <div class="nav-logo">RK/</div>
  <ul class="nav-links">
    <li><a href="#about">ABOUT</a></li>
    <li><a href="#projects">PROJECTS</a></li>
    <li><a href="#stack">STACK</a></li>
    <li><a href="#journey">JOURNEY</a></li>
    <li><a href="#contact">CONTACT</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero" style="max-width:100%; padding: 0; margin: 0;">
  <div class="float-element hex hex-1"></div>
  <div class="float-element hex hex-2"></div>
  <div class="float-element hex hex-3"></div>
  <div class="float-element hex hex-4"></div>
  <div class="float-element ring ring-1"></div>
  <div class="float-element ring ring-2"></div>

  <div class="hero-content">
    <div class="hero-tag">// ANDROID DEVELOPER & BUILDER FROM BANGLADESH</div>
    <h1 class="hero-name">
      <span class="line1 glitch" data-text="RAKIB">RAKIB</span>
      <span class="line2">HOSSAIN</span>
    </h1>
    <p class="hero-title">
      Kotlin · Jetpack Compose · <span>Cyberpunk UI</span>
    </p>
    <div class="hero-cta">
      <a href="#projects" class="btn btn-primary">VIEW PROJECTS</a>
      <a href="#contact" class="btn btn-secondary">CONTACT ME</a>
    </div>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="section-header reveal">
    <span class="section-number">01</span>
    <h2 class="section-title">ABOUT</h2>
    <div class="section-line"></div>
  </div>

  <div class="about-grid">
    <div class="about-text reveal">
      <p>
        I'm a developer from <strong>Jashore, Bangladesh</strong> — building Android apps with clean architecture and a strong aesthetic sense.
      </p>
      <p>
        My focus is <strong>Kotlin + Jetpack Compose</strong> on Android and TypeScript on the web. I care deeply about both the technical quality of the code and how the product actually feels to use.
      </p>
      <p>
        Currently building <strong>UniWorld</strong> — a global university discovery platform — and shipping utilities like <strong>PrivGuard</strong>, a cyberpunk AES encryption app.
      </p>
      <p>
        I'm also a photographer and use AI tools strategically to move faster without compromising quality.
      </p>
    </div>

    <div class="about-stats reveal">
      <div class="stat-card">
        <span class="stat-number">4+</span>
        <span class="stat-label">PROJECTS SHIPPED</span>
      </div>
      <div class="stat-card">
        <span class="stat-number">2</span>
        <span class="stat-label">LANGUAGES</span>
      </div>
      <div class="stat-card">
        <span class="stat-number">AES</span>
        <span class="stat-label">128-BIT ENCRYPTION</span>
      </div>
      <div class="stat-card">
        <span class="stat-number">∞</span>
        <span class="stat-label">BUILDING MODE</span>
      </div>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects" style="max-width:100%; padding-left: 40px; padding-right: 40px; margin: 0 auto; max-width: 1100px;">
  <div class="section-header reveal">
    <span class="section-number">02</span>
    <h2 class="section-title">PROJECTS</h2>
    <div class="section-line"></div>
  </div>

  <div class="projects-grid">

    <div class="project-card reveal" style="--delay:0.1s">
      <div class="project-accent" style="--accent-color: #00F0FF;"></div>
      <span class="project-icon">🔐</span>
      <div class="project-name">PRIVGUARD</div>
      <p class="project-desc">AES-128/CBC encryption & decryption Android app. Cyberpunk neon UI, dark/light theme toggle, clipboard copy. 100% offline — no accounts, no tracking.</p>
      <div class="project-tags">
        <span class="tag tag-blue">KOTLIN</span>
        <span class="tag tag-blue">JETPACK COMPOSE</span>
        <span class="tag tag-purple">MVVM</span>
        <span class="tag tag-pink">AES-128</span>
      </div>
      <a href="https://github.com/mr-10/PrivGuard" class="project-link" target="_blank">VIEW ON GITHUB</a>
    </div>

    <div class="project-card reveal" style="--delay:0.2s">
      <div class="project-accent" style="--accent-color: #BC13FE;"></div>
      <span class="project-icon">🎓</span>
      <div class="project-name">UNIWORLD</div>
      <p class="project-desc">Global university discovery & application assistant. 5-tab mobile app with university database, scholarship tracker, email draft generator, and comparison engine.</p>
      <div class="project-tags">
        <span class="tag tag-blue">TYPESCRIPT</span>
        <span class="tag tag-green">REACT NATIVE</span>
        <span class="tag tag-purple">EXPO</span>
        <span class="tag tag-pink">AI-POWERED</span>
      </div>
      <a href="https://github.com/mr-10/uniworld-app" class="project-link" target="_blank">VIEW ON GITHUB</a>
    </div>

    <div class="project-card reveal" style="--delay:0.3s">
      <div class="project-accent" style="--accent-color: #FF006E;"></div>
      <span class="project-icon">📸</span>
      <div class="project-name">LOVLOOM</div>
      <p class="project-desc">AI-powered photo regeneration WebAPK using Google Gemini. Three distinct processing methods to transform and enhance photographs. Built with AI Studio.</p>
      <div class="project-tags">
        <span class="tag tag-blue">TYPESCRIPT</span>
        <span class="tag tag-pink">GEMINI AI</span>
        <span class="tag tag-green">WEBAPK</span>
        <span class="tag tag-purple">AI STUDIO</span>
      </div>
      <a href="https://github.com/mr-10/LovLoom" class="project-link" target="_blank">VIEW ON GITHUB</a>
    </div>

    <div class="project-card reveal" style="--delay:0.4s">
      <div class="project-accent" style="--accent-color: #00FF88;"></div>
      <span class="project-icon">🚨</span>
      <div class="project-name">LOCAL SHEBA</div>
      <p class="project-desc">Emergency services connector app for local communities. Built to bridge people with the help they need, fast. TypeScript + React Native.</p>
      <div class="project-tags">
        <span class="tag tag-blue">TYPESCRIPT</span>
        <span class="tag tag-green">REACT NATIVE</span>
        <span class="tag tag-green">EMERGENCY</span>
      </div>
      <a href="https://github.com/mr-10/Local-Sheba" class="project-link" target="_blank">VIEW ON GITHUB</a>
    </div>

  </div>
</section>

<!-- STACK -->
<section id="stack">
  <div class="section-header reveal">
    <span class="section-number">03</span>
    <h2 class="section-title">STACK</h2>
    <div class="section-line"></div>
  </div>

  <div class="stack-grid reveal">
    <div class="stack-item" style="--item-color: #7F52FF">
      <span class="stack-icon">🟣</span>
      <div class="stack-name">KOTLIN</div>
      <div class="stack-sub">PRIMARY LANG</div>
    </div>
    <div class="stack-item" style="--item-color: #4285F4">
      <span class="stack-icon">🔵</span>
      <div class="stack-name">COMPOSE</div>
      <div class="stack-sub">JETPACK UI</div>
    </div>
    <div class="stack-item" style="--item-color: #3178C6">
      <span class="stack-icon">📘</span>
      <div class="stack-name">TYPESCRIPT</div>
      <div class="stack-sub">WEB & MOBILE</div>
    </div>
    <div class="stack-item" style="--item-color: #61DAFB">
      <span class="stack-icon">⚛️</span>
      <div class="stack-name">REACT NATIVE</div>
      <div class="stack-sub">CROSS-PLATFORM</div>
    </div>
    <div class="stack-item" style="--item-color: #06B6D4">
      <span class="stack-icon">🌊</span>
      <div class="stack-name">TAILWIND</div>
      <div class="stack-sub">STYLING</div>
    </div>
    <div class="stack-item" style="--item-color: #3DDC84">
      <span class="stack-icon">🤖</span>
      <div class="stack-name">ANDROID</div>
      <div class="stack-sub">NATIVE SDK</div>
    </div>
    <div class="stack-item" style="--item-color: #00F0FF">
      <span class="stack-icon">🔐</span>
      <div class="stack-name">AES-128</div>
      <div class="stack-sub">ENCRYPTION</div>
    </div>
    <div class="stack-item" style="--item-color: #FF006E">
      <span class="stack-icon">🧠</span>
      <div class="stack-name">GEMINI AI</div>
      <div class="stack-sub">AI TOOLS</div>
    </div>
    <div class="stack-item" style="--item-color: #BC13FE">
      <span class="stack-icon">⚡</span>
      <div class="stack-name">MANUS AI</div>
      <div class="stack-sub">ORCHESTRATION</div>
    </div>
  </div>
</section>

<!-- JOURNEY -->
<section id="journey">
  <div class="section-header reveal">
    <span class="section-number">04</span>
    <h2 class="section-title">JOURNEY</h2>
    <div class="section-line"></div>
  </div>

  <div class="timeline">
    <div class="timeline-item" style="--delay: 0.1s">
      <div class="timeline-dot"></div>
      <div class="timeline-date">2026 — PRESENT</div>
      <div class="timeline-title">ANDROID DEVELOPER · KOTLIN</div>
      <p class="timeline-desc">Building production Android apps with Jetpack Compose and clean MVVM architecture. Shipped PrivGuard (AES encryption) and multiple utility apps.</p>
    </div>
    <div class="timeline-item" style="--delay: 0.2s">
      <div class="timeline-dot" style="background: var(--neon-purple); box-shadow: var(--glow-purple);"></div>
      <div class="timeline-date">2025 — 2026</div>
      <div class="timeline-title">FULL-STACK BUILDER · WEB & MOBILE</div>
      <p class="timeline-desc">Expanded into TypeScript and React Native. Built UniWorld (university platform) and LovLoom (AI photo app). Started using AI tools strategically in the build process.</p>
    </div>
    <div class="timeline-item" style="--delay: 0.3s">
      <div class="timeline-dot" style="background: var(--neon-pink); box-shadow: var(--glow-pink);"></div>
      <div class="timeline-date">EARLIER</div>
      <div class="timeline-title">STUDENT · ECONOMICS · JASHORE COLLEGE</div>
      <p class="timeline-desc">Studying Economics while teaching myself Android development. Began exploring Kotlin, clean architecture, and cyberpunk design aesthetics.</p>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="section-header reveal">
    <span class="section-number">05</span>
    <h2 class="section-title">CONTACT</h2>
    <div class="section-line"></div>
  </div>

  <div class="contact-grid">
    <div class="reveal">
      <p class="contact-intro">
        Building something interesting? Want to collaborate? I'm always open to <strong>real projects</strong> with real purpose.
      </p>
      <div class="contact-links">
        <a href="https://github.com/mr-10" class="contact-link" target="_blank" style="--link-color: #E0E0E0">
          <span class="contact-link-icon">⚡</span>
          <span class="contact-link-text">GITHUB / MR-10</span>
        </a>
        <a href="mailto:your@protonmail.com" class="contact-link" style="--link-color: #6D4AFF">
          <span class="contact-link-icon">🛡️</span>
          <span class="contact-link-text">PROTON MAIL</span>
        </a>
        <a href="https://t.me/yourusername" class="contact-link" target="_blank" style="--link-color: #26A5E4">
          <span class="contact-link-icon">✈️</span>
          <span class="contact-link-text">TELEGRAM</span>
        </a>
      </div>
    </div>

    <div class="terminal reveal">
      <div class="terminal-bar">
        <div class="dot dot-red"></div>
        <div class="dot dot-yellow"></div>
        <div class="dot dot-green"></div>
        <span class="terminal-title">rakib@privguard ~ contact.sh</span>
      </div>
      <div class="terminal-body">
        <div class="terminal-line">
          <span class="prompt">❯</span>
          <span class="cmd">whoami</span>
          <span class="output">Rakib · Android Dev · Jashore, Bangladesh</span>
        </div>
        <div class="terminal-line">
          <span class="prompt">❯</span>
          <span class="cmd">cat skills.txt</span>
          <span class="output"><span class="highlight">Kotlin</span> · Jetpack Compose · TypeScript · AES Encryption</span>
        </div>
        <div class="terminal-line">
          <span class="prompt">❯</span>
          <span class="cmd">echo $STATUS</span>
          <span class="output" style="color: var(--neon-green);">✓ OPEN TO COLLABORATION</span>
        </div>
        <div class="terminal-line">
          <span class="prompt">❯</span>
          <span class="cmd">cat current_mission.txt</span>
          <span class="output">Building UniWorld · Studying abroad · Shipping apps</span>
        </div>
        <div class="terminal-line">
          <span class="prompt">❯</span>
          <span class="cursor-blink"></span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">RAKIB</div>
  <p class="footer-copy">JASHORE, BANGLADESH · 2026 · BUILT WITH <span>♥</span> AND NEON</p>
</footer>

<script>
  // CURSOR
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
  });

  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  document.querySelectorAll('a, button, .project-card, .stat-card, .stack-item').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.transform = 'translate(-50%, -50%) scale(2)';
      cursor.style.background = '#BC13FE';
      ring.style.width = '60px';
      ring.style.height = '60px';
      ring.style.borderColor = '#BC13FE';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.transform = 'translate(-50%, -50%) scale(1)';
      cursor.style.background = '#00F0FF';
      ring.style.width = '36px';
      ring.style.height = '36px';
      ring.style.borderColor = '#00F0FF';
    });
  });

  // SCROLL REVEAL
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) e.target.classList.add('visible');
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // 3D CARD TILT
  document.querySelectorAll('.project-card').forEach(card => {
    card.addEventListener('mousemove', e => {
      const r = card.getBoundingClientRect();
      const x = (e.clientX - r.left) / r.width - 0.5;
      const y = (e.clientY - r.top) / r.height - 0.5;
      card.style.transform = `translateY(-8px) rotateX(${-y * 10}deg) rotateY(${x * 10}deg)`;
    });
    card.addEventListener('mouseleave', () => {
      card.style.transform = '';
    });
  });
</script>
</body>
</html>
