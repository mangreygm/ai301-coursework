# Procedure: how this skill grades a plan package

## Read order

1. Read the Issue section first. Note the exact reported behavior and the stated expected behavior.
2. Read the Repro evidence block next. Note the specific environment, each step's observed behavior, and any evidence of an exact failure point (a specific file, function, stack trace, or log line). This is the ground truth every later check compares against.
3. Read Thread highlights. Note any alternative theories, other contributors' test results, or constraints a maintainer stated (e.g., limited review bandwidth).
4. Read Repo facts. Note the contribution policy (including any AI-disclosure requirement) and any issue/PR template requirements.
5. Read the Candidate plan (Diagnosis, Scope, Files, Approach, Test plan) last, now that the evidence to check it against is already noted. Reading the plan before the evidence risks grading the plan's own framing of the evidence instead of the evidence itself.
6. Read the Candidate plan comment last of all.

## Evidence gathering

- Diagnosis and grounding: quote the plan's stated cause. Quote every specific fact from the Repro evidence section, especially any step identifying an exact failure point.
- Scope: quote the plan's in-scope/not-in-scope lines and its Files section verbatim.
- Executability: quote the Approach section's steps verbatim, in order, plus the Files section.
- Test plan: quote the plan's Test section, and the Repro evidence's exact steps/commands/outputs to compare it against.
- Honesty: quote any Risks/Unknowns/Deviations content. Separately note any confident claim in the Diagnosis or Scope that dismisses an alternative explanation without citing evidence for the dismissal.
- Comms: quote the plan comment verbatim. Quote the repo-facts contribution policy and the thread highlights verbatim.

## Check execution

1. Execute checks in the order listed in rubric.md's table.
2. Grade "Diagnosis grounded in repro evidence" first: several later checks (Scope, Test plan) presume the diagnosis is at least internally consistent with the evidence.
3. For each check, compare only the evidence gathered above against that check's pass condition as written. Do not re-interpret a pass condition differently from package to package.
4. If the evidence a check names is entirely absent from the package (for example, no Risks/Unknowns section exists at all), grade that check `unclear`, not an automatic fail — but when the plan's own confidence elsewhere implies real uncertainty exists and goes unstated, grade "Uncertainty stated honestly" as a fail rather than `unclear`, since silence on a known risk is itself overconfidence.
5. A check may be graded from the Read order notes alone once they are complete; re-read the specific section directly only if a note is ambiguous.

## Verdict assembly

1. Apply the rubric's verdict rule: accept only if every required check passes.
2. Any required check graded `fail` or `unclear` produces `reject`.
3. Preferred checks are recorded in the output but never change the verdict.
4. For each check in the output JSON, quote the specific fact (not a paraphrase) that decided its grade — for a failing diagnosis check, this should be the exact repro-evidence sentence the plan's stated cause contradicts or ignores.