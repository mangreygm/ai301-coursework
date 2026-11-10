# Contribution: Document weapon/tool oversize animation frame sizes

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Jeffrey Eromonsele
**GitHub Username:** mangreygm
**Issue:** https://github.com/LiberatedPixelCup/Universal-LPC-Spritesheet-Character-Generator/issues/167
**Pull Request:** https://github.com/LiberatedPixelCup/Universal-LPC-Spritesheet-Character-Generator/pull/606

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Patched issue-scout's rubric, picked an issue it rejected**

I wrote search-strategy.md (four gh search issues queries traced to my fit profile, plus ranking filters) on top of my existing issue-select rubric, and ran three rounds of scans. The first scan showed two real gaps: no tie-break (337 of ~373 results tied at 0 comments, so the scout graded whatever order the search happened to return) and a rubric check that passed a same-day, 0-star repo on "Repo in active use" purely because it had just tagged v1.0.0; I added a createdAt tie-break and a 30-day minimum repo-age floor. The second scan caught that createdAt wasn't actually in the queries' requested fields despite being sorted on, and that one inactive owner had eaten three of five grading slots, so I added the missing field and a one-per-owner cap. A later direct-grade run on candidates from the Issue Selection site exposed a bigger gap: "Not a duplicate" only checked for an *open* linked PR, so it passed an issue whose work was already merged (in a separate docs repo); I rewrote that check to catch merged PRs and cross-repo references too. I ultimately chose an issue my own rubric rejected (LiberatedPixelCup#167, failed only on "Repo in active use"), since a recent maintainer commit and an explicit maintainer reframing of the issue as docs work were stronger live signals than that check's narrow release/issue-volume conditions capture for a quiet, low-traffic project.

**Unit 6: Wired voice-guard as a hook; patched the scope check**

I consolidated my voice guide into one canonical file read by repro-check,
plan-check, and pr-precheck alike, wrote the Upstream section (claims,
questions, pings), and wired the voice-guard as a Claude Code hook so it
checks every outgoing GitHub comment automatically instead of only when I
remember to invoke a skill. I also patched issue-scout's rubric per the
Unit 6 scope patch, replacing "Scope is bounded" with "scope-feasible,"
which stopped treating open edges as automatic rejections and turned them
into a difficulty note instead — closer to how real issues actually look.
I caught a recurrence of a Markdown formatting bug from Unit 5 (two table
rows merged onto one line) while re-reading the patched rubric and fixed
it again.

**Unit 7: Installed the ship-gate and wrote my first ship-manifest.md**

The ship-gate ran my repo's real checks (lint, type-check, npm ci) and
my pr-precheck against a live branch for the first time, and it
rejected my branch twice before passing: once for an unfilled manifest
template (leftover `<owner/repo>` brackets and a duplicated check row),
and once for real problems my own pr-precheck tool caught — a stray
`CLAUDE.local.md` that had been committed by accident despite being
meant to stay local-only, and a failure count I'd miscounted in my PR
description (3 vs. the actual 5 that npm reported). I also hit the same
Windows `subprocess` PATH bug from earlier units, this time in the
gate's own `claude -p` call, and fixed it the same way: resolving the
binary with `shutil.which` before spawning it. Between the manifest and
the pr-precheck pass, the gate caught real issues in my branch that I
would not have caught just by eyeballing the diff myself.

**Unit 8: PR monitor**

- Installed the monitor, move-forms.md, and playbook-template.md to the
  Windows canonical home (`~/.claude/pr-monitor/`).
- `monitor.py --state` crashed on Windows with a UnicodeDecodeError,
  then a TypeError — its `sh()` subprocess helper was missing
  `encoding="utf-8", errors="replace"`, the same Windows subprocess bug
  from check_voice.py and check_gate.py in earlier units. Fixed by
  adding those arguments; `--state` then ran cleanly and showed PR
  #606's live state.
- Wrote the playbook's Staleness thresholds from real data: checked
  CONTRIBUTING.md (states no explicit wait), then pulled merged PRs
  from outside contributors via `gh pr list`. Had to filter out the
  maintainer (Gaurav0) and dependabot to find real comparisons; the 5
  that qualified ranged from ~7 hours to ~14 days open-to-merge, mostly
  on the fast end. Set the nudge threshold at 3 days, past every fast
  case found.
- A full monitor run hit a second instance of the same bug class: the
  `shutil.which` patch had been added to the `claude -p` subprocess
  call but `import shutil` was never added to the file. Fixed by adding
  the import.
- The full run then worked end-to-end: it picked the review-response
  form (the thread's latest item is a comment), correctly recognized
  that comment was an automated Codex summary rather than human
  feedback, and drafted a wait note instead of inventing a response —
  applying the Staleness threshold with the real timestamps and naming
  the next check date (2026-11-13).

---

## Why I Chose This Issue

I chose this issue even though my own issue-scout rubric rejected it, on
"Repo in active use" — the repo has no tagged releases and a low 90-day
issue-opening rate, the two conditions that check looks for. But the
signals that actually matter for whether a project is alive pointed the
other way: a non-bot commit from the maintainer 13 days before my scan,
and a MEMBER (Gaurav0) actively engaging with this exact issue, reframing
it from a bug report into a documentation task he explicitly wants kept
open for that purpose. A quiet, low-traffic project with an engaged
maintainer is a better bet than my rubric's release-cadence and
issue-volume proxies capture for a project this size.

The task itself is well-bounded: some weapon animations use 128x128 or
192x192 frames instead of the project's default 64x64, and that isn't
documented anywhere exact — the original reporter found it only by chance
in a Reddit thread, and the README mentions oversize frames in passing in
a history section without giving sizes. My job is to find every
non-standard size in the sheet_definitions JSON files and document them
plainly. CONTRIBUTING.md is silent on AI assistance, so I disclosed my use
of Claude Code in the claim comment anyway, following course practice
rather than a repo requirement.

**Toolkit**

- Tool: issue-scout (my search strategy, my rubric), and how I used it
- What it produced: a three-round scan that included LPC#167 among its
  candidates; the final verdict on #167 was REJECT, failing only the
  "Repo in active use" check (no tagged release, low 90-day
  issue-opening rate) — every other check passed.
- Difficulties: the active-use check's two proxies (release cadence,
  issue volume) don't capture a small, quiet repo with an actively
  engaged maintainer — exactly this project's situation. That's a
  structural blind spot in the check's design, not a scan bug; nothing
  here was a tool malfunction.
- What changed: nothing to the tool itself at this point — I logged an
  explicit override instead of loosening the check further, since
  weakening "repo in active use" to admit this one issue would make it
  worse at catching genuinely dead repos for every future scan.

---

## Understanding the Issue

**Problem Description**

Some weapon and tool animations in ULPC render at larger-than-default
frame sizes (128px or 192px instead of the standard 64x64), but no
contributor-facing documentation states which animations these are or
what size each uses. The original reporter (Krim10000) only found this
by chance in a Reddit thread, and the maintainer (Gaurav0) confirmed
it's a real, unaddressed documentation gap rather than a duplicate.

**Expected Behavior**

A contributor or tool user working with the sheet definitions should be
able to look up the exact frame size for any oversize weapon/tool
animation from the docs, without having to read the TypeScript source.

**Current Behavior**

The only place the real pixel values live is `sources/custom-animations.ts`.
README.md's Terminology section mentions that ULPC has "weapons with
oversize animation frames" but gives no sizes and no names. Nothing in
CONTRIBUTING.md, ARCHITECTURE.md, or the contributor-facing
sheet-definition skill doc states the values either.

**Affected Components**

- `README.md` — where the missing documentation needs to be added (the
  actual change in this PR).
- `sources/custom-animations.ts` — the existing source of truth for
  frame sizes; read but not modified.
- `sheet_definitions/weapons/*.json` and `sheet_definitions/tools/*.json`
  — the files that reference these oversize animations via
  `"custom_animation"`; read but not modified.

**Toolkit**

- Tool: Claude Code, used to grep every `custom_animation` reference
  across `sheet_definitions/`, read `sources/custom-animations.ts`, and
  check every existing doc file for prior documentation of the sizes
- What it produced: confirmation that the frame-size data exists only
  in code, with a full list of which animations use it and where
- Difficulties: none — straightforward code-reading once I knew to look
  past `sheet_definitions/` into `sources/`
- What changed: nothing; this matched what the maintainer's comment on
  the issue predicted

---

## Reproduction Process

**Environment Setup**

Repo: LiberatedPixelCup/Universal-LPC-Spritesheet-Character-Generator (own
fork). `package.json` requires Node ^22.19.0 || ^24.0.0 || >=26.0.0.

My machine: Windows 11, Node v22.19.0, npm 10.9.3. `npm ci` completed
cleanly.

**Steps to Reproduce**

1. Searched `sheet_definitions/weapons/` for every file referencing
   `"custom_animation"`. All five weapon subcategories (sword, polearm,
   ranged/bow, blunt, magic) use it — e.g. `weapon_sword_katana.json`
   sets `"custom_animation": "walk_128"` and `"slash_128"` on its
   walk/slash layers.
2. Traced those keys to `sources/custom-animations.ts`, which defines a
   `frameSize` per key, and wrote a short script to pull every
   non-64 `frameSize` out of that file programmatically rather than by
   hand.
3. Observed result: every weapon category ships at least one oversize
   animation — `128` for `tool_rod`, `slash_128`, `backslash_128`,
   `halfslash_128`, `walk_128`, `thrust_128`, `tool_axe`, `tool_hammer`;
   `192` for `thrust_oversize`, `slash_oversize`,
   `slash_reverse_oversize`, `whip_oversize`, `tool_whip` — and none of
   these values appear anywhere in README.md, CONTRIBUTING.md,
   ARCHITECTURE.md, or the contributor-facing sheet-definition skill
   doc. The only place the real numbers live is this TypeScript file,
   confirming the gap is real and exactly matches what Krim10000 and
   Gaurav0 described.

**Reproduction Evidence**

- **Commit showing reproduction:** https://github.com/LiberatedPixelCup/Universal-LPC-Spritesheet-Character-Generator/commit/b561eb1e90c851b135df1c7d95c466079abf537e
- **Screenshots/logs:** 
custom_animation usage counts across sheet_definitions/weapons/ and
sheet_definitions/tools/:
thrust_oversize x20 (192px)
slash_oversize x18 (192px)
walk_128 x12 (128px)
slash_128 x8 (128px)
slash_reverse_oversize x5 (192px)
halfslash_128 x2 (128px)
backslash_128 x2 (128px)
- **My findings:** The frame-size information Krim10000 asked for
  already exists in code (`sources/custom-animations.ts`), it's just
  never surfaced anywhere a contributor or tool-user would read it.
  README.md's Terminology section gestures at "oversize animation
  frames" without giving pixel values. This is a pure documentation
  gap, not a bug — there's nothing to fix in the generator itself, only
  something to add in docs.

**Toolkit**

- Tool: Claude Code, used to search the cloned repo for every
  `custom_animation` reference, read `sources/custom-animations.ts`,
  and check every doc file for existing size documentation
- What it produced: a confirmed list of every non-default frame size
  and where each is used, and confirmation that no existing doc states
  them
- Difficulties: none — this was a straightforward code-reading task
  once I knew to look past `sheet_definitions/` into `sources/`
- What changed: none; this matched what the maintainer's comment
  predicted

---

## Solution Approach

**Analysis**

The cause isn't a bug — it's a documentation gap. The frame-size data
Krim10000 needed already exists in code: `sources/custom-animations.ts`
defines a `frameSize` per custom animation key (128px for `tool_rod`,
`slash_128`, `backslash_128`, `halfslash_128`, `walk_128`, `thrust_128`,
`tool_axe`, `tool_hammer`; 192px for `thrust_oversize`, `slash_oversize`,
`slash_reverse_oversize`, `whip_oversize`, `tool_whip`), and every weapon
category's `sheet_definitions/weapons/*.json` references one of these
keys via `"custom_animation"`. But no contributor-facing doc states the
exact sizes — README.md's Terminology section only says ULPC added
"weapons with oversize animation frames," with no pixel values.

**Proposed Solution**

Add a table to README.md's Terminology section listing every custom
animation name and its frame size, sourced directly from
`sources/custom-animations.ts`, so a tool user cutting sheets at the
default 64x64 can see up front which animations need 128 or 192
instead. I am deliberately NOT changing any code — `custom-animations.ts`
is correct and doesn't need touching, and I'm not modifying any
`sheet_definitions/` JSON, since those already reference the right
keys.

**Implementation Plan**

1. Add a short table to README.md's Terminology section (near the
   existing "oversize animation frames" sentence) listing each
   non-default custom animation name and its frame size in px.
2. No tests to add — this is a documentation-only change; `npm run
   test:node` and `npm run lint`/`type-check` confirm nothing broke.
3. Keep the extraction script (`scripts/debug/list-oversize-animations.ts`)
   out of the PR diff, or decide whether to keep it as a small dev
   utility — default is to drop it since nothing in CONTRIBUTING.md
   asks for one; it was reproduction scaffolding, not part of the fix.

**Toolkit**

- Tool: the ship-gate (Unit 7)
- What it produced: a manifest-driven pre-flight that ran the repo's
  own checks (npm ci, lint, type-check) then my pr-precheck against
  the real branch, diff, plan, and test evidence, and blocked the PR
  three separate times before it would pass
- Difficulties: my first manifest still had the `<owner/repo>`
  placeholder brackets and a duplicate "Node unit tests" row in both
  the must-pass and excluded tables; `pr_draft.md` and `test_evidence.md`
  both got created with hidden `.txt` extensions on Windows the first
  time; `claude -p` wasn't resolvable from the gate's `subprocess.run`
  call until I patched it with `shutil.which("claude")`, the same
  Windows PATH issue from earlier units; and my own pr-precheck caught
  a real arithmetic slip (I'd said "3 failures" when npm's own output
  said 5) and caught that `CLAUDE.local.md`, meant to stay local-only,
  had been swept into a commit
- What changed: fixed the manifest's placeholder and duplicate row,
  renamed the hidden-extension files, patched `check_gate.py` and
  `check_voice.py` with `shutil.which`, corrected the failure count
  everywhere it appeared, removed `CLAUDE.local.md` from tracking and
  squashed the branch down to one clean commit before pushing

---

## Testing Strategy

**Diff check:** `git diff --stat` against `master` shows exactly one
file touched — `README.md`, a 21-line addition under the Terminology
section (the new "Oversize animation frame sizes" table). No other
file in the branch is changed.

**Repo's own checks, run on the branch:**
- `npm run lint` — clean.
- `npm run type-check` — clean.
- `npm run test:node` — 5 failures (4 Windows path-separator/EPERM-symlink
  failures in `link-agent-skills_spec.ts`, 1 openssl-dependent TLS
  failure in `cls-profile_spec.ts`). Re-ran the same command against a
  clean checkout of `master` with no branch changes: same 5 failures,
  same files, same count. This confirms none of them are caused by this
  change — they're pre-existing environment issues unrelated to a
  README edit.

Together these show the change is exactly what it claims to be (one
doc addition, nothing else touched) and that it introduces no new
failures anywhere in the repo's own test suite.

**Toolkit**

- Tool: the repo's own npm scripts (lint, type-check, test:node), run
  directly, plus `git diff --stat` for the diff check
- What it produced: a clean lint/type-check result and a confirmed,
  pre-existing (not caused by this PR) 5-failure baseline for test:node
- Difficulties: initially miscounted the test:node failures as 4 instead
  of 5 when writing this up the first time; caught by my own
  pr-precheck tool flagging the inconsistency against npm's own output
- What changed: corrected the failure count everywhere it appears in
  this story and in the PR description

---

## Implementation Notes

**2026-11-09**

Built `test_evidence.md` and `pr_draft.md`, then ran the ship-gate for
the first time. It rejected the branch twice before passing: once for
a templated `ship-manifest.md` (leftover `<owner/repo>` brackets, a
duplicate check row), and once for real problems its `pr-precheck`
caught — a stray `CLAUDE.local.md` committed by accident, and a
test-failure count I'd gotten wrong (said 4, npm's own output said 5).
Fixed both, squashed the branch to one clean commit with
`git reset --soft master`, and force-pushed with `--force-with-lease`
since it had already been pushed once before the squash.

**2026-11-10**

Opened PR #606. Installed the Unit 8 PR monitor and hit the same
Windows subprocess bug class twice more: `--state` crashed on a missing
`encoding="utf-8"` in the `sh()` helper, then a full run crashed on a
missing `import shutil` even though the `shutil.which` call itself had
already been patched in. Fixed both, wrote the playbook's Staleness
thresholds from real merged-PR data (filtering out the maintainer and
dependabot), and ran the monitor end-to-end — it correctly told the
two bot comments on the thread apart from real human feedback and
drafted a wait note instead of inventing a response.

**Toolkit**

- Tool: the ship-gate and the PR monitor (Units 7-8)
- What it produced: a working log of every real stop each tool made
  and what each one caught
- Difficulties: the same Windows subprocess bug (missing PATH
  resolution, missing encoding) recurred across three separate scripts
  before I started checking for it proactively
- What changed: patched all three scripts the same way once the
  pattern was clear, instead of treating each as a one-off

---

## Pull Request

**PR Link:** https://github.com/LiberatedPixelCup/Universal-LPC-Spritesheet-Character-Generator/pull/606

**PR Description:** Adds an "Oversize animation frame sizes" subsection to README.md's
Terminology section, listing every weapon/tool custom animation that
uses a non-default frame size (128px or 192px instead of the standard
64x64), with the exact pixel value for each, sourced from
`sources/custom-animations.ts`. No code changes. Fixes #167.

**Maintainer Feedback:**

2026-11-10: none yet — the only activity so far is an automated Netlify
deploy-preview notice and a Codex bot review that found nothing to flag.
No human has reviewed it.

**Status:** Awaiting Review

**Toolkit**

- Tool: the ship-gate (Unit 7)
- What it produced: a manifest-driven pre-flight that ran the repo's
  own checks (npm ci, lint, type-check) then my pr-precheck against
  the real branch, diff, plan, and test evidence, and blocked the PR
  three separate times before it would pass
- Difficulties: my first manifest still had the `<owner/repo>`
  placeholder brackets and a duplicate "Node unit tests" row in both
  the must-pass and excluded tables; `pr_draft.md` and `test_evidence.md`
  both got created with hidden `.txt` extensions on Windows the first
  time; `claude -p` wasn't resolvable from the gate's `subprocess.run`
  call until I patched it with `shutil.which("claude")`, the same
  Windows PATH issue from earlier units; and my own pr-precheck caught
  a real arithmetic slip (I'd said "3 failures" when npm's own output
  said 5) and caught that `CLAUDE.local.md`, meant to stay local-only,
  had been swept into a commit
- What changed: fixed the manifest's placeholder and duplicate row,
  renamed the hidden-extension files, patched `check_gate.py` and
  `check_voice.py` with `shutil.which`, corrected the failure count
  everywhere it appeared, removed `CLAUDE.local.md` from tracking and
  squashed the branch down to one clean commit before pushing

---

## Learnings and Reflections

**Technical Skills Gained**

- Diagnosing Windows-specific Python `subprocess` failures (PATH
  resolution via `shutil.which`, encoding crashes from `cp1252` vs
  `utf-8`) and recognizing the same bug class on sight by the third
  occurrence.
- Reading GitHub PR/CI state through `gh` (checks, review decision,
  comment threads) well enough to tell automated bot activity apart
  from real maintainer feedback.
- Squashing a branch's history with `git reset --soft` plus a clean
  recommit, and safely force-pushing with `--force-with-lease` after a
  prior push.
- Writing grading rules (a rubric check, a staleness threshold) from
  real project data instead of guessing a plausible-sounding number.

**Challenges Overcome**

- My own `pr-precheck` tool caught two real mistakes in my branch
  before I shipped it: an accidentally-committed local-only file, and
  an arithmetic error in my own PR description. Both were genuine
  gaps, not the tool being pedantic, and I'd have shipped both if the
  gate hadn't stopped me.
- Chose an issue my own issue-scout rubric rejected, and had to make a
  real, logged case for why the override was correct rather than just
  picking a more convenient issue.

**What I'd Do Differently Next Time**

I'd check every staff-provided script for the Windows subprocess bug up
front, across all three (`check_voice.py`, `check_gate.py`,
`monitor.py`), instead of discovering it fresh in each one. I'd also
add `.git/info/exclude` entries for local-only working files (like
`CLAUDE.local.md`) the moment they're created, rather than after one
gets swept into a commit by accident.

---

## Resources Used

- [Issue #167](https://github.com/LiberatedPixelCup/Universal-LPC-Spritesheet-Character-Generator/issues/167) — the maintainer's own reframing comment is what told me this was real, wanted documentation work, not a rejected bug report.
- [CONTRIBUTING.md](https://github.com/LiberatedPixelCup/Universal-LPC-Spritesheet-Character-Generator/blob/master/CONTRIBUTING.md) — confirmed the repo's real CI checks and said nothing about AI-assistance disclosure or PR wait times, which shaped both the ship-manifest and the playbook.
- `sources/custom-animations.ts` and `AGENTS.md`/the sheet-definition skill doc in the repo itself — confirmed this file is the actual source of truth for frame sizes and that no contributor doc restates it.
