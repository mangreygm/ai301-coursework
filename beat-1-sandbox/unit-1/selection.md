# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
`gh` wasn't authenticated, so I gathered everything from the public GitHub API. All three candidates are in the scoped repo (`codepath/pathreview-ai301-fa26-s3`), and the Path Review house rule on claim comments turned out to be moot — none of the three has any comments at all.

**Repo-level evidence (shared by all three, measured against today, 2026-09-22):**
- Last default-branch commit `2026-09-16` by Andrew Burke (`Aburke225`, non-bot) — 6 days old → maintainer active
- No releases or tags, but 73 issues opened in the last 90 days → repo in active use
- `archived: false`, no deprecation banner in README or description
- `docs/CONTRIBUTING.md` (189 lines), the PR template, and the repo root say nothing about AI contributions → silence passes

**Accepted, in fit order:**

1. **#12 — Add snapshot tests for prompt templates.** All 7 required checks pass, and both preferred checks pass (good-first-issue label; purely additive). Best fit: it touches exactly one file, `tests/unit/test_prompt_templates.py`, so it is the additive pytest work you asked for — no runtime behavior changes at all, and it puts you through `make lint`/`make typecheck`/`make test-unit` on a change that cannot regress anything.
2. **#18 — Repo analyzer never receives a file list.** All required checks pass, both preferred pass. A small isolated bugfix across two files with a clear root cause already diagnosed in the body, and it carries the `tests` label — more than #12 asks of you, but it stays clear of stateful subsystems.
3. **#15 — Agent session state not cleared between reviews.** All required checks pass, so the rubric accepts it, but it fails the preferred low-review-burden check: it spans three modules (`orchestrator.py`, `session_store.py`, `context_manager.py`) and rewrites cache and session-state lifetime — precisely the stateful caching/session work your profile says to avoid. Ranked last on fit, not rejected.

Worth flagging: all three are seeded course issues opened the same minute by the same collaborator, so the "already claimed" and "duplicate" checks pass on an absence of evidence rather than on positive signal. Under the house rule that's expected, and classmates may claim alongside you regardless.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12",
    "checks": [
      {"name": "Maintainer active", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 by Andrew Burke (Aburke225, non-bot), 6 days before 2026-09-22"},
      {"name": "Repo in active use", "grade": "pass", "evidence": "73 issues opened in the last 90 days (all between 2026-09-10 and 2026-09-16); no releases or tags exist"},
      {"name": "Not archived/deprecated", "grade": "pass", "evidence": "API reports archived: false; README and description contain no deprecated/unmaintained/superseded text"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "Not an umbrella issue; zero comments so no unresolved design debate; no maintainer statement about core internals"},
      {"name": "Scope has enough detail to start", "grade": "pass", "evidence": "Explicit acceptance criteria: 'snapshot tests that fail if a template's content changes without a version bump'"},
      {"name": "Not already claimed", "grade": "pass", "evidence": "assignees: []; comments: 0"},
      {"name": "Not a duplicate / not stale-abandoned by a prior claimant", "grade": "pass", "evidence": "Timeline shows only labeled events — no cross-referenced or connected PRs, and no prior claim"},
      {"name": "Labeled for newcomers", "grade": "pass", "evidence": "Labels include 'good first issue'"},
      {"name": "Low review burden expected", "grade": "pass", "evidence": "Purely additive: only relevant file is tests/unit/test_prompt_templates.py"},
      {"name": "Contribution policy allows AI assistance", "grade": "pass", "evidence": "docs/CONTRIBUTING.md, PR template, and repo root contain no AI clause; no AI_POLICY.md exists"},
      {"name": "Feature requests have maintainer buy-in", "grade": "pass", "evidence": "Opener Aburke225 has author_association COLLABORATOR"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/18",
    "checks": [
      {"name": "Maintainer active", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 by Andrew Burke (Aburke225, non-bot), 6 days before 2026-09-22"},
      {"name": "Repo in active use", "grade": "pass", "evidence": "73 issues opened in the last 90 days; no releases or tags exist"},
      {"name": "Not archived/deprecated", "grade": "pass", "evidence": "API reports archived: false; no deprecation banner in README or description"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "Not an umbrella issue; zero comments so no unresolved design debate; no maintainer statement about core internals"},
      {"name": "Scope has enough detail to start", "grade": "pass", "evidence": "Expected vs actual stated: '_detect_tests() ... read file names from repo_data.get(\"file_structure\", \"\"), but no code sets that key, so has_tests and has_ci are always False'"},
      {"name": "Not already claimed", "grade": "pass", "evidence": "assignees: []; comments: 0"},
      {"name": "Not a duplicate / not stale-abandoned by a prior claimant", "grade": "pass", "evidence": "Timeline shows only labeled events — no linked PRs and no prior claim"},
      {"name": "Labeled for newcomers", "grade": "pass", "evidence": "Labels include 'good first issue'"},
      {"name": "Low review burden expected", "grade": "pass", "evidence": "Small isolated bugfix across 2 files with root cause diagnosed; estimated 2-4 hours; no public API change"},
      {"name": "Contribution policy allows AI assistance", "grade": "pass", "evidence": "No AI policy in docs/CONTRIBUTING.md, PR template, or repo root"},
      {"name": "Feature requests have maintainer buy-in", "grade": "pass", "evidence": "Bug report (always-False detection flags), and opener Aburke225 is COLLABORATOR"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/15",
    "checks": [
      {"name": "Maintainer active", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 by Andrew Burke (Aburke225, non-bot), 6 days before 2026-09-22"},
      {"name": "Repo in active use", "grade": "pass", "evidence": "73 issues opened in the last 90 days; no releases or tags exist"},
      {"name": "Not archived/deprecated", "grade": "pass", "evidence": "API reports archived: false; no deprecation banner in README or description"},
      {"name": "Scope is bounded", "grade": "pass", "evidence": "Not an umbrella issue; zero comments so no unresolved design debate; no maintainer statement that it touches core internals — 3 named files do not fail this check per the rubric"},
      {"name": "Scope has enough detail to start", "grade": "pass", "evidence": "Actual behavior plus fix criteria: 'returns the first run's result for every tool whose input hasn't changed. Empty that cache and delete the profile's saved session state when run starts.'"},
      {"name": "Not already claimed", "grade": "pass", "evidence": "assignees: []; comments: 0"},
      {"name": "Not a duplicate / not stale-abandoned by a prior claimant", "grade": "pass", "evidence": "Timeline shows only labeled events — no linked PRs and no prior claim"},
      {"name": "Labeled for newcomers", "grade": "pass", "evidence": "Labels include 'good first issue'"},
      {"name": "Low review burden expected", "grade": "fail", "evidence": "Not additive and not isolated: changes cache and session-state lifetime across orchestrator.py, session_store.py, and context_manager.py"},
      {"name": "Contribution policy allows AI assistance", "grade": "pass", "evidence": "No AI policy in docs/CONTRIBUTING.md, PR template, or repo root"},
      {"name": "Feature requests have maintainer buy-in", "grade": "pass", "evidence": "Bug report (stale session state), and opener Aburke225 is COLLABORATOR"}
    ],
    "verdict": "accept"
  }
]
```

```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

Only one run was executed. From eval-run.txt:

agreement: 18/20 scored items (bar: 18/20: PASS)

**Issue analysis**

issue-04. From eval-run.txt:

issue-04 accept reject NO failed: Scope has enough detail to start

My rubric's decision was reject; the gold label is accept. The rubric rejected it because the Scope has enough detail to start check requires the issue body to contain at least one of reproduction steps, expected/actual behavior, or explicit acceptance criteria, and my check graded none of those as present. The gold grader evidently still considered the issue actionable — likely because the missing detail was recoverable from context even though it wasn't phrased as one of my three named patterns. That's a false negative: the check enforces a literal format rather than "can a newcomer actually start," and this issue satisfied the spirit without satisfying the letter.

**Check rationale**

Scope has enough detail to start | Issue body: whether steps to reproduce, expected vs actual behavior, or acceptance criteria are present | At least one of (reproduction steps, expected/actual behavior, explicit acceptance criteria) is present in the issue body | required

I made it required, not preferred, because vague scope is one of the most common reasons a first-time contributor stalls out — even a healthy, active repo with a perfectly bounded issue is unusable if the newcomer can't tell what "done" looks like without asking. I anchored the pass condition to three named patterns rather than a vaguer "has enough context" so a different grader would produce the same verdict I did.

**Trade-offs**

The check's canary is issue-04 itself: gold says accept, my rubric said reject, and the note names this exact check as the failure. The check buys consistency (anyone applying it gets the same answer) at the cost of recall — it only recognizes detail when it arrives in one of three explicit shapes, so it misses issues where enough information is present but conveyed some other way (e.g., a self-explanatory title plus a code reference). I haven't re-run with --only to confirm this is the sole cause, but the note field ties the miss directly to this check with no other failing check listed.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. Fit to interests and time available: the 3–5 hour estimate for #12 fits a first PR I can finish in one sitting, and writing snapshot tests is a low-stakes way to learn the repo's test conventions (make lint/make typecheck/make test-unit) before touching anything that changes runtime behavior.
2. What the verdict got right vs. what I weighed that it couldn't: the verdict correctly caught that this is purely additive — one file, tests/unit/test_prompt_templates.py — and that the acceptance criteria are stated outright. What it can't weigh is my own comfort with the codebase's specific snapshot-testing pattern, which I won't know until I open the file.
3. Anticipated difficulty in claiming: the issue has no assignee and no comments, so it's technically open, but it's one of three seeded course issues opened in the same minute by the same collaborator for a whole cohort — a classmate could claim it around the same time I do, so I plan to post a claim comment promptly rather than assuming it'll sit unclaimed.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
