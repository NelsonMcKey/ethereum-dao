# Primitive selection framework

How a deployment becomes eligible, and how eligible deployments are ordered. Policy context is in the [requirements](requirements-spec.md). A full application is the [constant-product AMM dossier](dossiers/amm-constant-product.md).

## Process

1. Nominate a deployment by address, with the source repository, commit, and license.
2. Apply the gates. A failure stops the proposal. Scores do not rescue it.
3. Score what passed.
4. Governance votes on a listing, or on a new deployment if the [deployment program](deployment-program-spec.md) allows one.

The candidate is a deployment. A repository with no address can be nominated only as a proposal to deploy, and it starts with no operational history.

## Gates

All three are pass/fail. They used to be small weights (immutability 10 percent, license 3 percent, fee viability 2 percent). A weighted score let a useful but upgradeable system outrank an ownerless one. That contradicted the point of the registry.

| Gate | Pass | Fail |
| --- | --- | --- |
| Ownerless and immutable | No admin key, no upgrade proxy, no role that can change fees, pause, or move funds. The same standard applies to contracts it depends on for safety. | A fee setter, an owner, a proxy admin, or an oracle whose admin sits outside the deployment. |
| License | OSI-approved, and the terms allow modification and deployment. GPL-3.0 passes. The listing cites the license and keeps source available when the license requires it. | Business Source, non-commercial, or any non-OSI grant. "Permissive only" is not the rule. |
| Protocol fee | No protocol-level extraction. User-to-user fees may exist. If this DAO deploys a fee, the recipient is a burn path with no setter. | A live fee switch, or a protocol fee paid to a treasury, a token, or any address that can be changed. |

Oracle-dependent primitives usually fail the first gate. A lending market or a collateralized stablecoin that reads an upgradeable price proxy is not ownerless, even if its own `owner()` is the zero address. Liquity v1 is the concrete case, documented in the [deployment program](deployment-program-spec.md).

## Scores

Each criterion is 1 to 5. Weights sum to 100. They are the previous non-gate weights (usefulness 25, lindy 25, security 20, composability 15, which summed to 85) rescaled and rounded.

| Criterion | Weight | What a high score requires |
| --- | --- | --- |
| Usefulness and adoption | 29 | Demand on this deployment: volume, liquidity, or a counted set of integrators. Empty pairs and unused forks do not count. |
| Deployment lindy | 29 | Age of this address, liquidity that stayed, and survival through drawdowns. The age of the source code does not transfer to a new address. |
| Security history | 24 | A public record: incidents, what was affected, and whether funds in this deployment were lost. Absence of a found incident report is not a proof that nothing happened. |
| Composability | 18 | Other systems already depend on this address or this interface, and the dependency does not require an admin. |

Weighted total = Σ (score × weight) / 100. The total orders eligible deployments. It does not create eligibility.

## Evidence

Prefer a primary source: the repository, the license file, a deployment transaction, an onchain read, or the project's own post. Mark anything not re-checked. The dossier shows the expected density of citations.
