# Documentation guide

How these docs are organized. The mission is stated in the [vision brief](vision-brief.md) and is not repeated as a preface in every file.

## Rules

- Each doc opens with the job of that doc, in a sentence or two, then links outward.
- Open decisions live only in [open-questions.md](open-questions.md).
- The fee policy is specified in the [requirements](requirements-spec.md). Other docs link to it.
- Voting is specified in the [voting mechanism](voting-mechanism.md).
- Claims about deployments cite a source. Unverified points are labeled.

## Set

| Doc | Job |
| --- | --- |
| [Vision brief](vision-brief.md) | Mission, non-goals, success signals. |
| [Requirements](requirements-spec.md) | Requirements, fee policy, license rule. |
| [Voting mechanism](voting-mechanism.md) | How ETH votes, and the options that were rejected. |
| [Governance charter](governance-charter.md) | What votes can do, including removal. |
| [Selection framework](primitive-selection-framework.md) | Gates and weights. |
| [Deployment program](deployment-program-spec.md) | When to list, when to deploy, oracle limit. |
| [Dossier](dossiers/amm-constant-product.md) | The framework applied to one primitive. |
| [Architecture](architecture-blueprint.md) | Components and invariants. |
| [Technical spec](technical-spec.md) | Draft interfaces. |
| [PRD](prd.md) | Flows and metrics for an implementer. |
| [Threat model](security-threat-model.md) | Attacks and accepted limits. |
| [Risk register](risk-register.md) | Operational risks. |
| [Research brief](research-brief.md) | Prior art the draft uses. |
| [Roadmap](roadmap.md) | Sequence from this draft to a first registry action. |
| [Contribution guide](contribution-guide.md) | How to nominate. |
| [Open questions](open-questions.md) | Owner decisions still open. |

## UI

Wireframes and a governance UI are not part of this repository. When a UI exists, it should use the same words as the charter: registry, removal as a signal, vault deposit, timelock. Canonical state stays onchain if the UI is down.

## License

Documentation is CC BY 4.0. See the repository `LICENSE`. Code discussed in a dossier keeps the license of that code.
