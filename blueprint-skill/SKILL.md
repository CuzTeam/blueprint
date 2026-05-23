---
name: blueprint
description: >
  Generate a structured set of planning documents for a project under a dedicated .docs folder.
  Trigger this skill whenever the user wants to plan, scaffold, or document a project —
  including phrases like "create workdoc", "帮我建文档", "plan this project", "scaffold docs for",
  "create-workdoc", "blueprint", "create blueprint", or any request to set up project documentation.
  Always trigger when the user names a project and wants structured planning files generated.
  Once triggered, align with the user on Tier and options before writing any files.
---

# Blueprint Skill

Generates a structured, consistent, cross-referenced documentation set for a project at `/.docs/<planname>/`.

---

## Module Index

| Module | Path | When to read |
|--------|------|-------------|
| Tier System | `modules/tiers.md` | Always — read first |
| Alignment Interview | `modules/alignment.md` | Always — before writing any files |
| Extension System | `modules/extensions.md` | Always — read during alignment |
| File Writing Order | `modules/write-order.md` | When generating files |
| Consistency Check | `modules/consistency.md` | After all files written |
| DESIGN.md Integration | `modules/design-integration.md` | When FRONTEND_DESIGN.md is in scope |
| File Standards | `references/file-standards.md` | When writing any specific file |
| Accessibility Standards | `references/accessibility/` | When writing FRONTEND_DESIGN.md |

---

## Execution Flow

```
1. READ modules/tiers.md
2. READ modules/alignment.md → run alignment interview → confirm with user
   └── READ modules/extensions.md → scan extensions/ → present & install as needed
3. READ references/file-standards.md
4. IF FRONTEND_DESIGN.md in scope → READ modules/design-integration.md
5. READ modules/write-order.md → write files in order
   └── FOR each enabled extension → apply inject points per modules/extensions.md
6. READ modules/consistency.md → run consistency check
7. Output results + prompts
```

**Do not write any files before completing Step 2.**
