# Toolkit Portfolio

**Student:** Harsh Kumar

## Featured Tools

Three of them (issue-scout, repro-check, ship-gate) visibly changed through use, and the PR monitor covers the stage after the PR is open.

**issue-scout**

**What it is, and the judgment hole I wrote:** Searches GitHub with my `gh` queries, ranks the results, and grades the top 5 on my `rubric.md`. For my real pick, Claude scraped the Issue Selection site's list, I screened it with `gh`, and the scout graded the shortlist.

> Repo in use: Pass if the repo has 50 or more stars on the capture date (live mode: today). Fail below 50, or if the count can't be read

**How it evolved, dated:**

- 2026-10-22: I added date-bounded queries and the required 50-star "Repo in use" check. Additionally, I scoped it to issues that are at least 30 days old and were updated in the last 60 days.
- 2026-10-22: The AI-policy check now also fails a policy that bars AI on beginner issues or limits AI to review.
- 2026-11-05: I replaced "Scope fits a newcomer" with scope-feasible plus a difficulty note, and airflow#63374 was then accepted as "ambitious".

**Evidence:**

```text
Scan 1 (2026-10-22): the top 5 were graded and ALL 5 were accepted, none rejected.
Scan 2 (2026-10-22): ALL 5 REJECTED (discriminating now, but 0 yield).
  open PR #1225 and a claim comment on nutshell#476; open PR #1753 plus two closed
  ones on django-modern-rest#1493; owner handed aquascope#432 to someone with a
  draft PR, and the repo has 30 stars against the 50 floor
```

**repro-check**

**What it is, and the judgment hole I wrote:** Grades a claim comment plus a repro report against my `rubric.md` (five required checks).

> Outcome stated honestly: the claim comment promises only investigation, never a fix or a timeline, before the work is done, and the report's conclusion is exactly as strong as its evidence

**How it evolved, dated:**

- 2026-09-30 (`9b46687`): pkg-19 passed despite promising a fix in 2 days. I made "Outcome stated honestly" grade the claim's promises, dropped the `conda list` clause, and removed duplicate rows. Eval went from 17/20 to 20/20.
- 2026-11-05: On my #417 report, run 1 failed "Steps are followable" because `repro.py` was not in the report. I put the full script in, and run 2 passed it; the package was still rejected on my posted claim.

**Evidence:**

```text
pkg-19 claim comment: "Kindly assign it to me, I will fix it within 2 days guaranteed"
First full run:  agreement: 17/20 scored items  (bar: 18/20: below the bar)
Fourth full run: agreement: 20/20 scored items  (bar: 18/20: PASS)
```

**ship-gate and ship-manifest.md**

**What it is, and the judgment hole I wrote:** Runs my manifest's repo checks, then pr-precheck, before `gh pr create`. I wrote the must-pass table and a dated known-failures table.

> tests/test_afgs.py::test_afg3k | 2026-11-05 | Fails on upstream/main 9e565e7 too (AssertionError: assert '' == 'PyVISA-...'), in a file my PR does not touch.

**How it evolved, dated:**

- 2026-11-05: pyright run from a fresh terminal found no `.venv` and reported 1,311 errors. I added `--pythonpath .venv/bin/python` to the lint row.

```text
before: .venv/bin/pyright                                   1,311 errors
after:  .venv/bin/pyright --pythonpath .venv/bin/python     0 errors
```

**Evidence:**

```text
2026-11-06 03:20 IST, tektronix/tm_devices @ feat/visa-library-option
- verdict: PASS
- Lint and types: ... .venv/bin/pyright --pythonpath .venv/bin/python -> ok (121s)
- Public API breaking changes: .venv/bin/griffe check ... -> ok (39s)
- Honesty [pass]: plan.md Deviations and test_evidence.md plainly name the changed
  warning location, the double DeprecationWarning, the test_afg3k failure, the
  coverage shortfall and the unfinished test_docs.
```

**PR monitor and playbook.md**

**What it is, and the judgment hole I wrote:** Reads my PR's state and drafts my next move. I wrote the four playbook sections from five merged tm_devices PRs (#638, #612, #598, #596, #573), where a maintainer answered within a day each time.

> Approved but not merged, or review stalled after my reply: nudge after 7 working days.
> Bot comments (CI results, Codecov, CLA, Read the Docs) don't count as activity from either side.

**How it evolved, dated:**

- 2026-11-06: `--state` called bot comments review feedback. I added the playbook rule that bots don't count. The full run then hit my spend limit, so it drafted nothing.

**Evidence:**

```text
$ monitor.py --state   (PR #649, 2026-11-06)
- review decision: APPROVED
- state: FEEDBACK-IN: review feedback is in (latest from the thread: comment under a day ago)

$ monitor.py
pr-monitor: STOP. the drafting pass could not complete (claude exited 1: You've hit
your individual spend limit ...). Nothing was drafted and nothing was posted
```

## Inventory

- issue-select (unit 1, `7abeffb`, eval 18/20): grew into issue-scout in unit 5.
- plan-check (unit 3, `e18164a`, eval 19/20): accepted my #417 plan 6/6, but on a plan written after the build.
- pr-precheck (unit 4, `baedb66`, eval 19/20): runs inside the ship-gate; passed 5/5 on PR #649.
- voice guard and voice-guide.md (unit 6): installed after my claim and PR; on a late audit it stopped my posted claim; no rule changed.
- CLAUDE.local.md (unit 6): 35 lines for my tm_devices clone, written after the work, so it saved no orientation on #417.

## The Arc

**Beat 1**
Date: 2026-09-30
Friction: repro-check passed pkg-19, whose claim promised a fix in 2 days.
Change: "Outcome stated honestly" now grades the claim's promises; duplicate rubric rows removed.
Result: eval rose from 17/20 to 20/20.

**Beat 2**
Date: 2026-10-22
Friction: scan 1 accepted all 5 issues; 4 sat in repos with 23 or fewer stars.
Change: date-bounded queries and a required 50-star "Repo in use" check.
Result: scan 2 rejected all 5, each on a named open PR, claim or star count.

**Beat 3**
Date: 2026-10-22
Friction: beets' AI policy bars AI on good first issues, and my AI-policy check would have passed it.
Change: the check now fails policies that bar AI on beginner issues or limit AI to review.
Result: none

**Beat 4**
Date: 2026-10-22
Friction: the scans gave nothing claimable, and the pick had to come from the Issue Selection site.
Change: screened the site's list with `gh` and graded the shortlist with the scout.
Result: tm_devices#417 accepted in two grade runs; claimed 2026-10-22, assigned 2026-10-27, PR #649 opened 2026-11-04 and approved 2026-11-05.

**Beat 5**
Date: 2026-11-05
Friction: "Scope fits a newcomer" rejected issues just for an open design edge.
Change: scope-feasible plus a difficulty note.
Result: grade run 4 accepted airflow#63374 as "ambitious".

**Beat 6**
Date: 2026-11-05
Friction: pyright from a fresh terminal reported 1,311 errors.
Change: `--pythonpath .venv/bin/python` in the manifest's lint row.
Result: ship-gate PASS on `5e06c15`, 2026-11-06 03:20 IST.

**Beat 7**
Date: 2026-11-05
Friction: repro-check failed my #417 report on "Steps are followable"; `repro.py` was missing.
Change: put the full script in the report.
Result: run 2 passed the steps check.

**Beat 8**
Date: 2026-11-06
Friction: the PR monitor read bot comments on #649 as review feedback.
Change: playbook rule that bot comments don't count.
Result: none

## Limitations and What's Next

My tools ran after the work they check: the voice guard after my claim, the plan after the fix, and the ship-gate after the PR was open. The spend limit stopped two runs, grade run 3 and the monitor's draft.

Next: the ship-gate compares `pr_draft.md` with the `gh pr view` body and blocks on a mismatch, and the monitor skips `[bot]` authors before it picks the state.

**Tool limits.**

issue-scout: no exemption for my own claim; it rejected #417 after I claimed it.
repro-check: built for bug reports; for my feature request I had to treat "reproduce" as showing the missing behavior.
ship-gate: pr-precheck grades `pr_draft.md`, not the PR body actually posted.
PR monitor: counts bot comments as activity, and it never produced a draft for me.
