# Failure Handling Protocol

Use this protocol when any required gate fails or returns UNKNOWN.

## 1) Identify and isolate

- Identify the failing gate and the exact behavior or module affected.
- Re-run only the failing checks first to confirm reproducibility.
- Avoid changing unrelated code while triaging.

## 2) Remediate in priority order

1. Fix correctness failures first (tests, type errors, high-severity analyzer findings).
2. Fix determinism issues next (flaky tests, timing/race instability).
3. Fix quality-threshold failures (coverage, mutation, complexity).

## 3) Escalate only with explicit risk language

- If a required gate cannot run due to missing tooling, mark status as BLOCKED or UNKNOWN.
- State impact in terms of behavior risk, not tooling inconvenience.
- Propose a concrete follow-up action (for example, "add mutation task to CI").

## 4) Delivery rules

- Do not mark complete while required gates fail.
- Do not silently suppress warnings or relax thresholds.
- Accept delivery with risk only when the client explicitly approves and the evidence report records it.

## 5) Evidence requirements on failure

Include in the report:

- failing command(s)
- first failing output line(s)
- remediation attempts performed
- current status (FAIL, BLOCKED, or UNKNOWN)
- next action owner and timeline
