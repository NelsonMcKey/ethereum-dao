# Security and threat model

Threats to the registry and the voting system. The economic policy is in the [requirements](requirements-spec.md).

## Threats

| Threat | What happens | Response in this design |
| --- | --- | --- |
| Flash-loaned vote | ETH is borrowed and repaid inside the voting transaction. | Weight is a vault checkpoint from the proposal block, so the intra-transaction balance is irrelevant. |
| Borrowed ETH around a snapshot | The attacker holds ETH only for the snapshot block. | The vault's withdrawal delay is at least the voting period plus the timelock. A one-block borrow cannot enter and exit in time. A loan that outlasts the delay still votes. |
| Exchange or custodian deposits | Customer ETH is deposited and voted. | Visible onchain. No contract-level distinction between customer and house funds. Accepted. |
| Whale control of a small vault | Quorum is a fraction of deposits, so a large depositor in a quiet vault passes votes alone. | Public timelock. Quorum fraction is an open parameter and has to be set with this failure in mind. |
| Proposal spam | Empty proposals crowd the queue. | A minimum vault deposit to propose. The number is open. |
| Malicious listing | A contract with a hidden admin or a lookalike address is registered. | Gates, published bytecode evidence, timelock. Integrators still have to read the address. |
| Registry poisoning | A direct write to the list. | Only the governor can write, and only after a successful vote and timelock. |
| Live exploit in a listed contract | Funds are at risk now. | No pause and no patch. Removal is a signal and arrives after the timelock. Users who can exit do so on their own. |
| Dependency capture | An oracle admin or a proxy on a dependency changes behavior the listing cannot stop. | The ownerless gate applies to those dependencies. Oracle-dependent systems usually fail it. |
| Vote buying | A bribe buys a delegation. | Delegation is public. Bribes are not prevented. |

## Invariants

- Listed deployments and the vault have no admin.
- Protocol-level fees are absent or burned. User-to-user fees are untouched.
- Registry entries are added and removed only through the governor.
- Execution waits for the timelock.

## What this project accepts

- No DAO-funded audit program, because there is no treasury. A review paid for by someone else can be evidence. It is not a gate, and it is not something this DAO can promise.
- Reduced ability to respond during an incident. The alternative was an admin key, which this project rejects.
- Staked ETH, LST holders, and WETH holders do not vote unless they unwrap and deposit native ETH.
- Low turnout. Carbonvote is the historical shape of ETH-balance signaling, described in the [voting mechanism](voting-mechanism.md).
