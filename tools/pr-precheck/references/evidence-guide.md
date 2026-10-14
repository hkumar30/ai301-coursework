# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Where it lives: in an eval bundle, the plan-context block's stated scope and test plan, read against the candidate PR's diff and description. In live mode, `plan.md` (including any `## Deviations` note), read against `git diff main...HEAD` and the draft description in `pr_draft.md`.

What good looks like: every file the diff touches falls inside what the plan's approach section names, in plain language, not necessarily its exact path. The plan's "a changelog entry" counts as naming the changelog file it adds. A file the diff touches that the plan never named in any form, with no `## Deviations` note explaining it, is silent drift. A description that claims more or less than the diff actually delivers ("no changes beyond it" when an extra file is touched) is also silent drift, not a comms problem.

## Test evidence (harness category: not-tested)

Where it lives: in an eval bundle, the repo-facts block's stated test/lint/type-check commands for that specific repo, and the test-evidence section's before/after and command output, read against the plan's test plan. In live mode, `docs/CONTRIBUTING.md` or the PR template for whatever commands that repo actually names (Path Review names `make test-unit`, `make test-integration`, `make lint`, `make typecheck`; a different repo names its own, such as `pytest` or `cargo test`), and `test_evidence.md`'s pasted output for those commands plus the repro's before/after, read against `plan.md`'s test plan.

What good looks like: specificity, not a particular format. The primary repro's before and after each need a real, verifiable detail behind them, a command's actual result or the exact text that did or didn't appear, and that detail counts the same whether it sits in a separately pasted block or a precise inline note. `# before: rg: ./.gitignore: line 1: error parsing glob 'foo\': dangling '\'` is real evidence because it is the issue's own literal error text, not a vague gloss; a bare `# before: it errored` would not be. A claim that something wasn't added ("no options added") can be verified directly from the diff and needs no pasted output of its own.

Every test, lint, and type-check command that repo's own stated conventions call for needs a result, but how specific that result must be depends on what the tool itself conventionally reports. A tool that gives a count (`pytest`, `cargo test`) needs that count. A tool that doesn't (`go test`, a formatter, a linter with a clean run) needs only a definite named pass/fail, "`go test ./...` passes" or "`cargo fmt` and `clippy` clean" is sufficient on its own, with no pasted block required; demanding a count from a tool that doesn't produce one is holding the PR to a standard the tool can't meet. Never grade a package against Path Review's specific command names if it belongs to a different repo; grade it against that repo's own stated commands instead.

A routine, typically CI-enforced checklist item that isn't itself a named test command, code formatted, cheatsheets regenerated, no config changes, needs no separate command or output beyond the stated assertion; it isn't the kind of claim this category exists to catch. A secondary or control case from the plan's test plan, one confirming behavior that should stay unchanged, may be stated in prose without its own transcript, as long as the primary repro and the named commands are concretely verifiable; lazygit's "a tracked change still stashes" is this kind of case. Any specific test the description claims to have added (a named scenario, an all-comments or nested-case control) needs coverage for that case somewhere in the diff, but that coverage can be one assertion bundled into a shared test function rather than a separately named test per case; a checklist box ticked for a test that was never written, in any form, is exactly as decisive as a missing command's output.

A failing or not-applicable result, reported honestly with its reason, still counts as evidence; this category is about absent or fabricated proof, not about failure itself. What fails this check: the primary repro, a required command, or a specifically claimed test with no verifiable detail behind it at all, vague ("it works", "tests pass"), fabricated, or an unfilled placeholder, in any format, or a failing result quietly omitted instead of disclosed.

## Diff quality (harness category: unreviewable)

Where it lives: the unified diff itself (`git diff main...HEAD` and `--stat` for the file list), read against the description's Changes bullets.

What good looks like: every file the diff touches is named by a Changes bullet, and nothing rides along that the issue doesn't call for: no debug lines, no commented-out code, no formatting-only churn mixed into a functional change. A diff that is otherwise correct but carries one unrelated edit is still unreviewable, because a reviewer has to understand the unrelated edit before trusting the rest.

## Standards and comms (harness category: standards-wall)

Where it lives: the repo-facts block's stated PR template and CONTRIBUTING.md conventions for that specific repo (its own section names and its own issue-reference convention, not assumed to be Path Review's), read against the candidate PR's title and every section of its description, including disclosure. In live mode, the Path Review repo's actual `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md`, read against `pr_draft.md`.

What good looks like: every section that repo's own template defines carries real content, not its own placeholder text left in place; the issue is referenced the way that repo's convention asks (Path Review and many repos use `Closes #<n>`, but confirm it against this repo's own template rather than assuming it); AI-use disclosure is present when that repo's policy asks for it; and a stated convention like branch naming is actually followed. Whether the description's claims match the diff is plan fidelity, above, not this check.
