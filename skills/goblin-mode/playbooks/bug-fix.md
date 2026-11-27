# Bug fix

Be scientific. Every shipped line traces to runtime evidence. "Might help" is a hypothesis, not a fix.

1. Reproduce yourself on the same surface the bug shows. Won't fire → tighten conditions or instrument. Ask user only with a specific reason you can't reach it.
2. List candidate causes. Cut the space with the cheapest check that eliminates most. Instrument and read real state; don't guess. Two fixes failed on one premise → Attack the Premise.
3. Fix at root cause (first wrong decision), smallest change the evidence justifies. Revert anything a refuted hypothesis motivated.
4. Verify on same surface: original repro now passes, plus one negative case (`verify` skill). Unit tests alone don't prove absence.
5. Failing repro/test lands before fix in history when a cheap test path exists. Skip if test would be costly or unclear.
6. `review`, then `pr`.

**Reply:** what broke, root cause, fix, how verified. Paste failing-then-passing output.
