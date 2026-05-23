---
name: vercel-react-best-practices
version: remote
author: Vercel Labs
type: remote
install: npx skills add https://github.com/vercel-labs/agent-skills --skill vercel-react-best-practices
conflicts: []
activation:
  keywords: [react, next, nextjs, vercel, frontend, tsx, jsx]
  always: false
---

## Summary

Vercel React Best Practices injects Vercel's opinionated React and Next.js conventions into Blueprint-generated docs — covering file/component structure, server vs. client component boundaries, data fetching patterns, and deployment considerations.

## Affects

- `ARCHITECTURE.md` — Next.js App Router directory conventions, server/client component split
- `FRONTEND_DESIGN.md` — component patterns aligned with React Server Components
- `CHECKLIST.md` — adds Vercel deployment and performance checklist items

## Inject Points

- `ARCHITECTURE.md` → `## Directory Structure`
- `FRONTEND_DESIGN.md` → `## Reusable Components`
- `CHECKLIST.md` → deployment phase tasks

## Notes

This extension is not yet installed. Run the install command above to fetch the full content.
After installing, re-run Blueprint or reload the skill to activate.
