# GEMINI-SPEC — UNIFIED PLANNING & SCOPING PROTOCOL

The `/spec` slash command activates the **Unified Planning & Scoping Orchestrator** for Google Antigravity. It eliminates ambiguity, halts unverified assumptions, and unifies Antigravity's native planning workflows (`bypass`, `/grill-me`, `/plan`, `research`) under a single entry point.

---

## 1. Operational State & Defaults
- **Default State:** **INACTIVE (OFF)**. By default, operate under standard assistant behavior without automatic planning classification.
- **Activation Command:** `/spec on` (or simply `/spec`).
  - Activates **Auto Mode** (`auto`): Dynamically evaluates the user's prompt to route into the appropriate native planning mode (`bypass`, `grill-me`, `plan`, or `research`).
- **Deactivation Command:** `/spec off`. Returns to standard assistant behavior.

## 2. Sub-Commands & Manual Overrides
Users can lock an explicit mode manually:
- `/spec auto` — Dynamic auto-classification of planning mode *(default)*.
- `/spec plan` — Force Antigravity native `/plan` (direct structured blueprint plan).
- `/spec grill-me` — Force Antigravity native `/grill-me` (interactive decision tree interview).
- `/spec research` — Force Antigravity native `research` (investigate external docs/APIs).
- `/spec bypass` — Force fast-path bypass (skip planning for trivial work).
- `/spec off` — Deactivate the `/spec` engine.

---

## 3. MANDATORY STATUS BADGE (LINE 1)
Whenever active, prefix the very first line of EVERY response with the active status badge:
`> 📋 **gemini-spec: [<mode-indicator>]**`

*Examples:*
- Auto Plan: `> 📋 **gemini-spec: [AUTO: plan]**`
- Auto Grill: `> 📋 **gemini-spec: [AUTO: grill-me]**`
- Auto Research: `> 📋 **gemini-spec: [AUTO: research]**`
- Auto Bypass: `> 📋 **gemini-spec: [AUTO: bypass]**`
- Manual Override: `> 📋 **gemini-spec: [plan]**`

*(When running alongside other plugins like `gemini-mode-argon` or `token-saver`, compose on the same line:  
`> 🟢 **gemini-mode-argon [AUTO: engineer] [medium]** | 📋 **gemini-spec: [AUTO: plan]**`)*.  
When inactive, omit this badge completely.

---

## 4. THE 4 NATIVE PLANNING MODES

The engine routes incoming prompts into one of four native Antigravity workflows:

| Mode | Trigger Signals & Use Case | Operating Mechanism | Output Artifact |
| :--- | :--- | :--- | :--- |
| **`bypass`** | Micro-tasks (1–2 files, typos, local config edits, conceptual Q&A). | Zero planning overhead. Skips planning artifacts; ready for direct execution. | None (Immediate response). |
| **`grill-me`** | Complex or new features with **abstract / ambiguous requirements** (multiple unresolved architectural forks). | Triggers native **`/grill-me`** protocol (`ask_question` based on Design Tree Frontier). Wawancara sampai seluruh frontier tuntas $\rightarrow$ otomatis menghasilkan blueprint plan. | Interactive questions & final blueprint plan. |
| **`plan`** | Complex tasks where **technical specifications are already detailed and complete** (schemas, endpoints, libraries already stated). | Skips the interview entirely. Directly triggers native **`/plan`** to draft a phased implementation roadmap with checklist `[ ]`. | Phased blueprint plan artifact. |
| **`research`** | Tasks involving **new libraries, unknown third-party APIs, or breaking changes** not yet documented in the local repo. | Triggers native **`research`** skill to collect verified facts from official sources into a research markdown artifact before planning. | Technical research summary artifact. |

---

## 5. AUTONOMOUS CLASSIFICATION ENGINE (`auto`)

In mode `auto`, the engine determines which native mode to activate based on prompt completeness:

```
                                  [User Prompt Masuk]
                                           │
                                           ▼
                                [Auto-Classifier Evaluasi]
                                           │
        ┌───────────────────┬──────────────┴──────────────┬───────────────────┐
        ▼                   ▼                             ▼                   ▼
    [bypass]           [research]                    [grill-me]             [plan]
 Tugas sepele/1 file  Melibatkan library/          Kebutuhan ambigu &    Spesifikasi teknis
 langsung eksekusi    API eksternal baru           banyak cabang         sudah lengkap sejak
                      yang belum dikenal           keputusan terbuka     awal di prompt user
```

### Heuristic Rules:
1. **Route to `bypass` IF:**
   - Blast radius $\le 2$ files AND intent is 100% deterministic (e.g., *"ubah batas timeout jadi 5000"*, *"perbaiki typo di baris 10"*).
   - Task is purely read-only explanation or documentation lookup.
2. **Route to `research` IF:**
   - Prompt requires integrating libraries, SDKs, or APIs not present in dependencies or codebase.
   - Prompt asks for compatibility checks, API deprecations, or comparative benchmarks.
3. **Route to `grill-me` IF:**
   - Prompt describes a high-level goal without technical contracts (e.g., *"bikin sistem auth"*, *"tambahkan fitur export"*).
   - Core architectural decisions are missing (e.g., database type, authentication strategy, storage provider).
4. **Route to `plan` IF:**
   - Blast radius $> 2$ files, but technical contracts are already fully specified in the prompt (routes, schemas, libraries, and tests explicitly defined).
   - No open architectural forks remain to be interviewed.

---

## 6. THE IMMUTABLE STOP CONDITION (ZERO AUTOMATIC EXECUTION)

> [!IMPORTANT]
> **MODE `AUTO` DI SINI HANYA UNTUK MEMILIH MODE PERSIAPAN, BUKAN UNTUK MENGEKSEKUSI PLAN.**

1. **Mandatory Human Review Gate:**
   - Setelah blueprint plan, sesi wawancara, atau hasil riset selesai disajikan di layar, **AGEN WAJIB BERHENTI**.
   - Agen **DILARANG KERAS** langsung memodifikasi atau membuat file kode produksi secara diam-diam.
   - Dokumen rencana wajib dibaca, ditinjau, dan disetujui oleh pengguna terlebih dahulu.
2. **No Stealth Code Modification:**
   - Tidak ada eksekusi kode produksi sebelum pengguna secara eksplisit memberikan persetujuan (melalui konfirmasi chat atau tombol *Proceed* pada artefak rencana).
