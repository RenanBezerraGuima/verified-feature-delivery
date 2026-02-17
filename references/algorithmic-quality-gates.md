# Algorithmic Quality Gates

Use this policy to evaluate code quality beyond line coverage.
Pair it with `risk-based-gating-matrix.md` to determine required rigor and with `default-quality-thresholds.md` when repository thresholds are missing.

## Gate set

A behavior-changing task passes algorithmic quality only when all required gates pass.

### Gate A (required): Static correctness

- Run repository static analyzers (lint, type, bug-finders, security analyzers where configured).
- Allow zero new high-severity findings on touched code.

### Gate B (required): One effectiveness signal beyond coverage

Pass at least one of the following:

- mutation testing gate for touched module(s) reaches repository threshold
- complexity budget does not regress on touched module(s)
- property-based tests validate key invariants for touched critical logic

### Gate C (conditional): Boundary confidence

Run contract/integration checks when the change touches external boundaries (DB schema, API contracts, queues, files, auth/session, payment paths).

## Pass/fail policy

- Mark PASS only when Gate A and Gate B pass, and Gate C passes when applicable.
- Mark FAIL when any required gate fails or cannot be verified.
- Mark UNKNOWN only when tooling is unavailable; include explicit risk and follow-up action.
- For Critical risk changes, do not allow UNKNOWN outcomes.

## Minimal fallback when tooling is weak

If mutation or complexity tooling is not configured:

1. Add at least one property-based or invariant-focused test for risky logic.
2. Add one additional edge-path example for each critical behavior.
3. Record follow-up to install proper tooling in CI.

This fallback is temporary and should not replace proper automated gates long-term.
