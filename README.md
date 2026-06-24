# ADIX

**Agent Directory Index**

> Your agent should never operate blind.

---

*Built from [ICM](https://github.com/RinDig/Interpreted-Context-Methdology) (Jake Van Clief) and [DOX](https://github.com/agent0ai/dox) / [Agent Zero](https://github.com/agent0ai/agent-zero) (agent0ai) — the frameworks that proved the filesystem is the state machine. This is those ideas applied, as a skill, free for your agent.*

---

You heard about Interpretable Context Methodology. This is it applied.

One line in your system prompt. Your agent becomes self-documenting. It navigates any directory it encounters. It edits surgically — one line per call, verified by diff, backed up before every change.

## One Line

Add this to your agent's system profile:

```markdown
**BOOTSTRAP PROTOCOL:** Before invoking any tool or executing any action, you must locate and read the root `CONTEXT.md` of the active project directory structure.
```

That's it. The agent reads `CONTEXT.md` before every action. Everything else is automatic.

## How It Works

Every tool call follows five phases:

| # | Phase | What happens |
|---|-------|-------------|
| 1 | **Initialize** | Agent reads root `CONTEXT.md` — no tool use until it knows where it is |
| 2 | **Traverse** | Follows the path from root to target, reading every `CONTEXT.md` and `NOTES.md` along the way |
| 3 | **Backup** | Snapshots current state before any edit — no backup, no edit |
| 4 | **Execute** | Modifies exactly one line per tool call |
| 5 | **Closeout** | Verifies the diff, logs to `NOTES.md`, updates parent indexes |

The agent never operates blind. It always knows where it is, what the directory expects, and what changed.

## Quick Start

**Install as a skill** (agent discovers it automatically):

```bash
git clone https://github.com/karma-devops/adix.git
cd adix
mkdir -p <skills-dir>/adix/{references,templates}
cp skills/adix/SKILL.md <skills-dir>/adix/
cp references/adix-spec-v1.2.0.md <skills-dir>/adix/references/
cp templates/*.md <skills-dir>/adix/templates/
```

Replace `<skills-dir>` with your agent's skill path (e.g. `~/.hermes/skills/`, `~/.claude/skills/`, `~/.codex/skills/`).

**Or copy templates directly to your project:**

```bash
cp templates/HANDSHAKE.md /path/to/your/project/
cp templates/CONTEXT.md /path/to/your/project/
cp templates/NOTES.md /path/to/your/project/
mkdir -p /path/to/your/project/backups
```

Then add the Bootstrap Protocol line to your agent's system profile. Start a new session. The agent reads `CONTEXT.md` first.

## What You Get

- **Surgical precision.** One line per tool call. Verified by diff. No batch edits.
- **Self-documenting agents.** Every closeout writes to the filesystem. State is never trapped in a conversation window.
- **Phase-backup safety.** Every edit is preceded by a timestamped, versioned snapshot. Revert to the last `_STABLE` marker in one command.
- **Structural awareness.** The agent knows where it is in the tree, what the node expects, and what the parent needs to know.
- **Framework-agnostic.** Works with Claude Code, Open Codex — any agent that reads a system prompt.

## Repo Structure

```
adix/
├── README.md                  ← You are here
├── LICENSE                    ← MIT
├── docs/
│   └── INSTALL.md             ← Platform-specific install instructions
├── references/
│   └── adix-spec-v1.2.0.md   ← Full specification
├── templates/
│   ├── HANDSHAKE.md           ← Relational contract
│   ├── CONTEXT.md             ← Directory node contract
│   └── NOTES.md               ← Memory and execution loop
└── skills/
    └── adix/
        └── SKILL.md           ← Agent-facing artifact
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

*Built from [DOX](https://github.com/agent0ai/dox) / [Agent Zero](https://github.com/agent0ai/agent-zero) (agent0ai), [ICM](https://github.com/RinDig/Interpreted-Context-Methdology) ([eduba.io](https://eduba.io)), [agentskills.io](https://agentskills.io), [AEE](https://solvingforsingularity.com), and Karpathy's guidelines. Synthesized into one coherent methodology.*
