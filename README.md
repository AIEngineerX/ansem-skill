# ansem-skill

An [Agent Skill](https://agentskills.io) that teaches any AI agent to operate
safely in the $ANSEM ("The Black Bull") Solana token ecosystem: verify the
real mint, read live price data, prepare a buy the user's own wallet signs,
and route to the right ecosystem surface. Read-only knowledge — no keys, no
custody, no autonomous trading.

Mirrored from [AnsemOS](https://ansemos.com) (the source of truth) — this repo
exists so the skill can be installed independently of that project's own repo.

## Install

Vendor-agnostic, works across Claude Code, Cursor, and 75+ other agents:

```
npx skills add AIEngineerX/ansem-skill --skill ansem
```

Or manually: copy `skills/ansem/SKILL.md` to your agent's skills directory
(e.g. `~/.claude/skills/ansem/SKILL.md` for Claude Code), or paste its
contents into any AI chat's custom/project instructions.

Unofficial, community-built. Not affiliated with Ansem. Not financial advice.
