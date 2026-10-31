---
name: gemini-spec
description: Unified planning and requirement scoping orchestrator for Antigravity. Automatically routes between bypass, native /grill-me, native /plan, and native research. Triggered via /spec [on|off].
---

# Gemini Spec: Master Dispatcher (/spec)

Controls the activation of the **Unified Planning & Scoping Orchestrator** for Google Antigravity.

## Usage
- `/spec on` (or simply `/spec`): Activates **Auto Planning Mode**. Automatically classifies incoming tasks into one of 4 native modes:
  - **`bypass`**: Micro-tasks and trivial edits (skips planning overhead).
  - **`grill-me`**: Ambiguous features requiring interactive decision tree interview before planning.
  - **`plan`**: Fully-specified complex tasks requiring immediate structured blueprint roadmap.
  - **`research`**: Uncharted libraries or external APIs requiring technical fact-gathering.
- `/spec off`: Deactivates `/spec` and returns to standard assistant behavior.

## Sub-Commands & Manual Overrides
- `/spec auto` — Dynamic auto-classification of planning mode *(default)*.
- `/spec plan` — Lock directly into native `/plan` blueprint roadmap generation.
- `/spec grill-me` — Lock directly into native `/grill-me` decision interview.
- `/spec research` — Lock directly into native `research` primary-source fact-finding.
- `/spec bypass` — Lock directly into fast-path execution (skip planning).

## Mandatory Active Status Badge
When active, every response begins with:
`> 📋 **gemini-spec: [<mode-indicator>]**`
*(Default: `> 📋 **gemini-spec: [AUTO: <mode>]**`)*.

## Strict Human Review Gate
Mode `auto` only chooses which planning workflow to activate. Once a plan or research document is generated, the agent **MUST STOP** for user review. No automatic code execution is permitted until the user reads and approves the specification.
