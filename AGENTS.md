# Agent instructions

GitHub template repository with Prettier, Markdownlint, Yamllint, reusable CI workflows
([quality-checks](https://github.com/garretpatten/quality-checks),
[security-guardrails](https://github.com/garretpatten/security-guardrails),
[codeowners-enforcer](https://github.com/garretpatten/codeowners-enforcer)), and standard
project docs. When bootstrapping a consumer repo from this template, customize paths and
trim linters that do not apply.

## Repository standards

[garretpatten/github-standards](https://github.com/garretpatten/github-standards) is the
**canonical source of truth** for how every `garretpatten` repository must be structured
and maintained: license, security policy, contributing, community files, README
branding, CODEOWNERS, branch protection, pull requests, signed commits, Dependabot,
dependency hygiene, secret hygiene, workflow permissions, action pinning, repository
metadata, CI and quality, and exceptions.

- **Before starting any task**, read the current standards from the source of truth
  rather than from memory or a cached copy — they change over time. The standards index
  is at <https://github.com/garretpatten/github-standards#standards-files>; fetch raw
  files from
  `https://raw.githubusercontent.com/garretpatten/github-standards/master/<standard>.md`
  (via web fetch, `curl`, or `gh api`) and read every standard relevant to the task.
- **While working**, apply the standards to every change: workflows, dependency files,
  community files, repository metadata, and commit practices must conform to the
  standards as they exist at the time of the change.
- **When you detect drift** — this repository lagging behind a standard that changed —
  bring the repository back in line as part of normal work and call it out in your
  summary. If an update would be large or ambiguous, propose it instead of applying it
  silently.
- **Before finishing**, confirm the work satisfies the
  [verification](https://github.com/garretpatten/github-standards/blob/master/verification.md)
  standard and that local checks pass.
- For a full compliance review, use the `github-audit` skill, which audits a repository
  against these standards and reports numbered findings.

## Before you finish

Do **not** consider work complete until local checks pass. Run from the
repository root:

```bash
npm install
npm run lint
```

Or run the same checks step by step:

```bash
npx prettier --check .
npx markdownlint-cli2 "**/*.md" "#node_modules"
yamllint .github .yamllint .markdownlint.yaml
actionlint
```

**Fix failures instead of ignoring them** when practical:

- Prettier: `npx prettier --write .` (or only the paths you changed), then re-run
  `npx prettier --check .`.
- Markdown/YAML: correct the files per the rule messages, then re-run until
  clean.

| If you edited              | Also run                                                         |
| -------------------------- | ---------------------------------------------------------------- |
| `.github/workflows/*.yaml` | `yamllint .github .yamllint .markdownlint.yaml` and `actionlint` |
| Any `*.md`                 | `markdownlint-cli2` on those paths or `npm run lint:markdown`    |
| YAML or workflow files     | `npm run lint:yaml`                                              |

Install missing tools as needed:

| Tool       | Example install           |
| ---------- | ------------------------- |
| actionlint | `brew install actionlint` |
| yamllint   | `pip install yamllint`    |

CI **Quality Checks** runs PR-scoped linters via `garretpatten/quality-checks`. Disable
unused `*_run` inputs in `.github/workflows/quality-checks.yaml` for projects that do not
need every tool (ESLint, Ruff, Hadolint, etc.).

CI **Security Guardrails** runs OpenGrep, TruffleHog, and supply-chain scans. CI **Codeowners
Enforcer** requires every changed file to have an owner in `.github/CODEOWNERS` (or an
entry in `.github/.codeownersignore`).

## Layout

| Path                               | Role                                              |
| ---------------------------------- | ------------------------------------------------- |
| `.prettierrc`, `.prettierignore`   | Formatting (80-char YAML via override)            |
| `.markdownlint.yaml`               | Markdown lint rules (`MD013` off; Prettier wraps) |
| `.yamllint`                        | YAML lint (80-char lines, `document-start` off)   |
| `.truffleignore`, `.trivyignore`   | Scanner exclusions for security workflows         |
| `.github/CODEOWNERS`               | Required ownership for changed files              |
| `.github/workflows/`               | Quality, security, and CODEOWNERS enforcement     |
| `.github/ISSUE_TEMPLATE/`          | Bug report and feature request issue forms        |
| `.github/pull_request_template.md` | PR checklist and change summary                   |
| `.github/dependabot.yaml`          | Dependency update automation                      |
| `package.json`                     | Prettier and Markdownlint dev dependencies        |

## Commits

Only commit when the user asks. Do not commit secrets.

## GitHub Actions

Whenever a GitHub workflow is added, all GitHub Action pins in that workflow
should be updated to point to the full-length commit SHA of the most recent
release.
