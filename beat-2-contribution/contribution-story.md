# Contribution: [Issue Title]

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** [Jeffrey Eromonsele]
**GitHub Username:** [mangreygm]
**Issue:** [https://github.com/LiberatedPixelCup/Universal-LPC-Spritesheet-Character-Generator/issues/167]
**Pull Request:** [GitHub PR link, once opened]

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

**Unit 5: [one line on the tool work]**

I wrote search-strategy.md (four gh search issues queries traced to my fit profile, plus ranking filters) on top of my existing issue-select rubric, and ran three rounds of scans. The first scan showed two real gaps: no tie-break (337 of ~373 results tied at 0 comments, so the scout graded whatever order the search happened to return) and a rubric check that passed a same-day, 0-star repo on "Repo in active use" purely because it had just tagged v1.0.0; I added a createdAt tie-break and a 30-day minimum repo-age floor. The second scan caught that createdAt wasn't actually in the queries' requested fields despite being sorted on, and that one inactive owner had eaten three of five grading slots, so I added the missing field and a one-per-owner cap. A later direct-grade run on candidates from the Issue Selection site exposed a bigger gap: "Not a duplicate" only checked for an *open* linked PR, so it passed an issue whose work was already merged (in a separate docs repo); I rewrote that check to catch merged PRs and cross-repo references too. I ultimately chose an issue my own rubric rejected (LiberatedPixelCup#167, failed only on "Repo in active use"), since a recent maintainer commit and an explicit maintainer reframing of the issue as docs work were stronger live signals than that check's narrow release/issue-volume conditions capture for a quiet, low-traffic project.

**Unit 6: [one line on the tool work]**

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

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

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

- Tool: issue-scout (your scout: your search strategy, your rubric),
  and how you used it
- What it produced: [the scan and its verdict on this issue, described]
- Difficulties: [where it fell short, or "none met" if none did]
- What changed: [what you patched or would update, or "nothing"]

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
