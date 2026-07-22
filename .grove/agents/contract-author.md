# contract-author — design-system addendum

## No spec-quality rubric — self-check against the artifact contract

design-system has no dedicated spec-quality rubric file (`SPEC_RUBRIC_PATH` is
honest-none in `.grove/config.toml`). Where the charter says "self-check
against the spec-quality rubric," self-check against `specs/README.md`'s
artifact contract instead — frontmatter present, `## Acceptance criteria`
testable, `## Open questions` present even if empty — and append a
`## Rubric check` section recording the result honestly. A failing check is
listed, never silently passed.
