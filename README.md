&lt;!--
  GITHUB PROFILE README — Aryan Kumar Chowdhury
  =========================================================
  Design Strategy:
  • One-screen layout (100vh) with overflow hidden on desktop.
  • F-Pattern: Name → tagline → skills flow down the visual left/center.
  • Z-Pattern: Eye travels from header → projects → contact bottom-right.
  • Dark theme with teal/cyan primary and gold secondary accents.
  • All motion is CSS @keyframes (no JS).
  • Responsive: stacks vertically on mobile with natural scroll.
--&gt;

&lt;style&gt;
  /* ── Font & Reset ─────────────────────────────────────── */
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=JetBrains+Mono:wght@400&display=swap');

  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  /* ── CSS Variables ──────────────────────────────────── */
  :root {
    --bg: #0a0e17;
    --surface: rgba(22, 27, 34, 0.65);
    --border: rgba(48, 54, 61, 0.6);
    --text: #c9d1d9;
    --text-secondary: #8b949e;
    --accent: #00d4aa;       /* Teal */
    --accent2: #00a8e8;      /* Cyan */
    --gold: #f7b731;         /* Gold */
    --shadow: rgba(0, 212, 170, 0.12);
  }

  /* ── Main Container ─────────────────────────────────── */
  .aryan-profile {
    font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 1.5rem 2rem;
    position: relative;
    overflow: hidden;
    line-height: 1.5;
  }

  /* Animated ambient gradient orbs */
  .aryan-profile::before {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background:
      radial-gradient(circle at 20% 35%, rgba(0, 212, 170, 0.04) 0%, transparent 45%),
      radial-gradient(circle at 85% 75%, rgba(247, 183, 49, 0.04) 0%, transparent 45%),
      radial-gradient(circle at 50% 50%, rgba(0, 168, 232, 0.03) 0%, transparent 40%);
    animation: ambientDrift 18s ease-in-out infinite;
    pointer-events: none;
    z-index: 0;
  }

  /* Subtle grid overlay for "tech" texture */
  .aryan-profile::after {
    content: '';
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(0, 212, 170, 0.025) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0, 212, 170, 0.025) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
    z-index: 0;
    mask-image: radial-gradient(ellipse at center, black 40%, transparent 80%);
    -webkit-mask-image: radial-gradient(ellipse at center, black 40%, transparent 80%);
  }

  @keyframes ambientDrift {
    0%, 100% { transform: translate(0, 0) scale(1); }
    33% { transform: translate(-2%, -1%) scale(1.04); }
    66% { transform: translate(1%, 2%) scale(0.98); }
  }

  /* ── Content Wrapper ────────────────────────────────── */
  .ap-content {
    position: relative;
    z-index: 1;
    max-width: 1100px;
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 1.25rem;
  }

  /* ── Header (F-Pattern anchor) ──────────────────────── */
  .ap-header {
    text-align: center;
    animation: fadeInDown 0.7s ease-out both;
  }

  .ap-name {
    font-size: clamp(2.2rem, 5vw, 3.2rem);
    font-weight: 700;
    letter-spacing: -0.03em;
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 50%, var(--gold) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 0.25rem;
  }

  /* Typing effect container */
  .ap-typewrap {
    display: inline-block;
    margin: 0.4rem 0;
  }

  .ap-tagline {
    font-size: 1.05rem;
    font-style: italic;
    color: var(--text-secondary);
    border-right: 2.5px solid var(--accent);
    white-space: nowrap;
    overflow: hidden;
    width: 0;
    max-width: 46ch;
    animation:
      typing 3.2s steps(46, end) forwards,
      blinkCaret 0.8s step-end infinite;
  }

  @keyframes typing {
    from { width: 0; }
    to   { width: 100%; }
  }

  @keyframes blinkCaret {
    50% { border-color: transparent; }
  }

  .ap-bio {
    font-size: 0.9rem;
    color: var(--text-secondary);
    max-width: 560px;
    margin: 0.6rem auto 0;
    line-height: 1.5;
    animation: fadeIn 0.8s ease-out 0.4s both;
  }

  .ap-bio b {
    color: var(--text);
    font-weight: 600;
  }

  /* ── Current Focus Strip ────────────────────────────── */
  .ap-focus {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.6rem;
    font-size: 0.8rem;
    color: var(--text-secondary);
    animation: fadeIn 0.6s ease-out 0.6s both;
    flex-wrap: wrap;
  }

  .ap-pulse {
    width: 7px;
    height: 7px;
    background: var(--accent);
    border-radius: 50%;
    animation: pulse 2s infinite;
    display: inline-block;
  }

  @keyframes pulse {
    0%   { box-shadow: 0 0 0 0 rgba(0, 212, 170, 0.6); }
    70%  { box-shadow: 0 0 0 8px rgba(0, 212, 170, 0); }
    100% { box-shadow: 0 0 0 0 rgba(0, 212, 170, 0); }
  }

  .ap-focus span {
    background: rgba(0, 212, 170, 0.08);
    padding: 0.15rem 0.5rem;
    border-radius: 4px;
    border: 1px solid rgba(0, 212, 170, 0.15);
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    color: var(--accent);
  }

  /* ── Skills (Horizontal strip) ──────────────────────── */
  .ap-skills {
    animation: fadeInUp 0.5s ease-out 0.5s both;
  }

  .ap-skillrow {
    display: flex;
    flex-wrap: wrap;
    gap: 0.45rem;
    justify-content: center;
  }

  .ap-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.3rem;
    padding: 0.3rem 0.7rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    font-size: 0.78rem;
    color: var(--text);
    transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1);
    cursor: default;
    backdrop-filter: blur(8px);
    font-family: 'JetBrains Mono', monospace;
  }

  .ap-badge:hover {
    transform: translateY(-2px) scale(1.06);
    border-color: var(--accent);
    box-shadow: 0 4px 14px var(--shadow);
    background: rgba(0, 212, 170, 0.08);
  }

  .ap-badge .dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    display: inline-block;
  }
  .ap-badge.ml  .dot { background: var(--accent); }
  .ap-badge.data .dot { background: var(--accent2); }
  .ap-badge.fe   .dot { background: var(--gold); }
  .ap-badge.tool .dot { background: var(--text-secondary); }

  /* ── Projects (Z-Pattern diagonal) ──────────────────── */
  .ap-projects {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
    animation: fadeInUp 0.6s ease-out 0.7s both;
  }

  .ap-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 1.1rem;
    transition: all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    overflow: hidden;
    backdrop-filter: blur(10px);
  }

  /* Animated top border on hover */
  .ap-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 2.5px;
    background: linear-gradient(90deg, var(--accent), var(--accent2), var(--gold));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.35s ease;
  }

  .ap-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 32px rgba(0, 0, 0, 0.25), 0 0 0 1px rgba(0, 212, 170, 0.15);
    border-color: rgba(0, 212, 170, 0.25);
  }

  .ap-card:hover::before {
    transform: scaleX(1);
  }

  .ap-card-title {
    font-size: 0.92rem;
    font-weight: 600;
    color: #e6edf3;
    margin-bottom: 0.35rem;
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }

  .ap-card-desc {
    font-size: 0.78rem;
    color: var(--text-secondary);
    line-height: 1.4;
    margin-bottom: 0.7rem;
  }

  .ap-card-tech {
    display: flex;
    flex-wrap: wrap;
    gap: 0.3rem;
  }

  .ap-techtag {
    font-size: 0.68rem;
    padding: 0.12rem 0.45rem;
    background: rgba(0, 212, 170, 0.1);
    color: var(--accent);
    border-radius: 4px;
    font-family: 'JetBrains Mono', monospace;
    border: 1px solid rgba(0, 212, 170, 0.15);
  }

  /* ── Areas of Interest (Chip cloud) ─────────────────── */
  .ap-interests {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
    justify-content: center;
    animation: fadeIn 0.5s ease-out 0.9s both;
  }

  .ap-chip {
    padding: 0.3rem 0.75rem;
    background: rgba(247, 183, 49, 0.06);
    border: 1px solid rgba(247, 183, 49, 0.18);
    color: var(--gold);
    border-radius: 16px;
    font-size: 0.75rem;
    transition: all 0.2s ease;
    cursor: default;
  }

  .ap-chip:hover {
    background: rgba(247, 183, 49, 0.12);
    transform: scale(1.06);
    border-color: rgba(247, 183, 49, 0.35);
  }

  /* ── Contact (Icon buttons) ─────────────────────────── */
  .ap-contact {
    display: flex;
    justify-content: center;
    gap: 0.9rem;
    animation: fadeInUp 0.5s ease-out 1.1s both;
  }

  .ap-btn {
    display: inline-flex;
    align-items: center;
    gap: 0.45rem;
    padding: 0.55rem 1.1rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    color: var(--text);
    text-decoration: none;
    font-size: 0.82rem;
    font-weight: 500;
    transition: all 0.25s ease;
    backdrop-filter: blur(8px);
  }

  .ap-btn svg {
    width: 16px;
    height: 16px;
    stroke: currentColor;
    fill: none;
    stroke-width: 2;
    stroke-linecap: round;
    stroke-linejoin: round;
    transition: transform 0.25s ease;
  }

  .ap-btn:hover {
    border-color: var(--accent);
    color: var(--accent);
    box-shadow: 0 4px 16px var(--shadow);
    transform: translateY(-2px);
  }

  .ap-btn:hover svg {
    transform: scale(1.15);
  }

  /* ── Quote ──────────────────────────────────────────── */
  .ap-quote {
    text-align: center;
    font-size: 0.85rem;
    color: var(--text-secondary);
    font-style: italic;
    margin-top: 0.25rem;
    animation: fadeIn 0.6s ease-out 1.3s both;
  }

  .ap-quote::before {
    content: '“';
    color: var(--accent);
    font-size: 1.2rem;
    margin-right: 0.2rem;
  }

  .ap-quote::after {
    content: '”';
    color: var(--accent);
    font-size: 1.2rem;
    margin-left: 0.2rem;
  }

  /* ── Keyframe Utilities ─────────────────────────────── */
  @keyframes fadeInDown {
    from { opacity: 0; transform: translateY(-18px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeInUp {
    from { opacity: 0; transform: translateY(18px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to   { opacity: 1; }
  }

  /* ── Responsive ─────────────────────────────────────── */
  @media (max-width: 768px) {
    .aryan-profile {
      min-height: auto;
      overflow-y: auto;
      padding: 1.5rem 1rem;
      gap: 1.5rem;
    }

    .ap-content {
      gap: 1.5rem;
    }

    .ap-projects {
      grid-template-columns: 1fr;
    }

    .ap-tagline {
      white-space: normal;
      border-right: none;
      width: auto;
      animation: fadeIn 1s ease-out 0.3s both;
    }

    .ap-focus {
      font-size: 0.75rem;
    }
  }
&lt;/style&gt;

&lt;!-- ═══════════════════════════════════════════════════════ --&gt;
&lt;!--  HTML CONTENT                                         --&gt;
&lt;!-- ═══════════════════════════════════════════════════════ --&gt;

&lt;div class="aryan-profile"&gt;

  &lt;div class="ap-content"&gt;

    &lt;!-- HEADER: Name + Typing Tagline + Mini-Bio --&gt;
    &lt;div class="ap-header"&gt;
      &lt;div class="ap-name"&gt;Aryan Kumar Chowdhury&lt;/div&gt;
      &lt;div class="ap-typewrap"&gt;
        &lt;div class="ap-tagline"&gt;Building knowledge systems from first principles.&lt;/div&gt;
      &lt;/div&gt;
      &lt;p class="ap-bio"&gt;
        Reconstructing ideas from the ground up — validating them experimentally.  
        I care more about understanding &lt;b&gt;why&lt;/b&gt; a system works than simply learning how to use it.
      &lt;/p&gt;
    &lt;/div&gt;

    &lt;!-- CURRENT FOCUS: Compact status strip --&gt;
    &lt;div class="ap-focus"&gt;
      &lt;span class="ap-pulse"&gt;&lt;/span&gt;
      Currently:
      &lt;span&gt;Data Science Portfolio&lt;/span&gt;
      &lt;span&gt;ML Internals&lt;/span&gt;
      &lt;span&gt;Knowledge Systems&lt;/span&gt;
      &lt;span&gt;Public Learning&lt;/span&gt;
    &lt;/div&gt;

    &lt;!-- SKILLS: Grouped badge strip --&gt;
    &lt;div class="ap-skills"&gt;
      &lt;div class="ap-skillrow"&gt;
        &lt;span class="ap-badge ml"&gt;&lt;span class="dot"&gt;&lt;/span&gt;Python&lt;/span&gt;
        &lt;span class="ap-badge ml"&gt;&lt;span class="dot"&gt;&lt;/span&gt;Pandas&lt;/span&gt;
        &lt;span class="ap-badge ml"&gt;&lt;span class="dot"&gt;&lt;/span&gt;NumPy&lt;/span&gt;
        &lt;span class="ap-badge ml"&gt;&lt;span class="dot"&gt;&lt;/span&gt;Scikit-learn&lt;/span&gt;
        &lt;span class="ap-badge ml"&gt;&lt;span class="dot"&gt;&lt;/span&gt;TensorFlow&lt;/span&gt;
        &lt;span class="ap-badge ml"&gt;&lt;span class="dot"&gt;&lt;/span&gt;PyTorch&lt;/span&gt;
        &lt;span class="ap-badge data"&gt;&lt;span class="dot"&gt;&lt;/span&gt;SQL&lt;/span&gt;
        &lt;span class="ap-badge data"&gt;&lt;span class="dot"&gt;&lt;/span&gt;Power BI&lt;/span&gt;
        &lt;span class="ap-badge data"&gt;&lt;span class="dot"&gt;&lt;/span&gt;Excel&lt;/span&gt;
        &lt;span class="ap-badge fe"&gt;&lt;span class="dot"&gt;&lt;/span&gt;React&lt;/span&gt;
        &lt;span class="ap-badge fe"&gt;&lt;span class="dot"&gt;&lt;/span&gt;TypeScript&lt;/span&gt;
        &lt;span class="ap-badge fe"&gt;&lt;span class="dot"&gt;&lt;/span&gt;Tailwind&lt;/span&gt;
        &lt;span class="ap-badge tool"&gt;&lt;span class="dot"&gt;&lt;/span&gt;Git&lt;/span&gt;
        &lt;span class="ap-badge tool"&gt;&lt;span class="dot"&gt;&lt;/span&gt;Docker&lt;/span&gt;
        &lt;span class="ap-badge tool"&gt;&lt;span class="dot"&gt;&lt;/span&gt;Linux&lt;/span&gt;
      &lt;/div&gt;
    &lt;/div&gt;

    &lt;!-- PROJECTS: 3-card horizontal layout --&gt;
    &lt;div class="ap-projects"&gt;

      &lt;div class="ap-card"&gt;
        &lt;div class="ap-card-title"&gt;
          &lt;svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"&gt;&lt;polyline points="22 12 18 12 15 21 9 3 6 12 2 12"&gt;&lt;/polyline&gt;&lt;/svg&gt;
          ML Benchmark Suite
        &lt;/div&gt;
        &lt;div class="ap-card-desc"&gt;
          9 regression algorithms benchmarked on 10,000+ housing records with systematic cross-validation.
        &lt;/div&gt;
        &lt;div class="ap-card-tech"&gt;
          &lt;span class="ap-techtag"&gt;Python&lt;/span&gt;
          &lt;span class="ap-techtag"&gt;Scikit-learn&lt;/span&gt;
          &lt;span class="ap-techtag"&gt;Statistics&lt;/span&gt;
        &lt;/div&gt;
      &lt;/div&gt;

      &lt;div class="ap-card"&gt;
        &lt;div class="ap-card-title"&gt;
          &lt;svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"&gt;&lt;path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"&gt;&lt;/path&gt;&lt;polyline points="3.27 6.96 12 12.01 20.73 6.96"&gt;&lt;/polyline&gt;&lt;line x1="12" y1="22.08" x2="12" y2="12"&gt;&lt;/line&gt;&lt;/svg&gt;
          Retail Sentiment & Placement
        &lt;/div&gt;
        &lt;div class="ap-card-desc"&gt;
          Sentiment analysis + demographic modeling + Power BI dashboards for high-value store zones.
        &lt;/div&gt;
        &lt;div class="ap-card-tech"&gt;
          &lt;span class="ap-techtag"&gt;NLP&lt;/span&gt;
          &lt;span class="ap-techtag"&gt;Power BI&lt;/span&gt;
          &lt;span class="ap-techtag"&gt;DAX&lt;/span&gt;
        &lt;/div&gt;
      &lt;/div&gt;

      &lt;div class="ap-card"&gt;
        &lt;div class="ap-card-title"&gt;
          &lt;svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"&gt;&lt;ellipse cx="12" cy="5" rx="9" ry="3"&gt;&lt;/ellipse&gt;&lt;path d="M21 12c0 1.66-4 3-9 3s-9-1.34-9-3"&gt;&lt;/path&gt;&lt;path d="M3 5v14c0 1.66 4 3 9 3s9-1.34 9-3V5"&gt;&lt;/path&gt;&lt;/svg&gt;
          Supply Chain SQL Analytics
        &lt;/div&gt;
        &lt;div class="ap-card-desc"&gt;
          Advanced SQL (CTEs, window functions) on 50,000+ transactions to identify cost bottlenecks.
        &lt;/div&gt;
        &lt;div class="ap-card-tech"&gt;
          &lt;span class="ap-techtag"&gt;SQL&lt;/span&gt;
          &lt;span class="ap-techtag"&gt;ETL&lt;/span&gt;
          &lt;span class="ap-techtag"&gt;Analytics&lt;/span&gt;
        &lt;/div&gt;
      &lt;/div&gt;

    &lt;/div&gt;

    &lt;!-- INTERESTS: Chip cloud (condensed from table) --&gt;
    &lt;div class="ap-interests"&gt;
      &lt;span class="ap-chip"&gt;Statistics & Probability&lt;/span&gt;
      &lt;span class="ap-chip"&gt;Bayesian Methods&lt;/span&gt;
      &lt;span class="ap-chip"&gt;Machine Learning&lt;/span&gt;
      &lt;span class="ap-chip"&gt;Data Science&lt;/span&gt;
      &lt;span class="ap-chip"&gt;Optimization&lt;/span&gt;
      &lt;span class="ap-chip"&gt;VLSI&lt;/span&gt;
      &lt;span class="ap-chip"&gt;Knowledge Systems&lt;/span&gt;
      &lt;span class="ap-chip"&gt;Ontologies&lt;/span&gt;
    &lt;/div&gt;

    &lt;!-- CONTACT: Icon buttons --&gt;
    &lt;div class="ap-contact"&gt;
      &lt;a href="mailto:chowdhuryaryan81@gmail.com" class="ap-btn"&gt;
        &lt;svg viewBox="0 0 24 24"&gt;&lt;path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"&gt;&lt;/path&gt;&lt;polyline points="22,6 12,13 2,6"&gt;&lt;/polyline&gt;&lt;/svg&gt;
        Email
      &lt;/a&gt;
      &lt;a href="https://linkedin.com/in/aryan-chowdhury-b50069407/" class="ap-btn"&gt;
        &lt;svg viewBox="0 0 24 24"&gt;&lt;path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"&gt;&lt;/path&gt;&lt;rect x="2" y="9" width="4" height="12"&gt;&lt;/rect&gt;&lt;circle cx="4" cy="4" r="2"&gt;&lt;/circle&gt;&lt;/svg&gt;
        LinkedIn
      &lt;/a&gt;
      &lt;a href="https://aryanchowdhury-art.github.io/portfolio-2025/" class="ap-btn"&gt;
        &lt;svg viewBox="0 0 24 24"&gt;&lt;circle cx="12" cy="12" r="10"&gt;&lt;/circle&gt;&lt;line x1="2" y1="12" x2="22" y2="12"&gt;&lt;/line&gt;&lt;path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"&gt;&lt;/path&gt;&lt;/svg&gt;
        Portfolio
      &lt;/a&gt;
    &lt;/div&gt;

    &lt;!-- QUOTE --&gt;
    &lt;div class="ap-quote"&gt;
      Every model is a hypothesis until reality disagrees.
    &lt;/div&gt;

  &lt;/div&gt;
&lt;/div&gt;

&lt;!--
  DESIGN NOTES FOR ARYAN
  ======================
  1. One-screen fit: The container uses 100vh on desktop. Content is spaced
     with flex gaps so it naturally compresses to fit without scrolling.
     On mobile (&lt;768px) it switches to auto height for readability.

  2. Reading patterns:
     • F-Pattern: Name (top, heavy) → tagline → bio → skills cascade
       down the center-left visual axis.
     • Z-Pattern: Eye moves from header (top) → projects (middle, left-to-right)
       → contact (bottom right). The gradient accent line on cards guides this.

  3. Animation rationale:
     • Typing effect: Draws attention to the philosophical tagline.
     • Staggered fade-ins (0.1s increments): Creates a "reveal" flow without
       overwhelming the reader.
     • Hover lifts on cards/badges: Affords interactivity in a static page.
     • Ambient gradient drift: Adds life to the background without distraction.

  4. Color system:
     • Teal (#00d4aa) = Primary action / ML & Data badges
     • Cyan (#00a8e8) = Secondary / SQL & Analytics
     • Gold (#f7b731) = Highlights / Frontend & Interests
     • Dark surface = GitHub-native dark mode feel

  5. Content condensation:
     • "About" + "Current Focus" paragraphs → merged into bio + focus strip.
     • Areas of Interest table → chip cloud (scannable, no table borders).
     • Tech stack list → categorized pills with color-coded dots.
     • 4 projects → top 3 featured (most visual impact), LLM pipeline implied
       in "Knowledge Systems" focus chip.

  6. GitHub constraints handled:
     • Zero JavaScript. All motion is CSS @keyframes.
     • No external images; icons are inline SVG.
     • Google Fonts imported via @import (fallback to system stack if blocked).
     • If GitHub's sanitizer strips &lt;style&gt;, convert this to inline styles
       using the same CSS variable values.
--&gt;
