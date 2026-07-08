<div align="center">

# AI Job Search for Cursor

<a href="https://www.cursor.com/">
  <img src="https://img.shields.io/badge/Cursor-native-000000?style=for-the-badge&logo=cursor&logoColor=white" alt="Cursor native">
</a>
<a href="https://github.com/MadsLorentzen/ai-job-search">
  <img src="https://img.shields.io/badge/forked%20from-MadsLorentzen%2Fai--job--search-blue?style=for-the-badge" alt="Forked from MadsLorentzen/ai-job-search">
</a>

</div>

A Cursor-native AI job application workspace. Fill in your profile, then use Cursor Agent to evaluate job postings, search job portals, rank matches, tailor CVs, write cover letters, verify PDFs, track outcomes, and plan upskilling.

This is a Cursor-native fork/port of [`MadsLorentzen/ai-job-search`](https://github.com/MadsLorentzen/ai-job-search). The objective is to adapt the original Claude Code-oriented workflow into Cursor conventions: Cursor Agent Skills, project rules, natural-language workflows, and reusable local job-search tooling. It does not require any external coding-agent CLI.

## Attribution

This project is derived from the original open-source repository [`MadsLorentzen/ai-job-search`](https://github.com/MadsLorentzen/ai-job-search). The original concept, workflow structure, LaTeX application assets, and job-search assistant idea come from that project.

This fork focuses on the Cursor port:
- Replacing Claude Code slash-command workflows with Cursor Agent Skills.
- Moving persistent project guidance into `.cursor/rules/`.
- Preserving the job-search, ranking, CV tailoring, cover-letter, outcome tracking, and upskilling workflows in a Cursor-native form.
- Keeping personal candidate data, CVs, application drafts, search reports, salary data, and tracker files out of version control.

## What This Is

The repository combines:
- Cursor rules in `.cursor/rules/` for application integrity, profile truth, LaTeX verification, and portal tooling.
- Cursor skills in `.cursor/skills/` for setup, applications, scraping, ranking, outcomes, upskilling, templates, portals, expansion, and reset.
- Executable job-portal CLIs in `.agents/skills/`.
- LaTeX CV and cover-letter templates in `cv/` and `cover_letters/`.
- Personal source material and application history under `documents/`.

Typical flow:

```text
Set up profile -> Search jobs -> Rank matches -> Apply to a posting -> Record outcome
       |              |              |                |                    |
       v              v              v                v                    v
  PROFILE.md    seen_jobs.json   shortlist     CV + cover PDFs     calibration data
```

## Prerequisites

- Cursor with Agent mode.
- Python 3.10+ for salary tools.
- Bun for the job-search CLIs.
- LaTeX with `lualatex` and `xelatex` for PDF generation.
- Optional: `pdftotext` from poppler for ATS text-layer checks.

## Quick Start

### 1. Install Job Search Tools

From the repository root:

```powershell
$tools = @("jobbank-search", "jobdanmark-search", "jobindex-search", "jobnet-search", "linkedin-search")
foreach ($tool in $tools) {
  Set-Location ".agents/skills/$tool/cli"
  bun install
  Set-Location "..\..\..\.."
}
```

For `linkedin-search`, install is optional for runtime because it has zero runtime dependencies.

### 2. Set Up Your Profile

Open the repository in Cursor and ask Cursor Agent:

```text
Set up my job search profile.
```

The `job-profile-setup` skill offers three paths: read files from `documents/`, import one CV, or interview you section by section. It populates `PROFILE.md`, `.cursor/skills/job-application/references/*.md`, `cv/main_example.tex`, and `.cursor/skills/job-scraper/search-queries.md`.

### 3. Search And Rank Jobs

Ask:

```text
Find new jobs for my profile.
Rank the new scraped jobs.
```

The scraper deduplicates against `job_scraper/seen_jobs.json` and `job_search_tracker.csv`. Ranking batch-scores postings before you spend time applying.

### 4. Apply To A Job

Ask:

```text
Apply to this job: https://example.com/job-posting
```

Cursor Agent will evaluate fit first and ask before drafting. If you proceed, it creates tailored LaTeX files, runs a reviewer pass, compiles PDFs, performs layout and ATS checks, and reports verification results.

## Main Workflows

- `job-profile-setup`: build or refresh your profile.
- `job-scraper`: find and deduplicate postings.
- `job-ranking`: score scraped jobs into a shortlist.
- `job-application`: evaluate, draft, review, compile, and verify applications.
- `job-outcome`: record interviews, offers, rejections, and no-response outcomes.
- `job-upskill`: identify skill gaps and generate learning plans.
- `job-template-management`: register custom LaTeX templates.
- `job-portal-management`: add a local job-board integration.
- `job-profile-expansion`: discover source-traceable competencies from documents and public links.
- `job-reset`: clear profile data or documents after explicit confirmation.

## File Structure

```text
ai-job-search/
|-- PROFILE.md                         # Main candidate profile + workflow checklist
|-- .cursor/
|   |-- rules/                         # Cursor project rules
|   `-- skills/                        # Cursor workflow skills
|-- .agents/skills/                    # Bun job-portal CLI tools
|-- cv/                                # LaTeX CV variants
|-- cover_letters/                     # LaTeX cover letters and cover.cls
|-- templates/                         # Custom templates
|-- documents/                         # Career source materials and application history
|-- salary_lookup.py                   # Optional salary benchmarking
|-- tools/                             # Salary data conversion tools
|-- job_scraper/                       # Scraper state
|-- upskill/                           # Learning-plan reports
|-- job_search_tracker.csv             # Application tracker
`-- SETUP.md                           # Detailed setup guide
```

## Important Guarantees

The workflow is designed to be honest and verifiable:
- Fit is evaluated before drafting.
- Claims must come from your profile or verified research.
- Generated PDFs are compiled and inspected before final delivery.
- ATS keyword checks never stuff unsupported skills.
- Outcomes feed future calibration instead of being lost in chat.

## Customization

Use `job-template-management` to register your own CV or cover-letter templates. Use `job-portal-management` to add job boards for your country or market. The shipped Danish portal tools and LinkedIn public listings remain as examples and usable integrations.

## License

MIT
