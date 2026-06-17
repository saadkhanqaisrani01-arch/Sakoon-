<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>The Free AI Catalog</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Special+Elite&family=IBM+Plex+Mono:wght@400;500;600&family=Source+Sans+3:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --paper:#ECE7D8;
    --paper-card:#E2DCC8;
    --paper-card-hover:#D8D0B8;
    --ink:#272421;
    --ink-soft:#5B564E;
    --drawer:#5B4636;
    --drawer-dark:#3F2F25;
    --manila:#CBA876;
    --manila-dark:#B08F5E;
    --stamp:#A23B2E;
    --library:#3F5C49;
    --rule:rgba(39,36,33,0.18);
    --font-display:'Special Elite', cursive;
    --font-body:'Source Sans 3', sans-serif;
    --font-mono:'IBM Plex Mono', monospace;
  }

  *{box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    margin:0;
    background:var(--paper);
    color:var(--ink);
    font-family:var(--font-body);
    line-height:1.5;
    -webkit-font-smoothing:antialiased;
  }
  a{color:var(--library);}
  img{max-width:100%;}

  /* subtle paper texture via layered gradients */
  body{
    background-image:
      radial-gradient(rgba(39,36,33,0.035) 1px, transparent 1px);
    background-size:3px 3px;
  }

  .skip-link{position:absolute;left:-9999px;}
  .skip-link:focus{
    left:8px; top:8px; background:var(--ink); color:var(--paper);
    padding:8px 14px; border-radius:4px; z-index:200; font-family:var(--font-mono);
  }

  /* ---------- HERO / DRAWER FRONT ---------- */
  .drawer{
    background:linear-gradient(180deg,var(--drawer) 0%, var(--drawer-dark) 100%);
    padding:3.2rem 1.25rem 2.5rem;
    position:relative;
    border-bottom:6px solid var(--drawer-dark);
  }
  .drawer::before{
    /* drawer pull handle */
    content:"";
    position:absolute;
    top:0; left:50%; transform:translate(-50%,-45%);
    width:64px; height:14px;
    background:#8a6f56;
    border-radius:7px;
    box-shadow:0 2px 0 rgba(0,0,0,0.35) inset, 0 2px 3px rgba(0,0,0,0.4);
  }
  .drawer-inner{
    max-width:880px;
    margin:0 auto;
    text-align:center;
  }
  .label-holder{
    display:inline-block;
    background:var(--manila);
    border:2px solid var(--manila-dark);
    border-radius:2px;
    padding:0.85rem 1.6rem 0.7rem;
    box-shadow:0 3px 0 rgba(0,0,0,0.25), 0 6px 14px rgba(0,0,0,0.3);
    transform:rotate(-0.6deg);
  }
  .label-holder h1{
    margin:0;
    font-family:var(--font-display);
    font-size:clamp(1.5rem, 5vw, 2.5rem);
    color:var(--ink);
    letter-spacing:0.04em;
  }
  .catalogued{
    margin-top:0.9rem;
    font-family:var(--font-mono);
    font-size:0.72rem;
    letter-spacing:0.08em;
    color:#cfc4ad;
    text-transform:uppercase;
  }
  .drawer-sub{
    margin:1.1rem auto 0;
    max-width:520px;
    color:#e7e0cf;
    font-size:1rem;
  }

  .search-wrap{
    margin:1.6rem auto 0;
    max-width:480px;
    position:relative;
  }
  .search-wrap input{
    width:100%;
    font-family:var(--font-mono);
    font-size:0.95rem;
    padding:0.85rem 1rem 0.85rem 2.4rem;
    border:none;
    border-radius:3px;
    background:var(--paper);
    color:var(--ink);
    box-shadow:inset 0 0 0 1px var(--rule), 0 4px 10px rgba(0,0,0,0.25);
  }
  .search-wrap input::placeholder{color:var(--ink-soft);}
  .search-wrap input:focus{outline:3px solid var(--manila); outline-offset:1px;}
  .search-wrap::before{
    content:"⌕";
    position:absolute;
    left:0.85rem; top:50%; transform:translateY(-50%);
    font-size:1.1rem; color:var(--ink-soft);
  }

  /* ---------- TABS ---------- */
  .tabs-bar{
    background:var(--paper-card);
    border-bottom:1px solid var(--rule);
    position:sticky;
    top:0;
    z-index:50;
  }
  .tabs{
    max-width:1080px;
    margin:0 auto;
    display:flex;
    gap:0.4rem;
    overflow-x:auto;
    padding:0.7rem 1rem;
    scrollbar-width:thin;
  }
  .tab{
    flex:0 0 auto;
    font-family:var(--font-mono);
    font-size:0.74rem;
    letter-spacing:0.04em;
    text-transform:uppercase;
    background:var(--manila);
    color:var(--ink);
    border:1px solid var(--manila-dark);
    border-bottom:none;
    padding:0.5rem 0.85rem 0.45rem;
    border-radius:5px 5px 0 0;
    cursor:pointer;
    transform:translateY(2px);
    transition:transform 0.15s ease, background 0.15s ease;
    white-space:nowrap;
  }
  .tab:hover{transform:translateY(0);}
  .tab[aria-pressed="true"]{
    background:var(--paper);
    border-color:var(--rule);
    border-bottom:3px solid var(--library);
    transform:translateY(0);
    font-weight:600;
  }

  /* ---------- MAIN ---------- */
  main{
    max-width:1080px;
    margin:0 auto;
    padding:2.2rem 1rem 1rem;
  }

  .section-label{
    display:flex;
    align-items:baseline;
    gap:0.7rem;
    margin:2.4rem 0 1rem;
  }
  .section-label:first-child{margin-top:0;}
  .section-label .drawer-no{
    font-family:var(--font-mono);
    font-size:0.72rem;
    color:var(--ink-soft);
    background:var(--paper-card);
    border:1px solid var(--rule);
    padding:0.15rem 0.5rem;
    border-radius:3px;
  }
  .section-label h2{
    font-family:var(--font-display);
    font-size:1.25rem;
    margin:0;
    letter-spacing:0.01em;
  }
  .section-label .rule{
    flex:1;
    height:1px;
    background:repeating-linear-gradient(to right, var(--ink-soft) 0 6px, transparent 6px 11px);
    opacity:0.5;
  }

  .grid{
    display:grid;
    grid-template-columns:repeat(auto-fill, minmax(250px,1fr));
    gap:1rem;
  }

  /* ---------- CARD ---------- */
  .card{
    background:var(--paper-card);
    border:1px solid var(--rule);
    border-radius:3px;
    padding:1.1rem 1.1rem 1rem;
    position:relative;
    box-shadow:0 1px 0 rgba(255,255,255,0.4) inset, 0 2px 5px rgba(39,36,33,0.08);
    transition:transform 0.15s ease, box-shadow 0.15s ease, background 0.15s ease;
    display:flex;
    flex-direction:column;
    gap:0.5rem;
  }
  .card:hover{
    background:var(--paper-card-hover);
    transform:translateY(-2px);
    box-shadow:0 6px 14px rgba(39,36,33,0.16);
  }
  .card-holes{
    position:absolute;
    top:8px; left:0; right:0;
    display:flex;
    justify-content:center;
    gap:18px;
  }
  .card-holes span{
    width:7px; height:7px;
    border-radius:50%;
    background:var(--paper);
    box-shadow:inset 0 1px 2px rgba(0,0,0,0.35);
  }
  .stamp{
    position:absolute;
    top:0.6rem; right:0.6rem;
    font-family:var(--font-mono);
    font-size:0.62rem;
    font-weight:600;
    letter-spacing:0.06em;
    color:var(--stamp);
    border:2px solid var(--stamp);
    border-radius:50%;
    padding:0.38rem 0.3rem;
    line-height:1.05;
    text-align:center;
    width:2.7rem;
    height:2.7rem;
    display:flex;
    align-items:center;
    justify-content:center;
    transform:rotate(-9deg);
    mix-blend-mode:multiply;
    opacity:0.92;
  }
  .card-title{
    font-family:var(--font-display);
    font-size:1.02rem;
    margin:1.1rem 2.7rem 0 0;
  }
  .card-desc{
    font-size:0.88rem;
    color:var(--ink);
    margin:0;
    flex-grow:1;
  }
  .card-note{
    font-family:var(--font-mono);
    font-size:0.7rem;
    color:var(--ink-soft);
    margin:0;
    border-top:1px dashed var(--rule);
    padding-top:0.5rem;
  }
  .card-link{
    font-family:var(--font-mono);
    font-size:0.76rem;
    text-decoration:none;
    color:var(--library);
    font-weight:600;
    align-self:flex-start;
  }
  .card-link:hover{text-decoration:underline;}

  .empty-state{
    font-family:var(--font-mono);
    color:var(--ink-soft);
    text-align:center;
    padding:3rem 1rem;
    display:none;
  }

  footer{
    max-width:1080px;
    margin:2rem auto 0;
    padding:1.6rem 1rem 3rem;
    border-top:1px solid var(--rule);
    font-size:0.8rem;
    color:var(--ink-soft);
  }
  footer p{margin:0.4rem 0;}

  @media (max-width:520px){
    .label-holder{padding:0.7rem 1.1rem 0.6rem;}
    .card-title{margin-right:2.5rem;}
  }

  @media (prefers-reduced-motion: reduce){
    *{transition:none !important; scroll-behavior:auto !important;}
  }
</style>
</head>
<body>
<a class="skip-link" href="#main">Skip to catalog</a>

<header class="drawer">
  <div class="drawer-inner">
    <div class="label-holder">
      <h1>FREE AI TOOLS</h1>
    </div>
    <p class="catalogued">Catalogued June 2026 · 28 entries</p>
    <p class="drawer-sub">A browsable drawer of AI tools you can use today without paying a cent — chat assistants, image and video generators, coding help, and more. Free tiers shift often, so treat the notes here as a starting point, not a guarantee.</p>
    <div class="search-wrap">
      <input type="text" id="search" placeholder="search the catalog — try “image” or “code”" aria-label="Search the catalog">
    </div>
  </div>
</header>

<nav class="tabs-bar" aria-label="Filter by category">
  <div class="tabs" id="tabs"></div>
</nav>

<main id="main">
  <!-- sections injected by JS from data, but written statically below for content/SEO -->

  <section class="section-label-wrap" data-section="chat">
    <div class="section-label"><span class="drawer-no">01</span><h2>Chat &amp; Research</h2><span class="rule"></span></div>
    <div class="grid">
      <article class="card" data-category="chat">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">ChatGPT</h3>
        <p class="card-desc">OpenAI's general-purpose assistant for writing, brainstorming, research, and quick coding help.</p>
        <p class="card-note">Free gets you: a capable model with a daily message cap and built-in image generation.</p>
        <a class="card-link" href="https://chatgpt.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="chat">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Claude</h3>
        <p class="card-desc">Anthropic's assistant, known for careful reasoning, long-document analysis, and clean code.</p>
        <p class="card-note">Free gets you: a daily allowance of messages, no credit card required.</p>
        <a class="card-link" href="https://claude.ai" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="chat">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Gemini</h3>
        <p class="card-desc">Google's assistant, woven into Search, Gmail, and Docs, with built-in image generation.</p>
        <p class="card-note">Free gets you: chat plus a daily quota of image generations.</p>
        <a class="card-link" href="https://gemini.google.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="chat">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Perplexity</h3>
        <p class="card-desc">An AI search engine that answers in plain language and links its sources, instead of just guessing.</p>
        <p class="card-note">Free gets you: unlimited basic search, with a cap on deeper "Pro" searches.</p>
        <a class="card-link" href="https://perplexity.ai" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="chat">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE</span>
        <h3 class="card-title">NotebookLM</h3>
        <p class="card-desc">Upload your own notes, PDFs, or links, and it summarizes them, answers questions, and can narrate an audio overview.</p>
        <p class="card-note">Free gets you: generous notebook and source limits for personal use.</p>
        <a class="card-link" href="https://notebooklm.google.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="chat">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE</span>
        <h3 class="card-title">DeepSeek</h3>
        <p class="card-desc">An open, fast chatbot favored by people who run into usage caps elsewhere.</p>
        <p class="card-note">Free gets you: open web chat, no subscription needed.</p>
        <a class="card-link" href="https://chat.deepseek.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
    </div>
  </section>

  <section class="section-label-wrap" data-section="writing">
    <div class="section-label"><span class="drawer-no">02</span><h2>Writing &amp; Editing</h2><span class="rule"></span></div>
    <div class="grid">
      <article class="card" data-category="writing">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Grammarly</h3>
        <p class="card-desc">Checks grammar, clarity, and tone as you type, in the browser, in docs, or in email.</p>
        <p class="card-note">Free gets you: core corrections and basic tone rewrites.</p>
        <a class="card-link" href="https://grammarly.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="writing">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Notion AI</h3>
        <p class="card-desc">Drafting, summarizing, and translating built directly into a Notion workspace.</p>
        <p class="card-note">Free gets you: a limited number of AI actions inside a free Notion account.</p>
        <a class="card-link" href="https://notion.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="writing">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE</span>
        <h3 class="card-title">Rytr</h3>
        <p class="card-desc">A lightweight writing assistant with templates for ads, emails, and short posts.</p>
        <p class="card-note">Free gets you: a permanent free plan with a monthly character allowance.</p>
        <a class="card-link" href="https://rytr.me" target="_blank" rel="noopener">Visit site →</a>
      </article>
    </div>
  </section>

  <section class="section-label-wrap" data-section="images">
    <div class="section-label"><span class="drawer-no">03</span><h2>Images &amp; Design</h2><span class="rule"></span></div>
    <div class="grid">
      <article class="card" data-category="images">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Gemini (Images)</h3>
        <p class="card-desc">Google's image generator, built into the Gemini app, strong on photorealism and accurate text in images.</p>
        <p class="card-note">Free gets you: a daily image quota, no watermark.</p>
        <a class="card-link" href="https://gemini.google.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="images">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE</span>
        <h3 class="card-title">Microsoft Designer</h3>
        <p class="card-desc">DALL·E-powered image generation in the browser — sign in with any Microsoft account.</p>
        <p class="card-note">Free gets you: unlimited standard-speed generations, plus daily priority boosts.</p>
        <a class="card-link" href="https://designer.microsoft.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="images">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Leonardo AI</h3>
        <p class="card-desc">A model playground with style presets for photoreal, anime, concept art, and product shots.</p>
        <p class="card-note">Free gets you: a daily token allowance across multiple models.</p>
        <a class="card-link" href="https://leonardo.ai" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="images">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Ideogram</h3>
        <p class="card-desc">Specializes in images with legible text — posters, logos, signage, anything words need to read correctly.</p>
        <p class="card-note">Free gets you: a daily batch of generations.</p>
        <a class="card-link" href="https://ideogram.ai" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="images">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Adobe Firefly</h3>
        <p class="card-desc">Trained on licensed assets, which makes its outputs comparatively comfortable to use commercially.</p>
        <p class="card-note">Free gets you: a monthly allowance of generative credits.</p>
        <a class="card-link" href="https://firefly.adobe.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="images">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Canva Magic Studio</h3>
        <p class="card-desc">AI image generation built right into Canva's drag-and-drop design editor.</p>
        <p class="card-note">Free gets you: a starter batch of generations plus the full free design toolkit.</p>
        <a class="card-link" href="https://canva.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
    </div>
  </section>

  <section class="section-label-wrap" data-section="video">
    <div class="section-label"><span class="drawer-no">04</span><h2>Video &amp; Animation</h2><span class="rule"></span></div>
    <div class="grid">
      <article class="card" data-category="video">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Google Veo</h3>
        <p class="card-desc">Google's video model, reachable through the Gemini app, known for realistic motion and physics.</p>
        <p class="card-note">Free gets you: rate-limited access, no subscription required.</p>
        <a class="card-link" href="https://gemini.google.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="video">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE</span>
        <h3 class="card-title">CapCut</h3>
        <p class="card-desc">A video editor with AI captions, background removal, and text-to-video features.</p>
        <p class="card-note">Free gets you: desktop exports without a watermark.</p>
        <a class="card-link" href="https://capcut.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="video">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">HeyGen</h3>
        <p class="card-desc">Turns a script into a talking AI avatar video, with voice cloning and dozens of languages.</p>
        <p class="card-note">Free gets you: a starter plan covering short videos.</p>
        <a class="card-link" href="https://heygen.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="video">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Luma Dream Machine</h3>
        <p class="card-desc">Turns a photo or a short prompt into a cinematic video clip.</p>
        <p class="card-note">Free gets you: a recurring monthly generation allowance.</p>
        <a class="card-link" href="https://lumalabs.ai" target="_blank" rel="noopener">Visit site →</a>
      </article>
    </div>
  </section>

  <section class="section-label-wrap" data-section="audio">
    <div class="section-label"><span class="drawer-no">05</span><h2>Audio, Music &amp; Voice</h2><span class="rule"></span></div>
    <div class="grid">
      <article class="card" data-category="audio">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Suno</h3>
        <p class="card-desc">Generates a full song — vocals, lyrics, and instrumentation — from a single text prompt.</p>
        <p class="card-note">Free gets you: a handful of songs every day.</p>
        <a class="card-link" href="https://suno.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="audio">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">ElevenLabs</h3>
        <p class="card-desc">Realistic text-to-speech and voice cloning, used for narration, dubbing, and assistants.</p>
        <p class="card-note">Free gets you: a monthly character allowance.</p>
        <a class="card-link" href="https://elevenlabs.io" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="audio">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Otter.ai</h3>
        <p class="card-desc">Transcribes meetings and lectures live, then pulls out the key points automatically.</p>
        <p class="card-note">Free gets you: a monthly transcription-minute allowance.</p>
        <a class="card-link" href="https://otter.ai" target="_blank" rel="noopener">Visit site →</a>
      </article>
    </div>
  </section>

  <section class="section-label-wrap" data-section="code">
    <div class="section-label"><span class="drawer-no">06</span><h2>Code &amp; Development</h2><span class="rule"></span></div>
    <div class="grid">
      <article class="card" data-category="code">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">GitHub Copilot</h3>
        <p class="card-desc">Code completions and an in-editor chat from the most widely used coding assistant.</p>
        <p class="card-note">Free gets you: a monthly allowance of completions and chats.</p>
        <a class="card-link" href="https://github.com/features/copilot" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="code">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE</span>
        <h3 class="card-title">Codeium (Windsurf)</h3>
        <p class="card-desc">Inline code completion across most major editors, built for individuals working solo.</p>
        <p class="card-note">Free gets you: unlimited completions, no monthly cap.</p>
        <a class="card-link" href="https://codeium.com" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="code">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Gemini Code Assist</h3>
        <p class="card-desc">Google's coding assistant for VS Code and JetBrains, tuned for navigating large codebases.</p>
        <p class="card-note">Free gets you: a generous individual usage allowance.</p>
        <a class="card-link" href="https://codeassist.google" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="code">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Amazon Q Developer</h3>
        <p class="card-desc">AWS's coding assistant — useful well beyond AWS-specific projects.</p>
        <p class="card-note">Free gets you: unlimited completions plus a monthly allowance of agentic requests.</p>
        <a class="card-link" href="https://aws.amazon.com/q/developer/" target="_blank" rel="noopener">Visit site →</a>
      </article>
    </div>
  </section>

  <section class="section-label-wrap" data-section="productivity">
    <div class="section-label"><span class="drawer-no">07</span><h2>Productivity &amp; Planning</h2><span class="rule"></span></div>
    <div class="grid">
      <article class="card" data-category="productivity">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE TIER</span>
        <h3 class="card-title">Gamma</h3>
        <p class="card-desc">Turns an outline or a prompt into a designed slide deck or one-page document.</p>
        <p class="card-note">Free gets you: a starter batch of AI credits.</p>
        <a class="card-link" href="https://gamma.app" target="_blank" rel="noopener">Visit site →</a>
      </article>
      <article class="card" data-category="productivity">
        <div class="card-holes"><span></span><span></span></div>
        <span class="stamp">FREE</span>
        <h3 class="card-title">Napkin AI</h3>
        <p class="card-desc">Converts plain text into diagrams, flowcharts, and visuals automatically.</p>
        <p class="card-note">Free gets you: unlimited basic visual generation.</p>
        <a class="card-link" href="https://napkin.ai" target="_blank" rel="noopener">Visit site →</a>
      </article>
    </div>
  </section>

  <p class="empty-state" id="emptyState">No cards match that search. Try a different word, or clear the search.</p>
</main>

<footer>
  <p>Free-tier limits, prices, and policies change often — confirm details on each tool's own site before relying on it for real work. Catalogued June 2026.</p>
  <p>This page lists third-party products for reference only and isn't affiliated with any of them.</p>
</footer>

<script>
  const categories = [
    {key:'all', label:'All'},
    {key:'chat', label:'Chat & Research'},
    {key:'writing', label:'Writing & Editing'},
    {key:'images', label:'Images & Design'},
    {key:'video', label:'Video & Animation'},
    {key:'audio', label:'Audio, Music & Voice'},
    {key:'code', label:'Code & Development'},
    {key:'productivity', label:'Productivity & Planning'}
  ];

  const tabsEl = document.getElementById('tabs');
  let activeCategory = 'all';

  categories.forEach((cat, i) => {
    const btn = document.createElement('button');
    btn.className = 'tab';
    btn.type = 'button';
    btn.textContent = cat.label;
    btn.setAttribute('aria-pressed', i === 0 ? 'true' : 'false');
    btn.addEventListener('click', () => {
      activeCategory = cat.key;
      document.querySelectorAll('.tab').forEach(t => t.setAttribute('aria-pressed','false'));
      btn.setAttribute('aria-pressed','true');
      applyFilters();
    });
    tabsEl.appendChild(btn);
  });

  const searchInput = document.getElementById('search');
  const allCards = Array.from(document.querySelectorAll('.card'));
  const sections = Array.from(document.querySelectorAll('.section-label-wrap'));
  const emptyState = document.getElementById('emptyState');

  function applyFilters(){
    const query = searchInput.value.trim().toLowerCase();
    let anyVisible = false;

    sections.forEach(section => {
      const sectionKey = section.dataset.section;
      let sectionHasVisible = false;

      section.querySelectorAll('.card').forEach(card => {
        const cardCategory = card.dataset.category;
        const text = card.textContent.toLowerCase();
        const matchesCategory = activeCategory === 'all' || activeCategory === cardCategory;
        const matchesQuery = query === '' || text.includes(query);
        const show = matchesCategory && matchesQuery;
        card.style.display = show ? '' : 'none';
        if(show){ sectionHasVisible = true; anyVisible = true; }
      });

      section.style.display = sectionHasVisible ? '' : 'none';
    });

    emptyState.style.display = anyVisible ? 'none' : 'block';
  }

  searchInput.addEventListener('input', applyFilters);
</script>

</body>
</html>
