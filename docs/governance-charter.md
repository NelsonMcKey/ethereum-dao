# Governance charter

Rules for how deposited ETH governs the registry. Voting mechanics are in the [voting mechanism](voting-mechanism.md). Parameter numbers are an [open question](open-questions.md).

## Scope

Before anything is listed, governance chooses which deployments to add.

After a primitive is deployed or listed, governance can:

- Add a registry entry.
- Remove a registry entry.
- Change quorum, threshold, voting period, timelock, and the proposal minimum, inside the hardcoded floors.

Governance cannot upgrade a listed contract, pause it, change its fees, seize deposits, or move ETH out of the voting vault. There is no treasury, so there is no grants proposal and no budget proposal.

## Who votes

Any address that has deposited ETH in the vault can vote, or can delegate the vote. Weight is the checkpointed deposit at the proposal's snapshot block, in proportion. Delegation does not transfer the ETH.

## Proposal lifecycle

1. Discussion offchain, using the [contribution template](contribution-guide.md). An offchain poll may inform the draft. It does not execute.
2. Onchain submission by an address with at least the proposal minimum deposited.
3. A fixed voting window.
4. A timelock on every successful proposal.
5. Execution of the calls in the proposal. If the timelock expires unexecuted, the proposal does not run.

## What removal means

`remove` deletes the registry's endorsement of an address and records a reason. The contract is unchanged. It keeps custody of user funds, keeps its code, and keeps serving callers. Integrators who treat the registry as a deny-list or an allow-list can stop routing to it. Integrators who hardcoded the address are unaffected. Users already inside the contract are unaffected. Removal cannot unwind a bug, a bad debt, or an exploit in progress.

A removal still waits for the timelock. During an active exploit the DAO cannot pause the contract, and the removal will land after the damage if the damage is fast. That limit is accepted. Publishing the removal early, while the timelock runs, is the whole emergency tool.

## Pass rules

- Quorum is a fraction of vault ETH at the snapshot, not of all ETH.
- The approval threshold is a fraction of yes votes among yes and no.
- Abstentions do not raise the yes share. They do count toward quorum if they are cast. The exact fractions are open.

## Invariants

- No admin key on listed primitives or on the vault.
- The vault's only withdrawal path is the depositor, after the delay.
- Registry changes happen only by executing a successful, timelocked proposal.
- No proposal type moves value to a person.
