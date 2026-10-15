# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diff matches the plan's scope | The diff's changed files and hunks, read against the plan's stated scope (in/out) and any `## Deviations` note | Every changed file and every substantive hunk falls inside the plan's stated scope, or is explicitly named in a `## Deviations` note explaining why it was added. A file or change outside both is silent drift and fails this check | required |
| Description matches the diff | The PR description's claims about what changed, read against the actual diff | The description claims neither more nor less than the diff delivers. A description that says a change was made but the diff doesn't show it, or vice versa, fails this check regardless of how well-written the description is | required |
| Test evidence is decisive | The PR's test-evidence section, read against the plan's test plan and the issue's original repro steps | The evidence shows an observable before/after (the plan's repro steps re-run, with a concrete before and after state, not just "tests pass") and reports the repo's own required checks (lint, typecheck, test suite) with their actual outcome, including any that failed | required |
| Diff is reviewable | The unified diff and the commit list | The diff contains only the change the plan describes: no debug leftovers, no commented-out code, no unrelated drive-by edits, no formatting-only churn mixed into the functional change. A diff where the real fix is buried under unrelated hunks fails this check even if the fix itself is correct | required |
| Repo's stated standards are met | The repo-facts block's PR template sections and stated contribution/AI-disclosure policy, read against the PR description | Every section the repo's PR template requires is filled with real content specific to this PR (not boilerplate), the issue is referenced (e.g. "Closes #N"), and an AI-use disclosure is present if the repo's policy asks for one. A required template section left blank or generic fails this check | required |
| Honest shortfall is not penalized | The PR description and `plan.md`'s `## Deviations` section, read against the diff and test evidence | This check never fails on its own — it exists to confirm the other checks are being read correctly: an honestly disclosed shortfall (a test that wasn't run, a case left unhandled, explicitly named as such) does not count as silent drift, not-tested, or a standards failure. Grade `pass` whenever a disclosed gap is actually disclosed; grade `unclear` only if you cannot tell whether a gap was disclosed or hidden | preferred |

## Verdict rule

Accept (ready to submit) only if every `required` check passes. Any `required` check graded `fail` or `unclear` holds the package (reject) — `unclear` on a required check is treated as a fail, not a pass, per the contract's default. `preferred` checks are recorded but never change the verdict.