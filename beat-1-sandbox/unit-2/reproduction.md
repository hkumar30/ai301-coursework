# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of my claim and reproduction on the issue I chose in Unit 1, and of the evaluation
runs that produced `eval-run.txt`.

---

## Your identity upstream

**GitHub username**

hkumar30

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5899834938

```
Claiming this. I'll set up the repo, change a prompt template's content without
bumping its version, and check whether tests/unit/test_prompt_templates.py
currently catches that kind of change. I'll post what I find here before
opening a PR.
```

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5900293660

```
Environment: macOS (Darwin 24.6.0, arm64), Python 3.14.5, pytest 9.1.1, installed
via `pip install -e ".[dev]"` into a fresh venv from a clean clone of my fork at
commit 2f4e82f. No Docker services needed for this test. The project's tooling
config targets Python 3.11 specifically; I'm on a newer minor version, but
nothing in this test touches version-specific behavior.

Steps:
1. Forked and cloned the repo, created a venv, ran `pip install -e ".[dev]"`.
2. Baseline: `pytest tests/unit/test_prompt_templates.py -q`
3. Edited `rag/generator/prompt_templates.py`, adding one line to the
   `skills_feedback` `v1` template's content without touching its version key:

 - tool_proficiency: list of tools used effectively
+- growth_trajectory: brief note on skill growth over time
 """},

4. Re-ran the same test command with no other changes.

Baseline output:
.....................................                                    [100%]
37 passed in 1.05s

After the content change (no version bump):
.....................................                                    [100%]
37 passed in 0.17s

This confirms the issue: the suite does not fail when a template's content
changes without a version bump. Reading `test_template_snapshot_content_hash`
shows why: it computes a real MD5 hash of all template content, but only
asserts `isinstance(content_hash, str)` and `len(content_hash) == 32`. Both
are true for any MD5 hash of any input, so this test can never fail
regardless of what the templates contain. It hashes the content but never
compares that hash against a stored expected value.

Expected (per the issue): a snapshot test that fails when template content
changes without a version bump.
Actual: template content changed, version left at v1, all 37 tests still pass.
```

## Eval iterations

**Run history**

1. Smoke run (`--limit 3`, first rubric draft): `agreement: 3/3 scored items`
2. First full run (five-check rubric, before the honest-cannot-reproduce fix):
   `agreement: 17/20 scored items  (bar: 18/20: below the bar)`
3. `--only pkg-05,pkg-09,pkg-10,pkg-20,pkg-08,pkg-04` (after fixing the honest-cannot-reproduce
   gap and the template-substance wording): `agreement: 6/6 scored items`
4. Second full run: `agreement: 17/20 scored items  (bar: 18/20: below the bar; category floor
   unmet: no match in disclosure)`. I initially read this as model variance, but it turned out
   `rubric.md` had duplicate rows: an old and a new version of two checks were both still in the
   table from earlier edits.
5. `--only pkg-05,pkg-19,pkg-20,pkg-08,pkg-04,pkg-01` (testing a broadened honesty check and a
   stricter disclosure check): `agreement: 5/6 scored items`
6. `--only pkg-05,pkg-20` (after removing an over-strict template-field clause):
   `agreement: 2/2 scored items`
7. Third full run, saved: `agreement: 19/20 scored items  (bar: 18/20: PASS)`. Live-mode testing
   of my claim comment right after this run is what surfaced the duplicate rows directly (the
   skill printed two rows each for two checks), so I deduplicated `rubric.md` down to five rows.
8. Fourth full run, saved with `--save-run eval-run.txt`: `agreement: 20/20 scored items
   (bar: 18/20: PASS)`. This is my submitted run.

**Package analysis**

My rubric rejects pkg-19 (vuejs/core#15205); the gold label also says reject. The repro
report itself is solid: a real environment, a fresh playground reproduction, an artifact
showing the actual CSS output, and a conclusion that matches it. The problem is the claim
comment: "Hello sir! Great project, I love Vue and use it every day... Kindly assign it to
me, I will fix it within 2 days guaranteed... keep this issue reserved for me..." That
promises a fix and a deadline before any investigation has happened, and it is generic
flattery with nothing specific to this issue. My first version of "Outcome stated
honestly" only read the repro report's conclusion, so this package passed by default:
nothing in the rubric was reading the claim comment's own promises. I broadened that check
to grade the claim comment's promises alongside the report's conclusion, which is what
makes this package correctly reject now.

**Check rationale**

"Pass if confidence matches evidence throughout: the claim comment promises only
investigation, never a fix or a timeline, before the work is done, and the report's
conclusion is exactly as strong as its evidence. Fail if the claim comment promises an
outcome or deadline it hasn't earned, is generic boilerplate with no specifics about this
issue, or the report asserts an outcome with no artifact or detail backing it."

I broadened this check after pkg-19 showed a gap: a repro report can be technically
excellent while the claim comment that went up first promises an outcome it has not
earned. Since the claim comment is the first thing a stranger reads on the issue, and
over-promising is what my voice guide treats as a real failure, I folded the
claim comment's promises into this same check. Both are testing the same underlying
thing: whether confidence matches what has actually been done.

**Trade-offs**

This check used to also fail a package if it skipped a maintainer-required template
field (for example, conda's request for `conda list` output), on top of checking
AI-disclosure. That extra clause caused a real false reject: pkg-05's report gave the
conda version and Python version in prose but never touched `conda list`, even though
`conda list` has nothing to do with that bug, and gold says accept. I removed the
template-field clause entirely, since no eval category actually tests for it, only
`disclosure` does. The trade-off: a package that skips a template field for a reason
unrelated to AI-disclosure is no longer caught by this specific check. It would have
to be caught by "Environment recorded" or "Steps are followable" instead, which test
overlapping but not identical ground.

---

Related paths: `eval-run.txt` in this directory; my skill's files in `tools/repro-check/`.
