# Repository Context System (RCS)

RCS is a reusable context architecture for software repositories used with capable coding agents. It keeps durable project knowledge in Git and uses a small router plus current-state file to progressively disclose the right requirements, architecture, decisions, risks, research, code, and tests for the task at hand.

## Start Here
1. Read `RCS_SPECIFICATION.md`.
2. For a new project, instantiate only the templates the project genuinely needs.
3. For an existing project, follow `guides/MIGRATION_GUIDE.md`.
4. Validate the setup with a fresh agent session using only: `Continue this project.`

## Design Goal
The repository should be sufficient for a new capable agent to determine where the project is, what comes next, what constrains the work, how to validate it, and what requires human approval—without relying on prior conversation history.
