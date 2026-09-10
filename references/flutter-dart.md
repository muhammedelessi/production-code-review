# Flutter and Dart Review Guide

Apply this reference to Flutter applications and Dart packages.

## Flutter correctness and lifecycle

- Check `State` lifecycle ownership for controllers, focus nodes, animation controllers, streams, subscriptions, listeners, and other disposable resources.
- Verify owned resources are disposed at the correct lifecycle boundary.
- Check asynchronous work for stale `BuildContext`, state updates after disposal, race conditions, and ignored failures.
- Verify navigation and deep-link flows preserve authorization and expected back-stack behavior.
- Check platform permissions and platform-channel calls for denied/unavailable states on Android and iOS.
- Review persistence and secure-storage usage for tokens, credentials, and sensitive data.
- Verify state-management boundaries are explicit and consistent with the project pattern (for example Riverpod, Bloc, Provider, or another established approach). Do not force a state-management migration during review.

## Flutter performance

- Avoid expensive or repeated work in `build()`.
- Flag very large widgets when splitting by change boundary can reduce rebuild scope or improve maintainability.
- Prefer `const` constructors where they are valid and meaningful.
- Localize state changes instead of rebuilding unnecessarily large subtrees.
- Use lazy builders for large or unbounded lists/grids.
- Check image sizes, decoding, repeated network loading, animation cost, clipping/opacity, and layout patterns when they are on a hot path.
- Do not judge release performance from debug mode; profile-mode evidence is preferred for performance findings.

## Dart quality

- Follow Effective Dart naming, API, usage, and documentation conventions when they align with the repository.
- Prefer sound null-safe modeling rather than widespread assertions or forced casts.
- Check Futures and Streams for uncaught errors, accidental serial work, unbounded concurrency, and leaked subscriptions.
- Prefer concise, intention-revealing APIs; avoid needless abstraction that makes ownership or control flow harder to trace.
- Use formatter/linter output as supporting evidence, not a replacement for behavioral review.

## Testing

Check unit tests for domain logic, widget tests for UI behavior, and integration tests for critical end-to-end flows where appropriate. Pay special attention to permissions, offline/error states, navigation, authentication, and lifecycle cleanup.

## Primary sources

- Flutter official Performance Best Practices and rendering performance guidance.
- Dart official Effective Dart guides.
