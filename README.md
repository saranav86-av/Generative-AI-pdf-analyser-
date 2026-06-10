# Generative-AI-pdf-analyser-
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>AI PDF Analyzer — Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=Inter:wght@300;400;500&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />
<style>
  :root {
    --bg:        #0b0c14;
    --surface:   #12131f;
    --card:      #181929;
    --border:    #2a2c42;
    --accent:    #6c63ff;
    --accent2:   #a78bfa;
    --glow:      rgba(108,99,255,.25);
    --text:      #e8e8f0;
    --muted:     #8888aa;
    --mono:      'JetBrains Mono', monospace;
    --display:   'Space Grotesk', sans-serif;
    --body:      'Inter', sans-serif;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--body);
    font-size: 16px;
    line-height: 1.6;
    overflow-x: hidden;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 18px 6vw;
    background: rgba(11,12,20,.85);
    backdrop-filter: blur(14px);
    border-bottom: 1px solid var(--border);
  }
  .nav-logo {
    font-family: var(--display);
    font-weight: 700; font-size: 1.05rem;
    color: var(--accent2);
    letter-spacing: -.01em;
  }
  .nav-links { display: flex; gap: 28px; list-style: none; }
  .nav-links a {
    color: var(--muted); text-decoration: none;
    font-size: .875rem; font-weight: 500;
    transition: color .2s;
  }
  .nav-links a:hover { color: var(--text); }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    text-align: center;
    padding: 120px 6vw 80px;
    position: relative;
    overflow: hidden;
  }
  .hero::before {
    content: '';
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse 70% 55% at 50% 40%, rgba(108,99,255,.18) 0%, transparent 70%),
      radial-gradient(ellipse 40% 30% at 20% 80%, rgba(167,139,250,.1) 0%, transparent 60%);
    pointer-events: none;
  }

  /* animated grid lines */
  .grid-lines {
    position: absolute; inset: 0; pointer-events: none;
    background-image:
      linear-gradient(var(--border) 1px, transparent 1px),
      linear-gradient(90deg, var(--border) 1px, transparent 1px);
    background-size: 60px 60px;
    opacity: .25;
    mask-image: radial-gradient(ellipse 80% 70% at 50% 50%, black 30%, transparent 80%);
  }

  .hero-badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(108,99,255,.12);
    border: 1px solid rgba(108,99,255,.35);
    border-radius: 100px;
    padding: 6px 16px;
    font-family: var(--mono); font-size: .75rem;
    color: var(--accent2);
    margin-bottom: 28px;
    position: relative;
  }
  .hero-badge::before {
    content: ''; width: 7px; height: 7px; border-radius: 50%;
    background: var(--accent); flex-shrink: 0;
    box-shadow: 0 0 8px var(--accent);
    animation: pulse 2s infinite;
  }
  @keyframes pulse {
    0%,100% { opacity: 1; } 50% { opacity: .4; }
  }

  .hero h1 {
    font-family: var(--display);
    font-size: clamp(2.4rem, 6vw, 4.2rem);
    font-weight: 700; line-height: 1.08;
    letter-spacing: -.03em;
    margin-bottom: 22px;
  }
  .hero h1 span {
    background: linear-gradient(135deg, #6c63ff 0%, #a78bfa 60%, #c4b5fd 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .hero-sub {
    max-width: 560px; margin: 0 auto 36px;
    color: var(--muted); font-size: 1.05rem; line-height: 1.65;
  }
  .hero-meta {
    font-family: var(--mono); font-size: .8rem;
    color: var(--muted); margin-bottom: 44px;
    display: flex; gap: 24px; justify-content: center; flex-wrap: wrap;
  }
  .hero-meta span { display: flex; align-items: center; gap: 6px; }
  .hero-meta span::before {
    content: '▸'; color: var(--accent); font-size: .7rem;
  }

  .btn-row { display: flex; gap: 14px; justify-content: center; flex-wrap: wrap; }
  .btn {
    display: inline-flex; align-items: center; gap: 8px;
    padding: 12px 26px;
    border-radius: 8px; border: none; cursor: pointer;
    font-family: var(--display); font-size: .9rem; font-weight: 600;
    text-decoration: none; transition: all .2s;
  }
  .btn-primary {
    background: var(--accent); color: #fff;
    box-shadow: 0 0 24px var(--glow);
  }
  .btn-primary:hover { background: #7c74ff; transform: translateY(-1px); box-shadow: 0 4px 32px var(--glow); }
  .btn-ghost {
    background: transparent; color: var(--text);
    border: 1px solid var(--border);
  }
  .btn-ghost:hover { border-color: var(--accent2); color: var(--accent2); transform: translateY(-1px); }

  /* ── SECTION SHELL ── */
  section { padding: 96px 6vw; }
  .section-eyebrow {
    font-family: var(--mono); font-size: .75rem; letter-spacing: .12em;
    text-transform: uppercase; color: var(--accent);
    margin-bottom: 14px;
  }
  .section-title {
    font-family: var(--display); font-size: clamp(1.8rem, 3.5vw, 2.6rem);
    font-weight: 700; letter-spacing: -.025em; line-height: 1.15;
    margin-bottom: 14px;
  }
  .section-sub {
    color: var(--muted); max-width: 540px; font-size: .97rem;
    margin-bottom: 60px; line-height: 1.65;
  }

  /* ── PROBLEM + OBJECTIVE ── */
  .two-col {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 28px;
  }
  .info-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 32px 28px;
    transition: border-color .25s, transform .25s;
    position: relative; overflow: hidden;
  }
  .info-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    opacity: 0; transition: opacity .25s;
  }
  .info-card:hover { border-color: var(--accent); transform: translateY(-3px); }
  .info-card:hover::before { opacity: 1; }
  .card-icon {
    width: 44px; height: 44px; border-radius: 10px;
    background: rgba(108,99,255,.15);
    display: flex; align-items: center; justify-content: center;
    font-size: 1.3rem; margin-bottom: 18px;
  }
  .info-card h3 {
    font-family: var(--display); font-weight: 600; font-size: 1.1rem;
    margin-bottom: 12px;
  }
  .info-card ul { list-style: none; }
  .info-card ul li {
    color: var(--muted); font-size: .9rem; padding: 5px 0;
    display: flex; align-items: flex-start; gap: 10px;
  }
  .info-card ul li::before {
    content: '→'; color: var(--accent); flex-shrink: 0; margin-top: 1px;
  }

  /* ── ARCHITECTURE ── */
  #architecture { background: var(--surface); }
  .arch-wrapper {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 48px; align-items: start;
  }
  @media (max-width: 800px) { .arch-wrapper { grid-template-columns: 1fr; } }

  .pipeline {
    display: flex; flex-direction: column; gap: 0;
  }
  .pipe-step {
    display: flex; align-items: center; gap: 16px;
    padding: 14px 20px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    font-family: var(--mono); font-size: .82rem;
    transition: border-color .2s, background .2s;
    position: relative;
  }
  .pipe-step:hover { border-color: var(--accent); background: rgba(108,99,255,.07); }
  .pipe-step-num {
    width: 28px; height: 28px; border-radius: 7px;
    background: rgba(108,99,255,.2); color: var(--accent2);
    display: flex; align-items: center; justify-content: center;
    font-size: .75rem; font-weight: 600; flex-shrink: 0;
  }
  .pipe-arrow {
    text-align: center; color: var(--accent); font-size: .7rem;
    padding: 3px 0; letter-spacing: 2px;
  }

  .arch-desc h3 {
    font-family: var(--display); font-size: 1.2rem; font-weight: 600;
    margin-bottom: 16px;
  }
  .arch-desc p { color: var(--muted); font-size: .9rem; line-height: 1.7; margin-bottom: 22px; }

  .tag-list { display: flex; flex-wrap: wrap; gap: 10px; }
  .tag {
    padding: 6px 14px;
    border-radius: 6px;
    border: 1px solid var(--border);
    font-family: var(--mono); font-size: .75rem;
    color: var(--muted); background: var(--card);
    transition: all .2s;
  }
  .tag:hover { border-color: var(--accent2); color: var(--accent2); }

  /* ── TECH STACK ── */
  .tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
    gap: 20px;
  }
  .tech-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 28px 20px;
    text-align: center;
    transition: all .25s;
    cursor: default;
  }
  .tech-card:hover { border-color: var(--accent); transform: translateY(-4px); box-shadow: 0 12px 40px var(--glow); }
  .tech-emoji { font-size: 2rem; margin-bottom: 12px; display: block; }
  .tech-name {
    font-family: var(--display); font-weight: 600; font-size: .95rem;
    margin-bottom: 6px;
  }
  .tech-role { color: var(--muted); font-size: .78rem; }

  /* ── FEATURES ── */
  #features { background: var(--surface); }
  .feat-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 22px;
  }
  .feat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 26px 24px;
    display: flex; gap: 18px;
    transition: all .25s;
  }
  .feat-card:hover { border-color: var(--accent2); transform: translateY(-3px); }
  .feat-icon {
    font-size: 1.5rem; flex-shrink: 0;
    width: 44px; height: 44px; border-radius: 10px;
    background: rgba(108,99,255,.12);
    display: flex; align-items: center; justify-content: center;
  }
  .feat-body h4 { font-family: var(--display); font-size: 1rem; font-weight: 600; margin-bottom: 6px; }
  .feat-body p { color: var(--muted); font-size: .84rem; line-height: 1.55; }

  /* ── RESULTS ── */
  .results-row {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 24px; margin-bottom: 56px;
  }
  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 32px 24px; text-align: center;
    transition: all .25s;
    position: relative; overflow: hidden;
  }
  .stat-card::after {
    content: '';
    position: absolute; bottom: 0; left: 0; right: 0; height: 3px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
  }
  .stat-card:hover { transform: translateY(-3px); box-shadow: 0 12px 40px var(--glow); }
  .stat-val {
    font-family: var(--display); font-size: 2.4rem; font-weight: 700;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 8px;
  }
  .stat-label { color: var(--muted); font-size: .85rem; }

  /* ── FUTURE / CONCLUSION ── */
  #future { background: var(--surface); }
  .future-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 20px;
  }
  .future-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 26px 24px;
    transition: all .25s;
  }
  .future-card:hover { border-color: var(--accent); transform: translateY(-3px); }
  .future-card h4 { font-family: var(--display); font-size: .98rem; font-weight: 600; margin-bottom: 8px; }
  .future-card p { color: var(--muted); font-size: .84rem; line-height: 1.55; }
  .future-num {
    font-family: var(--mono); font-size: .72rem; color: var(--accent);
    margin-bottom: 14px; letter-spacing: .1em;
  }

  /* ── CONCLUSION BANNER ── */
  .conclusion {
    border-radius: 20px;
    background: linear-gradient(135deg, rgba(108,99,255,.15) 0%, rgba(167,139,250,.08) 100%);
    border: 1px solid rgba(108,99,255,.3);
    padding: 56px 48px;
    text-align: center;
    position: relative; overflow: hidden;
  }
  .conclusion::before {
    content: '';
    position: absolute; top: -50%; left: -20%; width: 60%; height: 200%;
    background: radial-gradient(ellipse, rgba(108,99,255,.12) 0%, transparent 70%);
    pointer-events: none;
  }
  .conclusion h2 {
    font-family: var(--display); font-size: clamp(1.6rem, 3vw, 2.2rem);
    font-weight: 700; letter-spacing: -.025em; margin-bottom: 18px;
  }
  .conclusion p {
    color: var(--muted); max-width: 560px; margin: 0 auto 36px;
    font-size: .97rem; line-height: 1.65;
  }
  .conclusion-points {
    display: flex; gap: 36px; justify-content: center; flex-wrap: wrap;
    margin-bottom: 40px;
  }
  .conclusion-point {
    display: flex; align-items: center; gap: 10px;
    font-size: .88rem; color: var(--text);
  }
  .conclusion-point::before {
    content: '✓';
    width: 22px; height: 22px; border-radius: 50%;
    background: rgba(108,99,255,.2); color: var(--accent2);
    display: flex; align-items: center; justify-content: center;
    font-size: .7rem; flex-shrink: 0;
  }

  /* ── FOOTER ── */
  footer {
    border-top: 1px solid var(--border);
    padding: 32px 6vw;
    display: flex; align-items: center; justify-content: space-between;
    flex-wrap: wrap; gap: 16px;
    color: var(--muted); font-size: .82rem;
  }
  .footer-logo { font-family: var(--display); font-weight: 600; color: var(--accent2); }
  .footer-links { display: flex; gap: 22px; }
  .footer-links a { color: var(--muted); text-decoration: none; transition: color .2s; }
  .footer-links a:hover { color: var(--text); }

  /* ── SCROLL REVEAL ── */
  .reveal {
    opacity: 0; transform: translateY(28px);
    transition: opacity .55s ease, transform .55s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* ── DEMO MOCKUP ── */
  .mockup-wrap { position: relative; }
  .mockup {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px; overflow: hidden;
    box-shadow: 0 24px 80px rgba(0,0,0,.45);
  }
  .mockup-bar {
    background: #1c1d2e;
    padding: 12px 18px;
    display: flex; align-items: center; gap: 8px;
    border-bottom: 1px solid var(--border);
  }
  .dot { width: 10px; height: 10px; border-radius: 50%; }
  .dot-r { background: #ff5f57; } .dot-y { background: #febc2e; } .dot-g { background: #28c840; }
  .mockup-body { padding: 24px; }
  .mock-input {
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 8px; padding: 14px 18px;
    font-family: var(--mono); font-size: .8rem; color: var(--muted);
    margin-bottom: 16px;
  }
  .mock-q {
    background: rgba(108,99,255,.1);
    border: 1px solid rgba(108,99,255,.25);
    border-radius: 8px; padding: 14px 18px;
    font-size: .88rem; color: var(--text);
    margin-bottom: 12px;
  }
  .mock-a {
    background: rgba(167,139,250,.07);
    border: 1px solid rgba(167,139,250,.2);
    border-radius: 8px; padding: 14px 18px;
    font-size: .84rem; color: var(--muted); line-height: 1.6;
  }
  .mock-a strong { color: var(--accent2); }
  .mock-label {
    font-family: var(--mono); font-size: .68rem; color: var(--accent);
    text-transform: uppercase; letter-spacing: .1em; margin-bottom: 6px;
  }

  @media (max-width: 600px) {
    .conclusion { padding: 36px 24px; }
    .nav-links { display: none; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-logo">AI PDF Analyzer</div>
  <ul class="nav-links">
    <li><a href="#problem">Problem</a></li>
    <li><a href="#architecture">Architecture</a></li>
    <li><a href="#stack">Tech Stack</a></li>
    <li><a href="#features">Features</a></li>
    <li><a href="#results">Results</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="grid-lines"></div>
  <div class="hero-badge">Amazon Summer School 2026 · Generative AI Project</div>
  <h1>
    PDF Question-Answering<br/>
    <span>with RAG & Generative AI</span>
  </h1>
  <p class="hero-sub">
    Upload any PDF, ask questions in plain English, and get precise answers extracted directly from your document — powered by Gemini, FAISS, and LangChain.
  </p>
  <div class="hero-meta">
    <span>RAG Architecture</span>
    <span>Gemini LLM</span>
    <span>Vector Search</span>
    <span>Streamlit UI</span>
  </div>
  <div class="btn-row">
    <a href="#architecture" class="btn btn-primary">Explore Architecture ↓</a>
    <a href="#features" class="btn btn-ghost">View Features</a>
  </div>
</section>

<!-- PROBLEM + OBJECTIVE -->
<section id="problem">
  <div class="section-eyebrow reveal">Why This Exists</div>
  <h2 class="section-title reveal">The Problem & Objective</h2>
  <p class="section-sub reveal">Large documents are time-consuming to navigate. This system removes that friction entirely.</p>
  <div class="two-col">
    <div class="info-card reveal">
      <div class="card-icon">🔍</div>
      <h3>Problem Statement</h3>
      <ul>
        <li>Large PDFs are difficult to navigate manually</li>
        <li>Keyword search misses context and semantic meaning</li>
        <li>Users spend hours finding answers buried in documents</li>
        <li>No easy way to extract structured insights at scale</li>
      </ul>
    </div>
    <div class="info-card reveal">
      <div class="card-icon">🎯</div>
      <h3>Project Objective</h3>
      <ul>
        <li>Upload one or multiple PDFs instantly</li>
        <li>Ask questions in natural language — no query syntax</li>
        <li>Generate accurate, context-aware answers from document content</li>
        <li>Reduce research and search time dramatically</li>
      </ul>
    </div>
  </div>
</section>

<!-- ARCHITECTURE -->
<section id="architecture">
  <div class="section-eyebrow reveal">How It Works</div>
  <h2 class="section-title reveal">System Architecture</h2>
  <p class="section-sub reveal">A clean Retrieval-Augmented Generation (RAG) pipeline: ingest, embed, retrieve, and generate.</p>
  <div class="arch-wrapper">
    <div class="pipeline reveal">
      <div class="pipe-step"><div class="pipe-step-num">01</div> PDF Upload</div>
      <div class="pipe-arrow">↓</div>
      <div class="pipe-step"><div class="pipe-step-num">02</div> Text Extraction</div>
      <div class="pipe-arrow">↓</div>
      <div class="pipe-step"><div class="pipe-step-num">03</div> Chunking</div>
      <div class="pipe-arrow">↓</div>
      <div class="pipe-step"><div class="pipe-step-num">04</div> Embeddings (HuggingFace)</div>
      <div class="pipe-arrow">↓</div>
      <div class="pipe-step"><div class="pipe-step-num">05</div> FAISS Vector Database</div>
      <div class="pipe-arrow">↓</div>
      <div class="pipe-step"><div class="pipe-step-num">06</div> User Query</div>
      <div class="pipe-arrow">↓</div>
      <div class="pipe-step"><div class="pipe-step-num">07</div> Similarity Search</div>
      <div class="pipe-arrow">↓</div>
      <div class="pipe-step"><div class="pipe-step-num">08</div> Gemini LLM</div>
      <div class="pipe-arrow">↓</div>
      <div class="pipe-step"><div class="pipe-step-num">09</div> Generated Answer</div>
    </div>
    <div class="arch-desc reveal">
      <h3>RAG: Retrieval-Augmented Generation</h3>
      <p>
        Rather than sending an entire PDF to the LLM (expensive and limited), this system first splits the document into semantic chunks, converts them into vector embeddings, and stores them in FAISS — a fast similarity search index.
      </p>
      <p>
        When a user asks a question, the query is embedded and matched against the stored chunks. Only the most relevant passages are retrieved and passed to Gemini, ensuring accurate, grounded answers — not hallucinations.
      </p>
      <div class="tag-list">
        <span class="tag">LangChain</span>
        <span class="tag">FAISS</span>
        <span class="tag">Gemini API</span>
        <span class="tag">HuggingFace Embeddings</span>
        <span cl
