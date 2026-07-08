# kodhama icon family — grammar

**Finalized.** This supersedes the provisional grammar the previous
`icons/grammar.md` flagged as pending: it is the output of the
design-review pass (run with Claude design, plan-suite-lift T2) that the
old file, `identity/README.md`, and the repo `README.md` all named as the
open item. The icons are no longer placeholders.

## The family logic

**kodhama** is the guardian tree-spirit (a *kodama*) that watches the whole
forest. There are four marks: the org mark plus the three products — and
each product carries **one fragment of the kodhama mark**, so the family
reads as one thing split three ways:

| Mark | Fragment | Reading |
|---|---|---|
| **kodhama** | the whole — ring + sparks + laths | the guardian spirit / the forest |
| **trellis** | the **laths** | governance: the frame growth is trained along |
| **grove** | the **ring** | the assembly: tending agents gathered as a crown |
| **wisp** | the **sparks** | observability: little watchers, mini-kodhamas |

A wisp is a spark drifted free of the great spirit's ring — same soul,
smaller scale.

## Family rule — spirits are solid, structure is faint

This **retires** the old per-mark rule ("solid accent = living layer, 0.55
opacity = structure") *and* the trellis exception. The new rule:

- **kodhama** and **wisp** carry the living spark — they have solid fills.
- **grove** and **trellis** are structure the spirits inhabit — no solid
  fill; their depth comes from a **second tone** (`--accent-soft`), not
  from opacity.

## Shared pen

- **24×24 viewBox**, **1.7 stroke**, **round caps and round joins**,
  `currentColor` — no hard-coded hex inside a mark.
- UI icons keep a **2px safe area** (artwork within 2–22).
- Every mark and icon must survive **16px** (favicon). If a detail dies
  there, drop it.

## Two-tone — `--accent-soft`

```css
--accent-soft: color-mix(in srgb, var(--accent) 58%, var(--surface));
```

A lighter shade of the (possibly seasonal) accent, mixed toward the
surface so it tracks **both theme and season** and never muddies to grey
the way an opacity-dimmed accent does. The structure marks (trellis, grove)
use it for their secondary strand; **functional UI icons stay monoline
`currentColor`** — the two-tone is reserved for the brand-inflected few.

## The marks — exact geometry

- **kodhama — spark echo** (`kodhama.svg`): laths `M2 9h20 M2 15h20` at .55
  + ring r6.8 + solid spark (19.3, 4.7) r1.3 + faint spark (21.9, 2.1) r.85
  @ .45. For standalone contexts (avatar, favicon, app icon, social).
- **kodhama — quiet echo** (`kodhama-quiet.svg`): laths .55 + plain ring
  r7.5. For lockups — the wordmark carries the sparks, so the mark goes
  quiet. **One echo per surface.**
- **trellis** (`trellis.svg`): **woven** — three posts and two laths in a
  true over-under, square butt corners at the tucks, round caps on the open
  ends. Posts take the accent; laths take `--accent-soft`.
- **grove** (`grove.svg`): a mature crown (`circle 13.4,9.4 r5.6`, accent)
  with a younger tree tucked **behind** it (`circle 7.4,12 r3.2`,
  `--accent-soft`, its arc broken by true occlusion where it passes behind
  the crown) + two trunks.
- **wisp** (`wisp.svg`): five sparks splayed from one solid base —
  base (12, 17) r2.3 + four rising dots (opacity .58–.75). A mini-kodhama.

## UI iconography

Functional icons are **monoline `currentColor`**. The brand-inflected few
carry a motif in the two-tone: **watcher** (ring + spark — a mini-kodhama;
observe), **signal** (a spark broadcasting; event/telemetry), **watch**
(eye with a soft iris; live view). Solid dots are living points; outlines
are structure. See `identity/preview.html` for the specimen set. The full
inventory grows with the wisp UI, where real icon needs surface.

## Files in this directory

- `kodhama.svg`, `kodhama-quiet.svg` — the org mark's two adaptive states.
- `trellis.svg`, `grove.svg`, `wisp.svg` — the three product marks.

Each is self-contained: `xmlns` + `viewBox="0 0 24 24"`, `currentColor` for
strokes/fills. The two-tone strands read `var(--accent-soft, …)` with a
self-contained `color-mix` fallback, so they work with or without the token
defined by the host.
