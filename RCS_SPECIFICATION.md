# Repository Context System (RCS) v1.0

## Purpose
RCS is a project-agnostic repository context architecture for solo and small-team software development. It lets a capable coding agent enter a repository cold, orient itself, load only relevant context, respect authority boundaries, implement bounded work, validate it, and synchronize repository knowledge without relying on prior chat history.

## Core Principles
1. The Git repository is the source of truth for durable project context.
2. Context is progressively disclosed: route first, load details only when relevant.
3. Correctness and traceability outrank token reduction.
4. Project state records reality; it does not create authority.
5. Documentation synchronization is part of Definition of Done.
6. Code/tests describe implemented reality; approved requirements and decisions describe intended authority. Disagreement is a discrepancy to resolve, not permission to silently redefine intent.
7. Do not create documentation merely because a template exists.

## Three Layers
### Layer 1 — Navigation
- `AGENTS.md`: project router, task routing, approval boundaries, completion protocol.
- `PROJECT_STATE.md`: concise current-state pointer (“you are here”).

### Layer 2 — Project Context
As needed: Charter, Requirements, Architecture, Roadmap, Decision Log, Risk Register, and research artifacts.

### Layer 3 — Work
Source code, tests, scripts, configuration, fixtures, generated outputs, and project-specific tooling.

## Recommended Structure
```text
repo/
├── AGENTS.md
├── PROJECT_STATE.md
├── README.md
├── docs/
│   ├── PROJECT_CHARTER.md
│   ├── REQUIREMENTS.md
│   ├── ARCHITECTURE.md
│   ├── ROADMAP.md
│   ├── DECISION_LOG.md
│   ├── RISK_REGISTER.md
│   └── research/
├── src/ (or project-specific source tree)
├── tests/
└── ...
```
Not every project needs every document.

## Authority and Conflict Handling
Mandatory platform, safety, and security constraints are hard boundaries. No human, global, session, or repository instruction may override them. Within those boundaries, use this precedence for intended project behavior:
1. Global agent governance.
2. Current explicit human project instruction.
3. Project `AGENTS.md`.
4. Approved requirements and decisions.
5. Approved architecture.
6. Project state and roadmap.
7. Research/evidence documents.
8. README/general documentation.

A current explicit instruction from a human authorized to make the decision may intentionally change prior project intent, requirements, scope, or decisions, subject to mandatory constraints and global governance. Reconcile affected repository documentation to the authorized change; do not leave contradictory requirements, decisions, architecture, roadmap, state, or routing in place.

Source code and tests are evidence of implemented reality. If implementation conflicts with higher-authority intent, stop treating the discrepancy as settled and surface it.

## Status Vocabulary
Use only when applicable: `PROPOSED`, `APPROVED`, `IMPLEMENTED`, `VALIDATING`, `COMPLETED`, `BLOCKED`, `REJECTED`, `SUPERSEDED`.

## Task Lifecycle
1. **Orient** — read project router and current state; inspect Git status.
2. **Classify** — identify the task type.
3. **Route** — load required context, conditional context, and avoid unrelated context.
4. **Check authority** — determine whether approval is required.
5. **Implement** — perform one bounded objective.
6. **Validate** — run the repository’s canonical applicable checks.
7. **Reconcile** — compare implementation, tests, requirements, architecture, decisions, roadmap, risks, and state.
8. **Synchronize** — update affected authoritative artifacts, including `PROJECT_STATE.md` when meaningful state changed.
9. **Report** — summarize outcome, validation, state change, and unresolved issues.

## `PROJECT_STATE.md` Policy
`PROJECT_STATE.md` is agent-maintained. The agent updates it autonomously after authorized, validated work changes meaningful project state.

State maintenance MUST NOT be used to approve or legitimize a change that requires human authority. If work would change scope, approved architecture, approved requirements, business rules, security boundaries, costs, branches, or another approval-controlled area, stop and request approval first.

State contains the present, not a running history. Git, roadmap completion records, decisions, and research retain history.

## Approval Model
### AUTONOMOUS
Routine implementation inside approved requirements; tests; documentation synchronization; behavior-preserving refactoring; formatting/lint fixes; bounded bug fixes that do not alter approved behavior.

### NOTIFY
Low-risk internal changes that are useful to surface but do not alter project authority, such as a small internal abstraction or test utility. Project/global instructions may tighten this category.

### APPROVAL REQUIRED
At minimum: branch creation/switching; costs or paid services; consequential architecture changes; new external services; weakening security; scope changes; destructive operations; irreversible migrations; credential/secret changes; production actions; ambiguous/conflicting requirements; changes to established business rules; or project-specific restricted actions.

Project rules may add restrictions but may not weaken global restrictions.

## Task Routing / Negative Routing
`AGENTS.md` should contain a compact routing table. For each common task type specify:
- required context;
- conditional context;
- context not to load by default;
- applicable validation;
- approval triggers.

The router is a map, not an encyclopedia.

## Continue-Project Protocol
When instructed `Continue this project`:
1. Read project `AGENTS.md`.
2. Read `PROJECT_STATE.md`.
3. Inspect Git status.
4. Inspect recent relevant Git history.
5. Read the active milestone in `docs/ROADMAP.md`, unless `PROJECT_STATE.md` explicitly identifies a different authoritative roadmap path for migration compatibility.
6. Follow authoritative references from project state.
7. Verify important state claims against implementation where appropriate.
8. Detect discrepancies/blockers.
9. Determine the next bounded action.
10. Report orientation before modifying anything.

The orientation should state: current milestone, last completed work, current state, next bounded action, relevant requirements/decisions/risks, likely files, validation, and whether approval is required.

## RCS Specification Decisions
### DEC-RCS-001 — Keep mandatory constraints above project-level authority
- **Status:** APPROVED

#### Decision
Mandatory platform, safety, and security constraints are not overridable. Within those boundaries, global agent governance precedes current explicit human project instructions, followed by the project authority hierarchy defined above.

#### Context
The original ordering could be read as allowing a human instruction to override mandatory constraints or global governance.

#### Alternatives Considered
1. Retain the ordering and rely on readers to infer non-overridable constraints.
2. Explicitly state the hard boundary and order project-level authorities beneath it.

#### Rationale
The explicit boundary prevents project or session instructions from weakening mandatory controls while preserving authorized human control over project intent.

#### Trade-offs
The hierarchy is longer, but makes the non-overridable boundary clear.

#### Consequences
Agents must honor mandatory constraints first. Authorized human changes to project intent must be reflected in affected repository documentation.

#### Revisit When
Platform or governance requirements materially change.

### DEC-RCS-002 — Use a canonical roadmap path with migration compatibility
- **Status:** APPROVED

#### Decision
Use `docs/ROADMAP.md` as the canonical roadmap path. For migration compatibility, `PROJECT_STATE.md` may explicitly identify a different authoritative roadmap path in an existing repository.

#### Context
Generic references to the active roadmap did not tell agents where to find it, while requiring an immediate move could disrupt existing repositories.

#### Alternatives Considered
1. Leave the roadmap path unspecified.
2. Require every repository to use `docs/ROADMAP.md` immediately.
3. Specify the canonical path and permit a state-declared migration exception.

#### Rationale
The canonical path makes cold-start routing reliable, and the explicit exception supports incremental migrations without ambiguity.

#### Trade-offs
Repositories using a temporary alternate path must keep the location explicit in project state.

#### Consequences
Templates and protocols route agents to `docs/ROADMAP.md` unless project state names the existing authoritative alternative.

#### Revisit When
The recommended repository structure or migration model changes.

## Definition of Done
A bounded task is complete only when:
- implementation is complete;
- applicable validation passes (or failures are explicitly reported);
- tests are added/updated where appropriate;
- no unexplained regressions remain;
- affected documentation is synchronized;
- project state is synchronized when meaningful state changed;
- consequential new decisions are recorded with rationale;
- no approval boundary was crossed without approval.

## Decision Standard
Every consequential decision records: decision, context, alternatives considered, rationale for the chosen option, trade-offs, consequences, revisit conditions, and supporting evidence when applicable.

## Roadmap Standard
Roadmaps are milestone-based, not sprint/date based. Each milestone has an ID/name, objective, status, deliverables, exit criteria, dependencies, and related requirements where useful. Dates appear only for real external deadlines or time-bound evidence windows.

## Research Standard
Research is episodic and normally lives under `docs/research/`. Long research artifacts are not default context. Higher-level documents point to them when evidence is needed.

## Validation Contract
Every serious repository exposes canonical validation instructions. RCS does not prescribe a universal language/tool stack; the project router points to the project-specific checks.

## Bootstrap Workflow
Brainstorm → structure decisions → create project documentation → completeness review → resolve open questions → initialize repository → create project router → initialize state → begin first milestone.

## Cold-Start Acceptance Test
Open a fresh coding-agent session with no prior conversation and issue only: `Continue this project.`

Pass criteria: the agent correctly identifies project purpose, current milestone/objective, last completed work, next bounded action, relevant requirements/decisions/risks, likely files, validation, and approval needs without broad repository archaeology or invented context.

If the test fails, improve repository context architecture rather than enlarging the prompt.

## Anti-Bloat Rules
Do not create `CODEBASE_MAP.md`, `CURRENT_TASK.md`, `SESSION_LOG.md`, `IMPLEMENTATION_LOG.md`, `TODO.md`, `KNOWLEDGE_BASE.md`, or similar artifacts by default. Add an artifact only after a real project demonstrates a distinct, non-duplicative need.
