# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

Where it lives: in an eval bundle, the plan's "Diagnosis" or "Cause" subsection states what's wrong; the "Repro evidence" section pins down the specific observed behavior, including any step that identifies an exact failure point (a debug trace, a specific function or file, a specific log line). Live, this is the student's `plan.md` Diagnosis section read against their own posted Unit 2 repro comment (or the house repro pack).

What good looks like: the stated cause explains every behavior the repro evidence shows, including its most specific evidence (if the repro evidence names an exact stack frame or call path, the diagnosis must be consistent with that exact point, not just generally plausible). A diagnosis that dismisses a specific piece of repro evidence without explaining why that evidence doesn't actually contradict the stated cause does not meet this bar.

## Scope

Where it lives: the plan's "Scope" (in/out) subsection and its "Files" subsection.

What good looks like: explicit in-scope and not-in-scope lines; named files or areas, not vague references; a scope no larger than what the diagnosed cause requires — not a broader refactor of adjacent, unaffected code.

## Executability

Where it lives: the plan's "Approach" subsection (its ordered steps) and "Files" subsection.

What good looks like: steps name specific files, functions, or mechanisms, in an order someone who has not read the diagnosis's reasoning could follow without asking the author a clarifying question. "Fix the parsing issue" is not executable; "extend the item-separator regex in requestitems.py to accept tokens following a flag" is.

## Test plan

Where it lives: the plan's "Test plan" or "Test" subsection, read against the Repro evidence's exact steps, commands, and outputs.

What good looks like: the test plan re-runs or directly extends the repro evidence's actual steps (not a generic "add tests") and states a specific, observable result expected after the fix — an exact output, exit code, or rendered state — matching the repro evidence's own level of specificity.

## Honesty

Where it lives: a Risks/Unknowns subsection if the plan has one; also any strongly stated claim within Diagnosis or Scope that dismisses an alternative explanation.

What good looks like: real uncertainty (untested environments, unverified assumptions, edge cases the test plan doesn't cover) is named as uncertain rather than folded into the diagnosis as settled fact. A claim that something is definitely not the cause, or definitely will fix the issue, made without evidence supporting that certainty, is overconfidence rather than honesty.

## Comms

Where it lives: the "Candidate plan comment" section, read against the Thread highlights and the Repo facts' stated contribution policy, AI-disclosure requirement, and any issue-comment template.

What good looks like: the comment is specific to this issue rather than boilerplate, follows any disclosure or template requirement the repo states, addresses points other commenters actually raised (an alternate theory, a conflicting test result) instead of ignoring them, and makes no calendar-bound delivery promise (a specific date, day, or duration like ‘by Friday,’ ‘within a week,’ or ‘tomorrow’). Describing what happens next in sequence — ‘once the tests pass,’ ‘after the fix lands’ — is normal plan language, not a timeline promise.