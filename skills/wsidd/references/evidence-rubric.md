# Status evidence rubric

Use this rubric to avoid optimistic or misleading project-status claims.

## Evidence strength

Prefer evidence in roughly this order, while accounting for recency and project context:

1. Current successful execution, test, evaluation, build, or deployed-state observation.
2. Existing deliverable plus a recorded validation result or explicit acceptance record.
3. Source and configuration that implement the requirement, supported by relevant tests.
4. Relevant working-tree changes, focused diffs, notebook outputs, or partial artifacts.
5. Documentation, plans, checklists, issue text, comments, or TODO markers.

Lower-ranked evidence can define intent but usually cannot prove completion by itself. A stale test record can be weaker than a current source change that invalidates it.

## Decision rules

### Completed

Use when all material acceptance conditions visible in the project are satisfied. Cite the output and validation evidence. If runtime validation is unavailable, say `Completed (static validation only)` or use `Needs confirmation` when runtime behavior is essential.

### In progress

Use when at least one concrete implementation artifact exists and at least one required condition remains. Typical signals include a partial module, related uncommitted diff, TODO inside implemented work, failing focused test, missing evaluation, or an incomplete deliverable.

Do not label an entire phase in progress merely because the repository has unrelated uncommitted files.

### Not started

Use only when the item comes from a credible requirement or plan and no relevant implementation evidence is found. Absence from a quick scan is not proof; describe the inspected scope when the repository is large.

### Needs confirmation

Use when evidence is missing, contradictory, inaccessible, stale, or cannot establish the required environment state. State the exact evidence needed to resolve it, such as a production health check, field evaluation, stakeholder acceptance, or access to an external tracker.

## Common traps

- A checked documentation box may be stale.
- A source file may be scaffolding or dead code.
- Passing unit tests do not prove deployment or field performance.
- Notebook cells and saved outputs do not prove the current environment can reproduce them.
- A generated artifact does not prove it was reviewed or accepted.
- A commit message describes intent; inspect the relevant change or current state.
- File modification time is weak evidence and should not be the sole basis for status.
- `TODO` can mark optional future improvement rather than an unmet acceptance condition.

## Conflicting sources

When evidence conflicts:

1. Report the conflict explicitly.
2. Prefer current direct evidence over older summaries.
3. Reduce confidence or use `Needs confirmation` rather than inventing certainty.
4. Recommend the smallest check that would settle the status.
