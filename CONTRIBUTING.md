# Contributing

Participants are expected to follow the [Code of Conduct](./CODE_OF_CONDUCT.md).

## Issues

Security vulnerabilities are **not** tracked in public issues until addressed; see **[SECURITY.md](./SECURITY.md)**.

Use [GitHub Issues](https://github.com/garretpatten/template/issues) with the **Bug report** or **Feature request** form. Include reproduction steps, environment details, and relevant logs (redact secrets and private paths).

## Pull requests

- Branch from **`master`**, focused scope per PR.
- Update **`.github/CODEOWNERS`** when you add paths that need explicit ownership.
- Pin third-party GitHub Actions to full commit SHAs in workflow files; let Dependabot propose bumps.
- Trim unused linters from **`.github/workflows/quality-checks.yaml`** when bootstrapping a new project from this template.

### Checks (from repo root)

```bash
npm install
npm run lint
```

Or step by step:

```bash
npx prettier --check .
npx markdownlint-cli2 "**/*.md" "#node_modules"
yamllint .github .yamllint .markdownlint.yaml
actionlint
```

Install **actionlint** and **yamllint** locally if missing (`brew install actionlint`, `pip install yamllint`). **`npm run lint`** mirrors the Prettier, Markdownlint, and Yamllint portions of CI **Quality Checks**.

Documentation-only changes still need **`prettier`** and **`markdownlint`** on touched Markdown files.
