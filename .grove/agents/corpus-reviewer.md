# corpus-reviewer — design-system addendum

Local rules for the `grove:corpus-reviewer` role, read on top of the canonical
charter (`adr-0026` D3). Corpus and contract come from `.grove/config.toml`
(`ARTIFACT_DIRS` = `decisions/`, `specs/`; `ARTIFACT_CONTRACT_PATHS` =
`decisions/README.md`, `specs/README.md`).

## Repo-typed check 8 — keep the consumer-tag rule in view

No repo-typed frontmatter checks beyond the family core (`REPO_TYPED_CHECKS` =
none). But this repo carries one hard consumer rule that sits next to where a
repo-typed check would live, and this role keeps it in view even though it is
not a frontmatter check: **consumers read this repo at a pinned git tag, never
`main` — content consumed by others must be covered by a tag.**

design-system's release unit is a git tag (`vX.Y.Z`; see `decisions/README.md`
§"Versioning is a separate axis"), and an artifact's `status: approved` is about
the decision being ratified, not about a release being cut — the two can and do
drift apart.

**Worked example of the gap this watches for:** the `identity/` directory landed
on `main` 47 minutes after the `v0.1.0` tag was cut, so no tag covered it — a
narrow but real violation of the repo's own "read at a pinned tag, never main"
consumer contract (recorded once in the external kodhama conductor ledger).

This role does not audit tags directly (that is a release-process check, not a
corpus-frontmatter one), but flag any artifact whose content consumers would
reasonably expect to reach through a tag and that the current tag doesn't cover.
