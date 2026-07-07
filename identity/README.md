# kodhama icon family — initial identity (provisional)

Open `preview.html` to see the three marks side by side, light and dark.
**Provisional by design**: these are the initial stab; the design-system
pass (plan-suite-lift T2, run with Claude design) reviews, refines, and
finalizes before anything ships on a landing page.

## The family logic

Org: **kodhama** — a play on the *kodama*, the tree spirits of Japanese
folklore (see Miyazaki's *Mononoke Hime*): the quiet watchers of a healthy
forest. kodhama is the forest all three packages live in.

One grammar, three marks, each adding a layer to the same scene:

| Mark | Scene | Reading |
|---|---|---|
| **trellis** (existing) | posts + laths — the bare structure | governance: the frame everything grows along |
| **grove** (new) | the tree trained along the laths: trunk, tiers on the wires, growing tip | the swarm: growth under the frame |
| **wisp** (new) | nodes perched on the laths, edges converging, one lit | observability: the kodama watching — who is working, right now |

## Shared grammar (the rules the design pass will formalize)

- 24×24 viewBox, 1.7 stroke, round caps, `currentColor`.
- **Solid accent = the living/active layer; 0.55 opacity = the structure.**
- The two laths (`M2 9h20 M2 15h20`) are the family constant — present in
  every mark, always as structure (except in trellis's own mark, where the
  structure *is* the subject and the verticals carry the accent).
- Marks must survive 19px (header size); check in `preview.html`.

## Sources

```svg
<!-- grove -->
<svg viewBox="0 0 24 24" fill="none">
  <path d="M2 9h20M2 15h20" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" opacity=".55"/>
  <path d="M12 21V7M12 7C11 6.3 10.6 5.2 10.5 4M12 7C13 6.3 13.4 5.2 13.5 4" stroke="currentColor" stroke-width="1.7" stroke-linecap="round"/>
  <path d="M12 11C9.8 11 8.2 9 5 9M12 11C14.2 11 15.8 9 19 9M12 17C9.8 17 8.2 15 5 15M12 17C14.2 17 15.8 15 19 15" stroke="currentColor" stroke-width="1.7" stroke-linecap="round"/>
</svg>

<!-- runtime viz (in use in ../viz/dashboard.html) -->
<svg viewBox="0 0 24 24" fill="none">
  <path d="M2 9h20M2 15h20" stroke="currentColor" stroke-width="1.7" stroke-linecap="round" opacity=".55"/>
  <path d="M7.5 10.8 10 13.2M16.5 10.8 14 13.2" stroke="currentColor" stroke-width="1.7" stroke-linecap="round"/>
  <circle cx="5.5" cy="9" r="2.1" stroke="currentColor" stroke-width="1.7"/>
  <circle cx="18.5" cy="9" r="2.1" stroke="currentColor" stroke-width="1.7"/>
  <circle cx="12" cy="15" r="2.1" fill="currentColor"/>
</svg>
```

At lift these move to their ONE home: the grammar and all marks to
`kodhama/design-system` (its own repo, git-tag versioned — the DS is a
family asset at org level, consumed by every product incl. trellis).
