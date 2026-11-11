# Technical spec

Draft interfaces. They become normative after the owner sets the numbers in [open questions](open-questions.md). This file describes shapes. It is not a contract.

## Voting vault

Holds native ETH. The internal receipt is non-transferable and is not a token listing.

Draft calls:

- `deposit()` payable. Credits the sender and writes a checkpoint.
- `startWithdraw(uint256 amount)` and `finishWithdraw()`. `finishWithdraw` succeeds only after the delay. Voting power includes the ETH until `finishWithdraw`. The delay is at least the voting period plus the timelock.
- `delegate(address to)`. Moves voting power. Does not move ETH.
- `getPastVotes(address account, uint256 blockNumber)`.

No admin, no fee, no transfer, no approval.

## Governor

Draft calls:

- `propose(address[] targets, bytes[] calldatas, string metadataURI)`. Snapshot block is the proposal block. The proposer needs the minimum vault balance at that block.
- `castVote(uint256 proposalId, uint8 support)`. Weight is `getPastVotes` at the snapshot. Support is yes, no, or abstain.
- `queue(uint256 proposalId)` and `execute(uint256 proposalId)`.

State: `Pending → Active → Defeated`, or `Pending → Active → Queued → Executed` or `Expired`.

Quorum uses vault ETH at the snapshot as the denominator. Parameter changes are themselves proposals, and they revert if they cross the floors.

## Registry

Draft fields: deployment address, metadata URI, listed-at block.

Draft calls, governor-only:

- `add(address deployment, string metadataURI)`
- `remove(address deployment, string reason)`

`remove` updates the registry and emits the reason. It does not call `deployment`. A removed address can be added again only by a new proposal. Metadata is evidence, not an instruction the contract interprets.

## Factory

Optional. `deploy(bytes params) returns (address)`. Params are fixed in the creation transaction: no owner, protocol-fee setter is the zero address. The factory does not retain a role on the created contract. Listings of contracts the factory did not create skip this component.

## Burn path

`burn()` sends this DAO's protocol-level ETH fee to a burn sink. There is no function that sets the sink. Deployments with a zero protocol fee do not wire this in. The path is not used to take LP fees or interest.

## Events

- Vault: `Deposited`, `WithdrawStarted`, `WithdrawFinished`, `DelegateChanged`.
- Governor: `ProposalCreated`, `VoteCast`, `ProposalQueued`, `ProposalExecuted`.
- Registry: `DeploymentAdded`, `DeploymentRemoved`. The removal event carries the reason string.

## Offchain

`metadataURI` points at the evidence package. The package can be wrong. The registry's endorsement is the onchain add. Consumers who need bytecode certainty re-check the code at the address.

## Invariants

- No admin on the vault, the factory's children, or listed primitives.
- Registry writes come from the governor after a timelock.
- `remove` has no effect on the target account's code or balance.
- User-to-user fees are not an input to these contracts.
