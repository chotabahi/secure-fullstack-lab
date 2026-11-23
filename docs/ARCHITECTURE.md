# Target architecture

```
        GitHub Codespace (dev)            CI (GitHub Actions)              Deployment target
 ┌──────────────────────────┐    ┌───────────────────────────┐    ┌─────────────────────────────┐
 │  devcontainer            │    │  lint → tests → audit     │    │  reverse proxy (TLS)        │
 │  ├ Node 22 + gh CLI      │───▶│  gitleaks → CodeQL        │───▶│    └─ app container         │
 │  └ Docker-in-Docker      │    │  Trivy → SBOM             │    │       (non-root)            │
 └──────────────────────────┘    └───────────────────────────┘    └─────────────────────────────┘
```

| Component | Choice | Notes |
|---|---|---|
| App | Next.js (default — finalized in Phase 1) | Vehicle for all lessons |
| Runtime | Containers, non-root | Hardened in Phase 2 |
| CI/CD | GitHub Actions | Scanner suite lands in Phase 3 |
| Edge | Reverse proxy + TLS | Phase 4 |
| Secrets | GitHub/Codespace secrets + env at runtime | Never committed |

## Security principles (enforced from Phase 0)

1. **No secrets in the repository** — gitleaks blocks PRs that add them.
2. **Least privilege** — every workflow job declares minimal `permissions`.
3. **Everything through PRs** — `main` gets branch protection in Phase 3.
4. **Fail closed** — High/Critical scan findings break the build.
5. **Reproducibility** — lockfiles committed and action versions pinned.
