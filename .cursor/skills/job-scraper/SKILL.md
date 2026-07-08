---
name: job-scraper
description: Search job portals for new positions, deduplicate results, update scraper state, and present quick-fit matches. Use when the user asks to scrape jobs, find jobs, search jobs, find new positions, or use job portals.
---

# Job Scraper

## Quick Start

Search for jobs using `.cursor/skills/job-scraper/search-queries.md`, the portal skills under `.agents/skills/`, WebSearch, and WebFetch. Maintain `job_scraper/seen_jobs.json` and exclude applications already tracked in `job_search_tracker.csv`.

Prefer the shipped portal CLIs when they match the target market:
- `.agents/skills/jobindex-search/`
- `.agents/skills/jobnet-search/`
- `.agents/skills/jobdanmark-search/`
- `.agents/skills/jobbank-search/`
- `.agents/skills/linkedin-search/`

Present only real open postings found from actual search/fetch results. For long result sets, suggest the job-ranking skill.

## Reference

- [Search queries](search-queries.md)
