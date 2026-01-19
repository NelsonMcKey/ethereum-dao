# Primitive Selection Framework

## Purpose
Create a consistent, transparent method to identify and prioritize DeFi primitives that should be curated and deployed as immutable, ownerless, minimal-fee (or fee-free) contracts that burn ETH.

## Selection Process
- **Nomination:** any ETH holder can nominate a primitive and reference candidate codebases.
- **Screening:** community checks for lindy criteria and ownerless deploy feasibility.
- **Scoring:** proposals are scored using the criteria below.
- **Prioritization:** top-ranked primitives move to deployment proposals.

## Core Criteria
- **Usefulness and adoption:** real demand, active usage, and meaningful volume/TVL.
- **Lindy status:** time in production, total usage, and survivability through market cycles.
- **Security history:** known incidents, bug bounty history, and patch frequency.
- **Composability:** how often the primitive is a dependency for other protocols.
- **Immutability feasibility:** can be deployed without admin keys or upgrades.
- **License clarity:** permissive OSS license suitable for reuse.
- **Minimal fee viability:** can run sustainably at zero or minimal fees that are burned.

## Scoring Model (Draft)
Each criterion is scored 1–5. Weighted totals determine priority.

- Usefulness and adoption: 25%
- Lindy status: 25%
- Security history: 20%
- Composability: 15%
- Immutability feasibility: 10%
- License clarity: 3%
- Minimal fee viability: 2%

## Evidence Requirements
- Adoption metrics (usage, volume/TVL, integrator count).
- Deployment age and survivability through cycles.
- Audit history (if any) and known incidents.
- Prior deployments with no admin keys or upgrade paths.
- Codebase license and governance policy.

## Outputs
- Ranked list of candidate primitives.
- Shortlist for governance vote.
- Documentation of rationale and evidence for each ranking.

## Open Questions
- Minimum lindy thresholds for eligibility.
- How to handle primitives with critical dependencies (e.g., oracles).
