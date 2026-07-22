# run-resumer — design-system addendum

## Repo conventions for resuming a run

- **Branch discovery** — design-system has no issue-number-in-branch
  convention; branches are `<category>/<slug>` (e.g. `chore/install-grove`).
  Find a task's branch with `git branch -r | grep <the task's slug>`.
- **Landing discipline** — conventional commits, PR-first: **agents never
  merge**. Resume toward a PR, not a merge.
- **Consumer contract (hard constraint)** — consuming repos read this repo at a
  pinned git tag, never `main` (README §"How this is consumed"). Never resume
  work in a way that silently breaks that for a pinned consumer; check
  `.trellis/` and `CLAUDE.md` for this repo's other constraints.
