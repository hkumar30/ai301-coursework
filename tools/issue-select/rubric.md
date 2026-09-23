# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer alive | Last 5 default-branch commit dates/authors, and the maintainer first-response sample | Pass if either signal shows life: at least one of the last 5 default-branch commits is dated within 90 days of the capture date (live mode: today), OR an Owner/Member/Collaborator reply lands within 30 days on any sampled issue. Fail only if both signals are stale | required |
| Active repo | Latest release date, last push, archived flag | A release or push happened in the last 90 days, and the repo isn't archived | required |
| AI-contribution policy | CONTRIBUTING.md / AI policy line | Fails only if AI-generated contributions are outright banned. Rules/conditions are fine. No policy mentioned = fine. | required |
| Scope fits a newcomer | Issue body, full comment thread, and linked-PR history | Fail if the issue explicitly proposes breaking the work into multiple separate issues/PRs, the thread shows active unresolved design debate, a maintainer says the fix touches core internals, it's a usage/support question rather than a concrete change, or the thread shows 2 or more distinct people having claimed and then been auto-unassigned/gone silent, and/or 2 or more closed-unmerged PR attempts on the same issue (real difficulty beyond its apparent scope). A checklist of concrete steps or files within ONE cohesive change is not an umbrella issue by itself — pass it. Otherwise pass, regardless of how terse the writeup is | required |
| Nobody already on it | Assignees box; linked PRs (Development box + PRs mentioned in thread); claim comments in thread, with dates | Fail if an assignee is set, an open PR addressing the issue is linked/mentioned, or someone claimed it within the last 14 days with no sign of abandonment. A closed/unmerged PR or a stale (14+ day, no follow-up) claim does not fail this check | required |

## Verdict rule

Accept only if every check above passes. If a check fails, reject. If a
check is unclear, treat it as a fail. It is better to skip an issue you
can't verify than take one blind.

No "preferred" checks yet. Can add some later (like a good-first-issue
label) to help rank between accepted issues, but they'd never change
accept/reject.
