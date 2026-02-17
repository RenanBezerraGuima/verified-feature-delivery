# Agent Conversation Protocol

Use this protocol to keep behavior framing and delivery evidence clear for the human client.

## 1) Intake message pattern

Send a short message that asks for behavior details, not implementation:

```md
To implement this safely, confirm behavior:
1. Who triggers this behavior?
2. What must already be true?
3. What exact outcome should be observable?
4. What should happen on invalid input or failures?
5. Any constraints (performance, security, accessibility, compliance)?
```

## 2) Behavior confirmation pattern

Before coding, restate agreed behavior:

```md
Behavior contract to confirm:
- Actor:
- Preconditions:
- Trigger:
- Expected outcome:
- Edge/failure outcomes:
- Constraints:
- Assumptions:
```

## 3) Progress update pattern

During implementation, report status in one sentence:

```md
Status: <current step>. Next: <next gate/check>. Blockers: <none or short blocker>.
```

## 4) Completion pattern

Finish with an evidence-first summary:

```md
Implemented behavior: <short statement>.
Verification:
- Tests:
- Coverage:
- Algorithmic quality:
- Contract/integration checks:
Residual risk:
- <risk or none>
```

## Rules

- Keep messages concrete and auditable.
- Avoid claiming PASS without command evidence.
- Mark unknowns explicitly.
