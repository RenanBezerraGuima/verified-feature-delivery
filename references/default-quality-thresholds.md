# Default Quality Thresholds

Use these defaults only when repository policy is missing.
Repository-defined thresholds always take priority.

## Coverage defaults

- new or modified behavior must be covered by automated tests
- touched-line coverage for new code: at least 85%
- touched-branch coverage for new logic: at least 70%
- overall project coverage must not regress

## Static analysis defaults

- zero new high-severity findings on touched code
- zero new medium-severity findings on touched code for High/Critical changes

## Effectiveness signal defaults

Apply at least one:

- mutation score on touched modules: at least 60% (Low/Medium), at least 70% (High/Critical)
- complexity non-regression: no increase above baseline on touched modules
- property-based invariants added for risky decision logic

## Complexity defaults (if no local budget exists)

- cyclomatic complexity per new or modified function: 10 or lower
- cognitive complexity per new or modified function: 15 or lower

## Reliability defaults

- no flaky-test retries counted as PASS for required gates
- required gates must be reproducible with the same commands

## Unknown policy

- UNKNOWN is allowed only for Low/Medium when tooling is unavailable.
- UNKNOWN is never allowed for Critical changes.
