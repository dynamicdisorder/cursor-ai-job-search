---
name: job-portal-management
description: Generate a job portal search skill for a local market, investigate public endpoints, scaffold a Bun CLI, and verify live results. Use when the user asks to add a job board, add a portal, generate a portal skill, or support a local job site.
---

# Job Portal Management

## Quick Start

Follow `WORKFLOW.md`. Investigate the portal before scaffolding, respect access rules, generate under `.agents/skills/<name>/`, and require live search/detail verification plus typecheck/test before registration.

Generated portal skills should follow the shipped CLI contract so the scraper can use them interchangeably.

## Reference

- [Workflow](WORKFLOW.md)
- [LinkedIn reference implementation](../../../.agents/skills/linkedin-search/SKILL.md)
