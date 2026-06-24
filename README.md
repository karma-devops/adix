# ADIX

**Agent Directory Index**

> Your agent needs a spine.

---

*Built from [ICM](https://arxiv.org/abs/2504.01427) (Jake Van Clief, McDermott) and [dox](https://github.com/agent0ai/dox) — the frameworks that proved the filesystem is the state machine. This is those ideas applied, as a skill, free for your agent.*

---

You heard about Interpretable Context Methodology. This is it applied.

One line in your system prompt. Your agent becomes self-documenting. It navigates any directory it encounters. It edits surgically — one line per call, verified by diff, backed up before every change.

The filesystem is the state machine. Every directory is a processing node governed by a `CONTEXT.md` (the rails) and `NOTES.md` (the memory) pair. The agent reads the directory structure before touching anything, edits exactly one line per tool call, snapshots state before every modification, and self-documents every closeout.

No more context drift. No more catastrophic overwrites. No more agents operating blind.

## One Line

```markdown
**BOOTSTRAP PROTOCOL:** Before invoking any tool or executing any action, you must locate and read the root `CONTEXT.md` of the active project directory structure.
```

That's it. Append that to your agent's system profile. The rest is automatic.

## How It Works

| Phase | What Happens |
|-------|-------------|
| **Initialization** | Bootstrap Protocol fires — agent reads root CONTEXT.md before any tool use |
| **Pre-Flight Traversal** | Follows the directory path from root to target, reads each CONTEXT.md + NOTES.md along the route |
| **Phase-Backup Guard** | Snapshots state before every edit — no backup, no edit |
| **Active Execution** | Modifies exactly one line per tool call |
| **Post-Flight Closeout** | Verifies diff, logs to NOTES.md, re-indexes parent tree |

## What You Get

- **Surgical precision.** One line per tool call. Verified by diff. No batch edits.
- **Self-documenting agents.** Every closeout writes to the filesystem. State is never trapped in a conversation window.
- **Phase-backup safety.** Every edit is preceded by a timestamped, versioned snapshot. Revert to the last `_STABLE` marker in one command.
- **Structural awareness.** The agent knows where it is in the tree, what the node expects, and what the parent needs to know.
- **Framework-agnostic.** Works with Claude Code, Open Codex — any agent that reads a system prompt.

## Quick Start

```bash
# 1. Clone the repo
git clone https://github.com/karma-devops/adix.git
cd adix

# 2. Copy templates to your project
cp templates/HANDSHAKE.md /path/to/your/project/
cp templates/CONTEXT.md /path/to/your/project/
cp templates/NOTES.md /path/to/your/project/
mkdir -p /path/to/your/project/backups

# 3. Add one line to your agent's system profile
#    (see docs/INSTALL.md for platform-specific instructions)

# 4. Start a new session. The agent reads CONTEXT.md first.
```

## Repo Structure

```
adix/
├── README.md                  ← You are here
├── LICENSE                    ← MIT — free to use, modify, distribute
├── docs/
│   └── INSTALL.md             ← Platform-specific install instructions
├── references/
│   └── adix-spec-v1.2.0.md   ← Full specification (8 sections)
├── templates/
│   ├── HANDSHAKE.md           ← Relational contract — how agent and user work together
│   ├── CONTEXT.md             ← Directory node structural contract
│   └── NOTES.md               ← Directory node memory and execution loop
└── skills/
    └── adix/
        └── SKILL.md           ← Agent-facing artifact (loadable by compatible agents)
```

## Why ADIX?

Existing agent methodologies treat the conversation as state. ADIX treats the **filesystem** as state. This means:

- **Persistence.** Close the session. Open a new one. The agent picks up where it left off because the state is on disk, not in a chat log.
- **Auditability.** Every edit is logged. Every backup is versioned. Every decision is documented in NOTES.md.
- **Composability.** Multi-agent systems share state through the filesystem. Each agent reads the same CONTEXT.md and writes to the same NOTES.md.
- **Discipline.** The single-line edit constraint is uncomfortable at first. That's the point. It forces the agent to think before acting.

## License

MIT — use it, modify it, ship it. No restrictions.

---

*Built from [dox](https://github.com/agent0ai/dox), [ICM](https://arxiv.org/abs/2504.01427), [agentskills.io](https://agentskills.io), [AEE](https://solvingforsingularity.com), and Karpathy's guidelines. Synthesized into one coherent methodology.*
