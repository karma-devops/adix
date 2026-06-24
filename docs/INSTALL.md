# Install ADIX

## Prerequisites

- An AI agent that supports a system prompt or core profile (AGENT.md, SOUL.md, CLAUDE.md, etc.)
- A project directory you want to bring under ADIX discipline

## Step 1: Bootstrap Protocol

Add this block to your agent's core system profile:

```markdown
**BOOTSTRAP PROTOCOL:** Before invoking any tool or executing any action, you must locate and read the root `CONTEXT.md` of the active project directory structure. The filesystem is the state machine. Every directory node operates as an independent processing boundary governed by a local `CONTEXT.md` (the structural rails) and `NOTES.md` (the memory engine) pair. You are strictly bound by the active directory's localized contract, its documentation update rules, its phase-backup validation loops, and the mandatory **SINGLE-LINE EDIT** constraint: modify exactly one line per tool execution block. Parse the root-level `CONTEXT.md` first to initialize your operational boundaries.
```

**Where to put it:**

| Platform | File | Notes |
|----------|------|-------|
| Claude Code | `CLAUDE.md` at project root | Append to the end |
| Open Codex | `AGENTS.md` or equivalent | Check your platform docs |
| Custom | Your agent's system prompt | Append as the final instruction block |

## Step 2: Scaffold Your Project

Copy the templates from this repo to your project root:

```bash
# From the ADIX repo
cp templates/HANDSHAKE.md /path/to/your/project/HANDSHAKE.md
cp templates/CONTEXT.md /path/to/your/project/CONTEXT.md
cp templates/NOTES.md /path/to/your/project/NOTES.md
mkdir -p /path/to/your/project/backups
```

Then edit each file to match your project — the HANDSHAKE sets expectations, CONTEXT.md defines structure, NOTES.md tracks memory.

## Step 3: Verify

Start a new session with your agent. The first tool call should trigger the Bootstrap Protocol — the agent will read `CONTEXT.md` before doing anything else. You should see:

1. Agent reads root `CONTEXT.md` on initialization
2. First edit is preceded by a phase-backup snapshot
3. Every tool call modifies exactly one line
4. Every closeout appends to `NOTES.md` [NOTED] section

## Framework-Specific Notes

### Claude Code
Place the Bootstrap Protocol in your project's `CLAUDE.md`. The agent will follow the structural traversal and single-line edit discipline automatically.

### Other Frameworks
The Bootstrap Protocol is framework-agnostic. Any agent that reads its system prompt will respect the execution gate. The templates and spec are pure markdown — no platform-specific dependencies.
