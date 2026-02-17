---
name: verified-feature-delivery
description: Build or modify software with demonstrable correctness across any tech stack by using behavior framing with the human client, test-driven development, and explicit quality gates. Use when adding features, fixing bugs, refactoring, reducing regressions, raising test coverage, or working in under-tested legacy code where proof of behavior is required.
---

# verified-feature-delivery

## Overview

Use this skill to turn a human request into verified software behavior. Treat the human as the client, frame requested behavior before coding, implement with TDD, and deliver with test, coverage, and algorithmic quality evidence.
Use `references/agent-conversation-protocol.md` to keep client interactions concise and consistent.

## Workflow

### 1) Frame behavior with the client (BDD intake)

- Ask for behavior, not implementation details.
- Capture a behavior contract with: actor, context, trigger, observable outcome, edge/failure behavior, and non-functional constraints.
- Translate the contract into concise acceptance examples (`Given/When/Then` or equivalent) and confirm the examples with the client before coding.
- State explicit assumptions when details are missing and ask for confirmation.
- Use `references/behavior-framing.md` as the intake template.
- Use intake phrasing from `references/agent-conversation-protocol.md`.

### 2) Classify change risk and plan test strategy

- Classify the change using `references/risk-based-gating-matrix.md`.
- Select the minimum gate profile required by the risk level.
- Prefer the smallest test layer that still proves behavior.

- Use unit tests for logic and invariants.
- Use integration or contract tests for boundaries (DB, API, queue, filesystem).
- Use end-to-end tests only for critical user journeys.
- Add at least one happy-path and one sad-path/edge-path test for each behavior.
- For bug fixes, write a failing regression test first.
- For under-tested legacy code, write characterization tests before refactoring.

### 3) Execute TDD loop

- Run `Red -> Green -> Refactor` for each behavior slice.
- Keep each cycle small and focused on one behavior.
- Write the simplest code that makes tests pass.
- Refactor only with a green test suite.
- Keep tests deterministic by controlling time, randomness, and external services.

### 4) Enforce quality gates

- Run repository-required gates first (tests, lint, types, static analysis, security checks where configured).
- Apply coverage policy.
- If the repository has a threshold, meet it.
- If there is no threshold, avoid regressions on touched modules and add coverage for new behavior.
- Apply algorithmic quality policy from `references/algorithmic-quality-gates.md`.
- If repository thresholds are missing, use `references/default-quality-thresholds.md`.
- Require no new high-severity static analysis findings on touched code.
- Require one additional non-coverage signal for touched logic (especially critical logic): mutation score gate (if configured), complexity budget non-regression, or property-based invariant checks.
- Block "done" status when behavior-changing code has no automated tests.

### 5) Publish evidence

- Report results using `references/evidence-report-template.md`.
- Include behavior contract, risk level, tests added/updated, commands executed, pass/fail outcomes, coverage status, and unresolved risks.
- Use completion phrasing from `references/agent-conversation-protocol.md`.

### 6) Handle failures and unknowns

- Apply `references/failure-handling.md` whenever any required gate fails.
- Keep task status blocked until required gates pass or the client explicitly accepts risk.
- Record every skipped or unavailable check in the evidence report with reason and impact.

## Stack Adapters

Use `references/stack-adapters.md` to map this workflow to common ecosystems. Prefer project-native scripts and CI conventions when available.

## Guardrails

- Do not merge behavior changes without tests unless the client explicitly accepts risk.
- Do not treat high coverage as proof of correctness; verify behavior relevance.
- Do not overuse brittle UI tests when lower-level tests can prove behavior faster.
- Do not mock uncontrolled internals across every layer; keep boundary tests realistic.
- Do not treat analyzer warnings as cosmetic if they indicate correctness risk.

## Definition of Done

Mark work complete only when all items are true:

- behavior contract is confirmed with the client
- tests fail before the change and pass after the change
- quality gates pass for the repository
- coverage policy is satisfied
- algorithmic quality policy is satisfied
- evidence report is delivered
- residual risks and follow-ups are explicit
