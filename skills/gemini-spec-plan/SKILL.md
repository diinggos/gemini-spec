---
name: gemini-spec-plan
description: Forces direct generation of structured blueprint plan via Antigravity native /plan without interview overhead. Triggered via /spec plan.
---

# Gemini Spec: Plan Mode (/spec plan)

Locks the planning engine directly into Antigravity's **native `/plan` workflow**.

## Usage
- `/spec plan`: Force immediate creation of a structured implementation plan artifact (`plan.md` / `spec.md`) complete with phased milestone checklists `[ ]` and interactive Proceed button.

## Best Used When
- The prompt already contains complete, explicit technical requirements (schemas, endpoints, libraries, and tests are clearly specified).
- You do NOT want or need an interview (`/grill-me`), but require a clear, reviewable roadmap before execution begins.

## Mandatory Active Status Badge
`> 📋 **gemini-spec: [plan]**`

## Stop Condition
The agent must generate the complete blueprint plan and **STOP**. The user must review the plan before any implementation takes place.
