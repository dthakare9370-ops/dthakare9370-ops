<style>
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Inter:wght@300;400;500;700;900&display=swap');

  * { box-sizing: border-box; margin: 0; padding: 0; }

  .readme-wrap {
    background: #0d1117;
    min-height: 100vh;
    font-family: 'Inter', sans-serif;
    color: #e6edf3;
    position: relative;
    overflow: hidden;
  }

  canvas#particles {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none;
    z-index: 0;
  }

  .spotlight {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none;
    z-index: 1;
    background: radial-gradient(600px circle at var(--mx, 50%) var(--my, 30%), rgba(88,166,255,0.07), transparent 60%);
    transition: background 0.1s ease-out;
  }

  .progress-bar {
    position: fixed;
    top: 0; left: 0;
    height: 3px;
    width: 0%;
    background: linear-gradient(90deg, #58a6ff, #bc8cff, #f78166);
    z-index: 10;
    transition: width 0.1s ease-out;
  }

  .content {
    position: relative;
    z-index: 2;
    max-width: 880px;
    margin: 0 auto;
    padding: 2rem 1.5rem 3rem;
  }

  .hero {
    text-align: center;
    padding: 3rem 0 2.5rem;
    border-bottom: 1px solid #21262d;
    position: relative;
  }

  .hero-greeting {
    font-size: 13px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: #58a6ff;
    margin-bottom: 0.8rem;
    opacity: 0;
    animation: fadeUp 0.6s ease 0.3s forwards;
  }

  .hero-name {
    font-size: clamp(2rem, 5vw, 3.2rem);
    font-weight: 900;
    letter-spacing: -1px;
    background: linear-gradient(135deg, #58a6ff 0%, #bc8cff 50%, #f78166 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    opacity: 0;
    animation: fadeUp 0.7s ease 0.5s forwards;
    min-height: 1.2em;
  }

  .typewriter-role {
    font-family: 'JetBrains Mono', monospace;
    font-size: 14px;
    color: #3fb950;
    margin-top: 0.6rem;
    min-height: 22px;
    opacity: 0;
    animation: fadeUp 0.6s ease 0.9s forwards;
  }

  .cursor {
    display: inline-block;
    width: 2px;
    height: 14px;
    background: #3fb950;
    margin-left: 2px;
    vertical-align: middle;
    animation: blink 1s step-end infinite;
  }

  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  .hero-badges {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
    margin-top: 1.5rem;
    opacity: 0;
    animation: fadeUp 0.6s ease 1.2s forwards;
  }

  .badge {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 6px 14px;
    border-radius: 20px;
    font-size: 12px;
    font-weight: 500;
    text-decoration: none;
    border: 1px solid;
    transition: transform 0.2s, box-shadow 0.2s;
    cursor: pointer;
  }
  .badge:hover { transform: translateY(-2px); box-shadow: 0 4px 16px rgba(0,0,0,0.4); }
  .badge-blue { background: rgba(88,166,255,0.1); border-color: rgba(88,166,255,0.4); color: #58a6ff; }
  .badge-purple { background: rgba(188,140,255,0.1); border-color: rgba(188,140,255,0.4); color: #bc8cff; }
  .badge-red { background: rgba(247,129,102,0.1); border-color: rgba(247,129,102,0.4); color: #f78166; }
  .badge-green { background: rgba(63,185,80,0.1); border-color: rgba(63,185,80,0.4); color: #3fb950; }

  .orbit-wrap {
    margin: 2.2rem auto 0;
    width: 220px;
    height: 220px;
    position: relative;
    perspective: 900px;
    opacity: 0;
    animation: fadeUp 0.8s ease 1.5s forwards;
  }
  .orbit-ring {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0; left: 0;
    transform-style: preserve-3d;
    animation: spin3d 18s linear infinite;
  }
  .orbit-ring.reverse {
    width: 150px; height: 150px;
    top: 35px; left: 35px;
    animation: spin3dRev 24s linear infinite;
  }
  .orbit-core {
    position: absolute;
    top: 50%; left: 50%;
    width: 56px; height: 56px;
    margin: -28px;
    border-radius: 50%;
    background: radial-gradient(circle at 30% 30%, #bc8cff, #58a6ff 60%, #161b22 100%);
    box-shadow: 0 0 40px rgba(88,166,255,0.5), 0 0 80px rgba(188,140,255,0.25);
    display: flex; align-items: center; justify-content: center;
    font-size: 1.6rem;
    z-index: 2;
  }
  .orbit-item {
    position: absolute;
    top: 50%; left: 50%;
    width: 38px; height: 38px;
    margin: -19px;
    border-radius: 10px;
    background: #161b22;
    border: 1px solid #30363d;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.1rem;
    box-shadow: 0 4px 16px rgba(0,0,0,0.4);
  }
  .orbit-item:nth-child(1) { transform: rotateY(0deg) translateZ(110px); }
  .orbit-item:nth-child(2) { transform: rotateY(60deg) translateZ(110px); }
  .orbit-item:nth-child(3) { transform: rotateY(120deg) translateZ(110px); }
  .orbit-item:nth-child(4) { transform: rotateY(180deg) translateZ(110px); }
  .orbit-item:nth-child(5) { transform: rotateY(240deg) translateZ(110px); }
  .orbit-item:nth-child(6) { transform: rotateY(300deg) translateZ(110px); }
  .orbit-ring.reverse .orbit-item:nth-child(1) { transform: rotateX(0deg) translateZ(75px); }
  .orbit-ring.reverse .orbit-item:nth-child(2) { transform: rotateX(90deg) translateZ(75px); }
  .orbit-ring.reverse .orbit-item:nth-child(3) { transform: rotateX(180deg) translateZ(75px); }
  .orbit-ring.reverse .orbit-item:nth-child(4) { transform: rotateX(270deg) translateZ(75px); }

  @keyframes spin3d { from { transform: rotateY(0deg) rotateX(8deg); } to { transform: rotateY(360deg) rotateX(8deg); } }
  @keyframes spin3dRev { from { transform: rotateX(0deg) rotateY(-8deg); } to { transform: rotateX(-360deg) rotateY(-8deg); } }

  .section {
    margin-top: 2.5rem;
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.5s, transform 0.5s;
  }
  .section.visible { opacity: 1; transform: translateY(0); }

  .section-title {
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 3px;
    color: #7d8590;
    margin-bottom: 1rem;
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .section-title::after {
    content: '';
    flex: 1;
    height: 1px;
    background: #21262d;
  }

  .code-block {
    background: #161b22;
    border: 1px solid #30363d;
    border-radius: 8px;
    padding: 1.2rem 1.5rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    line-height: 1.8;
    overflow-x: auto;
    position: relative;
  }
  .code-block::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, #58a6ff, #bc8cff, #f78166);
    border-radius: 8px 8px 0 0;
  }
  .kw { color: #ff7b72; }
  .fn { color: #d2a8ff; }
  .str { color: #a5d6ff; }
  .prop { color: #79c0ff; }
  .comment { color: #8b949e; }
  .val { color: #3fb950; }

  .achievement-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 12px;
  }

  .tilt-card {
    background: #161b22;
    border: 1px solid #30363d;
    border-radius: 10px;
    padding: 1.1rem;
    cursor: default;
    position: relative;
    overflow: hidden;
    transform-style: preserve-3d;
    transform: perspective(700px);
    transition: transform 0.15s ease-out, border-color 0.25s, box-shadow 0.25s;
    will-change: transform;
  }
  .tilt-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
  }
  .tilt-card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at var(--mx,50%) var(--my,50%), rgba(255,255,255,0.08), transparent 60%);
    opacity: 0;
    transition: opacity 0.25s;
    pointer-events: none;
  }
  .tilt-card:hover::after { opacity: 1; }
  .tilt-card.gold::before { background: linear-gradient(90deg, #f5a623, #f7d06e); }
  .tilt-card.silver::before { background: linear-gradient(90deg, #79c0ff, #a5d6ff); }
  .tilt-card.bronze::before { background: linear-gradient(90deg, #bc8cff, #d2a8ff); }
  .tilt-card:hover { border-color: #58a6ff; box-shadow: 0 16px 40px rgba(88,166,255,0.18); }

  .achievement-icon { font-size: 1.8rem; margin-bottom: 0.4rem; transform: translateZ(20px); }
  .achievement-title { font-size: 13px; font-weight: 600; color: #e6edf3; transform: translateZ(20px); }
  .achievement-sub { font-size: 11px; color: #7d8590; margin-top: 3px; line-height: 1.5; transform: translateZ(20px); }

  .project-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 14px;
  }

  .project-card {
    background: #161b22;
    border: 1px solid #30363d;
    border-radius: 10px;
    padding: 1.2rem;
    cursor: default;
    display: flex;
    flex-direction: column;
    gap: 8px;
    position: relative;
    overflow: hidden;
    transform-style: preserve-3d;
    transform: perspective(700px);
    transition: transform 0.15s ease-out, border-color 0.2s, box-shadow 0.3s;
    will-change: transform;
  }
  .project-card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at var(--mx,50%) var(--my,50%), rgba(188,140,255,0.12), transparent 60%);
    opacity: 0;
    transition: opacity 0.25s;
    pointer-events: none;
  }
  .project-card:hover::after { opacity: 1; }
  .project-card:hover { border-color: #bc8cff; box-shadow: 0 16px 40px rgba(188,140,255,0.2); }
  .project-header { display: flex; align-items: center; gap: 8px; transform: translateZ(24px); }
  .project-icon { font-size: 1.3rem; }
  .project-name { font-size: 14px; font-weight: 600; color: #58a6ff; }
  .project-desc { font-size: 12px; color: #7d8590; line-height: 1.6; transform: translateZ(24px); }
  .project-tags { display: flex; flex-wrap: wrap; gap: 6px; margin-top: 4px; transform: translateZ(24px); }
  .tag { font-size: 10px; padding: 3px 8px; border-radius: 12px; font-family: 'JetBrains Mono', monospace; }
  .tag-dart { background: rgba(88,166,255,0.15); color: #58a6ff; border: 1px solid rgba(88,166,255,0.3); }
  .tag-java { background: rgba(247,129,102,0.15); color: #f78166; border: 1px solid rgba(247,129,102,0.3); }
  .tag-react { background: rgba(63,185,80,0.15); color: #3fb950; border: 1px solid rgba(63,185,80,0.3); }
  .tag-ai { background: rgba(188,140,255,0.15); color: #bc8cff; border: 1px solid rgba(188,140,255,0.3); }
  .tag-iot { background: rgba(245,166,35,0.15); color: #f5a623; border: 1px solid rgba(245,166,35,0.3); }

  /* CURRENTLY BUILDING TICKER */
  .ticker-outer {
    background: #161b22;
    border: 1px solid #30363d;
    border-radius: 10px;
    padding: 1rem 1.2rem;
    overflow: hidden;
    margin-top: 1.2rem;
  }
  .ticker-label {
    font-size: 11px; color: #3fb950; font-family: 'JetBrains Mono', monospace;
    letter-spacing: 2px; margin-bottom: 0.6rem;
    display: flex; align-items: center; gap: 6px;
  }
  .dot-live {
    width: 7px; height: 7px; border-radius: 50%; background: #3fb950;
    animation: pulse 1.4s ease-in-out infinite; flex-shrink: 0;
  }
  @keyframes pulse { 0%,100%{opacity:1;transform:scale(1)} 50%{opacity:0.4;transform:scale(1.5)} }
  .ticker-track { overflow: hidden; }
  .ticker-inner {
    display: flex; gap: 2.5rem; width: max-content;
    animation: marquee 26s linear infinite;
  }
  .ticker-inner:hover { animation-play-state: paused; }
  @keyframes marquee { from{transform:translateX(0)} to{transform:translateX(-50%)} }
  .ticker-item {
    display: flex; align-items: center; gap: 8px; white-space: nowrap;
    font-size: 12px; color: #c9d1d9;
  }
  .ticker-item .t-icon {
    font-size: 1rem; background: #0d1117; border: 1px solid #30363d;
    border-radius: 6px; padding: 2px 6px;
  }
  .ticker-item .t-tag {
    font-size: 10px; font-family: 'JetBrains Mono', monospace;
    padding: 2px 7px; border-radius: 10px;
    background: rgba(88,166,255,0.12); color: #58a6ff; border: 1px solid rgba(88,166,255,0.3);
  }

  /* PROJECT PROGRESS */
  .progress-cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
    gap: 10px;
    margin-top: 1.2rem;
  }
  .prog-card {
    background: #161b22; border: 1px solid #30363d; border-radius: 10px;
    padding: 0.9rem 1rem; position: relative; overflow: hidden;
    transition: border-color 0.2s, transform 0.2s;
  }
  .prog-card:hover { transform: translateY(-2px); }
  .prog-card::before { content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px; }
  .pc-blue::before { background: linear-gradient(90deg, #58a6ff, #79c0ff); }
  .pc-purple::before { background: linear-gradient(90deg, #bc8cff, #d2a8ff); }
  .pc-green::before { background: linear-gradient(90deg, #3fb950, #56d364); }
  .pc-orange::before { background: linear-gradient(90deg, #f5a623, #f7d06e); }
  .pc-blue:hover { border-color: #58a6ff; }
  .pc-purple:hover { border-color: #bc8cff; }
  .pc-green:hover { border-color: #3fb950; }
  .pc-orange:hover { border-color: #f5a623; }
  .pc-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 4px; }
  .pc-name { font-size: 12px; font-weight: 600; color: #e6edf3; }
  .pc-pct { font-size: 11px; font-family: 'JetBrains Mono', monospace; color: #7d8590; }
  .pc-desc { font-size: 11px; color: #7d8590; margin-bottom: 8px; }
  .pc-bar { background: #21262d; border-radius: 4px; height: 5px; overflow: hidden; }
  .pc-fill { height: 100%; border-radius: 4px; width: 0%; transition: width 1.3s cubic-bezier(.16,1,.3,1); }
  .fill-blue { background: #58a6ff; } .fill-purple { background: #bc8cff; }
  .fill-green { background: #3fb950; } .fill-orange { background: #f5a623; }

  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(72px, 1fr));
    gap: 10px;
  }

  .skill-chip {
    background: #161b22;
    border: 1px solid #30363d;
    border-radius: 8px;
    padding: 10px 6px;
    text-align: center;
    font-size: 10px;
    color: #8b949e;
    transition: transform 0.25s, border-color 0.2s, color 0.2s, box-shadow 0.25s;
    cursor: default;
  }
  .skill-chip:hover {
    transform: translateY(-4px) scale(1.06) rotateZ(-2deg);
    border-color: #58a6ff;
    color: #e6edf3;
    box-shadow: 0 10px 24px rgba(88,166,255,0.2);
  }
  .skill-chip .skill-icon { font-size: 1.4rem; margin-bottom: 5px; display: block; transition: transform 0.25s; }
  .skill-chip:hover .skill-icon { transform: scale(1.2) rotateZ(8deg); }

  .proficiency-list { display: flex; flex-direction: column; gap: 10px; margin-top: 1rem; }
  .prof-row { display: grid; grid-template-columns: 110px 1fr 40px; align-items: center; gap: 10px; font-size: 11px; }
  .prof-label { color: #c9d1d9; font-family: 'JetBrains Mono', monospace; }
  .prof-track { background: #21262d; border-radius: 6px; height: 8px; overflow: hidden; }
  .prof-fill {
    height: 100%; width: 0%; border-radius: 6px;
    background: linear-gradient(90deg, #58a6ff, #bc8cff);
    transition: width 1.2s cubic-bezier(.16,1,.3,1);
  }
  .prof-pct { color: #7d8590; text-align: right; font-family: 'JetBrains Mono', monospace; }

  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
    gap: 12px;
  }

  .stat-card {
    background: #161b22;
    border: 1px solid #30363d;
    border-radius: 10px;
    padding: 1rem;
    text-align: center;
    transition: transform 0.25s, border-color 0.25s;
  }
  .stat-card:hover { transform: scale(1.04) translateY(-2px); border-color: #3fb950; }
  .stat-num {
    font-size: 2rem; font-weight: 900;
    background: linear-gradient(135deg, #3fb950, #58a6ff);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .stat-label { font-size: 11px; color: #7d8590; margin-top: 4px; }

  .heatmap {
    margin-top: 1.2rem;
    display: grid;
    grid-template-columns: repeat(26, 1fr);
    gap: 3px;
  }
  .heatmap .cell {
    width: 100%; aspect-ratio: 1; border-radius: 2px;
    background: #161b22; border: 1px solid #21262d;
    transform: scale(0);
    animation: popIn 0.3s ease forwards;
  }
  .heatmap .cell.l1 { background: rgba(63,185,80,0.2); }
  .heatmap .cell.l2 { background: rgba(63,185,80,0.45); }
  .heatmap .cell.l3 { background: rgba(63,185,80,0.7); }
  .heatmap .cell.l4 { background: rgba(63,185,80,1); }
  @keyframes popIn { to { transform: scale(1); } }

  /* SNAKE */
  .snake-wrap {
    background: #161b22; border: 1px solid #30363d; border-radius: 10px;
    padding: 1rem 1.2rem; margin-top: 1.2rem; overflow: hidden;
  }
  .snake-label { font-size: 10px; color: #7d8590; font-family: 'JetBrains Mono', monospace; margin-bottom: 0.6rem; letter-spacing: 2px; }
  canvas#snake { display: block; width: 100%; border-radius: 4px; }

  .timeline { position: relative; padding-left: 24px; }
  .timeline::before {
    content: '';
    position: absolute;
    left: 6px; top: 6px; bottom: 6px;
    width: 2px;
    background: linear-gradient(180deg, #58a6ff, #bc8cff, transparent);
  }
  .exp-card {
    background: #161b22; border: 1px solid #30363d; border-radius: 10px;
    padding: 1rem 1.2rem; margin-bottom: 12px;
    transition: transform 0.2s, box-shadow 0.2s, border-color 0.2s;
    position: relative;
  }
  .exp-card::before {
    content: ''; position: absolute;
    left: -24px; top: 1.1rem;
    width: 10px; height: 10px;
    border-radius: 50%; background: #0d1117; border: 2px solid #58a6ff;
  }
  .exp-card:hover { transform: translateX(4px); box-shadow: 0 8px 24px rgba(88,166,255,0.15); border-color: #58a6ff; }
  .exp-role { font-size: 14px; font-weight: 600; color: #e6edf3; }
  .exp-company { font-size: 12px; color: #58a6ff; margin-top: 2px; }
  .exp-period { font-size: 11px; color: #7d8590; margin-top: 2px; font-family: 'JetBrains Mono', monospace; }
  .exp-desc { font-size: 11px; color: #8b949e; margin-top: 6px; line-height: 1.6; }

  .connect-grid { display: flex; flex-wrap: wrap; gap: 10px; justify-content: center; }
  .connect-btn {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 10px 20px; border-radius: 8px; font-size: 13px; font-weight: 500;
    border: 1px solid; cursor: pointer;
    transition: transform 0.2s, box-shadow 0.2s; text-decoration: none;
  }
  .connect-btn:hover { transform: translateY(-2px) scale(1.03); box-shadow: 0 6px 20px rgba(0,0,0,0.4); }
  .btn-portfolio { background: rgba(88,166,255,0.1); border-color: #58a6ff; color: #58a6ff; }
  .btn-linkedin { background: rgba(10,102,194,0.15); border-color: #0a66c2; color: #79c0ff; }
  .btn-gmail { background: rgba(234,67,53,0.1); border-color: #ea4335; color: #f78166; }
  .btn-resume { background: rgba(63,185,80,0.1); border-color: #3fb950; color: #3fb950; }

  /* OSS BANNER */
  .oss-banner {
    margin-top: 1.5rem; border: 1px dashed #30363d; border-radius: 10px;
    padding: 1.2rem; text-align: center;
    background: rgba(88,166,255,0.03);
    transition: border-color 0.25s;
  }
  .oss-banner:hover { border-color: #58a6ff; }
  .oss-title { font-size: 14px; font-weight: 600; color: #e6edf3; margin-bottom: 0.4rem; }
  .oss-desc { font-size: 12px; color: #7d8590; margin-bottom: 0.8rem; }
  .oss-badges { display: flex; justify-content: center; gap: 8px; flex-wrap: wrap; }
  .oss-badge {
    font-size: 10px; font-family: 'JetBrains Mono', monospace;
    padding: 3px 10px; border-radius: 12px; border: 1px solid;
  }
  .ob-blue { background: rgba(88,166,255,0.1); color: #58a6ff; border-color: rgba(88,166,255,0.3); }
  .ob-green { background: rgba(63,185,80,0.1); color: #3fb950; border-color: rgba(63,185,80,0.3); }
  .ob-purple { background: rgba(188,140,255,0.1); color: #bc8cff; border-color: rgba(188,140,255,0.3); }

  .footer-quote {
    text-align: center; margin-top: 2.5rem; font-style: italic;
    color: #7d8590; font-size: 13px;
    border-top: 1px solid #21262d; padding-top: 1.5rem;
  }
  .footer-quote span { color: #bc8cff; }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @media (prefers-reduced-motion: reduce) {
    * { animation: none !important; transition: none !important; }
  }
</style>

<div class="progress-bar" id="progressBar"></div>
<canvas id="particles"></canvas>
<div class="spotlight" id="spotlight"></div>

<div class="readme-wrap">
  <div class="content">

    <!-- HERO -->
    <div class="hero">
      <div class="hero-greeting">Welcome to my GitHub</div>
      <div class="hero-name" id="heroName"></div>
      <div class="typewriter-role"><span id="roleText"></span><span class="cursor"></span></div>
      <div class="hero-badges">
        <span class="badge badge-blue">📍 Pune, India</span>
        <span class="badge badge-purple">🎓 BE CSE @ SPPU · 9.46 CGPA</span>
        <span class="badge badge-green">✅ Open to Opportunities</span>
        <span class="badge badge-red">🏆 IEEE ProTech 2026</span>
      </div>
      <div class="orbit-wrap">
        <div class="orbit-ring">
          <div class="orbit-item">💙</div>
          <div class="orbit-item">⚛️</div>
          <div class="orbit-item">🟢</div>
          <div class="orbit-item">🐍</div>
          <div class="orbit-item">🍃</div>
          <div class="orbit-item">🤖</div>
        </div>
        <div class="orbit-ring reverse">
          <div class="orbit-item">☕</div>
          <div class="orbit-item">⚡</div>
          <div class="orbit-item">🐘</div>
          <div class="orbit-item">🎯</div>
        </div>
        <div class="orbit-core">👨‍💻</div>
      </div>
    </div>

    <!-- ABOUT ME -->
    <div class="section" id="s1">
      <div class="section-title">about me</div>
      <div class="code-block">
<span class="kw">const</span> <span class="fn">developer</span> = {<br>
&nbsp;&nbsp;<span class="prop">name</span>: <span class="str">"Dnyaneshwar Thakare"</span>,<br>
&nbsp;&nbsp;<span class="prop">location</span>: <span class="str">"Pune, Maharashtra, India 🇮🇳"</span>,<br>
&nbsp;&nbsp;<span class="prop">education</span>: <span class="str">"BE CSE @ TSSM BSCOER, SPPU"</span>, <span class="comment">// CGPA: 9.46</span><br>
&nbsp;&nbsp;<span class="prop">code</span>: [<span class="str">"Dart"</span>, <span class="str">"Flutter"</span>, <span class="str">"JavaScript"</span>, <span class="str">"Python"</span>, <span class="str">"Java"</span>],<br>
&nbsp;&nbsp;<span class="prop">stack</span>: {<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="prop">mobile</span>: <span class="str">"Flutter · Dart"</span>,<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="prop">web</span>: <span class="str">"React · Node.js · Express · FastAPI"</span>,<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="prop">db</span>: <span class="str">"MongoDB · MySQL · PostgreSQL"</span>,<br>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="prop">ai_ml</span>: <span class="str">"Deep Learning · Generative AI · NumPy · Pandas"</span>,<br>
&nbsp;&nbsp;},<br>
&nbsp;&nbsp;<span class="prop">currently</span>: <span class="val">true</span>, <span class="comment">// open to internships & full-time</span><br>
&nbsp;&nbsp;<span class="prop">resume</span>: <span class="str">"drive.google.com/.../view"</span>,<br>
&nbsp;&nbsp;<span class="prop">contact</span>: <span class="str">"dthakare9370@gmail.com"</span>,<br>
};
      </div>
    </div>

    <!-- ACHIEVEMENTS -->
    <div class="section" id="s2">
      <div class="section-title">achievements</div>
      <div class="achievement-grid">
        <div class="tilt-card silver">
          <div class="achievement-icon">🥈</div>
          <div class="achievement-title">2nd Rank — IEEE ProTech 2026</div>
          <div class="achievement-sub">National Level Hackathon @ Symbiosis Institute of Technology · AgroIntelX</div>
        </div>
        <div class="tilt-card gold">
          <div class="achievement-icon">🥇</div>
          <div class="achievement-title">Top Among 120+ Groups</div>
          <div class="achievement-sub">SUPER-X Competition · Educational PathFinder project</div>
        </div>
        <div class="tilt-card bronze">
          <div class="achievement-icon">🏅</div>
          <div class="achievement-title">Consolation Prize — SUPER-X</div>
          <div class="achievement-sub">AgroIntelX · IoT Smart Farming Innovation</div>
        </div>
      </div>
    </div>

    <!-- PROJECTS -->
    <div class="section" id="s3">
      <div class="section-title">featured projects</div>
      <div class="project-grid">
        <div class="project-card">
          <div class="project-header"><span class="project-icon">🌾</span><span class="project-name">AgroIntelX</span></div>
          <div class="project-desc">IoT-based Smart Farming App — real-time crop monitoring, sensor data, AI insights via Flutter</div>
          <div class="project-tags">
            <span class="tag tag-dart">Flutter</span>
            <span class="tag tag-iot">IoT</span>
            <span class="tag tag-ai">AI</span>
          </div>
        </div>
        <div class="project-card">
          <div class="project-header"><span class="project-icon">🎓</span><span class="project-name">Educational PathFinder</span></div>
          <div class="project-desc">AI-powered career guidance platform helping students discover ideal learning paths</div>
          <div class="project-tags">
            <span class="tag tag-react">React</span>
            <span class="tag tag-ai">Deep Learning</span>
          </div>
        </div>
        <div class="project-card">
          <div class="project-header"><span class="project-icon">📖</span><span class="project-name">StoryForge</span></div>
          <div class="project-desc">Desktop application for story creation and management, built solo in Java</div>
          <div class="project-tags">
            <span class="tag tag-java">Java</span>
          </div>
        </div>
      </div>

      <!-- ✨ NEW: CURRENTLY BUILDING TICKER -->
      <div class="ticker-outer">
        <div class="ticker-label"><span class="dot-live"></span> currently building</div>
        <div class="ticker-track">
          <div class="ticker-inner">
            <div class="ticker-item"><span class="t-icon">🌾</span> AgroIntelX v2 <span class="t-tag">IoT + AI</span></div>
            <div class="ticker-item"><span class="t-icon">🧠</span> Deep Learning crop model <span class="t-tag">Python</span></div>
            <div class="ticker-item"><span class="t-icon">📱</span> Flutter offline-first sync <span class="t-tag">Dart</span></div>
            <div class="ticker-item"><span class="t-icon">⚡</span> FastAPI microservice layer <span class="t-tag">Backend</span></div>
            <div class="ticker-item"><span class="t-icon">🎓</span> Educational PathFinder v2 <span class="t-tag">React</span></div>
            <div class="ticker-item"><span class="t-icon">🌾</span> AgroIntelX v2 <span class="t-tag">IoT + AI</span></div>
            <div class="ticker-item"><span class="t-icon">🧠</span> Deep Learning crop model <span class="t-tag">Python</span></div>
            <div class="ticker-item"><span class="t-icon">📱</span> Flutter offline-first sync <span class="t-tag">Dart</span></div>
            <div class="ticker-item"><span class="t-icon">⚡</span> FastAPI microservice layer <span class="t-tag">Backend</span></div>
            <div class="ticker-item"><span class="t-icon">🎓</span> Educational PathFinder v2 <span class="t-tag">React</span></div>
          </div>
        </div>
      </div>

      <!-- ✨ NEW: PROJECT PROGRESS CARDS -->
      <div class="progress-cards" id="progCards">
        <div class="prog-card pc-blue">
          <div class="pc-header"><span class="pc-name">AgroIntelX v2</span><span class="pc-pct">70%</span></div>
          <div class="pc-desc">AI crop advisory + sensor dashboard</div>
          <div class="pc-bar"><div class="pc-fill fill-blue" data-pct="70"></div></div>
        </div>
        <div class="prog-card pc-purple">
          <div class="pc-header"><span class="pc-name">PathFinder v2</span><span class="pc-pct">55%</span></div>
          <div class="pc-desc">Career-path recommendation engine</div>
          <div class="pc-bar"><div class="pc-fill fill-purple" data-pct="55"></div></div>
        </div>
        <div class="prog-card pc-green">
          <div class="pc-header"><span class="pc-name">StoryForge</span><span class="pc-pct">90%</span></div>
          <div class="pc-desc">Story management, Java GUI</div>
          <div class="pc-bar"><div class="pc-fill fill-green" data-pct="90"></div></div>
        </div>
        <div class="prog-card pc-orange">
          <div class="pc-header"><span class="pc-name">Portfolio v3</span><span class="pc-pct">40%</span></div>
          <div class="pc-desc">Next.js + Three.js rebuild</div>
          <div class="pc-bar"><div class="pc-fill fill-orange" data-pct="40"></div></div>
        </div>
      </div>
    </div>

    <!-- TECH ARSENAL -->
    <div class="section" id="s4">
      <div class="section-title">tech arsenal</div>
      <div class="skills-grid">
        <div class="skill-chip"><span class="skill-icon">💙</span>Flutter</div>
        <div class="skill-chip"><span class="skill-icon">🎯</span>Dart</div>
        <div class="skill-chip"><span class="skill-icon">☕</span>Java</div>
        <div class="skill-chip"><span class="skill-icon">🐍</span>Python</div>
        <div class="skill-chip"><span class="skill-icon">⚛️</span>React</div>
        <div class="skill-chip"><span class="skill-icon">🟢</span>Node.js</div>
        <div class="skill-chip"><span class="skill-icon">🚂</span>Express</div>
        <div class="skill-chip"><span class="skill-icon">⚡</span>FastAPI</div>
        <div class="skill-chip"><span class="skill-icon">🍃</span>MongoDB</div>
        <div class="skill-chip"><span class="skill-icon">🐬</span>MySQL</div>
        <div class="skill-chip"><span class="skill-icon">🐘</span>PostgreSQL</div>
        <div class="skill-chip"><span class="skill-icon">🧠</span>Deep Learning</div>
        <div class="skill-chip"><span class="skill-icon">🤖</span>Gen AI</div>
        <div class="skill-chip"><span class="skill-icon">📊</span>Pandas</div>
        <div class="skill-chip"><span class="skill-icon">🔢</span>NumPy</div>
        <div class="skill-chip"><span class="skill-icon">🐙</span>Git</div>
      </div>
      <div class="proficiency-list" id="profList">
        <div class="prof-row"><span class="prof-label">Flutter / Dart</span><div class="prof-track"><div class="prof-fill" data-pct="92"></div></div><span class="prof-pct">92%</span></div>
        <div class="prof-row"><span class="prof-label">React / JS</span><div class="prof-track"><div class="prof-fill" data-pct="85"></div></div><span class="prof-pct">85%</span></div>
        <div class="prof-row"><span class="prof-label">Node / Express</span><div class="prof-track"><div class="prof-fill" data-pct="80"></div></div><span class="prof-pct">80%</span></div>
        <div class="prof-row"><span class="prof-label">Python / AI-ML</span><div class="prof-track"><div class="prof-fill" data-pct="78"></div></div><span class="prof-pct">78%</span></div>
        <div class="prof-row"><span class="prof-label">Java</span><div class="prof-track"><div class="prof-fill" data-pct="75"></div></div><span class="prof-pct">75%</span></div>
      </div>
    </div>

    <!-- GITHUB STATS -->
    <div class="section" id="s5">
      <div class="section-title">github stats</div>
      <div class="stats-grid">
        <div class="stat-card"><div class="stat-num" id="c1">0</div><div class="stat-label">Total Commits</div></div>
        <div class="stat-card"><div class="stat-num" id="c2">0</div><div class="stat-label">Repositories</div></div>
        <div class="stat-card"><div class="stat-num">Java</div><div class="stat-label">Top Language (58%)</div></div>
        <div class="stat-card"><div class="stat-num">9.46</div><div class="stat-label">CGPA / 10.0</div></div>
      </div>
      <div class="heatmap" id="heatmap"></div>

      <!-- ✨ NEW: CONTRIBUTION SNAKE -->
      <div class="snake-wrap">
        <div class="snake-label">// contribution snake</div>
        <canvas id="snake" height="56"></canvas>
      </div>
    </div>

    <!-- EXPERIENCE -->
    <div class="section" id="s6">
      <div class="section-title">experience</div>
      <div class="timeline">
        <div class="exp-card">
          <div class="exp-role">Flutter Developer Intern</div>
          <div class="exp-company">Incubators Systems Pvt. Ltd.</div>
          <div class="exp-period">Sep 2025 – Nov 2025</div>
          <div class="exp-desc">Built and optimized cross-platform Flutter mobile applications, improving load performance and UI responsiveness.</div>
        </div>
        <div class="exp-card">
          <div class="exp-role">MERN Stack Developer Intern</div>
          <div class="exp-company">Sumago Infotech Pvt. Ltd.</div>
          <div class="exp-period">Jan 2024 – Jul 2024</div>
          <div class="exp-desc">Developed full-stack web applications using MongoDB, Express, React and Node.js across the product lifecycle.</div>
        </div>
      </div>
    </div>

    <!-- CONNECT -->
    <div class="section" id="s7">
      <div class="section-title">let's connect</div>
      <div class="connect-grid">
        <a href="https://dthakare.onrender.com" class="connect-btn btn-portfolio">🌐 Portfolio</a>
        <a href="https://www.linkedin.com/in/dnyaneshwar-thakare" class="connect-btn btn-linkedin">💼 LinkedIn</a>
        <a href="mailto:dthakare9370@gmail.com" class="connect-btn btn-gmail">✉️ Gmail</a>
        <a href="https://drive.google.com/file/d/1rnql9yWtRgzw-NltjOHrJ0ukE21QodEc/view" class="connect-btn btn-resume">📄 Resume</a>
      </div>

      <!-- ✨ NEW: OSS CALLOUT -->
      <div class="oss-banner">
        <div class="oss-title">✨ Open to Collaborations & Contributions</div>
        <div class="oss-desc">I love building things that matter. If you find my work useful, a ⭐ means the world!</div>
        <div class="oss-badges">
          <span class="oss-badge ob-blue">PRs welcome</span>
          <span class="oss-badge ob-green">good first issue</span>
          <span class="oss-badge ob-purple">flutter • react • python</span>
        </div>
      </div>

      <div class="footer-quote">
        <span>"Code is not just syntax —</span> it's a solution to someone's problem."
      </div>
    </div>

  </div>
</div>

<script>
/* PARTICLES */
const canvas = document.getElementById('particles');
const ctx = canvas.getContext('2d');
const wrap = document.querySelector('.readme-wrap');
let W, H, dots = [];

function resize() { W = canvas.width = wrap.clientWidth; H = canvas.height = wrap.clientHeight; }
resize();
window.addEventListener('resize', resize);

for (let i = 0; i < 60; i++) {
  dots.push({ x: Math.random()*1000, y: Math.random()*800, r: Math.random()*1.5+0.5, vx: (Math.random()-0.5)*0.3, vy: (Math.random()-0.5)*0.3, a: Math.random()*0.5+0.1 });
}

function drawParticles() {
  ctx.clearRect(0,0,W,H);
  dots.forEach(d => {
    d.x+=d.vx; d.y+=d.vy;
    if(d.x<0)d.x=W; if(d.x>W)d.x=0; if(d.y<0)d.y=H; if(d.y>H)d.y=0;
    ctx.beginPath(); ctx.arc(d.x,d.y,d.r,0,Math.PI*2);
    ctx.fillStyle=`rgba(88,166,255,${d.a})`; ctx.fill();
  });
  dots.forEach((d,i) => {
    dots.forEach((d2,j) => {
      if(i>=j)return;
      const dist=Math.hypot(d.x-d2.x,d.y-d2.y);
      if(dist<100){ ctx.beginPath(); ctx.strokeStyle=`rgba(88,166,255,${0.08*(1-dist/100)})`; ctx.lineWidth=0.5; ctx.moveTo(d.x,d.y); ctx.lineTo(d2.x,d2.y); ctx.stroke(); }
    });
  });
  requestAnimationFrame(drawParticles);
}
drawParticles();

/* SPOTLIGHT */
const spotlight = document.getElementById('spotlight');
wrap.addEventListener('mousemove', (e) => {
  const rect = wrap.getBoundingClientRect();
  spotlight.style.setProperty('--mx', ((e.clientX-rect.left)/rect.width*100)+'%');
  spotlight.style.setProperty('--my', ((e.clientY-rect.top)/rect.height*100)+'%');
});

/* SCROLL PROGRESS */
const progressBar = document.getElementById('progressBar');
window.addEventListener('scroll', () => {
  const scrollable = document.documentElement.scrollHeight - window.innerHeight;
  progressBar.style.width = (scrollable>0?(window.scrollY/scrollable)*100:0)+'%';
});

/* TYPEWRITER NAME */
const nameEl = document.getElementById('heroName');
const fullName = 'Dnyaneshwar Thakare';
let ni = 0;
function typeName() { if(ni<=fullName.length){ nameEl.textContent=fullName.slice(0,ni++); setTimeout(typeName,60); } }
setTimeout(typeName, 600);

/* TYPEWRITER ROLES */
const roles = ['> Flutter Developer','> Full Stack Engineer','> AI / ML Enthusiast','> BE CSE @ SPPU · CGPA 9.46'];
let ri=0, ci=0, deleting=false;
const roleEl = document.getElementById('roleText');
function typeRole() {
  const cur = roles[ri];
  if(!deleting){ roleEl.textContent=cur.slice(0,++ci); if(ci===cur.length){deleting=true;setTimeout(typeRole,1800);return;} }
  else{ roleEl.textContent=cur.slice(0,--ci); if(ci===0){deleting=false;ri=(ri+1)%roles.length;setTimeout(typeRole,300);return;} }
  setTimeout(typeRole, deleting?40:70);
}
setTimeout(typeRole, 1200);

/* SECTION REVEAL */
const sections = document.querySelectorAll('.section');
const io = new IntersectionObserver(entries => { entries.forEach(e => { if(e.isIntersecting) e.target.classList.add('visible'); }); }, {threshold:0.1});
sections.forEach(s => io.observe(s));

/* COUNT UP + PROF BARS + PROG CARDS */
function countUp(el, target, dur) {
  let s=0, step=target/(dur/16);
  const t = setInterval(()=>{ s=Math.min(s+step,target); el.textContent=Math.floor(s); if(s>=target)clearInterval(t); },16);
}

const s5 = document.getElementById('s5');
const s5io = new IntersectionObserver(entries => {
  if(entries[0].isIntersecting){
    countUp(document.getElementById('c1'),11,800);
    countUp(document.getElementById('c2'),8,800);
    document.querySelectorAll('.prof-fill').forEach(f => { f.style.width=f.dataset.pct+'%'; });
    s5io.disconnect();
  }
},{threshold:0.3});
s5io.observe(s5);

const s3 = document.getElementById('s3');
const s3io = new IntersectionObserver(entries => {
  if(entries[0].isIntersecting){
    document.querySelectorAll('.pc-fill').forEach(f => { f.style.width=f.dataset.pct+'%'; });
    s3io.disconnect();
  }
},{threshold:0.2});
s3io.observe(s3);

/* HEATMAP */
const heatmap = document.getElementById('heatmap');
for(let i=0;i<130;i++){
  const cell=document.createElement('div');
  const r=Math.random();
  let cls='cell';
  if(r>0.92)cls+=' l4'; else if(r>0.8)cls+=' l3'; else if(r>0.6)cls+=' l2'; else if(r>0.4)cls+=' l1';
  cell.className=cls; cell.style.animationDelay=(i*4)+'ms'; heatmap.appendChild(cell);
}

/* CONTRIBUTION SNAKE */
const snakeCanvas = document.getElementById('snake');
const sctx = snakeCanvas.getContext('2d');

function initSnake() {
  snakeCanvas.width = snakeCanvas.offsetWidth;
  snakeCanvas.height = 56;
  const SW = snakeCanvas.width, SH = snakeCanvas.height;
  const COLS = Math.floor(SW/13), ROWS = Math.floor(SH/13);
  const grid = [];
  for(let r=0;r<ROWS;r++) for(let c=0;c<COLS;c++){
    const v=Math.random();
    grid.push({r,c,level:v>0.7?3:v>0.5?2:v>0.3?1:0,eaten:false});
  }
  let snake=[{r:0,c:0}], tick=0;
  const colors=['#161b22','rgba(63,185,80,0.2)','rgba(63,185,80,0.5)','#3fb950'];

  function draw(){
    sctx.clearRect(0,0,SW,SH);
    grid.forEach(cell=>{
      if(cell.eaten)return;
      sctx.fillStyle=colors[cell.level]||colors[0];
      sctx.strokeStyle='#21262d'; sctx.lineWidth=0.5;
      sctx.beginPath(); sctx.roundRect(cell.c*13+1,cell.r*13+1,11,11,2);
      sctx.fill(); sctx.stroke();
    });
    snake.forEach((seg,i)=>{
      sctx.fillStyle=i===0?'#56d364':'#3fb950';
      sctx.beginPath(); sctx.roundRect(seg.c*13+1,seg.r*13+1,11,11,i===0?4:2); sctx.fill();
    });
  }

  function step(){
    tick++;
    if(tick%4===0){
      const head=snake[0];
      let nc=head.c+1, nr=head.r;
      if(nc>=COLS){nc=0; nr=(nr+1)%ROWS;}
      const cell=grid.find(g=>g.r===nr&&g.c===nc&&!g.eaten);
      if(cell&&cell.level>0){cell.eaten=true; snake.unshift({r:nr,c:nc}); if(snake.length>12)snake.pop();}
      else{snake.unshift({r:nr,c:nc}); if(snake.length>12)snake.pop();}
    }
    draw(); requestAnimationFrame(step);
  }
  requestAnimationFrame(step);
}
initSnake();
window.addEventListener('resize', initSnake);

/* 3D TILT CARDS */
document.querySelectorAll('.tilt-card, .project-card').forEach(card => {
  card.addEventListener('mousemove', (e) => {
    const rect=card.getBoundingClientRect();
    const x=e.clientX-rect.left, y=e.clientY-rect.top;
    const cx=rect.width/2, cy=rect.height/2;
    card.style.transform=`perspective(700px) rotateX(${((y-cy)/cy)*-8}deg) rotateY(${((x-cx)/cx)*8}deg) scale3d(1.02,1.02,1.02)`;
    card.style.setProperty('--mx',(x/rect.width*100)+'%');
    card.style.setProperty('--my',(y/rect.height*100)+'%');
  });
  card.addEventListener('mouseleave', () => {
    card.style.transform='perspective(700px) rotateX(0deg) rotateY(0deg) scale3d(1,1,1)';
  });
});
</script>
