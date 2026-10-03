# Project Agent Router

## Project Identity
[One-paragraph identity. Do not duplicate the README.]

## Always Read
- `PROJECT_STATE.md` — current position and next bounded action.
- [Any non-negotiable project-specific safety/context file.]

## Task Routing
| Task type | Required context | Conditional context | Do not load by default | Validation |
|---|---|---|---|---|
| Continue project | `PROJECT_STATE.md`, active milestone in `docs/ROADMAP.md` (or alternate path explicitly identified in project state), Git status/history | Referenced requirements/decisions | Historical research | Orientation only before changes |
| Implement feature | Relevant REQ(s), architecture section, active decisions | Risks/research | Unrelated requirements/research | Project canonical checks |
| Fix bug | Affected code/tests, relevant requirement | Architecture/decision if behavior is ambiguous | Roadmap history | Focused tests + canonical checks |
| Architecture | Requirements, architecture, decisions | Research/risks | Unrelated implementation | Review/validation plan |
| Research | Research question/evidence plan | Related decisions/architecture | Unrelated source | Research-specific checks |
| Security-sensitive | Security rules, affected architecture/source | Risks | Unrelated product context | Security + canonical checks |
| Finish task | State + affected authoritative docs | Roadmap/decision/risk docs | Unrelated context | Required checks before completion |

## Approval Boundaries
### Autonomous
[Project-specific additions consistent with global rules.]

### Notify
[Optional low-risk notification cases.]

### Approval Required
- All global approval-required actions.
- [Project-specific restrictions.]

## Context Rules
- Load the smallest sufficient authoritative context.
- Follow references instead of reading all documentation.
- Do not load historical research unless the active task requires its evidence.
- Treat code/tests as implemented reality, not automatic authority over approved intent.
- Surface contradictions rather than silently choosing a side.

## Completion Protocol
Before declaring bounded work complete:
1. Run applicable validation.
2. Review the resulting diff/behavior.
3. Synchronize affected authoritative documentation.
4. Update `PROJECT_STATE.md` if meaningful state changed.
5. Update the relevant milestone in `docs/ROADMAP.md`, unless `PROJECT_STATE.md` identifies an alternate authoritative roadmap path, when applicable.
6. Record consequential decisions with alternatives and rationale.
7. Surface unresolved discrepancies, risks, or approval needs.

## Continue-Project Protocol
When asked to continue:
1. Read this file and `PROJECT_STATE.md`.
2. Inspect Git status and recent relevant history.
3. Read the active milestone in `docs/ROADMAP.md`, unless `PROJECT_STATE.md` explicitly identifies a different authoritative roadmap path for migration compatibility; then read state-linked context.
4. Verify important state claims where appropriate.
5. Report current milestone, last completed work, current state, next bounded action, relevant IDs, likely files, validation, and approval requirement.
6. Do not modify files until orientation is complete.
