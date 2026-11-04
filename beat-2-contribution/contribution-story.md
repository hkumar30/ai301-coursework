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

**Unit 6: [one line on the tool work]**

[2-4 sentences: the voice-guard, the repo-memory file. What broke or
fell short, and what changed because of it. "Nothing broke" counts when
it is true - say how you know.]

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I started with my scout's own scans of GitHub. The first one accepted all five issues, mostly in new repos with almost no stars; after I fixed the queries and added a star floor, the second rejected all five, each for a real reason such as an open PR or a claim. My actual pick had to come from the Issue Selection site, so I screened its Python + good-first-issue list (1,203 issues) with `gh`, cutting dead repos and anything already assigned, claimed or linked to an open PR, then graded my best picks with the scout. It accepted tm_devices #417 in both grading runs. I also considered pytorch #74602, which the scout accepted too, but no maintainer had confirmed it was a bug rather than intended behavior, and llm4s #1529, which I never got graded because that run hit my spend limit. I chose #417 because it is Python, so I can focus on the contribution instead of a new toolchain. The maintainer had also already settled the design: deprecate `standalone` with a `DeprecationWarning` now and remove it in v4.0. And nfelt14 answered my question within two hours and assigned the issue to me five days later. An earlier PR for it (#633) had been closed by its author without being merged and a stale WIP label was still on the issue, so I asked whether it was open before claiming. My claim comment: https://github.com/tektronix/tm_devices/issues/417#issuecomment-6330861761. I want to learn a real maintainer review workflow (CLA, changelog, conventional commits, CI), how to change a public config API without breaking existing users, and how to test inside a mature codebase with tox, pre-commit and coverage gates.

My read on the scout is mixed. It caught things I would have missed or gotten wrong: open PRs and claims hidden in comment threads, beets' policy against AI on good first issues (after I patched the AI-policy check), and an Airflow bug that a commenter said no longer reproduces. But on a real search it could not narrow the field by itself. Its queries surfaced brand-new, near-empty repos until I changed them. Each scan grades only the top five, by design, to keep cost down, so I screened the site by hand with `gh` to choose what was worth grading. Even then, my hand screening missed claims worded like "I'd like to have a go," so the scout's own read of the thread is the real check. The WIP label on #417 was a judgment call the rubric could not make, so I settled it by asking the maintainer. Next time I would add a preferred check for maintainer activity on good first issues, and I would grade picks from the site directly instead of relying on scans.

**Toolkit**

- Tool: issue-scout (my search strategy and rubric), run as `issue-scout: run a scan` twice and `issue-scout: grade <urls>` twice, plus my own `gh` screening of the Issue Selection site to choose what to grade
- What it produced: two scans (5 accepted, then 0 accepted after fixes) and two grading runs; tm_devices #417 was accepted both times, with notes about the stale WIP label, the closed PR #633, and the CLA requirement
- Difficulties: scans surfaced low-quality new repos, grading cost limited how many issues I could check, ranking could not see claims or open PRs, my hand screening missed some claim wordings, and one grading run (llm4s #1529) never ran because I hit my spend limit
- What changed: date-bounded queries, a required 50-star "Repo in use" check, a stricter scope check for design questions left open in the issue body, and an AI-policy check that also fails policies barring AI on beginner issues; I would also add a preferred check for maintainer activity on good first issues

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

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

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
