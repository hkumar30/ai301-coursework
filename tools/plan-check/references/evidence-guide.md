# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

Where it lives: the plan's Diagnosis section, and the repro evidence block's numbered steps and their results.
What good looks like: the stated cause explains every repro step, including any step built specifically to isolate or rule out an alternative explanation. A diagnosis that borrows a thread comment's theory without checking it against a step that contradicts that theory does not pass.

## Scope

Where it lives: the plan's in-scope/not-in-scope lines, read against the files or areas named in its Changes/approach section.
What good looks like: one bounded change. Every file the Changes section touches appears in the scope statement, and the plan says at least one thing it will deliberately leave alone. If the Changes section mentions a production-code change whose file or location is never stated (a new module, a new helper), treat it as touching something scope doesn't name, unless the plan says explicitly where it will live. A new or updated test mentioned without an exact file path does not count against scope on its own — that's Test plan's job to judge.

## Executability

Where it lives: the plan's Changes/approach section.
What good looks like: a stranger could make the first edit today without asking the author anything: a named file, a concrete change, and an order of work, not just a destination.

## Test plan

Where it lives: the plan's Test plan section, read against the repro evidence's steps and artifacts.
What good looks like: a before/after state that two people watching it would agree passed or failed, and that reuses or maps onto something the repro evidence already showed, not a new unconnected claim.

## Honesty

Where it lives: the plan's stated risks or unknowns, read against its diagnosis and test plan.
What good looks like: an assumption is labeled as an assumption. A plan that states a guess as if the repro evidence already confirmed it is dressing up an unknown as certainty.

## Comms

Where it lives: the plan comment, read against the thread highlights and the repo-facts block's stated contribution policy, templates, and AI-use disclosure requirement.
What good looks like: the comment responds to anything in the thread that bears on the plan (a competing theory, a maintainer's ask) and discloses AI assistance when the repo's policy requires it. Silence in the policy is not a restriction.