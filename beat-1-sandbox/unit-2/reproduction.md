# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

mangreygm

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5901398102

Claiming this issue. I'll set up a local environment first, and if I can get the existing suite running properly, then I'll add some snapshot tests under tests/unit/test_prompt_templates.py that fail when a template's content changes without a corresponding version bump.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5903200672

## User Environment

Windows via WSL (Ubuntu), Python 3.12.3, pytest 9.1.1, installed via `pip install -e ".[dev]` into a `.venv` from a clean clone of my fork at commit `2f4e82f`. No Docker services needed for this test.

## Steps

1. Cloned my fork, created a `.venv`, ran `pip install -e ".[dev]"`.
2. Ran `make test-unit`
3. Edited `rag/generator/prompt_templates.py`, changing the `skills_feedback` section while leaving the `v1` alone, no other changes made.
Exact line featured here.

```diff
-    "skills_feedback": {"v1": """Analyze the skills demonstrated in the provided portfolio context.
+    "skills_feedback": {"v1": """Analyze the skills demonstrated in the provided portfolio context. This is a test edit to trigger the bug.
```

Re-ran with the edit made to `skills_feedback.`

## Output
The overall suite total was unchanged.
```
tests/unit/test_prompt_templates.py::TestPromptTemplates::test_template_snapshot_content_hash PASSED
...
375 passed, 53 xfailed in 67.92s (0:01:07)
```

## Result
Because `test_template_snapshot_content_hash` checks if the hash is 32 characters long and if it is a string, the test will never fail regardless of whether templates are changed, deleted, or even filled with garbage. The test is meant to catch unintended template changes, but the actual code is only written to verify the shape of the hash, not its value.


## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Only one run was executed. From eval-run.txt: agreement: 18/20 scored items (bar: 18/20: PASS)

**Package analysis**

pkg-10. Gold: accept. My rubric's verdict: reject, failing "Behavior matches the issue."

The candidate's repro report on pkg-10 is an honest, detailed "cannot reproduce": they tried
the exact symlink/config layout on Linux + zsh instead of the reporter's macOS + fish, showed
the prompt rendering normally, and explained specifically what differed from the report's
environment (OS, shell, and a note about how PWD resolution likely differs for fish on macOS).
My "Outcome is honestly stated" check is worded to pass exactly this case — it explicitly
names "an evidenced cannot-reproduce" as a pass. But "Behavior matches the issue" only
describes what a successful match looks like ("the artifact shows the same failure mode...").
It has no wording for a good-faith non-reproduction, so it fails by default whenever the bug
wasn't triggered, regardless of how well-documented the attempt was. The two checks disagree
with each other on this category of package, and the required-check-fails-verdict rule lets
the stricter one win.

**Check rationale**

"Behavior matches the issue | The artifacts (output excerpts, logs, screenshots/stack traces)
in the repro report, read against the specific behavior the issue describes | The artifact
shows the same failure mode the issue describes (same error, same symptom, same trigger
conditions) — not a different error, a partial match, or a plausible-looking but adjacent bug
| required"

I wrote this to stop a specific failure mode: a contributor triggers *some* bug, assumes it's
the one in the issue, and reports it as reproduced. Without this check, a plausible-looking
but wrong finding could get posted upstream, wasting a maintainer's time verifying it against
the actual report. Requiring an exact match on error/symptom/trigger conditions makes the
grader check the real thing (does this match?) rather than the write-up's polish.

**Trade-offs**

This check's canary is pkg-10 (and pkg-09, the same failure): gold says accept, my rubric says
reject, and the note names this exact check as the cause. The check buys protection against
false-positive "reproduced" claims, but at the cost of any package where reproduction
genuinely didn't happen — it has no separate path for "no artifact because nothing to show"
versus "no artifact because the attempt was thorough and honest." I did not re-run with --only
after noticing this, since fixing it risks reopening whichever wrong-target packages this
check is correctly catching elsewhere (4/4 in that category) — a canary I'd want to check
before loosening it.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
