# A guide and a starter for one decisions repository serving many code repositories

**Date:** 2026-11-09
**Actor:** Claude (session `9ea50777-8443-4c35-bdc1-1bf362ffd595`), at Emanuele Pugliese's request

## Merged
| PR | Title |
|---|---|
| https://github.com/puglieseweb/architecture-as-truth/pull/9 | One decisions repository for many code repositories: the guide and its starter |

## What changed
The starter is one repository, with the decisions, the contracts, the behaviours, the plan and the records beside the code. The only team listed in `IMPLEMENTATIONS.md` does not build that way: PuglieseWeb LTD keeps one decisions repository for more than sixty code repositories, with the contracts and the scenarios in the repository they are tested against. The kit said nothing about that shape. On 2026-11-09 the author asked whether it should be the recommended practice, and this change writes it down.

`guides/many-repositories.md` gives the split (decisions, records and the cross-repository plan in one decisions repository; contracts, behaviours and the agent file beside the code), reads principle 1's "beside the code" as version control against a wiki rather than one repository against two, says how the pieces name each other (the record's pull request URLs are the link), gives the checks for each side, and names the hazard the shape brings: a decision kept and a scenario never written, found in one of PuglieseWeb's own repositories the same day. `starter-many-repositories/` holds the two agent files and the two workflows for the shape; the document templates stay the starter's. The README, the starter's README, the checks' README, the implementations page and the site point at the guide. No wording changed and no check changed: `approved_guard.py --guard` and `record_check.py --dir` already took the paths the shape needs, and `checks/README.md` now says so.

## Documents reconciled
- `guides/many-repositories.md` — added: the guide
- `starter-many-repositories/README.md`, `starter-many-repositories/decisions-repository/AGENTS.md`, `starter-many-repositories/decisions-repository/.github/workflows/aat.yml`, `starter-many-repositories/code-repository/AGENTS.md`, `starter-many-repositories/code-repository/.github/workflows/aat.yml` — added: the starter for the shape. The four rules in both agent files are the fixed wording, unchanged
- `README.md`, `starter/README.md`, `checks/README.md` — updated: a row and a pointer to the guide; the checks' `--guard` and `--dir` options documented
- `IMPLEMENTATIONS.md` — updated: the PuglieseWeb row names the shape it uses
- `site/index.html`, `site/llms.txt` — updated: one link each to the guide
- `ARCHITECTURE-AS-TRUTH.md`, `agent/AGENTS.md` — unchanged: no definition, principle or rule changed; the guide reads principle 1 as it stands
- `CHANGELOG.md` — unchanged: the wording's version is still 1.0; a repository release is the author's to cut
- `checks/approved_guard.py`, `checks/record_check.py` — unchanged: the options the shape needs already existed
