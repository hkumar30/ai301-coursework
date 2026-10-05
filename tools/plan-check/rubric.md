# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis | The plan's stated cause, read against every step of the repro evidence, not just the ones that support it | Pass if the stated cause explains all the repro evidence, including any step that isolates or rules out an alternative explanation (e.g., a step with the suspected component removed from the loop entirely). Fail if the diagnosis contradicts or ignores any repro step, or adopts a thread comment's theory without checking it against the repro evidence | required |
| Scope | The plan's stated in-scope/not-in-scope lines, read against the files or areas its own Changes/approach section actually touches | Pass if every file or area the approach section touches is named in the scope statement, and the plan states at least one thing it will not touch. Fail if the approach touches something the scope statement doesn't mention, or there is no not-in-scope line at all. A production-code change with no stated file or location counts as touching something scope doesn't name; a new or updated test mentioned without an exact file path does not count against scope on its own, since Test plan already covers it. | required |
| Executability | The plan's Changes/approach section | Pass if a stranger could start making the first edit without asking the author anything: a concrete file, a concrete change, and an order of work. Fail if the plan describes the destination but not a first concrete step, or depends on information only the author has | required |
| Test plan | The plan's test plan, read against the repro evidence's steps and artifacts | Pass if the test plan names an observable before/after state that maps onto the repro evidence (reusing its steps or artifacts counts; a brand-new automated test is not required). Fail if the test plan is vague ("verify it works") or doesn't connect to the repro evidence's actual steps or artifacts | required |
| Comms | The plan comment, read against the thread highlights and the repo-facts block's stated contribution policy and templates (including AI-use disclosure, if required) | Pass if the comment engages with anything in the thread that bears on the plan (a competing theory, a maintainer ask) rather than ignoring it, and meets any stated disclosure requirement. Fail if the comment ignores thread content that bears directly on the plan, or misses a stated disclosure ask | required |
| Honesty | The plan's risks/unknowns section, read against what the diagnosis and test plan claim | Pass if stated unknowns are named as unknowns, not smuggled in as settled facts. Never changes the verdict | preferred |

## Verdict rule

Ready only if every required check grades pass. Any required check graded fail or unclear holds the package (unclear counts as fail). The preferred check never changes the verdict; it only flags a plan worth a closer read.