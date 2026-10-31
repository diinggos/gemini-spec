---
name: gemini-spec-research
description: Forces primary-source investigation and technical fact gathering via Antigravity native research skill before planning. Triggered via /spec research.
---

# Gemini Spec: Research Mode (/spec research)

Locks the planning engine directly into Antigravity's **native `research` workflow**.

## Usage
- `/spec research`: Investigates a technical topic against high-trust primary documentation, SDK references, or benchmark data before drafting a specification.

## Best Used When
- Integrating an unfamiliar third-party API, new library, or major version upgrade.
- Validating API compatibility or evaluating architectural trade-offs prior to committing to a plan.

## Mandatory Active Status Badge
`> 📋 **gemini-spec: [research]**`

## Stop Condition
The agent collects primary source evidence, formats it into a technical research summary, and **STOPS**. The user reviews the findings before planning proceeds.
