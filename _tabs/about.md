---
icon: fas fa-info-circle
order: 4
---

<style>
/* ── Reset inside page ───────────────────────────────────── */
.about-wrap * { box-sizing: border-box; }

/* ── Hero ────────────────────────────────────────────────── */
.about-hero {
  text-align: center;
  padding: 3rem 1rem 2.5rem;
  position: relative;
}
.about-hero::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(ellipse 70% 60% at 50% 0%, rgba(255,46,77,0.12) 0%, transparent 70%);
  pointer-events: none;
}
.about-name {
  font-size: clamp(2.2rem, 5vw, 3.2rem);
  font-weight: 900;
  letter-spacing: -1px;
  margin: 0 0 0.4rem;
  background: linear-gradient(135deg, #ffffff 40%, #ff2e4d 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
.about-title {
  font-family: 'Courier New', monospace;
  font-size: 1rem;
  color: #ff2e4d;
  letter-spacing: 2px;
  text-transform: uppercase;
  margin: 0 0 1.8rem;
}
.about-title::after {
  content: '█';
  animation: blink 1s step-end infinite;
  margin-left: 2px;
}
@keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

/* ── Social buttons ──────────────────────────────────────── */
.about-socials {
  display: flex;
  gap: 0.7rem;
  justify-content: center;
  flex-wrap: wrap;
}
.about-btn {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  padding: 9px 20px;
  border-radius: 999px;
  text-decoration: none !important;
  font-size: 0.875rem;
  font-weight: 700;
  letter-spacing: 0.3px;
  transition: transform 0.2s, box-shadow 0.2s;
}
.about-btn:hover { transform: translateY(-2px); }
.about-btn-li { background: #0a66c2; color: #fff !important; box-shadow: 0 4px 20px rgba(10,102,194,0.35); }
.about-btn-li:hover { box-shadow: 0 6px 28px rgba(10,102,194,0.55); }
.about-btn-gh { background: #24292f; color: #fff !important; box-shadow: 0 4px 20px rgba(0,0,0,0.4); border: 1px solid rgba(255,255,255,0.1); }
.about-btn-gh:hover { box-shadow: 0 6px 28px rgba(0,0,0,0.6); }

/* ── Stat strip ──────────────────────────────────────────── */
.about-stats {
  display: flex;
  justify-content: center;
  gap: 1px;
  margin: 2.5rem 0;
  flex-wrap: wrap;
}
.about-stat {
  flex: 1 1 130px;
  max-width: 180px;
  text-align: center;
  padding: 1.2rem 1rem;
  background: rgba(255,46,77,0.05);
  border: 1px solid rgba(255,46,77,0.18);
  position: relative;
}
.about-stat:first-child { border-radius: 12px 0 0 12px; }
.about-stat:last-child  { border-radius: 0 12px 12px 0; }
.about-stat-num {
  font-size: 2rem;
  font-weight: 900;
  color: #ff2e4d;
  display: block;
  line-height: 1;
}
.about-stat-label {
  font-size: 0.78rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  opacity: 0.6;
  margin-top: 0.3rem;
  display: block;
}

/* ── Terminal block ──────────────────────────────────────── */
.about-terminal {
  background: #0d1117;
  border: 1px solid rgba(255,46,77,0.25);
  border-radius: 12px;
  overflow: hidden;
  margin: 2rem 0;
  box-shadow: 0 8px 40px rgba(0,0,0,0.5), 0 0 0 1px rgba(255,46,77,0.05);
}
.about-terminal-bar {
  background: rgba(255,255,255,0.04);
  border-bottom: 1px solid rgba(255,255,255,0.06);
  padding: 10px 16px;
  display: flex;
  align-items: center;
  gap: 6px;
}
.dot { width: 12px; height: 12px; border-radius: 50%; }
.dot-r { background: #ff5f57; }
.dot-y { background: #febc2e; }
.dot-g { background: #28c840; }
.about-terminal-title {
  font-family: monospace;
  font-size: 0.78rem;
  opacity: 0.4;
  margin-left: auto;
  margin-right: auto;
}
.about-terminal-body {
  padding: 1.4rem 1.6rem;
  font-family: 'Courier New', monospace;
  font-size: 0.88rem;
  line-height: 1.9;
}
.t-prompt { color: #ff2e4d; }
.t-cmd    { color: #e6edf3; }
.t-out    { color: rgba(230,237,243,0.65); }
.t-key    { color: #79c0ff; }
.t-val    { color: #a5d6ff; }
.t-hi     { color: #ff7b8e; font-weight: 700; }

/* ── Work cards ──────────────────────────────────────────── */
.about-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
  gap: 1rem;
  margin: 2rem 0;
}
.about-card {
  border: 1px solid rgba(255,46,77,0.15);
  border-radius: 14px;
  padding: 1.5rem;
  background: rgba(255,46,77,0.03);
  transition: border-color 0.25s, transform 0.25s, box-shadow 0.25s;
  cursor: default;
}
.about-card:hover {
  border-color: rgba(255,46,77,0.5);
  transform: translateY(-3px);
  box-shadow: 0 12px 36px rgba(255,46,77,0.1);
}
.about-card-icon { font-size: 2rem; margin-bottom: 0.7rem; display: block; }
.about-card-title { font-weight: 800; font-size: 1rem; margin: 0 0 0.4rem; }
.about-card-desc  { font-size: 0.85rem; opacity: 0.6; margin: 0; line-height: 1.6; }

/* ── Pipeline ────────────────────────────────────────────── */
.about-pipeline {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 0;
  margin: 2rem 0;
  background: rgba(255,46,77,0.04);
  border: 1px solid rgba(255,46,77,0.15);
  border-radius: 14px;
  padding: 1.4rem 1rem;
}
.pipe-step {
  text-align: center;
  padding: 0.3rem 0.8rem;
}
.pipe-step-label {
  font-family: 'Courier New', monospace;
  font-size: 0.78rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: #ff2e4d;
}
.pipe-step-sub {
  font-size: 0.68rem;
  opacity: 0.45;
  margin-top: 2px;
}
.pipe-arrow {
  color: rgba(255,46,77,0.4);
  font-size: 1.2rem;
  padding: 0 0.2rem;
  flex-shrink: 0;
}

/* ── Section headings ────────────────────────────────────── */
.about-section-title {
  font-family: 'Courier New', monospace;
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 3px;
  color: #ff2e4d;
  margin: 2.5rem 0 1rem;
  opacity: 0.85;
}

/* ── Divider ─────────────────────────────────────────────── */
.about-hr {
  border: none;
  border-top: 1px solid rgba(255,46,77,0.1);
  margin: 2rem 0;
}

/* ── Quote ───────────────────────────────────────────────── */
.about-quote {
  border-left: 3px solid #ff2e4d;
  padding: 0.6rem 1.2rem;
  margin: 1.5rem 0;
  background: rgba(255,46,77,0.05);
  border-radius: 0 8px 8px 0;
  font-style: italic;
  font-size: 1.05rem;
  color: rgba(230,237,243,0.85);
}
</style>

<div class="about-wrap">

<!-- ── HERO ─────────────────────────────────────────────── -->
<div class="about-hero">
  <h1 class="about-name">Avinash Kotla</h1>
  <p class="about-title">Digital Forensic Analyst&nbsp;&nbsp;·&nbsp;&nbsp;DFIR</p>
  <div class="about-socials">
    <a class="about-btn about-btn-li" href="https://www.linkedin.com/in/avinash-kotla" target="_blank">
      <svg width="15" height="15" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
      LinkedIn
    </a>
    <a class="about-btn about-btn-gh" href="https://github.com/KotlaAvinash" target="_blank">
      <svg width="15" height="15" viewBox="0 0 24 24" fill="currentColor"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>
      GitHub
    </a>
  </div>
</div>

<!-- ── STATS ─────────────────────────────────────────────── -->
<div class="about-stats">
  <div class="about-stat">
    <span class="about-stat-num">TCS</span>
    <span class="about-stat-label">Employer</span>
  </div>
  <div class="about-stat">
    <span class="about-stat-num">3+</span>
    <span class="about-stat-label">Platforms</span>
  </div>
  <div class="about-stat">
    <span class="about-stat-num">OSS</span>
    <span class="about-stat-label">Tools Built</span>
  </div>
  <div class="about-stat">
    <span class="about-stat-num">∞</span>
    <span class="about-stat-label">Artifacts Left</span>
  </div>
</div>

<hr class="about-hr">

<!-- ── TERMINAL ──────────────────────────────────────────── -->
<p class="about-section-title">// whoami</p>

<div class="about-terminal">
  <div class="about-terminal-bar">
    <span class="dot dot-r"></span>
    <span class="dot dot-y"></span>
    <span class="dot dot-g"></span>
    <span class="about-terminal-title">analyst@kotla ~ bash</span>
  </div>
  <div class="about-terminal-body">
    <div><span class="t-prompt">❯</span> <span class="t-cmd">cat whoami.txt</span></div>
    <br>
    <div><span class="t-key">name</span>        <span class="t-out">:</span> <span class="t-val">Avinash Kotla</span></div>
    <div><span class="t-key">role</span>        <span class="t-out">:</span> <span class="t-val">Digital Forensic Analyst</span></div>
    <div><span class="t-key">employer</span>    <span class="t-out">:</span> <span class="t-val">Tata Consultancy Services</span></div>
    <div><span class="t-key">scope</span>       <span class="t-out">:</span> <span class="t-val">Windows · Linux · Mobile</span></div>
    <div><span class="t-key">specialty</span>   <span class="t-out">:</span> <span class="t-val">Evidence correlation &amp; timeline reconstruction</span></div>
    <div><span class="t-key">principle</span>   <span class="t-out">:</span> <span class="t-hi">Deleted is not gone.</span></div>
    <br>
    <div><span class="t-prompt">❯</span> <span class="t-cmd">_</span></div>
  </div>
</div>

<div class="about-quote">
  When a tool doesn't exist for the artifact in front of me, I build one.
</div>

<hr class="about-hr">

<!-- ── CARDS ─────────────────────────────────────────────── -->
<p class="about-section-title">// what I do</p>

<div class="about-cards">
  <div class="about-card">
    <span class="about-card-icon">🔍</span>
    <p class="about-card-title">Investigations</p>
    <p class="about-card-desc">End-to-end DFIR across Windows, Linux and mobile. From acquisition and chain of custody through to a defensible final report.</p>
  </div>
  <div class="about-card">
    <span class="about-card-icon">🛠️</span>
    <p class="about-card-title">Tool Building</p>
    <p class="about-card-desc">Open-source forensic tools written when the right one doesn't exist. Built to handle real evidence without touching originals.</p>
  </div>
  <div class="about-card">
    <span class="about-card-icon">📝</span>
    <p class="about-card-title">Writing</p>
    <p class="about-card-desc">Plain-language breakdowns of what operating systems quietly record — and how to read it before it disappears.</p>
  </div>
</div>

<hr class="about-hr">

<!-- ── PIPELINE ──────────────────────────────────────────── -->
<p class="about-section-title">// the workflow</p>

<div class="about-pipeline">
  <div class="pipe-step">
    <div class="pipe-step-label">acquire</div>
    <div class="pipe-step-sub">bit-for-bit</div>
  </div>
  <span class="pipe-arrow">›</span>
  <div class="pipe-step">
    <div class="pipe-step-label">custody</div>
    <div class="pipe-step-sub">hash &amp; seal</div>
  </div>
  <span class="pipe-arrow">›</span>
  <div class="pipe-step">
    <div class="pipe-step-label">analyse</div>
    <div class="pipe-step-sub">artifacts</div>
  </div>
  <span class="pipe-arrow">›</span>
  <div class="pipe-step">
    <div class="pipe-step-label">correlate</div>
    <div class="pipe-step-sub">logs + devices</div>
  </div>
  <span class="pipe-arrow">›</span>
  <div class="pipe-step">
    <div class="pipe-step-label">timeline</div>
    <div class="pipe-step-sub">single truth</div>
  </div>
  <span class="pipe-arrow">›</span>
  <div class="pipe-step">
    <div class="pipe-step-label">report</div>
    <div class="pipe-step-sub">defensible</div>
  </div>
</div>

<hr class="about-hr">

<!-- ── CONNECT ───────────────────────────────────────────── -->
<p class="about-section-title">// connect</p>

<p style="opacity:0.7;font-size:0.95rem;">Open to DFIR conversations, research collaboration, and hard forensic problems. Find me at:</p>

<div class="about-socials" style="justify-content:flex-start;margin-top:1rem;">
  <a class="about-btn about-btn-li" href="https://www.linkedin.com/in/avinash-kotla" target="_blank">
    <svg width="15" height="15" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
    linkedin.com/in/avinash-kotla
  </a>
  <a class="about-btn about-btn-gh" href="https://github.com/KotlaAvinash" target="_blank">
    <svg width="15" height="15" viewBox="0 0 24 24" fill="currentColor"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>
    github.com/KotlaAvinash
  </a>
</div>

<br>

</div>
