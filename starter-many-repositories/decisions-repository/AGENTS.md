# How an agent works in this repository: Architecture as Truth

This repository is built the Architecture as Truth (AAT) way. The architecture documents are the single source of truth about the product: the decisions, the contracts, the behaviours and the plan. People decide by changing those documents. You build from them. Everything that ships is reconciled back into them.

This is the team's decisions repository. It holds the decisions and the records for every repository the team builds, and no code.

## Where the truth is

| Kind | Where | What it holds |
|---|---|---|
| Decisions | `docs/decisions/ADR-NNNN-<slug>.md`, here | What was decided, why, and what was turned down, for every repository. Each names the repositories it binds |
| Contracts | `docs/contracts/` in each code repository | What that repository promises: OpenAPI or AsyncAPI documents, or a plain `*.contract.md` |
| Behaviours | `docs/behaviours/*.feature` in each code repository | Given/When/Then scenarios. They are also that repository's tests |
| The plan | `docs/plan.md` here for a change that touches several repositories; `docs/changes/<change>/plan.md` in a code repository for a change inside it | The stories, one pull request in one repository each, and their order |
| Records | `docs/records/YYYY-MM-DD-<slug>.md`, here | One dated record per change, in any repository: what merged, what changed, which documents it touched |

A document on the default branch has been approved by a person. The merge was the approval. A code repository links to a decision here; it never copies one.

## The four rules

1. **Read before writing.** Before it changes anything, the agent fetches the decisions, the contracts and the behaviours that govern what it is about to touch.
2. **Build what was approved.** It may not edit a contract, or the wording of a scenario, to make its own work pass.
3. **Stop, do not patch.** When the truth is wrong or silent, the agent raises an amendment for a person and waits for the answer.
4. **Leave the truth true.** Its change names the documents it relied on and updates the ones it made out of date.

## What the rules mean in practice

**A change here is a decision, an amendment or a record.** A new decision is a new file from `docs/decisions/TEMPLATE.md`. A change to a decision's text is an amendment: a pull request labelled `amendment` by a person, which says what was wrong or missing and proposes the answer. A record is a new file under `docs/records/`.

**Before the first edit.** Read the decisions that govern the part of the product in question, in full, and the contracts and behaviours of the code repositories they bind. Working from one repository's code alone is guessing.

**When the truth is wrong or silent.** Stop building, in whichever repository you are in. Open the amendment here, changing only the decision in question. Wait for a person to merge it, then build from the merged text. Do not build through the gap with a confident guess.

**With every change, in any repository.** Add a record at `docs/records/YYYY-MM-DD-<slug>.md` with three sections: `## Merged` (the URL of every pull request the change merged, in every repository), `## What changed` (in plain words) and `## Documents reconciled` (every document you relied on, here and in the code repositories, each updated in the change or marked unchanged with the reason). Update the plan and any decision your change made out of date. The pipeline refuses a change here that adds no record, and an edit to a decision without an amendment.

**Always.** Say in your pull request which documents you read and which you changed. If you made a judgement a person should have made, say so there.

---

Architecture as Truth (AAT) was set out by Emanuele Pugliese in 2026: https://www.puglieseweb.com/blog/architecture-as-truth · Standing reference: https://architectureastruth.org/ · This file: CC BY 4.0, © 2026 PuglieseWeb LTD.
