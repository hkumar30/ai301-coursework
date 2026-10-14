# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/201

**Branch**

fix/12-template-snapshot-hashes

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

In order, the agreement line from every `run_eval.py` call I made:

1. `--limit 5`: "agreement: 3/5 scored items"
2. `--only pkg-01,pkg-02,pkg-03,pkg-04,pkg-05`: "agreement: 4/5 scored items"
3. `--only pkg-09`: "agreement: 1/1 scored items"
4. `--only pkg-05`: "agreement: 0/1 scored items"
5. `--only pkg-01,pkg-02,pkg-03,pkg-04,pkg-05,pkg-09`: "agreement: 6/6 scored items"
6. `--only pkg-06,pkg-07,pkg-08,pkg-10,pkg-11`: "agreement: 3/5 scored items"
7. `--only pkg-01,pkg-02,pkg-03,pkg-04,pkg-05,pkg-06,pkg-07,pkg-08,pkg-09,pkg-10,pkg-11`: "agreement: 11/11 scored items"
8. `--only pkg-12,pkg-13,pkg-14,pkg-15,pkg-16`: "agreement: 5/5 scored items"
9. Full run, `--save-run eval-run.txt`: "agreement: 19/20 scored items  (bar: 18/20: PASS)"

**Package analysis**

pkg-11 (`BurntSushi/ripgrep#3477`, category `clear-accept`, gold `accept`). In the
confirming full run (run 9 above), my tool graded it `reject`, failing `Tested`. But
in run 7, the same tool graded it `accept`. Nothing in `rubric.md`, `procedure.md`,
or `evidence-guide.md` changed between those two runs; this is the same version of
the tool disagreeing with itself.

pkg-11's primary repro states its before/after as inline `# before: .../# after: ...`
comments carrying the issue's own literal error text (`dangling '\'`) rather than a
separately pasted terminal block. My `Tested` check's pass condition treats that as
evidence equal to a pasted block ("whether that is a separately pasted block or a
precise inline note; formatting alone never decides this"), but it is the single
closest case in the eval set to the line that condition draws between a precise
inline note and a vague one. A model grader reading the same comment can land on
either side of that call from one pass to the next, even with the rubric held fixed.
I read this disagreement as a case sitting right at my rubric's own boundary, not as
a wording gap still left to close.

**Check rationale**

The `Tested` row of `rubric.md`, as it reads now:

> `test_evidence.md`'s (or the PR's) pasted or inline-noted results for whatever
> test, lint, and type-check commands the repo's own `docs/CONTRIBUTING.md` or PR
> template actually names for that repo, plus the before/after repro output, read
> against the plan's test plan and any specific test the description claims to have
> added, read against the diff | Pass if the primary repro's before and after states
> each carry specific, verifiable detail (a command's real result, or the exact text
> that did or didn't appear), whether that is a separately pasted block or a precise
> inline note; formatting alone never decides this. Every test, lint, and type-check
> command that repo's own stated conventions call for (never assumed to be Path
> Review's specific commands) is named with a result as specific as that command
> conventionally reports: a count when the tool gives one (pytest, cargo test), a
> definite named pass/fail when it doesn't (`go test`, a formatter or linter with no
> findings). A routine, typically CI-enforced checklist item that isn't itself a
> named test command (code formatted, cheatsheets regenerated, no config changes)
> needs no separate command or output beyond the stated assertion. A secondary or
> control case from the plan's test plan, confirming behavior that should stay
> unchanged, may be stated in prose without its own transcript, as long as the
> primary repro and the named commands are concretely verifiable. Every specific
> test the description claims to have added needs coverage for that case somewhere
> in the diff, even bundled into one test function rather than split into separately
> named ones. A failing or not-applicable result reported honestly, with its reason,
> still counts as evidence. Fail if the primary repro, a required command, or a
> specifically claimed test has no verifiable detail behind it at all: vague ("it
> works", "tests pass"), fabricated, or an unfilled placeholder, in any format, or a
> failing result is omitted instead of disclosed

This went through two rewrites to get here. My first version named Path Review's own
commands (`make test-unit`, `make test-integration`, `make lint`, `make typecheck`)
and Path Review's own template section names directly in the check, which smoke-
tested as false-rejects on the first two real-world packages I tried (Rich, nushell),
since neither repo uses those commands. I generalized it to read whatever commands
and sections a package's own repo-facts block actually names, instead of Path
Review's.

That fixed the overfitting, but a second, subtler problem showed up across three
more packages: nushell's `fmt and clippy clean` claim was rejected for having no
pasted output, lazygit's `go test ./...` claim was rejected for giving no count (a
tool that never reports one), and lazygit's routine "code formatted" checklist item
and ripgrep's inline-comment repro were both rejected on formatting grounds despite
carrying real, specific detail. I rewrote the pass condition around the principle
the quote above now states: specificity is the bar, not a particular format, and
what counts as sufficiently specific depends on what the named tool conventionally
reports.

**Trade-offs**

The routine-checklist-item carve-out ("code formatted... needs no separate command
or output beyond the stated assertion") is what flipped pkg-08 (lazygit) from reject
to accept. What it gives up: a PR that ticks "code formatted" without ever having
run the formatter now passes that item with nothing behind it, and my rubric has no
way to catch that specific claim being false. I accept that gap because the
alternative, demanding a separately pasted command and output for a routine,
CI-enforced item the repo's own template never asks to be shown, was false-rejecting
real, honest PRs whose only failure was not proving something nobody asks them to
prove.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
