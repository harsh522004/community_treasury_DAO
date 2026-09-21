# Community Treasury DAO — Technical Requirements

Status: Draft. This document records decisions made together; open items are not yet implementation requirements.

Product requirements: [DAO_REQ.md](DAO_REQ.md)

## Agreed decisions

### Governance foundation

- Use OpenZeppelin governance contracts as the foundation for proposals, voting, and the timelock.
- Voting is based on DAO membership, not a transferable governance token. Each eligible member has one vote.
- The voting source must retain historical membership so the Governor can read eligibility and total eligible membership at each proposal's voting snapshot.
- A proposal's voting eligibility and quorum denominator are fixed at its voting snapshot, when voting starts. A member added after that snapshot cannot vote on the proposal. A member removed after it remains eligible for that proposal. Membership changes affect later snapshots.
- With a 30% quorum, the required number of participating members is rounded up (for example, five eligible members require two participants). The exact quorum percentage remains to be confirmed.

### Membership administration

- An Admin initiates member additions and removals.
- Adding or removing a member is a sensitive action and requires approval from at least two of three multisig signers before the change takes effect on-chain.
- A single Admin cannot complete a membership change alone.
- The contract enforces these conditions; frontend controls are only an interface to them.

## Open decisions

- Membership voting source design: a checkpointed member registry compatible with Governor, or a restricted voting token. A checkpointed registry best matches the current no-token product scope, subject to implementation review.
- Multisig implementation and how approvals authorize exactly one Admin action.
- Which configuration and role changes are sensitive, and who can initiate them.
- Exact quorum, voting delay, voting period, timelock delay, and their clock units.
- Proposal action restrictions, treasury custody, execution roles, and cancellation policy.
- Chain and test network, development tools, frontend, indexing, automation, storage, and deployment architecture.
