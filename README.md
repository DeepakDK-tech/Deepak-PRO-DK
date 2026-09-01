# Deepak-PRO-DK
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Deepak Kumar — Embedded Systems &amp; Electronics Engineer</title>
<meta name="description" content="Portfolio of Deepak Kumar — Electronics &amp; Communication Engineer specializing in embedded systems, IoT, robotics and PCB design.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600;700&family=IBM+Plex+Sans:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  /* =========================================================
     TOKENS
     Concept: PCB soldermask (dark) vs. printed datasheet (light)
     ========================================================= */
  :root{
    --bg:#0A0E17;
    --panel:#111826;
    --panel-2:#0D1320;
    --line:#232C3D;
    --copper:#C97A4E;
    --copper-bright:#E39469;
    --silk:#E7E4D8;
    --silk-dim:#9AA1AF;
    --teal:#5EC8C0;
    --amber:#E0B04B;
    --radius:2px;
    --mono:'IBM Plex Mono', ui-monospace, monospace;
    --sans:'IBM Plex Sans', system-ui, sans-serif;
    --trace-x: 46px;
  }
  [data-theme="light"]{
    --bg:#F3F1EA;
    --panel:#FFFFFF;
    --panel-2:#EDEAE0;
    --line:#D8D3C4;
    --copper:#A85A2E;
    --copper-bright:#8A4720;
    --silk:#181611;
    --silk-dim:#5A5648;
    --teal:#2C7E78;
    --amber:#9C6E1E;
  }

  *{box-sizing:border-box; margin:0; padding:0;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--bg);
    color:var(--silk);
    font-family:var(--sans);
    line-height:1.55;
    -webkit-font-smoothing:antialiased;
    transition:background .25s ease, color .25s ease;
    overflow-x:hidden;
  }
  a{color:inherit; text-decoration:none;}
  img{max-width:100%; display:block;}
  ::selection{background:var(--copper); color:#0A0E17;}
  :focus-visible{outline:2px solid var(--teal); outline-offset:3px;}

  .wrap{max-width:1120px; margin:0 auto; padding:0 24px;}
  @media (min-width:900px){ .wrap{padding-left: calc(24px + var(--trace-x)); } }

  .eyebrow{
    font-family:var(--mono);
    font-size:12px;
    letter-spacing:.14em;
    text-transform:uppercase;
    color:var(--copper);
  }
  h1,h2,h3{font-family:var(--mono); font-weight:600; letter-spacing:-0.01em;}
  .text-dim{color:var(--silk-dim);}

  /* =========================================================
     TRACE — signature element: a copper trace runs the length
     of the page, with square pads marking each section, labeled
     by real PCB reference-designator prefixes (U/R/J/Q/K/D).
     ========================================================= */
  #trace-svg{
    position:absolute; top:0; left:0; width:2px; height:100%;
    pointer-events:none; z-index:0; display:none;
  }
  @media (min-width:900px){ #trace-svg{ display:block; } }
  .trace-path{
    stroke:var(--line);
    stroke-width:2;
  }
  .trace-path-fill{
    stroke:var(--copper);
    stroke-width:2;
    stroke-dasharray: 1 1;
    transition: stroke-dashoffset .15s linear;
  }
  .pad{
    position:absolute; left:calc(var(--trace-x) - 6px);
    width:12px; height:12px; background:var(--panel);
    border:2px solid var(--line);
    transform:rotate(45deg);
    z-index:1; display:none;
  }
  @media (min-width:900px){ .pad{display:block;} }
  .pad.on{ border-color:var(--copper); background:var(--copper); }
  .pad-label{
    position:absolute; left:calc(var(--trace-x) + 18px);
    font-family:var(--mono); font-size:11px; color:var(--silk-dim);
    letter-spacing:.06em; white-space:nowrap; display:none;
  }
  @media (min-width:900px){ .pad-label{display:block;} }

  /* =========================================================
     NAV
     ========================================================= */
  header{
    position:sticky; top:0; z-index:50;
    background:color-mix(in srgb, var(--bg) 88%, transparent);
    backdrop-filter:blur(10px);
    border-bottom:1px solid var(--line);
  }
  .navbar{
    display:flex; align-items:center; justify-content:space-between;
    padding:16px 24px;
  }
  @media (min-width:900px){ .navbar{padding-left: calc(24px + var(--trace-x)); } }
  .logo{
    font-family:var(--mono); font-weight:700; font-size:15px;
    letter-spacing:.04em;
    display:flex; align-items:center; gap:8px;
  }
  .logo .dot{width:8px; height:8px; background:var(--teal); border-radius:50%; box-shadow:0 0 8px var(--teal);}
  nav ul{list-style:none; display:none; gap:28px;}
  @media (min-width:760px){ nav ul{display:flex;} }
  nav a{
    font-family:var(--mono); font-size:13px; color:var(--silk-dim);
    text-transform:uppercase; letter-spacing:.06em;
    position:relative; padding:4px 0;
  }
  nav a:hover{color:var(--silk);}
  nav a::after{
    content:""; position:absolute; left:0; bottom:-2px; width:0; height:1px;
    background:var(--copper); transition:width .2s ease;
  }
  nav a:hover::after{width:100%;}
  .nav-right{display:flex; align-items:center; gap:14px;}
  .theme-btn{
    font-family:var(--mono); font-size:11px; letter-spacing:.06em;
    border:1px solid var(--line); background:var(--panel);
    color:var(--silk-dim); padding:7px 10px; border-radius:var(--radius);
    cursor:pointer; text-transform:uppercase;
  }
  .theme-btn:hover{border-color:var(--copper); color:var(--copper-bright);}
  .menu-btn{display:block; background:none; border:1px solid var(--line); color:var(--silk); padding:7px 9px; border-radius:var(--radius); cursor:pointer; font-family:var(--mono);}
  @media (min-width:760px){ .menu-btn{display:none;} }
  #mobile-nav{
    display:none; flex-direction:column; gap:2px; padding:8px 24px 18px;
    border-bottom:1px solid var(--line); background:var(--bg);
  }
  #mobile-nav.open{display:flex;}
  #mobile-nav a{
    font-family:var(--mono); font-size:13px; padding:10px 0; color:var(--silk-dim);
    border-bottom:1px dashed var(--line); text-transform:uppercase; letter-spacing:.06em;
  }

  section{position:relative; z-index:1; padding:88px 0 0;}
  .section-inner{padding-bottom:88px; border-bottom:1px solid var(--line);}
  section:last-of-type .section-inner{border-bottom:none;}

  .section-head{margin-bottom:40px;}
  .section-head h2{font-size:26px; margin-top:8px;}

  /* =========================================================
     HERO
     ========================================================= */
  .hero{padding-top:64px;}
  .hero-grid{
    display:grid; grid-template-columns:1fr; gap:48px; align-items:center;
  }
  @media (min-width:860px){ .hero-grid{grid-template-columns:1.15fr .85fr;} }

  .designator{
    font-family:var(--mono); font-size:12px; color:var(--copper);
    border:1px solid var(--line); display:inline-flex; align-items:center; gap:8px;
    padding:6px 10px; border-radius:var(--radius); margin-bottom:22px;
  }
  .designator .pin{width:6px; height:6px; background:var(--teal); border-radius:50%;}

  .hero h1{
    font-size:clamp(32px, 5.2vw, 52px);
    line-height:1.08; color:var(--silk); margin-bottom:14px;
  }
  .hero .role{
    font-family:var(--mono); color:var(--teal); font-size:clamp(14px,2vw,18px);
    letter-spacing:.02em; margin-bottom:22px;
  }
  .hero p.lead{max-width:52ch; color:var(--silk-dim); font-size:16px; margin-bottom:32px;}

  .btn-row{display:flex; flex-wrap:wrap; gap:14px;}
  .btn{
    font-family:var(--mono); font-size:13px; letter-spacing:.03em;
    padding:13px 22px; border-radius:var(--radius); cursor:pointer;
    display:inline-flex; align-items:center; gap:8px; border:1px solid transparent;
  }
  .btn-primary{background:var(--copper); color:#0A0E17; font-weight:600;}
  .btn-primary:hover{background:var(--copper-bright);}
  .btn-ghost{border-color:var(--line); color:var(--silk);}
  .btn-ghost:hover{border-color:var(--copper); color:var(--copper-bright);}

  /* IC-package style avatar frame */
  .chip{
    position:relative; width:100%; max-width:300px; aspect-ratio:1/1; margin:0 auto;
    background:var(--panel); border:1px solid var(--line); border-radius:8px;
  }
  .chip-inner{
    position:absolute; inset:22px; border:1px solid var(--line); border-radius:4px;
    display:flex; align-items:center; justify-content:center; flex-direction:column;
    background:
      linear-gradient(var(--panel-2), var(--panel-2)) padding-box;
    overflow:hidden;
  }
  .chip-inner .initials{
    font-family:var(--mono); font-size:52px; font-weight:700; color:var(--silk-dim);
    letter-spacing:0.02em;
  }
  .chip-inner .swap-note{
    font-family:var(--mono); font-size:10px; color:var(--silk-dim); opacity:.6;
    margin-top:6px; text-align:center; padding:0 14px;
  }
  .chip-pin{position:absolute; background:var(--line);}
  .chip-pin.top{top:0; width:2px; height:22px;}
  .chip-pin.bottom{bottom:0; width:2px; height:22px;}
  .chip-pin.left{left:0; height:2px; width:22px;}
  .chip-pin.right{right:0; height:2px; width:22px;}
  .chip .dot-marker{
    position:absolute; top:14px; left:14px; width:7px; height:7px; border-radius:50%;
    background:var(--copper);
  }

  /* =========================================================
     ABOUT
     ========================================================= */
  .about-grid{display:grid; grid-template-columns:1fr; gap:40px;}
  @media (min-width:800px){ .about-grid{grid-template-columns:1fr 1fr;} }
  .about-grid p{color:var(--silk-dim); margin-bottom:16px; max-width:58ch;}
  .field-list{border:1px solid var(--line); border-radius:var(--radius); overflow:hidden;}
  .field-row{
    display:grid; grid-template-columns:120px 1fr; gap:12px;
    padding:14px 16px; border-bottom:1px solid var(--line); font-size:14px;
  }
  .field-row:last-child{border-bottom:none;}
  .field-row .k{font-family:var(--mono); font-size:11px; color:var(--copper); text-transform:uppercase; letter-spacing:.06em; padding-top:2px;}
  .field-row .v{color:var(--silk);}
  .field-row .v .sub{color:var(--silk-dim); font-size:13px;}

  .chip-tags{display:flex; flex-wrap:wrap; gap:8px; margin-top:18px;}
  .tag{
    font-family:var(--mono); font-size:11.5px; letter-spacing:.03em;
    border:1px solid var(--line); padding:6px 10px; border-radius:var(--radius);
    color:var(--silk-dim);
  }

  /* =========================================================
     PROJECTS
     ========================================================= */
  .project-list{display:flex; flex-direction:column; gap:2px;}
  .project{
    border:1px solid var(--line); background:var(--panel);
    border-radius:var(--radius); margin-bottom:20px; overflow:hidden;
  }
  .project-head{
    display:flex; align-items:center; justify-content:space-between; gap:16px;
    padding:18px 22px; cursor:pointer; user-select:none;
  }
  .project-head:hover{background:var(--panel-2);}
  .project-head-left{display:flex; align-items:center; gap:16px; min-width:0;}
  .ref{
    font-family:var(--mono); font-size:12px; color:var(--copper);
    border:1px solid var(--line); border-radius:50%; width:34px; height:34px;
    flex:none; display:flex; align-items:center; justify-content:center;
  }
  .project-head h3{font-size:16px; color:var(--silk); font-weight:600; font-family:var(--sans);}
  .project-head .ptag{font-family:var(--mono); font-size:11px; color:var(--silk-dim); margin-top:2px;}
  .chev{font-family:var(--mono); color:var(--silk-dim); transition:transform .2s ease; flex:none;}
  .project.open .chev{transform:rotate(45deg); color:var(--copper);}

  .project-body{
    max-height:0; overflow:hidden; transition:max-height .3s ease;
    border-top:1px solid transparent;
  }
  .project.open .project-body{border-top:1px solid var(--line);}
  .project-body-inner{padding:22px; display:grid; grid-template-columns:1fr; gap:22px;}
  @media (min-width:760px){ .project-body-inner{grid-template-columns: 1fr 1.3fr;} }

  .schematic{
    background:var(--panel-2); border:1px solid var(--line); border-radius:var(--radius);
    aspect-ratio:4/3; display:flex; align-items:center; justify-content:center;
    position:relative;
  }
  .schematic svg{width:70%; height:70%; opacity:.85;}
  .schematic .cap{
    position:absolute; bottom:8px; left:10px; font-family:var(--mono); font-size:10px;
    color:var(--silk-dim); letter-spacing:.05em; text-transform:uppercase;
  }

  .project-desc p{color:var(--silk-dim); font-size:14.5px; margin-bottom:14px;}
  .kv-table{width:100%; border-collapse:collapse; margin-bottom:16px;}
  .kv-table tr{border-bottom:1px solid var(--line);}
  .kv-table tr:last-child{border-bottom:none;}
  .kv-table td{padding:8px 0; font-size:13.5px; vertical-align:top;}
  .kv-table td:first-child{
    font-family:var(--mono); color:var(--silk-dim); width:120px; text-transform:uppercase;
    font-size:11px; letter-spacing:.05em; padding-top:10px;
  }
  .project-links{display:flex; flex-wrap:wrap; gap:10px;}
  .link-btn{
    font-family:var(--mono); font-size:12px; border:1px solid var(--line);
    padding:8px 12px; border-radius:var(--radius); color:var(--silk-dim);
    display:inline-flex; align-items:center; gap:6px;
  }
  .link-btn:hover{border-color:var(--teal); color:var(--teal);}

  /* =========================================================
     SKILLS
     ========================================================= */
  .skills-groups{display:grid; grid-template-columns:1fr; gap:28px;}
  @media (min-width:760px){ .skills-groups{grid-template-columns:repeat(3,1fr);} }
  .skill-group{border:1px solid var(--line); border-radius:var(--radius); padding:20px;}
  .skill-group .g-title{font-family:var(--mono); font-size:11px; color:var(--copper); text-transform:uppercase; letter-spacing:.08em; margin-bottom:14px;}
  .skill-pin-row{display:flex; align-items:center; gap:10px; padding:8px 0; border-bottom:1px dashed var(--line); font-size:14px;}
  .skill-pin-row:last-child{border-bottom:none;}
  .skill-pin-row .pn{
    font-family:var(--mono); font-size:10px; color:var(--silk-dim); width:22px; flex:none;
    border:1px solid var(--line); border-radius:2px; text-align:center; padding:2px 0;
  }

  /* =========================================================
     RESUME
     ========================================================= */
  .resume-box{
    border:1px solid var(--line); border-radius:var(--radius); padding:32px;
    display:flex; flex-wrap:wrap; align-items:center; justify-content:space-between; gap:22px;
    background:var(--panel);
  }
  .resume-box .rt h3{font-size:18px; color:var(--silk); margin-bottom:6px;}
  .resume-box .rt p{color:var(--silk-dim); font-size:14px;}

  /* =========================================================
     CONTACT
     ========================================================= */
  .contact-grid{display:grid; grid-template-columns:1fr; gap:40px;}
  @media (min-width:800px){ .contact-grid{grid-template-columns:.9fr 1.1fr;} }
  .contact-links{display:flex; flex-direction:column; gap:2px;}
  .contact-link{
    display:flex; align-items:center; justify-content:space-between;
    padding:16px 4px; border-bottom:1px solid var(--line);
  }
  .contact-link:first-child{border-top:1px solid var(--line);}
  .contact-link .l{font-family:var(--mono); font-size:11px; color:var(--silk-dim); text-transform:uppercase; letter-spacing:.06em;}
  .contact-link .r{color:var(--silk); font-size:14.5px;}
  .contact-link .r:hover{color:var(--copper-bright);}

  form{display:flex; flex-direction:column; gap:14px;}
  .field{display:flex; flex-direction:column; gap:6px;}
  .field label{font-family:var(--mono); font-size:11px; color:var(--silk-dim); text-transform:uppercase; letter-spacing:.05em;}
  .field input, .field textarea{
    background:var(--panel-2); border:1px solid var(--line); color:var(--silk);
    padding:12px 14px; border-radius:var(--radius); font-family:var(--sans); font-size:14px;
    resize:vertical;
  }
  .field input:focus, .field textarea:focus{border-color:var(--teal); outline:none;}
  form .btn{align-self:flex-start; margin-top:4px; border:none;}
  .form-note{font-family:var(--mono); font-size:11px; color:var(--silk-dim); margin-top:4px;}

  footer{
    padding:36px 0 48px; text-align:center; font-family:var(--mono); font-size:12px;
    color:var(--silk-dim);
  }
  footer .dot{color:var(--copper);}

  @media (prefers-reduced-motion: reduce){
    html{scroll-behavior:auto;}
    *{transition:none !important;}
  }
</style>
</head>
<body data-theme="dark">

<svg id="trace-svg"><line class="trace-path" x1="1" y1="0" x2="1" y2="100%"/><line id="trace-fill" class="trace-path-fill" x1="1" y1="0" x2="1" y2="100%"/></svg>

<header>
  <div class="navbar">
    <div class="logo"><span class="dot"></span>DEEPAK&nbsp;KUMAR</div>
    <nav><ul>
      <li><a href="#home">Home</a></li>
      <li><a href="#about">About</a></li>
      <li><a href="#projects">Projects</a></li>
      <li><a href="#skills">Skills</a></li>
      <li><a href="#resume">Resume</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul></nav>
    <div class="nav-right">
      <button class="theme-btn" id="theme-toggle" aria-label="Toggle light and dark theme">Light</button>
      <button class="menu-btn" id="menu-toggle" aria-label="Toggle menu">☰</button>
    </div>
  </div>
  <div id="mobile-nav">
    <a href="#home">Home</a>
    <a href="#about">About</a>
    <a href="#projects">Projects</a>
    <a href="#skills">Skills</a>
    <a href="#resume">Resume</a>
    <a href="#contact">Contact</a>
  </div>
</header>

<main class="wrap">

  <!-- HOME -->
  <section id="home" class="hero" data-pad="U1" data-pad-label="U1 — HOME">
    <div class="section-inner" style="border-bottom:none;">
      <div class="hero-grid">
        <div>
          <div class="designator"><span class="pin"></span>REF DES: U1 &nbsp;·&nbsp; PACKAGE: ENGINEER</div>
          <h1>Deepak Kumar</h1>
          <div class="role">Electronics &amp; Communication Engineer — Embedded Systems · IoT · Robotics</div>
          <p class="lead">I design and build hardware-software systems end to end — from schematic and PCB layout to firmware and field testing. Recent work spans servo-driven robotics, IoT sensor nodes, optical communication links, and biomedical signal acquisition.</p>
          <div class="btn-row">
            <a href="#projects" class="btn btn-primary">View Projects →</a>
            <a href="resume.pdf" class="btn btn-ghost" download>Download Resume ⭳</a>
          </div>
        </div>
        <div class="chip">
          <div class="chip-pin top" style="left:30%"></div>
          <div class="chip-pin top" style="left:70%"></div>
          <div class="chip-pin bottom" style="left:30%"></div>
          <div class="chip-pin bottom" style="left:70%"></div>
          <div class="chip-pin left" style="top:30%"></div>
          <div class="chip-pin left" style="top:70%"></div>
          <div class="chip-pin right" style="top:30%"></div>
          <div class="chip-pin right" style="top:70%"></div>
          <div class="dot-marker"></div>
          <div class="chip-inner">
            <div class="initials">DK</div>
            <div class="swap-note">Replace this frame with a profile photo — see comment in HTML source</div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- ABOUT -->
  <section id="about" data-pad="R1" data-pad-label="R1 — ABOUT">
    <div class="section-inner">
      <div class="section-head">
        <div class="eyebrow">01 · Profile</div>
        <h2>About Me</h2>
      </div>
      <div class="about-grid">
        <div>
          <p>I'm an Electronics &amp; Communication Engineering student focused on embedded systems and applied robotics. I like taking a project from a rough schematic sketch to a working, soldered prototype — writing the firmware, laying out the PCB, and debugging it on the bench.</p>
          <p>My interests sit at the intersection of microcontrollers, IoT connectivity, and signal acquisition — with a growing focus on optical communication and biomedical sensing (EMG/ECG). I'm comfortable across the stack: KiCad for schematic capture and PCB layout, LTspice for simulation, and Embedded C/C++ and Python for firmware and tooling.</p>
          <div class="chip-tags">
            <span class="tag">ESP32 / ESP8266</span>
            <span class="tag">Embedded C/C++</span>
            <span class="tag">KiCad</span>
            <span class="tag">IoT</span>
            <span class="tag">Robotics</span>
            <span class="tag">PCB Design</span>
          </div>
        </div>
        <div class="field-list">
          <div class="field-row">
            <div class="k">Education</div>
            <div class="v">B.Tech, Electronics &amp; Communication Engineering
              <div class="sub">Your College Name · Expected Year — update in source</div>
            </div>
          </div>
          <div class="field-row">
            <div class="k">Focus</div>
            <div class="v">Embedded systems, IoT, robotics, PCB design, optical &amp; biomedical signal systems</div>
          </div>
          <div class="field-row">
            <div class="k">Tools</div>
            <div class="v">KiCad · LTspice · Arduino IDE · VS Code · Git</div>
          </div>
          <div class="field-row">
            <div class="k">Currently</div>
            <div class="v">Open to internships / collaborations in embedded &amp; hardware engineering</div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section id="projects" data-pad="U2" data-pad-label="U2 — PROJECTS">
    <div class="section-inner">
      <div class="section-head">
        <div class="eyebrow">02 · Selected Work</div>
        <h2>Projects</h2>
      </div>

      <div class="project-list" id="project-list">

        <!-- Project 1 -->
        <article class="project">
          <div class="project-head" data-toggle>
            <div class="project-head-left">
              <div class="ref">01</div>
              <div>
                <h3>ESP32 Robot — 8-Servo Locomotion</h3>
                <div class="ptag">Robotics · Embedded C++ · Wireless control</div>
              </div>
            </div>
            <div class="chev">+</div>
          </div>
          <div class="project-body">
            <div class="project-body-inner">
              <div class="schematic">
                <svg viewBox="0 0 100 80" fill="none" stroke="currentColor" stroke-width="1.5" style="color:var(--copper)">
                  <rect x="35" y="30" width="30" height="20" rx="2"/>
                  <line x1="35" y1="35" x2="15" y2="20"/><circle cx="15" cy="20" r="3"/>
                  <line x1="35" y1="45" x2="15" y2="60"/><circle cx="15" cy="60" r="3"/>
                  <line x1="65" y1="35" x2="85" y2="20"/><circle cx="85" cy="20" r="3"/>
                  <line x1="65" y1="45" x2="85" y2="60"/><circle cx="85" cy="60" r="3"/>
                  <text x="43" y="43" font-size="6" stroke="none" fill="currentColor">ESP32</text>
                </svg>
                <div class="cap">Fig 1. Servo layout — replace with real photo</div>
              </div>
              <div class="project-desc">
                <p>A quadruped-style robot driven by 8 servo motors, controlled by an ESP32 over Wi-Fi. Gait sequences are generated in firmware, with a lightweight web UI served directly from the ESP32 for real-time control.</p>
                <table class="kv-table">
                  <tr><td>Components</td><td>ESP32 dev board, 8× SG90/MG90S servos, PCA9685 servo driver, LiPo battery + regulator, 3D-printed chassis</td></tr>
                  <tr><td>Principle</td><td>PWM gait sequencing over I2C via PCA9685, coordinated in firmware; control commands sent over Wi-Fi from a browser-based interface</td></tr>
                </table>
                <div class="project-links">
                  <a href="#" class="link-btn">↗ GitHub / Code</a>
                  <a href="#" class="link-btn">▶ Demo Video</a>
                </div>
              </div>
            </div>
          </div>
        </article>

        <!-- Project 2 -->
        <article class="project">
          <div class="project-head" data-toggle>
            <div class="project-head-left">
              <div class="ref">02</div>
              <div>
                <h3>Smart LED Keychain</h3>
                <div class="ptag">ESP8266 · MAX7219 · Wearable IoT</div>
              </div>
            </div>
            <div class="chev">+</div>
          </div>
          <div class="project-body">
            <div class="project-body-inner">
              <div class="schematic">
                <svg viewBox="0 0 100 80" fill="none" stroke="currentColor" stroke-width="1.5" style="color:var(--teal)">
                  <rect x="20" y="20" width="60" height="40" rx="3"/>
                  <circle cx="30" cy="30" r="2"/><circle cx="40" cy="30" r="2"/><circle cx="50" cy="30" r="2"/><circle cx="60" cy="30" r="2"/><circle cx="70" cy="30" r="2"/>
                  <circle cx="30" cy="40" r="2"/><circle cx="40" cy="40" r="2"/><circle cx="50" cy="40" r="2"/><circle cx="60" cy="40" r="2"/><circle cx="70" cy="40" r="2"/>
                  <circle cx="30" cy="50" r="2"/><circle cx="40" cy="50" r="2"/><circle cx="50" cy="50" r="2"/><circle cx="60" cy="50" r="2"/><circle cx="70" cy="50" r="2"/>
                </svg>
                <div class="cap">Fig 1. LED matrix — replace with real photo</div>
              </div>
              <div class="project-desc">
                <p>A pocket-sized scrolling LED display built around an ESP8266 and a MAX7219 dot-matrix driver. Messages are updated wirelessly over Wi-Fi, and the whole build fits on a keychain-sized PCB.</p>
                <table class="kv-table">
                  <tr><td>Components</td><td>ESP8266 (Wemos D1 Mini), MAX7219 8×8 LED matrix module, Li-Po cell + charger IC, custom PCB</td></tr>
                  <tr><td>Principle</td><td>SPI communication between ESP8266 and MAX7219; message text and scroll speed configurable over a small Wi-Fi web interface</td></tr>
                </table>
                <div class="project-links">
                  <a href="#" class="link-btn">↗ GitHub / Code</a>
                  <a href="#" class="link-btn">▶ Demo Video</a>
                </div>
              </div>
            </div>
          </div>
        </article>

        <!-- Project 3 -->
        <article class="project">
          <div class="project-head" data-toggle>
            <div class="project-head-left">
              <div class="ref">03</div>
              <div>
                <h3>Railway Track Crack Detection System</h3>
                <div class="ptag">IoT · Sensors · Safety systems</div>
              </div>
            </div>
            <div class="chev">+</div>
          </div>
          <div class="project-body">
            <div class="project-body-inner">
              <div class="schematic">
                <svg viewBox="0 0 100 80" fill="none" stroke="currentColor" stroke-width="1.5" style="color:var(--amber)">
                  <line x1="10" y1="30" x2="90" y2="30"/><line x1="10" y1="50" x2="90" y2="50"/>
                  <line x1="20" y1="26" x2="20" y2="54"/><line x1="35" y1="26" x2="35" y2="54"/>
                  <line x1="50" y1="26" x2="50" y2="54"/><line x1="65" y1="26" x2="65" y2="54"/><line x1="80" y1="26" x2="80" y2="54"/>
                  <path d="M45 30 L48 40 L44 50" stroke="red"/>
                </svg>
                <div class="cap">Fig 1. Track + sensor node — replace with real photo</div>
              </div>
              <div class="project-desc">
                <p>An embedded sensor node that rides along a rail section and flags surface irregularities consistent with cracks, reporting GPS-tagged alerts back to a base station.</p>
                <table class="kv-table">
                  <tr><td>Components</td><td>Microcontroller (Arduino/ESP32), IR or ultrasonic crack sensors, GPS module, GSM module, buzzer/LED alert</td></tr>
                  <tr><td>Principle</td><td>Sensor array scans the rail surface for discontinuities; on detection, GPS coordinates are packaged and sent as an SMS/IoT alert via GSM</td></tr>
                </table>
                <div class="project-links">
                  <a href="#" class="link-btn">↗ GitHub / Code</a>
                  <a href="#" class="link-btn">▶ Demo Video</a>
                </div>
              </div>
            </div>
          </div>
        </article>

        <!-- Project 4 -->
        <article class="project">
          <div class="project-head" data-toggle>
            <div class="project-head-left">
              <div class="ref">04</div>
              <div>
                <h3>Optical Communication Link</h3>
                <div class="ptag">Photonics · Analog design</div>
              </div>
            </div>
            <div class="chev">+</div>
          </div>
          <div class="project-body">
            <div class="project-body-inner">
              <div class="schematic">
                <svg viewBox="0 0 100 80" fill="none" stroke="currentColor" stroke-width="1.5" style="color:var(--copper)">
                  <rect x="10" y="35" width="14" height="10"/><line x1="24" y1="40" x2="76" y2="40" stroke-dasharray="2 2"/><rect x="76" y="35" width="14" height="10"/>
                  <text x="8" y="55" font-size="6" stroke="none" fill="currentColor">TX</text>
                  <text x="80" y="55" font-size="6" stroke="none" fill="currentColor">RX</text>
                </svg>
                <div class="cap">Fig 1. Free-space link — replace with real photo</div>
              </div>
              <div class="project-desc">
                <p>A free-space optical communication prototype transmitting audio/data over a modulated LED or laser beam, recovered at the receiver with a photodiode front end.</p>
                <table class="kv-table">
                  <tr><td>Components</td><td>Laser diode / high-intensity LED, photodiode, transimpedance amplifier, comparator/filter stage</td></tr>
                  <tr><td>Principle</td><td>Intensity modulation at the transmitter, direct detection and analog signal recovery at the receiver</td></tr>
                </table>
                <div class="project-links">
                  <a href="#" class="link-btn">↗ GitHub / Code</a>
                  <a href="#" class="link-btn">▶ Demo Video</a>
                </div>
              </div>
            </div>
          </div>
        </article>

        <!-- Project 5 -->
        <article class="project">
          <div class="project-head" data-toggle>
            <div class="project-head-left">
              <div class="ref">05</div>
              <div>
                <h3>EMG / ECG Signal Acquisition</h3>
                <div class="ptag">Biomedical · Analog front-end</div>
              </div>
            </div>
            <div class="chev">+</div>
          </div>
          <div class="project-body">
            <div class="project-body-inner">
              <div class="schematic">
                <svg viewBox="0 0 100 80" fill="none" stroke="currentColor" stroke-width="1.5" style="color:var(--teal)">
                  <polyline points="10,45 30,45 35,25 40,60 45,45 90,45" />
                </svg>
                <div class="cap">Fig 1. Waveform capture — replace with real photo</div>
              </div>
              <div class="project-desc">
                <p>A biopotential acquisition front end for capturing EMG/ECG signals — instrumentation amplifier, filtering, and digitization for real-time waveform display.</p>
                <table class="kv-table">
                  <tr><td>Components</td><td>Instrumentation amplifier (e.g. AD8232 / INA-series), active filter stage, ADC + microcontroller, surface electrodes</td></tr>
                  <tr><td>Principle</td><td>Differential biopotential sensing, band-pass filtering to isolate the signal band, then digitization and plotting</td></tr>
                </table>
                <div class="project-links">
                  <a href="#" class="link-btn">↗ GitHub / Code</a>
                  <a href="#" class="link-btn">▶ Demo Video</a>
                </div>
              </div>
            </div>
          </div>
        </article>

        <!-- Project 6 -->
        <article class="project">
          <div class="project-head" data-toggle>
            <div class="project-head-left">
              <div class="ref">06</div>
              <div>
                <h3>KiCad PCB Design Collection</h3>
                <div class="ptag">PCB layout · Schematic capture</div>
              </div>
            </div>
            <div class="chev">+</div>
          </div>
          <div class="project-body">
            <div class="project-body-inner">
              <div class="schematic">
                <svg viewBox="0 0 100 80" fill="none" stroke="currentColor" stroke-width="1.2" style="color:var(--copper)">
                  <rect x="15" y="15" width="70" height="50" rx="2"/>
                  <path d="M20 25 H50 V35 H70 V55" />
                  <path d="M20 55 H35 V45 H60" />
                  <circle cx="20" cy="25" r="1.5" fill="currentColor" stroke="none"/>
                  <circle cx="70" cy="55" r="1.5" fill="currentColor" stroke="none"/>
                </svg>
                <div class="cap">Fig 1. Trace routing — replace with real photo</div>
              </div>
              <div class="project-desc">
                <p>A set of two-layer PCB designs built in KiCad — from schematic capture through footprint placement, routing, and Gerber export for fabrication.</p>
                <table class="kv-table">
                  <tr><td>Tools</td><td>KiCad (Eeschema + Pcbnew), LTspice for pre-layout simulation, JLCPCB/PCBWay for fabrication</td></tr>
                  <tr><td>Scope</td><td>Power regulation boards, sensor breakout boards, and the custom PCBs used in the projects above</td></tr>
                </table>
                <div class="project-links">
                  <a href="#" class="link-btn">↗ GitHub / Code</a>
                </div>
              </div>
            </div>
          </div>
        </article>

      </div>
    </div>
  </section>

  <!-- SKILLS -->
  <section id="skills" data-pad="R2" data-pad-label="R2 — SKILLS">
    <div class="section-inner">
      <div class="section-head">
        <div class="eyebrow">03 · Capabilities</div>
        <h2>Skills</h2>
      </div>
      <div class="skills-groups">
        <div class="skill-group">
          <div class="g-title">Hardware &amp; Boards</div>
          <div class="skill-pin-row"><span class="pn">01</span>ESP32 / ESP8266</div>
          <div class="skill-pin-row"><span class="pn">02</span>Arduino</div>
          <div class="skill-pin-row"><span class="pn">03</span>GPS / GSM Modules</div>
          <div class="skill-pin-row"><span class="pn">04</span>Sensors &amp; Actuators</div>
        </div>
        <div class="skill-group">
          <div class="g-title">Software &amp; Firmware</div>
          <div class="skill-pin-row"><span class="pn">05</span>Embedded C / C++</div>
          <div class="skill-pin-row"><span class="pn">06</span>Python</div>
          <div class="skill-pin-row"><span class="pn">07</span>Verilog / VLSI Basics</div>
          <div class="skill-pin-row"><span class="pn">08</span>Git</div>
        </div>
        <div class="skill-group">
          <div class="g-title">Design &amp; Tools</div>
          <div class="skill-pin-row"><span class="pn">09</span>KiCad (PCB Design)</div>
          <div class="skill-pin-row"><span class="pn">10</span>LTspice</div>
          <div class="skill-pin-row"><span class="pn">11</span>IoT Architecture</div>
          <div class="skill-pin-row"><span class="pn">12</span>Robotics</div>
        </div>
      </div>
    </div>
  </section>

  <!-- RESUME -->
  <section id="resume" data-pad="J1" data-pad-label="J1 — RESUME">
    <div class="section-inner">
      <div class="section-head">
        <div class="eyebrow">04 · Document</div>
        <h2>Resume</h2>
      </div>
      <div class="resume-box">
        <div class="rt">
          <h3>Full resume — PDF</h3>
          <p>Add your resume file as <code>resume.pdf</code> next to this page, or link an online version.</p>
        </div>
        <div class="btn-row">
          <a href="resume.pdf" class="btn btn-ghost" download>Download PDF ⭳</a>
          <a href="resume.pdf" target="_blank" class="btn btn-primary">View Online →</a>
        </div>
      </div>
    </div>
  </section>

  <!-- CONTACT -->
  <section id="contact" data-pad="J2" data-pad-label="J2 — CONTACT">
    <div class="section-inner">
      <div class="section-head">
        <div class="eyebrow">05 · Reach Out</div>
        <h2>Contact</h2>
      </div>
      <div class="contact-grid">
        <div class="contact-links">
          <div class="contact-link"><span class="l">Email</span><a class="r" href="mailto:deepak.kumar@example.com">deepak.kumar@example.com</a></div>
          <div class="contact-link"><span class="l">LinkedIn</span><a class="r" href="#" target="_blank">linkedin.com/in/deepakkumar</a></div>
          <div class="contact-link"><span class="l">GitHub</span><a class="r" href="#" target="_blank">github.com/deepakkumar</a></div>
        </div>
        <form onsubmit="event.preventDefault(); alert('Wire this form to a backend or a service like Formspree — see comment in HTML source.');">
          <div class="field"><label for="name">Name</label><input id="name" type="text" required></div>
          <div class="field"><label for="email">Email</label><input id="email" type="email" required></div>
          <div class="field"><label for="message">Message</label><textarea id="message" rows="4" required></textarea></div>
          <button type="submit" class="btn btn-primary">Send Message →</button>
          <div class="form-note">This form has no backend yet — connect it to Formspree, EmailJS, or your own endpoint.</div>
        </form>
      </div>
    </div>
  </section>

</main>

<footer>
  DEEPAK KUMAR <span class="dot">◆</span> Designed as a PCB datasheet <span class="dot">◆</span> Built with HTML / CSS / JS <span class="dot">◆</span> © <span id="year"></span>
</footer>

<script>
  // Theme toggle (in-memory only — no localStorage)
  const root = document.body;
  const themeBtn = document.getElementById('theme-toggle');
  function setTheme(t){
    root.setAttribute('data-theme', t);
    themeBtn.textContent = t === 'dark' ? 'Light' : 'Dark';
  }
  themeBtn.addEventListener('click', () => {
    const next = root.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
    setTheme(next);
  });
  setTheme('dark');

  // Mobile nav
  const menuBtn = document.getElementById('menu-toggle');
  const mobileNav = document.getElementById('mobile-nav');
  menuBtn.addEventListener('click', () => mobileNav.classList.toggle('open'));
  mobileNav.querySelectorAll('a').forEach(a => a.addEventListener('click', () => mobileNav.classList.remove('open')));

  // Accordion projects
  document.querySelectorAll('[data-toggle]').forEach(head => {
    head.addEventListener('click', () => {
      const project = head.closest('.project');
      const body = project.querySelector('.project-body');
      const isOpen = project.classList.contains('open');
      document.querySelectorAll('.project.open').forEach(p => {
        p.classList.remove('open');
        p.querySelector('.project-body').style.maxHeight = null;
      });
      if(!isOpen){
        project.classList.add('open');
        body.style.maxHeight = body.scrollHeight + 'px';
      }
    });
  });

  // Signature trace: build pads from sections, animate fill on scroll
  const sections = document.querySelectorAll('section[data-pad]');
  const traceSvg = document.getElementById('trace-svg');
  const traceFill = document.getElementById('trace-fill');
  const padsLayer = document.createElement('div');
  padsLayer.style.position = 'absolute';
  padsLayer.style.top = '0'; padsLayer.style.left = '0'; padsLayer.style.width = '100%'; padsLayer.style.zIndex = '2';
  padsLayer.style.pointerEvents = 'none';
  document.querySelector('main').style.position = 'relative';
  document.querySelector('main').appendChild(padsLayer);

  function layoutPads(){
    padsLayer.innerHTML = '';
    const mainTop = document.querySelector('main').getBoundingClientRect().top + window.scrollY;
    sections.forEach(sec => {
      const rect = sec.getBoundingClientRect();
      const top = rect.top + window.scrollY - mainTop + 4;
      const pad = document.createElement('div');
      pad.className = 'pad';
      pad.style.top = top + 'px';
      pad.dataset.for = sec.id;
      padsLayer.appendChild(pad);
      const label = document.createElement('div');
      label.className = 'pad-label';
      label.style.top = (top - 3) + 'px';
      label.textContent = sec.dataset.padLabel;
      padsLayer.appendChild(label);
    });
  }
  layoutPads();
  window.addEventListener('resize', layoutPads);

  function onScroll(){
    const doc = document.documentElement;
    const scrollTop = window.scrollY;
    const scrollHeight = doc.scrollHeight - window.innerHeight;
    const pct = Math.min(1, Math.max(0, scrollTop / scrollHeight));
    const svgHeight = traceSvg.getBoundingClientRect().height || document.body.scrollHeight;
    traceFill.setAttribute('y2', (pct * 100) + '%');

    let current = null;
    sections.forEach(sec => {
      const r = sec.getBoundingClientRect();
      if(r.top < window.innerHeight * 0.5) current = sec.id;
    });
    document.querySelectorAll('.pad').forEach(p => p.classList.toggle('on', p.dataset.for === current));
  }
  document.addEventListener('scroll', onScroll);
  window.addEventListener('load', onScroll);

  document.getElementById('year').textContent = new Date().getFullYear();
</script>

<!--
  ============================================================
  SETUP NOTES FOR DEEPAK
  ============================================================
  1. PROFILE PHOTO: replace the .chip-inner block in the Home
     section with: <img src="profile.jpg" alt="Deepak Kumar">
     and add your photo file next to this HTML file.

  2. PROJECT PHOTOS: each project has a .schematic block with an
     inline SVG placeholder. Swap the <svg>...</svg> for
     <img src="projects/your-photo.jpg" alt="..."> once you have
     real photos, circuit diagrams, or PCB renders.

  3. LINKS: update the "#" hrefs for GitHub, LinkedIn, and each
     project's GitHub/demo links.

  4. RESUME: add a file named resume.pdf in the same folder as
     this index.html.

  5. CONTACT FORM: currently shows an alert on submit. Connect it
     to a service like Formspree (https://formspree.io) or EmailJS
     for a working backend with no server needed.

  6. DEPLOY: push this file (and any images/resume.pdf) to a GitHub
     repo named yourusername.github.io, or a repo with GitHub Pages
     enabled on the main branch — no build step required.
  ============================================================
-->
</body>
</html>
