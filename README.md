# ResumeMatch

A local AI-assisted resume and job-description application, imported from Resume Matcher.

## Features and stack

- Upload a master resume and tailor it to a job description.
- Edit resume content and export formatted PDFs.
- AI-provider configuration, including local models through Ollama.
- Python/FastAPI backend and Next.js/React/TypeScript frontend.
- Backend and frontend tests, dependency lockfiles, and Docker configuration.

## Local setup (PowerShell)

Prerequisites: Python 3.13+, Node.js 24+, npm 10+, and uv.

```powershell
git clone https://github.com/Rubyguru13/-ResumeMatch.git
cd -ResumeMatch/apps/backend
Copy-Item .env.example .env
uv sync
uv run app
```

Keep `HOST=127.0.0.1` in the backend configuration. This application is designed for local use and its API has no authentication.

From a second terminal at the repository root:

```powershell
cd apps/frontend
npm ci
npm run dev
```

Open http://localhost:3000 and configure an AI provider in the app. You can use Ollama locally or supply your own provider credentials. No paid API calls are included or enabled by this import.

PDF export needs Chromium or an installed compatible browser. If required, from `apps/backend` run `uv run playwright install chromium`.

## Project structure

- `apps/backend/`: FastAPI application, Python dependency lockfile, and tests.
- `apps/frontend/`: Next.js UI, runtime assets, tests, and npm lockfile.
- `docker/`, `scripts/`, `Dockerfile`, `docker-compose*.yml`: supporting configuration.

## Tests (after dependencies are installed)

```powershell
# From apps/backend:
uv sync --extra dev
# First supply synthetic replacements for omitted PDF fixtures.
uv run pytest
# From apps/frontend:
npm test
npm run typecheck
```

## Import changes

Removed promotional media, upstream GitHub workflows/templates, editor/agent configuration, and extra documentation. Kept runtime code, assets, and build configuration. Bundled resume PDF fixtures were omitted because they contain identifiable contact details; fixture-dependent tests need synthetic replacements before they can run. Replaced the root README; application code is unchanged.

## Ideas for your own extension

Build a skill-gap dashboard, add explainable keyword matching, or add synthetic test cases for different job descriptions. These are suggestions, not features claimed by this import.

## Source and license

Based on [srbhr/Resume-Matcher](https://github.com/srbhr/Resume-Matcher), revision `db0e6ac9bce8774d6abd692ddccbc02421b0ded2`. Original authorship and copyright notices are retained in `LICENSE` and source files. This is an imported learning/portfolio starting point; original application authorship is not claimed.

## Validation

Files, configuration manifests, and Python syntax were checked during packaging. Dependencies were not installed and the applications were not run end to end.

### Omitted test data

The PDF files under `apps/backend/tests/fixtures/ats/` are deliberately excluded. Do not add real resumes or personal contact details to a public repository. Create synthetic fixtures before running tests that reference those paths.
