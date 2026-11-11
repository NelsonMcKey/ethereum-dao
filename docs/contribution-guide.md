# Contribution guide

How to nominate a deployment and how to disagree with one. Voting rules are in the [charter](governance-charter.md). The evidence bar is the [selection framework](primitive-selection-framework.md).

## Who can contribute

Anyone can submit research and dossiers. Submitting an onchain proposal requires the vault minimum, once that minimum exists.

## What to submit

- A nomination of an existing address, or a request to deploy, with the reason a new address is justified.
- A correction of a cited fact, with the source.
- A gate review: owner, proxy, fee setter, dependencies, license.

## Nomination contents

- Primitive and what users pay each other, as distinct from any protocol fee.
- Address, chain, and creation transaction.
- Repository, tag or commit, and license name with a link to the license file.
- Gate results, each with the read or the file that supports it.
- Scores with the figures behind them. Say what was not measured.
- Known incidents, or an explicit statement that a search found none, which is not the same as a clean history.
- For a new deployment: init parameters and the statement that liquidity starts at zero.

The [constant-product AMM dossier](dossiers/amm-constant-product.md) is the worked example, including a recommendation not to list.

## Evidence

Use primary sources: repository, license file, deployment transaction, onchain call, project post. Name the block number for onchain reads. Mark anything you did not re-check. Do not import a TVL or a turnout figure you cannot reproduce.

## Conduct

State the claim and the source. Disclose if you are paid by the system under review. Do not describe a registry removal as a way to stop a contract.
