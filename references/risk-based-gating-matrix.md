# Risk-Based Gating Matrix

Classify each change before implementation to select the minimum required gate profile.
Base gates from `algorithmic-quality-gates.md` always apply.

## Step 1: Score change risk

Add 1 point for each true condition:

- touches auth, permissions, secrets, PII, billing, legal/compliance logic
- changes API contracts, DB schema, queues, files, or cross-service interfaces
- touches concurrency, retries, caching, idempotency, or ordering logic
- introduces or changes migrations, destructive updates, or irreversible state changes
- modifies under-tested legacy hotspots (high churn, prior defects, weak observability)

## Step 2: Map score to risk level

- 0-1: Low
- 2: Medium
- 3-4: High
- 5: Critical

## Step 3: Apply required gate profile

### Low

- targeted tests for touched behavior
- static/type/lint checks
- coverage non-regression on touched modules
- one non-coverage effectiveness signal (mutation, complexity, or property tests)

### Medium

- all Low gates
- at least two test layers for changed behavior (for example unit + integration)
- boundary contract/integration checks for touched interfaces

### High

- all Medium gates
- full relevant suite for the component/service
- explicit sad-path and recovery-path tests
- security/performance checks when behavior is security/perf sensitive

### Critical

- all High gates
- mandatory mutation or property-based invariant checks on critical logic
- explicit rollback/recovery validation when applicable
- no UNKNOWN gate results allowed for delivery

## Notes

- If repository CI defines stricter policy, CI policy wins.
- If risk is uncertain, classify one level higher.
