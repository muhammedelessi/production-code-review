---
name: production-code-review
description: "Perform rigorous, read-first production code reviews for full repositories, selected files, diffs, commits, or pull requests. Use when asked to review code quality, correctness, security, performance, maintainability, architecture, tests, release readiness, regressions, or production risk across web, mobile, backend, API, database, React/TypeScript, Flutter/Dart, Node.js, Python, and mixed-stack projects. Produce evidence-based findings with severity, file/line references when available, verification gaps, and a GO/CONDITIONAL/NO-GO recommendation. Do not modify code during the initial review; fixes require explicit approval."
---

# Production Code Review

Review software as a production gate, not as a style exercise. Prioritize defects and risks that change confidence in correctness, security, operability, performance, or maintainability.

## Non-Negotiable Review Contract

1. **Review first.** Do not edit, refactor, migrate, delete, reformat, or restructure code during the initial review.
2. **Evidence over intuition.** Every Critical or High finding must cite concrete evidence such as a file and line, a reproducible trace, a failing test, a broken contract, or a specific attack path.
3. **No invented certainty.** Separate confirmed findings from hypotheses and explicitly state review gaps.
4. **Preserve behavior.** Do not recommend broad refactors when a focused fix addresses the risk.
5. **Approval before fixes.** After reporting findings, wait for explicit user approval before making changes.
6. **Fix incrementally.** Once approved, fix one coherent finding or tightly related group at a time, run relevant verification, then re-review the affected surface.

## Review Modes

Identify the requested surface before analysis:

- **Full repository:** review architecture, critical paths, cross-cutting risks, tests, and release readiness.
- **Targeted files or directory:** review the requested surface plus the minimum surrounding context needed to validate contracts and callers.
- **Diff / commit / pull request:** focus on changed behavior, regressions, affected callers, migrations, compatibility, and missing tests.
- **Pre-release gate:** emphasize production failures, security, data integrity, rollback risk, observability, and deployment readiness.

If scope is ambiguous, choose the narrowest scope that satisfies the request and state it. Never claim full-repository coverage if only part of the code was inspected.

## Workflow

### 1. Establish scope and stack

Identify:

- languages, frameworks, runtime, package manager, and build system
- application type: web, mobile, backend, library, worker, API, or mixed
- authentication and authorization boundaries
- databases, queues, storage, external services, and payment or sensitive-data paths
- test frameworks and CI checks
- deployment/runtime assumptions when visible

Load only the references relevant to the detected stack:

- React or TypeScript: `references/react-typescript.md`
- Flutter or Dart: `references/flutter-dart.md`
- Backend or APIs: `references/backend-api.md`
- Database or migrations: `references/database.md`
- Security-sensitive scope: `references/security.md`
- Test quality or release verification: `references/testing.md`
- Severity and report rules: `references/review-method.md`

If a dedicated domain skill is available, use it for domain-specific validation rather than duplicating specialist rules. For example, use a Supabase-specific skill for Supabase Auth, RLS, migrations, or platform-specific database behavior.

### 2. Build enough context

Read the target and the surrounding code that determines its behavior. For meaningful changes, inspect relevant:

- callers and callees
- interfaces, schemas, DTOs, types, and validation
- auth guards and permission checks
- persistence/write paths and read paths
- error handling and retry behavior
- tests and fixtures
- configuration and environment assumptions

For a diff or PR, do not review changed lines in isolation. Check the landing surface and any contract that the change can break.

### 3. Review by risk

Prioritize in this order:

1. correctness and data integrity
2. authorization, authentication, secrets, and trust boundaries
3. production failure modes and error handling
4. migrations, schema compatibility, and destructive changes
5. API and caller contracts
6. concurrency, idempotency, retries, and duplicate side effects
7. performance and resource consumption
8. test coverage and assertion quality
9. maintainability and avoidable complexity
10. accessibility or platform-specific quality when relevant

Do not report generic formatting or naming preferences unless they materially affect maintainability, correctness, or consistency with an established project standard.

### 4. Verify findings

For every Critical or High finding, try to confirm the issue with at least one of:

- a concrete input and step-by-step execution trace
- a failing or missing test case that demonstrates the risk
- a caller/contract mismatch
- a permissions or data-flow trace
- a migration/data-state example
- a measurable performance path

If verification is incomplete, lower confidence or severity rather than overstating the finding.

### 5. Check tests and release safety

Determine whether tests cover the changed or risky behavior, including negative paths and authorization boundaries. Check whether available lint, typecheck, test, and build commands are appropriate to run. Do not claim they passed unless they were actually executed successfully.

For production-impacting changes, check rollback and compatibility risks. Treat migrations that can fail on existing data, corrupt data, or cause irreversible loss as release blockers unless a safe path is demonstrated.

### 6. Produce the report

Use the structure in `references/review-method.md`. Findings must be ordered by severity and deduplicated by root cause.

Each finding should include:

- ID and severity
- category
- evidence (`file:line` when available)
- what is wrong
- production impact
- reproduction or reasoning trace
- recommended direction, not an unsolicited code rewrite
- confidence: High / Medium / Low

Finish with one release recommendation:

- **NO-GO** — confirmed blocker or unacceptable production/security/data risk
- **CONDITIONAL** — shippable only after named conditions or verification steps
- **GO** — no blocking finding discovered within the reviewed scope

A GO is not a guarantee of defect-free software. Always state meaningful coverage or verification gaps.

## Fix Phase

Enter this phase only after explicit approval.

1. Confirm which finding IDs are approved for remediation.
2. Make the smallest safe change that resolves the root cause.
3. Preserve public behavior unless behavior change is required and approved.
4. Add or update a regression test when practical.
5. Run the narrowest relevant verification first, then broader checks if warranted.
6. Re-review the modified surface for regressions and second-order effects.
7. Report exactly what changed and what remains unresolved.

Do not bundle unrelated cleanup into a security or correctness fix.

## Interaction With Project Rules

Treat repository-specific instructions, architecture decisions, linting rules, and established conventions as higher-context constraints. Flag a conflict when a local rule creates an apparent production risk; do not silently ignore either side.

When reviewing legacy code, distinguish pre-existing debt from defects introduced or exposed by the current change. Avoid turning a focused review into an unbounded rewrite proposal.
