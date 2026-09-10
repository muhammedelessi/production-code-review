# Production Code Review

A reusable, platform-agnostic AI agent skill for rigorous production code review across web, mobile, backend, API, and database projects.

> **Version:** 1.0.0  
> **Status:** Public / reusable  
> **License:** MIT

The skill is designed as a production gate, not a style linter. It reviews first, reports evidence, waits for approval before fixes, and finishes with a release recommendation.

## What it does

- Reviews a full repository, selected files, diff, commit, pull request, or pre-release surface
- Covers correctness, security, data integrity, API contracts, performance, maintainability, testing, migrations, and release risk
- Includes specialized guidance for React/TypeScript and Flutter/Dart, plus backend/API and database review
- Uses a strict **Review -> Report -> Approve -> Fix -> Test -> Re-review** workflow
- Never modifies code during the initial review
- Produces evidence-based findings and a `GO`, `CONDITIONAL`, or `NO-GO` recommendation

## Import into Lovable

1. Open your Lovable workspace.
2. Go to **Settings -> Skills -> Import -> GitHub**.
3. Paste this repository URL:

```text
https://github.com/muhammedelessi/production-code-review
```

4. Import the skill and keep it enabled for projects where you want structured engineering review.

## Example requests

```text
Review this project before production release.
```

```text
Review the last change for correctness, regressions, security, and missing tests.
```

```text
Audit the architecture and identify the highest-risk maintainability problems. Do not modify code yet.
```

```text
Review this API and database flow for data-integrity and authorization issues.
```

## Review philosophy

Critical and High findings require concrete evidence when available: file/line references, broken contracts, execution traces, permission paths, failing tests, or reproducible risk. The reviewer separates confirmed findings from hypotheses and explicitly reports coverage gaps.

Fixes are intentionally gated behind explicit user approval and should be incremental rather than bundled with unrelated cleanup.

## Repository structure

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── review-method.md
│   ├── security.md
│   ├── react-typescript.md
│   ├── flutter-dart.md
│   ├── backend-api.md
│   ├── database.md
│   ├── testing.md
│   └── sources.md
├── CHANGELOG.md
├── CONTRIBUTING.md
└── LICENSE
```

## Source basis

The workflow is original and informed by official/public engineering guidance from OpenAI, Microsoft, React, TypeScript, Flutter, Dart, and OWASP. See `references/sources.md`.

## Contributing

Issues and pull requests are welcome. See `CONTRIBUTING.md` before proposing behavior or severity-model changes.
