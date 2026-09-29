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

Where it lives: the repro report's environment section, and (live mode) the target repo's README/CONTRIBUTING or the issue body for the version the bug targets.
What good looks like: the report names actual runtime and library versions and how the project was installed (e.g. "cloned commit abc123, Python 3.11, `pip install -e .`"), matching the issue's target, or explaining a difference.

## Steps

Where it lives: the repro report's steps section, in order.
What good looks like: a stranger with a fresh checkout could run the same commands and hit the same trigger. Steps name a concrete starting state and the specific action that exposes the bug. A vague line like "then I tested it and it broke" does not meet this bar.

## Behavior shown

Where it lives: the report's pasted output, logs, or screenshots, read against the issue body's description of the bug.
What good looks like: the artifact's content is recognizably the same symptom the issue describes: same operation, same failure mode. A different error that happens to occur nearby does not count, even if it looks similar. An honest cannot-reproduce is just as good: the report ran the same operation and pastes what it actually got, naming how that differs from the issue.

## Honesty

Where it lives: the claim comment's promises, and the report's concluding sentence(s), each read against what has actually been done or found.
What good looks like: the claim comment promises only investigation, never a fix or a timeline, before the work is done. The report's claim confidence matches its evidence: "I reproduced it, see the traceback above" needs a traceback above. "I could not reproduce it after installing the pinned version, running the documented steps, and trying two Python versions" earns full credit, as long as the report actually describes what was tried.

## Comms

Where it lives: the repo-facts block's stated AI-use or contribution policy, read against the claim comment and repro report's actual wording.
What good looks like: if the policy requires disclosing AI assistance, the comment says so plainly, naming the tool and the extent of its use. Silence in the policy is not a restriction.
