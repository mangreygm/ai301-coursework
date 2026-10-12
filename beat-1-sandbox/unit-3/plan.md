# Plan: fix test_template_snapshot_content_hash

## Diagnosis

`tests/unit/test_prompt_templates.py::test_template_snapshot_content_hash`
computes a real MD5 hash of all template content, but only asserts:

```python
assert isinstance(content_hash, str)
assert len(content_hash) == 32  # MD5 hash length
```

Both of these are true for the MD5 hash of any input whatsoever — an
empty string, one word, or the full template set all produce a
32-character hex string. The test can never fail regardless of what the
templates contain, so it does not actually detect unintended template
changes, despite being named and documented as a snapshot test for that
purpose.

Grounded in my Unit 2 repro: editing `skills_feedback`'s `v1` template
content, without changing its version key, and re-running the suite
produced `test_template_snapshot_content_hash PASSED` both before and
after the edit, with the full suite total unchanged
(`375 passed, 53 xfailed` in both runs).

## Scope

In scope: changing `test_template_snapshot_content_hash` to compare
each template's hash against a stored expected value keyed by
(template name, version), so the test fails when content changes
without a version bump, and when a version is added with no
corresponding stored entry.

Not in scope: any change to the templates themselves, to
`get_template()`, to `PROMPT_TEMPLATES`, or to any other test in the
file.

## Files

- `tests/unit/test_prompt_templates.py` — only this file, only this one
  test function.

## Approach

1. Compute the current hash of each individual template, keyed by
   (template name, version) — not one combined hash.
2. Store these as `EXPECTED_TEMPLATE_HASHES`, a dict mapping
   (name, version) to its expected hash.
3. Replace the test's two weak assertions with two real checks: (a)
   the set of (name, version) keys in `PROMPT_TEMPLATES` exactly
   matches the set of keys in `EXPECTED_TEMPLATE_HASHES` — so a newly
   added version with no corresponding entry fails, rather than
   passing silently; (b) each template's computed hash matches its
   entry in `EXPECTED_TEMPLATE_HASHES`.
4. Update the docstring: a deliberate version bump requires adding a
   new (name, version) entry to `EXPECTED_TEMPLATE_HASHES`. Editing an
   existing version's content without bumping the version will fail
   against that version's existing stored hash.

## Test plan

Re-run my Unit 2 repro steps against the fix:

1. Run `make check && make test-unit` — the updated test should pass
   against the current, unedited templates.
2. Repeat my Unit 2 edit: add a sentence to `skills_feedback`'s `v1`
   content, without touching the version key. Run the suite again —
   `test_template_snapshot_content_hash` must fail against `v1`'s
   existing stored hash in `EXPECTED_TEMPLATE_HASHES`.
3. New case: add a properly versioned `v2` for a template with no
   corresponding `EXPECTED_TEMPLATE_HASHES` entry. The test must fail,
   since the key-set check catches the missing entry — confirming a
   real version bump also requires a deliberate update to this file.
4. Revert both template edits, confirm the suite is green again.

## Risks and unknowns

Keying by (name, version) distinguishes a version bump from a silent
edit at the *same* version — but it cannot stop someone from editing
content and also updating `EXPECTED_TEMPLATE_HASHES`'s entry for that
same (name, version) key, bypassing a version bump entirely. That
requires a human reviewer to notice the diff touches both the template
and its stored hash together without a version change; this fix alone
can't catch it automatically.

## Deviations

None from the plan. Built exactly as planned: EXPECTED_TEMPLATE_HASHES
keyed by (name, version), with both the key-set check and the
per-entry hash check. All three test cases from the test plan were
verified with real output:

- Baseline: 375 passed, 53 xfailed
- Silent edit (skills_feedback v1, no version bump): FAILED —
  "Content for (skills_feedback, v1) changed without a version bump —
  hash mismatch"
- New version with no stored entry (skills_feedback v2): FAILED —
  "Added: {('skills_feedback', 'v2')}"

Both edits were reverted after confirming the failures; final state
is clean (375 passed, 53 xfailed) with only the test file change kept.