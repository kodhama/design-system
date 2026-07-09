# kodhama/design-system

The kodhama family's design system — a **brand asset**, not a library and
not a runtime dependency. It holds the tokens, component patterns, and icon
marks that give every kodhama product's landing page (and, eventually,
other brand surfaces) a consistent look, in one place instead of
copy-pasted and drifting across repos.

The family: [trellis](https://github.com/kodhama/trellis) (governance) ·
[grove](https://github.com/kodhama/grove) (agent swarm) ·
[wisp](https://github.com/kodhama/wisp) (runtime observability) ·
this repo (design-system) · [homebrew-tap](https://github.com/kodhama/homebrew-tap)
(delivery).

## What's here

- `tokens.css` — every CSS custom property from the source landing page
  (trellis's), covering the light block, the `prefers-color-scheme: dark`
  block, and the explicit `[data-theme="light"]` / `[data-theme="dark"]`
  override blocks.
- `patterns.md` — component patterns (eyebrow, card, terminal, lattice
  motif, theme toggle, climbing-plant animation, compare-pairs,
  buttons/pills) as faithful CSS/HTML reference extracts.
- `icons/` — the five family marks (the org mark `kodhama`/`kodhama-quiet`,
  plus the three product marks `trellis`, `grove`, `wisp`) as self-contained
  SVGs, plus `icons/grammar.md` with the shared grammar rules and the 16px
  legibility floor. **Finalized** by the T2 design-review pass — see
  `icons/grammar.md` and `identity/spec.md`.
- `identity/` — `spec.md` (the finalized identity spec) plus the original
  identity working notes and preview (`README.md` + `preview.html`) that
  `icons/` and `icons/grammar.md` were first extracted from during the wave
  1 lift, kept as provenance and marked superseded rather than rewritten.
- `lp-generator.md` — the contract a consuming repo's LP run follows to
  generate its own `docs/index.html` from this repo.

## How this is consumed

**Generation-time links, never build coupling.** This is the soft-dependency
rule (see the family's decision log): a consuming repo does not `npm
install` this package, does not import it at runtime, and does not fetch
anything from it in a shipped artifact. Instead, at generation time, a
product's LP run:

1. Reads this repo **at a pinned git tag** (never `main`, never a floating
   ref).
2. Combines its own content (`docs/lp-content.md` in the consuming repo)
   with this repo's `tokens.css` and `patterns.md`.
3. Writes out a single self-contained `docs/index.html` in the consuming
   repo — no external fetches, no `<link>` back to this repo, no runtime
   dependency once generated.
4. Stamps the tag it generated from into an HTML comment
   (`<!-- kodhama-ds: vX.Y.Z -->`) so staleness can be checked later,
   without that check ever blocking a build.

Full instructions for that process live in `lp-generator.md` — it's the
file a consuming repo's run actually loads.

This keeps dependency direction consistent with the rest of the family
(wisp → grove → trellis, strictly downward): the design system sits
above all of them and reaches them only through this generation-time link,
never the other way around, and never as a build-time coupling that could
break a product's build if this repo has an issue.

## Versioning

Version = **git tags**. Every release is a tag (`vX.Y.Z`); there is no
separate changelog or package registry entry to keep in sync — the tag
*is* the version, and consuming repos pin to one explicitly. Tag before any
consuming repo generates against a given state of this repo; an untagged
commit has no stable identity for the `kodhama-ds` stamp to record.

## Status

Bootstrapped from trellis's landing page (`docs/index.html`), the design
system's original source of truth — this is an extraction of what already
shipped there, not a from-scratch redesign. The icon family's
design-review pass is complete (see `icons/grammar.md` and
`identity/spec.md`); the additions from that pass (the org mark, the
two-tone marks, and the seasonal/type/spacing tokens in `tokens.css`)
aren't yet covered by a git tag — pin to the next tag cut after this
merges to pick them up.

## License

MIT — see `LICENSE`.
