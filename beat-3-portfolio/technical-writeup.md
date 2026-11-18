# Documenting ULPC's hidden oversize animation frame sizes

## Overview

The Universal LPC Spritesheet Character Generator (ULPC) is an
open-source tool for generating game character sprite sheets. Most
animations render at a default 64x64 frame, but a handful of weapon
and tool animations actually use larger frames — 128px or 192px — and
that fact lived only in the project's source code, never in its
documentation. A user had reported this as confusing (he'd only found
it by chance in a Reddit thread), and the maintainer confirmed it was
a real gap, not a duplicate. I traced every non-default frame size
back to its source, added a table to the README documenting all of
them, and opened pull request #606 against the project. The
maintainer merged it on November 11, 2026.

## What happened

I found this issue through my own issue-selection tooling, which had
actually rejected it — it failed my "repo in active use" check because
the project has no tagged releases and a low rate of new issues. I
overrode that rejection myself: a recent non-bot commit from the
maintainer, and the maintainer actively re-engaging with this specific
issue to reframe it as documentation work, were stronger signs of life
than my check's release/issue-volume proxies could capture for a
small, quiet project.

Once I claimed the issue, I had to find every place the gap actually
showed up. I grepped `sheet_definitions/weapons/*.json` for every
`"custom_animation"` reference, then traced those keys back to
`sources/custom-animations.ts`, which defines a `frameSize` per key.
That confirmed 13 animations use non-default sizes — 8 at 128px, 5 at
192px — and that none of this appeared in README.md, CONTRIBUTING.md,
or any other contributor-facing doc:

```
thrust_oversize  x20  (192px)
slash_oversize   x18  (192px)
walk_128         x12  (128px)
slash_128        x8   (128px)
slash_reverse_oversize x5 (192px)
halfslash_128    x2   (128px)
backslash_128    x2   (128px)
+ 4 more tool-specific keys
```

I added a single table to README.md's Terminology section listing
every one of those 13 animations and its exact size, sourced directly
from the TypeScript file — no code changed.

Before I opened the PR, I ran it through a personal pre-flight tool I'd
built over the term, which runs the repo's own checks plus a review of
my branch, diff, and PR description against each other. It caught two
real problems I would have shipped otherwise: a `CLAUDE.local.md`
working file that had been committed by accident, and a wrong number
in my own PR description. I had written that `npm run test:node` had 3
pre-existing failures unrelated to my change; the tool flagged that my
own evidence contradicted that:

```
npm test:node output:  # fail 5
My PR description:      "3 pre-existing failures"
```

The actual count was 5 (4 Windows path-separator/symlink failures in
`link-agent-skills_spec.ts`, 1 openssl-dependent failure in
`cls-profile_spec.ts`), confirmed identical on a clean checkout of
`main`. I corrected the number everywhere it appeared, removed the
stray file from the branch, squashed the cleanup into one commit, and
re-ran my pre-flight tool until it passed cleanly.

I opened PR #606 with an inline before/after summary and the corrected
test evidence in the description itself, rather than pointing to a
local file a reviewer couldn't see. The maintainer merged it on
November 11, 2026, closing the original issue.

## Limitations and what's next

My change documents the current 13 oversize animations, but nothing
keeps that table in sync going forward — if someone adds a new custom
animation with a non-default `frameSize` to `custom-animations.ts`,
the README won't automatically reflect it, and the gap I just fixed
could quietly reopen. A natural next step would be a small script or
lint check that reads `custom-animations.ts` directly and fails CI if
the README table doesn't match it, so the documentation can't drift
from the source of truth again.