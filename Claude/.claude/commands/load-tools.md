You are a Technical Setup Assistant.
Your only job in this command is to load and acknowledge all available tools, skills, and context for this project.
Do NOT start any implementation. Do NOT write any code. Do NOT modify any files.

---

## Dynamic Path Resolution

The base tools directory is provided as an argument: $ARGUMENTS

- If an argument is provided → use it as the base path
- If no argument is provided → use `.claude` as the default base path

Resolve all paths dynamically:
```
BASE     = $ARGUMENTS (or ".claude" if empty)
SKILLS   = {BASE}/skills/
COMMANDS = {BASE}/commands/
```

At the start, output:
```
📁 Base path: [resolved BASE]
   Skills path: [SKILLS]
   Commands path: [COMMANDS]
```

---

## Step 1 — Load All Skills

- Scan `{SKILLS}` directory completely
- Read EVERY skill file found
- For each skill, output:
  - **Name**: skill name
  - **Purpose**: what it does in one sentence
  - **Apply when**: specific scenarios where it should be used in this project

---

## Step 2 — Load All Commands

- Scan `{COMMANDS}` directory completely
- For each command, output:
  - **Name**: command name
  - **Purpose**: what it does in one sentence
  - **Usage**: how to invoke it

---

## Step 3 — Verify MCP Servers

Check and confirm availability of all MCP servers configured for this project:
- **Nuxt MCP** — Nuxt 4 documentation
- **Context7 MCP** — up-to-date library documentation
- **Playwright MCP** — browser automation and QA testing
- **GitHub MCP** — version control

For each MCP output:
- ✅ Connected — if available
- ⚠️ Missing — if not available, plus what will be affected

---

## Step 4 — Load Project Context

- Read `CLAUDE.md` if it exists
- Read `tasks.md` if it exists — report how many tasks are pending `[ ]` vs done `[x]`
- Read `.env.example` if it exists — report which required API keys are still empty
- Check if `fix-log.md` exists — if yes, report total fixes logged so far

---

## Step 5 — Output Full Summary

Output this exact summary when done:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
🔧 PROJECT TOOLS LOADED SUCCESSFULLY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📚 Skills ([X] loaded):
   • [Skill Name] → [when to apply]
   • [Skill Name] → [when to apply]

⚡ Commands ([X] available):
   • /[command-name] → [what it does]
   • /[command-name] → [what it does]

🔌 MCP Servers:
   • [MCP Name]: ✅ Connected / ⚠️ Missing
   • [MCP Name]: ✅ Connected / ⚠️ Missing

📋 Project Status:
   • CLAUDE.md: [found / not found]
   • tasks.md: [X] tasks pending, [X] done
   • .env.example: [X] API keys still empty → [list them]
   • fix-log.md: [X] fixes logged / not created yet

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
✅ All tools loaded. Ready for implementation.
   Run /implement to start building.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Rules
- Do not write any code
- Do not modify any file
- Do not start implementation
- This command is read-only — observation and reporting only
