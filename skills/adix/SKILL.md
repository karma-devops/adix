---
name: adix
description: "Use when your agent needs hardened execution discipline — single-line edits, phase-backup guards, structural traversal, and self-documenting closeout. Loads the ADIX methodology: the filesystem is the state machine, every directory is a processing node governed by CONTEXT.md and NOTES.md."
version: 1.2.0
license: MIT
---

# ADIX: Agent Directory Index

## Overview

ADIX is an execution methodology that treats the filesystem as the state machine. Every directory is an independent processing node governed by a `CONTEXT.md` (structural rails) and `NOTES.md` (memory engine) pair. The agent reads the directory structure before touching anything, edits exactly one line per tool call, snapshots state before every modification, and self-documents every closeout.

One line in your system prompt. Everything else is automatic.

## When to Use

- Your agent needs a repeatable, verifiable execution loop — not ad-hoc tool calls
- You want to eliminate context drift across long sessions
- You need phase-backup discipline to prevent catastrophic state destruction
- You're building a multi-agent system where each node has a clear contract
- You want self-documenting agents that externalize state changes to the filesystem

**Don't use for:** Simple one-shot tasks where the overhead of CONTEXT.md/NOTES.md pairs isn't justified. ADIX shines in complex, multi-step, multi-directory workflows.

## Setup

This skill is installed by placing its files in your agent's skills directory. The skill loader discovers it on the next session start.

### Step 1: Install the Skill Files

Create a directory for the skill at the path your agent loads skills from, then copy the files:

```bash
# Create the skill directory structure
mkdir -p <skills-dir>/adix/{references,templates}

# Copy SKILL.md to the skill root
cp skills/adix/SKILL.md <skills-dir>/adix/

# Copy reference files
cp references/adix-spec-v1.2.0.md <skills-dir>/adix/references/

# Copy templates
cp templates/HANDSHAKE.md <skills-dir>/adix/templates/
cp templates/CONTEXT.md <skills-dir>/adix/templates/
cp templates/NOTES.md <skills-dir>/adix/templates/
```

Replace `<skills-dir>` with your agent's skill path. Common locations:

- **Hermes Agent:** `~/.hermes/skills/`
- **Claude Code:** `~/.claude/skills/`
- **Open Codex:** `~/.codex/skills/`
- **Custom:** Check your agent's documentation

### Step 2: Bootstrap Protocol (Manual — One Line)

Add this block to your agent's core system profile (`AGENT.md`, `SOUL.md`, `CLAUDE.md`, or equivalent):

```markdown
**BOOTSTRAP PROTOCOL:** Before invoking any tool or executing any action, you must locate and read the root `CONTEXT.md` of the active project directory structure. The filesystem is the state machine. Every directory node operates as an independent processing boundary governed by a local `CONTEXT.md` (the structural rails) and `NOTES.md` (the memory engine) pair. You are strictly bound by the active directory's localized contract, its documentation update rules, its phase-backup validation loops, and the mandatory **SINGLE-LINE EDIT** constraint: modify exactly one line per tool execution block. Read the root-level `CONTEXT.md` first to initialize your operational boundaries.
```

This is the only manual step. It creates the execution gate — no tool use until the directory context is loaded.

### Step 3: Scaffold Your Project Root

Create three files at your project root. Use the templates from this skill's `templates/` directory, or write your own:

```bash
cp <skills-dir>/adix/templates/HANDSHAKE.md /path/to/your/project/
cp <skills-dir>/adix/templates/CONTEXT.md /path/to/your/project/
cp <skills-dir>/adix/templates/NOTES.md /path/to/your/project/
mkdir -p /path/to/your/project/backups
```

- `HANDSHAKE.md` — how we work together (relational contract)
- `CONTEXT.md` — what we're working on (structural rails)
- `NOTES.md` — what we've learned (memory engine)

The agent will automatically discover and bind to these files on every session start.

## The ADIX Execution Loop

Every tool call follows this five-phase cycle:

| Phase | What Happens | Failure Handler |
|-------|-------------|-----------------|
| **Initialization** | Bootstrap Protocol fires — agent reads root CONTEXT.md | Halt all tool use until root path is evaluated |
| **Pre-Flight Traversal** | Follow the directory path from root to target; read each `CONTEXT.md` and `NOTES.md` along the route. | Revoke write permissions if node parameters missing |
| **Phase-Backup Guard** | Verify a stamped slug snapshot matches current state before editing | Block edit — raise No Backup / No Edit Trap |
| **Active Execution** | Modify exactly one line per tool call | Line delta >= 2 triggers SIP Freeze |
| **Post-Flight Closeout** | Verify diff, update [NOTED] logs, re-index downstream map | Mark directory stale/unverified, halt handoffs |

## The Single-Line Execution Loop (within NOTES.md)

1. **THINK** — Evaluate intent against the node's CONTEXT.md boundaries
2. **PLAN** — Specify the exact single line to alter and its success metric
3. **SINGLE-LINE EDIT** — Call file tools to alter exactly one line
4. **VERIFY** — Run immediate syntax, test, or diff validation
5. **DOUBLE CHECK** — Critique the change against the original intent
6. **NEXT STEP** — Record state and advance to the next milestone

## Phase-Backup Slug Format

```
backups/(version)_(info-context)_(timestamp)/
```

- `version`: `v0`, `v1`, `v2` — sequential, never reused
- `info-context`: Short hyphenated description. Append `_STABLE` after verification
- `timestamp`: `YYYY-MM-DD_HHMM` local time

Example: `backups/v0_pre-native-fix_STABLE_2026-06-01_0057/`

Every backup root must contain a `VERSIONING.md` manifest. No loose files in the backups directory.

## Self-Documentation Closeout

After every single-line edit:

1. **Verify Line Delta** — diff confirms exactly one line changed
2. **Commit Memory Log** — append one-sentence summary to `NOTES.md` `[NOTED]` section
3. **Re-Index Parent Tree** — if a downstream folder changed, update parent `CONTEXT.md`
4. **Prune Context Clutter** — delete stale notes and contradictory rules

## Common Pitfalls

1. **Skipping the Bootstrap Protocol.** The entire methodology depends on that one line in the system prompt. Without it, the agent has no execution gate and will operate without context. This is the only manual step — do not skip it.

2. **Multi-line edits.** The single-line constraint is the sharpest edge in ADIX. Modifying two lines in one tool call triggers a SIP Freeze. If you need to change multiple lines, do it one tool call at a time with verification between each.

3. **Backups after the edit.** The snapshot must be taken *before* modification. A backup taken after an overwrite loop is useless. Enforce: backup first, then edit.

4. **Loose files in backups directory.** Every backup root must have a `VERSIONING.md` manifest. Loose files are banned — they create orphaned state that can't be traced.

5. **Forgetting to re-index parent CONTEXT.md.** When you create, rename, or remove a subdirectory, the parent node's downstream map must be updated immediately. Stale indexes cause traversal failures.

6. **Raw tool output piped into target files.** Failed `curl` responses, error traces, or network stream stdout must never be written directly into an active target file. If a write results in a net lineage drop, halt for validation.

## Verification Checklist

- [ ] Bootstrap Protocol is appended to the agent's system profile
- [ ] Root `CONTEXT.md` exists with upstream anchor and downstream mapping
- [ ] Root `NOTES.md` exists with [LOCKED] rules and [NOTED] log sections
- [ ] `backups/` directory exists at project root
- [ ] First edit was preceded by a phase-backup snapshot
- [ ] Every tool call modified exactly one line (verify with diff)
- [ ] Every closeout appended to [NOTED] in the local NOTES.md
- [ ] Parent CONTEXT.md re-indexed if downstream structure changed

## Reference Files

| File | Purpose |
|------|---------|
| `references/adix-spec-v1.2.0.md` | Full specification — all eight sections with detailed rationale |
| `templates/HANDSHAKE.md` | Relational contract — how agent and operator work together |
| `templates/CONTEXT.md` | Blueprint for directory node structural contract |
| `templates/NOTES.md` | Blueprint for directory node memory and execution loop |
