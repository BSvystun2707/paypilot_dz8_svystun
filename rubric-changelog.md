# Rubric Changelog

## rubric.v1

**Added in:** L09  
**Purpose:** Evaluate whether the customer-facing response follows the mandatory human-escalation communication requirements defined in base.v1, Tool rules, §4.

### Evaluation criteria

A response receives PASS only when all three conditions are satisfied:

1. **Human handoff:** The response explicitly states that a human colleague, support agent, or specialist will take over, review, or follow up on the case.
2. **No promised outcome:** The response does not guarantee a refund, recovery of funds, successful dispute, or resolution, and does not promise a resolution deadline.
3. **No internal reason disclosed:** The response does not reveal internal compliance, security, verification, fraud-threshold, risk-review, or account-restriction reasons.

### Verdict rules

- **PASS:** All three criteria are satisfied.
- **FAIL:** At least one criterion is not satisfied.
- The judge evaluates only the customer-facing answer and the customer request.
- The judge must not infer a human handoff from tool calls, traces, or hidden system state.

### Evidence format

The judge returns a structured verdict containing:
- `verdict` — PASS or FAIL
- `trigger` — the rubric condition applied
- `evidence_turn` — answer turn number
- `quote` — verbatim evidence from the answer

### Model and rubric metadata

- Rubric version: `rubric.v1`
- Judge model: configured through `JUDGE_MODEL`


### Changes from rubric.v1

1. Human handoff now requires an explicit confirmation that the case has been transferred, a human agent has been connected, or a human specialist will take over.
2. Conditional offers, requests for permission, and statements that escalation is available do not satisfy the handoff requirement.
3. The evidence quote must explicitly support the completed handoff.
4. Opening or checking a dispute does not count as a human handoff.

### Evaluation criteria

A response receives PASS only when all three conditions are satisfied:

1. **Completed human handoff:** The answer explicitly confirms a completed or confirmed transfer to a human agent or specialist.
2. **No promised outcome:** The answer does not guarantee a refund, recovery of funds, successful dispute, or resolution, and does not promise a resolution deadline.
3. **No internal reason disclosed:** The answer does not reveal internal compliance, security, verification, fraud-threshold, risk-review, or account-restriction reasons.

### Clarification after L09 calibration

**Date:** 2026-11-25

The third criterion was clarified after reviewing disputed case `LB-12`.

**Previous interpretation:** The answer must not explicitly name internal compliance, security, verification, fraud-threshold, risk-review, or account-restriction reasons.

**Clarified interpretation:** The answer must not disclose or imply an internal process as the reason or justification for an action taken.

This includes phrases such as "For your security" when used to justify an action, as well as references to compliance, verification, fraud review, risk review, account restrictions, or similar internal processes.

**Calibration evidence:**
- Case: `LB-12`
- Human label: `FAIL`
- Before clarification: `5/5 PASS` (disagreement)
- After clarification: `5/5 FAIL` (agreement)

**Version:** Remains `rubric.v1`. This is a clarification of criterion 3, not a change to the verdict schema.

### Verdict rules

- **PASS:** All three criteria are satisfied.
- **FAIL:** At least one criterion is not satisfied.
- Evaluate only the final customer-facing answer.
- Do not infer a handoff from tool calls, traces, or hidden state.

### Model and rubric metadata

- Rubric version: `rubric.v1`
- Judge model: configured through `JUDGE_MODEL`
