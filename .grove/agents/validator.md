# validator — design-system addendum

## Guard the pinned-tag consumer contract

design-system's hard consumer rule (README §"How this is consumed",
`lp-generator.md`): a consuming repo reads this repo **at a pinned git tag,
never `main`**. In your per-PR critique, flag any change that would silently
break that contract for a consumer pinned to a past tag — a token value,
pattern, or icon a pinned consumer already depends on, changed without a tag to
carry it forward.
