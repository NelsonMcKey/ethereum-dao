# Security & Threat Model

## Purpose
Identify threats, attack vectors, and mitigations for an ETH-holder-governed DAO that deploys immutable, ownerless DeFi primitives with minimal or zero fees and ETH burn.

## Threat Categories
- **Governance Capture**
  - Whale dominance or coordination to pass harmful proposals.
  - Mitigation: quorum thresholds, timelocks, transparent proposal data.
- **Proposal Spam**
  - Flooding governance with low-quality proposals.
  - Mitigation: proposal templates, sponsorship or minimum stake for submission.
- **Malicious Code Selection**
  - Proposing a codebase with hidden controls or backdoors.
  - Mitigation: lindy criteria, reproducible builds, public bytecode review.
- **Deployment Misconfiguration**
  - Incorrect parameters leading to unsafe behavior.
  - Mitigation: published configuration and deterministic deployment.
- **Registry Poisoning**
  - Unauthorized registry updates or listing of non-immutable deployments.
  - Mitigation: registry updates only via governance execution.
- **Dependency Risk**
  - External oracle or library failures.
  - Mitigation: minimize dependencies and document trust assumptions.

## Invariants to Protect
- Deployments are immutable and ownerless.
- Fees, if any, are burned.
- Registry entries are verifiable and reproducible.
- Governance execution is time-delayed and transparent.

## Operational Risks
- Governance participation fatigue.
- Slow decision cycles in emergencies.
- Limited resources for security review beyond lindy signals.

## Risk Acceptance
- The DAO accepts reduced audit coverage in exchange for reliance on proven, long-running codebases.
- Emergency response is governance-only; no admin keys.

## Open Questions
- Anti-sybil measures for ETH-holder voting.
- Minimum lindy thresholds for different primitive types.
