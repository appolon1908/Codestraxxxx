# CI/CD authority

## Repository

- Repository: `appolon1908-hue/Codestraxxxx`
- Class: `placeholder`
- Purpose: unclassified placeholder with no runtime authority
- Implementation authority: No application implementation is authorized

## Persistent branches

This repository uses the following persistent branch train:

```text
development
test
staging
production
main
```

Feature and repair branches may be created from `development`. Promotion should proceed by reviewed pull request in this order:

```text
feature/fix -> development -> test -> staging -> production -> main
```

The initial branch bootstrap intentionally places the same CI/CD policy commit on all five persistent branches. That bootstrap is not production deployment evidence.

## Required CI

`.github/workflows/required-ci.yml` runs on every push, every pull request, and manual dispatch. It checks out the exact event SHA, rejects committed secrets, validates JSON/YAML/Markdown, discovers supported project types, runs relevant tests and builds, and uploads sanitized evidence. It never authorizes runtime deployment or external effects.

## Every-branch audit

`.github/workflows/all-branches-audit.yml` runs daily and on manual dispatch. It fetches every branch tip, checks each one in an isolated worktree, and applies the same static repository contract. This covers older branches created before this policy existed.

## Continuous delivery

`.github/workflows/continuous-delivery.yml` runs only on the five persistent branches. It creates deterministic source and build-output archives, records the exact Git source tree and SHA, records SHA-256 checksums, optionally publishes an immutable GHCR candidate only when reproducible build inputs exist, and uploads 90-day release evidence.

Continuous delivery ends at the artifact boundary. Runtime deployment remains separately gated.

## Repository-specific status

This repository is an unclassified placeholder. Continuous delivery produces only a checksummed source/governance evidence bundle. It never creates or deploys a runtime, and this CI/CD bootstrap does not assign production authority.

## Required GitHub settings

After the bootstrap PR is merged, configure `development`, `test`, `staging`, `production`, and `main` or equivalent repository rulesets to require `required-ci`, approving review, resolved conversations, linear history, no force pushes, no branch deletion, and up-to-date protected promotions.

Any future runtime authority requires an explicit repository mission, architecture, owner, protected environments, exact source SHAs, immutable digests, rollback evidence, and a separate reviewed change.
