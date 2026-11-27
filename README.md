# secure-fullstack-lab

**Secure full-stack deployment and DevOps learning lab** — built incrementally, one reviewed pull request at a time, inside GitHub Codespaces.

## Status

Phase 0 (scaffold) in progress. See [docs/ROADMAP.md](docs/ROADMAP.md).

## What this lab covers

- **Secure full-stack app** — a small but production-shaped application used as the vehicle for every lesson.
- **Containerization** — hardened, multi-stage images; non-root runtime.
- **Secure CI/CD** — GitHub Actions with secret scanning, dependency audit, SAST, image scanning.
- **Hardened deployment** — reverse proxy + TLS, security headers, least-privilege secrets handling.
- **Observability & ops** — health checks, structured logs, backups, incident runbook.

## Repository layout

```
.devcontainer/          Codespace definition (Node 22 + Docker-in-Docker)
docs/
  ROADMAP.md            Phased plan with "done when" criteria
  ARCHITECTURE.md       Target architecture and security principles
  ci.yml.example        CI baseline, ready to activate under .github/workflows/
SECURITY.md             Security policy and baseline rules
```

## How we work

1. Every change lands on a branch and goes through a pull request — no direct commits to `main`.
2. CI (gitleaks secret scanning) must pass before merge.
3. Each roadmap phase ships as its own PR with a short write-up of what was learned.

## Getting started (GitHub Codespace)

1. Open this repo on GitHub → **Code → Codespaces → Create codespace**.
2. The devcontainer provisions Node 22, Docker-in-Docker and the GitHub CLI automatically.
3. Port 3000 is pre-forwarded for the app once Phase 1 lands.

## Prerequisites (local, optional)

- Node.js 22+, Docker Engine, git
