# Architecture

Components and the boundary between canonical state and everything else. Behavior of voting is in the [voting mechanism](voting-mechanism.md). Removal is in the [charter](governance-charter.md).

## Onchain

- **Voting vault.** Holds ETH. Checkpoints deposits. Non-transferable receipt. Withdrawal delay. No admin.
- **Governor.** Creates proposals, reads vault checkpoints at a snapshot block, enforces quorum and threshold, queues execution behind a timelock.
- **Registry.** The list of endorsed addresses and the metadata hash for each. `add` and `remove` are the normal governor payloads. `remove` does not call the listed contract.
- **Optional factory.** Used only when a new deployment is justified. It does not wrap, upgrade, or custody an existing system. A listing does not have to come out of this factory.
- **Burn path.** Present only if a deployment this DAO controls charges a protocol-level fee. It has no setter. It is unused when the fee is zero, which is the default.

## Offchain

- Docs and evidence, including dossiers.
- A UI for proposing, voting, and reading the registry. The UI is not canonical. A missing UI does not stop an onchain vote.
- Reproducible build scripts for anything this DAO deploys.

An offchain temperature check may use Snapshot-style signatures. Those signatures are not an input to the governor.

## Flow

Nominate with evidence → gate review → onchain proposal → vault vote at the snapshot checkpoint → timelock → `add` or `remove`, or a factory deploy followed by `add`.

## Trust boundary

Listed primitives and the vault have no admin. The governor is the only writer of the registry, and only after a timelock. Offchain text can be wrong. The registry entry is the endorsement, and the contract's own code is the behavior.

## Invariants

- A listed primitive is immutable and ownerless, including the dependencies the gates cover.
- User-to-user fees are not redirected.
- A protocol-level fee under this DAO's control is either absent or burned.
- Vault ETH returns only to the depositor.
- A registry removal changes the list and nothing else.
