# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment recorded | The repro report's environment record (runtime/library versions, install method), read against the issue's stated target version | Pass if the report names the actual versions or commit used, and they match the issue's target, or the report explains a difference. Fail if no environment is recorded, or a mismatch goes unflagged | required |
| Steps are followable | The repro report's steps, read start to finish | Pass if a stranger with a fresh checkout could run the same steps from a stated starting point to the trigger, with no unstated assumptions ("then I tested it" is not a step). Fail if any step is missing, assumes private context, or skips straight from setup to the result | required |
| Behavior shown matches the issue | The report's pasted artifacts (output, logs, errors), read against the issue's own description of the bug | Pass if the artifact shows the same symptom on the same operation the issue describes, or the report honestly shows it attempted that operation and got a different, actual result (a genuine cannot-reproduce). Fail if a different result is narrated as if it matches the issue, or no artifact or direct comparison is given at all | required |
| Outcome stated honestly | The claim comment's promises and the repro report's concluding claim, each read against what has actually been done or found | Pass if confidence matches evidence throughout: the claim comment promises only investigation, never a fix or a timeline, before the work is done, and the report's conclusion is exactly as strong as its evidence. Fail if the claim comment promises an outcome or deadline it hasn't earned, is generic boilerplate with no specifics about this issue, or the report asserts an outcome with no artifact or detail backing it | required |
| Comments follow repo conventions | The repo-facts block's stated AI-use policy, read against the actual claim comment and repro report wording | Fail only if the policy requires disclosing AI assistance and neither the claim comment nor the repro report contains an explicit statement naming AI-tool use — an excellent, technically perfect report with zero mention of AI still fails here when the policy demands it. Silence in the policy passes | required |

## Verdict rule

Accept only if every required check above passes. Any required check graded fail or unclear holds the package (unclear counts as fail). No preferred checks yet.