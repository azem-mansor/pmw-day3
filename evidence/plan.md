# Approved increment plan

**Work item and contract version:**  
Lab 02, “Implement a bounded release context tool,” from `prompts/02-tool.md`. Contract version **1.0**, as specified in `docs/contract.md`.

**Current SHA and known dirty changes:**  
`evidence/readiness.md` records SHA `2a59476c9bfcb90b3ddc372c36762471b7dfad1c` on `main`.

**Branch name and target pull request:**  
`main` is recorded in the readiness file. No target pull request was provided.

**User outcome and exclusions:**  
A user can read advisory information for R1 or R2, and MCP tool usage is measured without saving private feature details. This work does not approve or publish a release, change the UI, or alter the existing transport, tests, or data.

**Allowed files and owner:**  
- Code changes: only the four named Lab 02 seams in `mcp/tools.mjs` and `mcp/usage.mjs`.
- After the check passes, append the existing Lab 02 suites to `ci/accepted-suites.json` and record actual results in `evidence/checks.md`. Record usage in `evidence/agent-usage.csv` only when actual usage details are known.
- No changes to test files or data.

**Implementation sequence:**  
1. Complete `LAB02_CONTEXT_START`: accept only R1 or R2 and return that release’s records, contract version, current revision, source revision, and `advisory: true`.
2. Complete `LAB02_USAGE_START`: estimate tokens by dividing result-text characters by four and rounding up.
3. Complete `LAB02_BUDGET_START`: return results that fit unchanged; shorten an oversized `items` or `features` list with a count of omitted entries and a hint; reject other oversized results.
4. Complete `LAB02_RECORD_START`: record the time, tool, sorted argument names, result size, estimate, duration, and outcome—never the argument values or result text.
5. Run the Lab 02 check. If it passes, update the accepted-suite and evidence records with actual results.

**API and UI acceptance:**  
R1 requests return only R1 records; R2 requests return only R2 records. Invalid releases and unsupported tools remain errors. The MCP tool stays read-only. No UI changes are expected.

**Checks and failure scenarios:**  
Run `npm run lab:02` from the repository root. Confirm invalid releases are rejected; oversized list results include correct omission details; other oversized results fail clearly; and usage records contain no argument values or result text. Record the actual output and exit status. No check has been run yet.

**Suites to add to `ci/accepted-suites.json`:**  
Append `tests/lab02.test.mjs` and `tests/usage.test.mjs` after the work passes. Do not modify either test file.

**Agent and model per step, expected prompts:**  
One implementation pass using the current Copilot assistant and model `gpt-6-luna`; use the Lab 02 work item in `prompts/02-tool.md`. No separate agents are planned.

**Rollback and preserved evidence:**  
Undo only the Lab 02 seam changes in the two MCP files and the corresponding Lab 02 entry in the accepted-suite list if rollback is needed. Keep prior evidence; do not replace it with unverified results.

**Product decisions:**  
None identified. The required source revision should come from the release context available to the agent; the current read returned only a TODO placeholder, so no release revision can be reported yet.

**Human approval name and time:**  
Nor Muhamad Azem Bin Mansor, 11:45 AM 13.10/26
