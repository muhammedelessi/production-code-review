# Testing and Verification Guide

Apply this reference when assessing test quality, release readiness, or the evidence for a finding.

## Test selection

Prefer the smallest test that proves or disproves the behavior first, then broaden verification as needed.

Review whether tests cover:

- happy path and realistic failure path
- authorization allowed and denied cases
- boundary/null/empty/invalid inputs
- concurrency, retries, duplicate delivery, or idempotency when relevant
- migration behavior with pre-existing data
- public API compatibility
- lifecycle/cleanup for UI and mobile code
- regressions for each fixed defect

## Assertion quality

Flag tests that execute code without proving the important outcome. Prefer assertions on observable behavior, persisted state, permissions, emitted events, or returned contracts rather than implementation details.

## Mocks and fixtures

Check that mocks preserve the behavior relevant to the test. A fixture that cannot occur in production can create false confidence. For important bug fixes, verify the test setup is actually reachable from real write/creation paths.

## Commands

When the repository defines lint, typecheck, unit, integration, build, or static-analysis commands, use the project-configured commands rather than inventing replacements.

Never report a command as passing unless it was executed and exited successfully. If tools or dependencies prevent execution, state that as a verification gap.

## Fix verification

After an approved fix:

1. reproduce the original failure when feasible
2. apply the focused fix
3. demonstrate the regression test now passes
4. run adjacent tests/typecheck/lint/build as appropriate
5. re-review the changed surface for second-order regressions
