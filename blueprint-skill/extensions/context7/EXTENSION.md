---
name: context7
version: remote
author: Context7
type: remote
install: npx ctx7 skills install /context7/skills context7
conflicts: []
activation:
  keywords: [skills, registry, install, extension, plugin, library, framework, docs]
  always: false
role: skills-registry
---

## Summary

Context7 provides access to the Agent Skills registry — a searchable marketplace of skills indexed from GitHub repositories. When installed, Blueprint can query Context7 to discover and suggest additional extensions relevant to the current project's tech stack, without the user needing to know extension names in advance.

## Role: Skills Registry

This extension has a special role: `skills-registry`. When active during the Alignment Extension Check (Q3.5), Blueprint can query Context7 to surface additional relevant extensions beyond what's already in `extensions/`.

## Registry Integration

During Q3.5 (Extension Check in alignment), if Context7 is active:

```
# Search for skills relevant to detected tech stack
ctx7 skills search "<tech>"          # e.g. "react", "python", "postgres"
ctx7 skills suggest                  # auto-suggest based on project dependencies

# Get details before recommending to user
ctx7 skills info /<repo>/<skill>

# If user wants to install a discovered skill
ctx7 skills install /<repo> <skill-name>
```

Present discovered skills alongside existing Blueprint extensions in the Q3.5 summary. User chooses which to install and enable.

## Trust Score Policy

Context7 assigns trust scores (0–10) to all registry skills. Blueprint must enforce:

```
IF trust score >= 7.0
  → Present normally as a recommended option

IF trust score 3.0–6.9
  → Present with note: "Community skill — review before enabling (trust: X.X)"

IF trust score < 3.0
  → Do not suggest automatically. Only present if user explicitly asks for it.
    Add warning: "Low trust score (X.X) — unverified source. Review SKILL.md before enabling."

IF skill is blocked (prompt injection detected)
  → Never present. Skip silently.
```

## Capabilities

| Command | Blueprint Use |
|---------|--------------|
| `ctx7 skills search <query>` | Find skills by keyword |
| `ctx7 skills suggest` | Auto-suggest based on project deps |
| `ctx7 skills info /<repo>` | Get skill details and trust score |
| `ctx7 skills install /<repo> <name>` | Install a discovered skill |
| `ctx7 skills list` | Show currently installed skills |

## Affects

- Extends: `modules/alignment.md` Q3.5 Extension Check (adds registry query step)
- No direct injection into Blueprint files

## Notes

Not yet installed. Run `npx ctx7 skills install /context7/skills context7` to install.
Most ctx7 commands work without authentication (no login required for search and install).
Login only required for `ctx7 skills generate` (AI-powered custom skill generation).
Skills install to `.claude/skills/` for Claude Code by default.
Use `--global` flag to install a skill available across all projects.