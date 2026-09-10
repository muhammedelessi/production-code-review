# Production Code Review

A reusable, platform-agnostic AI agent skill for evidence-based production code review across web, mobile, backend, API, and database projects.

## What it does

- Reviews a full repository, selected files, a diff, commit, pull request, or pre-release surface.
- Covers correctness, security, data integrity, API contracts, performance, maintainability, testing, migrations, and release risk.
- Includes specialized guidance for React/TypeScript and Flutter/Dart, plus backend/API and database review.
- Uses a strict **Review -> Report -> Approve -> Fix -> Test -> Re-review** workflow.
- Never modifies code during the initial review.
- Produces evidence-based findings and a `GO`, `CONDITIONAL`, or `NO-GO` release recommendation.

## Structure

- `SKILL.md` — control plane and review workflow
- `references/review-method.md` — severity, confidence, and report format
- `references/security.md` — application security review guidance
- `references/react-typescript.md` — React and TypeScript review guidance
- `references/flutter-dart.md` — Flutter and Dart review guidance
- `references/backend-api.md` — backend and API review guidance
- `references/database.md` — database and migration review guidance
- `references/testing.md` — testing and verification guidance
- `references/sources.md` — source basis and maintenance notes
- `agents/openai.yaml` — optional agent UI metadata

## Design philosophy

The skill keeps the main `SKILL.md` compact and loads stack-specific references only when relevant. This reduces context noise and makes it easier to extend to additional frameworks without turning the entrypoint into a monolithic checklist.

## Source basis

The workflow is original and informed by official/public engineering guidance from OpenAI, Microsoft, React, TypeScript, Flutter, Dart, and OWASP. See `references/sources.md`.

## Maintenance

Review framework-specific references periodically. When a rule depends on current runtime or framework behavior, verify the latest official documentation before changing production code.
