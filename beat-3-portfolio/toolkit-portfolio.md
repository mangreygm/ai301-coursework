# Toolkit Portfolio

**Student:** Jeffrey Eromonsele

## Featured Tools

I'm featuring issue-scout, voice-guard, ship-gate, and pr-monitor. The
first and third show the clearest arc — each one caught something real
and got rewritten because of it. The other two round out the story:
voice-guard is honest "it mostly just worked" middle-tier, and
pr-monitor ties the whole toolkit together at the end of the term by
reading the result of everything that came before it.

**issue-scout**

**What it is, and the judgment hole I wrote:** A Claude Code skill
that searches GitHub issues (`gh search issues`) and grades candidates
against a fit rubric I wrote myself, plus a search strategy of four
tuned queries. I used it to pick my beat-2 contribution.

**How it evolved, dated:**
- October 2026 (Unit 5, round 1): My first scan showed 337 of ~373
  results tied at 0 comments, with no tie-break — the scout was really
  just grading whatever order the GitHub search API happened to
  return. I added a `createdAt` tie-break and a 30-day minimum
  repo-age floor.
- October 2026 (Unit 5, round 2): The fixed rubric still had a bug —
  `createdAt` wasn't actually in the queries' requested fields despite
  being sorted on, and one inactive repo owner had eaten three of five
  grading slots. I added the missing field and a one-per-owner cap.
- October 2026 (Unit 5, round 3): A direct-grade run exposed a bigger
  gap — "Not a duplicate" only checked for an *open* linked PR, so it
  passed an issue whose fix was already merged in a separate docs
  repo. I rewrote the check to catch merged PRs and cross-repo
  references too.
- Early November 2026 (Unit 6): Patched "Scope is bounded" to
  "scope-feasible," so an issue with an open edge gets a logged
  difficulty note instead of an automatic rejection.

**Evidence:** My final scan rejected the issue I ultimately chose,
LiberatedPixelCup#167, on exactly one check — "Repo in active use"
(no tagged release, low 90-day issue rate). Every other check passed.
I overrode that rejection by hand rather than loosen the check itself,
since a maintainer's non-bot commit 13 days before my scan, and the
maintainer actively re-engaging with this exact issue, were stronger
live signals than the check's release/issue-volume proxies capture for
a small, quiet repo. The override is logged in my contribution story,
not silently absorbed into the rubric.

**voice-guard**

**What it is, and the judgment hole I wrote:** A PreToolUse hook that
checks every outgoing `gh issue/pr comment/create` body against a
canonical `voice-guide.md` before letting the command run, via a
Sonnet subprocess call. The judgment hole is the guide itself — my
Upstream section on claims, questions, and pings.

**How it evolved, dated:** Early November 2026 (Unit 6): consolidated
several drifting copies of the voice guide into one canonical file
read by `repro-check`, `plan-check`, and `pr-precheck` alike, and wired
it in as a hook so it runs automatically instead of only when I
remember to invoke it. Past that, it's barely changed — it's done one
job reliably rather than needing repeated rewrites.

**Evidence:** In Unit 7, the guard flagged that my PR draft and test
evidence never stated my own environment, against a rule I'd written
that says to "state my environment even when nobody asked." I added
"Windows 11, Node v22.19.0, npm 10.9.3" to both files because of that
one flag — a small catch, but a real one.

**ship-gate**

**What it is, and the judgment hole I wrote:** A PreToolUse hook that
runs a repo's real checks (from a `ship-manifest.md` I write per
project) plus my `pr-precheck` skill against a live branch, before
letting `gh pr create` through. The judgment hole is the manifest's
Must-pass/Excluded tables and `pr-precheck`'s own rubric.

**How it evolved, dated:** November 9, 2026 (Unit 7): my first real
run against the LPC repo rejected the branch twice. First, for a
templated manifest — leftover `<owner/repo>` brackets and a duplicate
check row, both fixed by hand. Second, for real problems:
`pr-precheck` caught a `CLAUDE.local.md` file I'd committed by
accident, and a test-failure count I'd gotten wrong in my own PR
description.

**Evidence:**

npm test:node output: # fail 5
My PR description said: “3 pre-existing failures”

I'd claimed 3; npm's own output said 5 (4 Windows path-separator
failures plus 1 openssl-dependent failure). I corrected the number
everywhere it appeared, removed `CLAUDE.local.md` from tracking,
squashed the branch's history, and re-ran the gate until it passed
clean — before any human reviewer ever saw either problem.

**pr-monitor**

**What it is, and the judgment hole I wrote:** Reads a real PR's live
state (checks, review decision, comments) and drafts the next move —
a review response, a nudge, a rebase plan, a merged follow-up —
against a `playbook.md` I wrote from real data. It never posts
anything itself.

**How it evolved, dated:** November 10, 2026 (Unit 8): `--state`
crashed on Windows with a `UnicodeDecodeError`, then a `TypeError` —
its subprocess helper was missing `encoding="utf-8"`. Fixed that, then
a full run crashed separately on a missing `import shutil`, even
though the PATH-resolution fix itself had already been patched in.
Fixed that too.

**Evidence:** Once both bugs were fixed, a full run correctly told two
automated bot comments (a Netlify deploy notice, a Codex review
summary) apart from real human feedback, and drafted a wait note
instead of inventing a response:

state: FEEDBACK-IN: review feedback is in (latest from the thread:
comment under a day ago)
drafted move: “No response to send. The thread has no human review
feedback, so this is a wait note.”

The playbook's own Staleness threshold (3 days, set from 5 real
merged-PR wait times in the repo ranging ~7 hours to ~14 days) never
actually got tested against a real wait — PR #606 merged on November
11, 2026, before 3 days of quiet ever passed.

## Inventory

- **repro-check:** verified my reproduction evidence (environment,
  steps, commit reference) against the real repo before I wrote up the
  contribution; used once, no revisions needed.
- **plan-check:** graded my Solution Approach and Implementation Plan
  draft before I built anything; used to sanity-check scope, never
  posted to the issue thread directly.

## The Arc

**Beat 1**
Date: October 2026 (Unit 5)
Friction: My first issue-scout scan showed 337 of ~373 results tied at
0 comments — no tie-break, so the scout graded whatever order the
search API happened to return.
Change: Added a `createdAt` tie-break and a 30-day minimum repo-age
floor to the rubric.
Result: The next scan, run against the fixed rubric, immediately
surfaced a second real bug (Beat 2) instead of running clean.

**Beat 2**
Date: October 2026 (Unit 5)
Friction: A direct-grade run showed "Not a duplicate" only checked for
an *open* linked PR, so it passed an issue whose work was already
merged in a separate docs repo.
Change: Rewrote the check to catch merged PRs and cross-repo
references too.
Result: none — I moved on to issue selection before running a full
scan against the rewritten check.

**Beat 3**
Date: Early November 2026 (Unit 6)
Friction: The "Scope is bounded" check treated any open edge in an
issue as an automatic rejection, which doesn't match how real issues
read.
Change: Replaced it with "scope-feasible," turning an open edge into a
logged difficulty note instead of a rejection.
Result: none directly measured — I didn't re-score prior candidates
against the new version.

**Beat 4**
Date: November 9, 2026 (Unit 7)
Friction: My first real ship-gate run against the LPC repo rejected my
branch for an accidentally-committed `CLAUDE.local.md` and a
miscounted test-failure number in my own PR description (claimed 3,
npm reported 5).
Change: Removed the stray file, corrected the count everywhere it
appeared, and squashed the branch to one clean commit.
Result: The gate passed clean, and PR #606 shipped without a reviewer
ever seeing either problem.

**Beat 5**
Date: November 10, 2026 (Unit 8)
Friction: `monitor.py --state` crashed on Windows with a
`UnicodeDecodeError`/`TypeError`; a full run then crashed separately on
a missing `import shutil`, even after the PATH-resolution fix had
already been applied elsewhere in the file.
Change: Added `encoding="utf-8", errors="replace"` to the subprocess
helper, then added the missing import.
Result: Both runs then worked end-to-end — `--state` showed PR #606's
live state, and a full run correctly told bot comments apart from real
feedback and drafted an honest wait note.

**Beat 6**
Date: November 10-11, 2026 (Unit 8)
Friction: My playbook's Staleness thresholds needed a real number, and
CONTRIBUTING.md stated no explicit wait time to start from.
Change: Pulled 60 merged PRs from the repo, filtered out the
maintainer and dependabot, and set a 3-day nudge threshold from 5 real
outside-contributor wait times (~7 hours to ~14 days).
Result: PR #606 merged on November 11, 2026 — before 3 days of quiet
ever passed, so the threshold was never actually needed for this PR,
but it's in place for the next one.

## Limitations and What's Next

Most of my toolkit's judgment is still hand-tuned per situation rather
than generalized. issue-scout's override of "Repo in active use" was a
one-off manual call, not a rule the rubric itself learned — a future
quiet-but-alive repo would hit the same rejection and need the same
manual override again. ship-gate's manifest has to be rewritten by
hand for every new repo, and nothing checks whether an "excluded, with
a dated reason" check has gone stale. pr-monitor's playbook was tuned
from a 5-PR sample on one repo, which is a thin basis for a threshold
I'd trust on a busier project. Next, I'd want to feed issue-scout's
override reasoning back into the rubric as a named, repeatable
exception path instead of an ad hoc comment, and build a small
drift-check — raised in my technical write-up too — that keeps
documentation and source in sync automatically rather than relying on
me to notice by hand next time.

**Tool limits.**

issue-scout: still can't tell a genuinely dead repo from a quiet one
with an engaged maintainer without a manual override — that judgment
isn't written into the rubric itself.
voice-guard: only checks commands run through Claude Code
(`gh ... comment/create`); a reply posted directly through the GitHub
web UI would bypass it entirely.
ship-gate: the Excluded-checks table is hand-maintained per repo and
per PR; nothing flags when an excluded check's "doesn't count against
this PR" reasoning has gone stale on a later branch.
pr-monitor: the playbook's Staleness thresholds come from a 5-PR
sample on one quiet repo; it has no way to tell when that sample is
too small to trust on a different, busier project.
