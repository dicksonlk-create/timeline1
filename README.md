# timeline1

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Day Anim 1 — Pulse Glow</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400;1,600;1,700&family=DM+Sans:wght@400;500;600;700&display=swap');
  *{margin:0;padding:0;box-sizing:border-box}
  body{font-family:'DM Sans',sans-serif;color:#1a1a1a}
  .tw{width:100%;max-width:1020px;margin:0 auto;padding:75px 30px 90px}
  .tw-title{font-family:'Playfair Display',serif;font-style:italic;font-size:33px;font-weight:700;text-align:center;color:#0F1923;margin-bottom:6px}
  .tw-sub{font-size:19.5px;color:#888;text-align:center;margin-bottom:60px}

  /* PROGRESS BAR */
  .progress-track{width:100%;height:9px;background:#e5e0d8;border-radius:0;margin-bottom:45px;position:relative;overflow:hidden}
  .progress-fill{height:100%;width:0;border-radius:0;animation:fillBar 12s ease-in-out infinite}
  @keyframes fillBar{0%{width:0;background:#0F1923}30%{width:50%;background:#0F1923}60%{width:85%;background:#D4C28E}80%{width:95%;background:#B8806A}100%{width:100%;background:#B8806A}}
  .progress-dot{position:absolute;top:-4.5px;width:18px;height:18px;border-radius:0;background:#0F1923;animation:dotSlide 12s ease-in-out infinite}
  @keyframes dotSlide{0%{left:0}30%{left:50%}60%{left:85%}80%{left:95%}100%{left:calc(100% - 18px)}}

  /* DAY MARKERS */
  .day-markers{display:flex;justify-content:space-between;margin-bottom:52.5px;padding:0 3px}
  .day-mark{text-align:center}
  .day-mark-num{font-size:15px;font-weight:800;color:#0F1923;letter-spacing:.08em;text-transform:uppercase}
  .day-mark-line{width:1.5px;height:18px;background:#d5cfc5;margin:4.5px auto}

  /* PHASE BLOCK */
  .phase{margin-bottom:27px;position:relative}
  .phase-header{display:flex;align-items:center;gap:18px;margin-bottom:0;background:#0F1923;padding:18px 24px;border-radius:9px 9px 0 0}
  .phase-badge{padding:7.5px 21px;border-radius:6px;font-size:16.5px;font-weight:800;letter-spacing:.08em;text-transform:uppercase;color:#fff;flex-shrink:0}
  .phase-badge.midnight{background:rgba(255,255,255,.15)}
  .phase-badge.gold{background:#D4C28E;color:#1a1a1a}
  .phase-badge.terra{background:#B8806A}
  .phase-name{font-size:22.5px;font-weight:700;color:#fff}
  .phase-day{font-family:'Playfair Display',serif;font-style:italic;font-size:18px;color:#fff;margin-left:auto;padding:6px 18px;border-radius:6px;border:2px solid rgba(255,255,255,.5);animation:dayPulse 2.5s ease-in-out infinite;flex-shrink:0}
  .phase-day span{position:relative;z-index:1}
  @keyframes dayPulse{0%,100%{box-shadow:0 0 5px rgba(255,255,255,.1),0 0 15px rgba(212,194,142,.05);border-color:rgba(255,255,255,.3)}50%{box-shadow:0 0 12px rgba(255,255,255,.4),0 0 30px rgba(212,194,142,.25);border-color:rgba(255,255,255,.7)}}

  .phase-body{border:3px solid;border-radius:9px;background:#fff;overflow:hidden}
  .phase-body.midnight{border-color:#0F1923}
  .phase-body.gold{border-color:#D4C28E}
  .phase-body.terra{border-color:#B8806A}
  .phase-body::before{content:'';display:block;height:6px}
  .phase-body.midnight::before{background:#0F1923}
  .phase-body.gold::before{background:#D4C28E}
  .phase-body.terra::before{background:#B8806A}

  .phase-grid{display:flex;flex-wrap:wrap;gap:0}
  .phase-cell{flex:1;min-width:270px;padding:18px 24px;border-right:1.5px solid rgba(0,0,0,.04);border-bottom:1.5px solid rgba(0,0,0,.04);display:flex;flex-direction:column;align-items:center;text-align:center}
  .phase-cell:last-child{border-right:none}
  .pc-icon{width:42px;height:42px;border-radius:6px;display:flex;align-items:center;justify-content:center;margin-bottom:10px}
  .pc-icon svg{width:21px;height:21px;stroke:#fff}
  .pc-icon.midnight{background:#0F1923}.pc-icon.gold{background:#D4C28E}.pc-icon.terra{background:#B8806A}
  .pc-label{font-size:18px;font-weight:700;color:#1a1a1a}
  .pc-sub{font-size:15px;color:#999;margin-top:3px}

  /* CONNECTOR */
  .phase-conn{display:flex;justify-content:center;height:52.5px;position:relative}
  .phase-conn-line{width:3px;height:100%;background:#d5cfc5}
  .phase-conn-dot{position:absolute;left:50%;transform:translateX(-50%);width:12px;height:12px;border-radius:0;animation:phaseDrop 2s ease-in-out infinite}
  @keyframes phaseDrop{0%{top:-6px;opacity:0}10%{opacity:1}90%{top:calc(100% - 6px);opacity:1}100%{opacity:0}}
  .phase-conn-dot.midnight{background:#0F1923}
  .phase-conn-dot.gold{background:#D4C28E}
  .phase-conn-dot.terra{background:#B8806A}

  /* PARALLEL LABEL */
  .par-label{text-align:center;margin:37.5px 0 22.5px;position:relative}
  .par-label span{font-family:'Playfair Display',serif;font-style:italic;font-size:19.5px;color:#888;background:#fff;padding:0 18px;position:relative;z-index:1}
  .par-label::before{content:'';position:absolute;top:50%;left:0;right:0;height:1.5px;background:#d5cfc5}

  /* 3-COL PARALLEL */
  .par-cols{display:flex;gap:15px;margin-bottom:27px}
  .par-col{flex:1;border:3px solid;border-radius:9px;background:#fff;padding:18px;position:relative;overflow:hidden}
  .par-col::before{content:'';position:absolute;top:0;left:0;right:0;height:6px}
  .par-col.midnight{border-color:#0F1923}.par-col.midnight::before{background:#0F1923}
  .par-col.gold{border-color:#D4C28E}.par-col.gold::before{background:#D4C28E}
  .par-col.terra{border-color:#B8806A}.par-col.terra::before{background:#B8806A}
  .par-col-title{font-size:16.5px;font-weight:800;text-transform:uppercase;letter-spacing:.08em;margin-bottom:12px}
  .par-col.midnight .par-col-title{color:#0F1923}
  .par-col.gold .par-col-title{color:#D4C28E}
  .par-col.terra .par-col-title{color:#B8806A}
  .par-item{font-size:15.8px;font-weight:600;padding:7.5px 12px;border-radius:4.5px;margin-bottom:4.5px;display:flex;align-items:center;gap:9px}
  .par-item::before{content:'';width:9px;height:9px;border-radius:0;flex-shrink:0}
  .par-col.midnight .par-item{background:rgba(15,25,35,.03)}.par-col.midnight .par-item::before{background:#0F1923}
  .par-col.gold .par-item{background:rgba(212,194,142,.06)}.par-col.gold .par-item::before{background:#D4C28E}
  .par-col.terra .par-item{background:rgba(184,128,106,.05)}.par-col.terra .par-item::before{background:#B8806A}

  /* LAUNCH */
  .launch-block{background:#0F1923;border-radius:9px;padding:30px 45px;display:flex;align-items:center;gap:24px;animation:launchGlow 2.5s ease-in-out infinite}
  @keyframes launchGlow{0%,100%{box-shadow:none}50%{box-shadow:0 6px 45px rgba(212,194,142,.25)}}
  .launch-icon{width:63px;height:63px;border-radius:6px;background:rgba(212,194,142,.2);display:flex;align-items:center;justify-content:center;flex-shrink:0}
  .launch-icon svg{width:33px;height:33px;stroke:#D4C28E}
  .launch-title{font-size:22.5px;font-weight:800;color:#fff;letter-spacing:.03em}
  .launch-sub{font-size:16.5px;color:rgba(255,255,255,.4);margin-top:3px}
  .launch-day{margin-left:auto;background:#D4C28E;color:#1a1a1a;padding:9px 21px;border-radius:6px;font-size:18px;font-weight:800;letter-spacing:.05em;flex-shrink:0}

  /* BRANCH SPLIT (1 to 2) */
  .branch-split{position:relative;width:100%;height:70px}
  .branch-split svg{position:absolute;top:0;left:0;width:100%;height:100%}
  .branch-split svg line{stroke:#d5cfc5;stroke-width:2;stroke-dasharray:8 5}
  .branch-split-dot{position:absolute;width:12px;height:12px;border-radius:0;z-index:3;will-change:transform,opacity}
  .branch-split-dot.to-left{top:0;left:50%;transform:translateX(-50%);background:#D4C28E;animation:splitLeft 2.8s ease-in-out infinite}
  .branch-split-dot.to-right{top:0;left:50%;transform:translateX(-50%);background:#B8806A;animation:splitRight 2.8s ease-in-out infinite .5s}
  @keyframes splitLeft{0%{transform:translate(-50%,0);opacity:0}10%{transform:translate(-50%,0);opacity:1}90%{transform:translate(calc(-50% - 180px),58px);opacity:1}100%{transform:translate(calc(-50% - 180px),68px);opacity:0}}
  @keyframes splitRight{0%{transform:translate(-50%,0);opacity:0}10%{transform:translate(-50%,0);opacity:1}90%{transform:translate(calc(-50% + 180px),58px);opacity:1}100%{transform:translate(calc(-50% + 180px),68px);opacity:0}}

  /* BRANCH MERGE (2 to 1) */
  .branch-merge{position:relative;width:100%;height:70px}
  .branch-merge svg{position:absolute;top:0;left:0;width:100%;height:100%}
  .branch-merge svg line{stroke:#d5cfc5;stroke-width:2;stroke-dasharray:8 5}
  .branch-merge-dot{position:absolute;width:12px;height:12px;border-radius:0;z-index:3;will-change:transform,opacity}
  .branch-merge-dot.from-left{top:0;left:calc(50% - 180px);background:#D4C28E;animation:mergeFromLeft 2.8s ease-in-out infinite}
  .branch-merge-dot.from-right{top:0;left:calc(50% + 180px);background:#B8806A;animation:mergeFromRight 2.8s ease-in-out infinite .5s}
  @keyframes mergeFromLeft{0%{transform:translate(0,0);opacity:0}10%{transform:translate(0,0);opacity:1}90%{transform:translate(180px,58px);opacity:1}100%{transform:translate(180px,68px);opacity:0}}
  @keyframes mergeFromRight{0%{transform:translate(0,0);opacity:0}10%{transform:translate(0,0);opacity:1}90%{transform:translate(-180px,58px);opacity:1}100%{transform:translate(-180px,68px);opacity:0}}

  /* MARKET RESEARCH GRID - 3 top + 1 centered */
  .mr-grid-top{display:flex;gap:0}
  .mr-grid-top .phase-cell{flex:1}
  .mr-grid-bottom{display:flex;justify-content:center;border-top:1.5px solid rgba(0,0,0,.04)}
  .mr-grid-bottom .phase-cell{flex:0 0 33.33%;text-align:center}

  /* SE CONFIG BLOCK (inside phase 3) */
  .se-config{border:3px solid #D4C28E;border-radius:9px;background:#fff;overflow:hidden}
  .se-config::before{content:'';display:block;height:6px;background:#D4C28E}
  .se-config-title{font-size:16.5px;font-weight:800;text-transform:uppercase;letter-spacing:.08em;color:#D4C28E;padding:14px 18px 0}
  .se-config-day{font-family:'Playfair Display',serif;font-style:italic;font-size:13px;color:#888;padding:2px 18px 10px}

  /* ========== TABLET RESPONSIVE ========== */
  @media (max-width: 991px) {
    .tw { padding: 50px 20px 60px; }
    .tw-title { font-size: 26px; }
    .tw-sub { font-size: 16px; margin-bottom: 40px; }

    .phase-cell { min-width: 0; flex: 1 1 45%; }
    .mr-grid-top { flex-wrap: wrap; }
    .mr-grid-top .phase-cell { flex: 1 1 45%; }
    .mr-grid-bottom .phase-cell { flex: 0 0 50%; }
    .phase-grid { flex-wrap: wrap; }

    .phase-name { font-size: 18px; }
    .phase-day { font-size: 15px; padding: 5px 12px; }
    .phase-badge { font-size: 14px; padding: 6px 14px; }
    .pc-label { font-size: 15px; }
    .pc-sub { font-size: 13px; }

    .branch-split-dot.to-left { animation: splitLeftTab 2.8s ease-in-out infinite; }
    .branch-split-dot.to-right { animation: splitRightTab 2.8s ease-in-out infinite .5s; }
    .branch-merge-dot.from-left { left: calc(50% - 120px); animation: mergeFromLeftTab 2.8s ease-in-out infinite; }
    .branch-merge-dot.from-right { left: calc(50% + 120px); animation: mergeFromRightTab 2.8s ease-in-out infinite .5s; }

    .par-cols { gap: 10px; }
    .par-col { padding: 14px; }
    .par-col-title { font-size: 14px; }
    .par-item { font-size: 13.5px; padding: 6px 10px; }

    .launch-block { padding: 20px 24px; flex-wrap: wrap; }
    .launch-title { font-size: 18px; }
    .launch-sub { font-size: 14px; }
    .launch-day { font-size: 15px; padding: 8px 16px; }
  }

  @keyframes splitLeftTab {
    0% { transform: translate(-50%, 0); opacity: 0; }
    10% { transform: translate(-50%, 0); opacity: 1; }
    90% { transform: translate(calc(-50% - 120px), 58px); opacity: 1; }
    100% { transform: translate(calc(-50% - 120px), 68px); opacity: 0; }
  }
  @keyframes splitRightTab {
    0% { transform: translate(-50%, 0); opacity: 0; }
    10% { transform: translate(-50%, 0); opacity: 1; }
    90% { transform: translate(calc(-50% + 120px), 58px); opacity: 1; }
    100% { transform: translate(calc(-50% + 120px), 68px); opacity: 0; }
  }
  @keyframes mergeFromLeftTab {
    0% { transform: translate(0, 0); opacity: 0; }
    10% { transform: translate(0, 0); opacity: 1; }
    90% { transform: translate(120px, 58px); opacity: 1; }
    100% { transform: translate(120px, 68px); opacity: 0; }
  }
  @keyframes mergeFromRightTab {
    0% { transform: translate(0, 0); opacity: 0; }
    10% { transform: translate(0, 0); opacity: 1; }
    90% { transform: translate(-120px, 58px); opacity: 1; }
    100% { transform: translate(-120px, 68px); opacity: 0; }
  }

  /* ========== MOBILE RESPONSIVE ========== */
  @media (max-width: 479px) {
    .tw { padding: 24px 10px 36px; }
    .tw-title { font-size: 20px; }
    .tw-sub { font-size: 13px; margin-bottom: 24px; }

    /* Progress bar */
    .progress-track { height: 6px; margin-bottom: 28px; }
    .progress-dot { width: 12px; height: 12px; top: -3px; }

    /* Phase headers - allow wrapping so Day badge doesn't clip */
    .phase-header {
      flex-wrap: wrap;
      gap: 8px;
      padding: 12px 14px;
    }
    .phase-badge { font-size: 11px; padding: 5px 10px; }
    .phase-name { font-size: 14px; flex: 1 1 auto; }
    .phase-day {
      font-size: 11px;
      padding: 4px 10px;
      margin-left: 0;
    }

    /* Phase cells - single column stack */
    .phase-cell {
      flex: 1 1 100% !important;
      min-width: 0 !important;
      padding: 14px 12px;
    }
    .mr-grid-bottom .phase-cell { flex: 0 0 100% !important; }
    .pc-icon { width: 34px; height: 34px; }
    .pc-icon svg { width: 17px; height: 17px; }
    .pc-label { font-size: 13px; }
    .pc-sub { font-size: 11px; }
    .phase { margin-bottom: 16px; }
    .phase-body { border-width: 2px; }

    /* Connectors - shorter */
    .phase-conn { height: 32px; }
    .phase-conn-line { width: 2px; }
    .phase-conn-dot { width: 10px; height: 10px; }

    /* Branch split/merge - tighter for narrow screens */
    .branch-split { height: 45px; }
    .branch-merge { height: 45px; }
    .branch-split-dot,
    .branch-merge-dot { width: 10px; height: 10px; }
    .branch-split-dot.to-left { animation: splitLeftMob 2.8s ease-in-out infinite; }
    .branch-split-dot.to-right { animation: splitRightMob 2.8s ease-in-out infinite .5s; }
    .branch-merge-dot.from-left { left: calc(50% - 65px); animation: mergeFromLeftMob 2.8s ease-in-out infinite; }
    .branch-merge-dot.from-right { left: calc(50% + 65px); animation: mergeFromRightMob 2.8s ease-in-out infinite .5s; }

    /* Parallel columns - stack vertically */
    .par-cols {
      flex-direction: column;
      gap: 10px;
    }
    .par-col {
      padding: 12px;
      border-width: 2px;
    }
    .par-col-title { font-size: 11px; margin-bottom: 8px; }
    .par-item { font-size: 12px; padding: 5px 8px; gap: 6px; }
    .par-item::before { width: 7px; height: 7px; }

    /* Launch block - vertical stack */
    .launch-block {
      flex-direction: column;
      text-align: center;
      padding: 18px 14px;
      gap: 10px;
    }
    .launch-icon { width: 44px; height: 44px; }
    .launch-icon svg { width: 22px; height: 22px; }
    .launch-title { font-size: 14px; }
    .launch-sub { font-size: 11px; }
    .launch-day { margin-left: 0; font-size: 13px; padding: 7px 14px; }
    .launch-block > div[style] { text-align: center !important; }
  }

  @keyframes splitLeftMob {
    0% { transform: translate(-50%, 0); opacity: 0; }
    10% { transform: translate(-50%, 0); opacity: 1; }
    90% { transform: translate(calc(-50% - 65px), 35px); opacity: 1; }
    100% { transform: translate(calc(-50% - 65px), 45px); opacity: 0; }
  }
  @keyframes splitRightMob {
    0% { transform: translate(-50%, 0); opacity: 0; }
    10% { transform: translate(-50%, 0); opacity: 1; }
    90% { transform: translate(calc(-50% + 65px), 35px); opacity: 1; }
    100% { transform: translate(calc(-50% + 65px), 45px); opacity: 0; }
  }
  @keyframes mergeFromLeftMob {
    0% { transform: translate(0, 0); opacity: 0; }
    10% { transform: translate(0, 0); opacity: 1; }
    90% { transform: translate(65px, 35px); opacity: 1; }
    100% { transform: translate(65px, 45px); opacity: 0; }
  }
  @keyframes mergeFromRightMob {
    0% { transform: translate(0, 0); opacity: 0; }
    10% { transform: translate(0, 0); opacity: 1; }
    90% { transform: translate(-65px, 35px); opacity: 1; }
    100% { transform: translate(-65px, 45px); opacity: 0; }
  }
</style>
</head>
<body>
<div class="tw">


  <div class="progress-track"><div class="progress-fill"></div><div class="progress-dot"></div></div>

  <!-- PHASE 1: ONBOARD -->
  <div class="phase">
    <div class="phase-header">
      <div class="phase-badge midnight">Phase 1</div>
      <div class="phase-name">Onboard Call</div>
      <div class="phase-day"><span>Day 1</span></div>
    </div>
    <div class="phase-body midnight">
      <div class="phase-grid">
        <div class="phase-cell"><div class="pc-icon midnight"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round"><path d="M22 16.92v3a2 2 0 01-2.18 2 19.79 19.79 0 01-8.63-3.07 19.5 19.5 0 01-6-6A19.79 19.79 0 014.12 2.12 2 2 0 014.11 2h3a2 2 0 012 1.72c.127.96.361 1.903.7 2.81a2 2 0 01-.45 2.11L8.09 9.91a16 16 0 006 6l1.27-1.27a2 2 0 012.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0122 16.92z"/></svg></div><div class="pc-label">Onboard Call & Quiz</div><div class="pc-sub">Define your ideal customer</div></div>
        <div class="phase-cell"><div class="pc-icon midnight"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round"><circle cx="12" cy="12" r="10"/><path d="M12 16v-4M12 8h.01"/></svg></div><div class="pc-label">Define ICP & GTM Strategy</div><div class="pc-sub">Targeting & positioning</div></div>
      </div>
    </div>
  </div>

  <div class="phase-conn"><div class="phase-conn-line"></div><div class="phase-conn-dot midnight"></div></div>

  <!-- PHASE 2: INFRA -->
  <div class="phase">
    <div class="phase-header">
      <div class="phase-badge gold">Phase 2</div>
      <div class="phase-name">Infrastructure Setup</div>
      <div class="phase-day"><span>Day 1</span></div>
    </div>
    <div class="phase-body gold">
      <div class="phase-grid">
        <div class="phase-cell"><div class="pc-icon gold"><svg viewBox="0 0 24 24" fill="none" stroke="#1a1a1a" stroke-width="2" stroke-linecap="round"><path d="M12 2L2 7l10 5 10-5-10-5z"/><path d="M2 17l10 5 10-5"/><path d="M2 12l10 5 10-5"/></svg></div><div class="pc-label">Connect Systems</div><div class="pc-sub">CRM, Clay, Instantly, Lemlist</div></div>
        <div class="phase-cell"><div class="pc-icon gold"><svg viewBox="0 0 24 24" fill="none" stroke="#1a1a1a" stroke-width="2" stroke-linecap="round"><rect x="2" y="4" width="20" height="16" rx="2"/><path d="m22 7-8.97 5.7a1.94 1.94 0 01-2.06 0L2 7"/></svg></div><div class="pc-label">Buy Domains & Inboxes</div><div class="pc-sub">Google & Outlook</div></div>
        <div class="phase-cell"><div class="pc-icon gold"><svg viewBox="0 0 24 24" fill="none" stroke="#1a1a1a" stroke-width="2" stroke-linecap="round"><path d="M22 11.08V12a10 10 0 11-5.93-9.14"/><polyline points="22 4 12 14.01 9 11.01"/></svg></div><div class="pc-label">Begin Inbox Warm Up</div><div class="pc-sub">Day 1–14 · Deliverability</div></div>
      </div>
    </div>
  </div>

  <div class="phase-conn"><div class="phase-conn-line"></div><div class="phase-conn-dot gold"></div></div>

  <!-- PHASE 3: CREATING THE CAMPAIGNS -->
  <div class="phase">
    <div class="phase-header">
      <div class="phase-badge terra">Phase 3</div>
      <div class="phase-name">Creating the Campaigns</div>
      <div class="phase-day"><span>Day 1–14</span></div>
    </div>

    <div class="phase-body midnight" style="border-radius:0 0 9px 9px;border-top:none">
      <div class="mr-grid-top">
        <div class="phase-cell"><div class="pc-icon midnight"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round"><circle cx="11" cy="11" r="8"/><path d="M21 21l-4.35-4.35"/></svg></div><div class="pc-label">Deep AI Market Research</div><div class="pc-sub">Analyze market landscape</div></div>
        <div class="phase-cell"><div class="pc-icon midnight"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round"><circle cx="12" cy="12" r="10"/><path d="M2 12h20M12 2a15.3 15.3 0 014 10 15.3 15.3 0 01-4 10 15.3 15.3 0 01-4-10 15.3 15.3 0 014-10z"/></svg></div><div class="pc-label">TAM Mapping</div><div class="pc-sub">Total addressable market</div></div>
        <div class="phase-cell"><div class="pc-icon midnight"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round"><path d="M17 21v-2a4 4 0 00-4-4H5a4 4 0 00-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 00-3-3.87M16 3.13a4 4 0 010 7.75"/></svg></div><div class="pc-label">ICP Development</div><div class="pc-sub">Ideal customer profile</div></div>
      </div>
      <div class="mr-grid-bottom">
        <div class="phase-cell"><div class="pc-icon midnight"><svg viewBox="0 0 24 24" fill="none" stroke-width="2" stroke-linecap="round"><path d="M21 16V8a2 2 0 00-1-1.73l-7-4a2 2 0 00-2 0l-7 4A2 2 0 003 8v8a2 2 0 001 1.73l7 4a2 2 0 002 0l7-4A2 2 0 0021 16z"/></svg></div><div class="pc-label">Identify Best Data Source</div><div class="pc-sub">Apollo, ZoomInfo, etc</div></div>
      </div>
    </div>
  </div>

  <!-- BRANCH SPLIT -->
  <div class="branch-split">
    <svg viewBox="0 0 800 70" preserveAspectRatio="none"><line x1="400" y1="0" x2="200" y2="70"/><line x1="400" y1="0" x2="600" y2="70"/></svg>
    <div class="branch-split-dot to-left"></div>
    <div class="branch-split-dot to-right"></div>
  </div>

  <!-- Data Process + Copywriting side by side -->
  <div class="par-cols" style="margin-bottom:0">
    <div class="par-col gold">
      <div class="par-col-title">Data Process</div>
      <div class="par-item">Scrape Data</div>
      <div class="par-item">Enrich Data</div>
      <div class="par-item">Score All Leads</div>
    </div>
    <div class="par-col terra">
      <div class="par-col-title">Copywriting</div>
      <div class="par-item">Copywriting Ideation</div>
      <div class="par-item">Pick Winners</div>
      <div class="par-item">Spam Check Templates</div>
      <div class="par-item">Spintax Templates</div>
      <div class="par-item">AI Personalize Emails</div>
    </div>
  </div>

  <!-- BRANCH MERGE -->
  <div class="branch-merge">
    <svg viewBox="0 0 800 70" preserveAspectRatio="none"><line x1="200" y1="0" x2="400" y2="70"/><line x1="600" y1="0" x2="400" y2="70"/></svg>
    <div class="branch-merge-dot from-left"></div>
    <div class="branch-merge-dot from-right"></div>
  </div>

  <!-- PHASE 4: SALES ENGAGEMENT CONFIG -->
  <div class="phase">
    <div class="phase-header">
      <div class="phase-badge gold">Phase 4</div>
      <div class="phase-name">Sales Engagement Tool Configuration</div>
      <div class="phase-day"><span>Day 14</span></div>
    </div>
    <div class="phase-body gold">
      <div class="phase-grid">
        <div class="phase-cell"><div class="pc-icon gold"><svg viewBox="0 0 24 24" fill="none" stroke="#1a1a1a" stroke-width="2" stroke-linecap="round"><path d="M4 4h16v16H4z"/><path d="M9 9h6v6H9z"/><path d="M9 1v3M15 1v3M9 20v3M15 20v3M20 9h3M20 15h3M1 9h3M1 15h3"/></svg></div><div class="pc-label">Configure Campaign Settings</div><div class="pc-sub">Platform & sequence setup</div></div>
        <div class="phase-cell"><div class="pc-icon gold"><svg viewBox="0 0 24 24" fill="none" stroke="#1a1a1a" stroke-width="2" stroke-linecap="round"><path d="M14 2H6a2 2 0 00-2 2v16a2 2 0 002 2h12a2 2 0 002-2V8z"/><polyline points="14 2 14 8 20 8"/><path d="M12 12v6M9 15h6"/></svg></div><div class="pc-label">Import Copywriting</div><div class="pc-sub">Templates & sequences</div></div>
        <div class="phase-cell"><div class="pc-icon gold"><svg viewBox="0 0 24 24" fill="none" stroke="#1a1a1a" stroke-width="2" stroke-linecap="round"><path d="M21 16V8a2 2 0 00-1-1.73l-7-4a2 2 0 00-2 0l-7 4A2 2 0 003 8v8a2 2 0 001 1.73l7 4a2 2 0 002 0l7-4A2 2 0 0021 16z"/><path d="M12 12v6M9 15h6"/></svg></div><div class="pc-label">Import Data</div><div class="pc-sub">Leads & enrichment data</div></div>
      </div>
    </div>
  </div>

  <div class="phase-conn"><div class="phase-conn-line"></div><div class="phase-conn-dot midnight"></div></div>

  <!-- LAUNCH -->
  <div class="launch-block">
    <div class="launch-icon"><svg viewBox="0 0 24 24" fill="none" stroke-width="2.5" stroke-linecap="round"><path d="M22 2L11 13"/><path d="M22 2l-7 20-4-9-9-4 20-7z"/></svg></div>
    <div style="flex:1;text-align:left">
      <div class="launch-title">Kickoff Call — Launch Campaigns</div>
      <div class="launch-sub">Campaigns go live</div>
    </div>
    <div class="launch-day">DAY 15</div>
  </div>
</div>
</body>
</html>
