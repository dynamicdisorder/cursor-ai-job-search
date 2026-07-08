---
name: job-ranking
description: Batch-score scraped jobs against the candidate profile and fit framework. Use when the user asks to rank jobs, shortlist scraped jobs, triage job matches, or choose which applications deserve effort.
---

# Job Ranking

## Quick Start

Follow `WORKFLOW.md`. Rank jobs from `job_scraper/seen_jobs.json` whose status is `new` unless the user asks to re-rank all. Read the fit framework and profile once, fetch each posting, score honestly, update status fields, and present a shortlist.

Ranking is triage only. It never replaces the full evaluation in the job-application skill.

## Reference

- [Workflow](WORKFLOW.md)
- [Evaluation framework](../job-application/references/04-job-evaluation.md)
- [Candidate profile](../job-application/references/01-candidate-profile.md)
