# Open questions

Every unresolved decision lives here. Other docs link to this page instead of keeping their own lists. "Owner" is the person accountable for the decision.

## Needs the owner

| # | Question | Status |
| --- | --- | --- |
| 1 | Accept the [voting escrow](voting-mechanism.md): an immutable vault holds depositor ETH, governance cannot move it, and only deposited ETH votes. | Proposed |
| 2 | If 1 is rejected, build the state-root log fallback instead. That fallback has a keeper-style liveness duty and a weaker defense against borrowed ETH. | Open, only if 1 is rejected |
| 3 | Set the voting period, timelock, withdrawal delay, quorum fraction of vault ETH, approval threshold, minimum balance to propose, and the hardcoded floors below which a later vote cannot put those values. The delay must be at least the voting period plus the timelock. Quorum and timelock floors are above zero. | Open |
| 4 | Set the minimum deployment age, and the usage measure, that a listing needs before it can score well on lindy. The framework defines the criterion. It does not yet set a number. | Open |
| 5 | Choose the next primitive to put through a dossier. The [constant-product AMM dossier](dossiers/amm-constant-product.md) does not produce a listing. | Open |

## Decided in this draft

The owner can reverse these. They are recorded so they are not re-litigated in every file.

| Decision | Where |
| --- | --- |
| No protocol-level fee. User-to-user fees stay. A protocol-level fee, if one is ever charged, is burned and cannot be redirected. | [Requirements](requirements-spec.md) |
| Immutability, license, and protocol-fee policy are pass/fail gates. The scored weights are usefulness 29, deployment lindy 29, security history 24, composability 18. | [Selection framework](primitive-selection-framework.md) |
| The registry may list an existing deployment. A new deployment needs a reason beyond "we want our own copy." | [Deployment program](deployment-program-spec.md) |
| Registry removal is a signal to integrators. It does not stop the contract. Emergency action has the same timelock and no admin key. | [Governance charter](governance-charter.md) |
| No treasury, no grants program, no DAO-paid audits. External parties may pay for reviews. An audit is not a gate. | [Requirements](requirements-spec.md), [Threat model](security-threat-model.md) |
| Licenses must be OSI-approved and must allow modification and deployment. GPL-3.0 qualifies. Business Source and non-commercial terms do not. | [Requirements](requirements-spec.md) |
| Offchain Snapshot-style votes are discussion only and do not execute. | [Voting mechanism](voting-mechanism.md) |
| ETH burned is not a success metric. | [Vision brief](vision-brief.md) |

## Closed

- Current-balance voting. A same-transaction flash loan is counted. Rejected.
- Quadratic or capped voting. It needs an identity system this project does not have. Rejected.
- "Anti-sybil" measures for linear ETH weighting. Splitting a balance does not raise its weight. Not applicable.
- Counting beacon ETH, LSTs, or the WETH contract in v1. Rejected under the recommended voting design.
- A DAO treasury, fee distributions, and proposal type "treasury allocations and grants." Removed.
- Permissive-only licensing. It would exclude GPL code such as Uniswap v2 core and Liquity v1. Replaced.
- Mandatory audits, and the DAO funding them. Inconsistent with having no treasury. Replaced by external review plus deployment history.
