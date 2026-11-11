# Voting mechanism

## Recommendation

ETH holders vote by depositing native ETH into an immutable vault and voting with the checkpointed balance from a past block. The vault has no admin and no fee. Only the depositor can withdraw. The deposit receipt cannot be transferred. Governance cannot spend, freeze, or redirect deposits.

This is the design the other docs assume. It is a proposal for the owner to accept or reject. The fallback, if any contract holding ETH is unacceptable, is the state-root log in the second option below. Numeric parameters are listed in [open questions](open-questions.md).

Quorum is a fraction of ETH in the vault at the snapshot block. The pass threshold is a fraction of yes votes among yes and no. Neither one uses all ETH in existence as its denominator.

## Why a contract cannot read "ETH held at some block"

The EVM exposes an account's current ETH balance. It does not expose that balance at an earlier block. A vote that calls `address.balance` during the voting transaction counts ETH that exists only inside that transaction. A flash loan is that pattern: borrow, vote, repay, and the balance at the end of the block is unchanged.

A balance observed at an earlier block boundary is immune to a same-transaction flash loan. It is not immune to ETH borrowed before that block and repaid after it. If the snapshot block is predictable and only minutes or hours away, the cost of that borrow is small.

Native ETH also has no transfer hook, so a token-style checkpoint (the ERC-20 votes pattern) cannot be written unless the ETH moves through a contract that sees the deposit and the withdrawal.

Three further facts constrain any balance-weighted design. Readings below are from Ethereum mainnet block 26,389,703 (2026-11-11 05:51:11 UTC). Sources are at the end.

- Staked ETH does not sit in the staker's account. The beacon deposit contract held 93,287,936 ETH. A staker's validator balance is not `address.balance`, and an LST is a separate token.
- The canonical WETH contract held 2,094,024 ETH. That balance belongs to the WETH contract. WETH holders are a different set of accounts. Counting both the contract and the holders double-counts. The WETH contract has no key with which to vote.
- Custodial exchanges hold customer ETH in their own addresses. Any scheme that weighs raw balances will weigh the custodian.

Linear weighting needs no sybil resistance. Splitting a balance across many addresses does not increase its weight. Sybil resistance matters for quadratic voting, which needs an identity system this project does not have. Quadratic voting is rejected. The phrase "anti-sybil" is not an open problem for this design.

## Option A — voting escrow (recommended)

Holders deposit native ETH. The vault writes a checkpoint on deposit, withdrawal, and delegation. A proposal fixes the snapshot at the block in which it is created. Votes cast later use the checkpoint from that block, so a flash loan in the voting transaction has nothing to add.

The receipt is non-transferable. A transferable receipt would be a new governance token, which this project does not issue. Delegation assigns the vote and leaves the ETH with the depositor.

Withdrawal is two steps. The depositor starts a withdrawal and finishes it after a delay. Voting power lasts until the withdrawal finishes. The delay is at least as long as the voting period plus the execution timelock, so ETH cannot enter, decide a proposal, and leave inside one cycle. Someone who keeps borrowed ETH in the vault for longer than that delay can still vote. The delay sets the interest cost of that attack. It does not make the attack impossible.

The vault is user escrow enforced by code. It is not a treasury. The charter's ban on custody means the DAO holds no funds and no operator can move deposits. It does not mean that no contract ever holds ETH for its depositor. That reading is a real change from "the ETH already in your wallet votes," and it is the point the owner has to accept. Under this design, an ETH holder who does not deposit does not vote.

What v1 does not count:

- Beacon-chain balances and LST tokens. Counting an LST trusts the issuer. The deposit-contract ETH is not counted either, so there is no double count. Staked ETH has no vote.
- WETH. Holders unwrap, then deposit. The WETH contract's own ETH is not a voter.
- Exchange inventories, except where the exchange itself deposits. Nothing in the contract can tell customer funds from proprietary funds. Deposits and delegations are public, which makes a large custodian visible. It does not stop one.

Quorum is reachable only because the denominator is vault deposits. A percentage of all ETH is not reachable. Carbonvote, below, is the precedent. The cost of a small vault is that a small depositor set can meet quorum. The quorum fraction, the proposal minimum, and the delay lengths are open numbers. The rule that is fixed here is the denominator, and the rule that governance cannot set the timelock or the quorum to zero. The floors themselves are an open decision.

Binding execution stays onchain: after the vote, a timelock, then the registry or a parameter change. The vault's ETH is not an executable balance.

## Option B — historical state proofs

EIP-2935, live on mainnet since the Pectra upgrade on 2025-05-07 10:05:11 UTC (epoch 364032), stores 8191 historical block hashes in a system contract. A contract can check a block header against one of those hashes, store the header's state root, and later check a Merkle proof of an account's balance against that root. Voters do not deposit. Nobody holds their ETH.

The hash window is 8191 blocks, about 27.3 hours at a 12-second slot. A proof against a block inside that window stops same-transaction flash loans. It does not stop a borrow that exists only for the snapshot block. Once a proposal is public, the snapshot of a recent block is something an attacker can still arrange, repay, and then prove.

A lookback of days or weeks needs something else to have stored the state root while the hash was still available. That is a permissionless log the governance contract would have to keep, written every day or so, for as long as governance runs. A gap in the log is a gap in history. Each vote then carries an account proof and costs more gas. Wallet support for building those proofs is thin.

This option has the same blind spots as a raw balance: exchange addresses count, staked ETH does not, and the WETH contract is not the WETH holders. Quorum still cannot be a percentage of ETH supply, and there is no natural smaller denominator.

Use this option only if the owner rejects Option A. It is a workable fallback with a standing liveness duty and a weak defense against borrowed ETH. It is not the recommendation.

## Option C — offchain votes

A Snapshot-style vote can read historical balances from an archive node, and a strategy can include or exclude WETH or LSTs. Signatures are cheap, and turnout tooling already exists.

The result does not write the registry. Putting it onchain requires an oracle and a dispute window (the SafeSnap / optimistic-oracle pattern). That oracle becomes a path into the only state this DAO is allowed to change. Option C is allowed as a temperature check during discussion. It has no binding effect and cannot add or remove a registry entry.

## Carbonvote

In July 2016, carbonvote.com polled ETH holders on the DAO hard fork. A holder signaled with a transaction. The poll counted the ETH balance of the signaling address. ETH was not locked.

While the poll was open, contemporaneous writeups put participation near 4 to 4.5 percent of ether, with the yes share in the mid-80s. One post on 2016-07-11 reported 4.5 percent of free ether and an 85/15 split. A note on 2016-07-13 reported about 4 percent, 3.2 million ETH, and an 83/17 split. This draft did not recover a final tally from carbonvote.com. The useful lesson is the shape of the result: unlocked balance-weighted signaling, on a question people were already arguing about, drew a small share of ETH. A quorum defined on all ETH will fail. A design that assumes broad turnout will also fail.

## Sources

Onchain reads use `eth_call`, `eth_getBalance`, and `eth_getCode` at block 26,389,703.

- Beacon deposit contract `0x00000000219ab540356cBB839Cbe05303d7705Fa`: 93,287,936.01363336 ETH, code present.
- WETH `0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2`: 2,094,024.2289885967 ETH, code present.
- EIP-2935: `HISTORY_SERVE_WINDOW` of 8191. <https://eips.ethereum.org/EIPS/eip-2935>
- Pectra mainnet activation: 2025-05-07 10:05:11 UTC, epoch 364032. <https://blog.ethereum.org/2025/04/23/pectra-mainnet> and <https://ethereum.org/roadmap/pectra/>
- Carbonvote commentary: <https://www.reddit.com/r/ethereum/comments/4sakeu/> (2016-07-11) and <http://franto4.blogspot.com/2016/07/ethereum-vote-update.html> (2016-07-13). Final official totals were not re-fetched.
