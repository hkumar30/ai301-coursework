# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the issue and its thread highlights first, noting any thread theory about the cause and any maintainer-stated template or disclosure asks.
2. Read the repro evidence next, noting every step and its result, including any step that rules out an explanation, not just the ones that confirm one.
3. Read the candidate plan (diagnosis, scope, approach, test plan), noting its stated cause, its in-scope/not-in-scope lines, its first concrete step, and its test plan.
4. Read the candidate plan comment last, since it is graded against everything already read.

## Evidence gathering

- Diagnosis: pull the plan's stated cause and every step and result from the repro evidence block; note which repro steps the stated cause would predict and whether any repro step contradicts it.
- Scope: pull the plan's in-scope/not-in-scope lines and its Changes/approach section's file list; note any production-code change the Changes section touches that scope doesn't name, including one whose location is never stated at all. A new or updated test mentioned without an exact file path does not count against scope on its own.
- Executability: pull the plan's Changes/approach section; note whether its first step is concrete enough to start today, with no missing file, function, or decision only the author could supply.
- Test plan: pull the plan's Test plan section and the repro evidence's steps and artifacts; note whether the test plan's before/after state maps onto a repro step or artifact.
- Comms: pull the plan comment, the thread highlights, and the repo-facts block's contribution policy and template asks; note whether the comment responds to anything in the thread highlights and whether it discloses AI use if the policy requires it.
- Honesty: pull the plan's risks/unknowns language; note whether anything stated as fact is actually an assumption the repro evidence doesn't confirm.

## Check execution

Grade in this order: Diagnosis, Scope, Executability, Test plan, Comms, Honesty. Grade each independently; a fail on one check never changes how you read evidence for another. Grade pass only when the gathered evidence satisfies the check's stated pass condition. Grade fail when the gathered evidence contradicts it. Grade unclear only when the needed evidence is genuinely absent from the package, not because you disagree with a judgment call the plan made; when the plan states its own working assumption and the repro evidence doesn't contradict it, treat that as resolved, not unclear.

## Verdict assembly

Apply the rubric's verdict rule: ready only if every required check grades pass. Any required check graded fail or unclear makes the verdict hold (unclear counts as fail). In the output, quote the evidence for whichever required check failed most directly against the repro evidence as the deciding check. If every required check passes, there is no deciding check to quote. State that plainly, and note the preferred check's result instead, since it's the only thing that could still flag a plan worth a closer look.