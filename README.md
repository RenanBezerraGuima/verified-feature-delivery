# verified-feature-delivery

`verified-feature-delivery` is a Codex skill for building or changing software with verifiable correctness. It combines behavior framing with the human client, TDD implementation, and explicit quality gates with evidence reporting.

## What It Includes

- `SKILL.md`: core workflow and guardrails
- `agents/openai.yaml`: agent-facing metadata and default prompt
- `references/`: templates and policies for behavior framing, risk classification, quality gates, failure handling, and evidence reporting

## Core Workflow

1. Frame behavior with the client.
2. Classify risk and choose gates.
3. Implement with `Red -> Green -> Refactor`.
4. Enforce quality gates.
5. Publish evidence.
6. Handle failures and unknowns explicitly.

## Usage

Call the skill directly by name:

```text
$verified-feature-delivery
```

Then follow the workflow in `SKILL.md` and use the reference docs for templates and thresholds.

## Repository Scope

This repository stores only the skill definition and supporting references so it can be versioned and published independently.
