# kodhama identity — spec

Locked 2026-07-07, from the identity sitting (design pass "plan-suite-lift T2").
Supersedes the **provisional** status in `icons/grammar.md`. Everything here
extends the existing grammar (24×24 viewBox · 1.7 stroke · round caps ·
`currentColor` · laths `M2 9h20 M2 15h20` as the family constant); nothing
replaces it.

## The org mark — the echo

Kodama also means *echo*. The kodhama mark is a ring holding the wires — the
forest the family lives in, answering back.

The mark is **adaptive** (two states, one rule — *one echo per surface*):

| State | File | When | Drawing |
|---|---|---|---|
| **Spark echo** | `icons/kodhama.svg` | Standing alone: GitHub org avatar, favicon, app icon, social | Ring r6.8 + two sparks leaving at 45°: solid Ø2.6 at (19.3, 4.7), faint Ø1.7 at (21.9, 2.1), opacity .45 |
| **Quiet echo** | `icons/kodhama-quiet.svg` | Beside the wordmark (headers, lockups) | Plain ring r7.5, nothing else |

Beside the name the mark goes quiet because the **wordmark carries the
sparks** (below) — mark and name speak one vocabulary, so the adaptive pair
reads as one being, not two logos. The ring shrinks to r6.8 in the spark
state to make room; that size difference is optical and intentional.

**Update (2026-07-15) — GitHub org avatar reassigned to the quiet echo.**
The table above still lists "GitHub org avatar" under the spark echo, but
that's now superseded: `kodhama.svg`'s faint outer spark (21.9, 2.1) sits
outside the inscribed circle of its own 24×24 canvas and gets clipped by
a true edge-to-edge circular avatar crop (verified by rendering — see
`decisions/adr-0001-t2-identity-finalization.md`, Open question 3). The
maintainer's call: use `icons/kodhama-quiet.svg` — plain ring, no corner
elements, immune to the crop — for the GitHub org avatar instead. This is
a one-off exception to *one echo per surface* (the quiet echo is now
standing alone here, not beside the wordmark); the spark echo keeps
favicon/app-icon/social.

## The shared fragment — family rule

Each product is **one fragment of the kodhama mark**, and the rule is
**spirits are solid, structure is faint**: kodhama and wisp carry the
living spark; grove and trellis are the structure the spirits inhabit.
(This retires the earlier "exactly one point of life per mark" rule.)

- **kodhama** — the whole: ring + two sparks, solid (19.3, 4.7) r1.3 and
  faint (21.9, 2.1) r.85 opacity .45. The great spirit; wisps are its
  sparks set free.
- **trellis** — the **laths** (the frame). Now a **woven** mark: three
  posts and two laths in a true over-under, square butt corners at the
  tucks and round caps only on the open ends. The posts take the accent;
  the laths take `--accent-soft` (a lighter shade of the accent, so the
  over/under reads in colour and tracks every seasonal palette). No bud
  dot — structure stays faint under the new rule; the weave is what gives
  trellis its character instead.
- **grove** — the **ring** as a crown over trunks. Now **two-tone**: a
  mature crown in the accent (`circle 13.4,9.4 r5.6`) with a younger tree
  tucked **behind** it in `--accent-soft` (`circle 7.4,12 r3.2`, its arc
  broken by true occlusion where it passes behind the crown), and two
  trunks. The soft second tree gives grove the same depth the woven laths
  give trellis.
- **wisp** — the **sparks**, three splayed from one solid base (a
  mini-kodama). Solid base (12,17) r2.3 is the living spark; the four
  rising dots (opacity .58–.75) are its echoes.

## Wordmark

Lowercase **kodhama**, always. Sans stack (`ui-sans-serif, system-ui,
-apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`), weight
650, letter-spacing −0.02em.

**The sparks** (from the swallowed apostrophe of *Kod'hama* — the spirit is
still in the name, just quiet): two dots rising off the final *a*,
up-and-right. At a 30px wordmark (the reference size):

- solid spark: Ø4.5px at +3px right of the final glyph, 25px above the
  inline-box top edge offset (`left:3px; top:-25px` on a zero-width anchor)
- faint spark: Ø3px at `left:8px; top:-31px`, opacity .45

Scale proportionally (em-based: Ø0.15em / Ø0.10em); nudge optically at
small sizes. The sparks appear **only when the wordmark stands alone or in
the lockup** — never on the mark at the same time (one echo per surface).

## Lockup

Quiet echo + wordmark, horizontal. At the 30px reference: mark 34px,
gap 12px (0.4em), and the wordmark raised **2px** above flex-center so the
lowercase x-height band sits between the mark's two wires (1px at ~17px
header size). This vertical trim is required, not optional — centered-box
alignment reads visibly low.

## Color

Marks and wordmark are `currentColor` — they take the accent from context.
Tokens per `tokens.css`: light `--accent: #1f9d68` / `--accent-ink:
#0c5d3c`; dark `--accent: #4ccb90`. On dark tiles (avatar) use the dark
accent on `--bg` (#0d1411).

### Seasonal accents (optional layer)

The accent triad may turn with the sun — solstices and equinoxes — while
every neutral stays fixed: the forest changes color, not shape. Green is
the year-round default wherever seasons are off.

| Season | From | accent | accent-ink | dark accent |
|---|---|---|---|---|
| spring (default) | Mar equinox | `#35b077` | `#156b45` | `#62dfa3` |
| summer — Alentejo wheat | Jun solstice | `#ba8b26` | `#7d5a14` | `#e6c260` |
| autumn — red leaf | Sep equinox | `#bf4f30` | `#86301c` | `#e89673` |
| winter — frost | Dec solstice | `#4f93a8` | `#245b6e` | `#85cfe0` |

Implementation: `:root[data-season="…"]` overrides the three tokens; season
picked by date at generation time (vendored LPs stay self-contained) or by
one line of runtime JS. Staleness is a finding, not a break — same as the
DS versioning rule.

**Codified in `tokens.css`:** the four `:root[data-season="…"]` blocks ship
with dark-mode variants and explicit-theme pins. The type scale, radius,
shadow and spacing tokens surfaced on the spec sheet were codified in the
same pass. This repo's release unit is a git tag (see root `README.md`
§Versioning) — these token additions are covered by `v0.2.0`; consuming
repos should pin to that tag (or later) to pick them up.

## Social preview images (2026-07-15)

Each product repo gets its own GitHub social-preview image (the card
GitHub/Slack/Discord/etc. render when a repo or PR link is shared) —
carrying **that repo's own mark**, distinct from the org avatar (which is
necessarily singular — GitHub has one avatar per org, not per repo; see
`lp-generator.md`'s Favicon section for that distinction spelled out).

Convention: 1280×640px (GitHub's recommended ratio), light background
(`--bg`/`--surface`, evergreen unless a repo has a specific reason to
season-pin a static image), the repo's own mark + bold wordmark + a
mono, uppercase, letter-spaced tagline pulled from that repo's own
README — plus a small `kodhama-quiet.svg` + "kodhama" chip, bottom-right,
tying the family together without competing with the product's own mark.

Convention path: `.github/social-preview.png`, committed in the
*consuming* repo (this repo stays source-SVG-only, per its own no-raster
convention) — GitHub does not auto-read this path, it's a manual upload
via that repo's Settings → General → Social preview, but checking in the
generated PNG keeps the artifact's provenance next to the repo it
represents, the same reasoning as `docs/favicon.svg` living in the
consuming repo rather than here. First three examples: `trellis`,
`grove`, `wisp` (added 2026-07-15) — reasonable references for the next
one.

## Lore register (internal)

*Kod'hama* is the true-name spelling — Gundisalwa Kod'hama — kept as lore,
never as the outward brand. Its only public surface is the sparks: the
apostrophe the name swallowed, still rising off the end of the word.

## Files

- `icons/kodhama.svg` — spark echo (standalone contexts)
- `icons/kodhama-quiet.svg` — quiet echo (lockups)
- `icons/trellis.svg` — the laths (the frame)
- `icons/grove.svg` — the ring as a crown over trunks
- `icons/wisp.svg` — the sparks, a splayed trio from one base

All self-contained, `currentColor`, 24×24. Must survive 19px (header) and
16px (favicon); the spark echo was checked at both.
