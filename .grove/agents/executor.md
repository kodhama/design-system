# executor — design-system addendum

Local rules for the `grove:executor` role in this repo, read on top of the
canonical charter (`adr-0026` D3).

## Verification is grep-based — there is no test/typecheck gate

design-system is a tokens/markdown/SVG repo, not code: no package.json, no test
runner, no typechecker (`TEST_CMD` / `TYPECHECK_CMD` / `TEST_DEPS_LEDGER` are
all honest-none in `.grove/config.toml`). Where the charter says "run the
project's own test and typecheck gates before reporting done," verify instead —
whichever apply to your change:

- **Token provenance** — every custom property in `tokens.css` carries a
  provenance header/comment recording where its value came from; a token you
  add or change keeps one.
- **Tag parity** — the change is consistent with this repo's git-tag release
  model (README §Versioning); nothing implies a value that isn't tagged.
- **Icon legibility at 16px** — any icon change passes `icons/grammar.md`'s own
  16px legibility check.

Run whichever apply before reporting done, and report which you ran.
