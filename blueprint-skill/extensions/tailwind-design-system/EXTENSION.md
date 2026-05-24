---
name: tailwind-design-system
version: remote
author: wshobson (agents)
type: remote
install: npx skills add https://github.com/wshobson/agents --skill tailwind-design-system
conflicts: []
activation:
  keywords: [tailwind, tailwindcss, utility, css, design-system, tokens, shadcn]
  always: false
---

## Summary

Enforces Tailwind CSS utility-first design system conventions — token usage, custom property patterns, component class composition, and avoiding common anti-patterns like arbitrary values and inline styles. When enabled, FRONTEND_DESIGN.md and ARCHITECTURE.md reflect Tailwind-aware design token structure.

## Affects

- `FRONTEND_DESIGN.md` — replaces abstract spacing/color values with Tailwind token references
- `ARCHITECTURE.md` — injects Tailwind config structure and CSS layer conventions
- `SPEC.md` — annotates UI-touching features with Tailwind class composition notes

## Inject Points

- `FRONTEND_DESIGN.md` → `## Design Principles`, `## Reusable Components`, `## Responsive Rules`
- `ARCHITECTURE.md` → `## Directory Structure` (tailwind.config, globals.css)
- `SPEC.md` → UI feature sections (append Tailwind implementation note)

## Notes

Not yet installed. Run install command above to fetch full content.
When enabled alongside `web-design-guidelines`, Tailwind token constraints take precedence
over abstract spacing/color values from that extension.
Verify Tailwind version (v3 vs v4) from ARCHITECTURE.md tech stack — v4 has breaking changes
in config structure and CSS variable handling.