# propagation-remediator — design-system addendum

Local rules for the `grove:propagation-remediator` role, read on top of the
canonical charter (`adr-0026` D3).

## Invoked by hand — there is no CI

design-system has no CI-enforced PR-contract check (no `.github/` in this repo;
`PR_CONTRACT_SECTIONS` = none CI-enforced). PR-first policy applies — agents
never merge — so a maintainer or another agent invokes you **by hand, before
merge**, when a PR's body is missing `## Propagation` and/or `## Recommended
next task`.

## This role is the propagation channel

design-system's self-improvement / propagation channel is **this role**, not a
separate `CLAUDE.md` section. Parked items ride each artifact's `## Open
questions` section and PR bodies (`PARKED_ITEM_STORE` = none dedicated);
decision-level triggers live in `decisions/` entries.
