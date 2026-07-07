# kodhama icon family — grammar

Three marks, one grammar. Extracted from
`tools/espalier/identity/README.md` and `tools/espalier/identity/preview.html`
in the espalier repo (mq-source at lift time) — the identity's source of
truth before this repo became its one home.

**Status: provisional.** The README this was extracted from says so
explicitly: these are an initial stab, not a finalized identity. The
design-system pass that reviews and finalizes them (a design/judgment
sitting, per this org's model-economy rule — not a Sonnet-class execution
wave) has not happened yet. Treat `icons/*.svg` as placeholders faithfully
lifted from their prior home, not as approved final marks. That review is
an open item for this repo, tracked in the conductor ledger, not resolved
by this bootstrap.

## The family logic

Org: **kodhama** — a play on the *kodama*, the tree spirits of Japanese
folklore (see Miyazaki's *Mononoke Hime*): the quiet watchers of a healthy
forest. kodhama is the forest all three packages live in.

One grammar, three marks, each adding a layer to the same scene:

| Mark | File | Scene | Reading |
|---|---|---|---|
| **trellis** | `trellis.svg` | posts + laths — the bare structure | governance: the frame everything grows along |
| **espalier** | `espalier.svg` | the tree trained along the laths: trunk, tiers on the wires, growing tip | the swarm: growth under the frame |
| **espial** | `espial.svg` | nodes perched on the laths, edges converging, one lit | observability: the kodama watching — who is working, right now |

## Shared grammar

- **24×24 viewBox**, **1.7 stroke**, **round caps**, `currentColor` — no
  hard-coded color inside a mark; it inherits from context.
- **Solid accent = the living/active layer; 0.55 opacity = the structure.**
- The two laths (`M2 9h20 M2 15h20`) are the family constant — present in
  every mark, always as structure — **except in trellis's own mark**, where
  the structure *is* the subject: there, the verticals (the posts) carry
  the accent (full opacity) and the laths are still the 0.55-opacity
  structure line. Trellis has no separate "living" layer drawn on top of
  its own structure; the frame itself is what's being depicted.
- Marks must survive at **19px** (header size) — legible, not muddy, no
  overlapping strokes reading as a blob. Check by rendering each mark at
  19×19 alongside its full-size version; `icons/preview.html`-style
  side-by-side (not included in this repo — build one ad hoc, or reuse the
  espalier repo's `identity/preview.html` pattern) is the fastest way to
  eyeball it. All three marks here were extracted from a source that had
  already passed this check once (see `preview.html`'s `.small` tiles,
  rendered at `width:19px;height:19px`).

## Files in this directory

- `trellis.svg` — posts + laths, no separate accent layer (see grammar
  exception above).
- `espalier.svg` — laths (structure) + trunk/tiers/tip (accent).
- `espial.svg` — laths (structure) + two open nodes + one filled (lit)
  node + converging edges (accent).

Each file is self-contained: `xmlns` declared, `viewBox="0 0 24 24"`
preserved, `currentColor` for strokes/fills so the mark inherits color from
whatever wraps it (set `color` on a parent element or pass a `style`/class
override — do not hard-code a hex inside these files).
