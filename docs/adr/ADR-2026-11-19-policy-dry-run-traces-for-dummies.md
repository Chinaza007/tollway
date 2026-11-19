# ADR for Dummies: Policy decision traces and dry-run

- **Status:** Proposed, awaiting maintainer approval
- **Date:** 2026-11-19
- **Technical ADR:** [ADR-2026-11-19-policy-dry-run-traces](ADR-2026-11-19-policy-dry-run-traces.md)

## The idea

PolicyEngine.check returns the first failure and client emits a skip string. #189 reservations are open; current check/record does not guarantee atomic concurrent budgets.

## What people see

1. Add evaluate(intent) with versioned trace entries for all configured/unconfigured rule families, in existing order, containing id, configured, limit, current, projected, window and pass/fail/not-applicable; amounts as integer strings.

2. Derive enforce check() from same trace with preserved first-failure rule/detail. Use one clock snapshot and avoid trace/decision disagreement.

3. Mode is explicit 'enforce' or 'dry-run', default enforce. Dry-run warns at construction, allows would-be blocks but records spend on successful settlement.

## Important limitation

Dry-run allows payments that would violate limits; shadow mode cannot change enforcement.

## What changes

After maintainer approval, this issue's feature or test coverage will be implemented and verified.

## What does not change

These proposal documents do not alter production code, payment settlement or policy enforcement.
