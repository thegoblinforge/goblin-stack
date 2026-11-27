# Feature

You own design and verification. Delegate only if the edit is big and mechanical.

1. Read affected code (inline; `how` skill if unfamiliar subsystem).
2. Name data shape and organizing structure (Model the Domain). Place each piece in a `code-quality` layer and name the owner of each rule. Sketch types/signatures if crossing a function boundary.
3. Implement. Inline by default; one `goblin-agent` with paths + shape + success check if large and mechanical.
4. `verify` skill on matching surface. Inconclusive or wrong surface = not done, say so.
5. Small ordered commits (Sequence Verifiable Units).
6. `review`, then `pr` playbook if shipping.

**Reply:** what you built and for whom, data shape chosen and why, verify output, open decisions. Table only if real alternatives compared.
