# Deployment program

How a deployment is reviewed and, rarely, created. Selection rules are in the [framework](primitive-selection-framework.md).

## List what already exists

Lindy sits on a deployment: its liquidity, its integrators, and its incident history. Redeploying the same bytecode at a new address resets all three and splits liquidity with the original. The registry's default action is to list an existing deployment that passes the gates, or to list nothing.

Failing the gates is a reason not to list. It is a reason to deploy a replacement only when the existing system is unfit to use.

A new deployment is justified only when all of the following hold:

- There is no live deployment of this function, or the live one is provably broken and integrators need a successor address. A fee this DAO would not charge, or an admin this DAO would not hold, is grounds to withhold a listing. It is not grounds to launch an empty copy.
- The new deployment is ownerless at the moment it is created. Renouncing later is not the plan, because "later" is an admin.
- The proposal says, in plain text, that liquidity and integrators start at zero and may never move.

A new deployment is not justified to put this DAO's name on a working system, to route around a fee on a contract this DAO does not control, or to hope that liquidity will migrate.

## Oracle-dependent primitives

A primitive that needs a price usually fails the ownerless gate. The failure is the oracle's admin, not the math.

Liquity v1 is the test case, checked at block 26,389,703:

- `BorrowerOperations` was deployed 2021-04-05 08:26:29 UTC from `0xa850535D3628CD4dFEB528dC85cfA93051Ff2984`, the deployer the project announced in advance.
- `owner()` on PriceFeed, TroveManager, BorrowerOperations, ActivePool, StabilityPool, and SortedTroves is the zero address.
- PriceFeed's own comments and code use a primary aggregator and a Tellor fallback. `priceAggregator()` is `0x5f4eC3Df9cbd43714FE2740f5E3616155c5b8419`, whose `description()` is "ETH / USD" and whose `decimals()` is 8. That proxy's `owner()` is `0x21f73D42Eb58Ba49dDb685dc29D3bf5c0f0373CA`, not zero, and `aggregator()` points at a separate implementation.
- The source is GPL-3.0, which passes the license gate.
- Liquity's launch post says LQTY captures the system's fee revenue via staking. That is a protocol-level fee paid to a token. It fails the fee gate on its own. This draft did not re-derive the fee formula from the contracts.

The core contracts are ownerless. The price they liquidate against is not, and the fee does not burn. This registry does not list Liquity v1. Lending markets and perpetual venues usually have the same shape: a renounced core, or a core that was never renounced, in front of an oracle somebody else administers. A primitive with no external price, such as a two-asset constant-product pool, is a better fit, and even that fit depends on the deployment. See the [AMM dossier](dossiers/amm-constant-product.md).

Sources for the Liquity reads: `eth_call` and the creation transaction at block 26,389,703; addresses from `liquity/dev` `packages/contracts/mainnetDeployment/mainnetDeploymentOutput.json`; oracle wiring from `PriceFeed.sol` in that repo; GPL statement from the repository disclaimer; deployer pre-announced in Liquity's "Launch Details" post, 2021-03-24, <https://www.liquity.org/blog/liquity-launch-details>. The fee-to-LQTY point is from that same post. The oracle owner's powers beyond `owner()` and `aggregator()` were not enumerated.

## Stages for a new deployment

1. Intake names the source commit, the license, and why no existing address qualifies.
2. Gate review and scoring, with lindy and usefulness starting at 1.
3. Publish init parameters, bytecode hash, and the verification steps.
4. Governance vote and timelock.
5. Deploy. Verify the bytecode. Register the address.

If verification fails, the address is not registered. There is no admin who can fix it in place. The remedy is a new proposal.

## Artifacts

- Source repository, tag or commit, and license.
- Deployment address and creation transaction, once it exists.
- Init parameters, including the protocol-fee setting.
- Bytecode hash and the command that reproduces it.
- A short dependency list. Any oracle or upgradeable library is a gate failure.

## Fee configuration

Follow the [fee policy](requirements-spec.md). On a constant-product pool the trader-to-LP fee stays. The protocol-fee recipient is unset, and the setter is the zero address so it cannot be turned on later.

## Registry

Entries are immutable deployments only. Metadata includes the address, the claimed commit, and a verification link. Removal is defined in the [charter](governance-charter.md): it is a signal, it is timelocked, and it does not stop the contract.
