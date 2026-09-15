---
name: wsidd
description: Inspect a project and present its real end-to-end workflow, separating completed, in-progress, and not-started work with file, Git, test, or artifact evidence. Use for project status reviews, progress maps, "what has been done", "what is being worked on", and "what should happen next" requests.
---

# What should I did & do?

Create an evidence-based snapshot of a project's workflow and current progress. Treat this as a read-only review unless the user separately asks for implementation or changes.

## Inspect the project

1. Identify the project root and read applicable `AGENTS.md` files before interpreting the project.
2. Inspect the smallest useful set of sources, prioritizing:
   - explicit plans, requirements, roadmaps, issue lists, and checklists;
   - README and architecture or workflow documentation;
   - relevant source, configuration, tests, notebooks, and deliverables;
   - Git status, focused diffs, and recent history when the project uses Git;
   - existing test, build, evaluation, or deployment records.
3. Do not scan secrets, credentials, large datasets, model weights, generated media, or unrelated directories merely to make the report look exhaustive.
4. If no explicit plan exists, infer a minimal workflow from actual project dependencies and label it as inferred. Adapt the phases to the project type; do not force a software-development lifecycle onto research, data, or document work.

Use `rg` or `rg --files` for discovery. Prefer static inspection for an ordinary status request. Run only safe, focused, inexpensive checks when the user asks for verification or when a current result is essential; never start training, deployment, uploads, long builds, or external mutations without separate authorization.

## Classify status

Read [references/evidence-rubric.md](references/evidence-rubric.md) when status is ambiguous, the project is substantial, or completion claims matter.

Assign each meaningful workflow phase or work item one primary state:

- `Completed`: the required output exists and available evidence shows its acceptance condition was met.
- `In progress`: work has materially started, but an acceptance condition, verification, dependency, or deliverable remains open.
- `Not started`: the item is explicitly planned or required, but there is no credible implementation evidence.

Do not force an uncertain item into one of those states. Put it under `Needs confirmation`, explain what is missing, and state the most likely status only if useful. Code presence alone does not prove completion. A plan or unchecked checkbox alone does not prove work started. Uncommitted changes are evidence of activity, not automatically evidence of completeness.

When sources disagree, prefer current executable artifacts and current test results over prose, but report the conflict. Never convert historical, synthetic, mocked, static, or partial validation into a claim of live or production completion.

## Present the result

Lead with a one-sentence project status. Include the snapshot date and state whether the workflow is documented or inferred.

Show the end-to-end workflow as a compact ordered flow using this legend:

- `✅` Completed
- `🟡` In progress
- `⚪` Not started
- `❓` Needs confirmation

Use a Mermaid flowchart only when it renders clearly; otherwise use a single-line or multiline text flow. Keep phase names specific to the project.

Then provide a concise status table with these columns:

| Phase or item | Status | Evidence | Remaining condition |
|---|---|---|---|

Link to local evidence with absolute file paths and line numbers when practical. For Git or command evidence, summarize the exact observation without pasting noisy output. Separate observed facts from inference.

Finish with:

1. `Now`: the current active focus or the strongest evidence-backed candidate.
2. `Next`: one to three dependency-aware actions, ordered by what unblocks the workflow rather than by file order.
3. `Risks / unknowns`: only material gaps that could change the status assessment.

Do not report a numeric completion percentage unless items have comparable weight or the user supplied weights. Counts such as “3 of 7 phases completed” are acceptable when the denominator is explicit.

Keep the report proportional to the project. For a small project, one workflow line and a short table are enough. For a large project, group details into phases and drill down only on active or blocked areas.
