# PRD

## Summary
An ETH-holder-governed DAO that identifies proven, useful DeFi primitives, contributes to their open-source development, and deploys immutable, ownerless, minimal-fee (or fee-free) contracts that burn ETH.

## Goals
- Deliver immutable, ownerless deployments of high-priority DeFi primitives.
- Ensure real-world usefulness and adoption.
- Provide ETH-burn economics as the sole value flow.
- Maintain simple, transparent governance for ETH holders.

## Non-Goals
- Launching a token.
- Running a treasury or distributing fees.
- Permissioned control, admin keys, or upgrade paths.

## Users
- ETH holders who want neutral, long-lived DeFi infrastructure.
- Developers seeking durable primitives to integrate.
- Open-source contributors who want to steward proven code.

## Core User Flows
1. **Nominate a primitive**
   - Submit a proposal with evidence of adoption and lindy status.
2. **Review and score**
   - Community review using the selection framework.
3. **Vote and approve**
   - ETH-holder governance vote.
4. **Deploy and verify**
   - Immutable deployment with verifiable bytecode.
5. **Registry listing**
   - Public registry entry for integration.

## Functional Requirements
- ETH-holder voting with snapshot/checkpoint mechanism.
- Onchain proposal lifecycle with timelock.
- Immutable deployment factory (where feasible).
- Onchain registry of approved deployments.
- Fee policy: zero or minimal, and burned.

## Non-Functional Requirements
- Immutability and ownerlessness enforced.
- Transparent, auditable deployment process.
- Reproducible builds and bytecode verification.
- High signal-to-noise governance UX.

## Metrics
- # of primitives deployed.
- Usage/TVL for deployments.
- ETH burned.
- Governance participation rate.

## Risks
- Governance capture by large ETH holders.
- Slow or low participation.
- Over-reliance on lindy without audits.
- Misconfiguration of deployments.

## Open Questions
- Exact voting mechanism and quorum thresholds.
- Minimum lindy/adoption thresholds for eligibility.
