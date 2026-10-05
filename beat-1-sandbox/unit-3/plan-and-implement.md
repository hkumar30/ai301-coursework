# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of my plan, the branch I built it on, and the evaluation runs that produced
`eval-run.txt`.

---

## Posted upstream

**GitHub username**

hkumar30

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-6002721176

````
## Diagnosis

`test_template_snapshot_content_hash` (`tests/unit/test_prompt_templates.py`) computes
a real hash of all template content but only checks that it's a 32-character string, so
it can never fail regardless of what the templates contain. The comment left above the
assertion, `# Expected hash - update if templates intentionally change`, shows this
was meant to compare against a stored value and never finished. Confirmed in my earlier
reproduction (https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5900293660):

```
# baseline
.....................................                                    [100%]
37 passed in 1.05s

# after editing skills_feedback's v1 content, no version bump
.....................................                                    [100%]
37 passed in 0.17s
```

## Plan

@FikerK96's idea of keying a stored hash by template name and version covers two gaps
my single-hash draft had: it only tells you something changed, not which template, and
it can't catch a new version added with no recorded baseline. My diagnosis, scope, and
test plan here are built from my own Unit 2 reproduction; what I'm adding on top of
their idea is failure messages that spell out the exact hash to record, so a future
contributor can fix a failure without recomputing anything by hand. (Also answering
your open question: all 5 templates are plain strings, so `.encode()` works directly
on each one.)

```python
EXPECTED_TEMPLATE_HASHES = {
    ("first_impression", "v1"): "ef6429d3a6d426b3c9913381020dd7e4",
    ("gaps_feedback", "v1"): "e5bfd6644fd62a0fe01f60c9aa456762",
    ("presentation_feedback", "v1"): "43549ee59818dfc8eb3627554a563b2e",
    ("projects_feedback", "v1"): "d346d01b24ee7aad92594014a46557af",
    ("skills_feedback", "v1"): "f93103d823482a2e65decc6653e4ee5c",
}

def test_template_snapshot_content_hash(self):
    """Snapshot test: every template version's content hash is recorded and unchanged."""
    for name in sorted(PROMPT_TEMPLATES.keys()):
        for version in sorted(PROMPT_TEMPLATES[name].keys()):
            content_hash = hashlib.md5(PROMPT_TEMPLATES[name][version].encode()).hexdigest()
            key = (name, version)
            assert key in EXPECTED_TEMPLATE_HASHES, (
                f"No recorded hash for {name!r} version {version!r}. "
                f"Add EXPECTED_TEMPLATE_HASHES[{key!r}] = {content_hash!r} "
                "if this is a new, intentional version."
            )
            assert content_hash == EXPECTED_TEMPLATE_HASHES[key], (
                f"{name!r} version {version!r} content changed but its version "
                "key did not. Bump the version if this is intentional, or revert "
                "the content change."
            )
```

In scope: `tests/unit/test_prompt_templates.py` only, this one test and the new dict.
Not in scope: `rag/generator/prompt_templates.py` and every other test in the file.

## Test plan

Before: `pytest tests/unit/test_prompt_templates.py -q` gives 37 passed.
After: same command, same result (every stored hash matches its template).
Then I'll repeat my earlier repro (edit `skills_feedback`'s `v1` content, no version
bump) and confirm the test fails on that specific template. I'll also rename that key
to `v2` with no new dict entry, and confirm the test fails on the missing version too.
Before opening the PR I'll run `make check && make test-unit`.

## A known limitation

Seeing the test fail still doesn't force someone to bump the version instead of just
updating the stored hash at the same key; either response makes the test pass again.

I'll open this on `fix/12-template-snapshot-hashes` on my fork.
````

---

## Your branch

**Branch**

fix/12-template-snapshot-hashes

**Evidence**

Before (Unit 2 baseline, no fix yet):

```
$ pytest tests/unit/test_prompt_templates.py -q
.....................................                                    [100%]
37 passed in 1.05s
```

Edited `skills_feedback`'s `v1` content (added a `growth_trajectory` line), no version
bump, same command:

```
.....................................                                    [100%]
37 passed in 0.17s
```

That confirmed the original bug: no failure despite the content change.

After (same edit, re-run on `fix/12-template-snapshot-hashes` with the fix in place):

```
$ pytest tests/unit/test_prompt_templates.py -q
.........................F...........                                  [100%]
...
E       AssertionError: 'skills_feedback' version 'v1' content changed but its version key did not. Bump the version if this is intentional, or revert the content change.
E       assert 'c8cdae968897...c028171144ad2' == 'f93103d82348...ecc6653e4ee5c'
...
1 failed, 36 passed in 0.17s
```

Reverted the edit, same command:

```
.....................................                                    [100%]
37 passed in 0.17s
```

Back to 37 passed. I also checked the case my first draft couldn't catch: renamed
`skills_feedback`'s `v1` key to `v2` with no new entry in `EXPECTED_TEMPLATE_HASHES`,
same command:

```
E       AssertionError: No recorded hash for 'skills_feedback' version 'v2'. Add EXPECTED_TEMPLATE_HASHES[('skills_feedback', 'v2')] = 'f93103d823482a2e65decc6653e4ee5c' if this is a new, intentional version.
```

Reverted that too, back to 37 passed. `make check` passes (ruff and black clean); `make
test-unit` gives 375 passed, 53 xfailed across the full suite. `mypy` fails on an
unrelated error in numpy's bundled type stubs; I confirmed this by stashing my change
and running `make check` again on unmodified `main`, where the identical error appears,
so it isn't connected to this diff.

## Eval iterations

**Run history**

1. Smoke run, first rubric/procedure/evidence-guide draft, `--limit 5`:
   `agreement: 4/5 scored items` (pkg-03, a `clear-accept` package, failed on Scope).
2. `--only pkg-01,pkg-02,pkg-03,pkg-04,pkg-05`, after narrowing the Scope check to
   production code only: `agreement: 5/5 scored items`.
3. `--only pkg-06,pkg-07,pkg-08,pkg-09,pkg-10`, sampling the remaining categories
   (`scope-creep`, `unbuildable`) before the full run: `agreement: 5/5 scored items`.
4. Full run, saved with `--save-run eval-run.txt`: `agreement: 19/20 scored items
   (bar: 18/20: PASS)`, categories `clear-accept 6/7  scope-creep 4/4
   thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4`. This is my submitted run.

**Package analysis**

My rubric initially rejected pkg-03 (BurntSushi/ripgrep#3222), a `clear-accept`
package; gold says accept. The plan itself was solid: a one-line fix in
`crates/cli/src/decompress.rs` to add a `--` separator before spawning compression
tools, scoped tightly to that one change. The failure was in my own rubric: Scope's
pass condition said any production-code change with no stated file or location counts
as touching something scope doesn't name, and the plan's Test plan line, "Add the
dash-named fixture to the compression integration tests," names no exact file. My
rubric treated that unnamed test fixture the same as an unnamed production change and
failed Scope over it, when a test's exact file is normal to leave unstated and is
already Test plan's job to judge, not Scope's.

**Check rationale**

"Pass if the stated cause explains all the repro evidence, including any step that
isolates or rules out an alternative explanation (e.g., a step with the suspected
component removed from the loop entirely). Fail if the diagnosis contradicts or
ignores any repro step, or adopts a thread comment's theory without checking it
against the repro evidence"

I wrote Diagnosis this way after reading `calib-03.md` (sharkdp/bat#3831): a thread
comment theorizes the delay comes from a pager key-binding bug and cites a real PR, and
the candidate plan adopts that theory. But the package's own accepted repro evidence
shows the delay persists even with the pager fully disabled, tracking only with
syntax-highlighting on or off, which the key-binding theory cannot explain at all. A
diagnosis that merely "matches the issue" can still be wrong if it never gets checked
against the repro steps built specifically to rule an explanation out, so I made that
check explicit rather than leaving "matches the evidence" to mean whatever evidence
happens to support it.

**Trade-offs**

This rubric still rejects pkg-14 (zellij-org/zellij#5174), a `clear-accept` package,
on Scope and Executability. The plan names its two affected crates precisely
(`zellij-server`'s client connection handling, `zellij-client`'s terminal query
issuance) but defers the exact function to a stated, already-working debug trace
rather than naming it outright, since the bug required tracing to localize. My rubric
currently reads "exact function not named" as a Scope and Executability failure
regardless of whether the plan gives a concrete, credible way to find it. Fixing this
would mean loosening both checks, which also decide the `unbuildable` and part of the
`scope-creep` categories (currently 4/4 and 3/3), so I left it as a known miss rather
than risk a flip there without a canary-and-full-run cycle to confirm it, since the
bar and category floor were already met at 19/20.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; my skill's files in
`tools/plan-check/`.
