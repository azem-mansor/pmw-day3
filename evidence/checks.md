# Validation record

Populate this file from actual execution. Do not mark a check as passed from an agent summary alone.

For every checkpoint record:

- Work item and lab:
- Candidate SHA and any dirty source changes:
- Command and working directory:
- Execution time and Node version:
- Pass/fail/selected check totals:
- Relevant actual output or approved output-file path:
- Interpretation and next action:

Separate a subprocess MCP probe from a live client invocation. Record the invoked tool, arguments, returned revision/contract and observed client activity separately. A later source change requires validation against that new candidate.

## Source seams

1. `LAB02_CONTEXT_START` (`mcp/tools.mjs`) implements the validated `get_release_context` read, returning the requested release's records and source revision as advisory context.
2. `LAB02_USAGE_START` (`mcp/usage.mjs`) estimates result tokens as the ceiling of the result text's character count divided by four.
3. `LAB02_BUDGET_START` (`mcp/usage.mjs`) truncates over-budget `items` or `features` lists with omission details and a hint, and fails closed for other oversized results.
4. `LAB02_RECORD_START` (`mcp/usage.mjs`) records tool usage metadata and argument keys without storing argument values or result text.
5. `LAB03_SCORE_START` (`src/domain.mjs`) calculates unrounded priority as reach multiplied by impact and confidence divided by effort.
6. `LAB03_READINESS_START` (`src/domain.mjs`) reports blockers for selected feature status, release, dependencies, dependency cycles and capacity while accumulating effort in integer hundredths.
7. `LAB04_SNAPSHOT_START` (`src/proposals.mjs`) re-derives release readiness and verifies the supplied contract version and snapshot before allowing a draft.
8. `LAB04_VIEW_START` (`web/release-view.mjs`) turns the server's preview and pending state into a release summary without deciding readiness in the UI.
9. `LAB05_VERSION_START` (`src/concurrency.mjs`) rejects absent or stale feature versions before a feature edit is saved.
10. `LAB05_PERCENTILE_START` (`src/metrics.mjs`) calculates nearest-rank percentiles from ascending request-duration values.
11. `LAB05_RECORD_START` (`src/metrics.mjs`) tracks lifetime request and error counts alongside a bounded per-route window of recent durations.
12. `LAB05_RETRY_START` (`src/retry.mjs`) retries transient read operations within the validated attempt limit while honoring the supplied delay and abort signal.
