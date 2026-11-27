# Security policy

## Baseline rules for this lab

1. **No secrets in the repo.** API keys, tokens, passwords and private URLs live in GitHub/Codespace secrets or environment variables only. CI enforces this with gitleaks.
2. **PRs only.** Direct pushes to `main` are disabled once branch protection lands (Phase 3).
3. **Least privilege.** Workflow jobs declare minimal `permissions`; containers run as non-root.
4. **Dependency hygiene.** Lockfiles committed; `npm audit` (and later Trivy/CodeQL) must pass with no High/Critical findings.
5. **Fail closed.** Security findings block merges; exceptions require a written note in the PR.

## Reporting a vulnerability

This is a personal learning lab — still, if you find a real issue, open a [security advisory](https://github.com/chotabahi/secure-fullstack-lab/security/advisories/new) or contact the owner privately instead of filing a public issue. Please allow a few days for a fix before public disclosure.
