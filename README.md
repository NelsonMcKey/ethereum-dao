# Ethereum DAO

Design notes for an ETH-holder DAO that keeps an onchain registry of immutable, ownerless DeFi deployments.

The registry does not extract a protocol fee. Fees that users pay each other — LP fees, interest — stay with those users. A protocol-level fee, if one is ever charged on a deployment this DAO controls, is burned. Listing an existing deployment is the default. A new deployment is a rare exception, because a new address has no liquidity and no history.

## Principles

- Ownerless deployments: no admin key and no upgrade proxy, including on dependencies such as oracles.
- Voting by deposited ETH, with the weight taken from a past checkpoint. The design is in [docs/voting-mechanism.md](docs/voting-mechanism.md). Raw wallet balances are not votes.
- Lindy belongs to a deployment, not to a source repository.
- OSI-approved licenses that allow deployment. GPL-3.0 qualifies.

## Documentation

- [Index](docs/index.md)
- Start here: [Vision](docs/vision-brief.md), [Voting](docs/voting-mechanism.md), [Selection framework](docs/primitive-selection-framework.md), [Open questions](docs/open-questions.md)
- Worked example: [Constant-product AMM dossier](docs/dossiers/amm-constant-product.md)

## Status

Design draft only. No contracts. Several decisions are still with the owner, listed in [docs/open-questions.md](docs/open-questions.md). The AMM dossier recommends neither listing Uniswap v2 nor redeploying it.

Documentation is [CC BY 4.0](LICENSE).
