# Evidence Report Template

Use this report at the end of each behavior-changing task.

```md
Delivery Evidence Report

1) Behavior Contract
- Feature:
- Actor:
- Confirmed Scenarios:
- Assumptions:
- Risk level (Low/Medium/High/Critical):
- Gate profile source (repo policy or default thresholds):

2) Test Work
- New tests:
- Updated tests:
- Removed tests (with reason):
- Happy-path coverage:
- Sad/edge-path coverage:

3) Commands Executed
- <command 1>
- <command 2>
- <command 3>
- Repro context (OS/runtime/tool versions if relevant):

4) Results
- Tests: PASS/FAIL
- Lint/types/static checks: PASS/FAIL
- Coverage policy: PASS/FAIL
- Algorithmic quality gate: PASS/FAIL
- Contract/Integration checks (if applicable): PASS/FAIL

5) Artifacts
- Changed files:
- Coverage summary:
- Static analyzer summary (new high-severity findings):
- Complexity delta on touched modules:
- Mutation/property-testing result:
- Relevant logs or output snippets:

6) Residual Risk
- Known gaps:
- Risk level (low/medium/high):
- Follow-up actions:
- Explicit client risk acceptance (if any):
```

## Reporting rules

- Keep claims tied to executed commands.
- Mark unknowns as unknown; do not infer passing status.
- Call out any skipped checks with reason and impact.
