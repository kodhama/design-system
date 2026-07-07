# kodhama-ds — LP generator instructions

This file is what a consuming repo's LP furrow (the agent/process that
builds that repo's landing page) loads to generate a page from this design
system. It is the contract between `kodhama/design-system` and every
product repo that wants a landing page in the family's look.

## Read this repo at a tag, never at a branch

Pin a git tag (e.g. `v0.1.0`) — never `main`, never a branch, never a
floating ref. This is the soft-dependency rule from the family's decision
0001: the DS reaches consumers only through generation-time links, and a
generation-time link that floats defeats the point. At generation time,
fetch `kodhama/design-system` at the pinned tag and read from it:

- `tokens.css` — the full set of custom properties (light, dark,
  `data-theme` blocks).
- `patterns.md` — the component patterns (CSS/HTML reference blocks) to
  draw on.
- `icons/*.svg` + `icons/grammar.md` — the mark family, if the page needs
  a brand mark.

## Generate `docs/index.html`

Inputs, both from the *consuming* repo:

1. `docs/lp-content.md` — the consuming repo's actual content: hero copy,
   sections, CTAs, install commands, whatever that product's landing page
   needs to say. This repo (`design-system`) supplies no copy — content is
   always the product's, never the DS's.
2. This repo's `tokens.css` + `patterns.md` (read at the pinned tag, per
   above).

Output: a single `docs/index.html` in the consuming repo, built by
composing the consuming repo's content into the DS's patterns, styled by
the DS's tokens. Follow `patterns.md` faithfully — it's a reference
extract, not a suggestion; deviate only where the consuming repo's content
genuinely doesn't fit a pattern, and note the deviation in the generated
file's own comments.

## Stamp the tag

The generated file must carry the tag it was generated from, in an HTML
comment near the top of `docs/index.html`:

```html
<!-- kodhama-ds: v0.1.0 -->
```

This is the only record of provenance the generated file carries — it's
how staleness gets checked later (see below). Don't omit it, don't stamp a
branch name or commit SHA instead of the tag, and don't hand-edit it after
generation.

## Vendor the output

The generated `docs/index.html` must be **self-contained**: all CSS
inlined (from `tokens.css` + whatever pattern CSS was used), no `<link>`
to this repo, no runtime `fetch()` of `tokens.css` or anything else from
`kodhama/design-system`, no CDN dependency. The DS is consumed at
generation time only — once `docs/index.html` exists in the consuming
repo, it must render correctly with network access to nothing but its own
bytes. This is what "generation-time links, never build coupling" means in
practice: the coupling happens once, when the furrow runs, and leaves
behind a plain static file.

## Staleness is a finding, not a build break

The furrow (or a periodic check) may compare the stamped tag in
`docs/index.html` against this repo's latest release tag. If they differ,
that's staleness: the consuming repo's LP was generated from an older DS
version than what's now available.

- Staleness is **never** a build failure and never blocks anything.
- Surface it as a finding — a line in a status report, a conductor ledger
  note, a comment on a PR — something a human sees, not something that
  halts a pipeline.
- Regenerating to pick up a newer tag is a deliberate choice the
  consuming repo's owner makes, not something forced by the mere existence
  of a newer DS version. A product may intentionally stay pinned to an
  older tag for a while; that's a legitimate state, not an error state.

## Versioning

This repo's version is its git tags (see `README.md`). Tag before a
consuming repo generates against a commit — an untagged commit has no
stable identity for the stamp to record.
