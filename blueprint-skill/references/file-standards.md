## SOURCES.md

Research audit trail. Generated automatically at the end of the Research Phase.
Updated incrementally whenever new sources are consulted during file generation.
Always required — generated for every project at every tier.

```markdown
---
plan: <planname>
generated: <YYYY-MM-DD HH:MM>
search_capability: full (native) | full (firecrawl) | full (other) | degraded
---

# Sources: <planname>

> This file is the complete audit trail of all external sources, standards, and references
> consulted during Blueprint document generation. It is generated automatically —
> do not edit by hand.

## Standards Always Consulted

<!-- These are consulted for every project with frontend/UI/mobile scope.
     If no frontend scope: mark each as "n/a — no frontend scope" -->

| Standard | Scope | Version / URL | Key rules applied |
|----------|-------|--------------|-------------------|
| WCAG 2.1 | Accessibility baseline | references/accessibility/WCAG21.md | AA minimum enforced |
| APCA | Contrast calculation | references/accessibility/APCA/ | Lc values used over WCAG 2.x ratios |
| Apple HIG | Interaction design | references/accessibility/HIG/ | Universal principles applied (not Apple-exclusive) |

## Research Queries

<!-- One row per search query executed during Research Phase -->

| # | Query | Tool used | Top result URL | Used in |
|---|-------|-----------|---------------|---------|
| 1 | ... | firecrawl / native / built-in | ... | SPEC.md / ARCHITECTURE.md / ... |
| 2 | ... | ... | ... | ... |

## Sources by Domain

<!-- One section per researched domain -->

### <Domain Name>

| Source | URL | Consulted for | Findings summary | Conflicts |
|--------|-----|--------------|-----------------|-----------|
| <name> | <url> | <which file/section> | <1-2 sentences> | none / <conflict description> |

## Conflict Log

<!-- All conflicts detected between sources, and how they were resolved -->

| Conflict | Source A | Source B | Resolution | Decided by |
|----------|---------|---------|------------|-----------|
| ... | ... | ... | ... | auto / user |

## Degraded Research Log

<!-- Only present if search_capability: degraded -->

### Domains with No Coverage

| Domain | Why not covered | Fallback used |
|--------|----------------|--------------|
| ... | no search capability | built-in references / inferred |

## Extension Sources

<!-- Sources injected by enabled extensions -->

| Extension | Source document | Applies to |
|-----------|----------------|-----------|
| hop | extensions/hop/EXTENSION.md | ARCHITECTURE.md, SPEC.md, CHECKLIST.md |
| ... | ... | ... |
```

**Rules:**
- Created during Research Phase, before any file is written
- Every search query must be logged — no silent queries
- Every source read must appear in Sources by Domain
- If a source influenced a specific line in a Blueprint file, the `<!-- research: <domain> -->` comment in that file cross-references back here
- SOURCES.md appears in README.md Documentation Index
- SOURCES.md is updated if Agent consults new sources during file generation (not only during Research Phase)