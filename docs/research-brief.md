# Research Brief

## Purpose
Collect prior art, governance models, and deployment patterns to inform a DAO that curates and deploys immutable, ownerless DeFi primitives with ETH-only governance and ETH-burn economics.

## Research Questions
- Which DeFi primitives are most critical and widely reused?
- What qualifies as "proven" open-source code?
- How do existing DAOs handle ETH-holder governance?
- What deployment patterns ensure immutability and ownerlessness?
- What incentive structures align with ETH burn only?

## Prior Art to Review
### Governance Models
- ETH-holder voting mechanisms (onchain voting, snapshot-based voting, balance checkpoints).
- Delegation and quorum design.
- Time-locks and proposal lifecycle patterns.

### Ownerless / Immutable Protocols
- Contracts without admin keys or upgrade proxies.
- Patterns for immutable configuration at deployment.
- Common pitfalls (hidden admin controls, dependency upgrades).

### Fee-Free / Minimal-Fee Models
- Protocols with no fees or with fees that are burned.
- Long-term sustainability without fee extraction.

### Open Source Stewardship
- Governance structures that fund audits and maintenance.
- Contribution workflows for upstream projects.
- Licensing considerations for OSS reuse and deployment.

## Candidate Primitives (Initial List)
- AMMs (swap and liquidity)
- Lending/borrowing markets
- Stablecoin minting or overcollateralized lending primitives
- Liquid staking derivatives
- Perpetuals / derivatives primitives
- Oracles (if applicable to the DAO’s scope)
- DEX aggregation / routing

## Evaluation Criteria (For Each Primitive)
- Maturity: time in production, audits, battle-tested usage.
- Security: known incidents, bug bounties, formal verification.
- Composability: how often used as a base layer.
- Maintainability: code quality and documentation.
- Immutability feasibility: minimal need for upgrades.

## Deliverables
- Annotated list of relevant protocols and papers.
- Summary of governance patterns and tradeoffs.
- Shortlist of primitives with priority scoring.
- Risks and constraints discovered during research.

## Output Format
- One-page summary per primitive.
- Comparative matrix of governance patterns.
- Final recommendations for Step 3 requirements.
