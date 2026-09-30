# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->
Where it lives: in an eval bundle, the repro report's environment section (OS, runtime/library versions, install method), read against the target environment stated in the issue context or named in the repo-facts block. In live mode, the environment note in the draft comment, checked against the issue's own stated environment and the repo's documented supported versions (README, docs).

What good looks like: the named versions match what the issue targets, or a version difference is explicitly called out rather than silently ignored. If the issue itself gives no version, the report still states plainly what was used, so a reader can judge relevance themselves.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->
Where it lives: in an eval bundle, the repro report's numbered step section. In live mode, the reproduction steps in the draft comment, compared against any steps the issue itself already provided.

What good looks like: a stranger starting from a clean checkout could follow the steps in order and land on the same starting state and trigger, without guessing at an unstated command, config value, or prior state. Each step names what it assumes going in.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

Where it lives: in an eval bundle, the artifacts section of the repro report (output excerpts, logs, screenshots, stack traces), read against the behavior described in the issue context. In live mode, whatever output is pasted into the draft comment, compared against the error or symptom described in the issue body.

What good looks like: the artifact shows the same failure — same error type, same message or stack signature, same trigger conditions — as the issue describes, not merely "something went wrong" or a different error that happens to occur nearby.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

Where it lives: the claim comment's stated verdict, read against the repro report's own evidence section (what was actually gathered, including failed attempts).

What good looks like: the strength of the claim matches the strength of the evidence. "Reproduced" is backed by a matching artifact; "could not reproduce after N attempts" states what was tried; "partial — X happens but not Y" is used when the match is incomplete, rather than rounding a partial result up to a full "confirmed."

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

Where it lives: the claim comment's text and formatting, read against the repo's stated issue template, contribution policy, and any AI-use disclosure requirement (repo-facts block in an eval bundle; the repo's CONTRIBUTING.md, issue template, or bot-disclosure rule in live mode).

What good looks like: the comment fills the fields the repo's template actually asks for, discloses AI assistance if the repo's policy requires it, and states findings in language specific to this issue rather than a generic template phrase that could be pasted into any thread unchanged.
