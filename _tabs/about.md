---
icon: fas fa-info-circle
order: 4
---

<style>
:root {
  --red: #ff2e4d;
  --red-dim: rgba(255,46,77,0.12);
  --red-line: rgba(255,46,77,0.22);
  --fg: #e6edf3;
  --fg-muted: rgba(230,237,243,0.55);
  --surface: rgba(255,255,255,0.035);
  --surface-hover: rgba(255,255,255,0.06);
  --border: rgba(255,255,255,0.07);
}

/* ─── BASE ──────────────────────────────────────────────────── */
.pf * { box-sizing: border-box; margin: 0; padding: 0; }
.pf a { text-decoration: none !important; }

/* ─── HERO ──────────────────────────────────────────────────── */
.pf-hero {
  position: relative;
  padding: 4rem 0 3rem;
  overflow: hidden;
}
.pf-hero-glow {
  position: absolute;
  width: 600px; height: 600px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(255,46,77,0.15) 0%, transparent 70%);
  top: -200px; left: 50%;
  transform: translateX(-50%);
  pointer-events: none;
  animation: pf-pulse 4s ease-in-out infinite;
}
@keyframes pf-pulse { 0%,100%{opacity:.7;transform:translateX(-50%) scale(1)} 50%{opacity:1;transform:translateX(-50%) scale(1.08)} }

.pf-eyebrow {
  font-family: 'Courier New', monospace;
  font-size: 0.72rem;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: var(--red);
  margin-bottom: 1.2rem;
  display: flex;
  align-items: center;
  gap: 10px;
}
.pf-eyebrow::before {
  content: '';
  display: inline-block;
  width: 32px;
  height: 1px;
  background: var(--red);
  opacity: 0.7;
}

.pf-name {
  font-size: clamp(2.6rem, 7vw, 4.5rem) !important;
  font-weight: 900 !important;
  line-height: 1.05 !important;
  letter-spacing: -2px !important;
  color: var(--fg) !important;
  margin-bottom: 0.5rem !important;
}
.pf-name span { color: var(--red); }

.pf-tagline {
  font-size: clamp(1rem, 2.5vw, 1.25rem);
  color: var(--fg-muted);
  font-weight: 400;
  line-height: 1.6;
  max-width: 540px;
  margin-bottom: 2.2rem;
}
.pf-tagline strong { color: var(--fg); font-weight: 600; }

/* ─── PILL BUTTONS ──────────────────────────────────────────── */
.pf-btns {
  display: flex;
  gap: 0.75rem;
  flex-wrap: wrap;
  margin-bottom: 3rem;
}
.pf-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 11px 22px;
  border-radius: 999px;
  font-size: 0.875rem;
  font-weight: 700;
  letter-spacing: 0.2px;
  color: #fff !important;
  transition: transform 0.2s ease, box-shadow 0.2s ease, filter 0.2s ease;
}
.pf-btn:hover { transform: translateY(-2px); filter: brightness(1.15); }
.pf-btn-li { background: #0a66c2; box-shadow: 0 4px 20px rgba(10,102,194,0.4); }
.pf-btn-gh { background: #161b22; box-shadow: 0 4px 20px rgba(0,0,0,0.5); border: 1px solid rgba(255,255,255,0.12); }

/* ─── BADGE ROW ─────────────────────────────────────────────── */
.pf-badges {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}
.pf-badge {
  padding: 5px 14px;
  border-radius: 6px;
  font-size: 0.78rem;
  font-weight: 600;
  letter-spacing: 0.5px;
  background: var(--surface);
  border: 1px solid var(--border);
  color: var(--fg-muted);
}

/* ─── DIVIDER ───────────────────────────────────────────────── */
.pf-divider {
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--red-line) 30%, var(--red-line) 70%, transparent);
  margin: 2.5rem 0;
}

/* ─── TWO-COL LAYOUT ────────────────────────────────────────── */
.pf-twocol {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  align-items: start;
}
@media (max-width: 640px) { .pf-twocol { grid-template-columns: 1fr; } }

/* ─── SECTION LABEL ─────────────────────────────────────────── */
.pf-label {
  font-family: 'Courier New', monospace;
  font-size: 0.68rem;
  text-transform: uppercase;
  letter-spacing: 3.5px;
  color: var(--red);
  margin-bottom: 1.1rem;
  display: flex;
  align-items: center;
  gap: 8px;
}
.pf-label::after {
  content: '';
  flex: 1;
  height: 1px;
  background: var(--red-line);
}

.pf-body {
  font-size: 0.96rem;
  line-height: 1.8;
  color: var(--fg-muted);
}
.pf-body strong { color: var(--fg); }
.pf-body p + p { margin-top: 0.9rem; }

/* ─── FACT LIST ─────────────────────────────────────────────── */
.pf-facts { list-style: none; }
.pf-facts li {
  display: flex;
  align-items: baseline;
  gap: 12px;
  padding: 0.65rem 0;
  border-bottom: 1px solid var(--border);
  font-size: 0.9rem;
  color: var(--fg-muted);
}
.pf-facts li:last-child { border-bottom: none; }
.pf-fact-key {
  font-family: 'Courier New', monospace;
  font-size: 0.75rem;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: var(--red);
  min-width: 90px;
  flex-shrink: 0;
}
.pf-fact-val { color: var(--fg); }

/* ─── HIGHLIGHT QUOTE ───────────────────────────────────────── */
.pf-quote {
  position: relative;
  padding: 1.4rem 1.6rem 1.4rem 2rem;
  margin: 2rem 0;
  background: var(--red-dim);
  border-radius: 12px;
  border: 1px solid var(--red-line);
}
.pf-quote::before {
  content: '';
  position: absolute;
  left: 0; top: 0; bottom: 0;
  width: 3px;
  background: var(--red);
  border-radius: 3px 0 0 3px;
}
.pf-quote-text {
  font-size: 1.1rem;
  font-style: italic;
  color: var(--fg);
  line-height: 1.65;
  font-weight: 500;
}
.pf-quote-attr {
  font-family: 'Courier New', monospace;
  font-size: 0.72rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--red);
  margin-top: 0.6rem;
}

/* ─── SPECIALTY CARDS ───────────────────────────────────────── */
.pf-cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 0.75rem;
  margin: 1.5rem 0;
}
@media (max-width: 640px) { .pf-cards { grid-template-columns: 1fr; } }

.pf-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 12px;
  padding: 1.3rem;
  transition: background 0.2s, border-color 0.25s, transform 0.25s;
  cursor: default;
}
.pf-card:hover {
  background: var(--surface-hover);
  border-color: var(--red-line);
  transform: translateY(-3px);
}
.pf-card-icon { font-size: 1.5rem; margin-bottom: 0.7rem; display: block; }
.pf-card-title { font-size: 0.92rem; font-weight: 700; color: var(--fg); margin-bottom: 0.35rem; }
.pf-card-text  { font-size: 0.8rem; color: var(--fg-muted); line-height: 1.55; }

/* ─── TIMELINE / WORKFLOW ───────────────────────────────────── */
.pf-timeline { position: relative; padding-left: 1.5rem; margin: 1.2rem 0; }
.pf-timeline::before {
  content: '';
  position: absolute;
  left: 0; top: 6px; bottom: 6px;
  width: 1px;
  background: linear-gradient(180deg, var(--red) 0%, rgba(255,46,77,0.1) 100%);
}
.pf-tl-step { position: relative; margin-bottom: 1.1rem; }
.pf-tl-step:last-child { margin-bottom: 0; }
.pf-tl-step::before {
  content: '';
  position: absolute;
  left: -1.65rem;
  top: 6px;
  width: 7px; height: 7px;
  border-radius: 50%;
  background: var(--red);
  box-shadow: 0 0 8px var(--red);
}
.pf-tl-name { font-size: 0.82rem; font-weight: 700; color: var(--fg); text-transform: uppercase; letter-spacing: 1px; font-family: 'Courier New', monospace; }
.pf-tl-desc { font-size: 0.8rem; color: var(--fg-muted); margin-top: 2px; }

/* ─── CONNECT STRIP ─────────────────────────────────────────── */
.pf-connect {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 1.2rem;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 1.5rem 1.8rem;
  margin-top: 1rem;
}
.pf-connect-text p:first-child { font-size: 1rem; font-weight: 700; color: var(--fg); }
.pf-connect-text p:last-child  { font-size: 0.85rem; color: var(--fg-muted); margin-top: 3px; }
</style>

<div class="pf">

<!-- ═══ HERO ════════════════════════════════════════════════ -->
<div class="pf-hero">
  <div class="pf-hero-glow"></div>
  <p class="pf-eyebrow">Digital Forensics &amp; Incident Response</p>
  <h1 class="pf-name">Avinash<br><span>Kotla.</span></h1>
  <p class="pf-tagline">
    I investigate what machines <strong>quietly record</strong> about everyone who uses them —
    and I build the tools to read it when nothing else can.
  </p>
  <div class="pf-btns">
    <a class="pf-btn pf-btn-li" href="https://www.linkedin.com/in/avinash-kotla" target="_blank">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
      LinkedIn
    </a>
    <a class="pf-btn pf-btn-gh" href="https://github.com/KotlaAvinash" target="_blank">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>
      GitHub
    </a>
  </div>
  <div class="pf-badges">
    <span class="pf-badge">Windows Forensics</span>
    <span class="pf-badge">Linux Forensics</span>
    <span class="pf-badge">Mobile DFIR</span>
    <span class="pf-badge">SQLite Analysis</span>
    <span class="pf-badge">Tool Builder</span>
    <span class="pf-badge">TCS</span>
  </div>
</div>

<div class="pf-divider"></div>

<!-- ═══ ABOUT + FACTS ════════════════════════════════════════ -->
<div class="pf-twocol">
  <div>
    <p class="pf-label">About</p>
    <div class="pf-body">
      <p>I'm a <strong>Digital Forensic Analyst at Tata Consultancy Services</strong>, running end-to-end DFIR investigations across Windows, Linux, and mobile.</p>
      <p>The work is always the same: take in the raw evidence, hold the chain of custody, pull every relevant artifact, and correlate it all into a single timeline that can be <strong>defended in front of anyone</strong>.</p>
      <p>When the right tool for an artifact doesn't exist, I write it. Every tool I build starts with one rule — <strong>never modify the original.</strong></p>
    </div>
  </div>
  <div>
    <p class="pf-label">Quick Facts</p>
    <ul class="pf-facts">
      <li><span class="pf-fact-key">role</span><span class="pf-fact-val">Digital Forensic Analyst</span></li>
      <li><span class="pf-fact-key">employer</span><span class="pf-fact-val">Tata Consultancy Services</span></li>
      <li><span class="pf-fact-key">scope</span><span class="pf-fact-val">Windows · Linux · Mobile</span></li>
      <li><span class="pf-fact-key">specialty</span><span class="pf-fact-val">Evidence correlation &amp; timelines</span></li>
      <li><span class="pf-fact-key">principle</span><span class="pf-fact-val">Deleted is not gone.</span></li>
      <li><span class="pf-fact-key">open to</span><span class="pf-fact-val">DFIR conversations &amp; research</span></li>
    </ul>
  </div>
</div>

<div class="pf-divider"></div>

<!-- ═══ QUOTE ════════════════════════════════════════════════ -->
<div class="pf-quote">
  <p class="pf-quote-text">"When a tool doesn't exist for the artifact in front of me, I build one."</p>
  <p class="pf-quote-attr">— Avinash Kotla</p>
</div>

<div class="pf-divider"></div>

<!-- ═══ SPECIALTIES ══════════════════════════════════════════ -->
<p class="pf-label">What I Do</p>
<div class="pf-cards">
  <div class="pf-card">
    <span class="pf-card-icon">🔍</span>
    <p class="pf-card-title">Investigations</p>
    <p class="pf-card-text">End-to-end DFIR — acquisition, chain of custody, analysis, and defensible final reports.</p>
  </div>
  <div class="pf-card">
    <span class="pf-card-icon">🛠️</span>
    <p class="pf-card-title">Tool Building</p>
    <p class="pf-card-text">Open-source forensic tools built to fill gaps — read-only, hash-verified, evidence-safe.</p>
  </div>
  <div class="pf-card">
    <span class="pf-card-icon">📝</span>
    <p class="pf-card-title">Writing</p>
    <p class="pf-card-text">Clear breakdowns of what operating systems silently record — and how to recover it.</p>
  </div>
</div>

<div class="pf-divider"></div>

<!-- ═══ WORKFLOW ═════════════════════════════════════════════ -->
<div class="pf-twocol">
  <div>
    <p class="pf-label">The Workflow</p>
    <div class="pf-timeline">
      <div class="pf-tl-step">
        <p class="pf-tl-name">Acquire</p>
        <p class="pf-tl-desc">Bit-for-bit images. Nothing touched until it's hashed.</p>
      </div>
      <div class="pf-tl-step">
        <p class="pf-tl-name">Chain of Custody</p>
        <p class="pf-tl-desc">Hash before, hash after. Every copy logged.</p>
      </div>
      <div class="pf-tl-step">
        <p class="pf-tl-name">Analyse</p>
        <p class="pf-tl-desc">Artifacts across all layers — live data, deleted rows, slack space.</p>
      </div>
      <div class="pf-tl-step">
        <p class="pf-tl-name">Correlate</p>
        <p class="pf-tl-desc">Logs, device artifacts, and evidence brought into one view.</p>
      </div>
      <div class="pf-tl-step">
        <p class="pf-tl-name">Report</p>
        <p class="pf-tl-desc">A single defensible timeline. No guesses, no gaps unmarked.</p>
      </div>
    </div>
  </div>
  <div>
    <p class="pf-label">This Blog</p>
    <div class="pf-body">
      <p>Case studies, tool write-ups, and honest notes from real investigations.</p>
      <p>Each post covers one thing in depth — an artifact, a technique, a mistake worth not repeating. If you work in DFIR or just want to understand what your own machine is quietly keeping track of, you're in the right place.</p>
      <p>Nothing here is theoretical. Every post starts with a real file, a real database, or a real question that needed an answer.</p>
    </div>
  </div>
</div>

<div class="pf-divider"></div>

<!-- ═══ CONNECT ══════════════════════════════════════════════ -->
<div class="pf-connect">
  <div class="pf-connect-text">
    <p>Let's talk DFIR.</p>
    <p>Open to conversations, hard problems, and research collaboration.</p>
  </div>
  <div class="pf-btns" style="margin:0;">
    <a class="pf-btn pf-btn-li" href="https://www.linkedin.com/in/avinash-kotla" target="_blank">
      <svg width="15" height="15" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
      LinkedIn
    </a>
    <a class="pf-btn pf-btn-gh" href="https://github.com/KotlaAvinash" target="_blank">
      <svg width="15" height="15" viewBox="0 0 24 24" fill="currentColor"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>
      GitHub
    </a>
  </div>
</div>

<br>
</div>
