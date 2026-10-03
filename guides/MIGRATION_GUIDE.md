# RCS Migration Guide

## Goal
Migrate an existing repository to RCS without destroying useful documentation, fabricating missing facts, or creating duplicate sources of truth.

## Procedure
### 1. Audit Before Editing
Determine from repository evidence:
- project purpose and boundaries;
- existing documentation and authority;
- current milestone/state;
- recent meaningful work;
- active requirements/decisions/risks;
- canonical validation;
- safety/approval boundaries;
- obvious stale or conflicting documents.

Do not rely on prior chat history when testing repository self-sufficiency.

### 2. Classify Existing Artifacts
For each document classify it as:
- retain as authoritative;
- move/rename without semantic change;
- merge into a canonical RCS artifact;
- retain as research/history;
- superseded/archive candidate;
- ambiguous — requires human decision.

### 3. Avoid Template-Driven Bureaucracy
Create only artifacts with distinct information to hold. A small repository may need only `AGENTS.md`, `PROJECT_STATE.md`, `README.md`, and one or two context documents.

### 4. Create Layer 1
Create project `AGENTS.md` as the router and `PROJECT_STATE.md` as the current-state pointer. Derive both from repository evidence. Do not invent unknown state.

### 5. Normalize Layer 2 Selectively
Where useful, establish Charter, Requirements, Architecture, Roadmap, Decision Log, Risk Register, and `docs/research/`. Preserve existing strong documents and link to them rather than duplicating them.

### 6. Encode Routing
Add task-specific positive and negative routing. Point to canonical validation and project-specific approval boundaries.

### 7. Reconcile
Check that state, roadmap, requirements, architecture, decisions, README, code, and tests do not make unexplained contradictory claims. Surface unresolved conflicts.

### 8. Validate
Run canonical repository validation if migration changed executable/configuration content. Documentation-only migration still requires link/path/reference review and Git diff review.

### 9. Cold-Start Test
Start a fresh coding-agent session and provide only: `Continue this project.`

Pass only if the agent can orient correctly and efficiently without hidden conversational context.

## Migration Rules
- Never fabricate historical decisions or rationale. Mark unknowns or ask the human.
- Do not rewrite working source merely to match RCS structure.
- Do not move files solely for aesthetic consistency if routing can solve discoverability.
- Preserve Git history where practical.
- Project-specific rules may be stricter than RCS/global rules, never weaker.
