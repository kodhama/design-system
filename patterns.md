# kodhama design system — patterns

Component patterns extracted from trellis's landing page (`docs/index.html`),
the design system's source of truth. Each entry is a short description
followed by a faithful CSS/HTML extract — copied as-is, not redesigned.
All patterns assume `tokens.css` is loaded first; they reference its custom
properties (`--bg`, `--accent`, `--line`, etc.) rather than hard-coded values.

Where the extract behaves interactively (theme toggle, terminal tabs/copy),
the vanilla-JS behavior from the source is included too, since the pattern
isn't complete without it.

---

## Eyebrow

Small caps, mono, wide-tracked label that introduces a section or hero.

```css
.eyebrow {
  font-family: var(--mono);
  font-size: 12.5px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--accent-ink);
}
```

```html
<p class="eyebrow">Governance for agentic development</p>
```

---

## Card

Surface block used inside grids (`.cols-3`, `.cols-2`) — numbered feature
cards, comparison callouts, etc.

```css
.grid { display: grid; gap: 20px; margin-top: 42px; }
.cols-3 { grid-template-columns: repeat(3, 1fr); }
.cols-2 { grid-template-columns: repeat(2, 1fr); }
@media (max-width: 820px) { .cols-3, .cols-2 { grid-template-columns: 1fr; } }

.card { background: var(--surface); border: 1px solid var(--line); border-radius: 14px; padding: 24px; }
.card h3 { font-size: 1.15rem; }
.card p { color: var(--muted); margin: 10px 0 0; font-size: 0.98rem; }
.card .num { font-family: var(--mono); font-size: 12px; color: var(--accent-ink); letter-spacing: 0.1em; }
```

```html
<div class="grid cols-3">
  <div class="card">
    <p class="num">01</p>
    <h3>Referential integrity</h3>
    <p>Every artifact — research, decisions, specs, code — points to the settled ground it depends on. Agents build on ratified truth, never a draft that's still moving.</p>
  </div>
  <!-- ...repeat for each card... -->
</div>
```

---

## Terminal (tabs / copy / prompt)

Fake terminal window: three dots, a row of install-method tabs, a copy
button, and command lines with a styled prompt glyph and dimmed inline
comments. Tabs and the copy button are behavior, not just markup — included
below.

```css
.terminal {
  margin-top: 34px; max-width: 760px; background: var(--code-bg); color: var(--code-text);
  border-radius: 12px; border: 1px solid #ffffff10; overflow: hidden;
  box-shadow: 0 18px 40px -24px #00000070;
}
.terminal .tt { display: flex; align-items: center; gap: 8px; padding: 8px 14px 8px; border-bottom: 1px solid #ffffff12; }
.terminal .dot { width: 11px; height: 11px; border-radius: 50%; background: #ffffff20; }
.tabs { display: flex; gap: 4px; margin-left: 10px; }
.tab {
  font-family: var(--mono); font-size: 12px; cursor: pointer;
  background: transparent; color: #ffffff66; border: 0; border-radius: 6px; padding: 5px 10px;
}
.tab:hover { color: #cfe9db; }
.tab.active { background: #ffffff14; color: #d7e6dd; }
.terminal .panel { display: none; padding: 9px 0; }
.terminal .panel.active { display: block; }
.terminal .cmd {
  padding: 7px 16px; overflow-x: auto; font-family: var(--mono); font-size: 13.5px;
  scrollbar-width: thin; scrollbar-color: #ffffff22 transparent;
}
.terminal .cmd::-webkit-scrollbar { height: 6px; }
.terminal .cmd::-webkit-scrollbar-thumb { background: #ffffff22; border-radius: 3px; }
.terminal .cmd code { white-space: pre; }
.terminal .cmd .prompt { color: var(--code-accent); user-select: none; }
.copy {
  margin-left: auto; flex: none; font-family: var(--mono); font-size: 12px; cursor: pointer;
  background: #ffffff12; color: #cfe9db; border: 0; border-radius: 7px; padding: 6px 11px;
}
.copy:hover { background: #ffffff22; }
.terminal .cmt { color: #ffffff40; }
.tnote { margin-top: 14px; color: var(--muted); font-size: 0.92rem; max-width: 640px; }
.tnote code { font-family: var(--mono); font-size: 0.85em; background: color-mix(in srgb, var(--accent) 13%, transparent); padding: 1px 6px; border-radius: 5px; color: var(--accent-ink); }
```

```html
<div class="terminal" role="group" aria-label="Install, then set up Trellis">
  <div class="tt">
    <i class="dot"></i><i class="dot"></i><i class="dot"></i>
    <div class="tabs" role="tablist" aria-label="Install method">
      <button class="tab active" role="tab" aria-selected="true" data-tab="curl">curl</button>
      <button class="tab" role="tab" aria-selected="false" data-tab="brew">Homebrew</button>
      <button class="tab" role="tab" aria-selected="false" data-tab="cc">Claude Code</button>
    </div>
    <button class="copy" id="copyBtn" aria-label="Copy commands">copy</button>
  </div>
  <div class="panel active" data-panel="curl">
    <div class="cmd"><code><span class="prompt">$ </span>curl -fsSL https://raw.githubusercontent.com/kodhama/trellis/main/install.sh | sh</code></div>
    <div class="cmd"><code><span class="prompt">$ </span>trellis setup<span class="cmt">    # then set it up in your project</span></code></div>
  </div>
  <div class="panel" data-panel="brew">
    <div class="cmd"><code><span class="prompt">$ </span>brew install kodhama/trellis/trellis</code></div>
    <div class="cmd"><code><span class="prompt">$ </span>trellis setup<span class="cmt">    # then set it up in your project</span></code></div>
  </div>
  <div class="panel" data-panel="cc">
    <div class="cmd"><code><span class="prompt">&gt; </span>/plugin marketplace add kodhama/trellis</code></div>
    <div class="cmd"><code><span class="prompt">&gt; </span>/plugin install trellis@trellis</code></div>
    <div class="cmd"><code><span class="prompt">&gt; </span>/trellis:setup<span class="cmt">    # the plugin covers the overlay natively</span></code></div>
  </div>
</div>
<p class="tnote">The installer just drops a single binary — it doesn't run anything on its own; you run <code>trellis setup</code>.</p>
```

```js
// tab switching + copy-to-clipboard behavior
var commands = {
  curl: "curl -fsSL https://raw.githubusercontent.com/kodhama/trellis/main/install.sh | sh\ntrellis setup",
  brew: "brew install kodhama/trellis/trellis\ntrellis setup",
  cc: "/plugin marketplace add kodhama/trellis\n/plugin install trellis@trellis\n/trellis:setup"
};
var activeTab = "curl";
var tabs = document.querySelectorAll(".tab");
var panels = document.querySelectorAll(".terminal .panel");
tabs.forEach(function (t) {
  t.addEventListener("click", function () {
    activeTab = t.getAttribute("data-tab");
    tabs.forEach(function (x) {
      var on = x === t;
      x.classList.toggle("active", on);
      x.setAttribute("aria-selected", on ? "true" : "false");
    });
    panels.forEach(function (p) {
      p.classList.toggle("active", p.getAttribute("data-panel") === activeTab);
    });
  });
});
var btn = document.getElementById("copyBtn");
btn.addEventListener("click", function () {
  navigator.clipboard.writeText(commands[activeTab]).then(function () {
    btn.textContent = "copied ✓";
    setTimeout(function () { btn.textContent = "copy"; }, 1600);
  });
});
```

---

## Lattice motif

Faint grid backdrop behind the hero, radially masked so it fades toward the
edges instead of hard-cropping. This is the visual echo of the trellis mark
itself — a background pattern, not the icon.

```css
.hero { position: relative; overflow: hidden; border-bottom: 1px solid var(--line); }
.hero .lattice {
  position: absolute; inset: 0; pointer-events: none; opacity: 0.5;
  background-image:
    linear-gradient(to right, var(--line) 1px, transparent 1px),
    linear-gradient(to bottom, var(--line) 1px, transparent 1px);
  background-size: 42px 42px;
  -webkit-mask-image: radial-gradient(120% 80% at 70% 0%, #000 30%, transparent 72%);
          mask-image: radial-gradient(120% 80% at 70% 0%, #000 30%, transparent 72%);
}
```

```html
<div class="hero">
  <div class="lattice" aria-hidden="true"></div>
  <div class="wrap"><!-- hero content --></div>
</div>
```

---

## Theme toggle

Pill-shaped button that flips between light/dark by stamping
`data-theme` on `<html>`, persisted to `localStorage`. Falls back to
`prefers-color-scheme` until the user picks explicitly. Pair with the
`[data-theme="light"]` / `[data-theme="dark"]` blocks in `tokens.css`.

```css
.toggle {
  font-family: var(--mono); font-size: 12px; cursor: pointer;
  background: transparent; color: var(--muted); border: 1px solid var(--line);
  border-radius: 999px; padding: 5px 11px;
}
.toggle:hover { color: var(--text); border-color: var(--accent); }
```

```html
<button class="toggle" id="themeToggle" aria-label="Toggle color theme">theme</button>
```

```js
(function () {
  var root = document.documentElement;
  var toggle = document.getElementById("themeToggle");
  var saved = null;
  try { saved = localStorage.getItem("trellis-theme"); } catch (e) {}
  if (saved) root.setAttribute("data-theme", saved);
  function themeNow() {
    return root.getAttribute("data-theme") ||
      (window.matchMedia("(prefers-color-scheme: dark)").matches ? "dark" : "light");
  }
  function syncToggle() { toggle.textContent = themeNow(); }
  syncToggle();
  toggle.addEventListener("click", function () {
    var next = themeNow() === "dark" ? "light" : "dark";
    root.setAttribute("data-theme", next);
    try { localStorage.setItem("trellis-theme", next); } catch (e) {}
    syncToggle();
  });
})();
```

Note: the storage key (`trellis-theme`) is product-specific in the source.
Consumers should namespace this per product (e.g. `grove-theme`) rather
than copying the literal key.

---

## Climbing-plant animation

Decorative SVG vine that draws itself up the right edge of the hero on
load: a stem path animates via `stroke-dashoffset`, tendrils uncurl on a
stagger, and leaves unfurl with a spring-ish easing. Respects
`prefers-reduced-motion`.

```css
.plant { position: absolute; right: clamp(6px, 5vw, 90px); bottom: -1px; height: min(86%, 540px); width: auto; pointer-events: none; z-index: 1; }
@media (max-width: 960px) { .plant { opacity: 0.18; right: -24px; } }
@media (max-width: 620px) { .plant { display: none; } }
.plant .stem, .plant .tendril, .plant .tip { stroke-dasharray: 1; stroke-dashoffset: 1; }
.plant .stem { animation: draw 2.9s ease forwards 0.15s; }
.plant .tendril { animation: draw 1.1s cubic-bezier(0.3,0,0.4,1) forwards var(--d); }
.plant .tip { animation: draw 1s cubic-bezier(0.3,0,0.4,1) forwards 2.85s; }
.plant .leaf { opacity: 0; transform: scale(0); transform-box: fill-box; transform-origin: left center; animation: unfurl 0.6s cubic-bezier(0.2,0.8,0.3,1.25) forwards var(--d); }
.plant .deep { color: color-mix(in srgb, var(--accent) 68%, var(--accent-ink) 32%); }
@keyframes draw { to { stroke-dashoffset: 0; } }
@keyframes unfurl { to { opacity: 1; transform: scale(1); } }
@media (prefers-reduced-motion: reduce) {
  .plant .stem, .plant .tendril, .plant .tip { animation: none; stroke-dashoffset: 0; }
  .plant .leaf { animation: none; opacity: 1; transform: scale(1); }
}
```

```html
<svg class="plant" viewBox="0 0 200 560" fill="none" aria-hidden="true" preserveAspectRatio="xMidYMax meet" style="color:var(--accent)">
  <defs>
    <g id="tl-leaf">
      <path d="M0 0 C 14 -16 40 -20 58 -7 C 44 5 18 9 0 0 Z" fill="currentColor"/>
      <path d="M6 -1 C 22 -7 40 -9 52 -8" stroke="#06110b" stroke-opacity=".22" stroke-width="1.4" fill="none"/>
    </g>
  </defs>
  <path class="stem" pathLength="1"
    d="M100 558 C 86 500 116 470 98 410 C 82 356 112 320 96 258 C 84 208 110 172 98 112 C 92 78 100 56 96 24"
    stroke="var(--accent)" stroke-width="3.2" stroke-linecap="round"/>
  <path class="tendril" pathLength="1" style="--d:1.55s" transform="translate(100,336) rotate(-12)"
    d="M0 0 C 10 -4 22 -12 30 -11 C 41 -10 42 2 34 5 C 27 7 22 0 28 -4"
    stroke="var(--accent)" stroke-width="2" stroke-linecap="round"/>
  <path class="tendril" pathLength="1" style="--d:2.35s" transform="translate(97,150) scale(-1,1) rotate(-10)"
    d="M0 0 C 10 -4 22 -12 30 -11 C 41 -10 42 2 34 5 C 27 7 22 0 28 -4"
    stroke="var(--accent)" stroke-width="2" stroke-linecap="round"/>
  <g transform="translate(103,486) rotate(-30) scale(1.08)"><use href="#tl-leaf" class="leaf" style="--d:.7s"/></g>
  <g transform="translate(92,430) scale(-1,1) rotate(-26)"><use href="#tl-leaf" class="leaf deep" style="--d:1s"/></g>
  <g transform="translate(101,372) rotate(-24) scale(1.02)"><use href="#tl-leaf" class="leaf" style="--d:1.3s"/></g>
  <g transform="translate(90,310) scale(-0.94,0.94) rotate(-26)"><use href="#tl-leaf" class="leaf deep" style="--d:1.6s"/></g>
  <g transform="translate(101,248) rotate(-26) scale(0.92)"><use href="#tl-leaf" class="leaf" style="--d:1.9s"/></g>
  <g transform="translate(92,192) scale(-0.84,0.84) rotate(-30)"><use href="#tl-leaf" class="leaf deep" style="--d:2.2s"/></g>
  <g transform="translate(99,140) rotate(-32) scale(0.78)"><use href="#tl-leaf" class="leaf" style="--d:2.45s"/></g>
  <path class="tip" pathLength="1"
    d="M96 24 C 92 8 106 0 113 7 C 119 13 113 22 106.5 19.5 C 102 17.5 103 11 108 11"
    stroke="var(--accent)" stroke-width="2.6" stroke-linecap="round"/>
</svg>
```

---

## Compare-pairs

Stacked "without / with" callouts — a labelled case header, a red-tinted
"without" row, a green-tinted "with" row.

```css
.compare-pairs { display: grid; gap: 12px; margin-top: 42px; max-width: 760px; }
.compare-pairs .stack { border: 1px solid var(--line); border-radius: 12px; overflow: hidden; }
.compare-pairs .case { font-family: var(--mono); font-size: 11px; letter-spacing: .07em; text-transform: uppercase; color: var(--muted); background: color-mix(in srgb, var(--accent) 6%, var(--surface)); padding: 8px 14px; }
.compare-pairs .s { padding: 13px 14px; font-size: .95rem; display: flex; gap: 12px; }
.compare-pairs .s.wo { background: color-mix(in srgb, #b4432f 8%, var(--surface)); }
.compare-pairs .s.wi { background: color-mix(in srgb, var(--accent) 9%, var(--surface)); border-top: 1px solid var(--line); }
.compare-pairs .lbl { flex: none; width: 62px; font-family: var(--mono); font-size: 10.5px; text-transform: uppercase; letter-spacing: .08em; font-weight: 600; }
.compare-pairs .s.wo .lbl { color: #b4432f; }
.compare-pairs .s.wi .lbl { color: var(--accent-ink); }
```

```html
<div class="compare-pairs">
  <div class="stack">
    <div class="case">directional flow</div>
    <div class="s wo"><span class="lbl">Without</span><span>an agent codes against a spec that's still being edited; it shifts, and the work is built on a version that no longer exists.</span></div>
    <div class="s wi"><span class="lbl">With</span><span>implementation reads only ratified specs; downstream never consumes a draft.</span></div>
  </div>
  <!-- ...repeat per case... -->
</div>
```

Note: `#b4432f` (the "without" red) is a one-off literal in the source, not
a token — it isn't in `tokens.css`. Consumers who want it themeable should
promote it to a custom property (e.g. `--danger`) rather than hard-coding it
again.

---

## Buttons / pills

Primary and ghost buttons for CTAs; the pill radius (`999px`) shows up
again on `.toggle` (see Theme toggle above) and is the family's "chip"
shape.

```css
.btn {
  display: inline-flex; align-items: center; gap: 8px; font-weight: 600; font-size: 15px;
  padding: 11px 20px; border-radius: 10px; text-decoration: none; border: 1px solid transparent;
}
.btn-primary { background: var(--accent); color: #06110b; }
.btn-primary:hover { filter: brightness(1.06); }
.btn-ghost { border-color: var(--line); color: var(--text); }
.btn-ghost:hover { border-color: var(--accent); }

.cta { display: flex; flex-wrap: wrap; gap: 12px; margin-top: 30px; }

@media (prefers-reduced-motion: no-preference) {
  .btn, .toggle, .copy, .tab { transition: all 0.15s ease; }
}
```

```html
<div class="cta">
  <a class="btn btn-primary" href="invariants.html">Explore the invariants →</a>
  <a class="btn btn-ghost" href="https://github.com/kodhama/trellis">View on GitHub →</a>
</div>
```

---

## Shared base (referenced by the above)

A few global rules the patterns above assume are in scope; not a
"component" on its own, included for completeness.

```css
* { box-sizing: border-box; }
html { -webkit-text-size-adjust: 100%; }
body {
  margin: 0; background: var(--bg); color: var(--text);
  font-family: var(--sans); line-height: 1.6;
  font-size: 17px; -webkit-font-smoothing: antialiased;
}
.wrap { max-width: var(--maxw); margin: 0 auto; padding: 0 24px; }
a { color: var(--accent-ink); text-decoration-color: color-mix(in srgb, var(--accent) 45%, transparent); text-underline-offset: 3px; }
h1, h2, h3 { line-height: 1.12; letter-spacing: -0.02em; text-wrap: balance; margin: 0; }
.muted { color: var(--muted); }
:focus-visible { outline: 2px solid var(--accent); outline-offset: 2px; border-radius: 4px; }
```
