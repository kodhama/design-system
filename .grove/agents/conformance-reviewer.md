# conformance-reviewer — design-system addendum

Local rules for the `grove:conformance-reviewer` role, read on top of the
canonical charter (`adr-0026` D3).

## No test/typecheck gate — verify by grep

design-system has no test suite, no typecheck command, and no test-deps ledger
(`TEST_CMD` / `TYPECHECK_CMD` / `TEST_DEPS_LEDGER` are honest-none;
tokens/markdown/SVG repo, not code). Where the charter says "run the gates
yourself," verify by grep instead — token provenance headers in `tokens.css`,
**tag parity** between what a claimed change touches and what it actually
changed, and icon legibility at 16px per `icons/grammar.md`'s own check. Do not
trust claimed results; look yourself. The absence of a gate is itself flagged,
never silently skipped.

## Broken consumer contract is a FAIL (adversarial check)

This repo's hard rule (README §"How this is consumed", `lp-generator.md`):
consuming repos read design-system **at a pinned git tag, never `main`**. A
change that would silently break a consumer reading a past tag — renaming or
removing something a generation-time link depends on without a tag/version
story, or that assumes unreleased `main` state a pinned consumer cannot see yet
— is a **FAIL** even if the diff looks clean in isolation.

## Propagation check by hand

There is no CI-enforced PR-body contract (no `.github/`; `PR_CONTRACT_SECTIONS`
= none CI-enforced) and no dedicated parked-item store (`PARKED_ITEM_STORE` =
none). Check propagation by hand: does the change action or fire anything parked
in an artifact's own `## Open questions` section or a PR body, a trigger
recorded in a `decisions/` entry, or a feedback artifact's disposition — that
the PR failed to name and update? A false "None." is a FAIL with the missed
item as evidence.
