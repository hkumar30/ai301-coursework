# Procedure: how this skill grades a PR package

## Read order

1. Read the issue and its thread highlights, the repo's PR template,
   and `docs/CONTRIBUTING.md` first, noting any required template
   sections, disclosure asks, and branch-naming or contribution
   conventions.
2. Read `plan.md` next, including any `## Deviations` section, noting
   its stated approach (the files/areas it says it will touch) and its
   test plan.
3. Read the diff (`git diff main...HEAD`) next, noting every file it
   touches, what changed in each, and anything that looks like debris
   (debug lines, commented-out code, edits unrelated to the issue).
4. Read `test_evidence.md` next, noting the pasted output for each of
   the four required commands and the before/after repro output.
5. Read `pr_draft.md` (title and description) last, since it is graded
   against everything already read.

## Evidence gathering

- Fidelity: pull the plan's approach section and any `## Deviations`
  note, and the diff's file list; note any file or change the diff
  makes that the plan's approach doesn't name and that no deviation
  note explains.
- Tested: first establish what this repo's own CONTRIBUTING.md or PR
  template actually names as its test, lint, and type-check commands
  (Path Review names `make test-unit`, `make test-integration`,
  `make lint`, `make typecheck`; another repo names its own, and some
  ask for routine checklist items, like "code formatted" or
  "cheatsheets regenerated", that are not themselves a named command).
  Pull the pasted or inline-noted result for each required command,
  and the primary repro's before/after; note whether each carries
  specific, verifiable detail, not vague narration or a placeholder,
  regardless of whether that detail sits in a separately pasted block
  or a precise inline comment. A named command's result only needs the
  specificity that tool conventionally reports (a count for pytest or
  cargo test; a plain named pass/fail for `go test` or a clean
  linter/formatter run, neither of which conventionally gives a
  count). A routine, CI-enforced checklist item that names no test
  command of its own needs no separate output beyond its stated
  assertion. A secondary or control case from the plan's test plan,
  confirming behavior that should stay unchanged, may be stated in
  prose, as long as the primary repro and the named commands are
  concretely verifiable. Note whether any failing result is disclosed
  rather than omitted, and whether every specific test the description
  claims to have added (a named scenario or control case) has coverage
  for it somewhere in the diff, even bundled into one test function
  rather than split into separately named ones.
- Reviewable: pull the diff's file list and content, and
  `pr_draft.md`'s Changes bullets; note any diff change not covered by
  a bullet, any bullet naming a file the diff doesn't touch, and any
  debris in the diff itself.
- Standards: first establish what sections and conventions this repo's
  own PR template and CONTRIBUTING.md actually ask for (never assume
  Path Review's section names apply to a different repo). Pull
  `pr_draft.md`'s sections against that repo's own template; note any
  section that template requires but is missing or left as
  boilerplate, any disclosure that repo's policy requires but is
  absent, and whether the issue is referenced the way that repo's
  convention asks.
- Honesty: pull any gap, failing check, or deviation language in
  `plan.md` and `test_evidence.md`; note whether it is named plainly
  or only visible by comparing against the diff/test output directly.

## Check execution

Grade in this order: Fidelity, Tested, Reviewable, Standards, Honesty.
Grade each independently; a fail on one check never changes how you
read evidence for another. Grade pass only when the gathered evidence
satisfies the check's stated pass condition. Grade fail when the
gathered evidence contradicts it. Grade unclear only when the needed
evidence is genuinely absent from the package, not because you
disagree with a judgment call the plan or PR made; when the PR states
its own working assumption or a disclosed limitation and nothing in
the package contradicts it, treat that as resolved, not unclear.

## Verdict assembly

Apply the rubric's verdict rule: ready only if every required check
grades pass. Any required check graded fail or unclear makes the
verdict hold (unclear counts as fail). In the output, quote the
evidence for whichever required check failed most directly against the
plan or the diff as the deciding check. If every required check
passes, there is no deciding check to quote. State that plainly, and
note the preferred check's result instead, since it's the only thing
that could still flag a PR worth a closer look.
