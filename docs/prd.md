# PRD

What an implementer is building. Goals and non-goals match the [vision brief](vision-brief.md) and the [requirements](requirements-spec.md).

## Goals

- A registry of immutable, ownerless deployments that integrators can read onchain.
- A voting vault and governor that let deposited ETH add or remove entries, after a timelock.
- A fee policy that leaves LP fees and interest alone and takes no protocol fee.

## Non-goals

- A token, a treasury, a grants program, or a fee switch that pays anyone.
- Admin keys, pauses, or upgrades on listed primitives.
- Binding offchain votes.
- Representing staked ETH or WETH in v1.

## Users

- ETH holders who deposit and vote.
- Integrators reading the registry.
- Contributors assembling evidence.

## Flows

1. **Nominate.** An evidence package names an address, a commit, a license, and gate results. The [AMM dossier](dossiers/amm-constant-product.md) is the pattern.
2. **Screen.** Gates, then scores. A failed gate is the end of that proposal.
3. **Vote.** Vault holders vote on the snapshot checkpoint. An offchain poll may precede this and does not count.
4. **Execute.** After the timelock, the registry adds or removes the address. A new deployment, when justified, is deployed and then added.
5. **Use.** Integrators read the registry. They still verify bytecode. Removal is a signal, not a kill switch.

## Requirements

Covered in the requirements spec, the voting mechanism, and the technical spec. This PRD does not restate interfaces.

## Metrics

- Entries that still pass the gates.
- Usage of listed deployments.
- Proposals that meet quorum.
- Time from a public incident report to a removal transaction, which includes the timelock on purpose.

ETH burned is not a metric.

## Risks

Capture of a small vault, low turnout, immutable bugs, and oracle dependencies. Detail is in the [risk register](risk-register.md) and the [threat model](security-threat-model.md).
