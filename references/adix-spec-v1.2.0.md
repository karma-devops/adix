# ADIX: Agent Directory Index
> **Specification Version:** 1.2.0
> **Core Architecture:** Agent Directory Index, Self-Documentation, Phase-Backup Engine, & Skill Architecture Standard
> **Copyright:** © 2026. Released under the [MIT License](../LICENSE). Free to use, modify, and distribute.

---

## 1. System Prompt Bootstrap Protocol

This framework-agnostic instruction block must be appended directly to the agent's core system profile (e.g., `AGENT.md`, `SOUL.md`, `CLAUDE.md`, or environment configuration blocks). It creates an absolute execution gate, preventing any tool use until the local directory context is loaded into memory.

```markdown
**BOOTSTRAP PROTOCOL:** Before invoking any tool or executing any action, you must locate and read the root `CONTEXT.md` of the active project directory structure. The filesystem is the state machine. Every directory node operates as an independent processing boundary governed by a local `CONTEXT.md` (the structural rails) and `NOTES.md` (the memory engine) pair. You are strictly bound by the active directory's localized contract, its documentation update rules, its phase-backup validation loops, and the mandatory **SINGLE-LINE EDIT** constraint: modify exactly one line per tool execution block. Read the root-level `CONTEXT.md` first to initialize your operational boundaries.
```

---

## 2. Structural Traversal Protocol (Read Before Editing)

To guarantee situational awareness and eliminate long-tail context drift, the agent must execute a deterministic traversal sequence before modifying any file:

1. **Identify the Target Surface:** Isolate the exact file or subdirectory marked for modification.
2. **Follow the Path:** Navigate from the project root directly to the target path.
3. **Read the Node Chain:** Read every `CONTEXT.md` and `NOTES.md` pair encountered along the route.
4. **Bind to the Nearest Node:** The closest `CONTEXT.md` governs local processing details and personas, while parent nodes dictate global repository-wide guardrails.

---

## 3. Self-Documentation Protocol (Update After Editing)

Every single-line file modification triggers an automatic **ADIX Closeout Pass**. The agent cannot pass execution to another node or mark a task as complete without externalizing its state changes directly onto the filesystem.

### A. Update Triggers

The nearest owning `CONTEXT.md` or `NOTES.md` must be updated immediately if a single-line edit changes:

* Local directory purpose, operational scope, or assigned persona profile responsibilities.
* Durable node workflows, tool structures, or operational parameter configurations.
* Input definitions, expected outputs, or newly produced file artifacts.
* Subdirectory instantiation, removal, renames, or index hierarchies.

### B. Closeout Execution Steps

1. **Verify Line Delta:** Run a post-execution diff check to ensure the tool call altered exactly one line.
2. **Commit Memory Log:** Append a concise, single-sentence execution summary to the `[NOTED]` section of the local `NOTES.md`.
3. **Re-Index Parent Tree:** If a downstream folder was created, modified, or renamed, immediately update the downstream index inside the parent node's `CONTEXT.md`.
4. **Prune Context Clutter:** Delete stale notes, contradictory rules, and historical conversational padding to minimize token overhead.

---

## 4. The Phase-Backup Engine (AEE Integration)

To prevent catastrophic infrastructure state destruction, ADIX embeds a strict, phase-based snapshotting engine directly into the execution loop. The foundational mandate is clear: **No backup = no edit.**

### A. The Slug Format

All phase-backups must be contained within dedicated subdirectories using a consistent slug format:

```text
(version)_(info-context)_(timestamp)/
```

* **`version`:** `v0`, `v1`, `v2`, etc., incremented sequentially per phase. Number reusing is completely prohibited.
* **`info-context`:** Short, hyphenated text describing the phase scope. Append `_STABLE` in all-caps only after live verification proves the edit works flawlessly.
* **`timestamp`:** Local time format `YYYY-MM-DD_HHMM` representing exact creation time.

*Examples:*

* `backups/v0_pre-native-fix_STABLE_2026-06-01_0057/`
* `backups/v1_hero-background_2026-06-01_0115/`

### B. Core Backup Constraints

* **Copy Before Destructive Overwrites:** The snapshot must be taken *before* any file modification tool runs. Backups generated after an overwrite loop are useless.
* **The `VERSIONING.md` Manifest:** Every backup root folder must contain an explicit indexing manifest tracking current system states, file contents, and known active bugs. Loose files are completely banned from the backups directory root.
* **Tool Output Sanitization:** Raw command or network stream stdout (e.g., failed `curl` 404 responses) must never be directly piped or written into an active target file. If a single-line file write results in a net lineage drop, execution must halt instantly for validation.
* **Reversion Mechanics:** If an edit compromises the environment, the agent must instantly drop changes, revert the target surface to the last marked `STABLE` backup, and increment the version trail from that baseline.

---

## 5. Standardized Skill Architecture (agentskills.io Compliance)

Every custom automation or execution capability integrated into an ADIX environment must adopt the standardized skill layout. This architecture guarantees that tools remain modular, reusable, self-documenting, and free from temporary directory leakage.

### A. The Canonical Skill Directory Layout

Every independent skill folder must preserve this exact internal directory footprint:

```text
skills/skill-name/
├── SKILL.md            # Skill declaration, triggers, metadata table, and boundaries
├── references/         # Durable knowledge, Rest-API matrices, session reports, configs
├── scripts/            # Executable tooling, diagnostic probes, automation helpers
└── templates/          # Structural boilerplate configurations and file templates
```

* **Script Discipline:** Small, re-runnable automation scripts or diagnostic helpers must live inside the skill's local `scripts/` directory. Leaving tool files or execution scripts long-term inside a volatile temporary path (e.g., `/tmp/`) is strictly forbidden.

### B. The Nested Category Constraint (`DESCRIPTION.md`)

When skill assets are categorized or grouped under multi-tiered directories (e.g., compliant with the [agentskills.io](https://agentskills.io) blueprint), the nesting category level must act as a structured gate map.

```text
skills/
└── creative/                   # Nesting Category Directory
    ├── DESCRIPTION.md          # Category Index (Custom vs Hub Skills)
    ├── skill-alpha/            # Nested Skill Node (Flat Layout)
    │   └── SKILL.md
    └── skill-beta/             # Nested Skill Node (Flat Layout)
        └── SKILL.md
```

The category folder **must** contain an explicit `DESCRIPTION.md` markdown file providing a clear, high-density index mapping both custom local extensions and core platform hub systems:

```markdown
---
description: [High-level one-line explanation of what this category boundary isolates]
---

# [Category Title]

[Brief explanation of the visual or technical capability provided by this skill pack.]

## Custom Skills
| Skill | Purpose / Bound Utility |
| :--- | :--- |
| `custom-tool-name` | Detailed explanation of what this specialized local extension transforms |

## Hub Skills
| Skill | Purpose / Core System Function |
| :--- | :--- |
| `platform-hub-name` | Explanation of the integrated platform capability provided |
```

---

## 6. Master File Templates

### A. `CONTEXT.md` Blueprint

```markdown
# CONTEXT.md — [Insert Directory Node Name]

> ⚠️ **CRITICAL: THINK → PLAN → SINGLE-LINE EDIT → VERIFY.**
> This folder is an isolated processing node. Limit file modifications to exactly one line per tool call. Multi-line writes, multi-file writes, and unverified execution blocks violate the ADIX architecture.

---

## 1. Structural Map & Compass
* **Upstream Anchor:** [Path to parent CONTEXT.md. Helper: If there is no upstream directory, this file IS the absolute project root.]
* **Downstream Mapping (Max 3 Levels Deep):**

```

[Active Node Name]
├── sub-directory-1/       # [Brief 1-sentence purpose description]
│   └── CONTEXT.md         # Level 1 Downstream
│       └── sub-sub-dir/   # Level 2 Downstream
└── sub-directory-2/       # [Brief 1-sentence purpose description]
└── CONTEXT.md

```

## 2. Local Node Contract (ICM Layer 2)
* **Role Profile:** [The explicit persona or processing specialist the model must adopt for this node]
* **Input Surface:** [Precise path to text, schema, or JSON artifacts required to begin work]
* **Process Intent:** [The exact, single transformation objective expected inside this node]
* **Output Surface:** [Precise path to the output text/JSON file this stage is mandated to yield]

## 3. Dynamic Dependencies & Cross-References
* **Active Links:** [Reference links to root MASTERPLAN.md, automation hooks, or adjacent tool paths]
* **System Toggles:** [Specific execution rules or alternative LLM routing models designated for this node]

```

### B. `NOTES.md` Blueprint

```markdown
# NOTES.md — [Insert Directory Node Name] — Notes & Hardening

> Process rules, localized constraints, and active session memory. For structural maps, see `CONTEXT.md`.

---

## 1. [LOCKED] Process Rules & Constraints (ICM Layer 3)

### The Single-Line Execution Loop
1. **THINK:** Evaluate the immediate target intent against the node's `CONTEXT.md` boundaries.
2. **PLAN:** Specify the exact single line to alter and define its verifiable success metric.
3. **SINGLE-LINE EDIT:** Call file modification tools to alter exactly one line of text or code.
4. **VERIFY:** Execute immediate syntax, test, or diff validation on that modified line.
5. **DOUBLE CHECK:** Critique the single change directly against the node's original intent.
6. **NEXT STEP:** Record state and advance to the subsequent single-line milestone.

### Local Execution Constraints
* **The Single-Line Restriction:** Every file modification tool call must alter exactly one line. Modifying multiple lines or files simultaneously is an unrecoverable failure path.
* **Surgical Diffing:** Diffs must be minimal, focused, and precise. Never rewrite adjacent working infrastructure to resolve a localized bug.
* **Document Non-Obvious Decisions:** Log *why* an architectural line deviation occurred, not just *what* was changed.

### Infrastructure Locks
* [Insert directory-specific locked rules, brand vocals, or immutable parameters here]

---

## 2. [NOTED] Working Artifacts & Active Logs (ICM Layer 4)

### Active State Logs
* [YYYY-MM-DD] — [Single-sentence log tracing current run outcomes, errors hit, and live single-line fixes]

### Hardened Lessons (Requires user approval to promote to LOCKED)
* [Edge-case discoveries from this run — promoted to LOCKED only after operator review]

```

---

## 7. Framework Operations Matrix

| Execution Phase | Core Requirement | Failure / Escape Handler |
| --- | --- | --- |
| **Initialization** | Node processing begins by triggering the global Bootstrap Protocol. | Halt tool execution; reject further action until the root path is evaluated. |
| **Pre-Flight Traversal** | Follow the directory path from root to target; read each `CONTEXT.md` and `NOTES.md` encountered along the route. | Revoke file write permissions if node parameters are missing or unreadable. |
| **Phase-Backup Guard** | Prior to executing modifications, verify a stamped slug snapshot matches current state. | Block the edit tool immediately; raise a **No Backup / No Edit Trap**. |
| **Active Execution** | Enforce file modifications to target exactly $\le 1$ line per tool block. | A line delta of $\ge 2$ triggers an immediate **Signal Integrity Protocol (SIP) Freeze**. |
| **Post-Flight Closeout** | Execute verification scripts, update local `[NOTED]` logs, and re-index the downstream map. | Mark directory state as "stale/unverified" and halt downstream pipeline handoffs. |

---

## 8. Original Source Foundations & Attributions

The ADIX framework synthesizes architectural breakthroughs from the following foundational open-source projects, methodologies, and direct repository implementations:

* **[agent0ai/dox Framework](https://github.com/agent0ai/dox) / [Space Agent](https://github.com/agent0ai/space-agent) / [Agent Zero](https://github.com/agent0ai/agent-zero):** DOX formulated the core thesis of structural directory contracts (`AGENTS.md`), linear reading chains, automated document closeout routines, and hierarchical directory mapping. Space Agent extends this to Hugging Face Spaces as agent tools. Agent Zero is the open, dynamic agentic framework that implements these patterns at scale.
* **[Interpretable Context Methodology (ICM)](https://github.com/RinDig/Interpreted-Context-Methdology):** (Jake Van Clief — Hugging Face Space Agent). Established the baseline structural principle of treating the local filesystem as the explicit state machine, defining distinct data isolation layers spanning from static entry contracts (Layer 2) to volatile runtime logs (Layer 4). [Website](https://eduba.io)
* **[agentskills.io Specification](https://agentskills.io):** Structured the canonical execution package layouts for autonomous tooling ecosystems, enforcing localized `SKILL.md` boundaries alongside category-level `DESCRIPTION.md` matrix manifests.
* **[Autonomous Execution Engine (AEE)](https://solvingforsingularity.com):** Designed the non-negotiable six-step operational loop (Think, Plan, Execute, Verify, Double Check, Cleanup) optimized for high-density, text-based payload generation.
* **The Karpathy Core 10 Guidelines:** Enforced the strict technical parameters for surgical minimalist file diffing, tight loop feedback evaluation, and the complete behavioral elimination of unverified batch file alterations.
