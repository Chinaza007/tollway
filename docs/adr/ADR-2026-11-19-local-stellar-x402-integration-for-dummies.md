# ADR for Dummies: Local Stellar integration harness

- **Status:** Proposed, awaiting maintainer approval
- **Date:** 2026-11-19
- **Technical ADR:** [ADR-2026-11-19-local-stellar-x402-integration](ADR-2026-11-19-local-stellar-x402-integration.md)

## The idea

Current integration tests need funded public testnet accounts and are skipped in CI. Installed x402/MPP SDKs map only public network identifiers; quickstart local defaults to Standalone Network ; February 2017.

## What people see

1. Propose quickstart --local with NETWORK_PASSPHRASE='Test SDF Network ; September 2015', supported by quickstart start script's local environment override, plus ExactStellarScheme rpcConfig.url pointing to local RPC. This compatibility approach is unproven until tested and needs explicit maintainer approval.

2. Pin quickstart image by immutable digest, start ephemeral RPC and friendbot, bounded readiness polling, per-run random keypairs and no printed secrets.

3. Fund payer, recipient and facilitator; issue test asset, establish trustlines and deploy Stellar Asset Contract.

## Important limitation

Do not monkey-patch SDKs. Proposed network passphrase must never be used for production.

## What changes

After maintainer approval, this issue's feature or test coverage will be implemented and verified.

## What does not change

These proposal documents do not alter production code, payment settlement or policy enforcement.
