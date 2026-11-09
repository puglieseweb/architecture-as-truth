# One decisions repository for many code repositories

[![Architecture as Truth](https://architectureastruth.org/badge.svg)](https://architectureastruth.org/)

The [starter](../starter/) is one repository: the decisions, the contracts, the behaviours, the plan and the records, beside the code they describe. That is the right shape for one product in one repository. Most teams that try Architecture as Truth (AAT) have more than one repository, and the question comes at once: where does the truth live when the code lives in ten places?

This guide gives the answer PuglieseWeb LTD has run since September 2026 across more than sixty repositories: **one decisions repository, and the contracts and the behaviours beside the code they are tested against.** It changes none of the wording. It is one shape the five principles and the four rules take.

## The split

| Kind | Where | Why |
|---|---|---|
| Decisions | The decisions repository, `docs/decisions/` | A decision rarely fits one repository. A copy in each repository it binds is the second copy that principle 3 forbids. |
| Records | The decisions repository, `docs/records/` | Rule 4 names every document a change reconciled, across repositories. One place to write it, one place to read it. |
| The plan | With the change: in the code repository it touches, or in the decisions repository when it touches several | The plan names pull requests in repositories. It goes where those pull requests are reviewed. |
| Contracts | Each code repository, `docs/contracts/` | Principle 4: the contract is tested against the real code. That test runs where the code is. |
| Behaviours | Each code repository, `docs/behaviours/` | The scenarios are the tests. A test lives in the repository whose pipeline runs it. |
| The agent file | Every repository | The agent reads the file at the root of the repository it is working in. |

The decisions repository holds no code. A code repository holds no decision, only links to them.

## Principle 1 says "beside the code"

> The documents live in version control, beside the code.

"Beside the code" sets the documents apart from a wiki, a shared drive or a chat: the same version control, the same pull request, the same merge as the approval. A decisions repository in the same organisation, changed by the same kind of pull request and approved by the same kind of merge, keeps all of that. What it must not become is a second copy. A code repository links to a decision by its path or URL; it never pastes it.

## How the pieces name each other

- A **decision** names the repositories it binds and the contracts and behaviours that carry it.
- A **code change** names its decision in the pull request, carries its contract and its scenarios in the repository it changes, and flips the scenarios it made pass from `@proposed` to `@built`.
- A **record** in the decisions repository names every pull request the change merged, in every repository, and every document it relied on, each updated or marked unchanged with the reason. The pull request URLs are the link between the two repositories; `record_check.py` refuses a record without one.
- The **plan** names the stories, one pull request in one repository each, and the order they ship in.

An agent asked for a change reads the decisions repository first, then the contracts and behaviours of the repository it is about to change. That is rule 1 in this shape.

## The checks in this shape

**In the decisions repository.** Every pull request there is a decision, an amendment or a record, so every one adds a record. A pull request that touches only records is the record of an earlier change, and passes.

```sh
python3 .aat/checks/record_check.py --root . --require-record "origin/$BASE"
python3 .aat/checks/approved_guard.py --base "origin/$BASE" --head HEAD --guard docs/decisions/ $AMENDMENT
```

The second line treats a decision on the default branch as approved: a change to its text is an amendment, labelled `amendment` by a person. Adding a new decision is always allowed.

**In each code repository.** Rule 2, as in the starter:

```sh
python3 .aat/checks/approved_guard.py --base "origin/$BASE" --head HEAD $AMENDMENT
```

Rule 4 for a code change is checked where the record lives, in the decisions repository, and the record is written when the change has merged. So a code repository's pipeline cannot refuse a change for having no record. What it can refuse is a change that adds behaviour with no scenario, and that is the one check this shape needs that the single repository did not.

## The hazard, and the rule that answers it

When the decisions move to one place, it becomes easy to stop there: decide in the decisions repository, build in the code repository, and never write the scenario. The decision is true, the build cites it, and nothing proves the behaviour.

We found this in our own repositories on 2026-11-09. One code repository had six features merged in five days, each citing an amendment in the decisions repository, and not one feature file. The decisions were kept; the behaviours were not. No check had noticed, because every check we ran looked at structure, not at whether a change that adds behaviour carries its scenarios.

The rule that answers it: **a change that adds behaviour a person can observe carries its scenarios in the repository it changes. A decision alone is not enough.** A pipeline can hold it with a check that a change touching code also touches `docs/behaviours/`, or carries a label a person gave it saying it changes no behaviour (a fix, a refactor, a dependency). The label is a person's, like `amendment`. This starter leaves that check to the team's pipeline. Either way the record makes the gap visible: a record whose code pull requests touched no `.feature` file is a record to read twice.

Measure before you enforce. When we counted, the same day, 110 of 164 feature merges across our repositories in two weeks had changed neither a feature file nor a change's documents. A check that refused them all from the first day would have turned two merges in three red. Ours began by reporting, with one switch per repository to make it refuse.

## Evidence

PuglieseWeb LTD has run this shape since September 2026: one decisions repository for more than sixty code repositories across several products, one owner who approves and AI agents that build. On 5 November 2026 the decisions repository held 226 decision records and 2,975 dated change records, each naming the documents it reconciled. The code repositories carry their contracts and scenarios per change, and the scenarios run as tests in their own pipelines.

Interest declared: the company builds [SystemDox](https://www.systemdox.com/architecture-as-truth), which reads this layout from a team's own repositories and serves it to agents over MCP. Nothing in this guide needs it. A Git host, two workflows and the two checks are enough.

## Try it

[`starter-many-repositories/`](../starter-many-repositories/) holds the two agent files and the two workflows for this shape. The templates for the documents are the starter's.

---

Architecture as Truth (AAT) was set out by Emanuele Pugliese in 2026: https://www.puglieseweb.com/blog/architecture-as-truth · CC BY 4.0, © 2026 PuglieseWeb LTD.
