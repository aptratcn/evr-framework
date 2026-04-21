# EVR Framework ✅

> Execute → Verify → Report. Stop fake completions and silent AI failures.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/type-agent--skill-blue)](SKILL.md)

**Why this exists:** AI agents say "Done! ✅" way too often without actually verifying. This skill forces a 3-step protocol: actually DO the thing, VERIFY it worked, then REPORT with evidence.

## The Problem

Every AI agent user has experienced this:
```
User: "Create a cron job"
Agent: "Done! ✅"
[No cron job exists — the agent never ran the command]
```

## The Solution: EVR Protocol

### E — Execute
Perform the action for real. Not describe it, not plan it — **do it**.

### V — Verify
Run a verification command. Check the output. Don't trust — verify.

### R — Report
Report what was done WITH EVIDENCE. "Cron job created" → show `crontab -l` output.

## Quick Start

```
# Install as an agent skill
# Claude Code: Copy SKILL.md to .claude/skills/evr-framework/
# OpenClaw: Copy to ~/.openclaw/workspace/skills/evr-framework/

# Triggers automatically when:
- Agent says "done", "finished", "created"
- User asks "did you actually do X?"
- Multi-step tasks complete
- User mentions "verify" or "check if worked"
```

## Example: EVR in Action

```
❌ Without EVR:
"Created the file" (no verification)

✅ With EVR:
EXECUTE: echo "hello" > test.txt
VERIFY:  cat test.txt → "hello" 
REPORT:  File test.txt created and verified. Contents: "hello" (6 bytes)
```

## Anti-Patterns This Prevents

- ❌ "I created the file" → but never ran the write command
- ❌ "The command ran" → but didn't check exit code
- ❌ "Should work" → but didn't test
- ❌ "The feature is ready" → but no verification steps passed

## Related Skills

- [skill-error-recovery](https://github.com/aptratcn/skill-error-recovery) — 4R error recovery when things do break
- [systematic-debugging](https://github.com/aptratcn/systematic-debugging) — When verification reveals a problem
- [cognitive-debt-guard](https://github.com/aptratcn/cognitive-debt-guard) — Prevent code comprehension issues

## Works With

- [OpenClaw](https://openclaw.ai)
- Claude Code, Cursor, Codex
- Any agent framework

## License

MIT
