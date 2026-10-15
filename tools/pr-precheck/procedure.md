# Procedure: how this tool grades a PR package

## Read order

1. Read the Issue section first. Note the exact reported behavior and any maintainer direction in the thread.
2. Read the Plan context block next: the plan's stated scope (in/out), named files, and test plan, plus any `## Deviations` note. This is the ground truth every side-by-side check compares against — read it before the diff, so you are not anchored by the diff's own framing of what it does.
3. Read the Repo facts block: the PR template's required sections and the stated contribution/AI-disclosure policy.
4. Read the candidate PR's diff and commit list.
5. Read the candidate PR's title and description last of all, now that you know independently what the diff actually does.
6. Read the test-evidence section.

## Evidence gathering

- Plan fidelity: list every file and hunk the diff touches; list every file and boundary the plan names. Compare the two lists directly.
- Description vs. diff: extract every factual claim the description makes about the change; check each against the diff's actual content.
- Test evidence: pull the plan's test plan and the issue's original repro steps; compare them against the test-evidence section's before/after and the repo's required checks' reported outcomes.
- Diff quality: scan the diff for hunks unrelated to the plan's named files/scope, debug statements, commented-out code, and pure formatting churn mixed into functional changes.
- Standards and comms: pull the repo-facts block's required PR template sections and stated policy; check each against the description's actual sections.
- Honest shortfall: note any place the description or `## Deviations` explicitly names a gap, limitation, or thing not done.

## Check execution

1. Execute checks in the order listed in rubric.md's table.
2. Grade "Diff matches the plan's scope" and "Description matches the diff" first, since later checks' readings depend on already knowing where the diff's real boundary is.
3. Compare only the evidence gathered above against each check's pass condition as written; do not reinterpret a pass condition differently package to package.
4. If evidence a check names is genuinely absent from the package, grade that check `unclear` rather than inventing an assumption.
5. A check may be graded from the Read-order notes alone once they are complete; re-read the specific section directly only if a note is ambiguous.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every required check passes.
2. Any required check graded `fail` or `unclear` produces `reject`.
3. Preferred checks are recorded but never change the verdict.
4. When more than one required check fails, quote the first failing required check in rubric-table order as the deciding one in the output JSON's evidence lines — quote the exact fact or line that failed it, not a paraphrase.