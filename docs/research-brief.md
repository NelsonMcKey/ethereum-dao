# Research brief

Prior art that the current draft actually uses. Open choices are not repeated here; they are in [open questions](open-questions.md).

## Voting

The design comparison is the [voting mechanism](voting-mechanism.md). In short: contracts see current ETH balances; EIP-2935 extends block-hash history to 8191 blocks and does not by itself provide a long lookback; Carbonvote (July 2016) showed low turnout for unlocked ETH signaling; Snapshot-style votes do not execute without an oracle.

## Fees

AMM swap fees and lending interest pay the user who takes the inventory risk. They are not rent. Uniswap v2's whitepaper (March 2020) separates the 0.30 percent LP fee from an optional protocol fee of one sixth of that, controlled by `feeToSetter`. The [dossier](dossiers/amm-constant-product.md) checks the live state of that switch.

## Deployments worth knowing, and why they are not automatic listings

| System | What was checked | Why it is not listed from this brief |
| --- | --- | --- |
| Uniswap v2 factory | See the dossier. GPL-3.0. Factory created 2020-05-04. Protocol fee is on. Fee setter is a timelock whose admin is a UNI governor. | Fails ownerless and protocol-fee gates. |
| Liquity v1 | See the [deployment program](deployment-program-spec.md). GPL-3.0. Core `owner()` is zero. Deployed 2021-04-05. Price proxy owner is not zero. Launch post says LQTY receives protocol fee revenue. | Fails the oracle dependency and the protocol-fee gate. |
| Lending markets, perps | Not dossiered. | Typically need an owned oracle, a liquidator role, or both. |
| LST and beacon staking | Deposit-contract balance cited in the voting doc. | The issuer or the protocol is an admin. Staked ETH is not a balance this registry can govern. |
| DEX routers and aggregators | Not dossiered. | Stateless helpers. The lindy sits in the pools, not in a new router. |

## License

GPL-3.0 is OSI-approved and allows deployment, with copyleft obligations. A "permissive only" rule would have rejected both Uniswap v2 core and Liquity v1. On 2024-07-03 Liquity announced that v2 would be published under the Business Source License, which is not an OSI license and would fail the gate. That is an announcement, not a check of the shipped v2 license file. v1 remains the system checked onchain. <https://www.liquity.org/blog/licensing-liquity-v2-may-the-fork-be-with-you>
