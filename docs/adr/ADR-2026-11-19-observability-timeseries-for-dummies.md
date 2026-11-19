# ADR for Dummies: Asset-safe observability time series

- **Status:** Proposed, awaiting maintainer approval
- **Date:** 2026-11-19
- **Technical ADR:** [ADR-2026-11-19-observability-timeseries](ADR-2026-11-19-observability-timeseries.md)

## The idea

The in-memory hub summarizes all outcomes and adds mixed-asset amounts; no time buckets or percentiles exist. The SQL store #217 remains open.

## What people see

1. Add timeseries with 1m, 5m, 1h and 1d UTC epoch-aligned half-open buckets; require valid from/to and reject reversed ranges.

2. Return contiguous bucket envelopes with empty buckets; each populated model (default), payer or payee and asset row reports settled bigint amount as integer string, settled/failed/skipped counts, and p50/p95/p99. Never invent an asset for empty buckets.

3. Nearest-rank percentiles use sorted finite nonnegative latency samples, rank ceil(p*n); no samples means null percentiles. Only settled outcomes contribute amounts.

## Important limitation

Existing totalAmount and other flat maps remain deprecated and cannot be treated as asset-safe.

## What changes

After maintainer approval, this issue's feature or test coverage will be implemented and verified.

## What does not change

These proposal documents do not alter production code, payment settlement or policy enforcement.
