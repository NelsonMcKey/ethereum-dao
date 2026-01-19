# Architecture Blueprint

## Purpose
Describe the high-level system architecture for an ETH-holder-governed DAO that curates and deploys immutable, ownerless DeFi primitives with minimal or zero fees that burn ETH.

## Onchain Components
- **Governance Contract**
  - Proposal creation, voting, and execution with timelock.
  - ETH-holder voting mechanism (snapshot or checkpoint based).
- **Primitive Registry**
  - Onchain list of approved immutable deployments.
  - Metadata: commit hash, deployment params, verification links.
- **Deployment Factory**
  - Deterministic deployments (CREATE2) where possible.
  - Enforces immutable configuration and burn-only fee policy.
- **Fee Burn Mechanism**
  - Any protocol fees are routed to an ETH burn sink.

## Offchain Components
- **Documentation Portal**
  - Houses proposals, evidence, and deployment artifacts.
- **Governance UI**
  - Proposal creation, voting, and registry browsing.
- **Research Pipeline**
  - Tracks lindy and adoption metrics for candidate primitives.
- **Verification Tooling**
  - Reproducible build scripts and bytecode comparison.

## Data Flow
- Nomination → evidence upload → governance proposal.
- Vote approval → deployment via factory → registry update.
- Registry update → public discoverability and integration.

## Trust Boundaries
- No admin keys for deployed primitives.
- Governance is the only control surface for registry changes.
- Offchain tooling is informational; onchain state is canonical.

## Key Invariants
- Deployed primitives are immutable and ownerless.
- Fees, if any, are burned.
- Registry entries map to verifiable, reproducible deployments.

## Open Questions
- Exact ETH voting mechanism and anti-sybil measures.
- Whether factory enforcement is feasible for all primitives.
