# code-reviewer — design-system addendum

Local rules for the `grove:code-reviewer` role, read on top of the canonical
charter (`adr-0026` D3).

## Convention sources (the standards-source priority order, resolved)

The root `CLAUDE.md` is grove/trellis managed blocks only, **not** a conventions
doc (`CONVENTIONS_PATH` records this). Judge against these declared sources:

- `patterns.md` — component patterns; extracts must reference `tokens.css`
  custom properties, never hard-coded values.
- `icons/grammar.md` — shared icon grammar and the **16px legibility floor**.
- `identity/spec.md` — the finalized identity spec.
- `specs/README.md` — the artifact contract for `specs/` and `decisions/`.

Where the project declares nothing, flag the absence of a declared convention
as a finding rather than inventing taste.

## No lint command — verify by grep

design-system has no linter/formatter (`LINT_CMD` is honest-none: no
package.json, no lint config; tokens/markdown/SVG, not code) and no quality
rubric (`QUALITY_RUBRIC_PATH` = none). Where the charter says "run the lint
command," run the grep-based checks instead — token provenance headers in
`tokens.css`, icon legibility at 16px per `icons/grammar.md`'s own check — and
report what you actually saw.
