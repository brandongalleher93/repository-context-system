# Decision Log

## DEC-001 — [Decision Title]
- **Date:** [YYYY-MM-DD]
- **Status:** APPROVED

### Decision
[What was decided.]

### Context
[Why a decision was necessary.]

### Alternatives Considered
1. **[Alternative A]** — [summary]
2. **[Alternative B]** — [summary]

### Rationale
[Why the chosen option won over the alternatives.]

### Trade-offs
[Costs/disadvantages knowingly accepted.]

### Consequences
[What follows from the decision.]

### Revisit When
[Conditions that justify reopening the decision.]

### Evidence
- [Research/reference if applicable.]

---

## DEC-EXAMPLE — Agent-maintained project state
- **Status:** APPROVED

### Decision
`PROJECT_STATE.md` is maintained automatically by the coding agent after authorized, validated work changes meaningful project state.

### Alternatives Considered
1. Agent-maintained state.
2. Human approval before every state-file update.

### Rationale
Human approval for routine state synchronization would recreate administrative work the system is intended to eliminate. State is descriptive rather than authorizing, and Git provides traceability and rollback.

### Trade-offs
An agent can record state incorrectly; this is mitigated by reconciliation against repository evidence and Git history.

### Consequences
State synchronization is part of Definition of Done. The state file may never be used to authorize scope, architecture, requirement, cost, branch, security, or other approval-controlled changes.

### Revisit When
State drift becomes frequent enough that automatic maintenance is less reliable than the administrative cost it saves.
