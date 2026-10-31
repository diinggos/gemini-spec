---
name: gemini-spec-bypass
description: Bypasses all planning workflows for trivial, 1-file, or obvious tasks directly into execution. Triggered via /spec bypass.
---

# Gemini Spec: Bypass Mode (/spec bypass)

Bypasses all planning overhead and interactive interviews, approving the task for immediate execution.

## Usage
- `/spec bypass`: Force immediate execution without generating a blueprint plan or asking questions.

## Best Used When
- Single-line bug fixes, typo corrections, localized configuration changes, or pure conceptual Q&A.
- Tasks where creating a specification document would be an unnecessary bureaucratic overhead.

## Mandatory Active Status Badge
`> 📋 **gemini-spec: [bypass]**`

## Safety Guardrail
If a task has a hidden destructive impact (e.g. dropping database columns, massive deletions), the agent is prohibited from bypassing and will escalate to `/spec plan` or `/spec grill-me`.
