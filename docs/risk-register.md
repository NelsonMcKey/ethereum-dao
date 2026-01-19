# Risk Register

## Purpose
Capture key risks and practical mitigations for the DAO’s model.

## Risks and Mitigations

### 1) Plutocratic ETH Governance
**Risk:** ETH-holder voting can be dominated by whales, recreating centralization.
**Mitigations:**
- Support delegation to enable broader coordination.
- Use quorum and time-locked votes to allow counter-mobilization.
- Consider quadratic or capped voting for select proposal types.

### 2) No Treasury, No Sustained Funding
**Risk:** Without a treasury, ongoing research and maintenance may stall.
**Mitigations:**
- Keep scope narrow and low-maintenance by design.
- Seek external, one-off grants or donations (not DAO-held).
- Encourage ecosystem sponsorships for research and verification.

### 3) Lindy Does Not Guarantee Safety
**Risk:** Long-lived code can still break under new conditions.
**Mitigations:**
- Define minimum lindy thresholds with objective metrics.
- Compare multiple independent implementations when possible.
- Maintain a deprecation path via registry removal.

### 4) Immutability Prevents Fixes
**Risk:** Critical bugs cannot be patched on immutable deployments.
**Mitigations:**
- Require clean migration paths and registry versioning.
- Use registry-level removal rather than contract-level control.
- Publish emergency redeploy playbooks.

### 5) Minimal Fees May Be Unsustainable
**Risk:** Lack of fees reduces incentives for long-term stewardship.
**Mitigations:**
- Prioritize primitives with near-zero operational cost.
- Allow minimal fees strictly for burn mechanics where needed.
- Favor primitives with strong existing maintainer ecosystems.

### 6) Burn Economics May Not Align Users
**Risk:** Users may not care about ETH burn vs direct utility.
**Mitigations:**
- Require demonstrated real-world usage and demand.
- Emphasize reliability and neutrality in UX and docs.
- Use adoption as a hard gate for deployment.

### 7) Dependency Risk (Oracles, Libraries)
**Risk:** External dependencies can reintroduce trust or upgrade risk.
**Mitigations:**
- Prefer primitives with minimal external dependencies.
- Require dependency maps and explicit trust assumptions.
- Limit eligibility for protocols depending on upgradeable components.

### 8) Governance Overhead and Apathy
**Risk:** Low participation and slow decisions reduce effectiveness.
**Mitigations:**
- Standardize proposal templates to reduce burden.
- Batch routine proposals to reduce vote fatigue.
- Tune quorum dynamically by proposal criticality.

### 9) Regulatory Uncertainty
**Risk:** Governance and deployment activities may attract scrutiny.
**Mitigations:**
- Avoid revenue distribution and token issuance.
- Maintain transparent, public governance records.
- Document non-custodial, non-profit intent and operation.

### 10) Attack Surface (Capture, Registry Poisoning)
**Risk:** Malicious proposals or social engineering can corrupt registry.
**Mitigations:**
- Enforce timelocks and public review windows.
- Allow registry changes only via onchain execution.
- Require strict evidence and metadata standards for proposals.
