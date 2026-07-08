# Cursor Setup Guide

Step-by-step instructions for running AI Job Search in Cursor.

## 1. Prerequisites

### Cursor

Install Cursor and open this repository as a workspace. Use Agent mode for the workflows because they create files, run tools, and may use subagents.

### Python

Python 3.10+ is required for salary lookup and salary data conversion:

```powershell
python --version
```

On Windows, `py --version` can be more reliable if `python` is not on PATH.

### Bun

The job portal CLIs are written in TypeScript and run with Bun.

Windows PowerShell:

```powershell
powershell -ExecutionPolicy Bypass -c "irm https://bun.sh/install.ps1 | iex"
```

Other options include `winget install Oven-sh.Bun` on Windows or the installer from https://bun.sh.

### LaTeX

Install a LaTeX distribution:
- Windows: MiKTeX
- macOS: MacTeX
- Linux: `texlive-full` or equivalent

The stock CV compiles with `lualatex`. The stock cover letter compiles with `xelatex` because `cover.cls` uses `fontspec`.

### Optional: pdftotext

Install poppler if you want mechanical ATS text-layer checks:
- Windows: `choco install poppler`
- macOS: `brew install poppler`
- Debian/Ubuntu: `sudo apt install poppler-utils`

If unavailable, the application workflow skips the mechanical parse check and reports degraded mode.

## 2. Install Portal CLI Dependencies

From the repository root:

```powershell
$tools = @("jobbank-search", "jobdanmark-search", "jobindex-search", "jobnet-search", "linkedin-search")
foreach ($tool in $tools) {
  Set-Location ".agents/skills/$tool/cli"
  bun install
  Set-Location "..\..\..\.."
}
```

For `linkedin-search`, this is optional for runtime; it only installs dev types.

## 3. Add Source Documents

Optional but recommended: put career materials under `documents/`:
- `documents/cv/`
- `documents/linkedin/`
- `documents/diplomas/`
- `documents/references/`
- `documents/applications/`

See `documents/README.md` for the expected layout.

## 4. Run Profile Setup In Cursor

Ask Cursor Agent:

```text
Set up my job search profile.
```

Cursor will use the `job-profile-setup` skill. It can read your documents folder, import one CV, or interview you from scratch.

The setup produces or updates:
- `PROFILE.md`
- `.cursor/skills/job-application/references/01-candidate-profile.md`
- `.cursor/skills/job-application/references/02-behavioral-profile.md`
- `.cursor/skills/job-application/references/04-job-evaluation.md`
- `.cursor/skills/job-application/references/05-cv-templates.md`
- `.cursor/skills/job-application/references/07-interview-prep.md`
- `cv/main_example.tex`
- `.cursor/skills/job-scraper/search-queries.md`

To update a section later, ask naturally, for example:

```text
Update only my job search queries.
Refresh my skills section from the documents folder.
```

## 5. Optional Salary Benchmarking

If you have salary data, create `salary_data.json` manually or convert Excel data:

```powershell
pip install openpyxl
python tools/convert_salary_excel.py path/to/salary-data.xlsx --source "My Salary Data 2026"
```

See `tools/README_SALARY_TOOL.md` for the schema.

## 6. Test A Job Application

Ask Cursor Agent:

```text
Evaluate this job and apply if it is a good fit: https://example.com/job-posting
```

Cursor will:
1. Fetch or parse the posting.
2. Evaluate fit and ask before drafting.
3. Draft a tailored CV and cover letter.
4. Run a reviewer pass.
5. Compile and inspect PDFs.
6. Run ATS checks where possible.
7. Present files and verification results.

## 7. Compile Manually If Needed

The application skill should compile during the workflow, but these are the stock commands:

```powershell
Set-Location cv; lualatex -interaction=nonstopmode main_<company>.tex; Set-Location ..
Set-Location cover_letters; xelatex -interaction=nonstopmode cover_<company>_<role>.tex; Set-Location ..
```

## Troubleshooting

### `salary_data.json` not found

Expected if salary benchmarking is not configured. The workflow skips salary lookup.

### Job search tools do not work

Confirm Bun is installed and `bun install` was run inside each `.agents/skills/<portal>/cli` directory.

### LaTeX errors

Confirm MiKTeX/TeX Live includes `moderncv`, `fontspec`, `lualatex`, and `xelatex`. The cover-letter template also expects Lato and Raleway fonts under `cover_letters/OpenFonts/fonts/`.

### Cursor does not pick up a workflow

Mention the task naturally with trigger words from the skill, for example "apply to this job", "rank scraped jobs", "record this outcome", or "set up my profile". The skills live in `.cursor/skills/` and the persistent rules live in `.cursor/rules/`.
