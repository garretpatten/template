# Security policy

## Supported scope

Security fixes ship on the default branch (**`master`**). Consume this repository by pinning commits or forks for supply-chain control rather than blindly tracking **`master`** when that matters.

## Reporting a vulnerability

Email **Garret Patten** at **<garret.patten@proton.me>** with:

- Brief description of impact and suspected component (script path, workflow, dependency, or config).
- Whether you believe it is remotely exploitable and any proof-of-concept you can safely share.

You should receive acknowledgement of receipt; substantive updates align with remediation progress. If a finding is declined, reasoning will be given.

Do not open public GitHub issues for security-sensitive reports.

### Out of scope without prior agreement

- Social engineering against maintainers or users.
- Physical access or already-compromised hosts.
- Theoretical attacks without a plausible path through this repository's automation or artifacts (document gaps as issues instead).

## Automated checks

Pull requests run [Security Guardrails](https://github.com/garretpatten/security-guardrails) (OpenGrep SAST, verified TruffleHog secrets, dependency review, Trivy vulnerability and license scans) and [Quality Checks](https://github.com/garretpatten/quality-checks) linters. Do not commit secrets, credentials, or sensitive personal data.
