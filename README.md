# Template Repository

A GitHub template for new projects with formatting standards, PR-scoped linting,
security guardrails, CODEOWNERS enforcement, and community docs preconfigured.

## Quick start

1. Click **Use this template** on GitHub (or clone and reinitialize).
2. Update **`.github/CODEOWNERS`** with your maintainers.
3. Replace placeholder URLs in **`.github/ISSUE_TEMPLATE/config.yml`** and **CONTRIBUTING.md**.
4. Trim unused `*_run` inputs in **`.github/workflows/quality-checks.yaml`** for your stack.
5. Run **`npm install`** and **`npm run lint`** before opening pull requests.

## Formatting and lint config

| File                                         | Purpose                                          |
| -------------------------------------------- | ------------------------------------------------ |
| [`.prettierrc`](./.prettierrc)               | Prettier defaults (100-char prose, 80-char YAML) |
| [`.prettierignore`](./.prettierignore)       | Build artifacts and lockfiles                    |
| [`.markdownlint.yaml`](./.markdownlint.yaml) | Markdown rules (`MD013` off; Prettier wraps)     |
| [`.yamllint`](./.yamllint)                   | YAML rules (80-char lines)                       |
| [`.truffleignore`](./.truffleignore)         | TruffleHog exclusions                            |
| [`.trivyignore`](./.trivyignore)             | Trivy vulnerability/license exclusions           |

Local lint entrypoint:

```bash
npm install
npm run lint
```

## GitHub workflows

| Workflow                                                            | Reusable source                                                                         | Purpose                                                                           |
| ------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| [quality-checks](./.github/workflows/quality-checks.yaml)           | [garretpatten/quality-checks](https://github.com/garretpatten/quality-checks)           | PR-scoped linters (Prettier, Markdownlint, Yamllint, Shellcheck, ESLint, Ruff, …) |
| [security-guardrails](./.github/workflows/security-guardrails.yaml) | [garretpatten/security-guardrails](https://github.com/garretpatten/security-guardrails) | OpenGrep SAST, verified TruffleHog, dependency review, Trivy                      |
| [codeowners-enforcer](./.github/workflows/codeowners-enforcer.yaml) | [garretpatten/codeowners-enforcer](https://github.com/garretpatten/codeowners-enforcer) | Fail PRs when changed files lack CODEOWNERS coverage                              |

Set each `*_run` input to `false` for tools your project does not use. Jobs no-op when
nothing relevant changed.

## GitHub configuration

- **[CODEOWNERS](./.github/CODEOWNERS)** — default owner for all paths
- **[Dependabot](./.github/dependabot.yaml)** — daily GitHub Actions update PRs (limit 0 open)
- **[Issue templates](./.github/ISSUE_TEMPLATE/)** — bug report and feature request forms
- **[Pull request template](./.github/pull_request_template.md)** — checklist with CoC and security links

## Project docs

- **[CONTRIBUTING.md](./CONTRIBUTING.md)** — how to report issues and run local checks
- **[SECURITY.md](./SECURITY.md)** — vulnerability disclosure and supported scope
- **[CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)** — community standards
- **[AGENTS.md](./AGENTS.md)** — conventions for AI coding agents
- **[LICENSE](./LICENSE)** — MIT

## VS Code

- **[`.vscode/settings.json`](./.vscode/settings.json)** — format on save with Prettier
- **[`.vscode/extensions.json`](./.vscode/extensions.json)** — recommends Prettier extension

## Requirements

- Node.js (for Prettier and Markdownlint)
- GitHub Actions enabled
- Optional locally: `yamllint`, `actionlint`, and stack-specific linters enabled in quality-checks

## License

MIT — see [LICENSE](./LICENSE).
