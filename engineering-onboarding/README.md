---
description: Everything you need to get up and running as an engineer at Nine Digital.
---

# Engineering Onboarding

Welcome to Nine Engineering! This guide covers everything you need for your first two weeks.

## Week 1 Checklist

### Access & accounts

- [ ] GitHub organisation access (`nine-digital`) — ask your team lead
- [ ] AWS SSO configured via Okta
- [ ] PagerDuty account linked to your Nine email
- [ ] Datadog access provisioned
- [ ] Slack workspace — join `#engineering`, `#deployments`, `#incidents`
- [ ] 1Password Teams — IT will send an invite on day 1
- [ ] VPN credentials (Tailscale) — see IT setup guide

### Development environment

- [ ] Clone your team's primary service repo
- [ ] Run `make setup` from the repo root (installs dependencies, configures pre-commit hooks)
- [ ] Confirm Docker Desktop is running and `make build` succeeds
- [ ] Install the standard toolchain: `brew bundle --file=Brewfile` in the `dev-tooling` repo

### First day meetings

- [ ] Meet your buddy (assigned by your manager on day 1)
- [ ] Team stand-up — ask your lead for the calendar link
- [ ] Engineering All-Hands (monthly) — check the `#engineering` Slack channel for the next date

## Week 2 Checklist

### Ship something small

The goal of week 2 is to merge your first PR. It doesn't need to be big — a docs fix, a test, a small bug counts.

- [ ] Identify a `good-first-issue` in your team's backlog
- [ ] Read the [CI/CD Standards](../cicd-standards/README.md) before opening your first PR
- [ ] Request a code review from your buddy

### Understand the platform

- [ ] Complete the Internal Developer Platform (IDP) walkthrough (30 min, self-paced — link in IDP space)
- [ ] Shadow an on-call shift — coordinate with your team's current on-call engineer
- [ ] Review the [Incident Response](../incident-response/README.md) runbook

## Key systems

| System | What it's for | Access |
|---|---|---|
| GitHub (`nine-digital`) | Source code, PRs, CI runs | Via Okta SSO |
| ArgoCD | GitOps deployments to Kubernetes | VPN required |
| Datadog | Metrics, logs, traces, dashboards | Via Okta SSO |
| PagerDuty | On-call schedules and alerting | Via Okta SSO |
| Confluence | Legacy documentation (being migrated here) | Via Okta SSO |
| Jira | Sprint planning and issue tracking | Via Okta SSO |

## Getting help

| Question type | Where to ask |
|---|---|
| "How do I set up X?" | `#engineering-help` Slack channel |
| "Who owns service Y?" | `#platform` Slack channel |
| "I think there's a production issue" | `#incidents` — follow the incident response guide |
| "I need access to Z" | `#it-helpdesk` Slack channel |

Your buddy is your first point of contact for anything not covered here. If they can't answer, they'll know who can.
