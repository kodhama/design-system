---
id: adr-0001-t2-identity-finalization
type: adr
status: draft
depends_on: []
owner: agent
updated: 2026-07-10
---

# ADR-0001: T2 identity & icon-family finalization

> **This is a retrospective reconstruction, authored 2026-07-10, not a
> contemporaneous decision record.** The T2 design pass it documents
> shipped on 2026-07-08 (commit `592b1df`, tag `v0.2.0`) — before this
> repo's `decisions/`/`specs/` machinery existed in practice for a design
> event of this size (the machinery itself landed earlier the same day,
> `67acfb2`, but T2 produced no artifact against it; see Context). This
> ADR was written *after the fact*, from the shipped diff, the current
> state of `icons/grammar.md` / `identity/spec.md` / `identity/README.md`
> / `tokens.css`, and the commit/PR trail — **not** from a transcript of
> the actual design conversation ("the identity sitting," run with Claude
> design per `plan-suite-lift` Lane T2). Anywhere this document states
> *why* a choice was made, it is quoting or paraphrasing the shipped
> artifacts' own stated rationale (verifiable) or explicitly flagged as
> this author's inference (not verifiable) — never invented to fill a
> gap. Status is `draft`, not `gated`/`approved`, because the maintainer
> needs to confirm the reconstruction matches actual intent before this
> is treated as settled ground.

## Context

`decisions/` and `specs/` were seeded in this repo by `67acfb2` ("install
grove as operating model," 2026-07-08 08:23 UTC+1), explicitly scoped by
`decisions/README.md` to "token/pattern/icon design choices." About 12
hours 22 minutes later the same day, `592b1df` ("identity: finalize icon
family + org mark (T2 design pass) (#6)," 2026-07-08 20:45 UTC+1, merged
as PR #6, tagged `v0.2.0` nine minutes after landing) shipped exactly
that kind of choice — the single largest design event in the repo's
history — and produced zero decision/spec artifacts.

This wasn't an unnoticed gap at the time. PR #6's own body says so
directly:

> No formal `specs/`/`decisions/` artifact. This repo recently adopted
> grove's frontmattered decision/spec contract, and an icon-grammar
> amendment is explicitly named as spec-worthy in `specs/README.md`. I
> didn't add one because the authorizing decision
> (`kodhama-0003-family-naming`) isn't present in this repo's own
> `decisions/` for a new spec to `depends_on` — happy to add one as a
> follow-up if that's expected process now.

That follow-up never happened until a 2026-07-10 family consistency-sweep
audit flagged the gap (`kodhama/design-system#9`). The maintainer's call,
recorded there: backfill a retroactive decision rather than accept T2 as
a one-time process gap. This ADR is that backfill.

**Separately, and only loosely related:** that same 2026-07-10 sweep also
flagged a legibility-floor contradiction between two T2-authored files.
This ADR's own drafting re-verified that finding directly against the
live files (see "Known unresolved contradiction, re-verified" below) and
found it was **still live in the repo at drafting time** — despite PR #8
and `kodhama/design-system#9`'s own text both describing it as
"already fixed" / "resolved... maintainer-confirmed." That claim did not
match the actual PR #8 diff (which touches only tag-coverage wording in
`README.md`/`identity/spec.md`, never the legibility-floor lines) or the
file contents as they stood then. Flagged loudly here rather than quietly
treated as settled, per this repo's own working rules — and, separately
from this backfill, it has since been fixed: PR #11 (merged 2026-07-10,
later the same day) resolved it in favor of `icons/grammar.md`'s 16px
floor. See "Known unresolved contradiction, re-verified" below for the
current state.

## Decision (reconstructed — what T2 actually shipped)

The org mark, kodhama, was added as an **adaptive two-state mark**
(`icons/kodhama.svg` — "spark echo," standalone contexts: org avatar,
favicon, app icon, social; `icons/kodhama-quiet.svg` — "quiet echo,"
beside the wordmark in lockups, one rule: *one echo per surface*).
`identity/spec.md`'s own stated reason for the two states: "the wordmark
carries the sparks... mark and name speak one vocabulary, so the adaptive
pair reads as one being, not two logos."

A new **family-fragment logic** replaced the prior "each mark separately
follows a shared grammar" framing: kodhama is the whole (ring + sparks +
laths), and each product mark now reads as carrying **one fragment** of
it — trellis the laths, grove the ring, wisp the sparks. `icons/
grammar.md`'s own framing: "each product carries one fragment of the
kodhama mark, so the family reads as one thing split three ways."

That reframing came with a new family rule, **"spirits are solid,
structure is faint,"** which explicitly retires the prior rule ("solid
accent = living layer, 0.55 opacity = structure," plus a one-off trellis
exception):
- **kodhama** and **wisp** carry the living spark (solid fills).
- **grove** and **trellis** are the structure the spirits inhabit — depth
  now comes from a second color tone, not opacity.

Concretely, three of the four/five mark files were redrawn (geometry
verified directly against the shipped SVGs):
- **trellis** (`icons/trellis.svg`): rewoven as three posts / two laths
  in a true over-under weave — square butt corners at the tucks, round
  caps only on the open ends; posts in the accent, laths in the new
  `--accent-soft` tone. Drops the previous mark's separate accent/
  structure split (posts full-opacity, laths 0.55-opacity) in favor of
  the two-tone treatment.
- **grove** (`icons/grove.svg`): redrawn as a mature crown
  (`circle 13.4,9.4 r5.6`, accent) with a younger tree tucked behind it
  (`circle 7.4,12 r3.2`, `--accent-soft`) plus two trunks; the younger
  tree's arc is drawn with true geometric occlusion where it passes
  behind the crown, rather than a flat opacity layer. Replaces the prior
  trunk/wire-tiers/growing-tip drawing entirely.
- **wisp** (`icons/wisp.svg`): redrawn as five sparks splayed from one
  solid base (`circle 12,17 r2.3`, solid; four rising dots at opacity
  .58–.75) — a "mini-kodhama." Replaces the prior two-open-node-plus-one-
  lit-node drawing.
- **kodhama** / **kodhama-quiet** (new files): per the adaptive-mark
  description above; exact geometry recorded in `identity/spec.md`.

A new token, **`--accent-soft`**, was added to carry the two-tone
treatment: `color-mix(in srgb, var(--accent) 58%, var(--surface))`. Its
stated reason (`icons/grammar.md`, `tokens.css`): tracks both theme and
season and "never muddies to grey the way an opacity-dimmed accent does."

`tokens.css` also gained several other token groups, verified directly
against the diff — the repo's own commit message groups these as
"`--accent-soft`, seasonal accents, type/spacing/radius/shadow tokens";
enumerated exactly, they are:
- 4 new layout/spacing tokens (`--gutter`, `--space-section`,
  `--card-pad`, `--grid-gap`)
- 5 new radius tokens (`--radius-chip/button/panel/card/pill`)
- 1 new elevation token (`--shadow-lift`)
- 7 new type-scale tokens (`--text-display/section/card/lede/body/
  eyebrow/mono`)
- 6 new type-treatment tokens (`--weight-heading/strong`,
  `--tracking-heading/eyebrow`, `--leading-heading/body`)
- a seasonal-accent subsystem: 4 seasons (spring/summer/autumn/winter) ×
  light-default + dark-media-query + explicit light/dark theme-pin
  overrides for `--accent`/`--accent-ink`

(This author cannot confirm whether "5" in prior audit language maps
exactly onto this enumeration — the grouping is a matter of how you
count a "category"; the token additions themselves are directly verified
against the diff, the count-label is not load-bearing.) `tokens.css`'s own
comment states these values were "codified from `identity/spec.md` + the
consistent values in use across the pages (surfaced on the design-system
spec sheet) — codification, not redesign." This author has **not**
independently re-verified that every numeric value matches live usage
across trellis/grove/wisp's pages byte-for-byte — that claim is quoted
from the source, not independently re-confirmed here.

`identity/README.md` (the pre-T2 working notes) was **left unedited** and
given a forward-pointer note marking it superseded by `identity/spec.md`
— this repo's supersede convention, applied correctly (verified: the diff
touching this file is additive-only, 7 lines added, 0 removed).

`identity/preview.html` was hand-regenerated as a static, self-contained
page for all 5 marks. The handoff's own `preview.dc.html` + `support.js`
runtime (an in-browser JSX runtime, per PR #6's description) was
deliberately not vendored, consistent with this repo's stated no-runtime-
dependency stance (root `README.md`, "How this is consumed").

Deliberately **not** done at T2 time (both per the commit message and
independently confirmed true as of this writing): no git tag cut manually
by the pass itself (`v0.2.0` was tagged separately, 9 minutes after the
commit landed); no changes to sibling repos (grove/wisp/trellis/homebrew-
tap).

## Rationale — sourced vs. inferred

Everything in "Decision" above is directly quoted or paraphrased from
`icons/grammar.md`, `identity/spec.md`, `tokens.css`'s own comments, or
PR #6's body — this author verified each claim against the live file
content rather than trusting the commit message alone. Two things this
ADR explicitly does **not** claim to know, because no record of them was
found:

1. **Why this specific fragment-split** (kodhama+wisp "spirit," grove+
   trellis "structure") over some other assignment — the shipped text
   states the mapping and a one-line thematic gloss per product
   (governance/assembly/observability), but does not record what
   alternative splits, if any, were considered and rejected during the
   actual design sitting. This ADR reports the metaphor as given, not a
   deeper justification that isn't written down anywhere this author
   could find.
2. **Why these specific geometric choices** (e.g., trellis's exact
   over/under tuck pattern, grove's specific occlusion radius) over other
   candidate drawings — the files record the final geometry precisely,
   not the design iteration that arrived at it. "The identity sitting"
   itself (the actual Claude-design conversation) is not preserved
   anywhere this author could locate in this repo or the sibling repos
   searched (`kodhama`, `math-quest`, `grove`).

Where the source material does state an explicit reason (accent-soft
over opacity; the adaptive mark's quiet-beside-wordmark logic; no-
runtime-dependency for `preview.html`; seasonal accents as a lore
extension), this ADR quotes it directly rather than restating it as this
author's own conclusion.

## Known unresolved contradiction, re-verified

`kodhama/design-system#9`'s own text described the `icons/grammar.md`
(16px) vs. `identity/spec.md` (19px + 16px) legibility-floor contradiction
as "already fixed in PR #8... resolved in favor of grammar.md (16px),
maintainer-confirmed." **At drafting time, this author re-verified that
claim against the actual PR #8 diff and the then-current file contents,
and it did not hold:**

- PR #8's own body lists this contradiction explicitly under "Out of
  scope (per instruction)," gated on "an unresolved maintainer question."
- PR #8's diff touches exactly three files (`​.trellis/profile.md`,
  `README.md`, `identity/spec.md`) and, within `identity/spec.md`, only
  the tag-coverage sentence — never the legibility-floor lines.
- At drafting time, `icons/grammar.md` line 41 read: "Every mark and icon
  must survive **16px** (favicon)." — no mention of 19px. `identity/
  spec.md` line 125–126 read: "Must survive 19px (header) and 16px
  (favicon); the spark echo was checked at both." Both lines had been
  unchanged since `592b1df` up to that point.

So the contradiction T2 itself introduced (two files it authored in the
same pass disagreeing on whether a 19px header-size legibility check was
still required, or only a 16px favicon check) was live when this ADR was
drafted.

**Update (2026-07-10, later the same day): resolved by PR #11, separately
from this ADR.** PR #11 dropped the 19px reference from `identity/
spec.md`, restating the floor as 16px only to match `icons/grammar.md`
(now the sole authority for the check), and made the corresponding fix in
`identity/preview.html`'s small-size specimens and in `.claude/agents/
executor.md` / `.claude/agents/conformance-reviewer.md`'s citations of
the check. This was handled as its own fix rather than folded into
gating this ADR — the maintainer's call, per the related discussion on
`kodhama/design-system#9`. As of PR #11, `icons/grammar.md` and
`identity/spec.md` no longer disagree.

Separately, and still open: `identity/spec.md`'s claim that "the spark
echo was checked at [16px]" is not corroborated anywhere else in the
repo — PR #6's own test plan carried an explicit, never-checked-off item:
"Reviewer: confirm the two-tone occlusion on `grove.svg` and the woven
over/under on `trellis.svg` read cleanly at 19px/16px in an actual
browser." This ADR does not resolve that unverified-legibility claim — it
remains open (see Open questions). The contradiction itself, per the
update above, was resolved separately by PR #11, not by this ADR.

## Consequences

- The repo now has a decision record for its largest design event,
  closing the "zero artifacts" gap `kodhama/design-system#9` flagged —
  but only once a human confirms this reconstruction is accurate (see
  status).
- This does not retroactively change T2's `gated`/`approved` status math
  — T2 shipped via ordinary PR merge (#6) before the decision/spec
  contract was being enforced on design work; this ADR does not assert
  T2 needed to be blocked on a decision that didn't exist yet. It only
  documents, after the fact, what was decided.
- Future design passes of this size are expected to produce a decision
  (`gated` before merge, `approved` at merge) prospectively, not
  retrospectively — this ADR is not a template for skipping that step
  again; it is a one-time backfill for a gap that predates the norm
  being enforced in practice.
- The legibility-floor contradiction was resolved separately, by PR #11
  (2026-07-10) — not by this ADR (see "Known unresolved contradiction,
  re-verified" above). The unverified 16px favicon render claim remains
  open (see above) — not resolved by this ADR, not silently waved through
  either.

## Open questions

1. **Maintainer confirmation needed:** does this reconstruction match
   actual intent from the identity sitting? In particular: is the
   fragment-split metaphor (§Rationale item 1) the actual reasoning, or
   was there additional design logic not captured in the shipped text?
2. ~~Should the `icons/grammar.md` (16px) vs. `identity/spec.md` (19px +
   16px) contradiction be resolved as part of gating this ADR, or handled
   as a separate follow-up decision?~~ **Moot, resolved:** PR #11
   (2026-07-10) fixed the contradiction directly as its own change,
   separate from this ADR — the maintainer's call, per the related
   discussion on `kodhama/design-system#9`. No gating decision on this
   ADR was needed.
3. Should the unverified 16px-favicon-legibility claim in
   `identity/spec.md` be checked against a real renderer before this ADR
   is gated, given `kodhama.svg`'s faint spark (`r=.85`, 45% opacity) is
   the highest-risk detail at that size?
4. Is the token-count framing ("5 new token categories," from the prior
   audit) worth reconciling against this ADR's more granular enumeration,
   or is the discrepancy immaterial?
