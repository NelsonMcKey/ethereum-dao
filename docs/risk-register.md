# Risk register

Practical risks of the model in the [vision brief](vision-brief.md). Mitigations that need a number point at [open questions](open-questions.md).

### 1. A small vault is easy to capture

**Risk.** Quorum is a share of deposits. If few people deposit, one holder clears quorum.

**Mitigation.** Long timelock, public proposals, and a quorum fraction chosen with a nearly empty vault in mind. No quadratic weighting: that needs identity, and this project will not add one.

### 2. Most ETH cannot vote

**Risk.** Staked ETH and WETH are outside the vault. The electorate is execution-layer ETH that someone chose to deposit. Large holders of liquid ETH are over-represented relative to stakers.

**Mitigation.** Say so in the voting docs. Do not paper over it by counting LST tokens, which would trust the issuer.

### 3. Custodians vote customer funds

**Risk.** An exchange can deposit ETH it holds for customers.

**Mitigation.** Deposits are public. There is no technical separation. Accept the risk or abandon balance-weighted voting.

### 4. No treasury means no paid work

**Risk.** Research, reviews, and UI work have no budget.

**Mitigation.** Keep the scope to a registry and rare deployments. Audits and writeups are paid by whoever wants them, outside the DAO. The DAO does not receive or spend that money.

### 5. Lindy does not copy into a new address

**Risk.** A fork of old code is a new system with no liquidity and no track record. A bug that was harmless at one size can show up at another.

**Mitigation.** Score the deployment, not the repository. Prefer listing an existing address. Deploy new code only under the [deployment program](deployment-program-spec.md).

### 6. Immutable contracts stay broken

**Risk.** A bug cannot be patched.

**Mitigation.** Registry removal warns integrators after the timelock. It does not move funds or stop the contract. Users exit on their own if the contract lets them.

### 7. Zero protocol fees are mistaken for zero LP fees

**Risk.** A literal reading of "zero fee" would ship an AMM nobody provisions, or a lending market nobody funds.

**Mitigation.** The [fee policy](requirements-spec.md) leaves user-to-user payments in place and refuses protocol rent. Burned ETH is not a success metric, so there is no pressure to switch a fee on.

### 8. Oracle admins re-enter through the side door

**Risk.** A renounced core that reads an owned price proxy is still owned, one contract away.

**Mitigation.** The ownerless gate includes dependencies. Liquity v1 fails it, as written up in the deployment program.

### 9. Low participation

**Risk.** Votes do not reach quorum, or a motivated minority always does.

**Mitigation.** Narrow proposal surface, one template, and parameter floors so a single quiet vote cannot set the timelock to zero. Exact quorum is open.

### 10. Regulatory attention

**Risk.** Operating a registry and deploying contracts may draw scrutiny even without a token or revenue.

**Mitigation.** No token sale, no fee distribution, no custody of user funds by the DAO, and a public record of votes. This is not legal advice.
