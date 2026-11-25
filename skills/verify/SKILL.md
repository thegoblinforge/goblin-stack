---
name: verify
description: Minimal proof that a change works. Runs one positive and one negative scenario on the real artifact and pastes the output. Use before saying a task is done, after a fix or feature, or when asked to verify, prove it works, or test the change.
---

# Verify

Smallest check that proves the change, run for real. Reasoning about code is not verification.

1. **Surface.** Pick the one closest to the user: CLI run, HTTP call (`curl`), test runner, browser, script. Prefer an existing test command if it covers the change.
2. **Positive.** One scenario where intended behavior must happen. Run it. Paste command + key output.
3. **Negative.** One scenario that must fail or be rejected correctly: bad input, old bug path, forbidden action. Expect a clear error, a rejection, or unchanged state. Run it. Paste command + key output.
   For a bug fix, the negative is the original repro, which must now behave correctly; show it failing before the fix when you can.
4. **Verdict.** VERIFIED only if both ran and matched expectation. Couldn't run, wrong surface, or ambiguous output → INCONCLUSIVE; say what's missing. Don't hide a failure.
5. **Keep it.** Repo already has tests (`test_*`, `*_test.*`, `*.spec.*`, `tests/`) → save both scenarios as tests in its existing style, next to similar ones, and run them. New behavior with no test covering its surface (e.g. CLI exit codes) → add one for that surface. Reason: next change reruns it for free. No test setup in repo → skip; don't add a framework. Note in report which test file holds them.

No feature maps, no live-session drivers, no formal models. Need more than two scenarios → add only the edge that the change itself touches.

**Report:**
```
verify: VERIFIED | NOT VERIFIED | INCONCLUSIVE
+ <positive cmd> → <observed>
- <negative cmd> → <observed>
tests: <file> | none (no test setup)
```
