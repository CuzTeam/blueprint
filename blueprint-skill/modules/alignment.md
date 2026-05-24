# Module: Alignment Interview

Run this interview **before writing any files**. Do not skip or abbreviate. The goal is to gather everything needed so no assumptions have to be made during file generation.

---

## Questions to Ask (in order)

### Q1 — Project Name
Ask for a project name. This becomes `<planname>` — the folder name and the identifier used across all docs.

Rules:
- Must be a single slug: lowercase, hyphens allowed, no spaces (e.g. `my-app`, `payment-service`)
- If the user gives a name with spaces, suggest a slugified version and confirm

### Q2 — Project Description
Ask for a brief description: what does it do, who uses it, why does it exist?

- One to three sentences is ideal
- This populates PLAN.md Overview and README.md description
- If vague, ask one follow-up: "Is this user-facing, internal tooling, or an API?"

### Q3 — Tier Selection
Present the tier table from `modules/tiers.md`. State your recommendation and why. Ask the user to confirm or choose a different tier.

> Example: "Based on your description, I'd recommend **T2 (Standard)** — it's a web app with backend logic but no design system yet. Does that work, or would you like T1 or T3?"

Do not proceed until the user confirms a tier.

### Q3.5 — Extension Check

Read `modules/extensions.md` fully. Scan the `extensions/` directory and read every EXTENSION.md.

#### Step A — Built-in registry query (if context7 active)
```
IF context7 extension is installed and active:
  → Run: ctx7 skills suggest   (auto-detect from project deps)
  → Run: ctx7 skills search "<tech stack keyword>"  (for each major tech detected)
  → Filter results by trust score per context7 EXTENSION.md policy
  → Add qualifying results to the extensions list for presentation
```

#### Step B — Present all available extensions

Group by status and show inline — do not make the user ask:

```
Extensions:

  Embedded (ready to use):
  ✅ hop — Human-Oriented Programming coding standards

  Not installed (I can install these):
  📦 verification-before-completion — Explicit verification gates before marking tasks done [always recommended]
  📦 subagent-driven-development — Multi-agent task coordination
  📦 firecrawl — Web search for Research Phase (enables full research)
  📦 web-design-guidelines — Vercel web UI/UX principles
  📦 tailwind-design-system — Tailwind CSS utility conventions
  📦 vercel-react — React/Next.js best practices
  📦 context7 — Skills registry browser

  [+ any ctx7 suggestions, with trust scores]

Would you like to enable any? For uninstalled ones I can run the install command now.
```

#### Step C — Install flow

For each extension the user wants that isn't installed:
```
→ Show the install command from EXTENSION.md
→ Ask: "Install now?"
→ IF yes → execute install command → confirm success → mark as enabled
→ IF no → skip, do not re-prompt this session
```

#### Step D — Conflict resolution
```
IF two enabled extensions declare a conflict:
  → Describe the conflict (from their EXTENSION.md Notes)
  → Ask user which to keep
  → Disable the other for this session
```

#### Step E — Search capability determination

After extensions are finalized, determine search mode for Research Phase:
```
IF native search tool available → search_capability: full (native)
ELIF firecrawl extension enabled → search_capability: full (firecrawl)
ELIF any browser/search tool available → search_capability: full (other)
ELSE → search_capability: degraded
   → Warn: "⚠️ No search capability. Research Phase will use built-in references only.
     Install firecrawl or enable a search tool for full research."
```

### Q4 — Optional Add-ons
After extensions are confirmed, ask:
- "Would you like to add any optional files from higher tiers?" (list what's available for their tier)
- "Do you need any custom files beyond the standard set?"

If they add a file with a reserved name, remind them: it must follow the standard in `references/file-standards.md`.
If they add a custom file, confirm the name won't cause confusion.

### Q5 — Existing Directory Check
Check silently if possible: does `/.docs/<planname>/` already exist?

- IF yes → warn: "This directory already exists. Overwrite, merge, or abort?"
- IF no → proceed

### Q6 — DESIGN.md Check
If `FRONTEND_DESIGN.md` is in scope (T3 or opted-in):
- Check if `DESIGN.md` already exists at `/.docs/<planname>/DESIGN.md`
- IF yes → confirm: "Found a DESIGN.md — I'll use it as the source for FRONTEND_DESIGN.md."
- IF no → note that FRONTEND_DESIGN.md will be inferred, remind user they can drop one in later

---

## After Alignment — Summary

Present a single consolidated summary before any work begins. Wait for user confirmation.

```
Here's the plan for /.docs/<planname>/:

Tier: T2 (Standard)

Files:
  ✅ README.md
  ✅ PLAN.md
  ✅ SPEC.md
  ✅ CHECKLIST.md
  ✅ ARCHITECTURE.md
  ➕ DATAMODEL.md (opted in)

Extensions enabled:
  ✅ hop (embedded)
  ✅ verification-before-completion (installing...)
  ✅ firecrawl (installing...)

Research Phase: full (firecrawl)
  Will research: [inferred domain list based on project description]

Shall I proceed?
```

Only after user confirms → proceed to Research Phase (modules/research.md).