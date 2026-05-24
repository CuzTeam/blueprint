---
name: subagent-driven-development
version: remote
author: obra (superpowers)
type: remote
install: npx skills add https://github.com/obra/superpowers --skill subagent-driven-development
conflicts: []
activation:
  keywords: [agent, subagent, parallel, multi-agent, orchestration, complex, large, team]
  always: false
---

## Summary

Subagent-Driven Development structures complex work as a graph of coordinated subagents, each owning a well-scoped task. Enables parallelism, clearer handoffs, and better failure isolation. When enabled, Blueprint's ARCHITECTURE.md and SPEC.md are extended with subagent boundary definitions and coordination contracts.

## Affects

- `ARCHITECTURE.md` — injects subagent boundary map and inter-agent contract definitions
- `SPEC.md` — adds subagent responsibility annotations per feature
- `CHECKLIST.md` — adds subagent handoff verification steps

## Inject Points

- `ARCHITECTURE.md` → `## Components` (append subagent topology)
- `SPEC.md` → each `##` feature section (append owning subagent annotation)
- `CHECKLIST.md` → each phase (append handoff verification)

## Notes

Not yet installed. Run install command above to fetch full content.
Best combined with `verification-before-completion` — subagent handoffs need explicit verification gates.