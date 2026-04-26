# Prompt Engineering Portfolio
**Jessica Riggleman** | Systems Architecture · Framework Design · AI Workflow Optimization

---

## About

I design structured prompt systems that turn complex, multi-variable problems into clear, actionable AI outputs. My background is in systems thinking, pattern recognition, and compressed framework design — applied to real-world planning, research synthesis, and decision architecture.

This portfolio documents prompt engineering projects with full methodology: problem definition, prompt design, iteration logs, and output analysis.

---

## Project 1: Multi-Phase Life Architecture System

**Problem:**
Design a comprehensive, multi-phase strategic plan integrating five interdependent domains — environment stabilization, income architecture, identity development, land acquisition, and legacy planning — grounded in real market data, tailored to specific geographic and demographic constraints, and structured for immediate execution.

**Why This Is Hard:**
Most AI outputs for "life planning" produce generic motivational content. This project required the AI to function as a research analyst, financial planner, and systems architect simultaneously — while respecting specific constraints (single parent, rural location, no-degree career paths, no social media exposure, privacy-first requirements).

**Prompt Design Approach:**

*Layer 1 — Context Compression:*
Rather than writing a long, detailed prompt upfront, I front-loaded identity-level constraints in compressed format: location, skill profile, parenting constraints, values (sovereignty, no-exposure income), and output format requirements (binder-ready, print-friendly, checklist-driven). This gave the model a decision filter for every downstream choice.

*Layer 2 — Domain Decomposition:*
I broke the request into five interconnected domains and specified that each needed:
- Concrete timelines (not vague phases)
- Real data (market prices, salary ranges, certification paths)
- Actionable checklists (not narrative advice)
- Internal cross-references between phases

*Layer 3 — Output Specification:*
I specified structural requirements: tables for comparative data, checkbox-format milestones, appendices for resources, and a master timeline showing phase overlap. This forced structured output instead of essay-style responses.

**Iteration Log:**

| Version | Change | Result |
|---------|--------|--------|
| v1 | Initial broad request | Output was generic, motivational, lacked real data |
| v2 | Added geographic constraints + market data requirement | AI pulled real Allegany County land prices, salary data from BLS |
| v3 | Added income filtering rules (no social media, no gig economy) | Eliminated irrelevant suggestions, focused on portfolio-driven paths |
| v4 | Specified output format (tables, checklists, appendices) | Final output matched binder-ready print format |

**Key Techniques Used:**
- Constraint-first prompting (identity/values before task)
- Domain decomposition with cross-referencing
- Output format specification (tables, checklists, appendices)
- Iterative refinement with targeted corrections
- Real-data grounding requirements (forcing the model to source current market data rather than generate plausible estimates)

**Output Metrics:**
- 5 structured phases with overlapping timelines
- 12 data tables with sourced figures
- 30+ actionable checklist items
- 2 appendices (resource list + binder system index


---

## Project 2: System Prompt Architecture — Land Parcel Evaluation Engine

**Problem:**
Build a reusable AI system that takes raw land listing data and returns a structured acquisition recommendation — scored against weighted criteria, flagging deal-breakers, and outputting a buy/pass/investigate verdict. The system must work for any rural land listing without being re-prompted each time.

**Why This Matters:**
Single-use prompts solve single problems. System prompts create tools. This project demonstrates the ability to architect a persistent AI decision-support system — the skill companies actually hire prompt engineers to build.

**System Prompt Design:**

The system prompt was built in four layers:

*Layer 1 — Persona and Role Definition:*
Defined the AI as a rural land acquisition analyst with expertise in Appalachian property markets, regenerative land use, and off-grid feasibility. Set behavioral guardrails: no speculative valuation, no legal advice, flag unknowns explicitly.

*Layer 2 — Input Schema:*
Specified exactly what the user would provide per listing:
- Acreage, price, county, road access type
- Water indicators (creek, spring, well potential)
- Zoning/restrictions (HOA, covenants, easements)
- Terrain and exposure (slope, tree cover, solar orientation)
- Days on market and price history

This standardized input format means any listing can be evaluated without rewriting the prompt.

*Layer 3 — Evaluation Logic:*
Designed a weighted scoring matrix embedded in the system prompt:

| Criterion | Weight | Pass Threshold |
|-----------|--------|----------------|
| Water access/potential | 25% | Must have at least one indicator |
| Price per acre vs. county median | 20% | Within 120% of median |
| No HOA/deed restrictions | 15% | Binary pass/fail |
| Road frontage or deeded access | 15% | Binary pass/fail |
| Buildable (perc test potential) | 15% | Must not be flagged unbuildable |
| Solar exposure | 10% | Southern or mixed exposure |

Built-in deal-breakers that trigger automatic PASS verdict:
- HOA or restrictive covenants present
- No road access and no deeded easement
- Price per acre exceeds 200% of county median
- Landlocked with no water indicators

*Layer 4 — Output Template:*
Forced structured output format for every evaluation:
1. Listing summary (one paragraph)
2. Criterion-by-criterion scoring table
3. Deal-breaker flags (if any)
4. Comparable context (how this listing compares to county market)
5. Final verdict: BUY / PASS / INVESTIGATE FURTHER
6. If INVESTIGATE: specific questions to answer before deciding

**Testing and Edge Cases:**

Tested the system against 8 real Allegany County listings with varied profiles:

| Test Case | Scenario | Expected Verdict | Actual Verdict | Match |
|-----------|----------|-------------------|----------------|-------|
| 1 | 10 acres, creek, no HOA, $28K | BUY | BUY | Yes |
| 2 | 3 acres, HOA, $15K | PASS | PASS | Yes |
| 3 | 15 acres, no water info, $22K | INVESTIGATE | INVESTIGATE | Yes |
| 4 | 40 acres, $180K, remote | PASS (price) | PASS | Yes |
| 5 | 7 acres, spring, steep slope | INVESTIGATE | INVESTIGATE | Yes |
| 6 | 2 acres, paved road, well, $45K | PASS (price/acre) | INVESTIGATE | Partial |
| 7 | 12 acres, timber, no road | PASS (access) | PASS | Yes |
| 8 | 8 acres, southern exposure, creek, $19K | BUY | BUY | Yes |

**Accuracy: 87.5%** (7/8 exact match, 1 partial — system correctly flagged concerns but chose a softer verdict than expected)

**Iteration Log:**

| Version | Issue | Fix |
|---------|-------|-----|
| v1 | Model ignored deal-breakers and gave nuanced verdicts for clear PASS listings | Added explicit "if any deal-breaker is triggered, verdict is PASS regardless of other scores" rule |
| v2 | Output format varied between runs — sometimes narrative, sometimes table | Locked output template with numbered sections and required table format for scoring |
| v3 | Price comparison was vague ("seems reasonable") | Added instruction to calculate exact price-per-acre and compare to provided county median ($9,500/acre) |
| v4 | Edge case — listing with no water data scored 0% on water but still got BUY | Added rule: missing critical data triggers INVESTIGATE, never BUY |

**Key Techniques Demonstrated:**
- Persona-constrained system prompt design
- Weighted decision matrix embedded in prompt logic
- Standardized input/output schema for reusability
- Deal-breaker logic (binary override rules)
- Systematic edge case testing with real data
- Iterative debugging based on output failures

**What I Would Change:**
- Add a confidence score to each criterion (how certain is the model about each data point)
- Build a companion prompt that generates the standardized input from raw listing text (a two-prompt pipeline)
- Test across models to compare verdict consistency — if Claude and GPT-4 disagree on a listing, that signals ambiguity worth flagging
