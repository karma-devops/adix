# NOTES.md — [Insert Directory Node Name] — Notes & Hardening

> Process rules, localized constraints, and active session memory. For structural maps, see `CONTEXT.md`.

---

## 1. [LOCKED] Process Rules & Constraints (ICM Layer 3)

### The Single-Line Execution Loop
1. **THINK:** Evaluate the immediate target intent against the node's `CONTEXT.md` boundaries.
2. **PLAN:** Specify the exact single line to alter and define its verifiable success metric.
3. **SINGLE-LINE EDIT:** Call file modification tools to alter exactly one line of text or code.
4. **VERIFY:** Execute immediate syntax, test, or diff validation on that modified line.
5. **DOUBLE CHECK:** Critique the single change directly against the node's original intent.
6. **NEXT STEP:** Record state and advance to the subsequent single-line milestone.

### Local Execution Constraints
* **The Single-Line Restriction:** Every file modification tool call must alter exactly one line. Modifying multiple lines or files simultaneously is an unrecoverable failure path.
* **Surgical Diffing:** Diffs must be minimal, focused, and precise. Never rewrite adjacent working infrastructure to resolve a localized bug.
* **Document Non-Obvious Decisions:** Log *why* an architectural line deviation occurred, not just *what* was changed.

### Infrastructure Locks
* [Insert directory-specific locked rules, brand vocals, or immutable parameters here]

---

## 2. [NOTED] Working Artifacts & Active Logs (ICM Layer 4)

### Active State Logs
* [YYYY-MM-DD] — [Single-sentence log tracing current run outcomes, errors hit, and live single-line fixes]

### Hardened Lessons (Requires user approval to promote to LOCKED)
* [Edge-case discoveries from this run — promoted to LOCKED only after operator review]
