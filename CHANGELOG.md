# Changelog

All notable changes to the OSINT Source Index. The dataset's `meta.issue` field tracks the same counter.

## Issue 087 (2026-09-20)

Interface rebuilt from the ground up, twice, before landing on the current version. First pass matched the wrong design system (the project's own design-system reference had gone stale relative to the live site). Second pass corrected the visual system but kept the general-purpose database-browser shape (two-column layout, static sidebar facets). Third pass reworked the interaction model itself around a single use case: a reporter on deadline finding one verified source fast, not browsing a dataset.

**Visual system**, matched to the live signalandshadow.io shell: Inter (sans) and DM Mono (identifiers), a light `#F4F5F8` canvas with white rounded panels, a deep violet accent (`#4B3178`), pill-shaped status badges. Identifier renamed from `SIG-ATL-001` to `SIG-SRC-001` to match the tool's current name (it was renamed Source Atlas to OSINT Source Index at Issue 059, but the identifier was never updated to match).

**Interaction model**, reworked around speed of lookup rather than browsing:

- Dropped the two-column database-browser layout (map before that, static sidebar facets after). The page is now a single search-first column: a large search box, two filter buttons (country, category, plus a risk-flag filter) that combine mad-lib style, and results directly below. No sidebar to scan before you can search.
- Country and category are now popover pickers triggered from filter buttons, not a permanently visible sidebar list. Country's picker is searchable, since the dataset spans 218 countries.
- Search matches every word independently rather than the query as one literal phrase. Previously "russia embassy" matched nothing, because no field contains that exact phrase in that order; it now matches 18 entities, including "Embassy of Russia in the United Kingdom". Results are ranked so a name or country match outranks a description-only match, matched terms are highlighted in the list and the detail view, and a type-ahead dropdown (up to 6 results, arrow-key and Enter navigable, `/` to focus from anywhere) appears as you type.
- Account links are now directly clickable from the results list, with a one-click copy-link icon next to each. Previously every link required opening the detail view first.
- New: pinning. A star on each row (and in the detail view) adds a source to a "Your sources" strip at the top of the page, persisted in the browser's `localStorage` (per browser, not synced, not sent anywhere). A "Copy all" button turns the pinned list into plain text (name, country, primary link, citation per source) for pasting into notes.
- The four stat cards collapsed into a single compact identity line. Stub toggle, dataset download, and the LST-001 link moved from sidebar cards into a small utility row, since they support the workflow but aren't part of the fast path.
- Stub toggle behaviour unchanged: 350 of 2,883 entities carry `verification_status: "stub"` and are excluded from the default view and headline stats until switched on, where they render visibly marked and dimmed.
- Detail view surfaces `description`, `wikidata_id`, `wikipedia_url`, `official_website`, `founded`, and `headquarters_location` where present, each account row has its own copy-link control, and risk flags split into amber (cautionary: state media, state affiliated) and red (severe: conflict party, propaganda outlet, terrorism designation).
- Per-platform brand colours on account rows removed in favour of a plain mono label, consistent with the site's single-accent approach to affordance.
- Fixed an em dash in the page `<title>`.
- `meta.title` corrected from `"Source Atlas"` to `"OSINT Source Index"`. It had never been updated after the Issue 059 rename.
- Page widened (880px to 1180px) to fit better inside the site's page template.
- Country flags added throughout (result rows, detail view, country filter, pinned chips). Built from an ISO 3166-1 mapping covering all 218 country strings in the dataset. 10 entries (breakaway or disputed territories, and cross-border groupings like "International" and "NGOs (cross-border)") render with no flag rather than take an editorial position on contested status.
- Category colour system added: each of the 15 categories gets a distinct accent colour, shown as a chip on every result row, in the detail view, and as a coloured dot in the category filter popover. The three filter buttons (country, category, risk flag) each carry a colour identity at rest, not only when active.
- Fixed: the three filter popovers (country, category, risk flag) were clipped by `overflow: hidden` on the quick find panel, added for the header's background gradient. The gradient is a CSS background and was already clipped to the panel's rounded corners without that property, so it was removed; popovers now render in full.
- Country flags added throughout (results list, detail view, country filter, pinned strip, search suggestions), both for colour and for faster scanning. All 218 countries in the dataset were checked against a name-to-flag mapping; the 10 that are disputed territories or editorial groupings without a standard flag (Abkhazia, International, Jammu & Kashmir, Migrant rescue, NGOs (cross-border), Northern Cyprus, Sahrawi Arab Democratic Republic, Somaliland, South Ossetia, Transnistria) show no flag rather than an invented one. Also surfaced, not fixed: the dataset represents Vatican three separate ways (`Vatican`, `Vatican City`, `Holy See (Vatican City State)`) and Czechia two ways (`Czech Republic`, `Czechia`); the flag mapping handles all variants, but the underlying duplication in `country` values is still there.

**Note on the gap between this entry and Issue 065.** The dataset's `meta.issue` was already at `086` (dated 2026-05-17) when this rebuild started, but this changelog's most recent entry was Issue 065. Nineteen to twenty issues of dataset changes were never logged here. This changelog cannot reconstruct what changed issue by issue in that gap, so the record below states the actual current counts rather than inventing a history. If a full account of Issues 066 to 086 is needed, it will have to come from wherever the dataset builds themselves are tracked outside this file.

**Actual current counts (Issue 087, verified sources only):**

- 2,533 verified institutional sources (2,883 total entities; 350 are stub records pending enrichment, see Known limitations)
- 218 countries (up from 93 at Issue 065)
- 15 categories: government, individual, media, diplomatic, law_enforcement, emergency, ngo, military, political_party, judiciary, legislature, infrastructure, other, space, sports
- 5 risk flag types: state_media, state_affiliated, conflict_party, propaganda_outlet, terrorism_designation (77 verified entities flagged)
- 14 social platforms indexed: Twitter, Facebook, YouTube, Instagram, Telegram, Weibo, LinkedIn, TikTok, VK, Flickr, Vimeo, web, SoundCloud, Snapchat
- 4,179 social accounts total across all entities

## Issue 065 (2026-05-04)

Public release.

- 1,811 verified institutional sources across 93 countries
- 15 categories: government, media, law_enforcement, emergency, ngo, military, political_party, individual, judiciary, diplomatic, legislature, infrastructure, space, sports, other
- 5 risk flag types: state_media, state_affiliated, conflict_party, propaganda_outlet, terrorism_designation
- 14 social platforms indexed: Twitter, Facebook, YouTube, Instagram, Telegram, Weibo, LinkedIn, TikTok, VK, Flickr, Vimeo, web, SoundCloud, Snapchat
- 3,077 verified social accounts total

## Interface history

The Index ships as a single-file viewer with the dataset embedded inline.

- Full design system rebuild, map dropped, stub toggle and searchable country facet added, identifier renamed to SIG-SRC-001 (Issue 087)
- Map-first investigative dashboard with side rail (Issue 049)
- Risk-mode and category-mode map overlays (Issue 049)
- Per-platform colour accents on account links (Issue 050, removed at Issue 087)
- Entity detail overlay with composed section structure (Issue 061)
- Database / Map view toggle, Database default (Issues 055, 058)
- Search facets in left rail showing category / country / risk counts (Issue 058)
- Full-width single-column source cards (Issue 063)
- Renamed from Source Atlas to OSINT Source Index (Issue 059)

## Dataset history

Major dataset additions:

- 281 embassies bulk imported from curated Twitter list (Issue 046)
- 12 Red Cross / Red Crescent records, including national societies and regional chapters (Issue 045)
- 14 FBI field offices linked to FBI HQ via parent_entity_id (Issue 044)
- Earlier additions: country-level builds covering most G20 nations, military, judiciary, and NGO records
- Issues 066 to 086: not logged in this changelog. Dataset grew from 1,811 to 2,883 entities and from 93 to 218 countries over this span. See the note under Issue 087 above.

## Known limitations

- 350 entities carry `verification_status: "stub"` rather than `"verified"`, mostly with no `accounts_verified_at` date and often no accounts at all. Excluded from the default view and headline stats as of Issue 087, visible via the stub toggle.
- 430 entities have zero accounts recorded, including some `verified` entities (an institution can be verified to exist and correctly attributed by country without having a confirmed social account yet).
- 161 entities are flagged `needs_resolution: true` in the source data. This field is not yet surfaced in the interface.
- Subdivision naming consistency drifts across some country builds (Türkiye / Turkey, etc).
- Embassy records (281 as of Issue 046, not reverified at Issue 087) carry `subdivision: null` and `headquarters_location` populated; UI rendering of embassy diplomatic relationships is not yet specialised.
- The legacy `IE-XXX` ID scheme mentioned in earlier versions of this changelog no longer applies. All records now use the `BM-XXXX` scheme. `description`, `wikidata_id`, `wikipedia_url`, `founded`, `headquarters_location`, and related fields are present on 255 entities (not limited to 8 legacy records as previously documented) and are unevenly populated across them.
- URL state: the selected entity persists on the iframe's URL via hash. Active filters (category, country, risk flag, search query, stub toggle) do not persist in the URL as of Issue 087.
