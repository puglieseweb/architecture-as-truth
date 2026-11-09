# The many-repositories guide says six features, not seven, and what a count of our own merges found

**Date:** 2026-11-09
**Actor:** Claude (session `9ea50777-8443-4c35-bdc1-1bf362ffd595`), at Emanuele Pugliese's request

## Merged
| PR | Title |
|---|---|
| https://github.com/puglieseweb/architecture-as-truth/pull/10 | The many-repositories guide: six features, not seven, and measure before you enforce |

## What changed
The guide said one of PuglieseWeb's repositories had "seven features merged in ten days" with no feature file. The count was wrong, and it was the agent's: the repository's history shows six feature merges between 30 October and 3 November 2026, five days. The sentence now says six in five days. The point it makes is unchanged: each cited an amendment in the decisions repository, and none carried a scenario.

One paragraph is added under the hazard. The same day the company counted its own merges before switching a check on: 110 of 164 feature merges in two weeks had changed neither a feature file nor a change's documents, so its check began by reporting, with a switch per repository to make it refuse. That is evidence a team adopting this shape can use, and it is why the guide still leaves the check to the team's pipeline.

## Documents reconciled
- `guides/many-repositories.md` — updated: the count, and the paragraph "Measure before you enforce"
- `docs/records/2026-11-09-one-decisions-repository-for-many-code-repositories.md` — unchanged: it names the hazard without a number; records are not rewritten
- `ARCHITECTURE-AS-TRUTH.md`, `agent/AGENTS.md` — unchanged: no definition, principle or rule changed
- `starter-many-repositories/`, `checks/` — unchanged: the starter still leaves the scenarios check to the team; no check was added to the kit
- `IMPLEMENTATIONS.md`, `site/` — unchanged: neither quotes the count
