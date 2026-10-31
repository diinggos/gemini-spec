# 📋 GEMINI-SPEC

> **The Unified Planning & Scoping Orchestrator for Google Antigravity**

[![Antigravity Compatible](https://img.shields.io/badge/Antigravity-Plugin-4285F4?style=flat-square&logo=google)](https://github.com/diinggos/gemini-spec)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](LICENSE)

**`gemini-spec`** unifies Antigravity's built-in planning workflows (`/grill-me`, `/plan`, `research`, and `bypass`) into a single, cohesive planning router triggered via **`/spec`**.

Instead of guessing whether you should type `/grill-me`, `/plan`, or research docs manually, `/spec` automatically evaluates your task's completeness and activates the appropriate native Antigravity workflow—**always stopping for your review before any code is executed**.

---

## 🏛 Architecture Overview

```
                                  [User Prompt Received]
                                             │
                                             ▼
                                    [/spec Auto Mode]
                             (ROUTING & PREPARATION ONLY)
                                             │
            ┌───────────────────┬────────────┴────────────┬───────────────────┐
            ▼                   ▼                         ▼                   ▼
        [bypass]           [grill-me]                  [plan]             [research]
      Trivial tasks,      Ambiguous requirements,   Detailed requirements, Uncharted libraries,
      skip planning       interactive decision tree direct blueprint plan  external docs/APIs
                          interview (/grill-me)     artifact (/plan)       fact gathering
            │                   │                         │                   │
            │                   └────────────┬────────────┘                   │
            │                                │                                │
            │                                ▼                                ▼
            │                     [BLUEPRINT PLAN ARTIFACT]          [RESEARCH SUMMARY]
            │                                │                                │
            ▼                                └────────────────┬───────────────┘
     Ready for direct                                         ▼
        execution                                      ⛔ ALWAYS STOPS ⛔
                                                  MANDATORY HUMAN REVIEW GATE
                                              (Zero automated code execution!)
```

---

## ⚡ The 4 Native Planning Modes

| Mode | Trigger Signals | Routed Native Antigravity Workflow | Output Artifact |
| :--- | :--- | :--- | :--- |
| **`bypass`** | Micro-tasks ($\le 2$ files, typos, local configs, conceptual Q&A). | Bypasses planning overhead; ready for direct execution. | None (Immediate response). |
| **`grill-me`** | Complex or new features with **abstract / ambiguous requirements** (unresolved architectural forks). | Triggers native **`/grill-me`** protocol (`ask_question` based on Design Tree Frontier) until all branches are settled $\rightarrow$ automatically synthesizes blueprint plan. | Interactive questions & final blueprint plan. |
| **`plan`** | Complex tasks where **technical specifications are already complete** (schemas, endpoints, and libraries explicitly stated). | Bypasses interview. Directly triggers native **`/plan`** to draft a phased implementation roadmap with checklist `[ ]`. | Phased blueprint plan artifact. |
| **`research`** | Tasks involving **new libraries, unknown third-party APIs, or breaking changes** not yet documented in the local repo. | Triggers native **`research`** skill to collect verified facts from official sources into a markdown artifact before planning. | Technical research summary artifact. |

---

## 🛡️ The Immutable Human Review Gate

> [!IMPORTANT]
> **Mode `auto` in `/spec` ONLY determines which planning workflow to activate. It NEVER executes code automatically.**

1. **Mandatory Stop Condition:** Once a blueprint plan, interview, or research document is prepared, the agent **MUST STOP**.
2. **Zero Stealth Modification:** The agent is strictly prohibited from modifying or creating production files in the background without explicit user review and approval (via chat confirmation or clicking the **Proceed** button).

---

## 🕹️ Slash Commands & Manual Overrides

### 1. Master Control
* `/spec` (or `/spec on` / `/spec auto`): Activates dynamic auto-classification *(default)*.
* `/spec off`: Deactivates `/spec` and returns to standard unrouted behavior.

### 2. Manual Workflow Overrides
* `/spec plan`: Force immediate creation of a structured blueprint plan without interview overhead.
* `/spec grill-me`: Force interactive decision tree interview via native `/grill-me`.
* `/spec research`: Force primary-source technical fact gathering via native `research`.
* `/spec bypass`: Force immediate execution bypass (skip planning).

---

## 📋 Status Badge Protocol

When active, the first line of every response displays the current planning mode:
* `> 📋 **gemini-spec: [AUTO: plan]**`
* `> 📋 **gemini-spec: [AUTO: grill-me]**`
* `> 📋 **gemini-spec: [AUTO: research]**`
* `> 📋 **gemini-spec: [AUTO: bypass]**`

*Composition with other plugins:*
When running alongside `gemini-mode-argon` and `token-saver`:
```text
> 🟢 **gemini-mode-argon [AUTO: engineer] [high]** | 📋 **gemini-spec: [AUTO: plan]**
```

---

## 💡 Real-World Walkthrough Examples

### Example 1: Ambiguous Feature $\rightarrow$ Routes to `grill-me`
> **User Prompt:** *"Build an audit logging system for all admin actions."*

The prompt specifies an abstract goal without technical specifics (storage type, retention policy, async buffering, schema).
```text
> 📋 gemini-spec: [AUTO: grill-me]

[Activates native /grill-me interview using ask_question cards]:
1. Where should audit logs be stored?
   - (Recommended) PostgreSQL dedicated table
   - ElasticSearch / OpenSearch cluster
   - S3 / GCS object storage
2. Should logging be synchronous or asynchronous?
   - (Recommended) Async buffered via background worker
   - Synchronous transactional write
```
*After user answers:* Synthesizes decisions into a final blueprint plan $\rightarrow$ **STOPS for review**.

---

### Example 2: Fully-Specified Feature $\rightarrow$ Routes to `plan`
> **User Prompt:** *"Add an audit log table `audit_logs` (id, user_id, action, ip_address, created_at) via Prisma migration, create an AuditLogger middleware in `src/middleware/audit.ts`, and wrap all `/admin/*` routes."*

The prompt already details the table schema, file paths, ORM, and routes. An interview would be annoying and redundant.
```text
> 📋 gemini-spec: [AUTO: plan]

[Generates structured implementation plan]:
- Phase 1: Create Prisma migration for audit_logs
- Phase 2: Implement AuditLogger middleware with IP extraction
- Phase 3: Bind middleware to /admin router
- Phase 4: Verification test in audit.test.ts

[Presents artifact with interactive Proceed button] -> STOPS for review.
```

---

## 📦 Installation

Clone directly into your Antigravity plugins directory:

```bash
git clone https://github.com/diinggos/gemini-spec.git ~/.gemini/config/plugins/gemini-spec
```

Restart Antigravity or open a new conversation. The plugin will be detected and loaded automatically.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE) - see the LICENSE file for details.
