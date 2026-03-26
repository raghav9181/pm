<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CoverSure — PM Case Study</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;0,900;1,700&family=DM+Sans:wght@300;400;500;600&family=DM+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --navy: #0a0f1e;
    --navy2: #111827;
    --navy3: #1a2235;
    --teal: #0d9488;
    --teal-light: #14b8a6;
    --amber: #f59e0b;
    --amber-light: #fbbf24;
    --coral: #f43f5e;
    --purple: #8b5cf6;
    --text: #e2e8f0;
    --text-muted: #94a3b8;
    --text-faint: #64748b;
    --border: rgba(255,255,255,0.07);
    --card-bg: rgba(255,255,255,0.03);
    --card-hover: rgba(255,255,255,0.06);
    --green: #10b981;
    --red: #ef4444;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--navy);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    line-height: 1.7;
    overflow-x: hidden;
  }

  /* ── NOISE OVERLAY ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.4;
  }

  /* ── GRID LINES ── */
  .grid-lines {
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(13,148,136,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(13,148,136,0.04) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
    z-index: 0;
  }

  /* ── NAVBAR ── */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    z-index: 100;
    background: rgba(10,15,30,0.85);
    backdrop-filter: blur(16px);
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 40px;
    height: 60px;
  }

  .nav-brand {
    display: flex;
    align-items: center;
    gap: 10px;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    color: var(--teal-light);
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  .nav-dot {
    width: 8px; height: 8px;
    background: var(--teal);
    border-radius: 50%;
    animation: pulse 2s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.5; transform: scale(0.8); }
  }

  .nav-links {
    display: flex;
    gap: 0;
    list-style: none;
  }

  .nav-links a {
    display: block;
    padding: 6px 14px;
    font-size: 12px;
    font-weight: 500;
    color: var(--text-muted);
    text-decoration: none;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    transition: color 0.2s;
    border-radius: 4px;
  }

  .nav-links a:hover { color: var(--teal-light); }

  /* ── HERO ── */
  .hero {
    position: relative;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 120px 40px 80px;
    overflow: hidden;
  }

  .hero-glow {
    position: absolute;
    top: -200px; left: -200px;
    width: 700px; height: 700px;
    background: radial-gradient(circle, rgba(13,148,136,0.12) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero-glow-2 {
    position: absolute;
    bottom: -100px; right: -100px;
    width: 500px; height: 500px;
    background: radial-gradient(circle, rgba(245,158,11,0.07) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero-inner {
    position: relative;
    max-width: 900px;
    z-index: 1;
  }

  .hero-tag {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--teal-light);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-bottom: 28px;
    padding: 6px 14px;
    border: 1px solid rgba(13,148,136,0.3);
    border-radius: 2px;
    opacity: 0;
    animation: fadeUp 0.6s ease forwards 0.1s;
  }

  .hero h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(42px, 7vw, 80px);
    font-weight: 900;
    line-height: 1.05;
    letter-spacing: -0.02em;
    margin-bottom: 28px;
    opacity: 0;
    animation: fadeUp 0.7s ease forwards 0.25s;
  }

  .hero h1 em {
    font-style: italic;
    color: var(--teal-light);
  }

  .hero-sub {
    font-size: 17px;
    color: var(--text-muted);
    max-width: 580px;
    line-height: 1.7;
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeUp 0.7s ease forwards 0.4s;
  }

  .hero-meta {
    display: flex;
    flex-wrap: wrap;
    gap: 24px;
    opacity: 0;
    animation: fadeUp 0.7s ease forwards 0.55s;
  }

  .meta-chip {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }

  .meta-chip .label {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    color: var(--text-faint);
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  .meta-chip .val {
    font-size: 14px;
    font-weight: 500;
    color: var(--text);
  }

  .hero-scroll {
    position: absolute;
    bottom: 40px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
    font-size: 11px;
    color: var(--text-faint);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    font-family: 'DM Mono', monospace;
    opacity: 0;
    animation: fadeUp 0.7s ease forwards 0.8s;
  }

  .scroll-line {
    width: 1px;
    height: 40px;
    background: linear-gradient(to bottom, var(--teal), transparent);
    animation: scrollLine 1.5s ease-in-out infinite;
  }

  @keyframes scrollLine {
    0%, 100% { transform: scaleY(1); opacity: 1; }
    50% { transform: scaleY(0.5); opacity: 0.4; }
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ── MAIN WRAPPER ── */
  main {
    position: relative;
    z-index: 1;
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 40px 100px;
  }

  /* ── SECTION ── */
  .section {
    margin-bottom: 100px;
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }

  .section.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .section-header {
    display: flex;
    align-items: center;
    gap: 16px;
    margin-bottom: 40px;
  }

  .section-number {
    font-family: 'DM Mono', monospace;
    font-size: 11px;
    color: var(--teal);
    letter-spacing: 0.1em;
    min-width: 24px;
  }

  .section-line {
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  .section-header h2 {
    font-family: 'Playfair Display', serif;
    font-size: 36px;
    font-weight: 700;
    letter-spacing: -0.02em;
    line-height: 1.1;
  }

  /* ── EXEC SUMMARY ── */
  .exec-box {
    background: rgba(13,148,136,0.06);
    border: 1px solid rgba(13,148,136,0.2);
    border-radius: 4px;
    padding: 32px;
    margin-bottom: 60px;
    position: relative;
    overflow: hidden;
  }

  .exec-box::before {
    content: '"';
    position: absolute;
    top: -20px;
    left: 20px;
    font-family: 'Playfair Display', serif;
    font-size: 160px;
    color: rgba(13,148,136,0.08);
    line-height: 1;
    pointer-events: none;
  }

  .exec-box p {
    font-size: 16px;
    line-height: 1.8;
    color: var(--text-muted);
    position: relative;
    z-index: 1;
  }

  .exec-box p strong {
    color: var(--text);
    font-weight: 600;
  }

  /* ── CARD ── */
  .card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 24px;
    transition: background 0.2s, border-color 0.2s;
  }

  .card:hover {
    background: var(--card-hover);
    border-color: rgba(13,148,136,0.2);
  }

  .card-title {
    font-size: 14px;
    font-weight: 600;
    color: var(--text);
    margin-bottom: 8px;
  }

  .card-desc {
    font-size: 14px;
    color: var(--text-muted);
    line-height: 1.7;
  }

  /* ── FEATURES GRID ── */
  .features-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 16px;
    margin-bottom: 48px;
  }

  .feature-card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 24px;
    transition: all 0.2s;
    position: relative;
    overflow: hidden;
  }

  .feature-card::after {
    content: '';
    position: absolute;
    top: 0; left: 0;
    width: 3px;
    height: 100%;
    background: var(--teal);
    transform: scaleY(0);
    transition: transform 0.2s;
    transform-origin: top;
  }

  .feature-card:hover::after { transform: scaleY(1); }
  .feature-card:hover { border-color: rgba(13,148,136,0.25); background: var(--card-hover); }

  .feature-icon {
    font-size: 24px;
    margin-bottom: 14px;
  }

  .feature-name {
    font-size: 14px;
    font-weight: 600;
    margin-bottom: 8px;
  }

  .feature-desc {
    font-size: 13px;
    color: var(--text-muted);
    line-height: 1.6;
  }

  /* ── STATS STRIP ── */
  .stats-strip {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 0;
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
    margin-bottom: 60px;
  }

  .stat-item {
    padding: 28px 24px;
    border-right: 1px solid var(--border);
    position: relative;
  }

  .stat-item:last-child { border-right: none; }

  .stat-val {
    font-family: 'Playfair Display', serif;
    font-size: 40px;
    font-weight: 700;
    color: var(--teal-light);
    line-height: 1;
    margin-bottom: 6px;
  }

  .stat-label {
    font-size: 13px;
    color: var(--text-muted);
    line-height: 1.4;
  }

  .stat-sub {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    color: var(--text-faint);
    margin-top: 6px;
    letter-spacing: 0.05em;
  }

  /* ── PROS CONS ── */
  .proscons-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }

  .pro-col, .con-col { display: flex; flex-direction: column; gap: 12px; }

  .col-header {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 12px 16px;
    border-radius: 3px;
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    margin-bottom: 4px;
  }

  .col-header.pro { background: rgba(16,185,129,0.1); color: var(--green); border: 1px solid rgba(16,185,129,0.2); }
  .col-header.con { background: rgba(239,68,68,0.08); color: var(--red); border: 1px solid rgba(239,68,68,0.15); }

  .pc-item {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 16px 18px;
    transition: all 0.2s;
  }

  .pc-item:hover { background: var(--card-hover); }

  .pc-title {
    font-size: 13px;
    font-weight: 600;
    margin-bottom: 4px;
  }

  .pro-col .pc-title { color: rgba(16,185,129,0.9); }
  .con-col .pc-title { color: rgba(239,68,68,0.9); }

  .pc-desc {
    font-size: 12px;
    color: var(--text-muted);
    line-height: 1.6;
  }

  /* ── PERSONAS ── */
  .personas-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    gap: 16px;
    margin-bottom: 40px;
  }

  .persona-card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 24px;
    transition: all 0.2s;
  }

  .persona-card:hover {
    border-color: rgba(13,148,136,0.25);
    background: var(--card-hover);
  }

  .persona-avatar {
    width: 48px; height: 48px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 22px;
    margin-bottom: 14px;
  }

  .persona-name { font-size: 15px; font-weight: 600; margin-bottom: 2px; }
  .persona-role { font-size: 12px; color: var(--text-faint); margin-bottom: 14px; }
  .persona-pain { font-size: 13px; color: var(--text-muted); line-height: 1.6; }
  .persona-pain strong { color: var(--text); font-weight: 500; }

  /* ── SWOT ── */
  .swot-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }

  .swot-cell {
    border-radius: 4px;
    padding: 24px;
    border: 1px solid;
  }

  .swot-cell h4 {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .swot-cell h4::before {
    content: '';
    display: inline-block;
    width: 6px; height: 6px;
    border-radius: 50%;
  }

  .sw-s { background: rgba(16,185,129,0.05); border-color: rgba(16,185,129,0.15); }
  .sw-s h4 { color: var(--green); }
  .sw-s h4::before { background: var(--green); }

  .sw-w { background: rgba(239,68,68,0.05); border-color: rgba(239,68,68,0.12); }
  .sw-w h4 { color: var(--red); }
  .sw-w h4::before { background: var(--red); }

  .sw-o { background: rgba(13,148,136,0.05); border-color: rgba(13,148,136,0.15); }
  .sw-o h4 { color: var(--teal-light); }
  .sw-o h4::before { background: var(--teal-light); }

  .sw-t { background: rgba(245,158,11,0.05); border-color: rgba(245,158,11,0.15); }
  .sw-t h4 { color: var(--amber); }
  .sw-t h4::before { background: var(--amber); }

  .swot-cell ul { list-style: none; }
  .swot-cell ul li {
    font-size: 13px;
    color: var(--text-muted);
    padding: 5px 0;
    border-bottom: 1px solid var(--border);
    line-height: 1.4;
    display: flex;
    gap: 8px;
  }

  .swot-cell ul li:last-child { border-bottom: none; }
  .swot-cell ul li::before { content: '→'; color: var(--text-faint); flex-shrink: 0; }

  /* ── REVENUE ── */
  .north-star-box {
    background: linear-gradient(135deg, rgba(13,148,136,0.08), rgba(139,92,246,0.06));
    border: 1px solid rgba(13,148,136,0.25);
    border-radius: 4px;
    padding: 36px;
    margin-bottom: 40px;
    text-align: center;
  }

  .ns-tag {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    color: var(--teal);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 16px;
  }

  .north-star-box h3 {
    font-family: 'Playfair Display', serif;
    font-size: 28px;
    font-weight: 700;
    line-height: 1.3;
    margin-bottom: 12px;
  }

  .north-star-box p {
    font-size: 14px;
    color: var(--text-muted);
  }

  .rev-streams {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 16px;
    margin-bottom: 40px;
  }

  .rev-card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 24px;
    transition: all 0.2s;
    position: relative;
  }

  .rev-card:hover {
    background: var(--card-hover);
    border-color: rgba(13,148,136,0.2);
    transform: translateY(-2px);
  }

  .rev-badge {
    display: inline-block;
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 3px 8px;
    border-radius: 2px;
    margin-bottom: 14px;
  }

  .badge-new { background: rgba(13,148,136,0.15); color: var(--teal-light); }
  .badge-existing { background: rgba(245,158,11,0.12); color: var(--amber); }
  .badge-strategic { background: rgba(139,92,246,0.12); color: #a78bfa; }

  .rev-card h4 { font-size: 15px; font-weight: 600; margin-bottom: 6px; }

  .rev-amount {
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    color: var(--teal-light);
    margin-bottom: 10px;
    font-weight: 500;
  }

  .rev-card p { font-size: 13px; color: var(--text-muted); line-height: 1.6; }

  /* ── ROADMAP / TIMELINE ── */
  .timeline {
    position: relative;
    padding-left: 32px;
  }

  .timeline::before {
    content: '';
    position: absolute;
    left: 7px;
    top: 12px;
    bottom: 12px;
    width: 1px;
    background: linear-gradient(to bottom, var(--teal), rgba(13,148,136,0.1));
  }

  .tl-item {
    position: relative;
    margin-bottom: 40px;
    opacity: 0;
    transform: translateX(-10px);
    transition: opacity 0.5s ease, transform 0.5s ease;
  }

  .tl-item.tl-visible {
    opacity: 1;
    transform: translateX(0);
  }

  .tl-dot {
    position: absolute;
    left: -28px;
    top: 6px;
    width: 10px; height: 10px;
    border-radius: 50%;
    border: 2px solid var(--navy);
  }

  .tl-dot.blue { background: #3b82f6; box-shadow: 0 0 8px rgba(59,130,246,0.4); }
  .tl-dot.amber { background: var(--amber); box-shadow: 0 0 8px rgba(245,158,11,0.4); }
  .tl-dot.purple { background: #8b5cf6; box-shadow: 0 0 8px rgba(139,92,246,0.4); }
  .tl-dot.green { background: var(--green); box-shadow: 0 0 8px rgba(16,185,129,0.4); }

  .tl-phase {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-bottom: 6px;
  }

  .phase-blue { color: #60a5fa; }
  .phase-amber { color: var(--amber); }
  .phase-purple { color: #a78bfa; }
  .phase-green { color: var(--green); }

  .tl-title {
    font-size: 16px;
    font-weight: 600;
    margin-bottom: 6px;
    display: flex;
    align-items: center;
    gap: 10px;
    flex-wrap: wrap;
  }

  .priority {
    font-size: 10px;
    font-weight: 600;
    padding: 2px 8px;
    border-radius: 2px;
    letter-spacing: 0.06em;
    text-transform: uppercase;
  }

  .p-critical { background: rgba(239,68,68,0.15); color: #fca5a5; }
  .p-high { background: rgba(245,158,11,0.12); color: var(--amber-light); }
  .p-medium { background: rgba(13,148,136,0.12); color: var(--teal-light); }
  .p-strategic { background: rgba(139,92,246,0.12); color: #c4b5fd; }

  .tl-desc {
    font-size: 14px;
    color: var(--text-muted);
    line-height: 1.7;
    max-width: 680px;
  }

  /* ── METRICS ── */
  .metrics-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 12px;
    margin-bottom: 40px;
  }

  .metric-card {
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 20px;
    transition: all 0.2s;
  }

  .metric-card:hover {
    background: var(--card-hover);
    border-color: rgba(13,148,136,0.2);
  }

  .metric-layer {
    font-family: 'DM Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-bottom: 10px;
  }

  .layer-acq { color: #60a5fa; }
  .layer-eng { color: var(--teal-light); }
  .layer-ret { color: var(--amber); }
  .layer-rev { color: var(--coral); }
  .layer-trust { color: #a78bfa; }

  .metric-name {
    font-size: 13px;
    color: var(--text-muted);
    margin-bottom: 8px;
    line-height: 1.4;
  }

  .metric-target {
    font-family: 'DM Mono', monospace;
    font-size: 14px;
    font-weight: 500;
    color: var(--text);
  }

  /* ── KPI TABLE ── */
  .kpi-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 14px;
  }

  .kpi-table thead th {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--text-faint);
    text-align: left;
    padding: 10px 16px;
    border-bottom: 1px solid var(--border);
    font-family: 'DM Mono', monospace;
  }

  .kpi-table tbody tr {
    border-bottom: 1px solid var(--border);
    transition: background 0.15s;
  }

  .kpi-table tbody tr:hover { background: var(--card-hover); }
  .kpi-table tbody tr:last-child { border-bottom: none; }

  .kpi-table td {
    padding: 14px 16px;
    color: var(--text-muted);
    vertical-align: top;
    line-height: 1.5;
  }

  .kpi-table td:first-child { font-weight: 500; font-size: 13px; }
  .kpi-table td:last-child {
    font-family: 'DM Mono', monospace;
    font-size: 13px;
    color: var(--teal-light);
    font-weight: 500;
  }

  /* ── COMPETITIVE ── */
  .comp-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }

  /* ── INSIGHT BOX ── */
  .insight-box {
    background: rgba(245,158,11,0.05);
    border: 1px solid rgba(245,158,11,0.2);
    border-radius: 4px;
    padding: 32px;
    position: relative;
    overflow: hidden;
  }

  .insight-box::before {
    content: '!';
    position: absolute;
    right: 20px;
    bottom: -20px;
    font-family: 'Playfair Display', serif;
    font-size: 140px;
    font-weight: 900;
    color: rgba(245,158,11,0.05);
    line-height: 1;
  }

  .insight-box h3 {
    font-size: 18px;
    font-weight: 600;
    color: var(--amber-light);
    margin-bottom: 12px;
    position: relative;
  }

  .insight-box p {
    font-size: 14px;
    color: var(--text-muted);
    line-height: 1.8;
    position: relative;
  }

  /* ── FOOTER ── */
  footer {
    border-top: 1px solid var(--border);
    padding: 40px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 12px;
    color: var(--text-faint);
    font-family: 'DM Mono', monospace;
    letter-spacing: 0.04em;
    max-width: 1100px;
    margin: 0 auto;
  }

  /* ── DIVIDER ── */
  .divider {
    height: 1px;
    background: var(--border);
    margin: 48px 0;
  }

  /* ── RESPONSIVE ── */
  @media (max-width: 768px) {
    nav { padding: 0 20px; }
    .nav-links { display: none; }
    .hero { padding: 100px 24px 60px; }
    main { padding: 0 24px 80px; }
    .proscons-grid, .swot-grid, .comp-grid { grid-template-columns: 1fr; }
    .stats-strip { grid-template-columns: 1fr; }
    .stat-item { border-right: none; border-bottom: 1px solid var(--border); }
    footer { flex-direction: column; gap: 12px; text-align: center; padding: 24px; }
    .personas-grid { grid-template-columns: 1fr 1fr; }
  }

  @media (max-width: 480px) {
    .hero h1 { font-size: 36px; }
    .personas-grid { grid-template-columns: 1fr; }
  }

  /* ── SECTION LABELS ── */
  .section-label {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    color: var(--teal);
    letter-spacing: 0.15em;
    text-transform: uppercase;
    margin-bottom: 12px;
    display: block;
  }

  /* ── TABLE WRAPPER ── */
  .table-wrap {
    border: 1px solid var(--border);
    border-radius: 4px;
    overflow: hidden;
  }

  /* ── JOBSTODO ── */
  .jtbd-list {
    display: flex;
    flex-direction: column;
    gap: 12px;
    margin-top: 24px;
  }

  .jtbd-item {
    display: flex;
    gap: 16px;
    background: var(--card-bg);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 20px;
    transition: all 0.2s;
  }

  .jtbd-item:hover { background: var(--card-hover); border-color: rgba(13,148,136,0.2); }

  .jtbd-num {
    font-family: 'Playfair Display', serif;
    font-size: 32px;
    font-weight: 700;
    color: rgba(13,148,136,0.3);
    line-height: 1;
    flex-shrink: 0;
    min-width: 32px;
  }

  .jtbd-content h4 { font-size: 14px; font-weight: 600; margin-bottom: 4px; }
  .jtbd-content p { font-size: 13px; color: var(--text-muted); line-height: 1.6; }

  .cards-stack { display: flex; flex-direction: column; gap: 12px; }
</style>
</head>
<body>

<div class="grid-lines"></div>

<!-- NAV -->
<nav>
  <div class="nav-brand">
    <div class="nav-dot"></div>
    CoverSure · PM Case Study
  </div>
  <ul class="nav-links">
    <li><a href="#overview">Overview</a></li>
    <li><a href="#proscons">Pros & Cons</a></li>
    <li><a href="#personas">Personas</a></li>
    <li><a href="#swot">SWOT</a></li>
    <li><a href="#revenue">Revenue</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#metrics">Metrics</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-glow"></div>
  <div class="hero-glow-2"></div>
  <div class="hero-inner">
    <div class="hero-tag">
      <span style="width:6px;height:6px;background:var(--teal);border-radius:50%;display:inline-block;"></span>
      Product Management Case Study · 2025
    </div>
    <h1>From free tool to<br><em>India's revenue engine</em><br>for insurance</h1>
    <p class="hero-sub">A full end-to-end PM teardown of CoverSure — the insurtech building the nervous system of Indian insurance. Pros, cons, personas, SWOT, revenue model redesign, roadmap, and north star metrics.</p>
    <div class="hero-meta">
      <div class="meta-chip">
        <span class="label">Company</span>
        <span class="val">Claycove23 Insurance Tech</span>
      </div>
      <div class="meta-chip">
        <span class="label">Founded</span>
        <span class="val">2022 · Mumbai</span>
      </div>
      <div class="meta-chip">
        <span class="label">IRDAI License</span>
        <span class="val">CA0894 · Composite</span>
      </div>
      <div class="meta-chip">
        <span class="label">Funding</span>
        <span class="val">$4M pre-Series A</span>
      </div>
    </div>
  </div>
  <div class="hero-scroll">
    <div class="scroll-line"></div>
    <span>Scroll</span>
  </div>
</section>

<!-- MAIN -->
<main>

  <!-- 01 OVERVIEW -->
  <section class="section" id="overview">
    <div class="section-header">
      <span class="section-number">01</span>
      <h2>Product Overview</h2>
      <div class="section-line"></div>
    </div>

    <div class="exec-box">
      <p>CoverSure has built a genuinely useful product for a genuinely underserved problem — <strong>80% of Indians don't understand the policies they're paying for.</strong> But there's a critical tension: every feature is free, and the only revenue comes from commissions when users convert advisory sessions into policy purchases. That's a low-frequency, high-friction event. This case study maps how to unlock 5× revenue without breaking user trust.</p>
    </div>

    <div class="stats-strip">
      <div class="stat-item">
        <div class="stat-val">$4M</div>
        <div class="stat-label">Pre-Series A raised</div>
        <div class="stat-sub">Led by Enam Holdings · 2023</div>
      </div>
      <div class="stat-item">
        <div class="stat-val">80%</div>
        <div class="stat-label">Indians unclear on their own insurance policy</div>
        <div class="stat-sub">CoverSure market survey 2024</div>
      </div>
      <div class="stat-item">
        <div class="stat-val">Jan '27</div>
        <div class="stat-label">IRDAI license validity</div>
        <div class="stat-sub">CA0894 · Corporate Agent Composite</div>
      </div>
    </div>

    <span class="section-label">Product suite</span>
    <div class="features-grid">
      <div class="feature-card">
        <div class="feature-icon">📁</div>
        <div class="feature-name">Insurance Portfolio</div>
        <div class="feature-desc">Centralised dashboard for all policies — health, term, motor, home. Renewal alerts, gap detection, and a unified view of your coverage universe.</div>
      </div>
      <div class="feature-card">
        <div class="feature-icon">⚖️</div>
        <div class="feature-name">CoverPro Risk Calculator</div>
        <div class="feature-desc">AI-powered coverage adequacy check. Identifies if you're under or over insured across life stages and risk profiles.</div>
      </div>
      <div class="feature-card">
        <div class="feature-icon">📄</div>
        <div class="feature-name">Know Your Policy</div>
        <div class="feature-desc">Upload any policy PDF and get a plain-English breakdown of inclusions, exclusions, waiting periods, and claim tips.</div>
      </div>
      <div class="feature-card">
        <div class="feature-icon">💳</div>
        <div class="feature-name">Insurance on Cards</div>
        <div class="feature-desc">Discovers hidden insurance bundled with credit and debit cards that most users never know about — and never claim.</div>
      </div>
      <div class="feature-card">
        <div class="feature-icon">🚗</div>
        <div class="feature-name">CoverSure Motor Club</div>
        <div class="feature-desc">FASTag top-up, PUC certificate, e-challan payment, roadside assistance and garage locator — the daily-use utility that drives retention.</div>
      </div>
      <div class="feature-card">
        <div class="feature-icon">🆘</div>
        <div class="feature-name">CoverSure SOS</div>
        <div class="feature-desc">One-tap emergency contacts — ambulance, towing, hospital locator — with live location sharing. The feature that makes the app feel essential.</div>
      </div>
    </div>
  </section>

  <!-- 02 PROS & CONS -->
  <section class="section" id="proscons">
    <div class="section-header">
      <span class="section-number">02</span>
      <h2>Pros &amp; Cons</h2>
      <div class="section-line"></div>
    </div>

    <div class="proscons-grid">
      <div class="pro-col">
        <div class="col-header pro">
          <span>✓</span> Strengths
        </div>
        <div class="pc-item">
          <div class="pc-title">Genuine consumer pain solved</div>
          <div class="pc-desc">80% of Indians don't understand their own policies. CoverSure directly addresses this confusion gap — a real problem, not a manufactured one.</div>
        </div>
        <div class="pc-item">
          <div class="pc-title">Unbiased brand positioning</div>
          <div class="pc-desc">Licensed IRDAI advisor with a genuine no-pressure ethos. Extremely rare in a market dominated by commission-hungry agents and comparison sites.</div>
        </div>
        <div class="pc-item">
          <div class="pc-title">Product breadth creates stickiness</div>
          <div class="pc-desc">7+ distinct features spanning portfolio, motor, SOS, and card discovery. Motor Club alone creates daily-use habits that keep users opening the app.</div>
        </div>
        <div class="pc-item">
          <div class="pc-title">ISO 27001 + DPDP compliant</div>
          <div class="pc-desc">Strong data trust infrastructure in a market where data privacy anxiety is the #1 barrier to fintech adoption.</div>
        </div>
        <div class="pc-item">
          <div class="pc-title">Micro-insurance innovation</div>
          <div class="pc-desc">₹5 Firecracker Insurance demonstrates creative product thinking and B2C distribution capability at low price points.</div>
        </div>
        <div class="pc-item">
          <div class="pc-title">Composite agent license</div>
          <div class="pc-desc">Can sell across all insurance categories — life, health, motor, general — giving maximum addressable market breadth.</div>
        </div>
      </div>
      <div class="con-col">
        <div class="col-header con">
          <span>✗</span> Weaknesses
        </div>
        <div class="pc-item">
          <div class="pc-title">Zero visible monetisation</div>
          <div class="pc-desc">Every tool is free with no freemium gate. Users have no incentive to upgrade or pay — ever. The company only earns on rare policy conversion events.</div>
        </div>
        <div class="pc-item">
          <div class="pc-title">App reliability issues</div>
          <div class="pc-desc">App Store reviews frequently cite "Service Unavailable" errors. In a trust-first product, broken reliability is brand suicide.</div>
        </div>
        <div class="pc-item">
          <div class="pc-title">Commission-only revenue is fragile</div>
          <div class="pc-desc">High CAC, lumpy revenue, and total dependency on infrequent events. One bad quarter of sales means zero revenue despite thousands of active users.</div>
        </div>
        <div class="pc-item">
          <div class="pc-title">No B2B or group insurance play</div>
          <div class="pc-desc">HR teams and SMEs spend crores on employee group health cover annually. CoverSure has no enterprise product to capture this high-LTV segment.</div>
        </div>
        <div class="pc-item">
          <div class="pc-title">Website is SEO-invisible</div>
          <div class="pc-desc">Heavy JavaScript rendering means search crawler bots see mostly empty pages. Organic discovery — the cheapest user acquisition channel — is near-zero.</div>
        </div>
        <div class="pc-item">
          <div class="pc-title">No in-app claims management</div>
          <div class="pc-desc">Advisory for claims exists but there's no in-app filing pipeline or status tracker. This is the #1 user anxiety moment — and CoverSure doesn't own it.</div>
        </div>
      </div>
    </div>
  </section>

  <!-- 03 PERSONAS -->
  <section class="section" id="personas">
    <div class="section-header">
      <span class="section-number">03</span>
      <h2>User Personas</h2>
      <div class="section-line"></div>
    </div>

    <div class="personas-grid">
      <div class="persona-card">
        <div class="persona-avatar" style="background:rgba(13,148,136,0.15);">🧑‍💼</div>
        <div class="persona-name">Rohan, 32</div>
        <div class="persona-role">IT Professional · Hyderabad · ₹18L/yr</div>
        <div class="persona-pain"><strong>Problem:</strong> Has 4 policies from 3 different agents plus employer cover. No idea what's actually covered. Scared of renewal lapse.<br><br><strong>Trigger:</strong> Friend got claim rejected due to a fine-print exclusion he'd never heard of.</div>
      </div>
      <div class="persona-card">
        <div class="persona-avatar" style="background:rgba(245,158,11,0.12);">👩‍👧</div>
        <div class="persona-name">Priya, 40</div>
        <div class="persona-role">Homemaker · Chennai · Family of 4</div>
        <div class="persona-pain"><strong>Problem:</strong> Husband manages all insurance but is now posted abroad. Medical emergency happened — she couldn't locate the policy or find the TPA code.<br><br><strong>Trigger:</strong> Hospital front desk asked for a cashless card she'd never seen.</div>
      </div>
      <div class="persona-card">
        <div class="persona-avatar" style="background:rgba(139,92,246,0.12);">👴</div>
        <div class="persona-name">Suresh, 58</div>
        <div class="persona-role">Retired Govt. Officer · Pune</div>
        <div class="persona-pain"><strong>Problem:</strong> 6+ policies accumulated over 30 years. Paying premiums on possibly redundant covers. Needs someone to make sense of it all.<br><br><strong>Trigger:</strong> Missed a term policy renewal by 3 days — lost ₹2.4L in coverage.</div>
      </div>
      <div class="persona-card">
        <div class="persona-avatar" style="background:rgba(244,63,94,0.1);">👩‍💻</div>
        <div class="persona-name">Kavya, 26</div>
        <div class="persona-role">Startup Founder · Bengaluru · 8 employees</div>
        <div class="persona-pain"><strong>Problem:</strong> Needs group health cover for her team. Agents quote wildly different prices with no transparency. No time to compare properly.<br><br><strong>Trigger:</strong> A key engineer resigned citing "no medical insurance" as reason.</div>
      </div>
    </div>

    <span class="section-label" style="margin-top:48px;">Jobs to be done</span>
    <div class="jtbd-list">
      <div class="jtbd-item">
        <div class="jtbd-num">1</div>
        <div class="jtbd-content">
          <h4>"Make my insurance chaos manageable in one place"</h4>
          <p>Users want a single source of truth for all policies. CoverSure's portfolio feature directly solves this. Opportunity: make it shareable with family members and financial advisors, and auto-import from insurer emails.</p>
        </div>
      </div>
      <div class="jtbd-item">
        <div class="jtbd-num">2</div>
        <div class="jtbd-content">
          <h4>"Tell me I won't be blindsided at claim time"</h4>
          <p>The deepest anxiety in all of insurance. Know Your Policy helps decode policies but doesn't resolve the claim-time fear. Opportunity: in-app claims pre-check wizard, document checklist, and real-time status tracker.</p>
        </div>
      </div>
      <div class="jtbd-item">
        <div class="jtbd-num">3</div>
        <div class="jtbd-content">
          <h4>"Help me stop wasting money on the wrong coverage"</h4>
          <p>CoverPro's risk calculator surfaces over and under-insurance. The current gap: it surfaces the problem but doesn't close the loop with a solution. Opportunity: in-context policy recommendation and 1-tap purchase after gap is identified.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- 04 SWOT -->
  <section class="section" id="swot">
    <div class="section-header">
      <span class="section-number">04</span>
      <h2>SWOT Analysis</h2>
      <div class="section-line"></div>
    </div>

    <div class="swot-grid">
      <div class="swot-cell sw-s">
        <h4>Strengths</h4>
        <ul>
          <li>IRDAI composite license — all insurance categories</li>
          <li>Unbiased advisory brand positioning</li>
          <li>ISO 27001 + DPDP data compliance</li>
          <li>$4M funding runway from credible backer</li>
          <li>Motor Club creates genuine daily-use habits</li>
          <li>Micro-insurance track record (₹5 Firecracker)</li>
          <li>SOS feature adds genuine life-safety utility</li>
        </ul>
      </div>
      <div class="swot-cell sw-w">
        <h4>Weaknesses</h4>
        <ul>
          <li>All features free — no monetisation trigger exists</li>
          <li>App stability issues cited in store reviews</li>
          <li>Website SEO-invisible due to client-side rendering</li>
          <li>No B2B or group insurance product line</li>
          <li>Claims management is advisory-only, not digital</li>
          <li>Small team bandwidth vs. larger funded rivals</li>
          <li>Commission-only revenue is lumpy and fragile</li>
        </ul>
      </div>
      <div class="swot-cell sw-o">
        <h4>Opportunities</h4>
        <ul>
          <li>₹5.5L Cr Indian insurance market, growing 15%+ YoY</li>
          <li>Only 3.7% life insurance penetration in India</li>
          <li>SME group health cover — massive, underserved</li>
          <li>AI claims prediction and prevention layer</li>
          <li>WhatsApp-first insurance for Tier 2/3 India</li>
          <li>Embedded insurance API for fintechs and banks</li>
          <li>IRDAI Bima Sugam digital infrastructure rollout</li>
        </ul>
      </div>
      <div class="swot-cell sw-t">
        <h4>Threats</h4>
        <ul>
          <li>Policybazaar's scale and massive ad spend</li>
          <li>Ditto Insurance (Zerodha) — identical positioning</li>
          <li>IRDAI regulatory changes to sandbox licenses</li>
          <li>Banks launching proprietary insurance management apps</li>
          <li>Data breach risk — trust is the core product</li>
          <li>Commission compression as market commoditises</li>
          <li>Well-funded InsurTech startups entering portfolio mgmt</li>
        </ul>
      </div>
    </div>

    <div class="divider"></div>
    <span class="section-label">Competitive positioning</span>
    <div class="comp-grid">
      <div class="card">
        <div class="card-title">CoverSure vs Policybazaar</div>
        <div class="card-desc">Policybazaar is a marketplace that sells. CoverSure is an advisor that guides. The risk: Policybazaar's new "PB Advisor" layer is entering CoverSure's turf with massive distribution. CoverSure must deepen its neutral-advisor moat and offer portfolio management that Policybazaar structurally cannot offer without appearing biased.</div>
      </div>
      <div class="card">
        <div class="card-title">CoverSure vs Ditto Insurance</div>
        <div class="card-desc">Ditto (by Zerodha) targets the same savvy millennial with plain-language advice and no commissions bias. CoverSure's differentiator: Motor Club, SOS, and card-insurance discovery — real daily utility features Ditto lacks entirely. CoverSure must double down on this "life utility" angle vs Ditto's purely advisory play.</div>
      </div>
    </div>
  </section>

  <!-- 05 REVENUE MODEL -->
  <section class="section" id="revenue">
    <div class="section-header">
      <span class="section-number">05</span>
      <h2>Revenue Model Redesign</h2>
      <div class="section-line"></div>
    </div>

    <div class="north-star-box">
      <div class="ns-tag">Revenue north star</div>
      <h3>Convert CoverSure from a free-tool aggregator<br>into a "monetise at every intent signal" platform</h3>
      <p>Without ever becoming pushy. Target: 5× revenue in 18 months through 4 new streams alongside existing commissions.</p>
    </div>

    <span class="section-label">New revenue streams</span>
    <div class="rev-streams">
      <div class="rev-card">
        <div class="rev-badge badge-new">New · Freemium</div>
        <h4>CoverSure Pro</h4>
        <div class="rev-amount">₹199–499 / month</div>
        <p>Unlock family sharing (5 members), unlimited policy uploads, WhatsApp portfolio report, annual coverage PDF, and priority claim assistance. Free tier stays free forever — this is peace-of-mind premium.</p>
      </div>
      <div class="rev-card">
        <div class="rev-badge badge-new">New · B2B SaaS</div>
        <h4>CoverSure for Teams</h4>
        <div class="rev-amount">₹99 / employee / month</div>
        <p>Group health management dashboard for SMEs with 5–200 employees. HR gets a centralised quotes, renewals, and claims console. Each employee gets their own CoverSure account linked to the company plan.</p>
      </div>
      <div class="rev-card">
        <div class="rev-badge badge-strategic">Strategic · API</div>
        <h4>Embedded Insurance API</h4>
        <div class="rev-amount">Revenue share model</div>
        <p>License the risk engine and portfolio management as an API. Target: neobanks, wealth apps, HR software. Turns CoverSure into infrastructure. Partners sell; CoverSure earns on every policy sold through them.</p>
      </div>
      <div class="rev-card">
        <div class="rev-badge badge-new">New · Micro</div>
        <h4>Event-based insurance</h4>
        <div class="rev-amount">₹5–99 per policy</div>
        <p>Expand the ₹5 Firecracker model — monsoon flood cover, travel delay, gadget protection, cricket match cancellation. Low ticket, high volume, zero agent friction.</p>
      </div>
      <div class="rev-card">
        <div class="rev-badge badge-strategic">Strategic · Data</div>
        <h4>Insurer intelligence reports</h4>
        <div class="rev-amount">₹X per anonymised insight</div>
        <p>Aggregated, anonymised risk insights sold to insurers for product design. Strictly no individual user data. Requires explicit consent framework and a strong data ethics charter.</p>
      </div>
      <div class="rev-card">
        <div class="rev-badge badge-existing">Existing · Commission</div>
        <h4>Policy sales commission</h4>
        <div class="rev-amount">10–35% commission</div>
        <p>Close the conversion loop: risk calculator identifies gap → recommended policy appears in-context → 1-tap buy with pre-filled proposal. Same commission, dramatically higher conversion rate.</p>
      </div>
    </div>

    <div class="divider"></div>
    <span class="section-label">Freemium playbook</span>
    <div class="cards-stack">
      <div class="card">
        <div class="card-title">Gate the right features — never the core value</div>
        <div class="card-desc">Keep the basic portfolio (up to 3 policies), risk calculator, and Know Your Policy free forever. Gate: adding more than 3 policies, family sharing, downloadable annual report, in-app claim filing, and priority advisor access. The free tier proves the product's value; Pro delivers the full peace of mind. Users pay for confidence, not features.</div>
      </div>
      <div class="card">
        <div class="card-title">Intent-triggered upsells — never interruptive pop-ups</div>
        <div class="card-desc">When user adds 4th policy → "You're on the free plan, which supports 3 policies. Upgrade to Pro to add all of them." When a claim is initiated → "Pro members get dedicated claim assistance with a 4-hour response SLA." No modal pop-ups. No email spam. Only contextual prompts at the exact moment the user experiences the limit.</div>
      </div>
    </div>
  </section>

  <!-- 06 ROADMAP -->
  <section class="section" id="roadmap">
    <div class="section-header">
      <span class="section-number">06</span>
      <h2>18-Month Roadmap</h2>
      <div class="section-line"></div>
    </div>

    <div class="timeline">
      <div class="tl-item">
        <div class="tl-dot blue"></div>
        <div class="tl-phase phase-blue">Q1 2025 · Fix the foundation</div>
        <div class="tl-title">App stability + SEO infrastructure overhaul <span class="priority p-critical">Critical</span></div>
        <div class="tl-desc">Fix "Service Unavailable" crashes. Migrate website to SSR (Next.js) for SEO visibility — every free organic user matters. Implement real-time monitoring (Sentry + Datadog). Target: 99.5% uptime, sub-2s page load. This is table stakes. Every other investment leaks value if the app breaks on users who need it most.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot amber"></div>
        <div class="tl-phase phase-amber">Q2 2025 · Monetise existing users</div>
        <div class="tl-title">CoverSure Pro freemium launch <span class="priority p-high">High priority</span></div>
        <div class="tl-desc">Introduce Pro at ₹199/month. Unlock: unlimited policies, family sharing (5 members), WhatsApp portfolio report, annual coverage summary PDF, and priority advisor access. Goal: 5–8% free-to-paid conversion from the existing active user base creates meaningful immediate ARR. Price test with ₹99, ₹199, and ₹299 tiers using A/B.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot amber"></div>
        <div class="tl-phase phase-amber">Q2 2025 · Close the conversion loop</div>
        <div class="tl-title">Risk-to-buy pipeline <span class="priority p-high">High priority</span></div>
        <div class="tl-desc">After the risk calculator identifies a gap (e.g., no term cover, health sum insured below threshold), show an in-context policy comparison and enable 1-click purchase with a pre-filled proposal. Users who've just identified their own coverage gap are the highest-intent audience in all of insurance — they don't need to be sold, just guided.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot purple"></div>
        <div class="tl-phase phase-purple">Q3 2025 · Own the claim moment</div>
        <div class="tl-title">In-app claims tracker and filing assistant <span class="priority p-high">High priority</span></div>
        <div class="tl-desc">Guide users through the claims process step by step: required document checklist, TPA code finder, cashless hospital locator, and real-time status tracking via insurer API. This is the highest-anxiety moment in any user's insurance life. The product that owns claims support becomes irreplaceable. This also becomes the most powerful upsell surface for Pro.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot purple"></div>
        <div class="tl-phase phase-purple">Q3 2025 · Unlock B2B revenue</div>
        <div class="tl-title">CoverSure for Teams — SME MVP <span class="priority p-medium">Medium</span></div>
        <div class="tl-desc">MVP for companies with 5–200 employees. HR gets a dashboard for group health quotes, renewals, and employee onboarding. Each employee gets their own CoverSure account pre-linked to company cover. Pilot with 10 companies at ₹0 cost — learn before pricing. The B2B LTV dwarfs B2C.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot green"></div>
        <div class="tl-phase phase-green">Q4 2025 · Expand distribution</div>
        <div class="tl-title">WhatsApp-first product for Bharat <span class="priority p-medium">Medium</span></div>
        <div class="tl-desc">A WhatsApp bot delivering portfolio summaries, renewal alerts, and micro-insurance purchases for users who won't download an app. Critical for Tier 2/3 city penetration. Uses the WABA API. Replicate the Motor Club utility experience in a conversational interface. This expands TAM beyond smartphone-comfortable users.</div>
      </div>
      <div class="tl-item">
        <div class="tl-dot green"></div>
        <div class="tl-phase phase-green">Q5–Q6 2025 · Become infrastructure</div>
        <div class="tl-title">CoverSure API — embedded insurance platform <span class="priority p-strategic">Strategic</span></div>
        <div class="tl-desc">License the risk calculator, portfolio engine, and claims tracker as an API to neobanks, wealth apps, and HR software. Revenue share on all policies sold via partners. This transforms CoverSure from a consumer app into a B2B2C platform — the most defensible position in insurtech. Start with one anchor partner to prove the model.</div>
      </div>
    </div>
  </section>

  <!-- 07 METRICS -->
  <section class="section" id="metrics">
    <div class="section-header">
      <span class="section-number">07</span>
      <h2>Success Metrics</h2>
      <div class="section-line"></div>
    </div>

    <div class="north-star-box">
      <div class="ns-tag">North star metric</div>
      <h3>"Insurance actions taken per active user per month"</h3>
      <p>Measures genuine utility — policy renewals completed, claims filed, risk reviews done, policy uploads, gap alerts actioned. A high score means a habit is formed, which means retention, which means a monetisable trust relationship.</p>
    </div>

    <span class="section-label">KPI Framework by funnel layer</span>
    <div class="table-wrap" style="margin-bottom:48px;">
      <table class="kpi-table">
        <thead>
          <tr>
            <th>Layer</th>
            <th>Metric</th>
            <th>12-month target</th>
            <th>Why it matters</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td style="color:#60a5fa;">Acquisition</td>
            <td>Monthly app installs</td>
            <td>50K / month</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">Baseline growth signal</td>
          </tr>
          <tr>
            <td style="color:#60a5fa;">Acquisition</td>
            <td>Organic search traffic share</td>
            <td>&gt;35%</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">Validates SEO investment</td>
          </tr>
          <tr>
            <td style="color:var(--teal-light);">Activation</td>
            <td>Users adding ≥1 policy within 7 days</td>
            <td>&gt;55%</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">Core "aha moment" completion</td>
          </tr>
          <tr>
            <td style="color:var(--teal-light);">Engagement</td>
            <td>MAU / registered users ratio</td>
            <td>&gt;40%</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">Sustained product utility</td>
          </tr>
          <tr>
            <td style="color:var(--teal-light);">Engagement</td>
            <td>Motor Club DAU (daily habit proxy)</td>
            <td>30% of MAU</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">Daily utility = retention flywheel</td>
          </tr>
          <tr>
            <td style="color:var(--amber);">Retention</td>
            <td>D30 retention</td>
            <td>&gt;35%</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">Signal of real habit formation</td>
          </tr>
          <tr>
            <td style="color:var(--amber);">Retention</td>
            <td>Policy renewal rate via app</td>
            <td>&gt;70%</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">Proves portfolio ownership value</td>
          </tr>
          <tr>
            <td style="color:var(--coral);">Revenue</td>
            <td>Free-to-Pro conversion rate</td>
            <td>5–8%</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">Core new revenue stream metric</td>
          </tr>
          <tr>
            <td style="color:var(--coral);">Revenue</td>
            <td>Revenue per MAU</td>
            <td>₹85+</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">Blended monetisation efficiency</td>
          </tr>
          <tr>
            <td style="color:var(--coral);">Revenue</td>
            <td>B2B ARR (SME segment)</td>
            <td>₹1.5Cr</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">New enterprise revenue line</td>
          </tr>
          <tr>
            <td style="color:#c4b5fd;">Trust</td>
            <td>App Store rating</td>
            <td>&gt;4.3 ★</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">Real-time trust signal</td>
          </tr>
          <tr>
            <td style="color:#c4b5fd;">Trust</td>
            <td>NPS post-claim assistance</td>
            <td>&gt;60</td>
            <td style="font-family:inherit;font-size:13px;color:var(--text-muted);">Measures outcome that matters most</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="insight-box">
      <h3>The one insight that changes everything</h3>
      <p>Own the claim moment — that's where loyalty and revenue collide. Claims are the most high-anxiety, high-involvement event in any user's insurance life. Today, CoverSure offers advisory but not in-app claims management. The insurtechs that own the claims experience — helping users file, track, and resolve claims — become irreplaceable. Every rupee of future CoverSure revenue, whether B2C Pro subscriptions, B2B Teams contracts, or API licensing, will be easier to close once users have experienced CoverSure actually coming through for them when it mattered most. <strong style="color:var(--amber-light);">Build claims first. Everything else follows.</strong></p>
    </div>
  </section>

</main>

<!-- FOOTER -->
<footer>
  <div>CoverSure PM Case Study · Built as a strategic analysis exercise · 2025</div>
  <div>Claycove23 Insurance Tech Pvt. Ltd. · IRDAI CA0894</div>
</footer>

<script>
  // Intersection observer for section reveals
  const sections = document.querySelectorAll('.section');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.08 });
  sections.forEach(s => observer.observe(s));

  // Timeline item stagger
  const tlItems = document.querySelectorAll('.tl-item');
  const tlObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const items = entry.target.closest('.timeline').querySelectorAll('.tl-item');
        items.forEach((item, i) => {
          setTimeout(() => item.classList.add('tl-visible'), i * 100);
        });
        tlObserver.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1 });

  const timelines = document.querySelectorAll('.timeline');
  timelines.forEach(tl => {
    const first = tl.querySelector('.tl-item');
    if (first) tlObserver.observe(first);
  });

  // Active nav link
  const navLinks = document.querySelectorAll('.nav-links a');
  const sectionEls = document.querySelectorAll('section[id]');

  window.addEventListener('scroll', () => {
    let current = '';
    sectionEls.forEach(s => {
      if (window.scrollY >= s.offsetTop - 80) current = s.id;
    });
    navLinks.forEach(a => {
      a.style.color = a.getAttribute('href') === '#' + current
        ? 'var(--teal-light)'
        : '';
    });
  });
</script>
</body>
</html>
