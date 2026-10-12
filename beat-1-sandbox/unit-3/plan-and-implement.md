# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

mangreygm

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-6116831265
---

## Your branch

**Branch**

fix/12-snapshot-hash-per-version

**Evidence**

Before (Unit 2 repro, bug present):
tests/unit/test_prompt_templates.py::TestPromptTemplates::test_template_snapshot_content_hash PASSED
...
375 passed, 53 xfailed in 67.92s (0:01:07)

After (same edit, fix built):
tests/unit/test_prompt_templates.py::TestPromptTemplates::test_template_snapshot_content_hash FAILED
AssertionError: Content for (skills_feedback, v1) changed without a
version bump — hash mismatch.
assert 'f2147765625b...bb1fa8b0d7d3d' == 'f93103d82348...ecc6653e4ee5c'

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Only one run was executed. From eval-run.txt: agreement: 19/20 scored items (bar: 18/20: PASS)

**Package analysis**

pkg-14 (category: clear-accept). Gold: accept. My rubric's verdict:
reject, failing "Plan is executable by a stranger."

The plan's Files section states: "exact functions to be pinned in the
PR after tracing the query issuance with debug logs, which I have
working." By the letter of my pass condition — naming specific
functions so a stranger could start without asking a clarifying
question — this fails, since the function names aren't pinned yet.
But the author isn't vague: they already have working debug
instrumentation that shows where the leak originates, so the real
starting point (run the existing debug tooling, trace from there) is
concrete even without the function name pre-filled. My check reads
"names a function" literally, rather than treating "names a concrete,
already-working method for finding the function" as equivalent. That
gap is why my rubric rejects a plan the gold label accepts.

**Check rationale**

"Plan is executable by a stranger | The plan's Approach steps and
Files section | The approach lists concrete, ordered steps naming
specific files, functions, or mechanisms, such that someone who has
not read the author's reasoning could start executing without asking
a clarifying question. A step that names an outcome but not a
mechanism or location ("fix the parsing issue") fails this check |
required"

I wrote this to stop a specific failure mode: a plan that describes
*what* should happen ("fix the bug") without saying *where* or *how*,
leaving a stranger unable to start without asking the author a
question first. Requiring named files/functions/mechanisms, rather
than accepting a general sense of the right area, makes the grader
check the real thing — can execution actually begin — rather than
how confident or detailed the writing sounds.


**Trade-offs**

This check's canary is pkg-14 itself: gold says accept, my rubric
says reject, and the note names this exact check as the cause. I
chose not to loosen the wording, since every other plan-check package
(including three "unbuildable" category packages, 3/3 matched) relies
on this check correctly rejecting plans that gesture at "fix it
somewhere" without any concrete starting point. Loosening the
condition to accept "I have a method but not the location yet" risks
also accepting genuinely vague plans that falsely claim to have a
method in hand. I accepted this one miss rather than risk that
regression — pkg-14 is a known, understood limitation, not an
oversight.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
