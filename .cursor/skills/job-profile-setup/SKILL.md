---
name: job-profile-setup
description: Build and update the candidate profile for the AI Job Search workspace. Use when the user asks to set up their profile, import a CV, read career documents, run setup, update search queries, or configure job-search preferences.
---

# Job Profile Setup

## Quick Start

Use this skill when the user wants to prepare the workspace for applications. Follow `WORKFLOW.md`.

The setup workflow supports three paths:
1. Read source files from `documents/`.
2. Import a single pasted or referenced CV.
3. Interview the user section by section.

Write confirmed profile data to `PROFILE.md`, `.cursor/skills/job-application/references/*.md`, `cv/main_example.tex`, and `.cursor/skills/job-scraper/search-queries.md`. Always show proposed changes before writing document-derived additions or resolving conflicts.

## Reference

- [Workflow](WORKFLOW.md)
- [Documents layout](../../../documents/README.md)
