# Evaluation Rubric

Standardized scoring criteria for evaluating AI prompt outputs. Each dimension is scored on a 1-5 scale with defined anchors.

## Scoring Dimensions

### 1. Accuracy (Weight: Critical)

Does the output contain factually correct, technically sound information?

| Score | Definition |
|-------|-----------|
| 5 | All claims are accurate and verifiable. No factual errors or misleading statements. |
| 4 | Minor imprecision in non-critical details. Core claims are accurate. |
| 3 | One factual error or unverified claim present. Core message is still sound. |
| 2 | Multiple factual errors or significant misleading framing. |
| 1 | Fundamentally incorrect or fabricated information. |

Evaluation notes: Check all numerical claims, technical terms, cause-effect relationships, and citations. Flag hallucinated references separately.

---

### 2. Completeness (Weight: High)

Does the output address all parts of the input request without omitting required elements?

| Score | Definition |
|-------|-----------|
| 5 | Every element of the request is addressed. No gaps or missing components. |
| 4 | All major elements addressed. One minor sub-point underexplored. |
| 3 | Most elements addressed. One significant component missing or superficial. |
| 2 | Multiple required elements missing. Output feels partial. |
| 1 | Output addresses only a fraction of the request or misses the point entirely. |

Evaluation notes: Map each requirement from the input to a corresponding section in the output. Track which requirements have no match.

---

### 3. Format Compliance (Weight: High)

Does the output follow the specified structure, length, and formatting rules?

| Score | Definition |
|-------|-----------|
| 5 | Exact match to all format specifications. Length, structure, and style are correct. |
| 4 | Minor deviation. Structure is correct. |
| 3 | One structural deviation from format spec. Output is still usable. |
| 2 | Multiple format violations. Output requires reformatting before use. |
| 1 | Format is ignored entirely. Output does not resemble the requested structure. |

Evaluation notes: Compare output against each format constraint individually. Note which constraints were met and which were violated.

---

### 4. Tone and Voice (Weight: Medium)

Does the output match the specified tone, audience level, and communication style?

| Score | Definition |
|-------|-----------|
| 5 | Tone is perfectly calibrated to the target audience. Voice is consistent throughout. |
| 4 | Tone is appropriate with minor inconsistencies. Audience level is correct. |
| 3 | Tone is generally appropriate but shifts in places. Some audience mismatch. |
| 2 | Tone is noticeably wrong for the audience. Inconsistent voice. |
| 1 | Completely wrong tone. Output would confuse or alienate the target audience. |

Evaluation notes: Identify the target audience and expected tone before scoring. Check for jargon level, formality, and consistent register.

---

### 5. Constraint Adherence (Weight: Critical)

Does the output respect all explicit constraints and prohibitions defined in the prompt?

| Score | Definition |
|-------|-----------|
| 5 | All constraints are respected. No prohibited content, behaviors, or patterns. |
| 4 | All explicit constraints respected. One implicit expectation unmet. |
| 3 | One explicit constraint violated, but the violation is minor and non-critical. |
| 2 | Multiple constraint violations. Output includes prohibited content or behaviors. |
| 1 | Constraints are systematically ignored. Output does the opposite of what was specified. |

Evaluation notes: List every constraint from the prompt. Check each one individually. Constraint violations are weighted more heavily than other dimensions because they indicate the prompt logic is failing.

---

### 6. Edge Case Resilience (Weight: Medium)

How well does the output handle unusual, ambiguous, or adversarial inputs?

| Score | Definition |
|-------|-----------|
| 5 | Handles all edge cases gracefully. Fails safely when input is truly out of scope. |
| 4 | Handles most edge cases. One minor failure mode under extreme conditions. |
| 3 | Handles standard edge cases. Fails on more complex or ambiguous inputs. |
| 2 | Fails on common edge cases. Output degrades significantly with non-standard input. |
| 1 | Any deviation from expected input causes failure or nonsensical output. |

Evaluation notes: Edge case resilience can only be scored after running the edge case and adversarial sections of the test suite.

---

## Composite Scoring

Calculate the composite score using weighted averages:

| Dimension | Weight |
|-----------|--------|
| Accuracy | 25% |
| Completeness | 20% |
| Format Compliance | 20% |
| Tone and Voice | 10% |
| Constraint Adherence | 15% |
| Edge Case Resilience | 10% |

### Threshold Definitions

| Composite Score | Rating | Action |
|----------------|--------|--------|
| 4.5 - 5.0 | Production Ready | Deploy with monitoring |
| 3.5 - 4.4 | Needs Polish | Minor iteration before deployment |
| 2.5 - 3.4 | Needs Rework | Significant prompt revision required |
| 1.0 - 2.4 | Failed | Redesign the prompt architecture |

---

## How to Use This Rubric

1. Read the prompt and identify the use case, target audience, format spec, and all constraints
2. Run the prompt with a test input and capture the output
3. Score each dimension independently — do not let a strong score in one area inflate another
4. Write a brief justification for each score explaining why you chose that number
5. Calculate the composite score and determine the action threshold
6. Log results in the iteration log for version tracking
