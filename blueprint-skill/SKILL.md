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
| Research Phase | `modules/research.md` | Always — mandatory after alignment |
| File Writing Order | `modules/write-order.md` | When generating files |
| Consistency Check | `modules/consistency.md` | After all files written |
| DESIGN.md Integration | `modules/design-integration.md` | When FRONTEND_DESIGN.md is in scope |
| File Standards | `references/file-standards.md` | When writing any specific file |
| Accessibility Standards | `references/accessibility/` | When writing FRONTEND_DESIGN.md |

---

## Execution Flow

```
1.  READ modules/tiers.md
2.  READ modules/alignment.md
    └── READ modules/extensions.md → scan extensions/ → present, install, resolve conflicts
    └── IF context7 active → query registry for additional relevant skills
3.  Run alignment interview → get user confirmation on tier + extensions
4.  READ modules/research.md
    └── CHECK: is search capability available?
        ├── YES (native tool OR firecrawl extension active) → Full Research
        └── NO → Degraded Research + warn user
    └── Produce /.docs/<planname>/.research/brief.md
    └── Resolve any open conflicts with user before continuing
5.  READ references/file-standards.md
6.  IF FRONTEND_DESIGN.md in scope → READ modules/design-integration.md
7.  READ modules/write-order.md → write files in order
    └── Before each file: re-read research brief, apply findings
    └── FOR each enabled extension → apply inject points per modules/extensions.md
8.  READ modules/consistency.md → run consistency check
9.  Output results + prompts
```

**Do not write any files before completing Steps 2–4.**

---

## Search Capability Detection

At Step 4, determine search capability by checking in order:

```
IF native web search tool is available → use it, search_capability: full
ELIF firecrawl extension is installed AND active → use firecrawl, search_capability: full
ELIF any other search/browser tool is available → use it, search_capability: full
ELSE → search_capability: degraded
```

Record the result in the Research Brief frontmatter.