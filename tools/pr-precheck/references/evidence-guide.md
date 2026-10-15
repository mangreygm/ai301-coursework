# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Where it lives: in an eval bundle, the Plan context block's stated
scope (in/out) and named files, read against the candidate PR's diff
and commit list; any `## Deviations` note the plan carries. Live, this
is your `plan.md` (including its `## Deviations` section) read against
`git diff main...HEAD` on your branch.

What good looks like: every changed file and every substantive hunk
falls inside the plan's stated boundary, or is named in a deviation
note explaining the addition. The description's own claims about what
changed are judged here too: a description claiming more or less than
the diff delivers is silent drift, not a wording problem, however
well the sentence reads.

## Test evidence (harness category: not-tested)

Where it lives: the candidate PR's Test evidence section, read against
the Plan context block's stated test plan and the issue's own repro
steps. Live, this is your `test_evidence.md` read against your
`plan.md`'s test plan and your Unit 2 repro.

What good looks like: an observable before/after state is named (an
exact error before, an exact correct output after — not "it works
now"), and the repo's own required checks (lint, typecheck, the test
suite) are reported with their actual outcome, including anything that
failed or didn't run (e.g. "no tests ran" for an empty suite is a
legitimate, honestly reported outcome, not evidence of a gap).

## Diff quality (harness category: unreviewable)

Where it lives: the unified diff itself and the commit list.

What good looks like: the fix is visible and isolated; nothing
unrelated rides along. Debris tells: leftover debug print/log
statements, dead or commented-out code, pure formatting/whitespace
churn mixed into a functional change, and drive-by edits to files the
plan never named.

## Standards and comms (harness category: standards-wall)

Where it lives: the repo-facts block's stated PR template sections and
contribution/AI-disclosure policy, read against the candidate PR's
actual description. Live, this is the repo's
`.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`, read
against your `pr_draft.md`.

What good looks like: every section the template requires is filled
with real, PR-specific content (not boilerplate or a copy-pasted
placeholder), the issue is referenced by number, and an AI-use
disclosure is present if the repo's stated policy calls for one.
Whether the description's content matches the diff is plan fidelity,
above — this heading is only about whether the repo's *own stated
asks* were honored at all.