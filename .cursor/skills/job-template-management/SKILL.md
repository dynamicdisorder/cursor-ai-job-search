---
name: job-template-management
description: Register, test, list, activate, or deactivate custom LaTeX CV and cover letter templates. Use when the user asks to add a template, use a custom CV template, switch templates, or manage LaTeX application templates.
---

# Job Template Management

## Quick Start

Follow `WORKFLOW.md`. Store reusable templates under `templates/cv/<name>/` or `templates/cover_letters/<name>/`, replace personal data with placeholders, create `TEMPLATE.md`, and require a successful compile before activation.

Activation uses managed blocks in the relevant Cursor reference file:
- CV: `.cursor/skills/job-application/references/05-cv-templates.md`
- Cover letter: `.cursor/skills/job-application/references/06-cover-letter-templates.md`

## Reference

- [Workflow](WORKFLOW.md)
- [Templates layout](../../../templates/README.md)
