# Module: Research Phase

Runs after Alignment, before writing any files. Ensures Agent arrives at document generation with comprehensive, multi-source knowledge rather than relying solely on built-in references.

---

## Search Capability Check

Before starting research:

```
IF Agent has web search capability (search tool, Firecrawl, browser, or equivalent)
  → Run Full Research (see below)
  → Do NOT skip this phase
ELSE
  → Run Degraded Research (see below)
  → Warn user: "⚠️ No search capability detected. Research will be limited to built-in
    references (WCAG, APCA, HIG). Results may miss project-specific standards,
    library docs, or recent best practices. Consider enabling web search."
```

**Full Research is mandatory when search is available. There are no exceptions.**

---

## Mandatory Standard Consultation

The following standards MUST be read — from built-in references or searched externally —
whenever the project has any frontend, mobile, or UI scope. This is non-negotiable and
applies regardless of tier, search capability, or enabled extensions.

### Trigger Conditions

```
IF project involves ANY of:
  - Web frontend (React, Vue, HTML, CSS, any web UI)
  - iOS or iPadOS app (native or hybrid)
  - Android app (native or hybrid)
  - Cross-platform mobile (Flutter, React Native, Expo, Capacitor)
  - Desktop app with UI (Electron, Tauri, macOS, Windows)
  - PWA / hybrid app
  - Any screen with user-facing interface

THEN the following MUST be consulted before writing FRONTEND_DESIGN.md or any UI-related SPEC section:

  1. WCAG 2.1 (full)          → references/accessibility/WCAG21.md
                                 OR search: "WCAG 2.1 specification W3C"
  2. APCA                      → references/accessibility/APCA/ (all files)
                                 OR search: "APCA contrast accessibility specification"
  3. Apple HIG (full breadth)  → references/accessibility/HIG/ (all files)
                                 AND search: "Apple Human Interface Guidelines <current year>"
                                 NOTE: HIG applies universally — not only for Apple platforms.
                                 Its interaction principles govern web, Android, desktop equally.
```

These three are not optional extras. They are the minimum baseline. Agent must read them,
not skim them. Key values must be extracted and recorded in SOURCES.md.

### If project has NO frontend scope

```
IF project is purely backend / CLI / API with no user-facing UI
  → Mark all three as "n/a — no frontend scope" in SOURCES.md
  → Do not apply UI-specific rules
  → FRONTEND_DESIGN.md should not be generated (unless user explicitly requests it)
```

---

## Full Research Protocol

### Step 1 — Domain Inference

From the project description, tech stack (if known), and enabled extensions, derive a research domain list. Be exhaustive — err on the side of more domains, not fewer.

| Project signal | Research domains to add |
|----------------|------------------------|
| Web frontend | WCAG 2.1, APCA, HIG (mandatory — see above) |
| iOS / Android / mobile | WCAG 2.1, APCA, HIG (mandatory), platform-specific guidelines |
| Payment / checkout | PCI DSS, Stripe/payment provider docs, fraud patterns |
| Auth / login / accounts | OWASP auth guidelines, OAuth 2.0 / OIDC specs |
| Healthcare / medical | HIPAA, HL7 FHIR if applicable |
| React / Next.js | React Server Components docs, Next.js App Router patterns, Vercel constraints |
| Tailwind | Tailwind v4 design tokens, utility-first constraints |
| PWA | PWA checklist, iOS/Android viewport quirks, service worker patterns |
| File uploads | MIME type security, size limits, virus scanning patterns |
| Real-time features | WebSocket vs SSE tradeoffs, connection management |
| i18n / localization | Unicode CLDR, RTL layout considerations |
| AI / LLM integration | Rate limiting, prompt injection risks, streaming UX |
| E-commerce | Accessibility for shopping flows, cart state management |
| HOP extension enabled | Verify HOP naming and structure patterns against current project language |

Always include regardless of project type:
- Current best practices for the detected tech stack
- Known security considerations for the feature set

### Step 2 — Research Execution

For each domain, search and read. Do not summarize prematurely — read enough to actually understand the standard, not just confirm it exists.

```
FOR each domain in research list:
  1. Search: "<domain> best practices <current year>"
     AND: "<domain> specification" or "<domain> official docs"
  2. Read at minimum 2 sources per domain
  3. Log every query and every URL read → will go into SOURCES.md
  4. IF sources conflict → note the conflict explicitly (see Step 3)
  5. IF a source is outdated (>2 years) → search for newer version
  6. Cross-reference: does this domain interact with another already researched?
     IF yes → note the interaction point
```

**Do not stop at the first result. Do not assume you know the answer before searching.**

### Step 3 — Conflict Detection and Resolution

```
IF conflict is between a legal/compliance standard and a design preference
  → Legal/compliance wins. No user input needed. Log it.

IF conflict is between two design standards (e.g., HIG says X, Material says Y)
  → Note both. Recommend the one better suited to project platform.
    Present to user for confirmation.

IF conflict is between an extension's rule and a core Blueprint rule
  → Core Blueprint rule wins. Log the conflict in Research Brief.

IF conflict cannot be resolved by priority
  → Surface to user with both positions clearly stated. Never silently pick one.
```

### Step 4 — Produce Research Brief + SOURCES.md

Write two files simultaneously:

**`/.docs/<planname>/.research/brief.md`** — internal Agent working memory. Not user-facing. Does not appear in README.md index.

```markdown
# Research Brief: <planname>
generated: <YYYY-MM-DD HH:MM>
search_capability: full (native) | full (firecrawl) | full (other) | degraded

## Domains Researched

| Domain | Sources consulted | Key findings | Conflicts noted |
|--------|------------------|--------------|-----------------|
| ... | ... | ... | ... |

## Key Standards Applied

### <Standard Name>
- Source: <url>
- Applies to: <which Blueprint files>
- Key rules: bullet list
- Conflicts with: <other standard if any> → Resolution: <how resolved>

## Conflicts Requiring User Input

- [ ] Conflict: <description> → Options: A or B → Awaiting user decision

## Research Gaps

- <domain>: insufficient sources. Falling back to <built-in / inferred>.

## Extensions Validated

- hop: consistent / inconsistent
- <other ext>: consistent / inconsistent
```

**`/.docs/<planname>/SOURCES.md`** — user-facing audit trail. Follows standard in `references/file-standards.md`. Appears in README.md Documentation Index. Written now, updated incrementally as new sources are consulted during file generation.

### Step 5 — Resolve Open Conflicts with User

```
IF Research Brief has items in "Conflicts Requiring User Input"
  → Present each conflict clearly
  → Wait for user decision before proceeding
  → Record decision in brief.md AND SOURCES.md Conflict Log
ELSE
  → Proceed to file writing
```

---

## Degraded Research Protocol

When no search capability is available:

1. Warn the user (see Search Capability Check above)
2. Still read all mandatory built-in references if frontend scope exists:
   - `references/accessibility/WCAG21.md`
   - `references/accessibility/APCA/` (all files)
   - `references/accessibility/HIG/` (all files)
3. Note which domains have no built-in coverage
4. Write brief.md marking all entries as `source: built-in` or `source: inferred`
5. Write SOURCES.md with `search_capability: degraded` and populate what was read
6. Proceed to file writing

**Degraded research does NOT exempt mandatory standard consultation.
WCAG/APCA/HIG must still be read from built-in references if frontend scope exists.**

---

## Research Brief Lifecycle

- **Created**: Research Phase, before any file writing
- **Read by**: write-order step — Agent reads brief before writing each file
- **Updated**: when user resolves conflicts mid-session
- **On re-run**: check `generated` date
  - IF < 7 days old → ask: "Existing research brief found. Re-research or reuse?"
  - IF > 7 days old → re-research automatically, overwrite both brief.md and SOURCES.md

---

## How Research Feeds Into File Generation

When writing each Blueprint file, Agent must:

1. Re-read the Research Brief before writing that file
2. Apply relevant findings to that file's content
3. Where a finding contradicts a Blueprint default, the finding wins (unless it violates a core rule)
4. Cite the source with a `<!-- research: <domain> -->` comment where a non-obvious standard is applied
5. Update SOURCES.md if any new source is consulted during this step

Example in SPEC.md:
```markdown
#### Error Handling
- Invalid card number → HTTP 400, message: "Please check your card number"
<!-- research: PCI DSS — never echo back card digits in error messages -->
```