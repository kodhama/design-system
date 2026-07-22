# decisions/

This repo's own architecture decision records (ADRs) — the intent-layer
artifacts for design-system itself (token/pattern/icon design choices,
versioning and consumption-contract calls). Seeded minimal alongside
installing [grove](https://github.com/kodhama/grove) as this repo's
operating model: this directory mirrors
[grove's own `decisions/`](https://github.com/kodhama/grove/tree/main/decisions)
shape, adapted, not a heavier process invented on top of it.

## Artifact contract

Every artifact in this repo (here, and in `specs/`) begins with YAML
frontmatter:

```yaml
---
id: adr-000x-short-slug   # kebab-case, prefixed by type
type: adr                 # adr | spec | plan | rubric | ...
status: draft | gated | approved | superseded
depends_on: [adr-0000-...]   # ids of upstream artifacts this one builds on
owner: agent | human
updated: YYYY-MM-DD
---
```

What each `status` value means, and who moves an artifact between
states, lives with the grove **lifecycle companion** — shipped in the
grove plugin, not vendored here (per the grove lifecycle companion, the
`grove plugin@<version>` stamp in this repo's `CLAUDE.md`; `grove/adr-0008`,
`grove/adr-0026` D7) — not restated here.

## Versioning is a separate axis

design-system's *release* unit is a git tag (`vX.Y.Z` — see the root
`README.md` §Versioning); a decision's `status: approved` is about the
decision being ratified, not about a release being cut. A decision that
changes what a consuming repo should pin to still needs a tag before
that change is real for anyone reading at a pinned ref — note that
explicitly in the decision rather than assuming the merge alone
propagates it.

## Decisions are append-only

**Never edit a ratified (`approved`) decision in place.** To change one:
write a new decision, mark the old one `status: superseded` (or
`superseded in part` for a partial change), and add a one-line forward
pointer at the top of the superseded text naming the new decision's
`id`. No reader should ever land on stale text without a link forward
— this is how "why is it this way?" stays answerable later.
