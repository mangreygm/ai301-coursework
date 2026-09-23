# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer active | Repo-facts block: (a) the last-5-commits list, using each commit's author name to exclude usernames ending in [bot], and (b) the "maintainer first-response sample," using each comment's author_association field to count only OWNER, MEMBER, or COLLABORATOR | Passes if EITHER at least one commit in the last-5-commits list has a non-[bot] author with a date within 30 days of the capture date, OR at least 2 of the 5 sampled issues in the first-response sample show a first reply from an OWNER/MEMBER/COLLABORATOR account, dated within 30 days of that issue's opening | required |
| Repo in active use | Repo-facts block: release/tag history and open issue creation rate over the last 90 days | Either a tagged release exists in the last 180 days, or at least 5 new issues were opened in the last 90 days | required |
| Not archived/deprecated | Repo-facts block: archived flag, and repo description/README banner text | Repo is not marked archived and no README/description banner says deprecated, unmaintained, or superseded-by | required |
| Scope is bounded | Issue body and comment thread: whether the issue is framed as an umbrella/tracking issue meant to be split up, whether the thread shows unresolved design disagreement with no maintainer decision, and whether a maintainer has stated the fix touches core internals/architecture | Fails only if one of those three conditions is true. Listing multiple possible causes or multiple candidate fix approaches for a single reported bug/behavior does NOT by itself count as an umbrella issue — it only fails if the issue explicitly asks for these to be split into separate issues or tracked as a checklist of independent tasks. Otherwise passes, regardless of description length or number of files named. | required |
| Scope has enough detail to start | Issue body: whether steps to reproduce, expected vs actual behavior, or acceptance criteria are present | At least one of (reproduction steps, expected/actual behavior, explicit acceptance criteria) is present in the issue body | required |
| Not already claimed | Comment thread: assignment field, and comments containing "I'll take this," "working on it," "assigned to me," or similar | Issue has no assignee, and no commenter has claimed it within the last 21 days without a follow-up "still working on this" | required |
| Not a duplicate / not stale-abandoned by a prior claimant | Comment thread: linked PRs, and any claim older than 21 days with no linked PR or update since | No open PR is linked to this issue, and any prior claim is either withdrawn or more than 21 days stale with no activity | required |
| Labeled for newcomers | Issue labels in repo-facts block | Issue carries a label such as "good first issue," "help wanted," "beginner-friendly," or equivalent | preferred |
| Low review burden expected | Issue body + repo-facts block: whether the change is additive (docs, tests, small bugfix) vs. behavior-changing | Change is additive or a small, isolated bugfix rather than a behavior change affecting public API | preferred |
| Contribution policy allows AI assistance | Repo-facts block: contribution policy line (from CONTRIBUTING.md or equivalent) | Fails only if the policy explicitly states AI-generated code/documentation/contributions are not accepted or will be rejected outright. Passes if AI use is explicitly allowed (with or without conditions like disclosure or requiring the contributor to understand/test the change), or if the policy says nothing about AI at all | required |
| Feature requests have maintainer buy-in | Issue body: the opener's role tag (shown as author_association — e.g. NONE, MEMBER, COLLABORATOR), and whether the issue is a new feature request vs. a bug report; comment thread for any endorsement | Passes automatically if this is a bug report/fix (not a new feature), OR if the opener's role is OWNER, MEMBER, or COLLABORATOR. Otherwise, fails unless at least one OWNER/MEMBER/COLLABORATOR has commented in support of building it | required |

## Verdict rule

Accept only if every `required` check passes. A single required failure rejects the issue, regardless of how many others pass. `preferred` checks never change the verdict — they exist only to rank accepted issues against each other (more preferred passes ranks higher). Any check whose evidence is missing, ambiguous, or cannot be determined from the repo-facts block, issue body, or comment thread is graded `unclear`, and `unclear` is treated as a fail for required checks (rejecting the issue) and as a non-pass for preferred checks (no ranking credit).
