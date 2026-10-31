---
name: gemini-spec-grill-me
description: Forces interactive decision tree interview via Antigravity native /grill-me before generating blueprint plan. Triggered via /spec grill-me.
---

# Gemini Spec: Grill-Me Mode (/spec grill-me)

Locks the planning engine directly into Antigravity's **native `/grill-me` workflow**.

## Usage
- `/spec grill-me` (or `/spec grill`): Forces an interactive interview to stress-test ideas and resolve open architectural decisions before drafting any plan.

## Operating Protocol
- Employs the native **Design Tree & Frontier** protocol: asks all unblocked decision branches in one round using `ask_question`.
- Automatically checks codebase facts first; asks the user ONLY for architectural or business decisions.
- Interview concludes once the decision frontier is empty, after which the system automatically synthesizes the agreed decisions into a final blueprint plan.

## Mandatory Active Status Badge
`> 📋 **gemini-spec: [grill-me]**`

## Stop Condition
The interview questions or final synthesized plan are presented to the user. The agent **MUST STOP** and wait for user answers or approval before touching code.
