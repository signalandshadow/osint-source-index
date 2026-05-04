# Changelog

All notable changes to the OSINT Source Index. The dataset's `meta.issue` field tracks the same counter.

## Issue 065 (2026-05-04)

Public release.

- 1,811 verified institutional sources across 93 countries
- 15 categories: government, media, law_enforcement, emergency, ngo, military, political_party, individual, judiciary, diplomatic, legislature, infrastructure, space, sports, other
- 5 risk flag types: state_media, state_affiliated, conflict_party, propaganda_outlet, terrorism_designation
- 14 social platforms indexed: Twitter, Facebook, YouTube, Instagram, Telegram, Weibo, LinkedIn, TikTok, VK, Flickr, Vimeo, web, SoundCloud, Snapchat
- 3,077 verified social accounts total

## Interface history

The Index ships as a single-file viewer with the dataset embedded inline.

- Map-first investigative dashboard with side rail (Issue 049)
- Risk-mode and category-mode map overlays (Issue 049)
- Per-platform colour accents on account links (Issue 050)
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

## Known limitations

- Subdivision naming consistency drifts across some country builds (Türkiye / Turkey, etc).
- Embassy records (281) carry `subdivision: null` and `headquarters_location` populated; UI rendering of embassy diplomatic relationships is not yet specialised.
- 8 records use a legacy `IE-XXX` ID scheme with additional fields (`description`, `wikidata_id`, `founded`, `country_code`) from a prior enrichment pass. Functional but schema-inconsistent.
- URL state (filters, selected record) lives on the iframe's URL when embedded, not on the parent page URL.
