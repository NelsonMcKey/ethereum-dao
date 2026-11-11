# Dossier: constant-product AMM

Worked application of the [selection framework](../primitive-selection-framework.md) to one primitive and one deployment. The recommendation is not to list it and not to redeploy it.

## Recommendation

Do not list the Ethereum mainnet Uniswap v2 factory. Do not deploy a new factory in order to replace it.

The primitive can be deployed in an ownerless form: pair bytecode with a hardcoded fee to liquidity providers, and a factory whose fee setter is the zero address. Every pair from the mainnet factory reads that factory's `feeTo`, so those pairs do not pass the protocol-fee gate while the switch is on. A new factory with the setter fixed at zero would pass the gates and would start with no pairs. That is not a reason to deploy one. The fee is a policy mismatch, not a broken invariant, and a second factory would not change the pools that already hold the liquidity. See the [deployment program](../deployment-program-spec.md).

## Primitive

A pair holds two tokens. The product of the reserves does not fall, after a fee on the input. Anyone can add liquidity and receive a share. Anyone can trade against the pool. The fee paid by the trader stays in the pool for liquidity providers. That fee is a user-to-user payment under the [fee policy](../requirements-spec.md). It is not protocol rent.

No oracle is required for the swap. That is why this primitive is in scope when lending and collateralized stablecoins usually are not.

## Deployment under review

| Fact | Value |
| --- | --- |
| Contract | Uniswap v2 factory `0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f` |
| Created | Block 10,000,835, 2020-05-04 16:34:02 UTC, by `0x9C33eaCc2F50E39940D3AfaF2c7B8246B681A374` |
| Creation tx | `0xc31d7e7e85cab1d38ce1b8ac17e821ccd47dbde00f9d57f2bd8613bff9428396` |
| Public launch post | Uniswap Labs, 2020-05-18, "Uniswap v2 Mainnet Launch" |
| Source cited | `Uniswap/v2-core` tag `v1.0.1`, commit `4dd59067c76dea4a0e8e4bfdda41877a6b16dedc`, 2020-05-18 |
| License | GPL-3.0, from the repository license file |
| Pairs created | 527,597 at block 26,389,703. This counts every pair the factory ever created, including empty and junk pairs. It is not a count of liquid markets. |
| Bytecode match to `v1.0.1` | Not re-checked |

Uniswap's launch post says the protocol had been deployed and that an audit and formal verification had been released. Current Uniswap v2 audit documentation says a six-engineer review ran from 8 January to 30 April 2020, and that the original report URL is no longer available. This dossier does not rely on a third-party copy of that report.

## Gates

Checked at block 26,389,703 (2026-11-11 05:51:11 UTC) unless noted.

### Ownerless and immutable — fail

The pair source at `v1.0.1` has no owner and no proxy. `createPair` uses `CREATE2` of the pair bytecode. That part of the design can pass.

The factory cannot. `feeToSetter()` is `0x1a9C8182C09F50C8318d769245beA52c32BE35BC`. In `UniswapV2Factory` at tag `v1.0.1`, that address may call `setFeeTo` and `setFeeToSetter`. The setter is a contract. At the same block it answers `delay()` with 172800 (2 days), `MINIMUM_DELAY()` with 2 days, `MAXIMUM_DELAY()` with 30 days, and `GRACE_PERIOD()` with 14 days. Its `admin()` is `0x408ED6354d4973f66138C91495F2f2FCbd8724C3`. That admin answers `timelock()` with the setter's address, `uni()` with `0x1f9840a85d5aF5bf1D1762F925BDADdC4201F984`, and that token's `symbol()` is `UNI`. `votingPeriod()` is 40320 blocks, `votingDelay()` is 13140 blocks, `proposalThreshold()` is 1,000,000 UNI, and `quorumVotes()` is 40,000,000 UNI.

So the live factory has a privileged role, and the role sits behind UNI governance, not behind an ETH-holder vote and not behind a burned setter. Pair bytecode being immutable does not remove that role: pairs read `factory.feeTo()` when they mint the protocol fee.

### License — pass

GitHub classifies the repository license as GPL-3.0. GPL-3.0 is an OSI-approved license and permits modification and deployment. Derivatives stay under GPL-3.0, and the corresponding source has to be offered. That is compatible with this project's license gate. A permissive-only rule would have failed this deployment for no security reason.

### Protocol fee — fail

`feeTo()` is `0xf38521f130fcCF29dB1961597bc5d2B60F995f85`, which is not the zero address, and that address has code. In the whitepaper and in `_mintFee` (tag `v1.0.1`), a non-zero `feeTo` turns on a protocol fee equal to one sixth of the LP fee, minted as LP shares to `feeTo`. Traders still pay 0.30 percent. Liquidity providers keep five sixths of that fee instead of all of it.

The 0.30 percent itself is the LP fee. The pair enforces it by charging 3/1000 of the input inside the constant-product check (`UniswapV2Pair.swap` at tag `v1.0.1`). This dossier does not propose setting that to zero.

Where the protocol-fee shares go after they reach `feeTo` was not traced. They are not burned by this registry, and this DAO cannot redirect them.

## Scores

Scored anyway, so the weights are visible. The failed gates are decisive. The total does not make the factory eligible.

| Criterion | Score | Weight | Notes |
| --- | --- | --- | --- |
| Usefulness and adoption | 4 | 29 | The factory has been in continuous use since 2020 and has created 527,597 pairs. Volume and TVL were not measured. The pair count includes junk. |
| Deployment lindy | 5 | 29 | Same factory address since 2020-05-04, through later market cycles. This score does not transfer to a new address. |
| Security history | 4 | 24 | Long production life and a documented 2020 review whose original report is no longer hosted. This review did not find a primary-source incident of a mainnet pair-reserve drain caused by a bug in the invariant, and that search is not a proof of a clean record. The live fee role is a privileged economic control, not a backdoor that was ruled out by reading storage. |
| Composability | 4 | 18 | The pair interface is widely copied and integrated. An integrator census was not done. |

Weighted total = (4×29 + 5×29 + 4×24 + 4×18) / 100 = 4.29 out of 5.

A new factory with `feeToSetter` fixed at the zero address would pass all three gates and would score usefulness 1 and lindy 1 on the day it is created. That is the wrong candidate to deploy.

## When a new constant-product deployment would be justified

Not on these facts. A factory that can never charge a protocol fee is buildable, and none of the 527,597 existing pairs would move to it. Those pairs would stay on a factory this registry refuses to endorse. The result would be two venues, one liquid and unlisted, one empty and listed. That is a worse outcome than an honest non-listing. A later dossier can revisit this if the live fee setter is renounced and `feeTo` is cleared, or if the pair invariant itself is shown to be broken.

## Sources

Onchain reads are `eth_call`, `eth_getTransactionByHash`, `eth_getTransactionReceipt`, `eth_getBlockByNumber`, and `eth_getCode` against Ethereum mainnet. Live factory, fee, and pair-count figures are at block 26,389,703.

- Factory creation: tx `0xc31d7e7e85cab1d38ce1b8ac17e821ccd47dbde00f9d57f2bd8613bff9428396`, block 10,000,835, timestamp 1588610042 (2020-05-04 16:34:02 UTC), contract `0x5C69bEe701ef814a2B6a3EDD4B1652CB9cc5aA6f`.
- `feeTo()`, `feeToSetter()`, `allPairsLength()` at block 26,389,703.
- Timelock view calls on the fee setter: `delay`, `MINIMUM_DELAY`, `MAXIMUM_DELAY`, `GRACE_PERIOD`, `admin`. Governor view calls on that admin: `timelock`, `uni`, `votingPeriod`, `votingDelay`, `proposalThreshold`, `quorumVotes`. Token `symbol` on the `uni()` address.
- Source: <https://github.com/Uniswap/v2-core> tag `v1.0.1`. License file classified GPL-3.0. `UniswapV2Factory.sol` functions `setFeeTo` and `setFeeToSetter`. `UniswapV2Pair.sol` `_mintFee` and `swap`.
- Whitepaper: Hayden Adams, Noah Zinsmeister, Dan Robinson, March 2020, section 2.4 (protocol fee). <https://app.uniswap.org/whitepaper.pdf>
- Launch post: <https://blog.uniswap.org/launch-uniswap-v2> (18 May 2020).
- Uniswap's statement that a review ran from 8 January to 30 April 2020 and that the original report URL is gone: <https://developers.uniswap.org/docs/protocols/v2/audits>, retrieved 2026-11-11.
- OSI listing for GPL-3.0: <https://opensource.org/license/gpl-3-0>

## Not established

- Bytecode of the live factory equals tag `v1.0.1`. The function calls succeed and match that source's ABI. That is not a full bytecode diff.
- No reserve-draining bug has ever affected a pair from this factory. Not established. A search did not surface a primary-source case.
- Current TVL, volume, or the number of pairs with meaningful liquidity. Not measured.
- The path of value after it reaches `feeTo`. Not traced.
- Whether the 2020 review's detailed findings match any particular mirror of the report. Not used.
