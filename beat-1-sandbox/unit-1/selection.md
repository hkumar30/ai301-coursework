# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12

**Verdict output**

```
Skill(issue-select)
Successfully loaded skill

I'll start by reading the skill's scope and rubric.

Read 3 files, ran 1 shell command

All three candidates are in the scoped repo. gh isn't installed, let me try the API directly.

Ran 1 shell command

Public and reachable. Gathering repo-level facts and the three issues.

Ran 3 shell commands

No AI ban in the contributing doc. Now the three issues.

Ran 3 shell commands

All three are in the scoped repo (codepath/pathreview-ai301-fa26-s3). Graded independently against rubric.md, then ranked by the fit profile.

Shared repo facts (capture date 2026-09-23): not archived; last push 2026-09-16 (7 days ago); last 5 main commits, three on 2026-09-16 and two on 2026-08-24, all authored by Andrew Burke (Aburke225, COLLABORATOR); no releases ever published; no CONTRIBUTING.md at root, policy lives at docs/CONTRIBUTING.md, which covers branch naming, CI, and xfail markers but says nothing about AI-generated contributions; repo has 0 pull requests of any state. Path Review house rule noted, but moot here: none of the three issues has any comments to apply it to.

Accepted, in fit order

1. #12 - Add snapshot tests for prompt templates (enhancement, good first issue, devops, rag, tests, tier-1)
Best fit: it's the only one of the three labeled rag, and the work snapshot-tests prompt-template content against version bumps, the closest thing on offer to the core-AI/LLM-systems work you want more of, in Python/pytest against a file that already exists (tests/unit/test_prompt_templates.py, HTTP 200). Estimated 3-5 hours, one cohesive change, no sub-issue split.

2. #63 - README scorer test fixture too short for its own word count (bug, good first issue, tests, tier-1)
Second: a crisp, fully-specified Python bug with a stated repro (assert 51 > 100), but the AI content is incidental, it's fixture arithmetic, not model or retrieval work.

3. #73 - README and .env.example disagree about which LLM API key env var to use (good first issue, docs, tier-1)
Third: the cleanest and smallest (1-2 hours, two files), but it's a docs/config reconciliation with no engineering substance against your goals. Accepted, just least interesting for you.

Rejected

None.

One note where I'd flag tension rather than override the rubric: the "well-specified" check has no lower bound, so #73 passes at full strength despite being a two-file docs edit. If you want triviality to sink an issue rather than just rank last, that belongs as a new row in the rubric.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "3 of the last 5 main commits are dated 2026-09-16, 7 days before the 2026-09-23 capture date, authored by Andrew Burke (COLLABORATOR)"},
      {"name": "Active repo", "grade": "pass", "evidence": "pushed_at 2026-09-16 (7 days ago) and archived=false; no releases exist, but the push signal satisfies the 90-day condition"},
      {"name": "AI-contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md covers branching, CI and xfail markers but states no AI ban; no AI_POLICY.md, AI_USAGE_POLICY.md or AGENTS.md in the repo"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Body names one file (tests/unit/test_prompt_templates.py, confirmed present) and '3-5 hours'; zero comments, so no design debate, no split proposal, no core-internals warning"},
      {"name": "Nobody already on it", "grade": "pass", "evidence": "assignees NONE, 0 comments, timeline shows only 6 'labeled' events with no cross-reference or connected PR, and the repo has 0 PRs total"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/63",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "3 of the last 5 main commits are dated 2026-09-16, 7 days before the 2026-09-23 capture date, authored by Andrew Burke (COLLABORATOR)"},
      {"name": "Active repo", "grade": "pass", "evidence": "pushed_at 2026-09-16 (7 days ago) and archived=false; no releases exist, but the push signal satisfies the 90-day condition"},
      {"name": "AI-contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md covers branching, CI and xfail markers but states no AI ban; no AI_POLICY.md, AI_USAGE_POLICY.md or AGENTS.md in the repo"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Concrete change to one test with a stated repro ('pytest tests/unit/test_readme_scorer.py -q' -> observed: assert 51 > 100); no debate or split proposal"},
      {"name": "Nobody already on it", "grade": "pass", "evidence": "assignees NONE, 0 comments, timeline shows only 4 'labeled' events with no cross-reference or connected PR, and the repo has 0 PRs total"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73",
    "checks": [
      {"name": "Maintainer alive", "grade": "pass", "evidence": "3 of the last 5 main commits are dated 2026-09-16, 7 days before the 2026-09-23 capture date, authored by Andrew Burke (COLLABORATOR)"},
      {"name": "Active repo", "grade": "pass", "evidence": "pushed_at 2026-09-16 (7 days ago) and archived=false; no releases exist, but the push signal satisfies the 90-day condition"},
      {"name": "AI-contribution policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md covers branching, CI and xfail markers but states no AI ban; no AI_POLICY.md, AI_USAGE_POLICY.md or AGENTS.md in the repo"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Body names two files (README.md, .env.example) and '1-2 hours' to make them agree; zero comments, so no debate, split proposal or core-internals warning"},
      {"name": "Nobody already on it", "grade": "pass", "evidence": "assignees NONE, 0 comments, timeline shows only 4 'labeled' events with no cross-reference or connected PR, and the repo has 0 PRs total"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

**Run history**

1. First smoke run, three issues, rubric had three checks: `agreement: 2/3 scored items`
2. Ran just issue-01, after adding the Scope and Nobody-already-on-it checks:
   `agreement: 1/1 scored items`
3. First full run with the five-check rubric:
   `agreement: 17/20 scored items  (bar: 18/20: below the bar)`
4. Ran issue-15, issue-19, and issue-20 again after writing a fix to the Scope check.
   I forgot to save the file, so this run used the same rubric as run 3 by mistake:
   `agreement: 1/3 scored items`
5. Ran the same three issues again after actually saving the fix:
   `agreement: 2/3 scored items`
6. Final full run, saved with --save-run to eval-run.txt:
   `agreement: 18/20 scored items  (bar: 18/20: PASS)`

**Issue analysis**

My rubric rejects issue-15 (zulip/zulip#19589), and the gold label agrees: reject. On
the surface the issue looks open and free, since the repo-facts block lists "this
issue: assignees: none; linked PRs: zulip/zulip#20840 (closed); zulip/zulip#23123
(closed)", both already closed. My first version of the "Nobody already on it" check
would have passed it for exactly that reason. But the comment thread has 97 comments
from 2021 to 2024, and the same pattern repeats: a contributor writes "@zulipbot
claim", and about two weeks later zulipbot replies "you have been unassigned from this
issue because you have not updated this issue or any referenced pull requests for over
14 days." That cycle happens at least seven times across different contributors. That
history shows the issue is harder than the empty assignee box suggests, which matches
the "age and history" signal the evidence guide names. I added a rule to the "Scope
fits a newcomer" check that flags repeated claim-and-abandon cycles and multiple
closed, unmerged pull requests. That change turned this issue from a wrong accept into
the correct reject.

**Check rationale**

"Fail if the issue explicitly proposes breaking the work into multiple separate
issues/PRs, the thread shows active unresolved design debate, a maintainer says the fix
touches core internals, it's a usage/support question rather than a concrete change, or
the thread shows 2 or more distinct people having claimed and then been
auto-unassigned/gone silent, and/or 2 or more closed-unmerged PR attempts on the same
issue (real difficulty beyond its apparent scope). A checklist of concrete steps or
files within ONE cohesive change is not an umbrella issue by itself — pass it. Otherwise
pass, regardless of how terse the writeup is"

I wrote it this way because one stale claim comment or one abandoned pull request is
normal, and it should not sink an otherwise good issue. A pattern of repeated attempts
is harder to explain away than a single stale comment, and it does not depend on my own
sense of how hard the issue looks.

**Trade-offs**

This check only fires when there is real claim or pull request history to read, so it
cannot catch a difficulty signal on an issue with no history at all. The eval bundle for
issue-20 (excalidraw#11811) is captured with "labels: none" and "(no comments)", opened
by "cursor[bot] (NONE)". Nobody has reviewed or asked for this feature at all, which is
a different warning sign than repeated abandonment. My rubric still marks it accept in
the final run ("issue-20  reject  accept   NO    graded accept"), because no check
currently looks for an unvetted, bot-filed issue with zero engagement. That is a case I
know my rubric still misses.

---

## Selection rationale

**Selection rationale**

1. Issue #12 fits my interests and the time I have. It is the only one of the three
   candidates labeled rag, which is closest to the core AI and LLM work I want to get
   better at. It is scoped to about three to five hours against one existing test file.
2. The verdict correctly showed the repo is active, that nobody has claimed the issue,
   and that it is scoped to one file with no design debate going on. What it could not
   weigh was personal fit. Issue #12 touches prompt template and RAG code specifically,
   which is why I ranked it above #63 and #73 even though my rubric accepted all three.
3. I expect moderate difficulty. I will need to learn the project's snapshot testing
   setup and read the existing prompt template code, but the work stays inside one
   file, and it is clear what "done" looks like.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.