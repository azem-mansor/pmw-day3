# Day 3 Workshop: An Ultra-Simple Guide

No chip knowledge or coding experience is assumed. Work through this page from top to bottom. The [Master Task Guide](GH600_Day3_Master_Task_Guide.md) has the exact commands, example results and worked answers for every task. The [Study Notes](GH600_Day3_Study_Notes.md) explain why the ideas work.

## What are we building?

Imagine a team deciding which improvements to put in its next software release. There are 12 possible features. Some need other features to be finished first. The team also has limited time.

The Product Release Workbench helps you **rank** features and **preview** a release. It explains why a release is ready or blocked. It can save a **draft** proposal, but it cannot approve a real release or control factory equipment.

The browser shows the answer. The server checks requests. The **domain code** holds the actual business rules. The store saves data. Copilot can ask a read-only MCP server for information. A feature note is data, not an instruction to Copilot.

## Five words to know first

| Word | Plain meaning |
| --- | --- |
| Feature | Something the team might build |
| Backlog | The list of possible features |
| Release | A group of features planned together |
| Capacity | How many engineering weeks the team has |
| Dependency | Something that must be done first |

**RICE** helps rank features: reach x impact x confidence / effort. It starts a conversation; it does not decide for the team. **Confidence** is a number like 0.80, not 80. A release is blocked if a selected feature is not ready, belongs to another release, needs unfinished work, creates a dependency loop, or takes too long. Lab 6 adds a confidence requirement of at least 0.80.

## Before the workshop

1. Open the `product-release-workbench` folder in VS Code. Keep its hidden `.github` and `.vscode` folders.
2. Have Node 24, Git, GitHub CLI and Copilot agent mode ready. Check `node -v` and `gh auth status`.
3. In a terminal in that folder, run `npm run preflight`, then `npm run baseline`. Baseline should show 8 passing tests.
4. Run `npm start` and open http://127.0.0.1:4173 in a browser. You should see 12 features. Stop the server with Ctrl+C when you are done.
5. Check which GitHub plan you have and where it shows your Copilot usage. If a number cannot be measured, write **not observed**. Never guess a cost.

The detailed repository setup is in Part B and Lab 1 of the Master Task Guide. Do not run `git init` or create a remote again if you already have a working repository.

## The rule for every pull request

Do these three passes **in order**. A pull request (PR) is a request to merge your branch into `main`.

1. **Build:** make the agreed change, check the diff, and run the relevant tests.
2. **Evidence:** record the real command output and the commit ID (SHA) that produced it. Fill in the PR template. Record usage only if you actually observed it.
3. **Review:** use a fresh chat, read the full diff yourself, record findings, and resolve comments. Tick the Review box only when the review is done.

Keep the PR description in a copy of the template outside the repository, such as `../pr-body.md`. Do not use `gh pr create --fill`; it skips the required boxes. After a new push or branch update, the code is a **new candidate**: check it again, update the evidence, untick and redo the Review pass. Merge only when the three passes are done and `accepted-checks`, `performance-budget` and `governance-guard` are green.

## Lab 1: Set up and protect the repo

**Goal:** create your own repository, protect `main`, and make your first reviewed change.

| Task | In plain words |
| --- | --- |
| L1.1 | Read the rules and tests. Some tests fail on purpose because later labs are unfinished. Find the marked `_START` code sections. |
| L1.2 | Create and publish your own GitHub repository. Check that you have Admin permission and CI runs. |
| L1.3 | Apply the `protect-main` ruleset. Prove it blocks your own direct push. Follow the Master Task Guide's exact proof steps. |
| L1.4 | Make a working branch. Read what `governance-guard` checks before editing agent settings. |
| L1.5 | Set up five agent roles. Give each only the tools it needs and choose its model deliberately. |
| L1.6 | Confirm the agents actually load; record your billing plan and a real usage starting point. |
| L1.7 | Ask the planner for a plan. Challenge it against the contract, then accept or correct it yourself. |
| L1.8 | Use the three passes to open and merge your first PR. Check the required CI results. |

**Checkpoint:** baseline 8/8; the ruleset rejects a direct push; your first PR has three completed passes and three green required checks. Only try the direct-push proof from L1.3 with a clean worktree: its cleanup command discards local changes. If GitHub rulesets cannot be enforced on your chosen repository, stop and use the repository option in the Master Task Guide that supports them.

## Lab 2: Give Copilot a small, safe view

**Goal:** let Copilot read current feature and release information without editing it or wasting context.

| Task | In plain words |
| --- | --- |
| L2.1 | Follow one MCP tool call from VS Code to the server, the result, and the usage log. |
| L2.2 | Run `npm run lab:02`. Seven failures are expected before you finish the missing code. |
| L2.3 | Fill only the marked Lab 2 sections in the MCP files. Check `npm run lab:02` and `npm run baseline`. |
| L2.4 | Start the MCP server in VS Code. Look at a **real** tool invocation, not just an agent's claim. |
| L2.5 | Check that a hostile feature note stays data, bad IDs are refused, and no publish tool exists. |
| L2.6 | Compare a whole-backlog result, one release, and one feature. Restore the token budget to `1500` after the `300` experiment. |
| L2.7 | Add the completed test suites to CI, record evidence, do the three passes, and merge. |

**Checkpoint:** Lab 2 tests 13/13. Logs contain argument **names**, not values or feature-note text. A shortened result says it was shortened.

## Lab 3: Rank features and check release plans

**Goal:** give the same correct answer every time and explain why a selection is blocked.

| Task | In plain words |
| --- | --- |
| L3.1 | Work out FEAT-001 and FEAT-002 scores before coding: 108 and 64. Three selected features need exactly 8 weeks. |
| L3.2 | Agree on the design: check inputs, keep scoring separate from saved data, and list all release blockers. |
| L3.3 | Fill the score section in `src/domain.mjs`; do not change the tests or seed. |
| L3.4 | Fill the readiness section: status, release, dependencies, cycles and capacity. Never auto-fix a person's selection. |
| L3.5 | Run `npm run lab:03`, `npm run baseline` and `npm run perf`. Investigate a failure before retrying. |
| L3.6 | Use the debugger to inspect one blocked preview and record one real observation. |
| L3.7 | Try ready, blocked and invalid choices in the browser. Record the results you see. |
| L3.8 | Add the completed suite, review the change on the current commit, and merge through a PR. |

**Checkpoint:** Lab 3 tests 12/12. A capacity of 8 allows 8 weeks; 7 does not. FEAT-003 alone needs FEAT-001 and is blocked.

## Lab 4: Build API and UI in separate folders

**Goal:** make the server enforce draft rules and the browser explain them.

| Task | In plain words |
| --- | --- |
| L4.1 | Agree on preview field names. Create separate API and UI worktrees (extra folders with separate branches). |
| L4.2 | Check whether the coordinator **actually called** the planner. If not, record a manual handoff. |
| L4.3 | In the API folder, make the server recalculate previews and refuse stale or blocked drafts. Test W04-W09. |
| L4.4 | In the UI folder, show loading, ready and blocked states. Test W01-W03. The button is not the safety check. |
| L4.5 | Review both PRs separately, including any Copilot review comments. Resolve each conversation. |
| L4.6 | Merge API first. Update the UI branch, **redo its Review pass**, merge it, and test the combined result. Use a third PR to accept the Lab 4 suite. |
| L4.7 | Create a draft in the browser. Try replaying the same request and checking a blocked request. |
| L4.8 | Confirm the integrated checks and the current review. Clean up worktrees only after their changes are merged. |

**Checkpoint:** Lab 4 tests 9/9; three merged PRs with their own passes. A blocked draft request sent directly to the API returns `BLOCKED_RELEASE`, even if the browser button is bypassed.

## Lab 5: Avoid overwrites and measure speed

**Goal:** handle conflicts correctly and see how long requests take.

| Task | In plain words |
| --- | --- |
| L5.1 | Open the same feature in two browser tabs. See the old edit overwrite the new one before the fix. |
| L5.2 | Require the version the editor saw. Refuse an old version with `STALE_VERSION`. Retry only temporary failures on safe reads. |
| L5.3 | Record request counts and recent timings without saving a separate series for every feature ID. |
| L5.4 | Run `npm run lab:05`, `npm test` and `npm run perf`. Repeat the two-tab experiment and check `/api/metrics`. |
| L5.5 | Review the failure examples and your **current** code, not output from an older commit. |
| L5.6 | Add the completed suites, do all three PR passes, and merge. |

**Checkpoint:** `npm test` 57/57. The second tab gets a 409 conflict and does not erase the first edit. The server reports p50 and p95 times.

## Lab 6: Make the product change

**Goal:** enforce the new confidence rule everywhere and hand off proof.

| Task | In plain words |
| --- | --- |
| L6.1 | Start a new branch, copy in the capstone tests, and see the expected failures before coding. |
| L6.2 | Plan the smallest change: domain rule, contract version, contract document, MCP description and accepted suite. |
| L6.3 | Block confidence **below** 0.80 in shared domain code. Set the contract version to `1.1`; do not add a second rule in the UI. |
| L6.4 | Run full tests and perf. Check 0.80 passes, 0.75 is blocked, and old previews are rejected. |
| L6.5 | Generate the usage report. Separate actual measured values from token estimates and missing readings. |
| L6.6 | Merge with three completed passes; fill in the handoff with real results and the final commit ID. |
| L6.7 | Prepare a four-part explanation: product flow, tool and usage evidence, prevented failure, and review. |

**Checkpoint:** contract 1.1; `npm test` 61/61; a blocked draft still fails when sent directly to the API; the handoff and review describe the current code.

## When something goes wrong

| What happened? | Next step |
| --- | --- |
| A test failed | Read its name; record the input, expected result and actual result. After two failed repair attempts, stop and narrow the case. |
| The server does not start | Check Node 24, the terminal output, and whether port 4173 is already in use. Do not claim the browser check passed. |
| `governance-guard` is red | Read its finding. Complete missing passes; do not remove accepted suites or weaken a budget just to get green. |
| Your edit got a 409 conflict | Reload and compare changes. Do **not** resubmit automatically with the newer version. |
| You do not know if a draft was created | Replay the **same body and idempotency key**. Do not invent a new key. |
| A preview is stale | Get a new preview and ask the person to decide again. |
| An MCP list says `truncated: true` | Ask for one release or one feature instead of assuming the list was complete. |
| You cannot see Copilot usage for one task | Write "not observed". Do not turn estimated tokens into a made-up bill. |

## Your finish line

Show a working draft flow, the CR01 confidence rule, the real test and performance output from the current commit, green required checks, your reviewed PRs, and a handoff that says who owns the next decision. The [Master Task Guide](GH600_Day3_Master_Task_Guide.md) gives exact evidence and commands for each checkpoint.