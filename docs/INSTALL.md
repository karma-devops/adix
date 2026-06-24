# Install ADIX

## Prerequisites

- An AI agent that supports a system prompt or core profile (AGENT.md, SOUL.md, CLAUDE.md, etc.)
- A project directory you want to bring under ADIX discipline

## Method 1: Install as a Skill (Recommended)

Place the skill files where your agent's skill loader can discover them:

```bash
# Clone the repo
git clone https://github.com/karma-devops/adix.git
cd adix

# Create the skill directory (replace <skills-dir> with your agent's skill path)
mkdir -p <skills-dir>/adix/{references,templates}

# Copy SKILL.md
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

## Method 2: Manual Setup

Copy the templates directly to your project:

```bash
cp templates/HANDSHAKE.md /path/to/your/project/
cp templates/CONTEXT.md /path/to/your/project/
cp templates/NOTES.md /path/to/your/project/
mkdir -p /path/to/your/project/backups
```

## Step 2: Bootstrap Protocol

Add this block to your agent's core system profile:

```markdown
**BOOTSTRAP PROTOCOL:** Before invoking any tool or executing any action, you must locate and read the root `CONTEXT.md` of the active project directory structure. The filesystem is the state machine. Every directory node operates as an independent processing boundary governed by a local `CONTEXT.md` (the structural rails) and `NOTES.md` (the memory engine) pair. You are strictly bound by the active directory's localized contract, its documentation update rules, its phase-backup validation loops, and the mandatory **SINGLE-LINE EDIT** constraint: modify exactly one line per tool execution block. Read the root-level `CONTEXT.md` first to initialize your operational boundaries.
```

**Where to put it:**

| Platform | File | Notes |
|----------|------|-------|
| Claude Code | `CLAUDE.md` at project root | Append to the end |
| Open Codex | `AGENTS.md` or equivalent | Check your platform docs |
| Custom | Your agent's system prompt | Append as the final instruction block |

## Step 3: Verify

Start a new session with your agent. The first tool call should trigger the Bootstrap Protocol — the agent will read `CONTEXT.md` before doing anything else. You should see:

1. Agent reads root `CONTEXT.md` on initialization
2. First edit is preceded by a phase-backup snapshot
3. Every tool call modifies exactly one line
4. Every closeout appends to `NOTES.md` [NOTED] section
