---
name: web-design-guidelines
version: remote
author: Vercel Labs
type: remote
install: npx skills add https://github.com/vercel-labs/agent-skills --skill web-design-guidelines
conflicts: []
activation:
  keywords: [ui, ux, design, web, interface, layout, visual, responsive, css, frontend]
  always: false
---

## Summary

Vercel Labs' web design guidelines covering UI/UX principles, spacing systems, typography scales, responsive layout patterns, and component composition. Complements Blueprint's built-in HIG/WCAG/APCA references with web-specific implementation patterns.

## Affects

- `FRONTEND_DESIGN.md` — injects web-specific layout grid, spacing scale, and component composition patterns
- `ARCHITECTURE.md` — adds CSS/styling architecture conventions

## Inject Points

- `FRONTEND_DESIGN.md` → `## Design Principles` and `## Reusable Components`
- `ARCHITECTURE.md` → `## Directory Structure` (styling layer)

## Notes

Not yet installed. Run install command above to fetch full content.
This extension is web-specific. For native app projects, HIG (already built into Blueprint) is more authoritative.
If both this and `tailwind-design-system` are enabled, they must be reconciled — Tailwind's utility constraints take precedence over abstract spacing guidelines.