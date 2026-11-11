# Requirements

Functional and non-functional requirements. The mission is in the [vision brief](vision-brief.md).

## Functional

- ETH-holder voting as specified in the [voting mechanism](voting-mechanism.md). v1 reads checkpointed vault balances. It does not read raw `address.balance`.
- Proposal lifecycle: submit, vote, timelock, execute. Execution is an onchain call. There is no admin override.
- An onchain registry of approved deployments. Adding and removing entries are the ordinary execution payloads.
- A deployment path for the rare case where a new immutable copy is justified. The registry can also point at a contract this DAO did not deploy.
- Fee policy, stated once here:
  - No protocol-level fee is the default.
  - LP fees, interest, and other user-to-user payments are part of the primitive. This DAO does not set them to zero and does not divert them.
  - If a protocol-level fee exists on a deployment this DAO controls, it is burned, and the burn address cannot be changed.
- Public records for proposals, votes, and registry changes.

## Non-functional

- Listed contracts have no upgrade proxy and no admin key.
- Security evidence is the deployment's own history, public review, and reproducible bytecode. An audit is not a requirement. This DAO cannot pay for one.
- Registry writes are onchain.
- Interfaces are standard enough for integrators to use without this DAO in the transaction path.
- Builds that this DAO deploys are reproducible. Listings of someone else's deployment cite the source commit they claim to match, and say so when the match was not re-checked.

## Constraints

- No token, no treasury, no custodial funds, no fee distribution.
- The voting vault may hold ETH that only the depositor can withdraw. Governance is not a custodian of that ETH. See the voting mechanism.
- Governance is limited to ETH deposited in the vault.
- Licenses of listed or deployed code are OSI-approved and allow modification and deployment. Copyleft is allowed. GPL-3.0 qualifies, which is why Uniswap v2 core and Liquity v1 are not excluded. Business Source, non-commercial, and other non-OSI terms do not qualify. A copyleft deployment must ship its corresponding source under that license.
- Voting weight, quorum base, and the rejection of quadratic voting are specified in the voting mechanism. Parameter numbers are an [open question](open-questions.md).

## Governance constraints

- Every execution waits out the timelock, including removals that people will want to call emergencies.
- There is no pause key, no guardian, and no fast path.
- Parameter changes cannot cross the floors once those floors are chosen. The floors are open.

## Deployment constraints

- The thing being judged is a deployment at an address, not a repository in the abstract.
- Configuration is fixed at deploy time: no owner, no upgrade role, protocol fee off or burned with no setter.
- External dependencies are in scope. An upgradeable oracle, a multisig price proxy, or an admin on a dependency fails the ownerless gate even when this contract's own owner is the zero address.

## Assumptions

- Useful ownerless deployments exist, and many popular systems will fail the gates because of an admin or an oracle.
- ETH-holder voting, narrowed to the vault, is the legitimacy model. It will not represent staked ETH.
