# Module: Write Order

Files must be written in dependency order. Later files reference earlier ones — writing out of order causes broken links and inconsistencies.

---

## Order

```
0. SOURCES.md
   └── Created during Research Phase (before any file below).
   └── Always required at every tier.
   └── Updated incrementally whenever a new source is consulted during steps 1–7.

1. PLAN.md
   └── No dependencies. Written first to establish goals and non-goals.

2. DATAMODEL.md (if included)
   └── Depends on: PLAN.md (scope)
   └── Must be written before SPEC so field names are established first.

3. SPEC.md
   └── Depends on: PLAN.md (non-goals), DATAMODEL.md (field names if present)
   └── Defines all features, logic branches, and tests.

4. ARCHITECTURE.md (if included)
   └── Depends on: SPEC.md (components must map to features)
   └── Defines directory structure, system layout, API contracts.

5. FRONTEND_DESIGN.md (if included)
   └── Depends on: SPEC.md (pages/features), ARCHITECTURE.md (routes), DESIGN.md (if present)
   └── REQUIRES: WCAG/APCA/HIG must be read before this step (see modules/research.md).
   └── See modules/design-integration.md for source priority rules.

6. CHECKLIST.md
   └── Depends on: SPEC.md (all section anchors must exist before referencing)
   └── Written second-to-last so all SPEC anchors are available.

7. README.md
   └── Depends on: all other files (indexes them)
   └── Written last. Must include SOURCES.md in Documentation Index.
```

---

## Pre-file Checklist (run before writing each file)

Before writing any file in steps 1–7:

```
1. Re-read /.docs/<planname>/.research/brief.md
2. Identify which research findings apply to this file
3. IF this file has frontend/UI content AND mandatory standards not yet applied
   → Read references/accessibility/ before proceeding (WCAG, APCA, HIG)
4. Apply findings. Cite with <!-- research: <domain> --> where non-obvious.
5. IF any new external source was consulted during writing → update SOURCES.md
```

---

## Naming Convention for Anchors

When writing SPEC.md, use consistent heading anchors so CHECKLIST.md can reference them:

```
## User System           → anchor: #user-system
### Register             → anchor: #register
### Login                → anchor: #login
```

CHECKLIST references use the full path pattern:
```
→ SPEC.md#user-system--register
```

Confirm your markdown renderer's anchor format before writing (GitHub uses `--` for nested headings, some renderers use `-`). Prefer simpler single-level anchors by keeping SPEC headings distinct across the document.