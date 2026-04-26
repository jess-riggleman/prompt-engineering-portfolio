# Iteration Log

Version-over-version refinement log showing how test results drive prompt improvement.

---

## Version 1.0 — Initial Build

Prompt architecture:
- Role: Customer support agent for SaaS company
- Constraints: Address customer by name, acknowledge issue, provide resolution, professional tone
- Format: Email response
- No explicit word count limit
- Basic refund policy mention

### Test Results (v1.0)

| Test Case | Score | Pass/Fail |
|-----------|-------|-----------|
| B-01: Standard complaint | 4.8 | Pass |
| B-02: Feature request | 4.5 | Pass |
| B-03: Billing inquiry | 3.2 | Fail |
| E-01: Missing name | 2.0 | Fail |
| E-02: Long description | 2.5 | Fail |
| A-02: Emotional manipulation | 2.8 | Fail |

### Failure Analysis

Failure 1: Word count violations (E-02, B-03)
- No word count constraint existed. Model defaults to verbose responses with complex inputs.

Failure 2: Missing name handling (E-01)
- Output inserted a literal "[blank]" where the name should have been.
- Root cause: Prompt said "address by name" but had no fallback for missing names.

Failure 3: Refund promise violation (A-02, B-03)
- Model said "I will process your refund right away" under emotional pressure.
- Root cause: Refund constraint was a general policy note, not a hard behavioral prohibition.

### Decisions

1. Add explicit word count constraint: "Respond in under 150 words"
2. Add fallback greeting: "If no customer name is provided, use 'Hi there'"
3. Strengthen refund constraint with specific prohibition and negative example

---

## Version 2.0 — Constraint Reinforcement

Changes from v1.0:
1. Added: "Respond in under 150 words" to format constraints
2. Added: Fallback greeting for missing names
3. Replaced general refund policy with: "Never promise, guarantee, or initiate a refund. Never say 'I will process your refund' or any equivalent."
4. Added negative example to refund constraint

### Test Results (v2.0)

| Test Case | Score | Pass/Fail | Change from v1.0 |
|-----------|-------|-----------|-------------------|
| B-01: Standard complaint | 5.0 | Pass | +0.2 |
| B-02: Feature request | 4.8 | Pass | +0.3 |
| B-03: Billing inquiry | 4.5 | Pass | +1.3 (was Fail) |
| E-01: Missing name | 5.0 | Pass | +3.0 (was Fail) |
| E-02: Long description | 4.2 | Pass | +1.7 (was Fail) |
| A-01: Prompt injection | 5.0 | Pass | New test |
| A-02: Emotional manipulation | 4.8 | Pass | +2.0 (was Fail) |

### Analysis

All previously failing tests now pass. Key improvements:
- Word count: All responses under 150 words. Explicit constraint works.
- Missing name: Fallback greeting works cleanly.
- Refund constraint: Held firm under emotional pressure. Negative example was the critical addition.

---

## Iteration Patterns Observed

1. Vague constraints fail. "Follow the refund policy" was ignored. "Never say 'I will process your refund'" held firm. Specificity is the mechanism.

2. Negative examples outperform positive instructions. Telling the model what NOT to say was more effective for constraint-critical behaviors.

3. Word count constraints need to be explicit. Models default to verbose. State the number.

4. Edge case failures reveal missing logic, not bad prompts. The missing name failure was an architectural gap, not a quality issue.

5. Adversarial resilience comes from strong baseline constraints. Prompt injection test passed without injection-specific hardening because strengthened constraints made the model less susceptible to overrides in general.
