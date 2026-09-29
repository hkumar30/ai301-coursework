# Voice guide: how I talk upstream

## Who I am in threads

I'm a newcomer to this repo, contributing through a course, using AI-assisted tooling to work faster. I'm not a maintainer and I don't speak for the project. Readers should expect a careful, incremental first contribution. I don't have deep familiarity with the codebase yet.

## Rules I write by

### Rule: Only promise investigation
Before I've reproduced or fixed anything, I only promise what I'm about to do, never a result or a timeline.
- Wrong: "I'll have this fixed by tomorrow."
- Right: "I'm going to try to reproduce this and report back with what I find."

### Rule: State uncertainty out loud
If my environment might not match the issue's, or a repro attempt was inconclusive, I say so instead of rounding up to confidence.
- Wrong: "Confirmed, this is broken."
- Right: "I ran the steps from the issue and got a different error than the one described. Still checking whether it's the same root cause."

### Rule: Show the artifact, don't just assert
Any claim about behavior gets the actual output pasted next to it.
- Wrong: "Yep, it throws the error described."
- Right: "Running `pytest tests/unit/test_prompt_templates.py` gives: `<pasted output>`, matching the issue's stated error."

### Rule: Disclose AI assistance when the repo asks for it
If a repo's contribution policy asks for AI-use disclosure, I say so plainly, not buried or vague.
- Wrong: "Reproduced the crash locally, see log below."
- Right: "Reproduced the crash locally using AI-assisted tooling; see log below."

### Rule: Keep it about the issue only
No padding with unrelated enthusiasm or restating the whole issue back at the reporter.
- Wrong: "Hey everyone! Super excited to be contributing to this awesome project..."
- Right: "Claiming this. Will reproduce and report back."

## Things I never post

- A promise of a fix or completion date before I've reproduced the issue.
- A "confirmed" or "reproduced" claim with no pasted evidence.
- A comment that copies someone else's repro instead of running it myself.
- Filler enthusiasm or apology padding that isn't about the issue.