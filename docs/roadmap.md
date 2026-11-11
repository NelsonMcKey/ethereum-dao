# Roadmap

The sequence from this draft to a first registry entry. No dates. Contract work is out of scope for this repository.

## 1. Design draft (this repository)

Written: vision, requirements, voting recommendation, charter, selection gates, deployment rules, threat model, and one worked dossier.

Waiting: the owner decisions in [open questions](open-questions.md), in particular whether the voting vault is accepted and what the numeric parameters are.

## 2. Evidence

Run another dossier only after the owner names a primitive. Do not treat the constant-product AMM dossier as a listing. It is a worked refusal.

## 3. Spec freeze

Lock the vault, governor, and registry interfaces in the [technical spec](technical-spec.md) once the open numbers exist. Until then those interfaces stay drafts.

## 4. Implementation (not this repo)

Contracts, tests, and a reproducible build. A UI can follow. The UI is not required for the vote to be valid.

## 5. First registry action

A proposal, a vault vote, a timelock, and either an `add` of an existing address or a new deployment that the deployment program allows. Both outcomes are allowed to be "no."

## Gates before that action

- The owner has accepted a voting design.
- Quorum, threshold, periods, and floors are numbers, not placeholders.
- The candidate passes the selection gates on cited evidence.
- For a new deployment, the proposal states that lindy starts at zero.
