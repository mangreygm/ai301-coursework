# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | The repro report's environment record (OS, runtime/library versions, install method), read against the issue's stated target environment (issue context / repo-facts block) | The versions named match what the issue targets, or a mismatch is explicitly called out rather than left silent; if the issue names no version, the report still states what was actually used | required |
| Steps are complete and followable | The repro report's step-by-step section, read against the issue's described starting state | A stranger with a clean checkout could execute the steps in order, from a stated starting point, and reach the trigger — with no skipped setup, no assumed prior state, and no unstated inputs | required |
| Behavior matches the issue | The artifacts (output excerpts, logs, screenshots/stack traces) in the repro report, read against the specific behavior the issue describes | The artifact shows the same failure mode the issue describes (same error, same symptom, same trigger conditions) — not a different error, a partial match, or a plausible-looking but adjacent bug | required |
| Outcome is honestly stated | The claim comment's stated verdict, read against what the report's own evidence actually shows | The verdict (reproduced / cannot reproduce / partial) follows from the evidence shown. An honest, evidenced cannot-reproduce is a pass; a confident "confirmed" resting on partial, missing, or inferred evidence is not | required |
| Comms match repo conventions | The claim comment's text and structure, read against the repo's issue template and contribution/AI-disclosure policy (repo-facts block) | The comment fills the repo's required template fields where one exists, discloses AI assistance where the repo's policy requires it, and its claims are specific to this issue rather than generic boilerplate | required |
| Comment is specific, not padded | The claim comment's prose itself | The comment states what was actually checked and found in terms specific to this issue; it is not padded with filler that could be pasted into any issue's thread unchanged | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept (ready to post) only if every `required` check passes. Any `required` check that fails, or is graded `unclear`, holds the package (reject) — `unclear` on a required check is treated as a fail, not as a pass. `preferred` checks are recorded but never change the verdict either way.