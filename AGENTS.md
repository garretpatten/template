# Agent instructions

GitHub template repository with Prettier, Markdownlint, Yamllint, reusable CI workflows
([quality-checks](https://github.com/garretpatten/quality-checks),
[security-guardrails](https://github.com/garretpatten/security-guardrails),
[codeowners-enforcer](https://github.com/garretpatten/codeowners-enforcer)), and standard
project docs. When bootstrapping a consumer repo from this template, customize paths and
trim linters that do not apply.

## Before you finish

Run local checks that match what you changed:

```bash
npm install
npm run lint
```

| If you edited              | Also run                                                      |
| -------------------------- | ------------------------------------------------------------- |
| `.github/workflows/*.yaml` | `yamllint .github .yamllint .markdownlint.yaml` and `actionlint` |
| Any `*.md`                 | `markdownlint-cli2` on those paths or `npm run lint:markdown` |
| YAML or workflow files     | `npm run lint:yaml`                                           |

CI **Quality Checks** runs PR-scoped linters via `garretpatten/quality-checks`. Disable
unused `*_run` inputs in `.github/workflows/quality-checks.yaml` for projects that do not
need every tool (ESLint, Ruff, Hadolint, etc.).

CI **Security Guardrails** runs OpenGrep, TruffleHog, and supply-chain scans. CI **Codeowners
Enforcer** requires every changed file to have an owner in `.github/CODEOWNERS` (or an
entry in `.github/.codeownersignore`).

## Layout

| Path                             | Role                                            |
| -------------------------------- | ----------------------------------------------- |
| `.prettierrc`, `.prettierignore` | Formatting (80-char YAML via override)          |
| `.markdownlint.yaml`             | Markdown lint rules (`MD013` off; Prettier wraps) |
| `.yamllint`                      | YAML lint (80-char lines, `document-start` off) |
| `.truffleignore`, `.trivyignore` | Scanner exclusions for security workflows       |
| `.github/CODEOWNERS`             | Required ownership for changed files            |
| `.github/workflows/`             | Quality, security, and CODEOWNERS enforcement   |
| `package.json`                   | Prettier and Markdownlint dev dependencies      |

## Commits

Only commit when the user asks. Do not commit secrets.
