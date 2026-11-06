# Contribution: Replace `standalone` config option flag with new option to specify visa backend

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Harsh Kumar
**GitHub Username:** hkumar30
**Issue:** https://github.com/tektronix/tm_devices/issues/417
**Pull Request:** https://github.com/tektronix/tm_devices/pull/649

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built issue-scout and patched its rubric after it accepted everything**

I grew my Unit 1 skill into issue-scout, with a Python-only fit profile, three `gh search issues` queries, ranking filters and a six-check rubric. Scan 1 accepted all five issues, but four sat in repos with 23 or fewer stars and most were opened the day before, so I added date-bounded queries and a required 50-star "Repo in use" check; scan 2 then rejected all five, each for a checkable reason such as an open PR or a claim comment. Screening the Issue Selection site with `gh` showed my AI-policy check would have passed beets, whose policy bars AI on good first issues and whose maintainer had closed earlier PRs on two of them for that reason, so I tightened it. Across two grading runs on picks from the Issue Selection site, the scout accepted tm_devices #417 and pytorch #74602 and rejected pytorch #119856 and airflow #63374 on scope, though the AI-policy patch has only been checked by reading policy text, not by a scout run that failed on it.

**Unit 6: Installed the voice guard and wrote a repo memory file**

I merged my three voice guides into one with new upstream rules for claims, questions and pings, installed a hook that checks every comment I post through Claude Code against it, and wrote a 35-line `CLAUDE.local.md` for my tm_devices clone. I did all of it after I had posted my claim and built the PR, so the guard checked neither, and the memory file saved no orientation work on this issue. As a late audit, the guard stopped my posted claim and repro-check rejected it for naming no first step and no report-back day, and I left the thread as it is. Dry runs of a ping and a reply passed, so I changed none of my existing rules.

**Unit 7: Installed ship-gate, wrote a gate manifest, and got PASS on the open PR**

I installed the ship-gate against my tm_devices clone and filled `ship-manifest.md` with the project's pytest, lint/type and griffe commands, plus a known-failures table for checks that already fail outside this change. The hook test of `gh pr create --help` logged a setup BLOCK on 2026-11-05, and a manual run on head `5e06c15` later that day (21:50 UTC) returned PASS. I had opened the PR by hand a day before the gate existed, so the PASS audited an already-open PR rather than gating the create. A fresh-terminal pyright run was the only real fight, and it is what put `--pythonpath` into the lint row.

**Unit 8: Installed the PR monitor and wrote a playbook, but the drafting run hit my spend limit**

I installed the monitor and wrote a playbook from five merged outside-contributor PRs, where a maintainer answered within a day each time, so I nudge after 4 quiet working days before a first review and 7 after an approval. `--state` read #649 correctly (approved, 5 failing checks, mergeable but blocked), yet labeled it "review feedback is in" because the newest thread items were CI and Codecov bot comments, so I added a playbook rule that bot comments don't count as activity. The full run stopped before drafting anything because Claude hit my spend limit, so there is no draft to judge and I posted nothing. The PR is approved and has been quiet for under a day, so by my own thresholds no move is due yet.

---

## Why I Chose This Issue

I started with my scout's own scans of GitHub. The first one accepted all five issues, mostly in new repos with almost no stars; after I fixed the queries and added a star floor, the second rejected all five, each for a checkable reason such as an open PR or a claim. My actual pick had to come from the Issue Selection site, so I screened its Python + good-first-issue list (1,203 issues) with `gh`, cutting dead repos and anything already assigned, claimed or linked to an open PR, then graded my best picks with the scout. It accepted tm_devices #417 in both grading runs. I also considered pytorch #74602, which the scout accepted too, but no maintainer had confirmed it was a bug rather than intended behavior, and llm4s #1529, which I never got graded because that run hit my spend limit.

I chose #417 because it is Python, so I can focus on the contribution instead of a new toolchain. The maintainer had also already settled the design: deprecate `standalone` with a `DeprecationWarning` now and remove it in v4.0. nfelt14 answered my question within two hours and assigned the issue to me five days later. An earlier PR for it (#633) had been closed by its author without being merged and a stale WIP label was still on the issue, so I asked whether it was open before claiming. My claim comment: https://github.com/tektronix/tm_devices/issues/417#issuecomment-6330861761.

After I patched the scope check, a regrade accepted pytorch #74602 (moderate) and airflow #63374 (ambitious), and rejected #417 on one check only, "Nobody already on it", because the assignee, the open PR and the claim comment are all mine. A rejected issue gets no difficulty note, so the note for #417 is mine, not the scout's: moderate. The issue is two sentences that name the change but no files, and my PR ended up touching the config options, the device manager, the config parser, tests and docs. I want to learn a real maintainer review workflow (CLA, changelog, conventional commits, CI), how to change a public config API without breaking existing users, and how to test inside a mature codebase with tox, pre-commit and coverage gates.

My read on the scout is mixed. It caught things I would have missed or gotten wrong: open PRs and claims hidden in comment threads, beets' policy against AI on good first issues (after I patched the AI-policy check), and an Airflow bug that a commenter said no longer reproduces. But searching GitHub at large, it could not narrow the field by itself. Its queries surfaced brand-new, near-empty repos until I changed them. Each scan grades only the top five, by design, to keep cost down, so I screened the site by hand with `gh` to choose what was worth grading. Even then, my hand screening missed claims worded like "I'd like to have a go," so the scout's own read of the thread is the real check. The WIP label on #417 was a judgment call the rubric could not make, so I settled it by asking the maintainer. Next time I would add a preferred check for maintainer activity on good first issues, and I would grade picks from the site directly instead of relying on scans.

The scope patch changed how the scout treats an open edge in an issue. The old scope check rejected the issue. The new `scope-feasible` check rejects only an issue that is not one piece of work, and anything else gets a difficulty note. The old check was also what had rejected airflow #63374, for two closed PRs and a comment saying the bug no longer reproduces. The new check alone would have accepted it with no warning, so I moved those two signals into the "ambitious" note, and the regrade accepted airflow with that note. I have not rerun my unit 1 gold-label check on the patched rubric, so I can't say its agreement with the labels held.

**Toolkit**

- Tool: issue-scout (my search strategy and rubric), run as `issue-scout: run a scan` twice and `issue-scout: grade <urls>` three times, the third after the scope patch, plus my own `gh` screening of the Issue Selection site to choose what to grade
- What it produced: two scans (5 accepted, then 0 accepted after fixes) and three grading runs; tm_devices #417 was accepted in the first two, with notes about the stale WIP label, the closed PR #633, and the CLA requirement. The regrade gave pytorch #74602 and airflow #63374 difficulty notes and rejected #417 only because I now hold it
- Difficulties: scans surfaced low-quality new repos, grading cost limited how many issues I could check, ranking could not see claims or open PRs, my hand screening missed some claim wordings, and one grading run (llm4s #1529) never ran because I hit my spend limit. The regrade took three tries: a non-interactive `claude -p` run was denied reads of the skill folder, a retry with a narrow tool allowlist left two AI-policy checks unclear, and I ran the third interactively. The rubric also has no exemption for my own claim, and a rejected issue gets no difficulty note
- What changed: date-bounded queries, a required 50-star "Repo in use" check, and an AI-policy check that also fails policies barring AI on beginner issues. In unit 6 I replaced the scope check with `scope-feasible` plus a difficulty note, which undid the stricter design-question rule I had added in unit 5. I left the self-claim gap unpatched because one example is thin evidence, and I would still add a preferred check for maintainer activity on good first issues

---

## Understanding the Issue

**Problem Description**

The `standalone` option doesn't say what it does. It only picks the PyVISA-py backend, and a config has no way to name any other VISA library. The issue asks for a new option that takes any VISA backend string, in place of `standalone`.

**Expected Behavior**

A `visa_library` option takes any string PyVISA accepts, such as `"@py"`, `"@ivi"` or the path to a library file. `standalone` keeps working but raises a `DeprecationWarning`, and it is removed in v4.0, as nfelt14 described in the issue.

**Current Behavior**

On `upstream/main`, `DMConfigOptions` rejects `visa_library` with a `TypeError`, and `TM_OPTIONS=VISA_LIBRARY=@py` raises a `KeyError`. `standalone=True` is accepted with no warning. The exact output is under Reproduction Evidence.

**Affected Components**

`DMConfigOptions` in `helpers/constants_and_dataclasses.py`, `DeviceManager.__set_options` and the `visa_library` setter in `device_manager.py`, `DMConfigParser.add_device` in `components/dm_config_parser.py`, the PyVISA-py error text in `helpers/functions.py` and `device_manager.py`, the JSON schema (`tm_devices_config_schema.json`), `docs/configuration.md`, and the tests.

**Toolkit**

- Tool: Claude Code, which I asked to explain the issue and how the config and VISA-library code in tm_devices fits together
- What it produced: explanations of what the issue asks for and where `standalone` is handled, plus the lines to read
- Difficulties: the issue is two sentences and names no files, so I checked each pointer against the code and nfelt14's comment myself
- What changed: I used the closed PR #633, which nfelt14 pointed me to, as a reference and wrote my own implementation

---

## Reproduction Process

**Environment Setup**

macOS 15.7.7, Python 3.14.5, pip 26.2.2, PyVISA 1.16.2, tm_devices 3.7.0 at `upstream/main` commit `9e565e7` (2026-10-19). Dependencies come from the Poetry `.venv` I already had in my clone.

I did not run this from my PR branch. I used a scratch export of `upstream/main` (step 1 below) with its `src` first on `PYTHONPATH`, so my changes can't leak in. The script prints `tm_devices.__file__` to show which copy loaded, and it pointed into the scratch export.

Two things on `main` itself are broken locally: `tests/test_afgs.py::test_afg3k` fails, and `tests/test_docs.py` hangs in `mkdocs build`. Neither touches this issue, so I run the suite with `--ignore=tests/test_docs.py` and expect that one failure.

**Steps to Reproduce**

1. Export the base commit: `git archive 9e565e7 | tar -x -C <scratch>/repro-main`.
2. Save this as `repro.py` in that folder. It makes the four calls and records any warnings:

   ```python
   import dataclasses
   import os
   import warnings
   from unittest import mock

   import tm_devices
   from tm_devices.components.dm_config_parser import DMConfigParser
   from tm_devices.helpers.constants_and_dataclasses import DMConfigOptions

   print("loaded from:", tm_devices.__file__)
   print("option fields:", [f.name for f in dataclasses.fields(DMConfigOptions)])

   print("\n[1] DMConfigOptions(visa_library='@py')")
   try:
       DMConfigOptions(visa_library="@py")
   except Exception as e:
       print("  ->", type(e).__name__, e)

   print("\n[2] DMConfigOptions(standalone=True), all warnings recorded")
   with warnings.catch_warnings(record=True) as w:
       warnings.simplefilter("always")
       opts = DMConfigOptions(standalone=True)
   print("  warnings raised:", [f"{x.category.__name__}: {x.message}" for x in w])
   print("  standalone =", opts.standalone)

   print("\n[3] TM_OPTIONS=VISA_LIBRARY=@py through DMConfigParser")
   with mock.patch.dict(os.environ, {"TM_OPTIONS": "VISA_LIBRARY=@py"}, clear=True):
       try:
           DMConfigParser()
       except Exception as e:
           print("  ->", type(e).__name__, str(e)[:300])

   print("\n[4] TM_OPTIONS=STANDALONE through DMConfigParser, all warnings recorded")
   with mock.patch.dict(os.environ, {"TM_OPTIONS": "STANDALONE"}, clear=True):
       with warnings.catch_warnings(record=True) as w:
           warnings.simplefilter("always")
           cfg = DMConfigParser()
   print("  warnings raised:", [f"{x.category.__name__}: {x.message}" for x in w])
   print("  options.standalone =", cfg.options.standalone)
   ```

3. From that folder, run it with a Python that has the project's dependencies: `PYTHONPATH=src python repro.py`. I used my clone's `.venv` and only ran it there.
4. Observed: calls 1 and 3 reject a `visa_library` option, and calls 2 and 4 accept `standalone` with no warning at all.

**Reproduction Evidence**

- **Commit showing reproduction:** none. I ran it against `upstream/main` in a scratch export, not in a commit.
- **Screenshots/logs:**

  ```text
  loaded from: <scratch>/repro-main/src/tm_devices/__init__.py
  option fields: ['standalone', 'setup_cleanup', 'teardown_cleanup', 'verbose_mode', ...]

  [1] DMConfigOptions(visa_library='@py')
    -> TypeError DMConfigOptions.__init__() got an unexpected keyword argument 'visa_library'

  [2] DMConfigOptions(standalone=True), all warnings recorded
    warnings raised: []

  [3] TM_OPTIONS=VISA_LIBRARY=@py through DMConfigParser
    -> KeyError "Invalid configuration options found: ['VISA_LIBRARY']"

  [4] TM_OPTIONS=STANDALONE through DMConfigParser, all warnings recorded
    warnings raised: []
    options.standalone = True
  ```

- **My findings:** the gap is real on `main` today. There is no option that names a VISA library, and `standalone` can be set without any `DeprecationWarning`, so there is no deprecation path yet. Reading the code, not running it: `device_manager.py:1592` turns `standalone` into the `"@py"` backend and nothing else, and the `DeviceManager.visa_library` setter at line 301 stores `standalone = (value == "@py")`, so a saved config can't record any other library. `docs/configuration.md` describes `standalone` only as "use the PyVISA-py VISA backend".

  This is a feature request, so I showed the missing behavior at the config layer only. I did not test against a real instrument or a non-`@py` VISA library. I also ran this after I had built the fix, so it is a retrospective reproduction, not the first step of the work.

**Toolkit**

- Tool: repro-check, run twice on `claim-draft.md` (my posted claim, copied unchanged) and `repro-draft.md`; the reproduction itself ran in a `git archive` export of `upstream/main`
- What it produced: the first run failed "Steps are followable" because `repro.py` was not in the report, and left the conventions check unclear because it could not find `CONTRIBUTING.md`. After I put the full script in the report and gave the grader the file's local path, the second run passed the environment, steps, behavior and conventions checks. It still rejected the package on "Outcome stated honestly", because my claim names no first step
- Difficulties: the claim cannot pass, since it was posted before I wrote the claim rule it breaks, and I did not rewrite it to get a pass. repro-check is built for bug reports, so for a feature request I treated "reproduce" as showing the missing behavior. Run non-interactively, the grader could not read files until I gave it a read allowlist
- What changed: the full script is now in the report. I posted nothing on the issue, and I did not send the follow-up comment repro-check suggested

---

## Solution Approach

**Analysis**

`standalone` is a boolean field on `DMConfigOptions` (`helpers/constants_and_dataclasses.py`). `DeviceManager.__set_options` (`device_manager.py`) turns it into the `"@py"` backend string and nothing else, and the `DeviceManager.visa_library` setter stores `standalone = (value == "@py")`, so any other library is lost when a config is saved. `DMConfigParser.add_device` (`components/dm_config_parser.py`) reads `standalone` to reject USB and GPIB connections under PyVISA-py. The error text in `helpers/functions.py` and `device_manager.py` tells users to set `STANDALONE`, and nothing warns when it is set.

**Proposed Solution**

Add `visa_library: Optional[str]` as the last `DMConfigOptions` field and read it first in `__set_options`, so the order is `visa_library`, then `standalone`, then the `TM_DEVICES_VISA_LIBRARY` environment variable and the default. Warn with a `DeprecationWarning` from `DMConfigOptions.__post_init__` whenever `standalone` is not None. Make the setter write `visa_library` and clear `standalone`, so users who never set `standalone` don't get the warning. Make the USB and GPIB check cover both options. I am not removing `standalone`, which waits for v4.0, and I am not adding logging for the deprecation, only `warnings.warn`. The files in `tests/samples/` keep `standalone: true` on purpose, to test the deprecated path.

**Implementation Plan**

I wrote this plan after building the fix, from the diff and my notes, so the plan and the code agree. The deviations below are where the build differs from what I first planned or told the maintainer.

1. Add the `visa_library` field to `DMConfigOptions`, mark `standalone` as deprecated in its description and docstring, and add the field to `tm_devices_config_schema.json`.
2. Warn in `DMConfigOptions.__post_init__` when `standalone` is not None.
3. Change `DeviceManager.__set_options` to check `visa_library` first, with a TODO to remove the `standalone` branch in v4.0, and change the `visa_library` setter.
4. Change `DMConfigParser.add_device` so the USB and GPIB rejection applies to `visa_library == "@py"` or to `standalone` when `visa_library` is unset.
5. Point the PyVISA-py warning in `helpers/functions.py` and the `get_available_devices()` error in `device_manager.py` at `visa_library`, using `PYVISA_PY_BACKEND`.
6. Add tests in `tests/test_config_parser.py` and `tests/test_device_manager.py`, and update `tests/validate_device_manager_delete.py`.
7. Update `docs/configuration.md`, the `adding_devices_with_env_var.py` example and the CHANGELOG.

Deviations:

- On 2026-10-27 I told nfelt14 the warning would go in `DeviceManager` where `standalone` is read, not in `__post_init__`. They did not answer that question. I put it in `__post_init__` so that `standalone: false` warns too.
- The first commit placed `visa_library` right after `standalone`. Commit `b0a552a` moved it to the end of the dataclass to keep positional arguments stable, after the griffe breaking-change check.
- Review on 2026-11-04 asked for the `PYVISA_PY_BACKEND` constant instead of a hard-coded `"@py"` (commit `d7984f3`), and for one Added entry in the CHANGELOG instead of Added plus Changed (commit `5e06c15`).
- I tried a logger call alongside the warning, but it flooded the output and broke a test that checks stdout, so the PR uses `warnings.warn` only and offers the log message in the description.

**Toolkit**

- Tool: plan-check, run once from my clone on `plan.md` and a draft `plan-comment.md`; earlier, Claude Code told me which lines to target
- What it produced: an accept, with all six checks passing. It also noted that my draft comment pastes no output, leaves out the setter change, and doesn't say the warning moved from `DeviceManager`
- Difficulties: plan-check is meant to run before the build, so on a plan written from the finished diff, an accept shows the plan matches the code, not that it would have steered the work. Its procedure has no step for a missing repro comment, so it took my quoted results as given and could not re-run them
- What changed: nothing in the plan, since it passed on the first run, and I left the comment alone because it stays off the issue. I would add live-mode steps to plan-check's procedure for a missing repro comment and for a plan written after the build

---

## Testing Strategy

Two checks prove the fix. The first is my reproduction steps, rerun on the branch against the `upstream/main` output. Before the fix, `visa_library` raised a `TypeError` and a `KeyError`, and `standalone` raised no warning. On `5e06c15`, `visa_library="@py"` is accepted from both the constructor and `TM_OPTIONS`, and `standalone` raises a `DeprecationWarning` that mentions `visa_library`. The new tests (11 cases) pass with the fix and all fail against the `upstream/main` source.

The second is the repo's own checks, from my manifest. 872 tests and 8 doctests pass, ruff, pylint and pyright are clean, and griffe reports no breaking change. Three failures are not caused by the change: `test_afg3k` also fails on `upstream/main`, local coverage is 98.55% with only AFG files below 100%, and `tests/test_docs.py` had not finished after 150 seconds. One finding I did not fix: `TM_OPTIONS=STANDALONE` raises the warning twice. All of this ran in scratch copies of the branch, and the output is in `test_evidence.md`, which stays on my computer.

**Toolkit**

- Tool: Claude Code, which reran my reproduction and the manifest checks in scratch copies of my branch; I had already run the suite myself while building
- What it produced: the before and after output, the check results, a run showing the new tests fail without the fix, and `test_evidence.md`
- Difficulties: my first pyright run reported 1,311 errors because pyright does not find `.venv` from a fresh terminal. The reproduction also showed the warning fires twice for `TM_OPTIONS=STANDALONE`, and local coverage cannot reach the project's 100%
- What changed: the manifest's pyright command now passes `--pythonpath .venv/bin/python`, and the three known failures sit in its second table. I left the double warning alone, since the plan did not cover it

---

## Implementation Notes

All times are UTC, the way GitHub shows them. My commits carry +05:30, which moves the last four to the next day on my clock. I rebuilt this log from `git log` and the PR timeline after the fact, so the two hurdles that git doesn't record are placed by the commits around them.

**2026-10-22**

I asked nfelt14 whether #417 was open, since #633 was closed and the WIP label was still on. They said it looked open now, and I asked to be assigned.

**2026-10-27**

I was assigned and asked nfelt14 two design questions: should the `DeviceManager.visa_library` setter write `options.visa_library`, and should the warning live in `DeviceManager` or `DMConfigOptions.__post_init__`. They answered neither directly, and pointed me to #633, which they said had the feature basically finished. I decided to use it as a reference and write my own version.

**2026-11-03**

First commit, `d650c92`: the `visa_library` field on `DMConfigOptions`, the `DeprecationWarning` for `standalone`, and the JSON schema entry. I put the field right after `standalone`.

**2026-11-04 (01:29 to 09:21)**

Three commits. `3085e1a` makes `DeviceManager.__set_options` read `visa_library` first and changes the setter to write `visa_library` and clear `standalone`. `893b785` makes the USB and GPIB check in `DMConfigParser.add_device` cover both options. `87f197f` adds the tests across three files. Somewhere between the first commit and the tests, I tried a logger call next to the warning. It flooded the output and broke a test that checks stdout, so I dropped it and kept `warnings.warn`. I did not write down the day.

**2026-11-04 (20:35 to 20:44)**

`b0a552a` moved `visa_library` to the end of the dataclass. Placed in the middle, it shifts every option after it. A griffe run on `d650c92`, done later, reports "Positional parameter was moved" for each of them. `3a2637c` added the docs, the example, the CHANGELOG entries and the updated error text. While writing the docs, mdformat rewrote YAML quotes from `""` to `''`, so I added the file again and recommitted. I did not note the day of that either.

**2026-11-04 (21:11 to 22:52)**

I opened PR #649 at 21:11. nfelt14 asked for `PYVISA_PY_BACKEND` in place of a hard-coded `"@py"`, and for one Added entry in the CHANGELOG instead of Added plus Changed. I did the first in `d7984f3` at 22:28 and the second in `5e06c15` at 22:51, and replied to each. nfelt14 approved after `d7984f3`, and my push of `5e06c15` dismissed that approval as stale.

**2026-11-05**

03:39: the ship-gate hook test stopped `gh pr create --help` with a setup BLOCK, which is the expected result with no PR text. 05:45: the CLA bot confirmed I had signed. 17:24: nfelt14 approved again, and the CI workflows ran: most passed, but `test-docs` failed when `nodeenv` could not parse a Node.js version, and `test-fast (macos)` failed on `test_ping_address`, neither in code I touched. 21:50: a manual ship-gate run on `5e06c15` returned PASS.

**2026-11-06**

01:21: I installed the PR monitor, and `--state` read the PR. After I filled the playbook, the full run at 01:24 stopped on my Claude spend limit, so nothing was drafted.

**Toolkit**

- Tool: Claude Code, which rebuilt this log from `git log`, the PR timeline read with `gh`, and my notes
- What it produced: the dated entries above, with commit times converted to UTC, and a griffe run on my first commit that confirmed why I moved the field
- Difficulties: I did not keep a log while building, so the days of two hurdles are inferred from nearby commits, and my commit times and GitHub's differ by a day for the last four commits
- What changed: all dates are UTC and the log says it was rebuilt afterwards. Next time I would write an entry as each commit lands

---

## Pull Request

**PR Link:** https://github.com/tektronix/tm_devices/pull/649

**PR Description:** The description names the `visa_library` option and the `standalone` deprecation, lists the eleven files the diff touches, and says `Addresses #417`. It has a before/after table for the four reproduction calls, the check results (872 tests, 8 doctests, ruff/pylint/pyright/griffe), the three known local failures, and an AI-use paragraph. The Types of changes and Checklist boxes from the repo template are filled in.

**Maintainer Feedback:**

- 2026-11-04: nfelt14 asked for `PYVISA_PY_BACKEND` instead of a hard-coded `"@py"`, and for one Added CHANGELOG entry instead of Added plus Changed.
- 2026-11-04: I did the first in `d7984f3` and the second in `5e06c15`, and replied on each review thread. nfelt14 approved after `d7984f3`; pushing `5e06c15` dismissed that approval as stale.
- 2026-11-05: the CLA bot confirmed all committers had signed. nfelt14 re-approved at 17:24 UTC. The first-time-contributor workflows had been approved by then and mostly passed; `test-docs` and `test-fast (macos)` still fail, for reasons outside this change: `nodeenv` could not parse a Node.js version (`'0-alpha'`), and `test_ping_address` expected `ttl=` in the macOS runner's `ping` output.

**Status:** Awaiting review (approved on 2026-11-05, not merged yet)

**Toolkit**

- Tool: ship-gate (`check_gate.py` plus the Claude Code hook), run once as the `gh pr create --help` hook test and once by hand on head `5e06c15` with `pr_draft.md`
- What it produced: a setup BLOCK on the hook test (no PR text to check), then PASS on the manual run. The three manifest checks were clean, and pr-precheck passed Fidelity, Tested, Reviewable, Standards and Honesty against `plan.md`, `test_evidence.md` and the draft
- Difficulties: I opened the PR by hand on 2026-11-04, a day before the gate existed, so the PASS audited an open PR and never gated the create. Each run spends about four minutes on the manifest checks before pr-precheck starts, and pr-precheck uses course credit
- What changed: the lint row in `ship-manifest.md` now passes `--pythonpath .venv/bin/python`, and the known-failures table holds `test_afg3k`, the local coverage shortfall and the unfinished `test_docs` run. I left the PR as it was; the gate did not ask for any further code change

---

## Learnings and Reflections

**Technical Skills Gained**

I learned how to deprecate a public option without breaking anyone: keep the old field, raise a `DeprecationWarning` from the dataclass's `__post_init__`, and give the new option precedence. griffe taught me that adding a dataclass field in the middle is a breaking change, because every later positional argument moves. I also learned to test a warning with `warnings.catch_warnings(record=True)`, to reproduce against a `git archive` export of `upstream/main` so my branch can't leak in, and to run pyright from a fresh terminal with `--pythonpath` pointed at `.venv`.

**Challenges Overcome**

My first commit put `visa_library` right after `standalone`, and griffe reported "Positional parameter was moved" for every field after it, so I moved it to the end in `b0a552a`. A logger call next to the warning flooded the output and broke a stdout test, so I kept `warnings.warn` only and offered the log message in the PR instead. mdformat rewrote the YAML quotes in the docs, so I re-added the file and committed again. Pushing the CHANGELOG fix dismissed nfelt14's approval as stale, and a second approval came the next day.

**What I'd Do Differently Next Time**

I built most of my tools after the work they were meant to check. The voice guard came after my claim, the plan after the fix, and the ship-gate after the PR was open, so each one audited instead of steering. Next time I would install the gate and write the plan before the first commit, and keep the Implementation Notes as I go instead of rebuilding them from `git log`. I would also check my Claude spend before a run that needs it, since the limit stopped two of my tool runs.

---

## Resources Used

- [tektronix/tm_devices#417](https://github.com/tektronix/tm_devices/issues/417): nfelt14's comment set the design (deprecate `standalone` now, remove it in v4.0), and nfelt14 answered my questions on the thread.
- [tektronix/tm_devices#633](https://github.com/tektronix/tm_devices/pull/633): the closed earlier PR nfelt14 pointed me to, which I used as a reference for my own version.
- [tm_devices CONTRIBUTING.md](https://github.com/tektronix/tm_devices/blob/main/CONTRIBUTING.md): commit signing, the CLA, the changelog entry and the pre-commit and tox commands my manifest is built from.
- nfelt14's review on [#649](https://github.com/tektronix/tm_devices/pull/649): the `PYVISA_PY_BACKEND` and CHANGELOG comments.
- [griffe](https://mkdocstrings.github.io/griffe/): the breaking-change check that made me move the new field to the end.
