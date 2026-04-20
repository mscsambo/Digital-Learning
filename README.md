<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Learnify — Modern Learning Platform</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet">
<style>
  :root {
    --bg-deep:    #080c14;
    --bg-mid:     #0d1320;
    --bg-card:    #111827;
    --bg-glass:   rgba(255,255,255,0.04);
    --border:     rgba(255,255,255,0.08);
    --accent:     #00e5a0;
    --accent2:    #6c63ff;
    --accent3:    #ff6b6b;
    --accent4:    #f9c74f;
    --text-hi:    #f1f5f9;
    --text-mid:   #94a3b8;
    --text-lo:    #475569;
    --radius-lg:  18px;
    --radius-md:  12px;
    --radius-sm:  8px;
    --sidebar-w:  260px;
    --topbar-h:   70px;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg-deep);
    color: var(--text-hi);
    min-height: 100vh;
    display: flex;
    overflow-x: hidden;
  }

  /* ── SIDEBAR ── */
  .sidebar {
    width: var(--sidebar-w);
    background: var(--bg-mid);
    border-right: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    position: fixed;
    top: 0; left: 0; bottom: 0;
    z-index: 100;
    padding: 28px 0;
    transition: transform .3s ease;
  }

  .logo {
    display: flex; align-items: center; gap: 10px;
    padding: 0 24px 28px;
    border-bottom: 1px solid var(--border);
  }
  .logo-icon {
    width: 36px; height: 36px;
    background: var(--accent);
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px;
  }
  .logo-text {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 20px;
    letter-spacing: -0.5px;
    color: var(--text-hi);
  }
  .logo-text span { color: var(--accent); }

  .nav-section { padding: 20px 16px 0; }
  .nav-label {
    font-size: 10px;
    font-weight: 500;
    letter-spacing: 1.2px;
    text-transform: uppercase;
    color: var(--text-lo);
    padding: 0 8px;
    margin-bottom: 6px;
  }

  .nav-item {
    display: flex; align-items: center; gap: 12px;
    padding: 11px 12px;
    border-radius: var(--radius-sm);
    cursor: pointer;
    transition: all .2s;
    color: var(--text-mid);
    font-size: 14px;
    font-weight: 400;
    position: relative;
    margin-bottom: 2px;
    text-decoration: none;
  }
  .nav-item:hover { background: var(--bg-glass); color: var(--text-hi); }
  .nav-item.active {
    background: rgba(0,229,160,0.12);
    color: var(--accent);
    font-weight: 500;
  }
  .nav-item.active::before {
    content: '';
    position: absolute;
    left: 0; top: 50%;
    transform: translateY(-50%);
    width: 3px; height: 60%;
    background: var(--accent);
    border-radius: 0 4px 4px 0;
  }
  .nav-icon { font-size: 17px; width: 20px; text-align: center; }
  .nav-badge {
    margin-left: auto;
    background: var(--accent3);
    color: #fff;
    font-size: 10px;
    font-weight: 600;
    padding: 2px 7px;
    border-radius: 99px;
  }

  .sidebar-footer {
    margin-top: auto;
    padding: 20px 16px 0;
    border-top: 1px solid var(--border);
  }
  .user-pill {
    display: flex; align-items: center; gap: 12px;
    padding: 12px;
    border-radius: var(--radius-md);
    cursor: pointer;
    transition: background .2s;
  }
  .user-pill:hover { background: var(--bg-glass); }
  .user-avatar {
    width: 36px; height: 36px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--accent2), var(--accent));
    display: flex; align-items: center; justify-content: center;
    font-weight: 700; font-size: 14px; color: #fff;
    flex-shrink: 0;
  }
  .user-info { flex: 1; min-width: 0; }
  .user-name { font-size: 13px; font-weight: 500; color: var(--text-hi); }
  .user-role { font-size: 11px; color: var(--text-lo); }

  /* ── MAIN ── */
  .main {
    margin-left: var(--sidebar-w);
    flex: 1;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  /* ── TOPBAR ── */
  .topbar {
    height: var(--topbar-h);
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center;
    padding: 0 36px;
    gap: 16px;
    position: sticky; top: 0;
    background: rgba(8,12,20,0.85);
    backdrop-filter: blur(16px);
    z-index: 50;
  }
  .topbar-title {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 20px;
    letter-spacing: -0.3px;
    flex: 1;
  }
  .search-bar {
    display: flex; align-items: center; gap: 10px;
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 99px;
    padding: 9px 18px;
    width: 280px;
    transition: border-color .2s;
  }
  .search-bar:focus-within { border-color: var(--accent); }
  .search-bar input {
    background: none; border: none; outline: none;
    color: var(--text-hi);
    font-family: 'DM Sans', sans-serif;
    font-size: 13.5px;
    width: 100%;
  }
  .search-bar input::placeholder { color: var(--text-lo); }
  .search-icon { color: var(--text-lo); font-size: 15px; }

  .topbar-actions { display: flex; align-items: center; gap: 8px; }
  .icon-btn {
    width: 38px; height: 38px;
    border-radius: 50%;
    border: 1px solid var(--border);
    background: var(--bg-card);
    display: flex; align-items: center; justify-content: center;
    cursor: pointer;
    font-size: 16px;
    color: var(--text-mid);
    transition: all .2s;
    position: relative;
  }
  .icon-btn:hover { border-color: var(--accent); color: var(--accent); }
  .notif-dot {
    width: 7px; height: 7px;
    background: var(--accent3);
    border-radius: 50%;
    position: absolute; top: 6px; right: 6px;
    border: 1.5px solid var(--bg-deep);
  }

  /* ── CONTENT ── */
  .content { padding: 36px; flex: 1; }

  /* ── HERO BANNER ── */
  .hero {
    border-radius: var(--radius-lg);
    background: linear-gradient(120deg, #0f2027, #203a43, #2c5364);
    padding: 40px 44px;
    display: flex; align-items: center; justify-content: space-between;
    margin-bottom: 36px;
    position: relative;
    overflow: hidden;
  }
  .hero::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(ellipse at 80% 50%, rgba(0,229,160,0.15) 0%, transparent 65%);
    pointer-events: none;
  }
  .hero-orb {
    position: absolute; right: 200px; top: -60px;
    width: 240px; height: 240px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(108,99,255,0.3), transparent 70%);
    pointer-events: none;
  }
  .hero-text h2 {
    font-family: 'Syne', sans-serif;
    font-size: 30px; font-weight: 800;
    line-height: 1.2; margin-bottom: 8px;
    letter-spacing: -0.5px;
  }
  .hero-text h2 span { color: var(--accent); }
  .hero-text p { color: var(--text-mid); font-size: 15px; max-width: 420px; line-height: 1.6; }
  .hero-stats {
    display: flex; gap: 32px;
    position: relative; z-index: 1;
  }
  .h-stat { text-align: center; }
  .h-stat-val {
    font-family: 'Syne', sans-serif;
    font-size: 32px; font-weight: 800;
    color: var(--accent);
    line-height: 1;
  }
  .h-stat-lbl { font-size: 12px; color: var(--text-mid); margin-top: 4px; }

  /* ── SECTION HEADING ── */
  .section-head {
    display: flex; align-items: center; justify-content: space-between;
    margin-bottom: 20px;
  }
  .section-head h3 {
    font-family: 'Syne', sans-serif;
    font-size: 18px; font-weight: 700;
    letter-spacing: -0.3px;
  }
  .see-all {
    font-size: 13px; color: var(--accent);
    cursor: pointer; text-decoration: none;
    font-weight: 500;
    transition: opacity .2s;
  }
  .see-all:hover { opacity: .7; }

  /* ── STATS STRIP ── */
  .stats-strip {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
    margin-bottom: 36px;
  }
  .stat-card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: var(--radius-lg);
    padding: 22px 24px;
    display: flex; align-items: center; gap: 16px;
    transition: border-color .2s, transform .2s;
    animation: fadeUp .5s both;
  }
  .stat-card:hover { border-color: rgba(255,255,255,0.16); transform: translateY(-2px); }
  .stat-icon-wrap {
    width: 48px; height: 48px;
    border-radius: var(--radius-md);
    display: flex; align-items: center; justify-content: center;
    font-size: 22px; flex-shrink: 0;
  }
  .si-green  { background: rgba(0,229,160,0.12); }
  .si-purple { background: rgba(108,99,255,0.12); }
  .si-red    { background: rgba(255,107,107,0.12); }
  .si-yellow { background: rgba(249,199,79,0.12); }
  .stat-val {
    font-family: 'Syne', sans-serif;
    font-size: 26px; font-weight: 800;
    letter-spacing: -0.5px; line-height: 1;
    margin-bottom: 4px;
  }
  .stat-lbl { font-size: 12.5px; color: var(--text-mid); }
  .stat-delta {
    font-size: 11.5px; color: var(--accent);
    margin-top: 2px; font-weight: 500;
  }
  .stat-delta.down { color: var(--accent3); }

  /* ── COURSE GRID ── */
  .course-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    margin-bottom: 36px;
  }
  .course-card {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: var(--radius-lg);
    overflow: hidden;
    cursor: pointer;
    transition: transform .25s, box-shadow .25s, border-color .25s;
    animation: fadeUp .6s both;
  }
  .course-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 60px rgba(0,0,0,0.4);
    border-color: rgba(255,255,255,0.14);
  }
  .course-thumb {
    height: 160px;
    display: flex; align-items: center; justify-content: center;
    font-size: 52px;
    position: relative;
    overflow: hidden;
  }
  .ct-1 { background: linear-gradient(135deg, #0f2027, #2c5364); }
  .ct-2 { background: linear-gradient(135deg, #1a0533, #6c1fd1); }
  .ct-3 { background: linear-gradient(135deg, #1a1000, #7d5a00); }
  .ct-4 { background: linear-gradient(135deg, #001a15, #005938); }
  .ct-5 { background: linear-gradient(135deg, #1a0008, #8a0022); }
  .ct-6 { background: linear-gradient(135deg, #050050, #1400a3); }
  .course-thumb::after {
    content: '';
    position: absolute; inset: 0;
    background: rgba(0,0,0,.1);
  }
  .badge-level {
    position: absolute; top: 12px; left: 12px;
    background: rgba(0,0,0,0.5);
    backdrop-filter: blur(8px);
    border: 1px solid rgba(255,255,255,0.15);
    border-radius: 99px;
    font-size: 10px; font-weight: 600;
    padding: 3px 10px;
    color: var(--text-hi);
    z-index: 1;
    letter-spacing: .5px;
  }
  .badge-progress {
    position: absolute; bottom: 0; left: 0; right: 0;
    height: 3px;
    background: rgba(255,255,255,0.1);
    z-index: 2;
  }
  .badge-progress-fill {
    height: 100%;
    background: var(--accent);
    border-radius: 0 2px 2px 0;
  }

  .course-body { padding: 18px 20px; }
  .course-cat {
    font-size: 10.5px; font-weight: 600;
    text-transform: uppercase; letter-spacing: 1px;
    margin-bottom: 6px;
  }
  .course-title {
    font-family: 'Syne', sans-serif;
    font-size: 15.5px; font-weight: 700;
    line-height: 1.35; margin-bottom: 10px;
    letter-spacing: -0.2px;
  }
  .course-meta {
    display: flex; align-items: center; gap: 14px;
    font-size: 12px; color: var(--text-lo);
  }
  .course-meta-item { display: flex; align-items: center; gap: 5px; }
  .course-footer {
    display: flex; align-items: center; justify-content: space-between;
    padding: 12px 20px 16px;
    border-top: 1px solid var(--border);
  }
  .instructor { display: flex; align-items: center; gap: 8px; }
  .inst-av {
    width: 26px; height: 26px;
    border-radius: 50%;
    font-size: 11px; font-weight: 700;
    color: #fff;
    display: flex; align-items: center; justify-content: center;
  }
  .inst-name { font-size: 12px; color: var(--text-mid); }
  .course-rating { display: flex; align-items: center; gap: 4px; font-size: 12px; color: var(--accent4); }

  /* ── TWO-COL LAYOUT ── */
  .two-col { display: grid; grid-template-columns: 1fr 340px; gap: 24px; margin-bottom: 36px; }

  /* ── ACTIVITY PANEL ── */
  .panel {
    background: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: var(--radius-lg);
    padding: 24px;
  }
  .panel-title {
    font-family: 'Syne', sans-serif;
    font-size: 16px; font-weight: 700;
    margin-bottom: 20px;
  }

  .activity-item {
    display: flex; align-items: flex-start; gap: 14px;
    padding: 12px 0;
    border-bottom: 1px solid var(--border);
  }
  .activity-item:last-child { border-bottom: none; }
  .act-dot {
    width: 10px; height: 10px;
    border-radius: 50%;
    margin-top: 4px; flex-shrink: 0;
  }
  .act-text { font-size: 13.5px; color: var(--text-mid); line-height: 1.5; }
  .act-text strong { color: var(--text-hi); font-weight: 500; }
  .act-time { font-size: 11px; color: var(--text-lo); margin-top: 3px; }

  /* ── LEADERBOARD ── */
  .lb-item {
    display: flex; align-items: center; gap: 14px;
    padding: 11px 0;
    border-bottom: 1px solid var(--border);
    transition: background .2s;
  }
  .lb-item:last-child { border-bottom: none; }
  .lb-rank {
    font-family: 'Syne', sans-serif;
    font-size: 15px; font-weight: 800;
    width: 26px; text-align: center;
    color: var(--text-lo);
    flex-shrink: 0;
  }
  .lb-rank.gold   { color: #ffd700; }
  .lb-rank.silver { color: #c0c0c0; }
  .lb-rank.bronze { color: #cd7f32; }
  .lb-av {
    width: 34px; height: 34px;
    border-radius: 50%;
    font-size: 13px; font-weight: 700; color: #fff;
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0;
  }
  .lb-info { flex: 1; min-width: 0; }
  .lb-name { font-size: 13.5px; font-weight: 500; }
  .lb-pts {
    font-family: 'Syne', sans-serif;
    font-size: 14px; font-weight: 700;
    color: var(--accent);
  }

  /* ── PROGRESS BARS ── */
  .progress-list { display: flex; flex-direction: column; gap: 18px; }
  .prog-item {}
  .prog-head { display: flex; justify-content: space-between; margin-bottom: 8px; }
  .prog-name { font-size: 13.5px; font-weight: 500; }
  .prog-pct { font-size: 13px; font-weight: 700; color: var(--accent); }
  .prog-track {
    height: 6px; background: rgba(255,255,255,0.07);
    border-radius: 99px; overflow: hidden;
  }
  .prog-fill {
    height: 100%; border-radius: 99px;
    background: linear-gradient(90deg, var(--accent2), var(--accent));
    transition: width 1s cubic-bezier(.4,0,.2,1);
  }

  /* ── UPCOMING ── */
  .upcoming-item {
    display: flex; gap: 14px; align-items: center;
    padding: 13px 0;
    border-bottom: 1px solid var(--border);
  }
  .upcoming-item:last-child { border-bottom: none; }
  .date-block {
    width: 44px; height: 50px;
    background: var(--bg-glass);
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    flex-shrink: 0;
  }
  .date-d {
    font-family: 'Syne', sans-serif;
    font-size: 18px; font-weight: 800;
    line-height: 1; color: var(--accent);
  }
  .date-m { font-size: 10px; color: var(--text-lo); font-weight: 500; text-transform: uppercase; }
  .upcoming-info { flex: 1; }
  .upcoming-title { font-size: 13.5px; font-weight: 500; margin-bottom: 3px; }
  .upcoming-sub { font-size: 12px; color: var(--text-lo); }
  .tag-pill {
    font-size: 10.5px; padding: 3px 9px;
    border-radius: 99px; font-weight: 600;
    letter-spacing: .3px;
  }
  .tag-live { background: rgba(255,107,107,0.15); color: var(--accent3); }
  .tag-quiz { background: rgba(249,199,79,0.15); color: var(--accent4); }
  .tag-new  { background: rgba(0,229,160,0.15);  color: var(--accent); }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity:0; transform: translateY(20px); }
    to   { opacity:1; transform: translateY(0); }
  }

  .stat-card:nth-child(1) { animation-delay:.05s }
  .stat-card:nth-child(2) { animation-delay:.1s }
  .stat-card:nth-child(3) { animation-delay:.15s }
  .stat-card:nth-child(4) { animation-delay:.2s }
  .course-card:nth-child(1) { animation-delay:.1s }
  .course-card:nth-child(2) { animation-delay:.15s }
  .course-card:nth-child(3) { animation-delay:.2s }
  .course-card:nth-child(4) { animation-delay:.25s }
  .course-card:nth-child(5) { animation-delay:.3s }
  .course-card:nth-child(6) { animation-delay:.35s }

  /* ── SCROLLBAR ── */
  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.1); border-radius: 99px; }
  ::-webkit-scrollbar-thumb:hover { background: rgba(255,255,255,0.2); }

  /* ── CTA BUTTON ── */
  .btn-primary {
    background: var(--accent);
    color: #080c14;
    border: none;
    padding: 11px 22px;
    border-radius: 99px;
    font-family: 'DM Sans', sans-serif;
    font-size: 13.5px; font-weight: 600;
    cursor: pointer;
    transition: opacity .2s, transform .15s;
    display: inline-flex; align-items: center; gap: 7px;
  }
  .btn-primary:hover { opacity: .85; transform: scale(1.03); }

  .btn-ghost {
    background: var(--bg-glass);
    border: 1px solid var(--border);
    color: var(--text-mid);
    padding: 11px 22px;
    border-radius: 99px;
    font-family: 'DM Sans', sans-serif;
    font-size: 13.5px; font-weight: 500;
    cursor: pointer;
    transition: border-color .2s, color .2s;
  }
  .btn-ghost:hover { border-color: var(--accent); color: var(--accent); }

  /* ── TABS ── */
  .tabs { display: flex; gap: 4px; background: var(--bg-card); border: 1px solid var(--border); border-radius: 99px; padding: 4px; width: fit-content; margin-bottom: 24px; }
  .tab {
    padding: 8px 20px;
    border-radius: 99px;
    font-size: 13px;
    cursor: pointer;
    color: var(--text-lo);
    transition: all .2s;
    font-weight: 500;
  }
  .tab.active { background: var(--accent); color: #080c14; font-weight: 600; }

  /* ── OVERVIEW CHIP ── */
  .chip {
    display: inline-flex; align-items: center; gap: 6px;
    background: rgba(0,229,160,0.1);
    border: 1px solid rgba(0,229,160,0.2);
    border-radius: 99px;
    padding: 5px 12px;
    font-size: 12px; color: var(--accent);
    font-weight: 500;
    margin-bottom: 14px;
  }
  .chip-dot { width: 6px; height: 6px; background: var(--accent); border-radius: 50%; animation: pulse 2s infinite; }
  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:.3} }

  .cert-card {
    background: linear-gradient(135deg, rgba(108,99,255,0.15), rgba(0,229,160,0.1));
    border: 1px solid rgba(108,99,255,0.25);
    border-radius: var(--radius-lg);
    padding: 22px 24px;
    display: flex; align-items: center; gap: 18px;
    margin-top: 20px;
  }
  .cert-icon { font-size: 36px; }
  .cert-title { font-family: 'Syne', sans-serif; font-size: 15px; font-weight: 700; margin-bottom: 4px; }
  .cert-sub { font-size: 12.5px; color: var(--text-mid); }

  /* ── MOBILE ── */
  .hamburger { display: none; font-size: 22px; cursor: pointer; color: var(--text-hi); }
  @media (max-width: 1100px) {
    .course-grid { grid-template-columns: repeat(2,1fr); }
    .stats-strip { grid-template-columns: repeat(2,1fr); }
  }
  @media (max-width: 860px) {
    .sidebar { transform: translateX(-100%); }
    .sidebar.open { transform: translateX(0); }
    .main { margin-left: 0; }
    .hamburger { display: flex; }
    .two-col { grid-template-columns: 1fr; }
    .hero-stats { display: none; }
    .content { padding: 20px; }
  }
  @media (max-width: 600px) {
    .course-grid { grid-template-columns: 1fr; }
    .stats-strip { grid-template-columns: 1fr 1fr; }
    .search-bar { display: none; }
  }
</style>
</head>
<body>

<!-- ── SIDEBAR ── -->
<aside class="sidebar" id="sidebar">
  <div class="logo">
    <div class="logo-icon">📚</div>
    <span class="logo-text">Learn<span>ify</span></span>
  </div>

  <div class="nav-section">
    <div class="nav-label">Menu</div>
    <a class="nav-item active" onclick="setPage('dashboard')">
      <span class="nav-icon">⊞</span> Dashboard
    </a>
    <a class="nav-item" onclick="setPage('courses')">
      <span class="nav-icon">🎓</span> My Courses
    </a>
    <a class="nav-item" onclick="setPage('explore')">
      <span class="nav-icon">🔭</span> Explore
    </a>
    <a class="nav-item" onclick="setPage('progress')">
      <span class="nav-icon">📈</span> Progress
    </a>
    <a class="nav-item" onclick="setPage('assignments')">
      <span class="nav-icon">📝</span> Assignments
      <span class="nav-badge">3</span>
    </a>
  </div>

  <div class="nav-section" style="margin-top:16px">
    <div class="nav-label">Community</div>
    <a class="nav-item" onclick="setPage('forum')">
      <span class="nav-icon">💬</span> Forum
    </a>
    <a class="nav-item" onclick="setPage('leaderboard')">
      <span class="nav-icon">🏆</span> Leaderboard
    </a>
    <a class="nav-item" onclick="setPage('events')">
      <span class="nav-icon">📅</span> Live Events
      <span class="nav-badge">2</span>
    </a>
  </div>

  <div class="nav-section" style="margin-top:16px">
    <div class="nav-label">Account</div>
    <a class="nav-item" onclick="setPage('profile')">
      <span class="nav-icon">👤</span> Profile
    </a>
    <a class="nav-item" onclick="setPage('settings')">
      <span class="nav-icon">⚙️</span> Settings
    </a>
  </div>

  <div class="sidebar-footer">
    <div class="user-pill">
      <div class="user-avatar">AJ</div>
      <div class="user-info">
        <div class="user-name">Alex Johnson</div>
        <div class="user-role">Pro Learner · Level 12</div>
      </div>
      <span style="color:var(--text-lo);font-size:14px;">⋯</span>
    </div>
  </div>
</aside>

<!-- ── MAIN ── -->
<div class="main">
  <!-- TOPBAR -->
  <header class="topbar">
    <span class="hamburger" onclick="toggleSidebar()">☰</span>
    <h1 class="topbar-title" id="page-title">Dashboard</h1>

    <div class="search-bar">
      <span class="search-icon">🔍</span>
      <input type="text" placeholder="Search courses, topics…">
    </div>

    <div class="topbar-actions">
      <div class="icon-btn" title="Notifications">
        🔔
        <span class="notif-dot"></span>
      </div>
      <div class="icon-btn" title="Messages">💌</div>
      <div class="icon-btn" title="Achievements">⚡</div>
    </div>
  </header>

  <!-- CONTENT -->
  <main class="content" id="content">

    <!-- ── HERO ── -->
    <div class="hero">
      <div class="hero-orb"></div>
      <div class="hero-text">
        <div class="chip"><span class="chip-dot"></span> 3 courses in progress</div>
        <h2>Welcome back,<br><span>Alex! 👋</span></h2>
        <p>You've been on a 7-day streak! Keep it up — you're in the top 5% of learners this month.</p>
        <div style="display:flex;gap:12px;margin-top:22px;">
          <button class="btn-primary" onclick="setPage('courses')">▶ Continue Learning</button>
          <button class="btn-ghost" onclick="setPage('explore')">Explore Courses</button>
        </div>
      </div>
      <div class="hero-stats">
        <div class="h-stat">
          <div class="h-stat-val">7</div>
          <div class="h-stat-lbl">Day Streak 🔥</div>
        </div>
        <div class="h-stat">
          <div class="h-stat-val">2,840</div>
          <div class="h-stat-lbl">XP Points</div>
        </div>
        <div class="h-stat">
          <div class="h-stat-val">14</div>
          <div class="h-stat-lbl">Completed</div>
        </div>
      </div>
    </div>

    <!-- ── STATS STRIP ── -->
    <div class="stats-strip">
      <div class="stat-card">
        <div class="stat-icon-wrap si-green">📘</div>
        <div>
          <div class="stat-val">18</div>
          <div class="stat-lbl">Enrolled Courses</div>
          <div class="stat-delta">↑ 3 this month</div>
        </div>
      </div>
      <div class="stat-card">
        <div class="stat-icon-wrap si-purple">⏱</div>
        <div>
          <div class="stat-val">142h</div>
          <div class="stat-lbl">Learning Hours</div>
          <div class="stat-delta">↑ 12h this week</div>
        </div>
      </div>
      <div class="stat-card">
        <div class="stat-icon-wrap si-yellow">🏅</div>
        <div>
          <div class="stat-val">9</div>
          <div class="stat-lbl">Certificates Earned</div>
          <div class="stat-delta">↑ 2 new</div>
        </div>
      </div>
      <div class="stat-card">
        <div class="stat-icon-wrap si-red">📊</div>
        <div>
          <div class="stat-val">#42</div>
          <div class="stat-lbl">Global Rank</div>
          <div class="stat-delta down">↓ 3 spots</div>
        </div>
      </div>
    </div>

    <!-- ── COURSE GRID ── -->
    <div class="section-head">
      <h3>Continue Learning</h3>
      <a class="see-all" onclick="setPage('courses')">View all →</a>
    </div>

    <div class="tabs" id="course-tabs">
      <div class="tab active" onclick="switchTab(this,'In Progress')">In Progress</div>
      <div class="tab" onclick="switchTab(this,'Completed')">Completed</div>
      <div class="tab" onclick="switchTab(this,'Saved')">Saved</div>
    </div>

    <div class="course-grid" id="course-grid">

      <div class="course-card" onclick="alert('Opening: Advanced Python & Machine Learning')">
        <div class="course-thumb ct-2">
          🐍
          <span class="badge-level">Advanced</span>
          <div class="badge-progress"><div class="badge-progress-fill" style="width:72%"></div></div>
        </div>
        <div class="course-body">
          <div class="course-cat" style="color:var(--accent2)">Python · ML</div>
          <div class="course-title">Advanced Python & Machine Learning</div>
          <div class="course-meta">
            <span class="course-meta-item">📖 48 lessons</span>
            <span class="course-meta-item">⏱ 18h 30m</span>
            <span class="course-meta-item" style="color:var(--accent)">72%</span>
          </div>
        </div>
        <div class="course-footer">
          <div class="instructor">
            <div class="inst-av" style="background:linear-gradient(135deg,#667eea,#764ba2)">SM</div>
            <span class="inst-name">Sarah Mitchell</span>
          </div>
          <div class="course-rating">★ 4.9</div>
        </div>
      </div>

      <div class="course-card" onclick="alert('Opening: React & Next.js Mastery')">
        <div class="course-thumb ct-1">
          ⚛️
          <span class="badge-level">Intermediate</span>
          <div class="badge-progress"><div class="badge-progress-fill" style="width:45%"></div></div>
        </div>
        <div class="course-body">
          <div class="course-cat" style="color:#61dafb">Frontend · React</div>
          <div class="course-title">React & Next.js Mastery 2024</div>
          <div class="course-meta">
            <span class="course-meta-item">📖 62 lessons</span>
            <span class="course-meta-item">⏱ 24h</span>
            <span class="course-meta-item" style="color:var(--accent)">45%</span>
          </div>
        </div>
        <div class="course-footer">
          <div class="instructor">
            <div class="inst-av" style="background:linear-gradient(135deg,#f093fb,#f5576c)">JL</div>
            <span class="inst-name">James Liu</span>
          </div>
          <div class="course-rating">★ 4.8</div>
        </div>
      </div>

      <div class="course-card" onclick="alert('Opening: Data Visualization with D3.js')">
        <div class="course-thumb ct-4">
          📊
          <span class="badge-level">Beginner</span>
          <div class="badge-progress"><div class="badge-progress-fill" style="width:28%"></div></div>
        </div>
        <div class="course-body">
          <div class="course-cat" style="color:var(--accent)">Data · Visualization</div>
          <div class="course-title">Data Visualization with D3.js</div>
          <div class="course-meta">
            <span class="course-meta-item">📖 35 lessons</span>
            <span class="course-meta-item">⏱ 12h</span>
            <span class="course-meta-item" style="color:var(--accent)">28%</span>
          </div>
        </div>
        <div class="course-footer">
          <div class="instructor">
            <div class="inst-av" style="background:linear-gradient(135deg,#4facfe,#00f2fe)">MK</div>
            <span class="inst-name">Maria Khan</span>
          </div>
          <div class="course-rating">★ 4.7</div>
        </div>
      </div>

      <div class="course-card" onclick="alert('Opening: Cloud Architecture on AWS')">
        <div class="course-thumb ct-3">
          ☁️
          <span class="badge-level">Advanced</span>
          <div class="badge-progress"><div class="badge-progress-fill" style="width:60%"></div></div>
        </div>
        <div class="course-body">
          <div class="course-cat" style="color:var(--accent4)">Cloud · AWS</div>
          <div class="course-title">Cloud Architecture on AWS</div>
          <div class="course-meta">
            <span class="course-meta-item">📖 54 lessons</span>
            <span class="course-meta-item">⏱ 20h</span>
            <span class="course-meta-item" style="color:var(--accent)">60%</span>
          </div>
        </div>
        <div class="course-footer">
          <div class="instructor">
            <div class="inst-av" style="background:linear-gradient(135deg,#fa8231,#f7b731)">TN</div>
            <span class="inst-name">Tom Nakamura</span>
          </div>
          <div class="course-rating">★ 4.9</div>
        </div>
      </div>

      <div class="course-card" onclick="alert('Opening: UI/UX Design Fundamentals')">
        <div class="course-thumb ct-5">
          🎨
          <span class="badge-level">Beginner</span>
          <div class="badge-progress"><div class="badge-progress-fill" style="width:15%"></div></div>
        </div>
        <div class="course-body">
          <div class="course-cat" style="color:var(--accent3)">Design · UX</div>
          <div class="course-title">UI/UX Design Fundamentals</div>
          <div class="course-meta">
            <span class="course-meta-item">📖 40 lessons</span>
            <span class="course-meta-item">⏱ 16h</span>
            <span class="course-meta-item" style="color:var(--accent)">15%</span>
          </div>
        </div>
        <div class="course-footer">
          <div class="instructor">
            <div class="inst-av" style="background:linear-gradient(135deg,#a18cd1,#fbc2eb)">ER</div>
            <span class="inst-name">Elena Ross</span>
          </div>
          <div class="course-rating">★ 4.6</div>
        </div>
      </div>

      <div class="course-card" onclick="alert('Opening: Kubernetes & DevOps')">
        <div class="course-thumb ct-6">
          🚀
          <span class="badge-level">Advanced</span>
          <div class="badge-progress"><div class="badge-progress-fill" style="width:5%"></div></div>
        </div>
        <div class="course-body">
          <div class="course-cat" style="color:#7b9cf7">DevOps · K8s</div>
          <div class="course-title">Kubernetes & Modern DevOps</div>
          <div class="course-meta">
            <span class="course-meta-item">📖 70 lessons</span>
            <span class="course-meta-item">⏱ 28h</span>
            <span class="course-meta-item" style="color:var(--accent)">5%</span>
          </div>
        </div>
        <div class="course-footer">
          <div class="instructor">
            <div class="inst-av" style="background:linear-gradient(135deg,#43e97b,#38f9d7)">DB</div>
            <span class="inst-name">David Berg</span>
          </div>
          <div class="course-rating">★ 4.8</div>
        </div>
      </div>

    </div>

    <!-- ── TWO-COL ── -->
    <div class="two-col">

      <!-- LEFT: LEARNING PROGRESS + UPCOMING -->
      <div style="display:flex;flex-direction:column;gap:24px;">

        <div class="panel">
          <div class="panel-title">Skill Progress</div>
          <div class="progress-list">
            <div class="prog-item">
              <div class="prog-head">
                <span class="prog-name">Python & Data Science</span>
                <span class="prog-pct">82%</span>
              </div>
              <div class="prog-track"><div class="prog-fill" style="width:82%"></div></div>
            </div>
            <div class="prog-item">
              <div class="prog-head">
                <span class="prog-name">Frontend Development</span>
                <span class="prog-pct">65%</span>
              </div>
              <div class="prog-track"><div class="prog-fill" style="width:65%"></div></div>
            </div>
            <div class="prog-item">
              <div class="prog-head">
                <span class="prog-name">Cloud & Infrastructure</span>
                <span class="prog-pct">48%</span>
              </div>
              <div class="prog-track"><div class="prog-fill" style="width:48%"></div></div>
            </div>
            <div class="prog-item">
              <div class="prog-head">
                <span class="prog-name">UI/UX Design</span>
                <span class="prog-pct">30%</span>
              </div>
              <div class="prog-track"><div class="prog-fill" style="width:30%"></div></div>
            </div>
            <div class="prog-item">
              <div class="prog-head">
                <span class="prog-name">Machine Learning</span>
                <span class="prog-pct">57%</span>
              </div>
              <div class="prog-track"><div class="prog-fill" style="width:57%"></div></div>
            </div>
          </div>

          <div class="cert-card" style="margin-top:24px">
            <div class="cert-icon">🎓</div>
            <div>
              <div class="cert-title">Python Fundamentals — Certificate Ready!</div>
              <div class="cert-sub">You've completed all requirements. Claim your certificate now.</div>
            </div>
            <button class="btn-primary" style="flex-shrink:0" onclick="alert('🎉 Certificate claimed!')">Claim</button>
          </div>
        </div>

        <!-- UPCOMING EVENTS -->
        <div class="panel">
          <div class="panel-title">Upcoming Events</div>
          <div class="upcoming-item">
            <div class="date-block"><div class="date-d">22</div><div class="date-m">Apr</div></div>
            <div class="upcoming-info">
              <div class="upcoming-title">Live Q&A: Machine Learning Interview Prep</div>
              <div class="upcoming-sub">2:00 PM • Sarah Mitchell • 240 attending</div>
            </div>
            <span class="tag-pill tag-live">LIVE</span>
          </div>
          <div class="upcoming-item">
            <div class="date-block"><div class="date-d">24</div><div class="date-m">Apr</div></div>
            <div class="upcoming-info">
              <div class="upcoming-title">React Mid-Course Assessment</div>
              <div class="upcoming-sub">Quiz • 30 questions • 45 minutes</div>
            </div>
            <span class="tag-pill tag-quiz">QUIZ</span>
          </div>
          <div class="upcoming-item">
            <div class="date-block"><div class="date-d">28</div><div class="date-m">Apr</div></div>
            <div class="upcoming-info">
              <div class="upcoming-title">New Course Launch: GenAI with LangChain</div>
              <div class="upcoming-sub">By James Liu • Early Access</div>
            </div>
            <span class="tag-pill tag-new">NEW</span>
          </div>
          <div class="upcoming-item">
            <div class="date-block"><div class="date-d">01</div><div class="date-m">May</div></div>
            <div class="upcoming-info">
              <div class="upcoming-title">Hackathon: Build with AI APIs</div>
              <div class="upcoming-sub">48hr challenge • $2,000 prize pool</div>
            </div>
            <span class="tag-pill tag-live">EVENT</span>
          </div>
        </div>
      </div>

      <!-- RIGHT: ACTIVITY + LEADERBOARD -->
      <div style="display:flex;flex-direction:column;gap:24px;">

        <!-- LEADERBOARD -->
        <div class="panel">
          <div class="panel-title">🏆 Leaderboard <span style="font-size:12px;color:var(--text-lo);font-family:'DM Sans'">This Week</span></div>
          <div class="lb-item">
            <div class="lb-rank gold">1</div>
            <div class="lb-av" style="background:linear-gradient(135deg,#f093fb,#f5576c)">PK</div>
            <div class="lb-info"><div class="lb-name">Priya Kumar</div><div style="font-size:11px;color:var(--text-lo)">12 courses · 48h</div></div>
            <div class="lb-pts">4,820</div>
          </div>
          <div class="lb-item">
            <div class="lb-rank silver">2</div>
            <div class="lb-av" style="background:linear-gradient(135deg,#43e97b,#38f9d7)">RW</div>
            <div class="lb-info"><div class="lb-name">Ryan Walsh</div><div style="font-size:11px;color:var(--text-lo)">9 courses · 36h</div></div>
            <div class="lb-pts">3,960</div>
          </div>
          <div class="lb-item">
            <div class="lb-rank bronze">3</div>
            <div class="lb-av" style="background:linear-gradient(135deg,#fa8231,#f7b731)">SO</div>
            <div class="lb-info"><div class="lb-name">Sofia Ortega</div><div style="font-size:11px;color:var(--text-lo)">11 courses · 41h</div></div>
            <div class="lb-pts">3,650</div>
          </div>
          <div class="lb-item" style="background:rgba(0,229,160,0.04);border-radius:var(--radius-sm);padding:11px 8px;">
            <div class="lb-rank" style="color:var(--accent)">42</div>
            <div class="lb-av" style="background:linear-gradient(135deg,#667eea,#764ba2)">AJ</div>
            <div class="lb-info"><div class="lb-name">You (Alex)</div><div style="font-size:11px;color:var(--text-lo)">7 courses · 28h</div></div>
            <div class="lb-pts">2,840</div>
          </div>
          <div class="lb-item">
            <div class="lb-rank">43</div>
            <div class="lb-av" style="background:linear-gradient(135deg,#4facfe,#00f2fe)">LM</div>
            <div class="lb-info"><div class="lb-name">Liam Moore</div><div style="font-size:11px;color:var(--text-lo)">6 courses · 22h</div></div>
            <div class="lb-pts">2,710</div>
          </div>
          <div style="text-align:center;margin-top:14px;">
            <a class="see-all" onclick="setPage('leaderboard')">View full leaderboard →</a>
          </div>
        </div>

        <!-- ACTIVITY FEED -->
        <div class="panel">
          <div class="panel-title">Recent Activity</div>
          <div class="activity-item">
            <div class="act-dot" style="background:var(--accent)"></div>
            <div>
              <div class="act-text">Completed <strong>Lesson 34: Neural Networks</strong> in Advanced Python & ML</div>
              <div class="act-time">2 hours ago</div>
            </div>
          </div>
          <div class="activity-item">
            <div class="act-dot" style="background:var(--accent2)"></div>
            <div>
              <div class="act-text">Earned badge <strong>🔥 7-Day Streak</strong></div>
              <div class="act-time">Today, 9:14 AM</div>
            </div>
          </div>
          <div class="activity-item">
            <div class="act-dot" style="background:var(--accent4)"></div>
            <div>
              <div class="act-text">Scored <strong>94% on React Hooks Quiz</strong> — Top 10%!</div>
              <div class="act-time">Yesterday</div>
            </div>
          </div>
          <div class="activity-item">
            <div class="act-dot" style="background:var(--accent3)"></div>
            <div>
              <div class="act-text">Joined <strong>AWS Cloud Architecture</strong> course</div>
              <div class="act-time">2 days ago</div>
            </div>
          </div>
          <div class="activity-item">
            <div class="act-dot" style="background:var(--accent)"></div>
            <div>
              <div class="act-text">Posted answer in <strong>Python Forum</strong> — 12 upvotes</div>
              <div class="act-time">3 days ago</div>
            </div>
          </div>
        </div>

      </div>
    </div>

  </main>
</div>

<script>
  function toggleSidebar() {
    document.getElementById('sidebar').classList.toggle('open');
  }

  const titles = {
    dashboard: 'Dashboard',
    courses: 'My Courses',
    explore: 'Explore',
    progress: 'Progress',
    assignments: 'Assignments',
    forum: 'Forum',
    leaderboard: 'Leaderboard',
    events: 'Live Events',
    profile: 'Profile',
    settings: 'Settings'
  };

  function setPage(page) {
    document.getElementById('page-title').textContent = titles[page] || page;
    document.querySelectorAll('.nav-item').forEach(el => el.classList.remove('active'));
    event && event.target && event.target.closest('.nav-item') && event.target.closest('.nav-item').classList.add('active');
    if (window.innerWidth < 860) document.getElementById('sidebar').classList.remove('open');
  }

  function switchTab(el, label) {
    document.querySelectorAll('#course-tabs .tab').forEach(t => t.classList.remove('active'));
    el.classList.add('active');
    const grid = document.getElementById('course-grid');
    grid.style.opacity = '0';
    grid.style.transform = 'translateY(10px)';
    setTimeout(() => {
      grid.style.transition = 'opacity .3s, transform .3s';
      grid.style.opacity = '1';
      grid.style.transform = 'translateY(0)';
    }, 100);
  }

  // Animate progress bars on load
  window.addEventListener('load', () => {
    document.querySelectorAll('.prog-fill').forEach(fill => {
      const w = fill.style.width;
      fill.style.width = '0';
      setTimeout(() => { fill.style.width = w; }, 400);
    });
  });
</script>
</body>
</html>
