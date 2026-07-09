# specs/

This repo's own specs — contract-layer artifacts for design-system's own
tooling (e.g. a spec for a change to `lp-generator.md`'s contract, or an
icon-grammar amendment), written by a `contract-author` agent from an
approved decision and never from a draft. Seeded minimal alongside
installing [grove](https://github.com/kodhama/grove) as this repo's
operating model: this directory mirrors
[grove's own `specs/`](https://github.com/kodhama/grove/tree/main/specs)
shape, adapted, not a heavier process invented on top of it.
design-system has no dedicated spec-quality or research-quality rubric
file yet — self-check against the artifact contract below (frontmatter
present, `## Acceptance criteria` testable, `## Open questions` present
even if empty) until one is warranted.

## Artifact contract

Every artifact in this repo (here, and in `decisions/`) begins with
YAML frontmatter:

```yaml
---
id: spec-short-slug       # kebab-case, prefixed by type
type: spec                # adr | spec | plan | rubric | ...
status: draft | gated | approved | superseded
depends_on: [adr-0000-...]   # ids of upstream artifacts this one builds on
owner: agent | human
updated: YYYY-MM-DD
---
```

- `draft` — not yet self-checked; not a valid downstream input. An
  `executor` agent never implements against a `draft` spec.
- `gated` — self-checked against its rubric (if any); agent-consumable.
  The `spec-adversary` agent runs against `gated` specs, before a
  human ever sees them.
- `approved` — ratified by human merge. Never set by hand.
- `superseded` — retired; a forward pointer names the replacement (see
  `decisions/README.md` for the append-only discipline this inherits).

Every spec must carry `## Acceptance criteria` (checkable) and
`## Open questions` (may be empty, but must exist) — a spec that
cannot say what "done" means is not yet a spec. A research artifact
(`type: discovery`, per the `divergent-researcher` agent) is also
filed here, since design-system has no separate research-artifact
directory.

## The pinned-tag consumer contract binds specs too

A spec that touches anything a consuming repo's generation-time link
depends on (`tokens.css`, `patterns.md`, `lp-generator.md`'s contract)
must say, in its acceptance criteria, whether the change requires a new
tag before any consumer can see it — design-system's hard rule is that
consumers read this repo at a pinned git tag, never `main` (see the root
`README.md` §"How this is consumed"). Silence on this is a gap the
`spec-adversary` agent should catch, not an assumption to leave
implicit.
