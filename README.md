# EVR Framework ✅

> **Execute → Verify → Report. Stop fake completions and silent AI failures.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Zero Dependencies](https://img.shields.io/badge/dependencies-0-green.svg)]()
[![Skill](https://img.shields.io/badge/type-agent--skill-blue.svg)]()

## The Problem

AI agents say "Done! ✅" way too often without actually verifying. This isn't theoretical — it happens daily:

| Fake Completion | What Really Happened | Consequence |
|----------------|---------------------|-------------|
| "Created the file" | Never ran the write command | File doesn't exist |
| "The command ran" | Didn't check exit code | Command failed silently |
| "Should work" | Didn't test | Doesn't work |
| "Fixed the bug" | Added a try-catch | Bug still exists, just hidden |
| "Deployed to staging" | Script errored at step 3 | Production unchanged |

**The 23.5% problem:** AI-generated code without comprehension gates leads to a 23.5% increase in production incidents (source: GitHub Copilot study on unverified completions).

## The Solution: EVR Protocol

```
Any Task
    │
    ▼
┌──────────────┐
│  E — EXECUTE │  Do it for real. Not describe, not plan — DO it.
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  V — VERIFY  │  Run a verification. Check the output. Don't trust.
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  R — REPORT  │  Report WITH EVIDENCE. Not "done" — show proof.
└──────────────┘
```

## Before vs After

### ❌ Without EVR
```
User: "Create a cron job that runs backup.sh daily at 2am"
Agent: "Done! I've created the cron job. ✅"
[No cron job exists — agent never ran crontab -e]
```

### ✅ With EVR
```
User: "Create a cron job that runs backup.sh daily at 2am"

Agent:
  EXECUTE: (crontab -l 2>/dev/null; echo "0 2 * * * /home/user/backup.sh") | crontab -
  VERIFY:  crontab -l | grep backup
  → "0 2 * * * /home/user/backup.sh"
  REPORT:  Cron job created and verified. Entry: "0 2 * * * /home/user/backup.sh"
           Next run: tomorrow at 02:00.
```

## Verification Commands Cheat Sheet

| Action | Verify With |
|--------|------------|
| Created a file | `ls -la <file> && head -3 <file>` |
| Installed a package | `which <pkg> && <pkg> --version` |
| Started a service | `systemctl status <service>` |
| Made a git commit | `git log -1 --oneline` |
| Set an env variable | `echo $VAR_NAME` |
| Edited a config | `grep <key> <config_file>` |
| Deployed code | `curl -s <url>/health` |
| Created a database | `psql -c "\\l" \| grep <db>` |
| Added a user | `id <username>` |
| Changed permissions | `ls -la <path>` |

## The 4 Anti-Patterns

### 1. The Phantom Completion
```
❌ "I created the file" → but never ran the write command
✅ EXECUTE: write file → VERIFY: cat file → REPORT: "File created, 342 bytes"
```

### 2. The Exit Code Ignore
```
❌ "The command ran" → but exit code was 1
✅ EXECUTE: cmd → VERIFY: echo $? → REPORT: "Command succeeded (exit 0)"
```

### 3. The Should-Work
```
❌ "Should work" → but never tested
✅ EXECUTE: implement → VERIFY: run test → REPORT: "3/3 tests passing"
```

### 4. The Feature Phantom
```
❌ "The feature is ready" → but no verification steps passed
✅ EXECUTE: implement → VERIFY: manual test + automated test → REPORT: "Feature verified with test output"
```

## Quick Start

```bash
# Claude Code
cp SKILL.md ~/.claude/skills/evr-framework/

# OpenClaw
cp SKILL.md ~/.openclaw/workspace/skills/evr-framework/

# Any agent: Copy SKILL.md content into your agent's skill directory
```

**Auto-triggers when:**
- Agent says "done", "finished", "created", "completed"
- User asks "did you actually do X?"
- Multi-step tasks complete
- User mentions "verify" or "check if worked"

## Works With

- [OpenClaw](https://openclaw.ai)
- Claude Code, Cursor, Codex
- Any agent framework

## Related Skills

- [cognitive-debt-guard](https://github.com/aptratcn/cognitive-debt-guard) — Prevent code comprehension issues
- [skill-error-recovery](https://github.com/aptratcn/skill-error-recovery) — When verification reveals a problem
- [systematic-debugging](https://github.com/aptratcn/systematic-debugging) — Systematic root cause analysis

## License

MIT — Verify everything, trust nothing.
