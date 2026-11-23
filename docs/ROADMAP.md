# Roadmap

Phased plan. Each phase = one pull request. A phase is done only when every "done when" item holds.

## Phase 0 — Scaffold & guardrails (this PR)

- [x] Repo structure, README, roadmap, architecture doc
- [x] SECURITY.md with baseline rules
- [x] Codespace devcontainer (Node 22, Docker-in-Docker, gh CLI)
- [x] CI config staged in `docs/ci.yml.example` (activate as `.github/workflows/ci.yml`)

**Done when:** a Codespace starts cleanly from the devcontainer and the CI workflow runs green.

## Phase 1 — Application baseline

- Small full-stack app. Proposed default: **Next.js + TypeScript**; alternatives: Node/Express API + React SPA, or FastAPI + React.
- ESLint + Prettier + unit tests wired into CI.
- Dependency audit job and committed lockfile.

**Done when:** the app runs in the Codespace on port 3000; CI runs lint, tests and audit.

## Phase 2 — Containerization

- Multi-stage Dockerfile, non-root user, minimal base image, `.dockerignore`.
- `docker compose up` runs the app locally (proxy joins in Phase 4).

**Done when:** the image builds in CI; the container runs as non-root; final image size is documented in the PR.

## Phase 3 — Secure CI/CD

- Add Trivy image scanning, SBOM generation (Syft), CodeQL SAST, pinned action SHAs, minimal `permissions` per job.
- Branch protection on `main`: PRs required, CI required.

**Done when:** all scanners run on PRs and fail the build on High/Critical findings; `main` is protected.

## Phase 4 — Hardened deployment

- Reverse proxy (nginx or Caddy) with TLS, security headers (CSP, HSTS, X-Content-Type-Options) and rate limiting.
- Secrets injected via environment/secret manager — never committed (gitleaks enforces this).

**Done when:** the deployment passes a header-check script and all scans are clean.

## Phase 5 — Observability & ops

- `/healthz` and `/readyz` endpoints, structured JSON logging, backup script + restore test, incident runbook.

**Done when:** the runbook is reviewed in a tabletop exercise and a restore is tested from a real backup.
