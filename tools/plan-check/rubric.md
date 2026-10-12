# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis grounded in repro evidence | The plan's stated cause, read against every behavior and specific failure point shown in the repro-evidence block | The stated cause is consistent with every behavior the repro evidence shows. If the repro evidence identifies an exact failure point (a specific function, debug trace, stack frame, or log line), the diagnosis must account for that specific point, not merely be plausible in general. A diagnosis that dismisses evidence pointing elsewhere (calling it a "red herring" or similar) without explaining why that evidence doesn't actually contradict the stated cause fails this check | required |
| Scope is bounded | The plan's Scope (in/out) statement and the files it names | The plan states explicit in-scope and not-in-scope boundaries, names specific files or areas (not "various files" or unnamed areas), and the named change is no larger than what the diagnosed cause requires — not a broader rewrite of adjacent, unaffected code | required |
| Plan is executable by a stranger | The plan's Approach steps and Files section | The approach lists concrete, ordered steps naming specific files, functions, or mechanisms, such that someone who has not read the author's reasoning could start executing without asking a clarifying question. A step that names an outcome but not a mechanism or location ("fix the parsing issue") fails this check | required |
| Test plan is decisive | The plan's Test section, read against the repro evidence's exact steps | The test plan re-runs or directly extends the repro evidence's actual steps and states a specific, observable expected result after the fix (an exact output, exit code, or rendered state) — not a generic "verify it works" | required |
| Uncertainty stated honestly | Any Risks/Unknowns content in the plan, and any claim in the Diagnosis or Scope that dismisses an alternative explanation | Genuine uncertainty (untested environments, unverified assumptions, edge cases outside the test plan) is named as uncertain. A claim that something is definitely not the cause, or definitely will fix the issue, stated without evidence supporting that certainty, fails this check | required |
| Comment respects thread and repo conventions | The plan comment's text, read against the repo-facts block's contribution policy/AI-disclosure requirement and the issue's thread highlights | The comment is specific to this issue, follows any disclosure or template requirement the repo states, addresses relevant points other commenters raised rather than ignoring them, and makes no calendar-bound delivery promise (a specific date, day, or duration like ‘by Friday,’ ‘within a week,’ or ‘tomorrow’). Describing what happens next in sequence — ‘once the tests pass,’ ‘after the fix lands’ — is normal plan language, not a timeline promise | required |
| Comment is specific, not padded | The plan comment's prose itself | The comment states what was actually found and planned in terms specific to this issue; it is not boilerplate that could be pasted into any issue's thread unchanged | preferred |

## Verdict rule

Accept (ready to post and build from) only if every `required` check passes. Any `required` check graded `fail` or `unclear` holds the package (reject) — `unclear` on a required check is treated as a fail, not a pass. `preferred` checks are recorded but never change the verdict.
