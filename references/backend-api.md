# Backend and API Review Guide

Apply this reference to HTTP APIs, RPC services, server functions, workers, Node.js/Python backends, and server-side business logic.

## Contracts and validation

- Validate external input at the boundary before using it in business logic, persistence, paths, templates, or downstream calls.
- Check response schemas, status/error semantics, nullability, pagination, filtering, and backward compatibility.
- Treat generated clients and actual serialized payloads as part of the public contract.
- Check versioning or compatibility when changing names, enums, required fields, defaults, or response shapes.

## Reliability

- Trace exceptions from origin to final response or retry layer; identify unhandled errors and silent failures.
- Check timeouts, retries, exponential backoff where appropriate, and retry safety.
- Verify idempotency for operations that can be repeated by clients, queues, webhooks, or infrastructure.
- Check partial failures when one request performs multiple writes or external side effects.
- Review transaction boundaries and compensation/rollback behavior.
- Flag unbounded loops, queues, concurrency, recursion, payload sizes, or memory growth.

## Authorization

- Apply auth checks at the trusted server/data boundary.
- Check both function-level permission and object/tenant ownership.
- Verify admin endpoints, internal routes, webhooks, background jobs, and service-to-service calls do not inherit unsafe trust assumptions.

## External integrations

- Validate webhook authenticity where the provider supports signatures.
- Check secrets are server-side and rotated/configured through supported secret mechanisms.
- Check timeouts, retries, duplicate deliveries, and provider error handling.
- Avoid logging raw tokens, credentials, payment data, or personal data.

## Operability

- Ensure important failure paths produce actionable logs/metrics without exposing secrets.
- Check health/readiness behavior when dependencies are degraded.
- Check environment configuration fails safely when required values are missing.
