<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Suman Seth — Software Engineer & Data Scientist</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        mono: ['JetBrains Mono', 'monospace'],
                    },
                }
            }
        }
    </script>
    <style>
        *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
        html { scroll-behavior: smooth; }
        body {
            font-family: 'Inter', sans-serif;
            background: #030712;
            color: #f1f5f9;
            overflow-x: hidden;
            cursor: none;
        }
        @media (max-width: 768px) { body { cursor: auto; } }

        ::selection {
            background: rgba(6, 182, 212, 0.25);
            color: #ecfeff;
        }
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.08); border-radius: 3px; }
        ::-webkit-scrollbar-thumb:hover { background: rgba(255,255,255,0.15); }

        /* Custom Cursor */
        .cursor-dot {
            width: 8px; height: 8px;
            background: #22d3ee;
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 9999;
            transition: transform 0.1s ease;
            mix-blend-mode: difference;
        }
        .cursor-ring {
            width: 40px; height: 40px;
            border: 1px solid rgba(34, 211, 238, 0.4);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 9998;
            transition: all 0.15s ease-out;
        }
        .cursor-ring.hover {
            width: 60px; height: 60px;
            border-color: rgba(34, 211, 238, 0.7);
            background: rgba(34, 211, 238, 0.05);
        }
        @media (max-width: 768px) {
            .cursor-dot, .cursor-ring { display: none; }
        }

        /* Scroll Progress */
        .scroll-progress {
            position: fixed;
            top: 0; left: 0;
            height: 2px;
            background: linear-gradient(to right, #06b6d4, #8b5cf6, #06b6d4);
            background-size: 200% 100%;
            animation: gradientShift 3s ease infinite;
            z-index: 100;
            transition: width 0.1s linear;
        }
        @keyframes gradientShift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        /* Three Canvas */
        #three-canvas {
            position: fixed;
            top: 0; left: 0;
            width: 100vw; height: 100vh;
            z-index: -10;
            opacity: 0.5;
        }

        /* Glass */
        .glass {
            background: rgba(255, 255, 255, 0.02);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.06);
        }
        .glass-strong {
            background: rgba(255, 255, 255, 0.04);
            backdrop-filter: blur(24px);
            -webkit-backdrop-filter: blur(24px);
            border: 1px solid rgba(255, 255, 255, 0.08);
        }
        .glass-nav {
            background: rgba(3, 7, 18, 0.75);
            backdrop-filter: blur(24px) saturate(180%);
            -webkit-backdrop-filter: blur(24px) saturate(180%);
            border-bottom: 1px solid rgba(255, 255, 255, 0.04);
        }

        /* Gradients */
        .text-gradient {
            background: linear-gradient(135deg, #67e8f9 0%, #06b6d4 40%, #8b5cf6 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        .text-gradient-subtle {
            background: linear-gradient(to right, #e2e8f0, #94a3b8);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }
        .border-gradient {
            position: relative;
        }
        .border-gradient::before {
            content: '';
            position: absolute;
            inset: 0;
            border-radius: inherit;
            padding: 1px;
            background: linear-gradient(135deg, rgba(6,182,212,0.3), transparent, rgba(139,92,246,0.3));
            -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
            pointer-events: none;
        }

        /* Buttons */
        .btn-primary {
            background: #ffffff;
            color: #030712;
            font-weight: 500;
            font-size: 13px;
            padding: 14px 28px;
            border-radius: 10px;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            border: none;
            cursor: none;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            text-decoration: none;
            letter-spacing: -0.01em;
        }
        .btn-primary:hover {
            background: #ecfeff;
            transform: translateY(-2px);
            box-shadow: 0 8px 30px rgba(255,255,255,0.1);
        }
        .btn-cta {
            background: linear-gradient(135deg, #06b6d4, #0891b2);
            color: #000000;
            font-weight: 500;
            font-size: 13px;
            padding: 14px 28px;
            border-radius: 10px;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            border: none;
            cursor: none;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            text-decoration: none;
            letter-spacing: -0.01em;
        }
        .btn-cta:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 30px rgba(6,182,212,0.3);
        }
        .btn-ghost {
            background: transparent;
            color: #cbd5e1;
            font-weight: 400;
            font-size: 13px;
            padding: 14px 28px;
            border-radius: 10px;
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            border: 1px solid rgba(255,255,255,0.08);
            cursor: none;
            display: inline-flex;
            align-items: center;
            gap: 8px;
            text-decoration: none;
        }
        .btn-ghost:hover {
            background: rgba(255,255,255,0.05);
            border-color: rgba(255,255,255,0.15);
            color: #ffffff;
            transform: translateY(-2px);
        }
        .btn-sm { padding: 10px 20px; font-size: 12px; border-radius: 8px; }
        .btn-xs { padding: 6px 14px; font-size: 11px; border-radius: 6px; }

        @media (max-width: 768px) {
            .btn-primary, .btn-cta, .btn-ghost { cursor: pointer; }
        }

        /* Cards */
        .card {
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            position: relative;
            overflow: hidden;
        }
        .card::after {
            content: '';
            position: absolute;
            inset: 0;
            border-radius: inherit;
            background: radial-gradient(800px circle at var(--mouse-x, 50%) var(--mouse-y, 50%), rgba(6,182,212,0.04), transparent 40%);
            pointer-events: none;
            opacity: 0;
            transition: opacity 0.5s;
        }
        .card:hover::after { opacity: 1; }
        .card:hover { transform: translateY(-6px); border-color: rgba(255,255,255,0.1); }

        /* Tags */
        .tag {
            display: inline-flex;
            align-items: center;
            padding: 5px 12px;
            border-radius: 6px;
            font-size: 11px;
            font-weight: 400;
            font-family: 'JetBrains Mono', monospace;
            border: 1px solid rgba(255,255,255,0.06);
            background: rgba(255,255,255,0.02);
            color: #94a3b8;
            transition: all 0.3s;
        }
        .tag:hover {
            background: rgba(255,255,255,0.06);
            border-color: rgba(255,255,255,0.12);
            color: #e2e8f0;
        }

        /* Section label */
        .section-label {
            font-size: 11px;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.15em;
            color: #22d3ee;
            font-family: 'JetBrains Mono', monospace;
        }
        .section-divider {
            width: 40px;
            height: 1px;
            background: linear-gradient(to right, #22d3ee, transparent);
            margin-top: 16px;
        }

        /* Typing cursor */
        .typing-cursor {
            display: inline-block;
            width: 2px;
            height: 1.1em;
            background: #22d3ee;
            margin-left: 2px;
            vertical-align: text-bottom;
            animation: blink 1s step-end infinite;
        }
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0; }
        }

        /* Fade animations */
        .reveal {
            opacity: 0;
            transform: translateY(40px);
            transition: opacity 0.9s cubic-bezier(0.4, 0, 0.2, 1),
                        transform 0.9s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .reveal.visible {
            opacity: 1;
            transform: translateY(0);
        }
        .reveal-left {
            opacity: 0;
            transform: translateX(-40px);
            transition: opacity 0.9s cubic-bezier(0.4, 0, 0.2, 1),
                        transform 0.9s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .reveal-left.visible {
            opacity: 1;
            transform: translateX(0);
        }
        .reveal-right {
            opacity: 0;
            transform: translateX(40px);
            transition: opacity 0.9s cubic-bezier(0.4, 0, 0.2, 1),
                        transform 0.9s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .reveal-right.visible {
            opacity: 1;
            transform: translateX(0);
        }
        .reveal-scale {
            opacity: 0;
            transform: scale(0.9);
            transition: opacity 0.9s cubic-bezier(0.4, 0, 0.2, 1),
                        transform 0.9s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .reveal-scale.visible {
            opacity: 1;
            transform: scale(1);
        }

        .d1 { transition-delay: 0.08s; }
        .d2 { transition-delay: 0.16s; }
        .d3 { transition-delay: 0.24s; }
        .d4 { transition-delay: 0.32s; }
        .d5 { transition-delay: 0.4s; }
        .d6 { transition-delay: 0.48s; }

        /* Timeline */
        .timeline-track {
            position: absolute;
            left: 20px;
            top: 8px;
            bottom: 8px;
            width: 1px;
            background: linear-gradient(to bottom, rgba(34,211,238,0.4), rgba(139,92,246,0.2), rgba(255,255,255,0.03));
        }
        .timeline-node {
            position: absolute;
            left: 13px;
            top: 6px;
            width: 16px;
            height: 16px;
            border-radius: 50%;
            border: 2px solid #22d3ee;
            background: #030712;
            z-index: 2;
            box-shadow: 0 0 12px rgba(34,211,238,0.3), inset 0 0 4px rgba(34,211,238,0.2);
        }
        .timeline-node.purple {
            border-color: #8b5cf6;
            box-shadow: 0 0 12px rgba(139,92,246,0.3), inset 0 0 4px rgba(139,92,246,0.2);
        }
        .timeline-node.amber {
            border-color: #f59e0b;
            box-shadow: 0 0 12px rgba(245,158,11,0.3), inset 0 0 4px rgba(245,158,11,0.2);
        }

        /* Project card image area */
        .project-visual {
            height: 220px;
            position: relative;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .project-visual .icon-bg {
            font-size: 56px;
            opacity: 0.12;
            transition: all 0.7s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .card:hover .icon-bg {
            opacity: 0.2;
            transform: scale(1.15) rotate(5deg);
        }
        .project-visual .grid-overlay {
            position: absolute;
            inset: 0;
            background-image:
                linear-gradient(rgba(255,255,255,0.02) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255,255,255,0.02) 1px, transparent 1px);
            background-size: 40px 40px;
            opacity: 0;
            transition: opacity 0.5s;
        }
        .card:hover .grid-overlay { opacity: 1; }

        /* Skill category bar */
        .skill-bar {
            height: 3px;
            border-radius: 2px;
            background: rgba(255,255,255,0.05);
            overflow: hidden;
        }
        .skill-bar-fill {
            height: 100%;
            border-radius: 2px;
            transform: scaleX(0);
            transform-origin: left;
            transition: transform 1.2s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .skill-bar-fill.animate { transform: scaleX(1); }

        /* Cert card */
        .cert-item {
            transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
        }
        .cert-item:hover {
            transform: translateX(4px);
            border-color: rgba(255,255,255,0.1);
            background: rgba(255,255,255,0.04);
        }

        /* Nav */
        .nav-link {
            color: #64748b;
            font-size: 13px;
            font-weight: 400;
            transition: color 0.3s;
            text-decoration: none;
            position: relative;
            letter-spacing: -0.01em;
        }
        .nav-link:hover { color: #e2e8f0; }
        .nav-link.active { color: #22d3ee; }
        .nav-link.active::after {
            content: '';
            position: absolute;
            bottom: -6px;
            left: 50%; right: 50%;
            height: 1px;
            background: #22d3ee;
            transition: all 0.3s;
            left: 0; right: 0;
        }

        /* Mobile menu */
        .mobile-overlay {
            position: fixed;
            inset: 0;
            background: rgba(3, 7, 18, 0.95);
            backdrop-filter: blur(30px);
            z-index: 45;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 32px;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.4s;
        }
        .mobile-overlay.open {
            opacity: 1;
            pointer-events: all;
        }
        .mobile-overlay a {
            font-size: 24px;
            font-weight: 300;
            color: #94a3b8;
            text-decoration: none;
            transition: color 0.3s;
        }
        .mobile-overlay a:hover { color: #22d3ee; }

        /* Toast */
        .toast-notification {
            position: fixed;
            bottom: 40px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            padding: 16px 28px;
            border-radius: 12px;
            font-size: 13px;
            z-index: 200;
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            opacity: 0;
            white-space: nowrap;
        }
        .toast-notification.show {
            transform: translateX(-50%) translateY(0);
            opacity: 1;
        }

        /* Glow decorations */
        .glow-cyan {
            position: absolute;
            width: 400px; height: 400px;
            background: radial-gradient(circle, rgba(6,182,212,0.08) 0%, transparent 70%);
            border-radius: 50%;
            pointer-events: none;
        }
        .glow-purple {
            position: absolute;
            width: 350px; height: 350px;
            background: radial-gradient(circle, rgba(139,92,246,0.06) 0%, transparent 70%);
            border-radius: 50%;
            pointer-events: none;
        }

        /* Separator */
        .sep {
            height: 1px;
            background: linear-gradient(to right, transparent, rgba(255,255,255,0.06), transparent);
        }

        /* What I Do icon container */
        .wido-icon {
            width: 48px; height: 48px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
        }
        .wido-icon::after {
            content: '';
            position: absolute;
            inset: -1px;
            border-radius: 13px;
            padding: 1px;
            background: linear-gradient(135deg, var(--glow-color), transparent);
            -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
            -webkit-mask-composite: xor;
            mask-composite: exclude;
            opacity: 0.5;
        }

        /* Form inputs */
        .form-input {
            width: 100%;
            background: rgba(255,255,255,0.03);
            border: 1px solid rgba(255,255,255,0.06);
            border-radius: 10px;
            padding: 14px 18px;
            color: #f1f5f9;
            font-size: 14px;
            font-family: 'Inter', sans-serif;
            font-weight: 300;
            transition: all 0.3s;
            outline: none;
        }
        .form-input::placeholder { color: #475569; }
        .form-input:focus {
            border-color: rgba(6,182,212,0.3);
            background: rgba(255,255,255,0.04);
            box-shadow: 0 0 0 3px rgba(6,182,212,0.05);
        }

        @media (max-width: 768px) {
            .project-visual { height: 160px; }
        }
    </style>
</head>
<body>

<!-- Custom Cursor -->
<div class="cursor-dot" id="cursor-dot"></div>
<div class="cursor-ring" id="cursor-ring"></div>

<!-- Scroll Progress -->
<div class="scroll-progress" id="scroll-progress"></div>

<!-- Three.js Canvas -->
<canvas id="three-canvas"></canvas>

<!-- Ambient Glows -->
<div class="glow-cyan" style="top: 10%; left: -10%;"></div>
<div class="glow-purple" style="top: 50%; right: -8%;"></div>
<div class="glow-cyan" style="bottom: 10%; left: 30%; opacity: 0.5;"></div>

<!-- ==================== NAVIGATION ==================== -->
<nav class="glass-nav fixed top-0 left-0 right-0 z-50 h-16 flex items-center px-6 lg:px-10">
    <div class="max-w-7xl mx-auto w-full flex items-center justify-between">
        <a href="#hero" class="flex items-center gap-3 text-decoration-none group" style="text-decoration:none">
            <div class="w-9 h-9 rounded-lg bg-gradient-to-br from-cyan-500/20 to-purple-500/20 border border-white/10 flex items-center justify-center group-hover:border-cyan-500/30 transition-colors">
                <span class="text-cyan-400 font-semibold text-xs font-mono">SS</span>
            </div>
            <div class="hidden sm:block">
                <div class="text-white text-sm font-medium leading-tight">Suman Seth</div>
                <div class="text-slate-600 text-[10px] font-mono tracking-wider">SOFTWARE ENGINEER</div>
            </div>
        </a>

        <div class="hidden lg:flex items-center gap-9">
            <a href="#about" class="nav-link" data-section="about">About</a>
            <a href="#whatido" class="nav-link" data-section="whatido">Expertise</a>
            <a href="#projects" class="nav-link" data-section="projects">Projects</a>
            <a href="#education" class="nav-link" data-section="education">Education</a>
            <a href="#skills" class="nav-link" data-section="skills">Skills</a>
            <a href="#certifications" class="nav-link" data-section="certifications">Certs</a>
            <a href="#contact" class="nav-link" data-section="contact">Contact</a>
        </div>

        <div class="flex items-center gap-2">
            <a href="https://github.com/Suman18-bit" target="_blank" class="w-9 h-9 rounded-lg flex items-center justify-center text-slate-500 hover:text-white hover:bg-white/5 transition-all">
                <i data-lucide="github" class="w-[18px] h-[18px]"></i>
            </a>
            <a href="https://www.linkedin.com/in/suman-seth-b05417324/" target="_blank" class="w-9 h-9 rounded-lg flex items-center justify-center text-slate-500 hover:text-white hover:bg-white/5 transition-all">
                <i data-lucide="linkedin" class="w-[18px] h-[18px]"></i>
            </a>
            <button id="mobile-toggle" class="lg:hidden w-9 h-9 rounded-lg flex items-center justify-center text-slate-500 hover:text-white hover:bg-white/5 transition-all">
                <i data-lucide="menu" class="w-[18px] h-[18px]" id="menu-icon"></i>
            </button>
        </div>
    </div>
</nav>

<!-- Mobile Overlay -->
<div id="mobile-overlay" class="mobile-overlay">
    <a href="#about" onclick="closeMobile()">About</a>
    <a href="#whatido" onclick="closeMobile()">Expertise</a>
    <a href="#projects" onclick="closeMobile()">Projects</a>
    <a href="#education" onclick="closeMobile()">Education</a>
    <a href="#skills" onclick="closeMobile()">Skills</a>
    <a href="#certifications" onclick="closeMobile()">Certifications</a>
    <a href="#contact" onclick="closeMobile()">Contact</a>
</div>

<!-- ==================== HERO ==================== -->
<section id="hero" class="min-h-screen flex flex-col justify-center px-6 lg:px-10 pt-32 pb-24 relative">
    <div class="max-w-5xl mx-auto w-full">
        <div class="reveal">
            <div class="flex items-center gap-3 mb-10">
                <span class="relative flex h-2.5 w-2.5">
                    <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-emerald-400 opacity-60"></span>
                    <span class="relative inline-flex rounded-full h-2.5 w-2.5 bg-emerald-500"></span>
                </span>
                <span class="text-slate-500 text-sm font-light tracking-wide">Open to opportunities</span>
                <span class="text-slate-700">—</span>
                <span class="text-slate-600 text-sm font-light">India 🇮🇳</span>
            </div>
        </div>

        <h1 class="reveal d1 text-5xl sm:text-6xl md:text-7xl lg:text-[5.5rem] font-semibold leading-[0.92] tracking-[-0.04em] mb-8">
            <span class="text-gradient-subtle">Hello, I'm</span><br>
            <span class="text-gradient">Suman Seth</span>
        </h1>

        <div class="reveal d2 mb-6">
            <p class="text-lg md:text-xl font-light text-slate-400 leading-relaxed">
                <span id="typed-text"></span><span class="typing-cursor"></span>
            </p>
        </div>

        <p class="reveal d3 text-base font-light text-slate-600 leading-relaxed max-w-2xl mb-12">
            Swami Vivekananda University, Class of 2028. Passionate about building intelligent systems that bridge the gap between data science, machine learning, and production-grade software.
        </p>

        <div class="reveal d4 flex flex-wrap gap-3 mb-20">
            <a href="#projects" class="btn-primary">
                <i data-lucide="layers" class="w-4 h-4"></i> View Projects
            </a>
            <a href="#contact" class="btn-cta">
                <i data-lucide="message-circle" class="w-4 h-4"></i> Get In Touch
            </a>
            <a href="https://github.com/Suman18-bit" target="_blank" class="btn-ghost">
                <i data-lucide="github" class="w-4 h-4"></i> GitHub
            </a>
        </div>

        <div class="reveal d5 grid grid-cols-2 md:grid-cols-4 gap-6 md:gap-10 pt-10 border-t border-white/[0.04]">
            <div>
                <div class="text-3xl md:text-4xl font-semibold tracking-tight text-gradient" data-count="4">0</div>
                <div class="text-slate-600 text-xs font-light mt-2 tracking-wide">Projects</div>
            </div>
            <div>
                <div class="text-3xl md:text-4xl font-semibold tracking-tight text-gradient" data-count="17">0</div>
                <div class="text-slate-600 text-xs font-light mt-2 tracking-wide">Certifications</div>
            </div>
            <div>
                <div class="text-3xl md:text-4xl font-semibold tracking-tight text-gradient" data-count="30">0</div>
                <div class="text-slate-600 text-xs font-light mt-2 tracking-wide">Technologies</div>
            </div>
            <div>
                <div class="text-3xl md:text-4xl font-semibold tracking-tight text-gradient">A+</div>
                <div class="text-slate-600 text-xs font-light mt-2 tracking-wide">Grade Point</div>
            </div>
        </div>
    </div>

    <!-- Scroll indicator -->
    <div class="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2 reveal d6">
        <span class="text-slate-700 text-[10px] font-mono uppercase tracking-widest">Scroll</span>
        <div class="w-5 h-8 rounded-full border border-white/10 flex items-start justify-center p-1.5">
            <div class="w-1 h-1.5 rounded-full bg-cyan-400 animate-bounce"></div>
        </div>
    </div>
</section>

<div class="sep max-w-7xl mx-auto"></div>

<!-- ==================== ABOUT ==================== -->
<section id="about" class="px-6 lg:px-10 py-28">
    <div class="max-w-7xl mx-auto">
        <div class="reveal">
            <span class="section-label">01 — About</span>
            <h2 class="text-3xl md:text-4xl font-medium tracking-[-0.025em] mt-4 mb-2">Who I Am</h2>
            <div class="section-divider"></div>
        </div>

        <div class="grid lg:grid-cols-12 gap-12 lg:gap-16 mt-16">
            <div class="lg:col-span-7 reveal-left">
                <div class="space-y-6">
                    <p class="text-slate-400 font-light leading-[1.85] text-[15px]">
                        I'm <span class="text-white font-normal">Suman Seth</span>, a Computer Science Engineering student at
                        <span class="text-cyan-400">Swami Vivekananda University</span>, Kolkata. My journey into technology started with a deep curiosity about how machines learn — and it has evolved into a relentless pursuit of building systems that solve real problems.
                    </p>
                    <p class="text-slate-400 font-light leading-[1.85] text-[15px]">
                        From developing a <span class="text-white font-normal">Smart Image Caption Generator</span> using CNN-LSTM architectures to building an
                        <span class="text-white font-normal">intelligent book Q&A system</span> powered by LLMs and vector databases, I thrive at the intersection of data, algorithms, and elegant software design.
                    </p>
                    <p class="text-slate-400 font-light leading-[1.85] text-[15px]">
                        I'm equally comfortable writing production-grade backend APIs with <span class="text-white font-normal">Django</span> as I am training neural networks with <span class="text-white font-normal">PyTorch</span>. With 17+ certifications from
                        <span class="text-white font-normal">Microsoft, LinkedIn Learning, Qualcomm, Saylor University,</span> and more — I believe in continuous, structured learning.
                    </p>
                </div>

                <div class="flex flex-wrap gap-3 mt-10">
                    <a href="#contact" class="btn-cta btn-sm">
                        <i data-lucide="download" class="w-3.5 h-3.5"></i> Download Resume
                    </a>
                    <a href="mailto:sethn533@gmail.com" class="btn-ghost btn-sm">
                        <i data-lucide="mail" class="w-3.5 h-3.5"></i> Email Me
                    </a>
                </div>
            </div>

            <div class="lg:col-span-5 reveal-right">
                <div class="glass-strong rounded-2xl p-7 space-y-5 border-gradient">
                    <h3 class="text-white font-medium text-sm tracking-wide mb-6">PERSONAL DETAILS</h3>

                    <div class="space-y-4">
                        <div class="flex items-center gap-4">
                            <div class="w-8 h-8 rounded-lg bg-cyan-500/10 flex items-center justify-center flex-shrink-0">
                                <i data-lucide="user" class="w-3.5 h-3.5 text-cyan-400"></i>
                            </div>
                            <div>
                                <div class="text-slate-600 text-[10px] uppercase tracking-widest font-mono">Name</div>
                                <div class="text-slate-200 text-sm font-light">Suman Seth</div>
                            </div>
                        </div>

                        <div class="h-px bg-white/[0.04]"></div>

                        <div class="flex items-center gap-4">
                            <div class="w-8 h-8 rounded-lg bg-cyan-500/10 flex items-center justify-center flex-shrink-0">
                                <i data-lucide="map-pin" class="w-3.5 h-3.5 text-cyan-400"></i>
                            </div>
                            <div>
                                <div class="text-slate-600 text-[10px] uppercase tracking-widest font-mono">Location</div>
                                <div class="text-slate-200 text-sm font-light">Nandigram-II, West Bengal</div>
                            </div>
                        </div>

                        <div class="h-px bg-white/[0.04]"></div>

                        <div class="flex items-center gap-4">
                            <div class="w-8 h-8 rounded-lg bg-purple-500/10 flex items-center justify-center flex-shrink-0">
                                <i data-lucide="graduation-cap" class="w-3.5 h-3.5 text-purple-400"></i>
                            </div>
                            <div>
                                <div class="text-slate-600 text-[10px] uppercase tracking-widest font-mono">University</div>
                                <div class="text-slate-200 text-sm font-light">Swami Vivekananda University</div>
                            </div>
                        </div>

                        <div class="h-px bg-white/[0.04]"></div>

                        <div class="flex items-center gap-4">
                            <div class="w-8 h-8 rounded-lg bg-emerald-500/10 flex items-center justify-center flex-shrink-0">
                                <i data-lucide="calendar" class="w-3.5 h-3.5 text-emerald-400"></i>
                            </div>
                            <div>
                                <div class="text-slate-600 text-[10px] uppercase tracking-widest font-mono">Graduation</div>
                                <div class="text-slate-200 text-sm font-light">August 2028</div>
                            </div>
                        </div>

                        <div class="h-px bg-white/[0.04]"></div>

                        <div class="flex items-center gap-4">
                            <div class="w-8 h-8 rounded-lg bg-amber-500/10 flex items-center justify-center flex-shrink-0">
                                <i data-lucide="phone" class="w-3.5 h-3.5 text-amber-400"></i>
                            </div>
                            <div>
                                <div class="text-slate-600 text-[10px] uppercase tracking-widest font-mono">Phone</div>
                                <a href="tel:+919547111445" class="text-slate-200 text-sm font-light hover:text-cyan-400 transition-colors">+91 9547111445</a>
                            </div>
                        </div>

                        <div class="h-px bg-white/[0.04]"></div>

                        <div class="flex items-center gap-4">
                            <div class="w-8 h-8 rounded-lg bg-rose-500/10 flex items-center justify-center flex-shrink-0">
                                <i data-lucide="mail" class="w-3.5 h-3.5 text-rose-400"></i>
                            </div>
                            <div>
                                <div class="text-slate-600 text-[10px] uppercase tracking-widest font-mono">Email</div>
                                <a href="mailto:sethn533@gmail.com" class="text-cyan-400 text-sm font-light hover:text-cyan-300 transition-colors">sethn533@gmail.com</a>
                            </div>
                        </div>
                    </div>

                    <div class="pt-5 flex gap-2">
                        <a href="https://github.com/Suman18-bit" target="_blank" class="btn-ghost btn-xs flex-1 justify-center">
                            <i data-lucide="github" class="w-3 h-3"></i> GitHub
                        </a>
                        <a href="https://www.linkedin.com/in/suman-seth-b05417324/" target="_blank" class="btn-ghost btn-xs flex-1 justify-center">
                            <i data-lucide="linkedin" class="w-3 h-3"></i> LinkedIn
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</section>

<div class="sep max-w-7xl mx-auto"></div>

<!-- ==================== WHAT I DO ==================== -->
<section id="whatido" class="px-6 lg:px-10 py-28">
    <div class="max-w-7xl mx-auto">
        <div class="reveal">
            <span class="section-label">02 — Expertise</span>
            <h2 class="text-3xl md:text-4xl font-medium tracking-[-0.025em] mt-4 mb-2">What I Do</h2>
            <div class="section-divider"></div>
        </div>

        <div class="grid md:grid-cols-2 lg:grid-cols-4 gap-5 mt-16">
            <div class="reveal d1 glass rounded-2xl p-7 card group">
                <div class="wido-icon bg-cyan-500/10 mb-6" style="--glow-color: rgba(6,182,212,0.5);">
                    <i data-lucide="brain" class="w-5 h-5 text-cyan-400"></i>
                </div>
                <h3 class="text-white font-medium text-[15px] mb-2">Machine Learning</h3>
                <p class="text-slate-500 font-light text-sm leading-relaxed">Building predictive models, classification systems, and recommendation engines using scikit-learn, TensorFlow, and PyTorch.</p>
            </div>

            <div class="reveal d2 glass rounded-2xl p-7 card group">
                <div class="wido-icon bg-purple-500/10 mb-6" style="--glow-color: rgba(139,92,246,0.5);">
                    <i data-lucide="message-square" class="w-5 h-5 text-purple-400"></i>
                </div>
                <h3 class="text-white font-medium text-[15px] mb-2">NLP & LLMs</h3>
                <p class="text-slate-500 font-light text-sm leading-relaxed">Working with LangChain, HuggingFace, and vector databases to build RAG systems and intelligent text applications.</p>
            </div>

            <div class="reveal d3 glass rounded-2xl p-7 card group">
                <div class="wido-icon bg-emerald-500/10 mb-6" style="--glow-color: rgba(16,185,129,0.5);">
                    <i data-lucide="code-2" class="w-5 h-5 text-emerald-400"></i>
                </div>
                <h3 class="text-white font-medium text-[15px] mb-2">Software Engineering</h3>
                <p class="text-slate-500 font-light text-sm leading-relaxed">Building robust backends with Django, REST APIs, and deploying production applications with Docker and cloud platforms.</p>
            </div>

            <div class="reveal d4 glass rounded-2xl p-7 card group">
                <div class="wido-icon bg-amber-500/10 mb-6" style="--glow-color: rgba(245,158,11,0.5);">
                    <i data-lucide="eye" class="w-5 h-5 text-amber-400"></i>
                </div>
                <h3 class="text-white font-medium text-[15px] mb-2">Computer Vision</h3>
                <p class="text-slate-500 font-light text-sm leading-relaxed">Developing image captioning, emotion detection, and visual recognition systems using OpenCV, CNNs, and deep learning.</p>
            </div>
        </div>
    </div>
</section>

<div class="sep max-w-7xl mx-auto"></div>

<!-- ==================== PROJECTS ==================== -->
<section id="projects" class="px-6 lg:px-10 py-28">
    <div class="max-w-7xl mx-auto">
        <div class="reveal">
            <span class="section-label">03 — Projects</span>
            <h2 class="text-3xl md:text-4xl font-medium tracking-[-0.025em] mt-4 mb-2">Featured Work</h2>
            <div class="section-divider"></div>
            <p class="text-slate-500 font-light text-[15px] mt-6 max-w-lg">A curated selection of projects that showcase my skills across AI, ML, and software engineering.</p>
        </div>

        <div class="grid md:grid-cols-2 gap-6 mt-16">
            <!-- Project 1 -->
            <div class="reveal d1 glass rounded-2xl overflow-hidden card border-gradient group">
                <div class="project-visual bg-gradient-to-br from-cyan-950/30 to-slate-950/50">
                    <div class="grid-overlay"></div>
                    <i data-lucide="book-open" class="icon-bg text-cyan-400"></i>
                    <div class="absolute top-4 right-4">
                        <span class="text-[10px] font-mono font-medium uppercase tracking-widest text-cyan-400/60 bg-cyan-400/5 border border-cyan-400/10 px-3 py-1 rounded-full">NLP · LLM</span>
                    </div>
                </div>
                <div class="p-7">
                    <h3 class="text-lg font-medium mb-2 group-hover:text-cyan-300 transition-colors">AskMyBook</h3>
                    <p class="text-slate-500 font-light text-sm leading-relaxed mb-5">
                        An intelligent Q&A system enabling users to interact with books via natural language. Uses LLMs with RAG architecture and vector embeddings for precise, context-aware answers.
                    </p>
                    <div class="flex flex-wrap gap-1.5 mb-6">
                        <span class="tag">Python</span>
                        <span class="tag">LangChain</span>
                        <span class="tag">ChromaDB</span>
                        <span class="tag">HuggingFace</span>
                    </div>
                    <a href="https://github.com/Suman18-bit/AskMyBook" target="_blank" class="inline-flex items-center gap-2 text-cyan-400 text-xs font-medium hover:text-cyan-300 transition-colors group/link">
                        <i data-lucide="github" class="w-3.5 h-3.5"></i> View Source
                        <i data-lucide="arrow-up-right" class="w-3 h-3 transition-transform group-hover/link:translate-x-0.5 group-hover/link:-translate-y-0.5"></i>
                    </a>
                </div>
            </div>

            <!-- Project 2 -->
            <div class="reveal d2 glass rounded-2xl overflow-hidden card border-gradient group">
                <div class="project-visual bg-gradient-to-br from-purple-950/30 to-slate-950/50">
                    <div class="grid-overlay"></div>
                    <i data-lucide="image" class="icon-bg text-purple-400"></i>
                    <div class="absolute top-4 right-4">
                        <span class="text-[10px] font-mono font-medium uppercase tracking-widest text-purple-400/60 bg-purple-400/5 border border-purple-400/10 px-3 py-1 rounded-full">Deep Learning</span>
                    </div>
                </div>
                <div class="p-7">
                    <h3 class="text-lg font-medium mb-2 group-hover:text-purple-300 transition-colors">Smart Image Caption Generator</h3>
                    <p class="text-slate-500 font-light text-sm leading-relaxed mb-5">
                        AI system that generates descriptive captions for images using a CNN-LSTM architecture. Combines computer vision feature extraction with sequence-to-sequence language modeling.
                    </p>
                    <div class="flex flex-wrap gap-1.5 mb-6">
                        <span class="tag">TensorFlow</span>
                        <span class="tag">Keras</span>
                        <span class="tag">OpenCV</span>
                        <span class="tag">NumPy</span>
                    </div>
                    <a href="https://github.com/Suman18-bit/Project(Smart)%20Image%20Caption%20Generator" target="_blank" class="inline-flex items-center gap-2 text-purple-400 text-xs font-medium hover:text-purple-300 transition-colors group/link">
                        <i data-lucide="github" class="w-3.5 h-3.5"></i> View Source
                        <i data-lucide="arrow-up-right" class="w-3 h-3 transition-transform group-hover/link:translate-x-0.5 group-hover/link:-translate-y-0.5"></i>
                    </a>
                </div>
            </div>

            <!-- Project 3 -->
            <div class="reveal d3 glass rounded-2xl overflow-hidden card border-gradient group">
                <div class="project-visual bg-gradient-to-br from-emerald-950/30 to-slate-950/50">
                    <div class="grid-overlay"></div>
                    <i data-lucide="clapperboard" class="icon-bg text-emerald-400"></i>
                    <div class="absolute top-4 right-4">
                        <span class="text-[10px] font-mono font-medium uppercase tracking-widest text-emerald-400/60 bg-emerald-400/5 border border-emerald-400/10 px-3 py-1 rounded-full">Data Science</span>
                    </div>
                </div>
                <div class="p-7">
                    <h3 class="text-lg font-medium mb-2 group-hover:text-emerald-300 transition-colors">Movie Recommendation System</h3>
                    <p class="text-slate-500 font-light text-sm leading-relaxed mb-5">
                        Content-based and collaborative filtering engine that suggests movies based on user preferences. Features data pipelines, similarity algorithms, and a Streamlit interface.
                    </p>
                    <div class="flex flex-wrap gap-1.5 mb-6">
                        <span class="tag">Python</span>
                        <span class="tag">Scikit-learn</span>
                        <span class="tag">Pandas</span>
                        <span class="tag">Streamlit</span>
                    </div>
                    <a href="https://github.com/Suman18-bit/Movie-Recommendation-System-" target="_blank" class="inline-flex items-center gap-2 text-emerald-400 text-xs font-medium hover:text-emerald-300 transition-colors group/link">
                        <i data-lucide="github" class="w-3.5 h-3.5"></i> View Source
                        <i data-lucide="arrow-up-right" class="w-3 h-3 transition-transform group-hover/link:translate-x-0.5 group-hover/link:-translate-y-0.5"></i>
                    </a>
                </div>
            </div>

            <!-- Project 4 -->
            <div class="reveal d4 glass rounded-2xl overflow-hidden card border-gradient group">
                <div class="project-visual bg-gradient-to-br from-amber-950/30 to-slate-950/50">
                    <div class="grid-overlay"></div>
                    <i data-lucide="smile" class="icon-bg text-amber-400"></i>
                    <div class="absolute top-4 right-4">
                        <span class="text-[10px] font-mono font-medium uppercase tracking-widest text-amber-400/60 bg-amber-400/5 border border-amber-400/10 px-3 py-1 rounded-full">Real-time AI</span>
                    </div>
                </div>
                <div class="p-7">
                    <h3 class="text-lg font-medium mb-2 group-hover:text-amber-300 transition-colors">Emotion Detection System</h3>
                    <p class="text-slate-500 font-light text-sm leading-relaxed mb-5">
                        Real-time facial emotion recognition from live video feeds using deep learning. Detects and classifies human emotions with optimized inference for smooth performance.
                    </p>
                    <div class="flex flex-wrap gap-1.5 mb-6">
                        <span class="tag">Python</span>
                        <span class="tag">OpenCV</span>
                        <span class="tag">TensorFlow</span>
                        <span class="tag">CUDA</span>
                    </div>
                    <a href="https://github.com/Suman18-bit/Emotion_detection_Project" target="_blank" class="inline-flex items-center gap-2 text-amber-400 text-xs font-medium hover:text-amber-300 transition-colors group/link">
                        <i data-lucide="github" class="w-3.5 h-3.5"></i> View Source
                        <i data-lucide="arrow-up-right" class="w-3 h-3 transition-transform group-hover/link:translate-x-0.5 group-hover/link:-translate-y-0.5"></i>
                    </a>
                </div>
            </div>
        </div>
    </div>
</section>

<div class="sep max-w-7xl mx-auto"></div>

<!-- ==================== EDUCATION ==================== -->
<section id="education" class="px-6 lg:px-10 py-28">
    <div class="max-w-7xl mx-auto">
        <div class="reveal">
            <span class="section-label">04 — Education</span>
            <h2 class="text-3xl md:text-4xl font-medium tracking-[-0.025em] mt-4 mb-2">Academic Journey</h2>
            <div class="section-divider"></div>
        </div>

        <div class="max-w-3xl mt-16">
            <div class="relative pl-12">
                <div class="timeline-track"></div>

                <div class="reveal d1 relative pb-14">
                    <div class="timeline-node"></div>
                    <div class="glass rounded-2xl p-7 card border-gradient">
                        <div class="flex flex-wrap items-center gap-3 mb-4">
                            <span class="text-[10px] font-mono font-semibold uppercase tracking-widest text-cyan-400 bg-cyan-400/10 px-3 py-1 rounded-full">Current</span>
                            <span class="text-slate-600 text-xs font-mono">Jul 2024 — Aug 2028</span>
                        </div>
                        <h3 class="text-[17px] font-medium mb-1">B.Tech in Computer Science & Engineering</h3>
                        <p class="text-cyan-400/80 text-sm font-light mb-4">Swami Vivekananda University, Kolkata</p>
                        <p class="text-slate-500 font-light text-sm leading-relaxed mb-4">
                            Specializing in AI/ML, Data Science, and Software Engineering. Building expertise in algorithms, system design, and machine learning with consistent academic excellence.
                        </p>
                        <div class="flex items-center gap-2">
                            <span class="w-1.5 h-1.5 rounded-full bg-emerald-500"></span>
                            <span class="text-emerald-400 text-sm font-medium font-mono">Grade: A+</span>
                        </div>
                    </div>
                </div>

                <div class="reveal d2 relative pb-14">
                    <div class="timeline-node purple"></div>
                    <div class="glass rounded-2xl p-7 card">
                        <div class="flex flex-wrap items-center gap-3 mb-4">
                            <span class="text-slate-600 text-xs font-mono">May 2022 — Apr 2024</span>
                        </div>
                        <h3 class="text-[17px] font-medium mb-1">Higher Secondary — Class 12</h3>
                        <p class="text-purple-400/80 text-sm font-light mb-4">WBCHSE</p>
                        <p class="text-slate-500 font-light text-sm leading-relaxed">
                            Science stream — Physics, Chemistry, Mathematics & Biology. Developed strong analytical foundations and problem-solving discipline.
                        </p>
                    </div>
                </div>

                <div class="reveal d3 relative">
                    <div class="timeline-node amber"></div>
                    <div class="glass rounded-2xl p-7 card">
                        <div class="flex flex-wrap items-center gap-3 mb-4">
                            <span class="text-slate-600 text-xs font-mono">Jan 2021 — Apr 2022</span>
                        </div>
                        <h3 class="text-[17px] font-medium mb-1">Secondary — Class 10</h3>
                        <p class="text-amber-400/80 text-sm font-light mb-4">WBBSE</p>
                        <div class="flex items-center gap-2">
                            <span class="w-1.5 h-1.5 rounded-full bg-emerald-500"></span>
                            <span class="text-emerald-400 text-sm font-medium font-mono">Grade: A</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</section>

<div class="sep max-w-7xl mx-auto"></div>

<!-- ==================== SKILLS ==================== -->
<section id="skills" class="px-6 lg:px-10 py-28">
    <div class="max-w-7xl mx-auto">
        <div class="reveal">
            <span class="section-label">05 — Skills</span>
            <h2 class="text-3xl md:text-4xl font-medium tracking-[-0.025em] mt-4 mb-2">Technical Arsenal</h2>
            <div class="section-divider"></div>
        </div>

        <div class="grid lg:grid-cols-3 gap-6 mt-16">
            <!-- Web & Backend -->
            <div class="reveal d1 glass rounded-2xl p-7 card border-gradient">
                <div class="flex items-center gap-4 mb-2">
                    <div class="w-10 h-10 rounded-xl bg-cyan-500/10 flex items-center justify-center">
                        <i data-lucide="globe" class="w-5 h-5 text-cyan-400"></i>
                    </div>
                    <div>
                        <h3 class="text-white font-medium text-[15px]">Software Engineering</h3>
                        <p class="text-slate-600 text-[11px] font-mono">Backend · Web · Deployment</p>
                    </div>
                </div>
                <div class="skill-bar mt-5 mb-6">
                    <div class="skill-bar-fill bg-gradient-to-r from-cyan-500 to-cyan-400" style="width:85%"></div>
                </div>
                <div class="flex flex-wrap gap-1.5">
                    <span class="tag">Django</span>
                    <span class="tag">HTML5</span>
                    <span class="tag">CSS3</span>
                    <span class="tag">JavaScript</span>
                    <span class="tag">PHP</span>
                    <span class="tag">Streamlit</span>
                    <span class="tag">Vercel</span>
                    <span class="tag">ChromaDB</span>
                    <span class="tag">Gradio</span>
                    <span class="tag">REST API</span>
                </div>
            </div>

            <!-- AI / ML -->
            <div class="reveal d2 glass rounded-2xl p-7 card border-gradient">
                <div class="flex items-center gap-4 mb-2">
                    <div class="w-10 h-10 rounded-xl bg-purple-500/10 flex items-center justify-center">
                        <i data-lucide="brain" class="w-5 h-5 text-purple-400"></i>
                    </div>
                    <div>
                        <h3 class="text-white font-medium text-[15px]">AI · ML · Data Science</h3>
                        <p class="text-slate-600 text-[11px] font-mono">Deep Learning · NLP · CV</p>
                    </div>
                </div>
                <div class="skill-bar mt-5 mb-6">
                    <div class="skill-bar-fill bg-gradient-to-r from-purple-500 to-purple-400" style="width:92%"></div>
                </div>
                <div class="flex flex-wrap gap-1.5">
                    <span class="tag">Python</span>
                    <span class="tag">TensorFlow</span>
                    <span class="tag">PyTorch</span>
                    <span class="tag">Scikit-learn</span>
                    <span class="tag">Keras</span>
                    <span class="tag">LangChain</span>
                    <span class="tag">HuggingFace</span>
                    <span class="tag">NumPy</span>
                    <span class="tag">Pandas</span>
                    <span class="tag">MLflow</span>
                    <span class="tag">OpenCV</span>
                    <span class="tag">CUDA</span>
                </div>
            </div>

            <!-- Tools & Cloud -->
            <div class="reveal d3 glass rounded-2xl p-7 card border-gradient">
                <div class="flex items-center gap-4 mb-2">
                    <div class="w-10 h-10 rounded-xl bg-emerald-500/10 flex items-center justify-center">
                        <i data-lucide="terminal" class="w-5 h-5 text-emerald-400"></i>
                    </div>
                    <div>
                        <h3 class="text-white font-medium text-[15px]">Languages · Tools · Cloud</h3>
                        <p class="text-slate-600 text-[11px] font-mono">DevOps · Infrastructure</p>
                    </div>
                </div>
                <div class="skill-bar mt-5 mb-6">
                    <div class="skill-bar-fill bg-gradient-to-r from-emerald-500 to-emerald-400" style="width:78%"></div>
                </div>
                <div class="flex flex-wrap gap-1.5">
                    <span class="tag">C</span>
                    <span class="tag">C++</span>
                    <span class="tag">Kotlin</span>
                    <span class="tag">Docker</span>
                    <span class="tag">Git</span>
                    <span class="tag">GitHub</span>
                    <span class="tag">GCP</span>
                    <span class="tag">PostgreSQL</span>
                    <span class="tag">VS Code</span>
                    <span class="tag">Linux</span>
                    <span class="tag">GH Actions</span>
                </div>
            </div>
        </div>
    </div>
</section>

<div class="sep max-w-7xl mx-auto"></div>

<!-- ==================== CERTIFICATIONS ==================== -->
<section id="certifications" class="px-6 lg:px-10 py-28">
    <div class="max-w-7xl mx-auto">
        <div class="reveal flex flex-col md:flex-row md:items-end md:justify-between gap-4">
            <div>
                <span class="section-label">06 — Certifications</span>
                <h2 class="text-3xl md:text-4xl font-medium tracking-[-0.025em] mt-4 mb-2">Credentials</h2>
                <div class="section-divider"></div>
                <p class="text-slate-500 font-light text-[15px] mt-6 max-w-lg">17 certifications from industry leaders — validating expertise in AI, ML, data engineering, and professional development.</p>
            </div>
            <button onclick="toggleCerts()" class="btn-ghost btn-sm self-start md:self-auto flex-shrink-0">
                <i data-lucide="chevrons-down" class="w-4 h-4" id="cert-icon"></i>
                <span id="cert-btn-text">Show All 17</span>
            </button>
        </div>

        <div class="mt-12 grid md:grid-cols-2 gap-3" id="certs-container">
            <!-- Visible certs -->
            <div class="reveal d1 cert-item glass rounded-xl p-5 flex items-center gap-4">
                <div class="w-9 h-9 rounded-lg bg-blue-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="linkedin" class="w-4 h-4 text-blue-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Advance Your Skills in NLP</h4>
                    <p class="text-slate-600 text-[11px] font-mono">LinkedIn · Jun 2026</p>
                </div>
            </div>
            <div class="reveal d2 cert-item glass rounded-xl p-5 flex items-center gap-4">
                <div class="w-9 h-9 rounded-lg bg-blue-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="linkedin" class="w-4 h-4 text-blue-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Generative AI: Working with LLMs</h4>
                    <p class="text-slate-600 text-[11px] font-mono">LinkedIn · Jun 2026</p>
                </div>
            </div>
            <div class="reveal d3 cert-item glass rounded-xl p-5 flex items-center gap-4">
                <div class="w-9 h-9 rounded-lg bg-blue-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="linkedin" class="w-4 h-4 text-blue-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Deep Learning with TensorFlow</h4>
                    <p class="text-slate-600 text-[11px] font-mono">LinkedIn · Jun 2026</p>
                </div>
            </div>
            <div class="reveal d4 cert-item glass rounded-xl p-5 flex items-center gap-4">
                <div class="w-9 h-9 rounded-lg bg-green-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="box" class="w-4 h-4 text-green-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Data Engineer Career Path</h4>
                    <p class="text-slate-600 text-[11px] font-mono">Microsoft · Jun 2026</p>
                </div>
            </div>
            <div class="reveal d5 cert-item glass rounded-xl p-5 flex items-center gap-4">
                <div class="w-9 h-9 rounded-lg bg-blue-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="linkedin" class="w-4 h-4 text-blue-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Hands-On NLP</h4>
                    <p class="text-slate-600 text-[11px] font-mono">LinkedIn · Jun 2026</p>
                </div>
            </div>
            <div class="reveal d6 cert-item glass rounded-xl p-5 flex items-center gap-4">
                <div class="w-9 h-9 rounded-lg bg-blue-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="linkedin" class="w-4 h-4 text-blue-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Advanced NLP with Python for ML</h4>
                    <p class="text-slate-600 text-[11px] font-mono">LinkedIn · Jun 2026</p>
                </div>
            </div>

            <!-- Hidden certs -->
            <div class="cert-hidden cert-item glass rounded-xl p-5 flex items-center gap-4" style="display:none">
                <div class="w-9 h-9 rounded-lg bg-green-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="box" class="w-4 h-4 text-green-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">AI Skills Fest 2026</h4>
                    <p class="text-slate-600 text-[11px] font-mono">Microsoft · Jun 2026</p>
                </div>
            </div>
            <div class="cert-hidden cert-item glass rounded-xl p-5 flex items-center gap-4" style="display:none">
                <div class="w-9 h-9 rounded-lg bg-blue-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="linkedin" class="w-4 h-4 text-blue-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Career Skills in Data Analytics</h4>
                    <p class="text-slate-600 text-[11px] font-mono">LinkedIn · Jun 2026</p>
                </div>
            </div>
            <div class="cert-hidden cert-item glass rounded-xl p-5 flex items-center gap-4" style="display:none">
                <div class="w-9 h-9 rounded-lg bg-amber-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="graduation-cap" class="w-4 h-4 text-amber-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Fundamentals of Machine Learning</h4>
                    <p class="text-slate-600 text-[11px] font-mono">Saylor University · Jun 2026</p>
                </div>
            </div>
            <div class="cert-hidden cert-item glass rounded-xl p-5 flex items-center gap-4" style="display:none">
                <div class="w-9 h-9 rounded-lg bg-indigo-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="printer" class="w-4 h-4 text-indigo-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Professional Networking for Career Growth</h4>
                    <p class="text-slate-600 text-[11px] font-mono">HP · Aug 2025</p>
                </div>
            </div>
            <div class="cert-hidden cert-item glass rounded-xl p-5 flex items-center gap-4" style="display:none">
                <div class="w-9 h-9 rounded-lg bg-red-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="cpu" class="w-4 h-4 text-red-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">AI Upskilling: Technical Foundations</h4>
                    <p class="text-slate-600 text-[11px] font-mono">Qualcomm · Jun 2026</p>
                </div>
            </div>
            <div class="cert-hidden cert-item glass rounded-xl p-5 flex items-center gap-4" style="display:none">
                <div class="w-9 h-9 rounded-lg bg-orange-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="trophy" class="w-4 h-4 text-orange-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Operating System (OS)</h4>
                    <p class="text-slate-600 text-[11px] font-mono">Unstop · Jan 2026</p>
                </div>
            </div>
            <div class="cert-hidden cert-item glass rounded-xl p-5 flex items-center gap-4" style="display:none">
                <div class="w-9 h-9 rounded-lg bg-cyan-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="database" class="w-4 h-4 text-cyan-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Introduction to SQL</h4>
                    <p class="text-slate-600 text-[11px] font-mono">Simplilearn · May 2026</p>
                </div>
            </div>
            <div class="cert-hidden cert-item glass rounded-xl p-5 flex items-center gap-4" style="display:none">
                <div class="w-9 h-9 rounded-lg bg-green-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="table" class="w-4 h-4 text-green-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Business Analytics with Excel</h4>
                    <p class="text-slate-600 text-[11px] font-mono">Microsoft · May 2026</p>
                </div>
            </div>
            <div class="cert-hidden cert-item glass rounded-xl p-5 flex items-center gap-4" style="display:none">
                <div class="w-9 h-9 rounded-lg bg-purple-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="sparkles" class="w-4 h-4 text-purple-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Python for Machine Learning</h4>
                    <p class="text-slate-600 text-[11px] font-mono">Great Learning · May 2026</p>
                </div>
            </div>
            <div class="cert-hidden cert-item glass rounded-xl p-5 flex items-center gap-4" style="display:none">
                <div class="w-9 h-9 rounded-lg bg-orange-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="trophy" class="w-4 h-4 text-orange-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Probability</h4>
                    <p class="text-slate-600 text-[11px] font-mono">Unstop · May 2026</p>
                </div>
            </div>
            <div class="cert-hidden cert-item glass rounded-xl p-5 flex items-center gap-4" style="display:none">
                <div class="w-9 h-9 rounded-lg bg-orange-500/10 flex items-center justify-center flex-shrink-0">
                    <i data-lucide="trophy" class="w-4 h-4 text-orange-400"></i>
                </div>
                <div class="flex-1 min-w-0">
                    <h4 class="text-[13px] font-medium truncate">Kascade, Kshitij 2026 — Participation</h4>
                    <p class="text-slate-600 text-[11px] font-mono">Unstop · Jan 2026</p>
                </div>
            </div>
        </div>
    </div>
</section>

<div class="sep max-w-7xl mx-auto"></div>

<!-- ==================== CONTACT ==================== -->
<section id="contact" class="px-6 lg:px-10 py-28">
    <div class="max-w-7xl mx-auto">
        <div class="reveal">
            <span class="section-label">07 — Contact</span>
            <h2 class="text-3xl md:text-4xl font-medium tracking-[-0.025em] mt-4 mb-2">Let's Work Together</h2>
            <div class="section-divider"></div>
            <p class="text-slate-500 font-light text-[15px] mt-6 max-w-lg">Have a project in mind, an opportunity, or just want to connect? I'm always open to meaningful conversations.</p>
        </div>

        <div class="grid lg:grid-cols-5 gap-10 mt-16">
            <div class="lg:col-span-2 reveal-left space-y-4">
                <a href="mailto:sethn533@gmail.com" class="glass rounded-xl p-5 flex items-center gap-4 hover:border-cyan-500/20 transition-all group block">
                    <div class="w-10 h-10 rounded-lg bg-cyan-500/10 flex items-center justify-center flex-shrink-0 group-hover:bg-cyan-500/20 transition-colors">
                        <i data-lucide="mail" class="w-4 h-4 text-cyan-400"></i>
                    </div>
                    <div class="min-w-0">
                        <div class="text-slate-600 text-[10px] uppercase tracking-widest font-mono">Email</div>
                        <div class="text-slate-300 text-sm font-light truncate group-hover:text-cyan-400 transition-colors">sethn533@gmail.com</div>
                    </div>
                </a>

                <a href="tel:+919547111445" class="glass rounded-xl p-5 flex items-center gap-4 hover:border-emerald-500/20 transition-all group block">
                    <div class="w-10 h-10 rounded-lg bg-emerald-500/10 flex items-center justify-center flex-shrink-0 group-hover:bg-emerald-500/20 transition-colors">
                        <i data-lucide="phone" class="w-4 h-4 text-emerald-400"></i>
                    </div>
                    <div class="min-w-0">
                        <div class="text-slate-600 text-[10px] uppercase tracking-widest font-mono">Phone</div>
                        <div class="text-slate-300 text-sm font-light group-hover:text-emerald-400 transition-colors">+91 9547111445</div>
                    </div>
                </a>

                <a href="https://www.linkedin.com/in/suman-seth-b05417324/" target="_blank" class="glass rounded-xl p-5 flex items-center gap-4 hover:border-blue-500/20 transition-all group block">
                    <div class="w-10 h-10 rounded-lg bg-blue-500/10 flex items-center justify-center flex-shrink-0 group-hover:bg-blue-500/20 transition-colors">
                        <i data-lucide="linkedin" class="w-4 h-4 text-blue-400"></i>
                    </div>
                    <div class="min-w-0">
                        <div class="text-slate-600 text-[10px] uppercase tracking-widest font-mono">LinkedIn</div>
                        <div class="text-slate-300 text-sm font-light truncate group-hover:text-blue-400 transition-colors">suman-seth-b05417324</div>
                    </div>
                </a>

                <a href="https://github.com/Suman18-bit" target="_blank" class="glass rounded-xl p-5 flex items-center gap-4 hover:border-white/10 transition-all group block">
                    <div class="w-10 h-10 rounded-lg bg-white/5 flex items-center justify-center flex-shrink-0 group-hover:bg-white/10 transition-colors">
                        <i data-lucide="github" class="w-4 h-4 text-slate-300"></i>
                    </div>
                    <div class="min-w-0">
                        <div class="text-slate-600 text-[10px] uppercase tracking-widest font-mono">GitHub</div>
                        <div class="text-slate-300 text-sm font-light truncate">Suman18-bit</div>
                    </div>
                </a>

                <div class="glass rounded-xl p-5 flex items-center gap-4">
                    <div class="w-10 h-10 rounded-lg bg-amber-500/10 flex items-center justify-center flex-shrink-0">
                        <i data-lucide="map-pin" class="w-4 h-4 text-amber-400"></i>
                    </div>
                    <div class="min-w-0">
                        <div class="text-slate-600 text-[10px] uppercase tracking-widest font-mono">Location</div>
                        <div class="text-slate-300 text-sm font-light">Nandigram-II, West Bengal</div>
                    </div>
                </div>
            </div>

            <div class="lg:col-span-3 reveal-right">
                <form id="contact-form" class="glass-strong rounded-2xl p-8 border-gradient space-y-5" onsubmit="handleSubmit(event)">
                    <div class="grid sm:grid-cols-2 gap-5">
                        <div>
                            <label class="text-slate-600 text-[10px] uppercase tracking-widest font-mono mb-2 block">Name</label>
                            <input type="text" required placeholder="Your name" class="form-input">
                        </div>
                        <div>
                            <label class="text-slate-600 text-[10px] uppercase tracking-widest font-mono mb-2 block">Email</label>
                            <input type="email" required placeholder="you@example.com" class="form-input">
                        </div>
                    </div>
                    <div>
                        <label class="text-slate-600 text-[10px] uppercase tracking-widest font-mono mb-2 block">Subject</label>
                        <input type="text" required placeholder="What's this about?" class="form-input">
                    </div>
                    <div>
                        <label class="text-slate-600 text-[10px] uppercase tracking-widest font-mono mb-2 block">Message</label>
                        <textarea required rows="5" placeholder="Tell me about your project or opportunity..." class="form-input resize-none"></textarea>
                    </div>
                    <button type="submit" class="btn-cta w-full justify-center">
                        <i data-lucide="send" class="w-4 h-4"></i> Send Message
                    </button>
                </form>
            </div>
        </div>
    </div>
</section>

<!-- ==================== FOOTER ==================== -->
<footer class="px-6 lg:px-10 py-12 border-t border-white/[0.03]">
    <div class="max-w-7xl mx-auto">
        <div class="flex flex-col md:flex-row items-center justify-between gap-6">
            <div class="flex items-center gap-3">
                <div class="w-8 h-8 rounded-lg bg-gradient-to-br from-cyan-500/20 to-purple-500/20 border border-white/10 flex items-center justify-center">
                    <span class="text-cyan-400 font-semibold text-[10px] font-mono">SS</span>
                </div>
                <div>
                    <span class="text-slate-500 text-xs font-light">© 2025 Suman Seth</span>
                    <span class="text-slate-700 text-xs font-light mx-2">·</span>
                    <span class="text-slate-600 text-xs font-light">Crafted with precision</span>
                </div>
            </div>
            <div class="flex items-center gap-5">
                <a href="https://github.com/Suman18-bit" target="_blank" class="text-slate-600 hover:text-white transition-colors"><i data-lucide="github" class="w-4 h-4"></i></a>
                <a href="https://www.linkedin.com/in/suman-seth-b05417324/" target="_blank" class="text-slate-600 hover:text-white transition-colors"><i data-lucide="linkedin" class="w-4 h-4"></i></a>
                <a href="mailto:sethn533@gmail.com" class="text-slate-600 hover:text-white transition-colors"><i data-lucide="mail" class="w-4 h-4"></i></a>
                <span class="text-slate-700 text-xs font-mono hidden sm:inline">v2.0</span>
            </div>
        </div>
    </div>
</footer>

<!-- Toast -->
<div id="toast" class="toast-notification glass-strong border border-emerald-500/20">
    <div class="flex items-center gap-3">
        <i data-lucide="check-circle-2" class="w-4 h-4 text-emerald-400"></i>
        <span class="text-sm font-light text-slate-200">Message sent! I'll get back to you soon.</span>
    </div>
</div>

<!-- Back to Top -->
<button id="back-to-top" onclick="window.scrollTo({top:0,behavior:'smooth'})"
    class="fixed bottom-8 right-8 w-11 h-11 rounded-xl glass flex items-center justify-center text-slate-500 hover:text-white hover:border-white/10 transition-all z-40 opacity-0 pointer-events-none"
    style="transition: opacity 0.4s, transform 0.4s;">
    <i data-lucide="arrow-up" class="w-4 h-4"></i>
</button>


<script>
// ==================== CUSTOM CURSOR ====================
const dot = document.getElementById('cursor-dot');
const ring = document.getElementById('cursor-ring');
let cx = 0, cy = 0, rx = 0, ry = 0;

document.addEventListener('mousemove', e => {
    cx = e.clientX; cy = e.clientY;
    dot.style.left = cx - 4 + 'px';
    dot.style.top = cy - 4 + 'px';
});

function animateRing() {
    rx += (cx - rx) * 0.15;
    ry += (cy - ry) * 0.15;
    ring.style.left = rx - 20 + 'px';
    ring.style.top = ry - 20 + 'px';
    requestAnimationFrame(animateRing);
}
animateRing();

document.querySelectorAll('a, button, .card, .cert-item, .tag, input, textarea').forEach(el => {
    el.addEventListener('mouseenter', () => ring.classList.add('hover'));
    el.addEventListener('mouseleave', () => ring.classList.remove('hover'));
});

// ==================== SCROLL PROGRESS ====================
const scrollBar = document.getElementById('scroll-progress');
window.addEventListener('scroll', () => {
    const h = document.documentElement;
    const pct = (h.scrollTop / (h.scrollHeight - h.clientHeight)) * 100;
    scrollBar.style.width = pct + '%';
});

// ==================== THREE.JS ====================
(function() {
    const canvas = document.getElementById('three-canvas');
    const renderer = new THREE.WebGLRenderer({ canvas, antialias: true, alpha: true });
    renderer.setSize(window.innerWidth, window.innerHeight);
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

    const scene = new THREE.Scene();
    scene.fog = new THREE.FogExp2(0x030712, 0.0018);

    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    camera.position.set(0, 12, 35);
    camera.rotation.x = -0.2;

    // Sphere of particles
    const sphereCount = 2000;
    const sphereGeo = new THREE.BufferGeometry();
    const sPos = new Float32Array(sphereCount * 3);
    const sColors = new Float32Array(sphereCount * 3);
    for (let i = 0; i < sphereCount; i++) {
        const theta = Math.random() * Math.PI * 2;
        const phi = Math.acos(2 * Math.random() - 1);
        const r = 20 + Math.random() * 5;
        sPos[i*3] = r * Math.sin(phi) * Math.cos(theta);
        sPos[i*3+1] = r * Math.sin(phi) * Math.sin(theta);
        sPos[i*3+2] = r * Math.cos(phi);
        const t = Math.random();
        sColors[i*3] = t < 0.5 ? 0.13 : 0.55;
        sColors[i*3+1] = t < 0.5 ? 0.83 : 0.36;
        sColors[i*3+2] = t < 0.5 ? 0.93 : 0.96;
    }
    sphereGeo.setAttribute('position', new THREE.BufferAttribute(sPos, 3));
    sphereGeo.setAttribute('color', new THREE.BufferAttribute(sColors, 3));
    const sphereMat = new THREE.PointsMaterial({
        size: 0.08, vertexColors: true, transparent: true, opacity: 0.6,
        blending: THREE.AdditiveBlending, depthWrite: false
    });
    const sphere = new THREE.Points(sphereGeo, sphereMat);
    scene.add(sphere);

    // Terrain
    const tCount = 2500;
    const tGeo = new THREE.BufferGeometry();
    const tPos = new Float32Array(tCount * 3);
    for (let i = 0; i < tCount; i++) {
        tPos[i*3] = (Math.random() - 0.5) * 100;
        tPos[i*3+1] = 0;
        tPos[i*3+2] = (Math.random() - 0.5) * 100;
    }
    tGeo.setAttribute('position', new THREE.BufferAttribute(tPos, 3));
    const tMat = new THREE.PointsMaterial({
        size: 0.12, color: 0x22d3ee, transparent: true, opacity: 0.5,
        blending: THREE.AdditiveBlending, depthWrite: false
    });
    const terrain = new THREE.Points(tGeo, tMat);
    scene.add(terrain);

    // Dust
    const dCount = 400;
    const dGeo = new THREE.BufferGeometry();
    const dPos = new Float32Array(dCount * 3);
    for (let i = 0; i < dCount; i++) {
        dPos[i*3] = (Math.random() - 0.5) * 60;
        dPos[i*3+1] = Math.random() * 30;
        dPos[i*3+2] = (Math.random() - 0.5) * 60;
    }
    dGeo.setAttribute('position', new THREE.BufferAttribute(dPos, 3));
    const dMat = new THREE.PointsMaterial({
        size: 0.04, color: 0xffffff, transparent: true, opacity: 0.3,
        blending: THREE.AdditiveBlending, depthWrite: false
    });
    const dust = new THREE.Points(dGeo, dMat);
    scene.add(dust);

    let mx = 0, my = 0;
    document.addEventListener('mousemove', e => {
        mx = (e.clientX / window.innerWidth - 0.5) * 2;
        my = (e.clientY / window.innerHeight - 0.5) * 2;
    });

    function animate() {
        requestAnimationFrame(animate);
        const t = performance.now() * 0.001;

        // Rotate sphere
        sphere.rotation.y += 0.0003;
        sphere.rotation.x = Math.sin(t * 0.1) * 0.1;

        // Terrain waves
        const tp = tGeo.attributes.position.array;
        for (let i = 0; i < tCount; i++) {
            const x = tp[i*3], z = tp[i*3+2];
            tp[i*3+1] = Math.sin(x*0.08 + t*0.4)*1.5 + Math.sin(z*0.04 + t*0.25)*1.5;
        }
        tGeo.attributes.position.needsUpdate = true;

        dust.rotation.y -= 0.00015;

        camera.position.x += (mx * 3 - camera.position.x) * 0.005;
        camera.position.y += (-my * 2 + 12 - camera.position.y) * 0.005;

        renderer.render(scene, camera);
    }
    animate();

    window.addEventListener('resize', () => {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
    });
})();

// ==================== LUCIDE ====================
lucide.createIcons();

// ==================== TYPING EFFECT ====================
const phrases = [
    "B.Tech CSE Student",
    "Software Engineer",
    "Data Scientist",
    "ML Engineer",
    "NLP Enthusiast",
    "Deep Learning Practitioner"
];
let phraseIdx = 0, charIdx = 0, deleting = false;
const typedEl = document.getElementById('typed-text');

function typeLoop() {
    const current = phrases[phraseIdx];
    if (!deleting) {
        typedEl.textContent = current.substring(0, charIdx + 1);
        charIdx++;
        if (charIdx === current.length) {
            setTimeout(() => { deleting = true; typeLoop(); }, 2200);
            return;
        }
        setTimeout(typeLoop, 60 + Math.random() * 40);
    } else {
        typedEl.textContent = current.substring(0, charIdx - 1);
        charIdx--;
        if (charIdx === 0) {
            deleting = false;
            phraseIdx = (phraseIdx + 1) % phrases.length;
            setTimeout(typeLoop, 400);
            return;
        }
        setTimeout(typeLoop, 30);
    }
}
setTimeout(typeLoop, 1200);

// ==================== SCROLL REVEAL ====================
const revealObs = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
}, { threshold: 0.08, rootMargin: '0px 0px -40px 0px' });

document.querySelectorAll('.reveal, .reveal-left, .reveal-right, .reveal-scale').forEach(el => revealObs.observe(el));

// ==================== SKILL BARS ====================
const barObs = new IntersectionObserver((entries) => {
    entries.forEach(e => {
        if (e.isIntersecting) {
            e.target.classList.add('animate');
            barObs.unobserve(e.target);
        }
    });
}, { threshold: 0.5 });
document.querySelectorAll('.skill-bar-fill').forEach(el => barObs.observe(el));

// ==================== NAV ACTIVE ====================
const sections = document.querySelectorAll('section[id]');
const navLinks = document.querySelectorAll('.nav-link[data-section]');
const navObs = new IntersectionObserver((entries) => {
    entries.forEach(e => {
        if (e.isIntersecting) {
            navLinks.forEach(l => l.classList.remove('active'));
            const a = document.querySelector(`.nav-link[data-section="${e.target.id}"]`);
            if (a) a.classList.add('active');
        }
    });
}, { threshold: 0.25 });
sections.forEach(s => navObs.observe(s));

// ==================== MOBILE MENU ====================
const mToggle = document.getElementById('mobile-toggle');
const mOverlay = document.getElementById('mobile-overlay');
let mOpen = false;
mToggle.addEventListener('click', () => {
    mOpen = !mOpen;
    mOverlay.classList.toggle('open', mOpen);
    document.body.style.overflow = mOpen ? 'hidden' : '';
});
function closeMobile() {
    mOpen = false;
    mOverlay.classList.remove('open');
    document.body.style.overflow = '';
}

// ==================== CERT TOGGLE ====================
let certsOpen = false;
function toggleCerts() {
    certsOpen = !certsOpen;
    document.querySelectorAll('.cert-hidden').forEach(el => {
        el.style.display = certsOpen ? 'flex' : 'none';
    });
    document.getElementById('cert-btn-text').textContent = certsOpen ? 'Show Less' : 'Show All 17';
    const icon = document.getElementById('cert-icon');
    icon.style.transform = certsOpen ? 'rotate(180deg)' : 'rotate(0deg)';
    icon.style.transition = 'transform 0.3s';
    if (certsOpen) {
        document.querySelectorAll('.cert-hidden').forEach(el => {
            el.style.opacity = '0'; el.style.transform = 'translateY(10px)';
            requestAnimationFrame(() => {
                el.style.transition = 'opacity 0.4s, transform 0.4s';
                el.style.opacity = '1'; el.style.transform = 'translateY(0)';
            });
        });
    }
}

// ==================== STAT COUNTERS ====================
const statObs = new IntersectionObserver((entries) => {
    entries.forEach(e => {
        if (e.isIntersecting) {
            const el = e.target;
            const target = parseInt(el.dataset.count);
            let cur = 0;
            const dur = 1400;
            const step = target / (dur / 16);
            const iv = setInterval(() => {
                cur += step;
                if (cur >= target) { cur = target; clearInterval(iv); }
                el.textContent = Math.floor(cur);
            }, 16);
            statObs.unobserve(el);
        }
    });
}, { threshold: 0.5 });
document.querySelectorAll('[data-count]').forEach(el => statObs.observe(el));

// ==================== CARD MOUSE GLOW ====================
document.querySelectorAll('.card').forEach(card => {
    card.addEventListener('mousemove', e => {
        const rect = card.getBoundingClientRect();
        card.style.setProperty('--mouse-x', (e.clientX - rect.left) + 'px');
        card.style.setProperty('--mouse-y', (e.clientY - rect.top) + 'px');
    });
});

// ==================== CONTACT FORM ====================
function handleSubmit(e) {
    e.preventDefault();
    const toast = document.getElementById('toast');
    toast.classList.add('show');
    e.target.reset();
    setTimeout(() => toast.classList.remove('show'), 4000);
}

// ==================== BACK TO TOP ====================
const btt = document.getElementById('back-to-top');
window.addEventListener('scroll', () => {
    if (window.scrollY > 500) {
        btt.style.opacity = '1';
        btt.style.pointerEvents = 'auto';
        btt.style.transform = 'translateY(0)';
    } else {
        btt.style.opacity = '0';
        btt.style.pointerEvents = 'none';
        btt.style.transform = 'translateY(10px)';
    }
});

// ==================== NAV HIDE/SHOW ON SCROLL ====================
let lastScroll = 0;
const nav = document.querySelector('nav');
window.addEventListener('scroll', () => {
    const curr = window.scrollY;
    if (curr > lastScroll && curr > 200) {
        nav.style.transform = 'translateY(-100%)';
        nav.style.transition = 'transform 0.35s ease';
    } else {
        nav.style.transform = 'translateY(0)';
    }
    lastScroll = curr;
});
</script>

</body>
</html>
