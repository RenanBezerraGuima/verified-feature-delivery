# Behavior Framing Intake

Use this intake before coding. Treat the human as the client requesting a feature.

## 1) Ask these minimum questions

- Who is the actor (user, admin, system, scheduled job, external service)?
- What context or preconditions must already be true?
- What event triggers the behavior?
- What observable outcome means success?
- What should happen on invalid input, missing permissions, timeouts, or empty data?
- What non-functional constraints apply (performance, accessibility, security, compliance, cost)?
- What should never happen (data loss, duplicate charge, stale state, unsafe side effects)?
- Does this behavior touch auth, billing, PII, schema, or external contracts?

## 2) Produce a behavior contract

Use this exact structure:

```md
Behavior Contract
- Feature:
- Actor:
- Preconditions:
- Trigger:
- Expected Outcome:
- Edge/Failure Outcomes:
- Non-Functional Constraints:
- Out of Scope:
- Assumptions:
```

## 3) Convert to executable examples

Represent each critical behavior with acceptance examples:

```gherkin
Scenario: <short behavior name>
  Given <precondition>
  When <trigger>
  Then <observable outcome>
  And <important constraint or side effect>
```

Add at least:

- one happy-path scenario
- one sad-path scenario
- one boundary scenario for risky logic

## 4) Confirm before implementation

Confirm with the client:

- "These examples represent expected behavior. Confirm or correct."

If confirmation is unavailable, proceed with explicit assumptions and mark risk in the evidence report.
