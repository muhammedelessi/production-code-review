# React and TypeScript Review Guide

Apply this reference to React, React-based frameworks, and TypeScript projects.

## React correctness

- Keep render logic pure. Flag mutation of props, state, context values, module-level mutable state, or other pre-existing objects during render.
- Check Hooks are called consistently and only from valid React contexts.
- Inspect Effects for missing cleanup, stale closures, unstable dependencies, update loops, duplicated network requests, and logic that belongs in an event handler or render calculation instead.
- Check async UI flows for race conditions, outdated responses overwriting newer state, and state updates after ownership/lifecycle changes.
- Verify list keys are stable and represent identity rather than accidental render position when order can change.
- Check controlled/uncontrolled form transitions and validation boundaries.

## React performance

- Do not recommend memoization by default. First identify unnecessary work or render churn.
- Prefer local state when state is transient and does not need global ownership.
- Flag expensive work in render when it is measurable or clearly scales with data size.
- Check large lists, repeated subscriptions, duplicated queries, waterfall requests, and avoidable global re-renders.
- Treat performance claims as hypotheses unless supported by a trace, profiler result, or obviously unbounded algorithmic behavior.

## TypeScript

- Prefer `strict` type checking for production codebases unless the repository explicitly documents a reason not to.
- Flag unsafe `any`, unchecked casts, non-null assertions, or overly broad types when they hide a realistic defect.
- Verify discriminated unions, nullable states, API response types, and error types model actual runtime possibilities.
- Check runtime validation at trust boundaries; TypeScript types do not validate network, storage, or user input at runtime.
- Check public types and function contracts for accidental breaking changes.

## Primary sources

- React official Rules of React and Keeping Components Pure.
- TypeScript official TSConfig documentation for `strict` and `noImplicitAny`.
