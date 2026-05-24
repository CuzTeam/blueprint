# File Standards Reference

Authoritative structure for every reserved filename. Any file using a reserved name must follow its standard exactly.

---

## README.md

Entry point. Written last. Agent reads this first when returning to a project.

```markdown
---
plan: <planname>
version: 1.0
created: <YYYY-MM-DD>
status: draft | active | archived
lang: <ISO 639-1 code, e.g. zh, en, ja, ko, fr>
---

# <planname>

> One-line description of the project.

## Documentation Index

| File | Purpose |
|------|---------|
| PLAN.md | Goals, non-goals, milestones |
| SPEC.md | Feature logic and behavior |
| CHECKLIST.md | Task list and progress tracking |
| ARCHITECTURE.md | System structure and directory layout |
| FRONTEND_DESIGN.md | UI and interaction specification |
| DATAMODEL.md | Data schema definitions |
| SOURCES.md | Research audit trail — all sources consulted during generation |

## Quick Start

<!-- How to get the project running in 3 steps or fewer -->

## Current Status

<!-- One paragraph: what phase is the project in, what's next -->
```

---

## PLAN.md

High-level direction. Human-readable. Not a task list.

```markdown
---
plan: <planname>
version: 1.0
created: <YYYY-MM-DD>
status: draft | active | archived
lang: <ISO 639-1 code, e.g. zh, en, ja, ko, fr>
---

# Plan: <planname>

## Overview

One paragraph. What is this, why does it exist, who uses it.

## Goals

- Goal 1 — why it matters
- Goal 2 — why it matters

## Non-Goals

<!-- Explicit scope boundaries. Anything listed here MUST NOT appear as a feature in SPEC.md -->
- We are not building X
- We are not handling Y in this version

## Milestones

| Phase | Deliverable | Target |
|-------|-------------|--------|
| Phase 1 | ... | ... |
| Phase 2 | ... | ... |

## Stakeholders

| Role | Responsibility |
|------|---------------|
| ... | ... |

## Open Questions

<!-- Unresolved decisions. Remove entries when resolved. -->
- [ ] Question 1
```

---

## SPEC.md

Behavioral specification. Authoritative source of truth for how the system acts.

```markdown
---
plan: <planname>
version: 1.0
created: <YYYY-MM-DD>
status: draft | active | archived
lang: <ISO 639-1 code, e.g. zh, en, ja, ko, fr>
---

# Spec: <planname>

<!--
  Structure: Feature > Sub-feature > Logic
  Use IF / ELIF / ELSE for all branching logic.
  Use <!-- comments --> for notes, clarifications, edge case callouts.
  Every sub-feature must end with a Tests block.
  Every error branch must specify: error type + HTTP status code + user-facing message.
  Multiple independent IF blocks are allowed within one sub-feature.
-->

## <Feature Name>

### <Sub-feature Name>

<!-- Optional clarifying comment -->

IF <condition>
  → <outcome with full detail>
ELIF <condition>
  → <outcome>
ELSE
  → <outcome>

<!-- Independent conditions can have their own IF block -->
IF <another independent condition>
  → <outcome>

#### Validation Rules

- Field X: required, max 255 chars
- Field Y: must be valid email format

#### Error Handling

<!-- Format: Error type → HTTP status, message: "user-facing text" -->
- Invalid email format → HTTP 400, message: "Please enter a valid email address"
- Email already registered → HTTP 409, message: "An account with this email already exists"

#### Tests

<!-- Minimum: one test per logical branch (per IF/ELIF/ELSE arm) -->
- [ ] Valid input submitted → HTTP 201, record created in DB
- [ ] Invalid email format → HTTP 400, response body contains "valid email"
- [ ] Duplicate email → HTTP 409, response body contains "already exists"
- [ ] Missing required field → HTTP 400, field name identified in response
```

**Rules enforced by consistency check:**
- Every `##` = feature domain
- Every `###` = sub-feature (must have Tests)
- All error branches: error type + HTTP status + user-facing message
- No feature without at least one IF/ELIF/ELSE or explicit single-path behavior
- `<!-- comments -->` for non-behavioral notes only

---

## CHECKLIST.md

Executable task list. References SPEC, never duplicates logic.

```markdown
---
plan: <planname>
version: 1.0
created: <YYYY-MM-DD>
status: draft | active | archived
lang: <ISO 639-1 code, e.g. zh, en, ja, ko, fr>
---

# Checklist: <planname>

<!--
  Status:
  [ ] Not started
  [~] In progress   ← must have inline comment explaining state
  [x] Complete      ← all SPEC Tests for referenced section must pass
  [!] Blocked       ← must have inline comment explaining blocker

  Completion standard: a task is [x] only when ALL Tests in its SPEC section pass.
  No exceptions. "Looks done" is not done.
-->

## Phase 1: <Phase Name>

- [ ] <Task description> → SPEC.md#<anchor>
  - Complete when: all Tests in SPEC.md#<anchor> pass
- [~] <Task description> → SPEC.md#<anchor> <!-- 60% — waiting on third-party API -->
- [!] <Task description> → SPEC.md#<anchor> <!-- Blocked: design decision pending on modal behavior -->

## Phase 2: <Phase Name>

- [ ] ...
```

---

## ARCHITECTURE.md

System structure. Always required at T2+. Defines where things live and how they connect.

```markdown
---
plan: <planname>
version: 1.0
created: <YYYY-MM-DD>
status: draft | active | archived
lang: <ISO 639-1 code, e.g. zh, en, ja, ko, fr>
---

# Architecture: <planname>

## Directory Structure

<!-- Authoritative. All new files should be placed per this structure. -->
<!-- Include /.docs/<planname>/ in the tree. -->

<planname>/
├── src/
│   ├── components/
│   ├── pages/
│   └── utils/
├── tests/
├── .docs/
│   └── <planname>/
│       ├── README.md
│       ├── PLAN.md
│       └── ...
└── README.md

## System Overview

<!-- ASCII diagram or plain prose. How do the major pieces fit together? -->

## Components

### <Component Name>

- **Responsibility**: What this does
- **Inputs**: What it receives
- **Outputs**: What it produces
- **Dependencies**: What it relies on

## Data Flow

1. User does X
2. X triggers Y
3. Y calls Z → returns W
4. W is rendered as V

## Tech Stack

| Layer | Technology | Reason |
|-------|-----------|--------|
| Frontend | ... | ... |
| Backend | ... | ... |
| Database | ... | ... |

## API Contracts

### <METHOD> /path

**Request**
```json
{ "field": "type" }
```

**Response 200**
```json
{ "field": "type" }
```

**Error cases**: → SPEC.md#<anchor>

## External Dependencies

| Dependency | Purpose | Version |
|-----------|---------|---------|
| ... | ... | ... |
```

---

## FRONTEND_DESIGN.md

UI and interaction specification. Optional at T1/T2, required at T3.
When generating, follow `modules/design-integration.md` for source priority and accessibility requirements.

```markdown
---
plan: <planname>
version: 1.0
created: <YYYY-MM-DD>
status: draft | active | archived
source: inferred | DESIGN.md
---

# Frontend Design: <planname>

## Design Principles

- Principle 1
- Principle 2

## Pages & Routes

### <Page Name> — `/<route>`

- **Purpose**: What the user does here
- **Components used**: List
- **Entry points**: How user arrives
- **Exit points**: Where user goes next
- **Empty state**: What shows with no data
- **Error state**: What shows on failure
- **Loading state**: What shows while fetching

## Reusable Components

### <ComponentName>

- **Variants**:
- **Props / Inputs**:
- **Behavior**:

## State Management

<!-- How state flows across the app -->

## Responsive Rules

| Breakpoint | Behavior |
|-----------|---------|
| Mobile (< 768px) | ... |
| Tablet (768–1024px) | ... |
| Desktop (> 1024px) | ... |

## Interaction Specification

| Interaction | Behavior | Duration |
|------------|---------|---------|
| Page transition | ... | ... |
| Button loading | ... | ... |

## Accessibility

<!-- Generated from references/accessibility/ — do not weaken these values -->

### Contrast (APCA preferred, WCAG 2.1 AA minimum)
- Body text (< 18px/400w): Lc 75 / 4.5:1
- Large text (>= 18px or 14px bold): Lc 60 / 3:1
- UI elements (icons, borders): Lc 45 / 3:1
- Disabled elements: Lc 30 (intentionally reduced)
- Dark mode: use APCA Lc values — WCAG 2.x ratios unreliable for dark mode

### Typography
- Minimum body font: 16px web / 17pt iOS / 13pt macOS
- Avoid Ultralight/Thin/Light weights at small sizes
- Support text scaling up to 200%

### Color
- Never use color alone to convey state — pair with label, icon, or pattern
- Provide light and dark variants for all custom colors

### Interaction
- All interactive elements keyboard-navigable
- Minimum tap target: 44×44pt
- Focus indicators: Lc 45 minimum

### Motion
- Respect prefers-reduced-motion
- All animations have static fallbacks
```

---

## DATAMODEL.md

Data schema definitions. Optional, but must stay consistent with SPEC.md field usage.

```markdown
---
plan: <planname>
version: 1.0
created: <YYYY-MM-DD>
status: draft | active | archived
lang: <ISO 639-1 code, e.g. zh, en, ja, ko, fr>
---

# Data Model: <planname>

<!--
  Every model referenced in SPEC.md must be defined here.
  Field names here are authoritative — SPEC.md must use the same names.
-->

## <ModelName>

| Field | Type | Constraints | Description |
|-------|------|-------------|-------------|
| id | UUID | required, unique | Primary key |
| created_at | timestamp | required, auto | Creation time |

### Relationships

- <ModelName> has many <OtherModel>
- <ModelName> belongs to <OtherModel>

### Indexes

- Index on `<field>` — reason

## Enums

### <EnumName>

| Value | Meaning |
|-------|---------|
| ... | ... |
```

---

## DESIGN.md (External Input Only)

User-supplied. Not generated by Blueprint. Follows Google design doc format.

When present at `/.docs/<planname>/DESIGN.md`:
- Read before generating FRONTEND_DESIGN.md
- Treat as authoritative for all design decisions
- Never contradict it
- Set `source: DESIGN.md` in FRONTEND_DESIGN.md frontmatter
- If DESIGN.md conflicts with SPEC.md, flag in README.md Open Questions — do not silently resolve

---

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

## Public Docs

<!-- Files read from /.docs/public/ — populated if any files were present -->

| File | Path | Applied to | Notes |
|------|------|-----------|-------|
| <filename> | /.docs/public/<filename> | <which Blueprint files> | <any conflicts or overrides noted> |

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
