# Database and Migration Review Guide

Apply this reference to relational or document databases, schema changes, migrations, indexes, access policies, and persistence logic.

## Data integrity

- Check constraints match business invariants rather than relying only on application validation.
- Check nullability, uniqueness, foreign-key behavior, defaults, enum/value constraints, and delete/update cascades.
- Trace every new persisted field through create, update, read, serialization, deduplication, and migration paths.
- Check race-sensitive read-then-write sequences for atomicity or uniqueness protection.

## Migrations

- Review migration behavior against existing production data, not only empty databases.
- Flag destructive operations, incompatible type changes, unsafe defaults, long table locks, and non-null additions without a safe backfill path.
- Check rollback/recovery strategy for irreversible changes.
- Separate expand/backfill/contract stages when a single-step migration would break old and new application versions during rollout.

## Query performance

- Check missing indexes on frequent filters, joins, foreign keys, ordering, and uniqueness constraints when data scale makes them relevant.
- Look for N+1 queries, unbounded result sets, offset pagination at large scale, unnecessary full-row reads, and repeated queries inside loops.
- Prefer evidence from query plans or realistic data volume for performance claims.

## Access control

- Check database-level permissions, policies, tenant isolation, and privileged functions where applicable.
- Do not assume application UI restrictions protect database rows.
- For platforms with row-level security, verify both read and write conditions and test positive and negative authorization cases.

## Specialist skills

If a dedicated database/platform skill is available, consult it for platform-specific semantics. For Supabase/Postgres, prefer the dedicated Supabase/Postgres skill for RLS, Auth-linked policies, views, security-definer behavior, indexes, and migration details.
