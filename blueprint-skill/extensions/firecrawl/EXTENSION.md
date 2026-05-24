---
name: firecrawl
version: remote
author: Firecrawl
type: remote
install: npx -y firecrawl-cli@latest init --all --browser
conflicts: []
activation:
  keywords: [search, crawl, scrape, web, research, docs, documentation]
  always: false
role: search-provider
---

## Summary

Firecrawl gives Blueprint's Research Phase real web search and scraping capability. When installed and enabled, Agent uses Firecrawl to query external standards, library docs, compliance requirements, and best practices during the mandatory Research Phase — instead of falling back to built-in references only.

## Role: Search Provider

This extension has a special role: `search-provider`. Blueprint's Research Phase checks for any enabled extension with this role. If found, the Research Phase runs in Full mode. If no search-provider is present and no native search tool is available, Research Phase degrades.

## Capabilities Unlocked

| Firecrawl Command | Blueprint Use |
|------------------|---------------|
| `firecrawl search "<query>"` | Discover standards, specs, and best practices |
| `firecrawl scrape <url> --only-main-content` | Read official documentation pages |
| `firecrawl map <url>` | Discover all pages in a docs site before targeted reading |
| `firecrawl agent "<prompt>"` | Deep research tasks across multiple sources |

## Research Phase Integration

When Firecrawl is the active search provider, the Research Phase uses this execution pattern:

```
FOR each domain in research list:

  # Discover
  firecrawl search "<domain> official specification <year>" --limit 5 --pretty

  # Read primary source
  firecrawl scrape <top_result_url> --only-main-content

  # Read secondary source for cross-reference
  firecrawl scrape <second_result_url> --only-main-content

  # If domain has a known docs site, map it first
  firecrawl map <docs_url> --search "<specific topic>" --limit 20
  # then scrape the most relevant pages found
```

For deep or ambiguous domains, use agent mode:
```
firecrawl agent "What are the current best practices for <domain> in <year>?
  Focus on: security, accessibility, performance. Cite sources." --wait
```

## Affects

- Enables: `modules/research.md` Full Research Protocol
- No direct injection into Blueprint files

## Notes

Not yet installed. Run install command to install and authenticate.
Authentication opens a browser window — run `firecrawl login` after init if browser doesn't open.
Check credits before large research runs: `firecrawl --status`
Use `--only-main-content` on all scrape calls to avoid nav/footer noise.
Self-hosted instance: set `FIRECRAWL_API_URL=http://localhost:3002` to skip API key requirement.