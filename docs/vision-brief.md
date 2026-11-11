# Vision brief

## Mission

An ETH-holder DAO that curates immutable, ownerless DeFi deployments. It charges no protocol-level fee. User-to-user payments, such as AMM fees to liquidity providers and interest to lenders, stay with those users. If a protocol-level fee is ever charged, it is burned.

The voting design is in [voting-mechanism.md](voting-mechanism.md). Unresolved choices are in [open-questions.md](open-questions.md).

## Problem

Many DeFi systems keep an admin key, an upgrade proxy, or a fee switch. That key is a governance surface and a way to collect rent. This project keeps a list of deployments that have neither, and it refuses to add a rent switch of its own.

## What the DAO does

- Decide which existing deployments belong on an onchain registry.
- Deploy a new copy only in the cases the [deployment program](deployment-program-spec.md) allows.
- Maintain the registry: add an entry, or remove one.

Removal does not stop a contract. It tells integrators the DAO no longer stands behind that address. After a deployment exists, that registry decision is most of the remaining governance surface, plus changes to governance parameters inside hardcoded floors.

## What it does not do

- Issue a token, hold a treasury, pay grants, or distribute fees.
- Upgrade, pause, or take funds from a listed contract.
- Set user-to-user fees to zero. An AMM with no fee to liquidity providers does not attract liquidity. Lending without interest does not attract lenders.
- Treat "ETH burned" as a goal. The fee policy implies that little or nothing is burned. A burn target would push the DAO to turn a fee on.

## Who it is for

- ETH holders who want a public list of neutral, immutable deployments.
- Integrators who need a stable address and a clear statement of what removal means.
- Contributors who bring evidence about a deployment.

## What would count as working

- Registry entries that still pass the [selection gates](primitive-selection-framework.md).
- Real usage of those deployments, measured by their own liquidity and volume, not by liquidity the DAO does not have.
- Proposals that reach the quorum defined for the voting vault.
- A reported break that is followed by a removal proposal. The timelock means this will be slow, and that slowness is part of the design.

## Assumptions

- Some deployments already exist that are immutable, ownerless, and useful. The registry's job is to name them, not to recreate them.
- A new address starts with no lindy. Lindy is liquidity, integrators, and history on that deployment.
- External groups, not this DAO, pay for any audits.
