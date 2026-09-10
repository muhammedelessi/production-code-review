# Review Method and Report Contract

Use this file for severity, confidence, deduplication, and final reporting.

## Severity

### Critical
A realistic path to catastrophic or immediate harm, such as authentication bypass, cross-tenant data access, remote code execution, destructive data loss, exposed high-value secrets, unrecoverable migration failure, or a production outage with no practical containment.

### High
A serious correctness, security, integrity, availability, or compatibility defect likely to affect real users or important workflows. Examples include privilege escalation with prerequisites, duplicate financial side effects, major contract breakage, unsafe migration behavior, or a common-path crash.

### Medium
A meaningful defect or risk with limited blast radius, stronger prerequisites, or a practical workaround. Examples include incomplete validation, localized performance degradation, brittle error handling, or an uncovered edge case with user-visible impact.

### Low
A non-blocking maintainability, resilience, observability, accessibility, or efficiency issue with limited direct production impact.

Do not inflate severity because an issue sounds security-related. Rate actual exploitability, likelihood, blast radius, and impact.

## Confidence

- **High:** directly demonstrated or clearly proven from code and reachable behavior.
- **Medium:** strong evidence but one material runtime assumption remains unverified.
- **Low:** plausible concern requiring more context or runtime verification.

Critical findings should normally have High confidence. If they do not, investigate further or downgrade.

## Deduplication

Report the root cause once and list affected locations beneath it. Do not create multiple findings for repeated symptoms of the same defect.

## Required Report

```markdown
# Production Code Review: <scope>

## Executive Summary
- Scope reviewed: ...
- Stack detected: ...
- Release recommendation: GO | CONDITIONAL | NO-GO
- Blocking findings: ...

## Findings

### Critical
#### PCR-001 — <title>
- Category: ...
- Evidence: path/to/file.ext:line
- Impact: ...
- Reproduction / trace: ...
- Recommendation: ...
- Confidence: High | Medium | Low

### High
...

### Medium
...

### Low
...

## Test Coverage Gaps
- ...

## Verification Performed
- Command/check: result

## Review Gaps and Assumptions
- ...

## Positive Observations
- Only include concrete practices that materially reduce risk.
```

If a severity section has no findings, omit it.

## Release Recommendation

**NO-GO** when at least one confirmed blocker remains.

**CONDITIONAL** when no confirmed blocker remains but specific verification, migration, rollout, or monitoring conditions are required.

**GO** when no blocking risk was found in scope and the executed verification supports release. State untested or inaccessible areas even with GO.
