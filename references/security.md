# Security Review Guide

Apply this reference when the scope includes authentication, authorization, user-controlled input, sensitive data, secrets, uploads, payments, external integrations, admin functions, or internet-facing endpoints.

## Review priorities

- Enforce authorization at the server or trusted data boundary, not only in UI state.
- Check object-level and tenant-level ownership on every sensitive read and write path.
- Verify authentication/session assumptions, logout/revocation behavior, token storage, expiry, and privilege changes.
- Treat client-side configuration and shipped application bundles as public; never rely on them to protect privileged secrets.
- Validate untrusted input at the boundary where it becomes trusted data or an executable/query/path parameter.
- Check injection surfaces: SQL/NoSQL, command execution, templates, URLs, file paths, headers, redirects, and structured parsers.
- Check file uploads for type, size, storage path, authorization, malware/content risk, and public-access assumptions.
- Check exception handling for sensitive-data leakage and fail-open authorization behavior.
- Review dependency and build-chain risk when new packages, install scripts, remote assets, or executable tooling are introduced.
- Check logging for credentials, tokens, personal data, payment data, or other sensitive content.
- Verify cryptographic choices use established platform/library primitives rather than custom cryptography.
- Check rate limits, replay resistance, idempotency, and abuse controls on costly or sensitive operations.

## Security evidence standard

A security finding should identify:

1. attacker/user capability
2. reachable entry point
3. missing or broken control
4. affected asset or action
5. concrete impact

Avoid generic statements such as "this may be insecure" without a reachable path.

## Secure-fix behavior

Do not auto-fix during the initial review. When fixes are approved, preserve compatibility and test both permitted and denied cases. Security changes frequently cause regressions when existing insecure behavior has become an implicit dependency.

## Primary sources

- OpenAI `security-best-practices` skill in the official `openai/skills` repository.
- OWASP Top 10:2025 and OWASP Developer Guide.
