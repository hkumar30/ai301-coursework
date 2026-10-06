# Plan: issue #12 (snapshot test never actually compares content)

## Diagnosis

`test_template_snapshot_content_hash` in `tests/unit/test_prompt_templates.py` (line 191)
computes a real MD5 hash over every template's content, but only asserts
`isinstance(content_hash, str)` and `len(content_hash) == 32`. Both hold for any MD5
hash of any input, so the test can never fail no matter what the templates contain.
The comment directly above the assertions, `# Expected hash - update if templates
intentionally change`, shows the original author meant to compare against a stored
value and never finished it. Confirmed in my Unit 2 reproduction
(https://github.com/codepath/pathreview-ai301-fa26-s3/issues/12#issuecomment-5900293660):

```
# baseline
.....................................                                    [100%]
37 passed in 1.05s

# after editing skills_feedback's v1 content, no version bump
.....................................                                    [100%]
37 passed in 0.17s
```

## Scope

In scope: `tests/unit/test_prompt_templates.py`, specifically
`test_template_snapshot_content_hash` and one new module-level dict placed above it.

Not in scope: `rag/generator/prompt_templates.py` itself (the `PROMPT_TEMPLATES` dict
and `get_template` stay untouched), every other test in the file, and any change to
how template versions are structured or chosen.

## Changes

My first draft used one combined hash over every template's content. @FikerK96's idea
of keying a stored hash by template name and version covers two gaps my single-hash
draft had: a single hash only tells you something changed, not which template, and it
can't catch a new version added with no recorded baseline. Replacing it with hashes
keyed by template name and version instead:

1. Add a module-level dict recording each template version's content hash, confirmed
   against the live `PROMPT_TEMPLATES` dict in my venv:

   ```python
   EXPECTED_TEMPLATE_HASHES = {
       ("first_impression", "v1"): "ef6429d3a6d426b3c9913381020dd7e4",
       ("gaps_feedback", "v1"): "e5bfd6644fd62a0fe01f60c9aa456762",
       ("presentation_feedback", "v1"): "43549ee59818dfc8eb3627554a563b2e",
       ("projects_feedback", "v1"): "d346d01b24ee7aad92594014a46557af",
       ("skills_feedback", "v1"): "f93103d823482a2e65decc6653e4ee5c",
   }
   ```

2. Replace `test_template_snapshot_content_hash`'s body so it checks each template
   version's hash individually:

   ```python
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

3. Nothing else in the file changes.

## Test plan

Before: `pytest tests/unit/test_prompt_templates.py -q` gives 37 passed (Unit 2
baseline).

After adding the new check, the same command still gives 37 passed (every stored hash
matches its template).

Then repeat the exact Unit 2 repro: edit `skills_feedback`'s `v1` content (add the
`growth_trajectory` line) without bumping its version key. The test should then fail
specifically on `("skills_feedback", "v1")`, where previously it passed regardless.
Revert the edit afterward.

New case this design adds: rename `skills_feedback`'s `v1` key to `v2` with no new
entry in `EXPECTED_TEMPLATE_HASHES`. The test should then fail with "No recorded hash
for 'skills_feedback' version 'v2'", confirming the test catches both a stale hash and
an untracked new version.

Before opening a PR: `make check && make test-unit`, per `docs/CONTRIBUTING.md`'s PR
process.

Branch: `fix/12-template-snapshot-hashes` on my fork.

## Risks / unknowns

Seeing the test fail still doesn't force a developer to bump the version instead of
updating the stored hash at the same key; either response makes the test pass again.
That limitation is smaller than my first draft's, which couldn't even detect a new
untracked version.

## Deviations
 
The build matched the plan's design exactly: the same `EXPECTED_TEMPLATE_HASHES`
dict, keyed and valued identically, and the same per-(name, version) check replacing
`test_template_snapshot_content_hash`'s body. Two small differences from the literal
plan, neither changing the design:
 
`make check` ran `black`, which reformatted the file to add one blank line before the
dict (its convention for the blank lines preceding a class definition). The
assertions, dict, and docstring are byte-identical to the plan; only whitespace
changed.
 
The plan's "Before opening a PR" step assumed `make check` would pass cleanly. It
didn't: `mypy` failed on a pre-existing error in numpy's bundled type stubs ("Type
statement is only supported in Python 3.12 and greater"), unrelated to this change. I
confirmed this by stashing the diff and re-running `make check` against unmodified
`main`, where the identical error appears. Per `docs/CONTRIBUTING.md`'s guidance on
CI failures unconnected to a diff, I'm recording it here rather than treating it as
blocking.
 
No change to the diagnosis, scope, or test plan was needed; the only departures were
a formatting pass and a pre-existing environment issue surfaced while following the
plan's own pre-PR check.
 