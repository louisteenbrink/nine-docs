---
description: CI/CD standards and pipeline conventions for all Nine Digital engineering teams.
---

# CI/CD Standards

This document defines the CI/CD standards and pipeline conventions for all engineering teams at Nine Digital.

## Branch Strategy

| Branch | Purpose | Deployment target |
|---|---|---|
| `main` | Production-ready code | Production |
| `staging` | Pre-production integration | Staging |
| `develop` | Active development | Development |
| `feature/*` | Feature branches | PR preview (optional) |
| `hotfix/*` | Emergency fixes | Direct to production via fast-track |

All changes to `main` and `staging` must go through a pull request. Direct pushes are blocked.

## Pipeline Stages

Every service pipeline must include these stages in order:

```
Lint → Unit Tests → Build → Integration Tests → Security Scan → Deploy → Smoke Tests
```

### Stage definitions

**Lint** — ESLint / Prettier / language-specific linters. Fail fast on style violations.

**Unit Tests** — Must achieve ≥80% line coverage. Coverage reports published as PR artefacts.

**Build** — Docker image build, tagged with git SHA. Images pushed to ECR on merge to `develop` and above.

**Integration Tests** — Run against a containerised stack (docker-compose or kind). No external dependencies.

**Security Scan** — Trivy for image vulnerabilities, Semgrep for SAST. Critical/High CVEs block the pipeline.

**Deploy** — Helm chart upgrade via ArgoCD. Deployment manifest changes committed back to the GitOps repo.

**Smoke Tests** — Synthetic health check against the deployed environment. Must pass before the pipeline is marked green.

## Deployment Gates

| Condition | Action |
|---|---|
| Unit test coverage < 80% | Block merge |
| Any Critical CVE | Block merge |
| Smoke tests fail | Auto-rollback, page on-call |
| Deployment > 10 min | Alert SRE |

## Environment Promotion

Code flows: `feature` → `develop` → `staging` → `main`

- **develop → staging**: automatic on merge, no manual approval
- **staging → main**: requires manual approval from a senior engineer or tech lead
- **Hotfixes**: branch from `main`, fast-track approval from on-call lead, merge back to both `main` and `develop`

## Rollback Procedures

ArgoCD maintains the last 10 successful deployment manifests. To roll back:

1. Open ArgoCD dashboard → select the application
2. Click **History & Rollback** → select the target revision
3. Click **Rollback** — ArgoCD will sync the cluster to that state
4. Notify the team in `#deployments` Slack channel with the incident link

For database migrations, rollback must be coordinated with the DBA on-call — see [Database Operations](../database-operations/README.md).

## Pre-Merge Checklist

Before raising a PR, verify:

- [ ] Tests pass locally (`make test`)
- [ ] No new lint errors (`make lint`)
- [ ] Docker image builds cleanly (`make build`)
- [ ] `.env.example` updated if new env vars added
- [ ] CHANGELOG entry added for user-facing changes
- [ ] Dependent services notified if API contract changed
