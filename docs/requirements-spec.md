# Requirements Spec

## Purpose
Define the functional and non-functional requirements for an ETH-holder-governed DAO that curates and deploys immutable, ownerless DeFi primitives with minimal or zero fees and ETH-burn economics.

## Functional Requirements
- ETH-holder governance: voting eligibility based on ETH ownership.
- Proposal lifecycle: submit, review, vote, execute with timelocks.
- Primitive registry: onchain registry of approved immutable deployments.
- Deployment workflow: curate proven OSS code → deploy immutable contracts.
- Fee policy: zero fees where possible; otherwise fees are burned.
- Transparency: onchain records for proposals, votes, deployments, and registry updates.

## Non-Functional Requirements
- Immutability: no upgrade proxies or admin keys in deployed primitives.
- Security: rely on lindy codebases, conservative scoping, and verifiable build/deploys rather than mandatory audits.
- Censorship resistance: governance and registry updates are onchain.
- Composability: primitives are standards-compliant and easy to integrate.
- Usability: clear governance UX for ETH holders.
- Reliability: deployments are deterministic and reproducible.

## Constraints
- No token issuance or protocol revenue distribution.
- Governance restricted to ETH holders.
- No treasury or custodial funds.
- Immutable deployment patterns only.
- Open-source codebases with permissive licenses.

## Governance Constraints
- Voting weight tied to ETH balance (mechanism TBD).
- Quorum and threshold requirements to prevent capture.
- Timelocks for execution.
- Emergency response limited to governance-approved actions (no admin keys).

## Deployment Constraints
- Proven code requirement: minimum time in production, audit history, and usage.
- Immutable configuration at deploy time (no owner or upgrade privileges).
- Clear fee configuration (0 or minimal + burn).
- Dependency risk review for external oracles and libraries.

## Compliance & Legal Considerations
- No profit distribution, no token sale.
- Avoid centralized operators or custodial control.
- Transparent governance documentation.

## Assumptions
- Sufficient OSS primitives exist and can be contributed to.
- The DAO can rely on lindy protocols and longevity as a security signal.
- ETH-holder voting is acceptable for legitimacy.

## Open Questions
- Snapshot vs continuous ETH voting and anti-sybil measures.
- Fee level and burn mechanism that ensures sustainability.
- Minimum lindy thresholds (time in production, usage) for deployment eligibility.
