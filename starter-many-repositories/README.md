# Architecture as Truth: the starter for many repositories

[![Architecture as Truth](https://architectureastruth.org/badge.svg)](https://architectureastruth.org/)

The shape for a team whose code lives in more than one repository: one decisions repository, and the contracts and the behaviours beside the code they are tested against. The reasoning is in [the guide](../guides/many-repositories.md). The templates for the documents are in [the starter](../starter/).

## The shape

```
decisions-repository/                 one for the team; it holds no code
  AGENTS.md                           the four rules; says where each kind of document lives
  docs/
    decisions/                        one record per decision, for every product and repository
    plan.md                           the plan for a change that touches several repositories
    records/                          one dated record per change, in any repository
  .github/workflows/aat.yml           every change adds a record; a decision changes only by amendment

code-repository/                      one per repository that holds code
  AGENTS.md                           the four rules; points at the decisions repository
  docs/
    contracts/                        what this repository promises; tested against its code
    behaviours/                       its scenarios; they are also its tests
    changes/<change>/plan.md          the plan for a change inside this repository
  .github/workflows/aat.yml           a build does not edit an approved contract or scenario
```

A document on the default branch of either repository has been approved. The merge was the approval. A code repository links to a decision; it never copies one.

## In an hour

1. **Make the decisions repository.** Copy `decisions-repository/` into a new repository. Copy `docs/decisions/TEMPLATE.md` and `docs/records/TEMPLATE.md` from the starter into it. Write the first decision from the template: that the team builds this way, and where each kind of document lives.
2. **Shape one code repository.** Copy `code-repository/` into it: `AGENTS.md`, `CLAUDE.md` if your agent is Claude Code (the starter's one-line file), and the workflow. Copy `docs/contracts/TEMPLATE.*` and `docs/behaviours/TEMPLATE.feature` from the starter. In `AGENTS.md`, replace `<decisions repository>` with the repository's address.
3. **Pick one part of the product.** Write its decision in the decisions repository. Write its contract and its scenarios, each tagged `@proposed`, in the code repository, and bind the scenarios to that repository's test runner so a `@proposed` scenario runs as an expected failure. Write the plan beside them.
4. **Merge the documents,** in both repositories. That is the first approval, and it is a person's.
5. **Ask your agent for the first story.** It reads the decisions repository, then this repository's contracts and behaviours, builds, flips the scenarios it made pass to `@built`, and writes the record in the decisions repository, naming this pull request.
6. **Open the pull requests.** The code repository's workflow refuses an edit to an approved contract or scenario without an `amendment` label. The decisions repository's workflow refuses a change that adds no record, and an edit to a decision without the label.
7. **Read the record,** not the code.

## The checks

Both workflows fetch the checks from the main repository at a tagged release.

- **The decisions repository** runs `record_check.py --require-record` (rule 4: every change adds a record naming the documents it relied on, with the pull request URLs of every repository it merged in) and `approved_guard.py --guard docs/decisions/` (rule 2, applied to decisions: an edit to one is an amendment, labelled by a person).
- **A code repository** runs `approved_guard.py` (rule 2: a build does not edit an approved contract or the wording of a scenario).

Rule 4 for a code change is checked in the decisions repository, on the record, once the change has merged. The one check this shape asks of a code repository that the single repository did not, that a change adding behaviour carries its scenarios, is the team's to add to its own pipeline; the guide says why.

---

Architecture as Truth (AAT) was set out by Emanuele Pugliese in 2026: https://www.puglieseweb.com/blog/architecture-as-truth · CC BY 4.0, © 2026 PuglieseWeb LTD.
