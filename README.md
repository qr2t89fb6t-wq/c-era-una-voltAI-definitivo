<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>C'era una voltAI</title>
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Epilogue:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --c1: #ff6b35;   /* arancione */
      --c2: #ffd23f;   /* giallo */
      --c3: #06d6a0;   /* verde */
      --c4: #118ab2;   /* blu */
      --c5: #ef476f;   /* rosa */
      --bg: #f5f0e8;
      --dark: #1a1a2e;
      --text: #1a1a2e;
      --muted: #6b6b8a;
      --white: #ffffff;
      --card-bg: #ffffff;
      --radius: 20px;
    }

    html { scroll-behavior: smooth; }
    body {
      font-family: 'Epilogue', sans-serif;
      background: var(--bg);
      color: var(--text);
      overflow-x: hidden;
    }

    /* ═══════════════════════════════
       NAVBAR
    ═══════════════════════════════ */
    nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 500;
      display: flex; align-items: center; gap: 0;
      padding: 0 40px;
      height: 64px;
      background: var(--dark);
      border-bottom: 3px solid var(--c1);
    }

    .nav-logo {
      font-family: 'Syne', sans-serif;
      font-weight: 800; font-size: 20px;
      color: var(--white);
      text-decoration: none;
      letter-spacing: -0.5px;
      cursor: pointer;
    }
    .nav-logo span { color: var(--c2); }

    .nav-links {
      display: flex; gap: 4px; margin-left: auto; align-items: center;
    }
    .nav-link {
      padding: 8px 16px; border-radius: 8px;
      font-family: 'Syne', sans-serif; font-size: 13px; font-weight: 600;
      color: #ccc; cursor: pointer; border: none; background: none;
      transition: color 0.2s, background 0.2s;
      letter-spacing: 0.02em;
    }
    .nav-link:hover, .nav-link.active { color: var(--white); background: rgba(255,255,255,0.08); }
    .nav-link.active { color: var(--c2); }

    .nav-cta {
      margin-left: 12px; padding: 9px 20px;
      background: var(--c1); color: var(--white);
      border: none; border-radius: 100px;
      font-family: 'Syne', sans-serif; font-size: 13px; font-weight: 700;
      cursor: pointer; transition: background 0.2s, transform 0.15s;
    }
    .nav-cta:hover { background: var(--c5); transform: scale(1.04); }

    /* ═══════════════════════════════
       PAGES
    ═══════════════════════════════ */
    .page { display: none; padding-top: 64px; min-height: 100vh; }
    .page.active { display: block; }

    /* ═══════════════════════════════
       HOME
    ═══════════════════════════════ */

    /* Hero */
    .hero {
      position: relative; overflow: hidden;
      min-height: calc(100vh - 64px);
      background: var(--dark);
      display: flex; align-items: center;
    }

    .hero-blobs {
      position: absolute; inset: 0; pointer-events: none;
    }
    .blob {
      position: absolute; border-radius: 50%;
      filter: blur(80px); opacity: 0.35;
      animation: blobMove 8s ease-in-out infinite alternate;
    }
    .blob-1 { width: 500px; height: 500px; background: var(--c1); top: -100px; left: -100px; animation-delay: 0s; }
    .blob-2 { width: 400px; height: 400px; background: var(--c4); bottom: -50px; right: 200px; animation-delay: 2s; }
    .blob-3 { width: 350px; height: 350px; background: var(--c5); top: 50%; right: -80px; animation-delay: 4s; }
    .blob-4 { width: 280px; height: 280px; background: var(--c3); bottom: 50px; left: 300px; animation-delay: 1s; }
    @keyframes blobMove {
      from { transform: translate(0,0) scale(1); }
      to   { transform: translate(30px, 20px) scale(1.1); }
    }

    .hero-content {
      position: relative; z-index: 2;
      max-width: 1100px; margin: 0 auto; padding: 80px 40px;
      display: grid; grid-template-columns: 1fr 1fr; gap: 60px; align-items: center;
    }

    .hero-tag {
      display: inline-flex; align-items: center; gap: 8px;
      background: rgba(255,255,255,0.1); border: 1px solid rgba(255,255,255,0.2);
      border-radius: 100px; padding: 6px 14px; margin-bottom: 24px;
      font-size: 12px; color: var(--c2); font-weight: 500; letter-spacing: 0.08em;
      text-transform: uppercase;
    }
    .hero-tag::before { content:''; width:6px; height:6px; border-radius:50%; background:var(--c3); animation: pulse 2s infinite; }
    @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.4} }

    .hero h1 {
      font-family: 'Syne', sans-serif; font-weight: 800;
      font-size: clamp(40px, 5vw, 68px); line-height: 1.05;
      color: var(--white); letter-spacing: -1px;
      margin-bottom: 24px;
    }
    .hero h1 em { font-style: normal; color: var(--c2); }
    .hero h1 .stroke {
      -webkit-text-stroke: 2px var(--c1);
      color: transparent;
    }

    .hero-desc {
      font-size: 18px; line-height: 1.7; color: #b0b0c8;
      margin-bottom: 36px; font-weight: 300;
    }

    .hero-btns { display: flex; gap: 14px; flex-wrap: wrap; }

    .btn-primary {
      padding: 14px 28px; border-radius: 100px;
      background: var(--c1); color: var(--white);
      font-family: 'Syne', sans-serif; font-size: 15px; font-weight: 700;
      border: none; cursor: pointer;
      transition: transform 0.2s, box-shadow 0.2s;
      box-shadow: 0 4px 20px rgba(255,107,53,0.4);
    }
    .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 30px rgba(255,107,53,0.5); }

    .btn-outline {
      padding: 14px 28px; border-radius: 100px;
      border: 2px solid rgba(255,255,255,0.3); color: var(--white);
      background: none; font-family: 'Syne', sans-serif; font-size: 15px; font-weight: 600;
      cursor: pointer; transition: border-color 0.2s, background 0.2s;
    }
    .btn-outline:hover { border-color: var(--c2); background: rgba(255,210,63,0.1); }

    /* Hero visual */
    .hero-visual {
      display: flex; justify-content: center; align-items: center;
    }
    .hero-card-stack {
      position: relative; width: 340px; height: 380px;
    }
    .hcard {
      position: absolute; border-radius: 24px; padding: 28px;
      font-family: 'Syne', sans-serif;
      box-shadow: 0 20px 60px rgba(0,0,0,0.4);
      transition: transform 0.3s;
    }
    .hcard:hover { transform: translateY(-6px) !important; }
    .hcard-1 {
      width: 240px; background: var(--c1); color: var(--white);
      top: 0; left: 0; transform: rotate(-4deg);
      animation: float1 4s ease-in-out infinite;
    }
    .hcard-2 {
      width: 220px; background: var(--c2); color: var(--dark);
      top: 80px; right: 0; transform: rotate(3deg);
      animation: float2 4s ease-in-out infinite;
    }
    .hcard-3 {
      width: 200px; background: var(--c3); color: var(--dark);
      bottom: 20px; left: 40px; transform: rotate(-2deg);
      animation: float3 4s ease-in-out infinite;
    }
    @keyframes float1 { 0%,100%{transform:rotate(-4deg) translateY(0)} 50%{transform:rotate(-4deg) translateY(-10px)} }
    @keyframes float2 { 0%,100%{transform:rotate(3deg) translateY(0)} 50%{transform:rotate(3deg) translateY(-14px)} }
    @keyframes float3 { 0%,100%{transform:rotate(-2deg) translateY(0)} 50%{transform:rotate(-2deg) translateY(-8px)} }
    .hcard-icon { font-size: 32px; margin-bottom: 12px; }
    .hcard-title { font-weight: 700; font-size: 15px; margin-bottom: 6px; }
    .hcard-sub { font-size: 12px; opacity: 0.75; font-family: 'Epilogue', sans-serif; }

    /* Stats band */
    .stats-band {
      background: var(--white);
      border-bottom: 3px solid var(--c2);
      display: flex; justify-content: center;
    }
    .stats-inner {
      max-width: 1100px; width: 100%;
      display: grid; grid-template-columns: repeat(4, 1fr);
      padding: 0 40px;
    }
    .stat-item {
      padding: 36px 20px; text-align: center;
      border-right: 1px solid #eee;
    }
    .stat-item:last-child { border-right: none; }
    .stat-num {
      font-family: 'Syne', sans-serif; font-weight: 800; font-size: 42px;
      background: linear-gradient(135deg, var(--c1), var(--c5));
      -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    }
    .stat-label { font-size: 13px; color: var(--muted); margin-top: 4px; font-weight: 500; }

    /* Section base */
    section {
      max-width: 1100px; margin: 0 auto; padding: 100px 40px;
    }

    .section-tag {
      display: inline-flex; align-items: center; gap: 8px;
      background: var(--c2); color: var(--dark);
      border-radius: 100px; padding: 6px 14px; margin-bottom: 16px;
      font-family: 'Syne', sans-serif; font-size: 11px; font-weight: 700;
      letter-spacing: 0.1em; text-transform: uppercase;
    }

    .section-title {
      font-family: 'Syne', sans-serif; font-weight: 800;
      font-size: clamp(28px, 4vw, 46px); line-height: 1.1;
      letter-spacing: -0.5px; margin-bottom: 16px;
    }
    .section-title em { font-style: normal; color: var(--c1); }

    .section-sub {
      font-size: 17px; color: var(--muted); line-height: 1.7;
      max-width: 580px; margin-bottom: 60px;
    }

    /* Feature cards home */
    .features-grid {
      display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px;
    }
    .feat-card {
      background: var(--card-bg); border-radius: var(--radius);
      padding: 32px; border: 2px solid transparent;
      transition: transform 0.2s, border-color 0.2s, box-shadow 0.2s;
      position: relative; overflow: hidden;
    }
    .feat-card::before {
      content: ''; position: absolute; inset: 0; opacity: 0;
      transition: opacity 0.3s;
    }
    .feat-card:hover { transform: translateY(-6px); box-shadow: 0 20px 50px rgba(0,0,0,0.1); }
    .feat-card:hover::before { opacity: 1; }

    .feat-card.c1 { border-color: var(--c1); }
    .feat-card.c2 { border-color: var(--c2); }
    .feat-card.c3 { border-color: var(--c3); }
    .feat-card.c4 { border-color: var(--c4); }
    .feat-card.c5 { border-color: var(--c5); }

    .feat-icon {
      width: 52px; height: 52px; border-radius: 14px;
      display: flex; align-items: center; justify-content: center;
      font-size: 24px; margin-bottom: 20px;
    }
    .c1 .feat-icon { background: #fff0eb; }
    .c2 .feat-icon { background: #fffbe8; }
    .c3 .feat-icon { background: #e8faf5; }
    .c4 .feat-icon { background: #e8f4fa; }
    .c5 .feat-icon { background: #fde8ee; }

    .feat-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 18px; margin-bottom: 10px; }
    .feat-desc  { font-size: 14px; color: var(--muted); line-height: 1.7; }

    /* CTA band */
    .cta-band {
      background: var(--dark); padding: 80px 40px;
      text-align: center;
    }
    .cta-band h2 {
      font-family: 'Syne', sans-serif; font-weight: 800;
      font-size: clamp(28px, 4vw, 48px); color: var(--white);
      margin-bottom: 16px;
    }
    .cta-band h2 span { color: var(--c2); }
    .cta-band p { font-size: 16px; color: #aaa; margin-bottom: 36px; }

    /* ═══════════════════════════════
       CHI SIAMO
    ═══════════════════════════════ */
    .about-hero {
      background: linear-gradient(135deg, var(--c4) 0%, var(--dark) 60%);
      padding: 100px 40px 80px; text-align: center;
    }
    .about-hero h1 {
      font-family: 'Syne', sans-serif; font-weight: 800;
      font-size: clamp(36px, 5vw, 64px); color: var(--white);
      margin-bottom: 20px; letter-spacing: -1px;
    }
    .about-hero h1 span { color: var(--c2); }
    .about-hero p { font-size: 18px; color: rgba(255,255,255,0.75); max-width: 600px; margin: 0 auto; line-height: 1.7; }

    .mission-grid {
      display: grid; grid-template-columns: 1fr 1fr; gap: 60px; align-items: center;
    }
    .mission-text h2 {
      font-family: 'Syne', sans-serif; font-weight: 800;
      font-size: 36px; margin-bottom: 20px; line-height: 1.2;
    }
    .mission-text h2 em { font-style: normal; color: var(--c4); }
    .mission-text p { font-size: 16px; color: var(--muted); line-height: 1.8; margin-bottom: 16px; }

    .mission-visual {
      display: flex; flex-direction: column; gap: 16px;
    }
    .value-pill {
      display: flex; align-items: center; gap: 16px;
      background: var(--white); border-radius: 16px; padding: 20px 24px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.06);
      transition: transform 0.2s;
    }
    .value-pill:hover { transform: translateX(8px); }
    .value-pill-icon {
      width: 44px; height: 44px; border-radius: 12px;
      display: flex; align-items: center; justify-content: center;
      font-size: 20px; flex-shrink: 0;
    }
    .value-pill-text h4 { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 15px; margin-bottom: 3px; }
    .value-pill-text p  { font-size: 13px; color: var(--muted); }

    .team-grid {
      display: grid; grid-template-columns: repeat(3, 1fr); gap: 28px; margin-top: 60px;
    }
    .team-card {
      background: var(--white); border-radius: var(--radius);
      padding: 32px; text-align: center;
      box-shadow: 0 4px 20px rgba(0,0,0,0.06);
      transition: transform 0.2s;
    }
    .team-card:hover { transform: translateY(-6px); }
    .team-avatar {
      width: 80px; height: 80px; border-radius: 50%;
      margin: 0 auto 16px;
      display: flex; align-items: center; justify-content: center;
      font-size: 32px; font-weight: 800;
      font-family: 'Syne', sans-serif;
    }
    .team-name { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 17px; margin-bottom: 4px; }
    .team-role { font-size: 13px; color: var(--muted); }

    /* ═══════════════════════════════
       SERVIZI
    ═══════════════════════════════ */
    .services-hero {
      background: linear-gradient(135deg, var(--c5) 0%, var(--c1) 50%, var(--c2) 100%);
      padding: 100px 40px 80px; text-align: center;
    }
    .services-hero h1 {
      font-family: 'Syne', sans-serif; font-weight: 800;
      font-size: clamp(36px, 5vw, 64px); color: var(--white); margin-bottom: 20px;
    }
    .services-hero p { font-size: 18px; color: rgba(255,255,255,0.85); max-width: 580px; margin: 0 auto; }

    .service-block {
      display: grid; grid-template-columns: 1fr 1fr; gap: 60px;
      align-items: center; padding: 80px 40px;
      max-width: 1100px; margin: 0 auto;
      border-bottom: 1px solid #e8e8e8;
    }
    .service-block:last-of-type { border-bottom: none; }
    .service-block.reverse { direction: rtl; }
    .service-block.reverse > * { direction: ltr; }

    .service-num {
      font-family: 'Syne', sans-serif; font-weight: 800; font-size: 80px;
      line-height: 1; margin-bottom: 10px; opacity: 0.12;
    }
    .service-info .tag {
      display: inline-block; padding: 5px 12px; border-radius: 100px;
      font-family: 'Syne', sans-serif; font-size: 11px; font-weight: 700;
      letter-spacing: 0.08em; text-transform: uppercase; margin-bottom: 16px;
    }
    .service-info h3 {
      font-family: 'Syne', sans-serif; font-weight: 800; font-size: 28px;
      margin-bottom: 16px; line-height: 1.2;
    }
    .service-info p { font-size: 15px; color: var(--muted); line-height: 1.8; }

    .service-visual {
      border-radius: 24px; overflow: hidden;
      display: flex; align-items: center; justify-content: center;
      min-height: 280px; position: relative;
    }
    .service-visual-inner {
      width: 100%; height: 280px; border-radius: 24px;
      display: flex; align-items: center; justify-content: center;
      font-size: 80px; position: relative; overflow: hidden;
    }
    .sv-pattern {
      position: absolute; inset: 0; opacity: 0.15;
      background-image: radial-gradient(circle, currentColor 1px, transparent 1px);
      background-size: 24px 24px;
    }

    /* ═══════════════════════════════
       CONTATTI / CHATBOT PAGE
    ═══════════════════════════════ */
    .contact-hero {
      background: linear-gradient(135deg, var(--c3) 0%, var(--c4) 100%);
      padding: 80px 40px 60px; text-align: center;
    }
    .contact-hero h1 {
      font-family: 'Syne', sans-serif; font-weight: 800;
      font-size: clamp(32px, 5vw, 56px); color: var(--white); margin-bottom: 16px;
    }
    .contact-hero p { font-size: 17px; color: rgba(255,255,255,0.85); max-width: 560px; margin: 0 auto; }

    .contact-layout {
      display: grid; grid-template-columns: 1fr 2fr; gap: 40px;
      max-width: 1100px; margin: 0 auto; padding: 60px 40px 80px;
    }

    .contact-info h3 {
      font-family: 'Syne', sans-serif; font-weight: 700; font-size: 20px; margin-bottom: 24px;
    }
    .info-item {
      display: flex; align-items: flex-start; gap: 14px; margin-bottom: 20px;
    }
    .info-icon {
      width: 40px; height: 40px; border-radius: 12px; flex-shrink: 0;
      display: flex; align-items: center; justify-content: center; font-size: 18px;
    }
    .info-item h4 { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 14px; margin-bottom: 3px; }
    .info-item p  { font-size: 13px; color: var(--muted); }

    /* ═══════════════════════════════
       EMBEDDED CHATBOT
    ═══════════════════════════════ */
    .chatbot-wrapper {
      background: var(--white); border-radius: 24px;
      overflow: hidden; box-shadow: 0 20px 60px rgba(0,0,0,0.12);
      border: 2px solid var(--c3);
      display: flex; flex-direction: column; height: 580px;
    }

    .chat-header {
      background: var(--dark); padding: 16px 22px;
      display: flex; align-items: center; gap: 12px;
      border-bottom: 3px solid var(--c3);
    }
    .chat-logo {
      width: 34px; height: 34px; border-radius: 10px;
      background: var(--c3); display: flex; align-items: center; justify-content: center;
      font-family: 'Syne', sans-serif; font-weight: 800; font-size: 14px; color: var(--dark);
    }
    .chat-header-title { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 15px; color: #fff; }
    .chat-header-sub   { font-size: 11px; color: #aaa; margin-top: 1px; }

    .chat-mode-toggle {
      margin-left: auto; display: flex;
      background: rgba(255,255,255,0.08); border-radius: 100px; padding: 3px; gap: 2px;
    }
    .chat-mode-btn {
      padding: 5px 12px; border: none; border-radius: 100px;
      font-family: 'Syne', sans-serif; font-size: 11px; font-weight: 600;
      cursor: pointer; transition: all 0.2s; background: transparent; color: #aaa;
      display: flex; align-items: center; gap: 5px;
    }
    .chat-mode-btn.active { background: var(--c3); color: var(--dark); }
    .chat-mode-btn svg { width: 11px; height: 11px; fill: currentColor; }

    .chat-messages {
      flex: 1; overflow-y: auto; padding: 20px;
      display: flex; flex-direction: column; gap: 16px;
      background: #f9f7f3;
      scrollbar-width: thin; scrollbar-color: #ddd transparent;
    }
    .chat-messages::-webkit-scrollbar { width: 3px; }
    .chat-messages::-webkit-scrollbar-thumb { background: #ddd; }

    .chat-intro {
      background: var(--white); border-radius: 16px; padding: 20px;
      border: 2px solid var(--c3);
    }
    .chat-intro p { font-size: 14px; color: var(--muted); line-height: 1.65; margin-bottom: 12px; }
    .chat-chips { display: flex; gap: 7px; flex-wrap: wrap; }
    .chat-chip {
      background: #f0fdf8; border: 1.5px solid var(--c3);
      border-radius: 100px; padding: 5px 12px;
      font-size: 11px; color: #0d8a6a; cursor: pointer;
      transition: background 0.2s; font-weight: 500;
    }
    .chat-chip:hover { background: #d4f5ec; }

    .cmsg { display: flex; gap: 8px; }
    .cmsg.user { flex-direction: row-reverse; }

    .cmsg-avatar {
      width: 28px; height: 28px; border-radius: 8px; flex-shrink: 0; margin-top: 14px;
      display: flex; align-items: center; justify-content: center; font-size: 12px;
    }
    .cmsg-avatar.ai   { background: var(--c3); color: var(--dark); font-family: 'Syne', sans-serif; font-weight: 800; }
    .cmsg-avatar.user { background: var(--dark); color: #fff; }

    .cmsg-inner { display: flex; flex-direction: column; max-width: 75%; }
    .cmsg-label { font-size: 10px; color: var(--muted); margin-bottom: 4px; font-weight: 600; letter-spacing: 0.06em; text-transform: uppercase; }

    .cmsg-bubble {
      padding: 10px 14px; border-radius: 14px; font-size: 13.5px; line-height: 1.65;
    }
    .cmsg.ai   .cmsg-bubble { background: var(--white); border: 1.5px solid #e0e0e0; border-top-left-radius: 4px; color: var(--text); }
    .cmsg.user .cmsg-bubble { background: var(--dark); color: #fff; border-top-right-radius: 4px; }

    .typing-dots { display:flex; gap:4px; align-items:center; padding: 3px 0; }
    .typing-dots span { width:5px; height:5px; border-radius:50%; background: var(--muted); animation: tdot 1.2s infinite; }
    .typing-dots span:nth-child(2){animation-delay:.2s}
    .typing-dots span:nth-child(3){animation-delay:.4s}
    @keyframes tdot { 0%,80%,100%{transform:translateY(0);opacity:.4} 40%{transform:translateY(-4px);opacity:1} }

    .chat-input-area {
      padding: 12px 16px; background: var(--white);
      border-top: 1.5px solid #eee; display: flex; gap: 8px; align-items: flex-end;
    }
    .chat-textarea {
      flex: 1; background: #f5f5f5; border: none; border-radius: 12px;
      padding: 10px 14px; font-family: 'Epilogue', sans-serif; font-size: 13.5px;
      color: var(--text); resize: none; outline: none; min-height: 42px; max-height: 100px; line-height: 1.5;
    }
    .chat-textarea::placeholder { color: #bbb; }
    .chat-send {
      width: 42px; height: 42px; border-radius: 12px;
      background: var(--c3); border: none; cursor: pointer;
      display: flex; align-items: center; justify-content: center;
      transition: background 0.2s, transform 0.15s; flex-shrink: 0;
    }
    .chat-send:hover { background: #05b888; transform: scale(1.06); }
    .chat-send:disabled { background: #ddd; cursor: not-allowed; transform: none; }
    .chat-send svg { fill: var(--dark); width: 16px; height: 16px; }

    /* ── Maintenance modal ── */
    #maint-modal {
      position: fixed; inset: 0; background: rgba(0,0,0,0.6);
      display: flex; align-items: center; justify-content: center;
      z-index: 999; opacity: 0; pointer-events: none; transition: opacity 0.25s;
    }
    #maint-modal.show { opacity: 1; pointer-events: all; }
    .maint-box {
      background: var(--white); border-radius: 24px; padding: 44px 48px;
      max-width: 400px; width: 90%; text-align: center;
      transform: scale(0.9); transition: transform 0.25s;
      border-top: 6px solid var(--c1);
    }
    #maint-modal.show .maint-box { transform: scale(1); }
    .maint-icon { font-size: 48px; margin-bottom: 16px; }
    .maint-box h3 { font-family: 'Syne', sans-serif; font-weight: 800; font-size: 22px; margin-bottom: 12px; }
    .maint-box p  { font-size: 14px; color: var(--muted); line-height: 1.7; }
    .maint-close {
      margin-top: 24px; padding: 11px 28px; border-radius: 100px;
      background: var(--dark); color: var(--white);
      border: none; font-family: 'Syne', sans-serif; font-size: 13px; font-weight: 700;
      cursor: pointer; transition: background 0.2s;
    }
    .maint-close:hover { background: var(--c1); }

    /* ═══════════════════════════════
       FOOTER
    ═══════════════════════════════ */
    footer {
      background: var(--dark); padding: 60px 40px 30px;
      border-top: 4px solid var(--c1);
    }
    .footer-inner {
      max-width: 1100px; margin: 0 auto;
      display: grid; grid-template-columns: 2fr 1fr 1fr; gap: 40px;
      padding-bottom: 40px; border-bottom: 1px solid rgba(255,255,255,0.1);
    }
    .footer-brand .logo {
      font-family: 'Syne', sans-serif; font-weight: 800; font-size: 22px;
      color: var(--white); margin-bottom: 12px;
    }
    .footer-brand .logo span { color: var(--c2); }
    .footer-brand p { font-size: 13px; color: #777; line-height: 1.7; max-width: 280px; }
    .footer-col h4 { font-family: 'Syne', sans-serif; font-weight: 700; font-size: 13px; color: var(--white); margin-bottom: 16px; letter-spacing: 0.06em; text-transform: uppercase; }
    .footer-col a  { display: block; font-size: 13px; color: #777; margin-bottom: 10px; text-decoration: none; cursor: pointer; transition: color 0.2s; }
    .footer-col a:hover { color: var(--c2); }
    .footer-bottom { max-width: 1100px; margin: 20px auto 0; display: flex; justify-content: space-between; align-items: center; }
    .footer-bottom p { font-size: 12px; color: #555; }
    .footer-dots { display: flex; gap: 8px; }
    .fdot { width: 10px; height: 10px; border-radius: 50%; }

    /* ═══════════════════════════════
       ANIMATIONS
    ═══════════════════════════════ */
    .fadeUp {
      opacity: 0; transform: translateY(30px);
      transition: opacity 0.6s ease, transform 0.6s ease;
    }
    .fadeUp.visible { opacity: 1; transform: translateY(0); }

    /* Responsive */
    @media (max-width: 768px) {
      .hero-content, .mission-grid, .service-block, .contact-layout { grid-template-columns: 1fr; }
      .features-grid, .team-grid { grid-template-columns: 1fr; }
      .stats-inner { grid-template-columns: repeat(2,1fr); }
      .footer-inner { grid-template-columns: 1fr; }
      .service-block.reverse { direction: ltr; }
      .hero-visual { display: none; }
      nav { padding: 0 20px; }
      .nav-links { gap: 2px; }
      .nav-link { padding: 6px 10px; font-size: 12px; }
    }
  </style>
</head>
<body>

<!-- NAVBAR -->
<nav>
  <a class="nav-logo" onclick="showPage('home')">C'era una volt<span>AI</span></a>
  <div class="nav-links">
    <button class="nav-link active" id="nav-home"     onclick="showPage('home')">Home</button>
    <button class="nav-link"        id="nav-about"    onclick="showPage('about')">Chi siamo</button>
    <button class="nav-link"        id="nav-services" onclick="showPage('services')">Servizi</button>
    <button class="nav-link nav-cta"id="nav-contact"  onclick="showPage('contact')">💬 Assistente</button>
  </div>
</nav>

<!-- ══════════════ HOME ══════════════ -->
<div id="page-home" class="page active">

  <!-- Hero -->
  <div class="hero">
    <div class="hero-blobs">
      <div class="blob blob-1"></div>
      <div class="blob blob-2"></div>
      <div class="blob blob-3"></div>
      <div class="blob blob-4"></div>
    </div>
    <div class="hero-content">
      <div>
        <div class="hero-tag">Progetto educativo sull'IA</div>
        <h1>C'era una <em>volt</em><span class="stroke">AI</span></h1>
        <p class="hero-desc">Spieghiamo l'intelligenza artificiale a scuole, aziende e persone di ogni età. Perché capire l'IA non è un lusso — è una necessità.</p>
        <div class="hero-btns">
          <button class="btn-primary" onclick="showPage('services')">Scopri i servizi</button>
          <button class="btn-outline"  onclick="showPage('contact')">Parla con noi</button>
        </div>
      </div>
      <div class="hero-visual">
        <div class="hero-card-stack">
          <div class="hcard hcard-1">
            <div class="hcard-icon">🎓</div>
            <div class="hcard-title">Corsi nelle Scuole</div>
            <div class="hcard-sub">Dalla primaria all'università</div>
          </div>
          <div class="hcard hcard-2">
            <div class="hcard-icon">🏢</div>
            <div class="hcard-title">Formazione Aziendale</div>
            <div class="hcard-sub">Team aggiornati sull'IA</div>
          </div>
          <div class="hcard hcard-3">
            <div class="hcard-icon">🎨</div>
            <div class="hcard-title">Arte & Restauro AI</div>
            <div class="hcard-sub">Cultura e tecnologia insieme</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Stats -->
  <div class="stats-band">
    <div class="stats-inner">
      <div class="stat-item">
        <div class="stat-num">200+</div>
        <div class="stat-label">Scuole raggiunte</div>
      </div>
      <div class="stat-item">
        <div class="stat-num">50+</div>
        <div class="stat-label">Aziende formate</div>
      </div>
      <div class="stat-item">
        <div class="stat-num">10k+</div>
        <div class="stat-label">Persone coinvolte</div>
      </div>
      <div class="stat-item">
        <div class="stat-num">5</div>
        <div class="stat-label">Attività speciali</div>
      </div>
    </div>
  </div>

  <!-- Features -->
  <section>
    <div class="fadeUp">
      <div class="section-tag">Cosa facciamo</div>
      <h2 class="section-title">Tutto quello che <em>offriamo</em></h2>
      <p class="section-sub">Dalla formazione base per i più piccoli fino a progetti avanzati per professionisti e anziani.</p>
    </div>
    <div class="features-grid fadeUp">
      <div class="feat-card c1">
        <div class="feat-icon">🎓</div>
        <div class="feat-title">Corsi Scolastici</div>
        <div class="feat-desc">Percorsi calibrati per ogni età, dall'infanzia all'università, obbligatori e interattivi.</div>
      </div>
      <div class="feat-card c4">
        <div class="feat-icon">🏢</div>
        <div class="feat-title">Formazione Aziendale</div>
        <div class="feat-desc">Aggiorniamo i team aziendali su come l'IA cambia il lavoro e come usarla al meglio.</div>
      </div>
      <div class="feat-card c3">
        <div class="feat-icon">👴</div>
        <div class="feat-title">Assistenza Anziani</div>
        <div class="feat-desc">Supporto dedicato per chi ha difficoltà con le nuove tecnologie: nessuno viene lasciato indietro.</div>
      </div>
      <div class="feat-card c5">
        <div class="feat-icon">🕵️</div>
        <div class="feat-title">Gara AI o Umano?</div>
        <div class="feat-desc">Alleniamo l'occhio critico: riconosci testi e immagini generati dall'IA senza strumenti esterni.</div>
      </div>
      <div class="feat-card c2">
        <div class="feat-icon">🎨</div>
        <div class="feat-title">Arte & Restauro AI</div>
        <div class="feat-desc">Creiamo modelli artistici e restauriamo opere d'arte con l'IA per scopi culturali.</div>
      </div>
      <div class="feat-card c4">
        <div class="feat-icon">🔍</div>
        <div class="feat-title">Rilevamento Immagini AI</div>
        <div class="feat-desc">Sviluppiamo software per riconoscere immagini generate dall'IA tramite metadati codificati.</div>
      </div>
    </div>
  </section>

  <!-- CTA -->
  <div class="cta-band">
    <h2>Hai domande sul progetto? <span>Chiedici!</span></h2>
    <p>Il nostro assistente virtuale è sempre disponibile per risponderti.</p>
    <button class="btn-primary" onclick="showPage('contact')">💬 Apri la chat</button>
  </div>

  <footer>
    <div class="footer-inner">
      <div class="footer-brand">
        <div class="logo">C'era una volt<span>AI</span></div>
        <p>Diffondere la conoscenza sull'intelligenza artificiale, una persona alla volta. Scuole, aziende, anziani: tutti meritano di capire l'IA.</p>
      </div>
      <div class="footer-col">
        <h4>Navigazione</h4>
        <a onclick="showPage('home')">Home</a>
        <a onclick="showPage('about')">Chi siamo</a>
        <a onclick="showPage('services')">Servizi</a>
        <a onclick="showPage('contact')">Contatti</a>
      </div>
      <div class="footer-col">
        <h4>Servizi</h4>
        <a>Corsi scolastici</a>
        <a>Formazione aziendale</a>
        <a>Assistenza anziani</a>
        <a>Gara AI o Umano?</a>
      </div>
    </div>
    <div class="footer-bottom">
      <p>© 2025 C'era una voltAI — Progetto educativo</p>
      <div class="footer-dots">
        <div class="fdot" style="background:var(--c1)"></div>
        <div class="fdot" style="background:var(--c2)"></div>
        <div class="fdot" style="background:var(--c3)"></div>
        <div class="fdot" style="background:var(--c4)"></div>
        <div class="fdot" style="background:var(--c5)"></div>
      </div>
    </div>
  </footer>
</div>

<!-- ══════════════ CHI SIAMO ══════════════ -->
<div id="page-about" class="page">
  <div class="about-hero">
    <h1>Chi <span>siamo</span></h1>
    <p>Un team di appassionati con un obiettivo: rendere l'intelligenza artificiale comprensibile e accessibile a tutti.</p>
  </div>

  <section>
    <div class="mission-grid fadeUp">
      <div class="mission-text">
        <div class="section-tag">La nostra missione</div>
        <h2>L'IA spiegata <em>davvero</em></h2>
        <p>C'era una voltAI nasce dalla convinzione che l'intelligenza artificiale stia cambiando il mondo — e che tutti, dai bambini agli anziani, meritino di capirla davvero, non solo di subirla.</p>
        <p>I nostri collaboratori portano nelle scuole e nelle aziende percorsi formativi concreti: non teoria astratta, ma comprensione reale di come funzionano gli algoritmi, come riconoscere i contenuti falsi e come usare queste tecnologie in modo critico e consapevole.</p>
        <p>Un'attenzione speciale va alle persone anziane o con difficoltà digitali: nessuno deve restare indietro nella rivoluzione dell'IA.</p>
      </div>
      <div class="mission-visual">
        <div class="value-pill">
          <div class="value-pill-icon" style="background:#fff0eb;">🎓</div>
          <div class="value-pill-text">
            <h4>Educazione per tutti</h4>
            <p>Dall'infanzia alla terza età, calibriamo ogni percorso</p>
          </div>
        </div>
        <div class="value-pill">
          <div class="value-pill-icon" style="background:#e8faf5;">🔬</div>
          <div class="value-pill-text">
            <h4>Approccio scientifico</h4>
            <p>Spieghiamo come funzionano davvero gli algoritmi</p>
          </div>
        </div>
        <div class="value-pill">
          <div class="value-pill-icon" style="background:#fde8ee;">🤝</div>
          <div class="value-pill-text">
            <h4>Inclusività</h4>
            <p>Assistenza dedicata a chi ha difficoltà con il digitale</p>
          </div>
        </div>
        <div class="value-pill">
          <div class="value-pill-icon" style="background:#fffbe8;">💡</div>
          <div class="value-pill-text">
            <h4>Pensiero critico</h4>
            <p>Insegniamo a riconoscere e valutare i contenuti AI</p>
          </div>
        </div>
      </div>
    </div>

    <div class="fadeUp" style="margin-top:80px;">
      <div class="section-tag">Il nostro team</div>
      <h2 class="section-title">Le persone <em>dietro</em> il progetto</h2>
    </div>
    <div class="team-grid fadeUp">
      <div class="team-card">
        <div class="team-avatar" style="background:#fff0eb;color:var(--c1);">A</div>
        <div class="team-name">Anna Rossi</div>
        <div class="team-role">Fondatrice & Responsabile Educativo</div>
      </div>
      <div class="team-card">
        <div class="team-avatar" style="background:#e8faf5;color:var(--c3);">M</div>
        <div class="team-name">Marco Bianchi</div>
        <div class="team-role">Responsabile Tecnologia & Ricerca</div>
      </div>
      <div class="team-card">
        <div class="team-avatar" style="background:#fffbe8;color:#b89000);">G</div>
        <div class="team-name">Giulia Ferrari</div>
        <div class="team-role">Coordinatrice Progetti Artistici</div>
      </div>
    </div>
  </section>

  <footer>
    <div class="footer-inner">
      <div class="footer-brand">
        <div class="logo">C'era una volt<span>AI</span></div>
        <p>Diffondere la conoscenza sull'intelligenza artificiale, una persona alla volta.</p>
      </div>
      <div class="footer-col">
        <h4>Navigazione</h4>
        <a onclick="showPage('home')">Home</a>
        <a onclick="showPage('about')">Chi siamo</a>
        <a onclick="showPage('services')">Servizi</a>
        <a onclick="showPage('contact')">Contatti</a>
      </div>
      <div class="footer-col">
        <h4>Servizi</h4>
        <a>Corsi scolastici</a>
        <a>Formazione aziendale</a>
        <a>Assistenza anziani</a>
      </div>
    </div>
    <div class="footer-bottom">
      <p>© 2025 C'era una voltAI — Progetto educativo</p>
      <div class="footer-dots">
        <div class="fdot" style="background:var(--c1)"></div>
        <div class="fdot" style="background:var(--c2)"></div>
        <div class="fdot" style="background:var(--c3)"></div>
      </div>
    </div>
  </footer>
</div>

<!-- ══════════════ SERVIZI ══════════════ -->
<div id="page-services" class="page">
  <div class="services-hero">
    <h1>I nostri Servizi</h1>
    <p>Cinque attività pensate per diffondere la cultura dell'IA in modo pratico, critico e creativo.</p>
  </div>

  <div class="service-block fadeUp">
    <div class="service-info">
      <div class="service-num" style="color:var(--c1)">01</div>
      <div class="tag" style="background:#fff0eb;color:var(--c1);">Formazione</div>
      <h3>Corsi nelle Scuole & Aziende</h3>
      <p>Incontri obbligatori e calibrati in base all'età: dalla scuola primaria fino alle aziende. I più piccoli imparano fin da subito a usare l'IA in modo consapevole e responsabile. I professionisti capiscono come questi strumenti stanno trasformando il loro settore.</p>
    </div>
    <div class="service-visual">
      <div class="service-visual-inner" style="background:linear-gradient(135deg,#fff0eb,#ffd9cc);color:var(--c1);">
        <div class="sv-pattern"></div>
        <span style="position:relative;z-index:1;">🎓</span>
      </div>
    </div>
  </div>

  <div class="service-block reverse fadeUp">
    <div class="service-info">
      <div class="service-num" style="color:var(--c3)">02</div>
      <div class="tag" style="background:#e8faf5;color:#0a6b50;">Assistenza</div>
      <h3>Supporto a Persone Anziane e con Difficoltà</h3>
      <p>L'associazione si occupa di ridurre il divario digitale: assistenza dedicata alle persone anziane o con difficoltà che non riescono a essere autonome con l'IA. Nessuno viene lasciato indietro nella rivoluzione tecnologica.</p>
    </div>
    <div class="service-visual">
      <div class="service-visual-inner" style="background:linear-gradient(135deg,#e8faf5,#b8f0e0);color:var(--c3);">
        <div class="sv-pattern"></div>
        <span style="position:relative;z-index:1;">👴</span>
      </div>
    </div>
  </div>

  <div class="service-block fadeUp">
    <div class="service-info">
      <div class="service-num" style="color:var(--c5)">03</div>
      <div class="tag" style="background:#fde8ee;color:var(--c5);">Competizione</div>
      <h3>Gara "AI o Umano?"</h3>
      <p>Una competizione appassionante: i partecipanti analizzano testi, articoli e immagini e devono stabilire — senza strumenti esterni — quali sono stati creati da un essere umano e quali dall'IA. L'obiettivo è allenare l'occhio critico e la consapevolezza mediatica.</p>
    </div>
    <div class="service-visual">
      <div class="service-visual-inner" style="background:linear-gradient(135deg,#fde8ee,#ffc5d4);color:var(--c5);">
        <div class="sv-pattern"></div>
        <span style="position:relative;z-index:1;">🕵️</span>
      </div>
    </div>
  </div>

  <div class="service-block reverse fadeUp">
    <div class="service-info">
      <div class="service-num" style="color:var(--c2)">04</div>
      <div class="tag" style="background:#fffbe8;color:#8a6e00;">Arte & Cultura</div>
      <h3>Progetto Artistico & Restauro con IA</h3>
      <p>Due attività creative: creiamo modelli artistici per insegnare all'IA nuovi stili grafici; e restauriamo opere d'arte con la ricostruzione tramite IA e stima dei danni, per valorizzare queste tecnologie a scopi culturali e conservativi.</p>
    </div>
    <div class="service-visual">
      <div class="service-visual-inner" style="background:linear-gradient(135deg,#fffbe8,#ffe9a0);color:#8a6e00;">
        <div class="sv-pattern"></div>
        <span style="position:relative;z-index:1;">🎨</span>
      </div>
    </div>
  </div>

  <div class="service-block fadeUp">
    <div class="service-info">
      <div class="service-num" style="color:var(--c4)">05</div>
      <div class="tag" style="background:#e8f4fa;color:var(--c4);">Tecnologia</div>
      <h3>Sistema di Rilevamento Immagini AI</h3>
      <p>Sviluppiamo un software innovativo per riconoscere immagini generate dall'IA: il sistema inserisce codici nei metadati delle immagini generate e li legge con un apposito software di rilevamento, rendendo più trasparente la provenienza dei contenuti visivi.</p>
    </div>
    <div class="service-visual">
      <div class="service-visual-inner" style="background:linear-gradient(135deg,#e8f4fa,#b8dff0);color:var(--c4);">
        <div class="sv-pattern"></div>
        <span style="position:relative;z-index:1;">🔍</span>
      </div>
    </div>
  </div>

  <footer>
    <div class="footer-inner">
      <div class="footer-brand">
        <div class="logo">C'era una volt<span>AI</span></div>
        <p>Diffondere la conoscenza sull'intelligenza artificiale, una persona alla volta.</p>
      </div>
      <div class="footer-col">
        <h4>Navigazione</h4>
        <a onclick="showPage('home')">Home</a>
        <a onclick="showPage('about')">Chi siamo</a>
        <a onclick="showPage('services')">Servizi</a>
        <a onclick="showPage('contact')">Contatti</a>
      </div>
      <div class="footer-col">
        <h4>Servizi</h4>
        <a>Corsi scolastici</a>
        <a>Formazione aziendale</a>
        <a>Assistenza anziani</a>
        <a>Gara AI o Umano?</a>
      </div>
    </div>
    <div class="footer-bottom">
      <p>© 2025 C'era una voltAI — Progetto educativo</p>
      <div class="footer-dots">
        <div class="fdot" style="background:var(--c1)"></div>
        <div class="fdot" style="background:var(--c2)"></div>
        <div class="fdot" style="background:var(--c3)"></div>
      </div>
    </div>
  </footer>
</div>

<!-- ══════════════ CONTATTI / CHAT ══════════════ -->
<div id="page-contact" class="page">
  <div class="contact-hero">
    <h1>Contatti & Assistente</h1>
    <p>Hai domande? Parla con il nostro assistente virtuale oppure contattaci direttamente.</p>
  </div>

  <div class="contact-layout">
    <!-- Info -->
    <div class="contact-info fadeUp">
      <h3>Dove trovarci</h3>
      <div class="info-item">
        <div class="info-icon" style="background:#fff0eb;">📍</div>
        <div>
          <h4>Sede principale</h4>
          <p>Via dell'Innovazione 42<br>Milano, Italia</p>
        </div>
      </div>
      <div class="info-item">
        <div class="info-icon" style="background:#e8faf5;">📧</div>
        <div>
          <h4>Email</h4>
          <p>info@cerauna-voltai.it</p>
        </div>
      </div>
      <div class="info-item">
        <div class="info-icon" style="background:#fffbe8;">📞</div>
        <div>
          <h4>Telefono</h4>
          <p>+39 02 1234 5678</p>
        </div>
      </div>
      <div class="info-item">
        <div class="info-icon" style="background:#fde8ee;">🕐</div>
        <div>
          <h4>Orari</h4>
          <p>Lun–Ven: 9:00–18:00<br>Sab: 10:00–14:00</p>
        </div>
      </div>
    </div>

    <!-- Chatbot -->
    <div class="chatbot-wrapper fadeUp">
      <div class="chat-header">
        <div class="chat-logo">V</div>
        <div>
          <div class="chat-header-title">C'era una voltAI — Assistente</div>
          <div class="chat-header-sub">Risponde alle domande sul progetto</div>
        </div>
        <div class="chat-mode-toggle">
          <button class="chat-mode-btn active" id="btn-ai" onclick="setChatMode('ai')">
            <svg viewBox="0 0 24 24"><path d="M12 2a5 5 0 1 1 0 10A5 5 0 0 1 12 2zm0 12c5.33 0 8 2.67 8 4v2H4v-2c0-1.33 2.67-4 8-4z"/></svg>
            Assistente AI
          </button>
          <button class="chat-mode-btn" id="btn-human" onclick="setChatMode('human')">
            <svg viewBox="0 0 24 24"><path d="M16 11c1.66 0 2.99-1.34 2.99-3S17.66 5 16 5c-1.66 0-3 1.34-3 3s1.34 3 3 3zm-8 0c1.66 0 2.99-1.34 2.99-3S9.66 5 8 5C6.34 5 5 6.34 5 8s1.34 3 3 3zm0 2c-2.33 0-7 1.17-7 3.5V19h14v-2.5c0-2.33-4.67-3.5-7-3.5zm8 0c-.29 0-.62.02-.97.05 1.16.84 1.97 1.97 1.97 3.45V19h6v-2.5c0-2.33-4.67-3.5-7-3.5z"/></svg>
            Persona reale
          </button>
        </div>
      </div>

      <div class="chat-messages" id="chat-msgs">
        <div class="chat-intro">
          <p>Ciao! 👋 Sono l'assistente virtuale di <strong>C'era una voltAI</strong>. Posso risponderti sul progetto, sui nostri servizi, i corsi, le attività speciali e molto altro.</p>
          <div class="chat-chips">
            <div class="chat-chip" onclick="useChip(this)">Di cosa si occupa il progetto?</div>
            <div class="chat-chip" onclick="useChip(this)">Quali attività speciali offrite?</div>
            <div class="chat-chip" onclick="useChip(this)">Come aiutate le persone anziane?</div>
            <div class="chat-chip" onclick="useChip(this)">I corsi sono per tutte le età?</div>
          </div>
        </div>
      </div>

      <div class="chat-input-area">
        <textarea class="chat-textarea" id="chat-input" placeholder="Scrivi un messaggio…" rows="1"></textarea>
        <button class="chat-send" id="chat-send-btn" onclick="sendChatMsg()">
          <svg viewBox="0 0 24 24"><path d="M2.01 21L23 12 2.01 3 2 10l15 2-15 2z"/></svg>
        </button>
      </div>
    </div>
  </div>

  <footer>
    <div class="footer-inner">
      <div class="footer-brand">
        <div class="logo">C'era una volt<span>AI</span></div>
        <p>Diffondere la conoscenza sull'intelligenza artificiale, una persona alla volta.</p>
      </div>
      <div class="footer-col">
        <h4>Navigazione</h4>
        <a onclick="showPage('home')">Home</a>
        <a onclick="showPage('about')">Chi siamo</a>
        <a onclick="showPage('services')">Servizi</a>
        <a onclick="showPage('contact')">Contatti</a>
      </div>
      <div class="footer-col">
        <h4>Contatti</h4>
        <a>info@cerauna-voltai.it</a>
        <a>+39 02 1234 5678</a>
        <a>Milano, Italia</a>
      </div>
    </div>
    <div class="footer-bottom">
      <p>© 2025 C'era una voltAI — Progetto educativo</p>
      <div class="footer-dots">
        <div class="fdot" style="background:var(--c1)"></div>
        <div class="fdot" style="background:var(--c2)"></div>
        <div class="fdot" style="background:var(--c3)"></div>
      </div>
    </div>
  </footer>
</div>

<!-- Maintenance Modal -->
<div id="maint-modal" onclick="closeMaint(event)">
  <div class="maint-box">
    <div class="maint-icon">🔧</div>
    <h3>Servizio in manutenzione</h3>
    <p>Il servizio di chat con una persona reale è momentaneamente in manutenzione.<br><br>Riprova più tardi, oppure continua a chattare con il nostro Assistente AI.</p>
    <button class="maint-close" onclick="closeMaintBtn()">Torna all'Assistente AI</button>
  </div>
</div>

<script>
  /* ── Page routing ── */
  function showPage(name) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.querySelectorAll('.nav-link').forEach(b => b.classList.remove('active'));
    document.getElementById('page-' + name).classList.add('active');
    const nb = document.getElementById('nav-' + name);
    if (nb) nb.classList.add('active');
    window.scrollTo(0, 0);
    observeFadeUps();
  }

  /* ── Scroll animations ── */
  function observeFadeUps() {
    const els = document.querySelectorAll('.fadeUp:not(.visible)');
    const io = new IntersectionObserver((entries) => {
      entries.forEach((e, i) => {
        if (e.isIntersecting) {
          setTimeout(() => e.target.classList.add('visible'), i * 100);
          io.unobserve(e.target);
        }
      });
    }, { threshold: 0.1 });
    els.forEach(el => io.observe(el));
  }
  document.addEventListener('DOMContentLoaded', observeFadeUps);

  /* ── Chat mode ── */
  function setChatMode(mode) {
    if (mode === 'human') {
      document.getElementById('maint-modal').classList.add('show');
      return;
    }
    document.querySelectorAll('.chat-mode-btn').forEach(b => b.classList.remove('active'));
    document.getElementById('btn-' + mode).classList.add('active');
  }

  function closeMaint(e) {
    if (e.target === document.getElementById('maint-modal')) closeMaintBtn();
  }
  function closeMaintBtn() {
    document.getElementById('maint-modal').classList.remove('show');
    document.querySelectorAll('.chat-mode-btn').forEach(b => b.classList.remove('active'));
    document.getElementById('btn-ai').classList.add('active');
  }

  /* ── Chat logic ── */
  const chatInput   = document.getElementById('chat-input');
  const chatMsgs    = document.getElementById('chat-msgs');
  const chatSendBtn = document.getElementById('chat-send-btn');

  chatInput.addEventListener('input', () => {
    chatInput.style.height = 'auto';
    chatInput.style.height = Math.min(chatInput.scrollHeight, 100) + 'px';
  });
  chatInput.addEventListener('keydown', e => {
    if (e.key === 'Enter' && !e.shiftKey) { e.preventDefault(); sendChatMsg(); }
  });

  function useChip(el) {
    chatInput.value = el.textContent;
    chatInput.focus();
  }

  function addChatMsg(role, text) {
    const wrap   = document.createElement('div');
    wrap.className = `cmsg ${role}`;

    const avatar = document.createElement('div');
    const inner  = document.createElement('div');
    inner.className = 'cmsg-inner';

    if (role === 'user') {
      avatar.className = 'cmsg-avatar user';
      avatar.textContent = '✦';
    } else {
      avatar.className = 'cmsg-avatar ai';
      avatar.textContent = 'V';
      const lbl = document.createElement('div');
      lbl.className = 'cmsg-label';
      lbl.textContent = 'Assistente AI';
      inner.appendChild(lbl);
    }

    const bubble = document.createElement('div');
    bubble.className = 'cmsg-bubble';
    bubble.textContent = text;
    inner.appendChild(bubble);

    if (role === 'user') { wrap.appendChild(inner); wrap.appendChild(avatar); }
    else                 { wrap.appendChild(avatar); wrap.appendChild(inner); }

    chatMsgs.appendChild(wrap);
    chatMsgs.scrollTop = chatMsgs.scrollHeight;
  }

  function addTyping() {
    const wrap = document.createElement('div');
    wrap.className = 'cmsg ai'; wrap.id = 'chat-typing';
    const avatar = document.createElement('div');
    avatar.className = 'cmsg-avatar ai'; avatar.textContent = 'V';
    const bubble = document.createElement('div');
    bubble.className = 'cmsg-bubble';
    bubble.innerHTML = '<div class="typing-dots"><span></span><span></span><span></span></div>';
    wrap.appendChild(avatar); wrap.appendChild(bubble);
    chatMsgs.appendChild(wrap);
    chatMsgs.scrollTop = chatMsgs.scrollHeight;
  }
  function removeTyping() { const t = document.getElementById('chat-typing'); if (t) t.remove(); }

  /* ── Knowledge base ── */
  const KB = [
    { keys:['cos','progetto','voltai','associazione','obiettivo','chi siete','di cosa','parlami'], answer:"C'era una voltAI è un'associazione con l'obiettivo di spiegare e diffondere informazioni sull'intelligenza artificiale. I collaboratori svolgono progetti nelle scuole e nelle aziende per spiegare come funzionano davvero gli algoritmi alla base dell'IA, incluso come riconoscere immagini e contenuti falsi." },
    { keys:['corsi','formazione','scuola','azienda','incontri','lezioni','bambini','obbligatori','eta','calibrati'], answer:"I nostri incontri formativi sono obbligatori e calibrati in base all'età del pubblico. I corsi partono fin dall'infanzia: già da piccoli si impara a usare l'IA in modo consapevole. Siamo presenti sia nelle scuole che nelle aziende." },
    { keys:['anziani','difficolta','assistenza','aiutate','autonomi','anziano','divario','digitale'], answer:"L'associazione si occupa di assistere le persone anziane o con difficoltà che non riescono a essere completamente autonome nell'uso dell'IA. L'obiettivo è ridurre il divario digitale e garantire a tutti la possibilità di interagire con le nuove tecnologie." },
    { keys:['gara','competizione','riconoscimento','umano','testo','articolo','indovinare','ai o umano','concorrenti'], answer:"Organizziamo una gara di riconoscimento di contenuti AI: i partecipanti analizzano testi, articoli e immagini e devono stabilire — senza strumenti esterni — quali sono stati creati da un essere umano e quali dall'IA. L'obiettivo è allenare l'occhio critico e la consapevolezza mediatica." },
    { keys:['arte','artistico','restauro','opere','stile','grafico','culturale','pittura','modelli'], answer:"Abbiamo due attività artistico-culturali: creiamo modelli artistici per insegnare all'IA nuovi stili grafici; e restauriamo opere d'arte con l'IA per scopi conservativi e culturali, con stima dei danni all'opera originale." },
    { keys:['software','metadati','codici','rilevamento','sistema','deepfake','generato','riconoscimento immagini'], answer:"Stiamo sviluppando un sistema per riconoscere le immagini generate dall'IA: funziona inserendo codici nei metadati delle immagini generate e leggendoli con un apposito software di rilevamento, rendendo più trasparente la provenienza dei contenuti visivi." },
    { keys:['attivita','servizi','cosa offrite','cosa fate','cosa offre','speciali'], answer:"Le nostre attività principali sono: 1) Corsi nelle scuole e aziende, calibrati per ogni età. 2) Assistenza alle persone anziane o con difficoltà. 3) Gara «AI o Umano?» per riconoscere contenuti generati dall'IA. 4) Progetti artistici e restauro di opere d'arte con l'IA. 5) Sistema software per rilevare immagini AI tramite metadati." },
    { keys:['contatti','sede','email','telefono','dove','indirizzo'], answer:"Puoi contattarci all'email info@cerauna-voltai.it oppure al telefono +39 02 1234 5678. La sede principale è in Via dell'Innovazione 42, Milano. Siamo disponibili dal lunedì al venerdì dalle 9:00 alle 18:00." },
  ];

  function normalize(t) { return t.toLowerCase().normalize("NFD").replace(/[\u0300-\u036f]/g,""); }

  function findAnswer(text) {
    const t = normalize(text);
    for (const e of KB) if (e.keys.some(k => t.includes(normalize(k)))) return e.answer;
    return "Grazie per la domanda! Non ho informazioni specifiche su questo argomento. Per una risposta più dettagliata puoi contattarci all'email info@cerauna-voltai.it.";
  }

  function sendChatMsg() {
    const text = chatInput.value.trim();
    if (!text) return;
    addChatMsg('user', text);
    chatInput.value = '';
    chatInput.style.height = 'auto';
    chatSendBtn.disabled = true;
    addTyping();
    setTimeout(() => {
      removeTyping();
      addChatMsg('ai', findAnswer(text));
      chatSendBtn.disabled = false;
      chatInput.focus();
    }, 700 + Math.random() * 500);
  }
</script>
</body>
</html>