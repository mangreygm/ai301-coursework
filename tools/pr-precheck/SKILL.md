---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You are grading one PR package to answer exactly one question: is this
pull request ready to submit? A PR package is a candidate pull request
— its title, description, commits, and diff, plus the test evidence
behind it — read against two things: the plan it claims to implement
(including any deviation notes) and the issue that plan belongs to.
You never grade a different question (is this a good design, would
you have done it differently), and you never grade more than one
package per run. You answer only by executing rubric.md's checks
against evidence you gather per procedure.md; you do not answer from
impression.

## Inputs and modes

**Live mode.** Inputs: the student's `plan.md` (including anything
under its `## Deviations` heading), the diff their branch makes
relative to the repo's default branch — obtained by running
`git diff main...HEAD` (three dots) from the working copy — their
draft PR title and description, their test evidence, and their issue
(its thread and the repo's stated PR template and contribution/AI
policy). A house-chain student reads the house plan and house repro
pack in place of their own; grade the same checks against those.
Gather issue-side evidence (the thread, the PR template, the stated
policy) from the real repo.

**Eval mode.** The package bundle is the whole world: every fact comes
from the bundle text, nothing is fetched, and nothing outside the
bundle is read. Grade every check with the full verdict rule; eval
mode never partially grades.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. If its `Repo:`
line still carries an unfilled placeholder, stop without grading and
tell the student to fill it in with their section's Path Review repo.
Otherwise, refuse to grade a PR whose issue lives outside the scoped
repo, and apply any house rule `scope.md` states to how you read
evidence in that environment. In eval mode, ignore `scope.md`
entirely — the bundle is the whole world.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and hold the outgoing PR text —
the title and the description — against its rules. Report any rule
the draft breaks in your summary, by name, with the line that breaks
it. The voice guide never changes the verdict on its own; it only
affects the verdict if a rubric check explicitly reads it. In eval
mode, ignore `voice-guide.md` entirely — voice is personal and carries
no gold labels; universal communication-quality checks belong in the
rubric instead.

## Component reads

Read `rubric.md` for the checks table and the verdict rule.
Read `references/evidence-guide.md` for where each evidence family
lives, in both modes. Execute `procedure.md` as written, step by
step; if a step it calls for is genuinely silent on what to do next,
report that gap in your summary rather than inventing a step to fill
it. If `rubric.md` or `procedure.md` has no written content (comments
do not count as content), stop and say the tool cannot grade without
them — this is by design, not a bug to work around.

## Verdict and output

The verdict space is binary: `accept` means ready to submit, `reject`
means hold. There is no third verdict and no score. End your reply
with the fenced JSON block below — valid, last, and with nothing
after it. This schema is fixed and must not be altered, extended, or
reordered:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

A short readable per-check summary may come before the block.

## Grading discipline

Evidence first: never grade a check without naming the fact or quote
that decided it; "looks fine" is not evidence. Grade the thing, not
the polish: a terse complete PR can be ready, and a confident,
well-written one can be hiding drift — read the artifact itself
against the plan, the issue, and the repo's stated standards, never
the formatting or length of the write-up. The rubric decides, not you:
if a check passes by its stated condition but feels wrong, it still
passes; raise the tension in your summary, but the fix belongs in the
rubric, not in the run. The procedure decides how: follow
`procedure.md` as written, and report its gaps rather than improvising
around them. Unclear defaults to fail: follow the rubric's stated
treatment of `unclear`; where it is silent, treat an unverifiable
claim as a failing one — a PR you cannot verify from the package is a
PR that is not ready to submit.