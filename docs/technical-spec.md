# Technical Spec

## Overview
This document defines the technical interfaces and data flows for an ETH-holder-governed DAO that curates and deploys immutable, ownerless DeFi primitives with minimal or zero fees that burn ETH.

## Core Contracts

### Governance
**Purpose:** manage proposal lifecycle, voting, and execution.

**Key capabilities:**
- Create proposals referencing offchain evidence and onchain actions.
- Snapshot or checkpoint ETH balances for voting power.
- Enforce quorum, thresholds, and timelocks.

**State (Draft):**
- `Pending` → `Active` → `Queued` → `Executed` or `Defeated`

**Interfaces (Draft):**
- `propose(metadataURI, actions)`
- `vote(proposalId, support)`
- `execute(proposalId)`

**Events (Draft):**
- `ProposalCreated(proposalId, proposer, metadataURI)`
- `VoteCast(proposalId, voter, support, weight)`
- `ProposalQueued(proposalId, eta)`
- `ProposalExecuted(proposalId)`

### Primitive Registry
**Purpose:** canonical list of approved immutable deployments.

**Key fields:**
- `deploymentAddress`
- `commitHash`
- `metadataURI`
- `createdAt`

**Interfaces (Draft):**
- `addDeployment(address, commitHash, metadataURI)`
- `removeDeployment(address, reason)`
- `getDeployment(address)`

**Events (Draft):**
- `DeploymentAdded(deploymentAddress, commitHash)`
- `DeploymentRemoved(deploymentAddress, reason)`

### Deployment Factory
**Purpose:** create deterministic, immutable deployments where feasible.

**Key capabilities:**
- Enforce immutable configuration at deploy.
- Emit deployment metadata.
- Optional CREATE2 deterministic address support.

**Interfaces (Draft):**
- `deploy(bytes deploymentParams) returns (address)`
- `predictAddress(bytes deploymentParams) returns (address)` (optional)

**Events (Draft):**
- `Deployed(deploymentAddress, paramsHash)`

### Fee Burn Adapter
**Purpose:** route any protocol fees to ETH burn.

**Key capabilities:**
- Accept ETH fees and send to a burn sink.
- Surface burn metrics.

**Interfaces (Draft):**
- `burn()`
- `burnedTotal()`

**Events (Draft):**
- `Burned(amount)`

## Data Flow
- Nomination → Governance proposal with `metadataURI`.
- Vote → Timelock → Execution.
- Execution adds registry entry and triggers deployment (if factory-based).

## Data Structures (Draft)
- `Proposal`: metadataURI, actions[], startBlock, endBlock, quorum, threshold, state.
- `DeploymentMetadata`: commitHash, metadataURI, createdAt.

## Minimal State Diagram (Governance)
```
Pending -> Active -> Queued -> Executed
                 \-> Defeated
```

## Offchain Components
- Evidence repository (metadataURIs).
- Reproducible build scripts and bytecode verification tooling.
- Governance UI and registry explorer.

## Invariants
- No admin keys or upgrades in deployed primitives.
- Registry updates only via governance execution.
- Fees, if any, are burned.

## Open Questions
- ETH voting implementation details (snapshot vs checkpoint).
- Factory feasibility for complex primitives.
