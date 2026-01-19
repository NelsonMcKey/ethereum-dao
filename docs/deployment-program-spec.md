# Immutable Deployment Program Spec

## Purpose
Define how the DAO coordinates the selection, validation, and immutable deployment of proven, useful DeFi primitives with minimal or zero fees that burn ETH.

## Program Stages
1. **Candidate Intake**
   - Proposal references a specific OSS codebase and commit range.
   - Evidence includes adoption metrics, lindy history, and license.
2. **Lindy & Usefulness Review**
   - Verify time in production and real usage.
   - Confirm the primitive is broadly useful and actively used.
3. **Immutability Review**
   - Identify and remove admin keys, upgrade proxies, and hidden controls.
   - Ensure deployment config is fully immutable.
4. **Deployment Proposal**
   - Publish deployment parameters, bytecode artifacts, and verification steps.
   - Define fee policy (0 or minimal + burn).
5. **Onchain Approval**
   - Governance vote to approve deployment.
6. **Immutable Deployment**
   - Deploy using deterministic factories if possible.
   - Verify bytecode and published artifacts match.
7. **Registry Listing**
   - Add deployment to onchain registry with metadata and links.

## Required Artifacts
- Source repository and license.
- Evidence of adoption and lindy status.
- Build instructions and deterministic bytecode hash.
- Deployment parameters and fee/burn configuration.
- Verification checklist and registry metadata.

## Fee and Burn Policy
- Default to zero fees.
- If fees are required for sustainability, set to minimal and burn all proceeds.

## Verification and Integrity
- Open-source build pipeline and reproducible builds.
- Public bytecode verification.
- Clear versioning and commit references.

## Safety Criteria (Non-Audit)
- Prior usage in production with no admin intervention.
- Transparent history of incident response.
- Conservative dependency set (minimize external trust).

## Registry Requirements
- Immutable deployments only.
- Clear metadata including commit hash and deployment parameters.
- Removal only via governance and only for verifiable breakage.

## Open Questions
- Deterministic deployment requirements vs flexibility.
- Minimum adoption thresholds for acceptance.
