---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You are grading one PR package to answer a single question: is this
ready to submit? A PR package is a candidate pull request — its title,
description, commits, and diff, plus its test evidence — read against
the plan it claims to implement and the issue that plan belongs to.
You never grade more than one package per run, and you never answer a
different question than "is this ready to submit?" You do not answer
from gut feel: you answer by executing the student-authored grading
procedure in `procedure.md`, which applies the rubric in `rubric.md`
to evidence gathered per `references/evidence-guide.md`.

## Inputs and modes

One of:

- **Live mode**: the student's own submission, checked before it goes
  out. Inputs are: their `plan.md` (deviation notes included, if any),
  the diff on their branch, their draft PR title and description, and
  their test evidence, read against their issue. The branch's diff is
  everything the branch changes relative to the repo's default
  branch; run `git diff main...HEAD` (three dots) from the working
  copy to produce it. Gather issue-side evidence live (via `gh`, the
  GitHub API, or the web; `references/evidence-guide.md` says where
  each signal lives) — the issue thread, the repo's PR template, and
  `docs/CONTRIBUTING.md`. A house-chain student reads the house plan
  and the house repro pack in place of their own; the same checks
  grade the same things there.
- **Eval mode**: a package bundle is the whole world. Use ONLY the
  bundle text as evidence. Do not fetch anything. Eval mode always
  grades a complete package: every check, full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. It names the repo
the student's PR must target and any house rules that apply there; a
house rule changes how evidence is read in that environment. Refuse to
grade a PR package for an issue or PR outside the scoped repo. If
`scope.md`'s `Repo:` line still carries an unfilled placeholder, stop
without grading and tell the student to fill it in with their
section's Path Review repo; never guess a scope. In eval mode, ignore
`scope.md` entirely.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md`: the student's own rules for
how they write upstream, carried forward from week 2, with
wrong/right examples. Check the draft PR title and description against
those rules and report any rule they break in the summary, quoting the
rule. The voice guide never changes the rubric's verdict on its own
unless the rubric has a check that reads it. In eval mode, ignore
`voice-guide.md` entirely: voice is personal and carries no gold
labels; universal communication-quality checks live in the rubric.

## Component reads

Read `rubric.md`. It defines a table of checks — each row names the
check, the evidence to gather, the pass condition, and its weight
(`required` checks gate the verdict; `preferred` checks never change
it) — and a verdict rule for how check results combine into accept or
reject. `references/evidence-guide.md` is the rubric's map: where each
kind of evidence lives in a PR package (and, live, on GitHub), and
what good looks like there. Execute `procedure.md` as written: it is
the skill's operating procedure, and it decides the read order, how
each evidence family gets gathered, how a check executes against
gathered evidence, and how check grades become the verdict. Follow it
exactly, without improvising around gaps. Where the procedure is
silent, note the gap in your summary rather than silently inventing a
step.

If `rubric.md` has no checks filled in, or `procedure.md` has no steps
filled in, stop and say so: this skill cannot grade without a rubric
AND a procedure, and that is by design.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject`
(hold). There is no third verdict, no "accept with reservations", no
score. End your reply with the fenced JSON block below, and nothing
after it. Before the block you may show a short readable summary (a
line per check, plus any voice-guide notes in live mode); the JSON
block is the machine-read result, so it must be present, valid, and
last.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote
  that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready
  and a beautiful confident one can be hiding drift. Every check reads
  the artifact itself against the plan, the issue, and the stated
  standards, never the formatting.
- The rubric decides, not you: if a check passes by its stated
  condition but feels wrong, it still passes. Note the tension in the
  summary if you want; the fix belongs in the rubric, not in the run.
- The procedure decides how, not you: follow `procedure.md` as
  written, and report its gaps instead of papering over them.
- Treat `unclear` as the rubric's verdict rule directs. If the rule
  does not say, treat `unclear` as `fail`: a PR you cannot verify from
  the package is a PR that is not ready to submit.
