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

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

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

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

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

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
