# Production Code Review

A reusable, platform-agnostic AI agent skill for rigorous production code review across web, mobile, backend, API, and database projects.

> **Version:** 1.0.0  
> **Status:** Public / reusable  
> **License:** MIT

The skill is designed as a production gate, not a style linter. It reviews first, reports evidence, waits for approval before fixes, and finishes with a release recommendation.

## Compatible environments

This skill can be used with:

- Lovable
- OpenAI Codex
- Cursor
- Visual Studio Code with GitHub Copilot Agent Skills
- Google Antigravity
- Other coding agents and vibe-coding tools that support the Agent Skills / `SKILL.md` format

The review logic is editor-independent. Installation and discovery differ by platform, but the same `SKILL.md` and references can be reused.

## What it does

- Reviews a full repository, selected files, diff, commit, pull request, or pre-release surface
- Covers correctness, security, data integrity, API contracts, performance, maintainability, testing, migrations, and release risk
- Includes specialized guidance for React/TypeScript and Flutter/Dart, plus backend/API and database review
- Uses a strict **Review -> Report -> Approve -> Fix -> Test -> Re-review** workflow
- Never modifies code during the initial review
- Produces evidence-based findings and a `GO`, `CONDITIONAL`, or `NO-GO` recommendation

## Installation and usage

### Lovable

Open your Lovable workspace and go to:

**Settings -> Skills -> Import -> GitHub**

Paste:

```text
https://github.com/muhammedelessi/production-code-review
```

Keep the skill enabled for projects where you want structured engineering review.

### OpenAI Codex

Use Codex's skill installer to install the skill from this GitHub repository, or place it under your project's Agent Skills directory, for example:

```text
.agents/skills/production-code-review/
```

Keep the repository structure intact so the agent can load the stack-specific references when needed.

### Cursor

Clone or copy this repository into one of Cursor's supported skill locations.

Project-level examples:

```text
.agents/skills/production-code-review/
.cursor/skills/production-code-review/
```

User-level examples:

```text
~/.agents/skills/production-code-review/
~/.cursor/skills/production-code-review/
```

Cursor can discover the skill automatically for review-related requests or invoke it from Agent chat.

### Visual Studio Code / GitHub Copilot

Copy or clone the repository into a supported Agent Skills directory.

Project-level examples:

```text
.github/skills/production-code-review/
.agents/skills/production-code-review/
```

User-level examples:

```text
~/.copilot/skills/production-code-review/
~/.agents/skills/production-code-review/
```

VS Code can load the skill automatically when relevant or invoke it directly from Copilot Chat.

### Google Antigravity

Project/workspace scope:

```text
<project-root>/.agents/skills/production-code-review/
```

Global scope for Antigravity IDE:

```text
~/.gemini/config/skills/production-code-review/
```

Use project scope when the review standard should travel with the repository, or global scope when you want it available across projects on your machine.

### Other Agent Skills-compatible tools

Place the repository under the tool's supported skills directory and keep `SKILL.md` as the entrypoint. The review workflow is portable as long as the agent can read the referenced files.

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

```text
Review this pull request and give me a GO, CONDITIONAL, or NO-GO recommendation.
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
