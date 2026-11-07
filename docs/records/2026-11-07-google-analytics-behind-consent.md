# Google Analytics measures visits, behind consent

**Date:** 2026-11-07
**Actor:** Claude, at Emanuele Pugliese's request

## Merged
| PR | Title |
|---|---|
| (this pull request) | Google Analytics measures visits, behind consent |

## What changed
The reference site loads Google Analytics 4 (property `architectureastruth.org`, measurement ID `G-37RCFT10FC`, enhanced measurement on) in Consent Mode v2, advanced mode. Every storage type starts denied. Until a visitor accepts, Google Analytics sets no cookie and receives only cookieless measurements, which GA4 uses for anonymous, modelled trends. A banner asks once; Accept grants `analytics_storage` only, Decline keeps it denied and deletes any `_ga` cookies. Advertising storage, ad personalisation and Google signals are never enabled. The choice is kept in the browser's local storage, and the footer's "Analytics choice" reopens the banner. The footer no longer says "No cookies, no tracking": it says what is measured, with and without consent. The 404 page loads nothing new.

## Documents reconciled
- `site/index.html` — updated: the tag, the banner, the footer notice
- `.github/workflows/pages.yml` — updated: its comment named no third-party assets
- `docs/records/2026-11-06-brand-seo-and-links.md` — unchanged: records are not rewritten; its note that the footer's "no tracking" stays true is superseded by this record
- `ARCHITECTURE-AS-TRUTH.md`, `agent/AGENTS.md` — unchanged: no definition, principle or rule changed
- `CHANGELOG.md` — unchanged: the wording's version is still 1.0
