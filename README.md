# OSINT Source Index

A working register of institutional sources for investigative journalism, organised by country and category, with verified social handles and editorial framing. Every entry signed, dated, and sourced.

Live at [signalandshadow.io/osint-source-index](https://signalandshadow.io/osint-source-index).

Maintained by [Signal & Shadow](https://signalandshadow.io). Identifier: `SIG-ATL-001`.

## What this is

A curated dataset of social media accounts belonging to governments, media organisations, NGOs, military and law enforcement bodies, embassies, courts, legislatures, and other institutions worldwide. Every entry is editorially verified before inclusion. Risk-flagged sources (state media, conflict parties, propaganda outlets, terrorism designations) are marked accordingly so reporters can frame their use appropriately.

The Index is built for reporters, fact-checkers, and accountability researchers who need to confirm a primary source, document an official statement, or trace what an institution has said.

## What this is not

This is not a directory of every account on social media. Inclusion is editorial. We index sources we would use ourselves and that meet the verification standard described in [LST-001](https://signalandshadow.io/lst-001).

This is not a real-time feed. The dataset is updated periodically, not continuously. Each entry carries `accounts_verified_at` and `first_indexed` dates so users can judge currency for themselves.

## Using the dataset

The full dataset lives inside `index.html` as embedded JSON. Click "Download sources.json" in the interface to extract it as a standalone file.

The dataset is licensed under [Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/). You may use it freely, including commercially, with attribution.

Suggested citation:

> OSINT Source Index. Signal & Shadow. https://signalandshadow.io/osint-source-index. Licensed under CC BY 4.0.

The interface code (HTML, CSS, JavaScript) is licensed separately under MIT. See `LICENSE-CODE.txt` and `LICENSE-DATA.txt`.

## Schema

Each record has the following structure:

```json
{
  "entity_id": "BM-1212",
  "entity_name": "FBI New York",
  "native_name": null,
  "country": "United States",
  "subdivision": "New York",
  "category": "law_enforcement",
  "subcategory": "Federal Field Office",
  "languages": ["en"],
  "risk_flags": [],
  "verification_status": "verified",
  "reliability_tier": "1",
  "accounts_verified_at": "2026-05-02",
  "first_indexed": "2026-04-23",
  "accounts": [
    {
      "platform": "twitter",
      "display_handle": "NewYorkFBI",
      "canonical_url": "https://twitter.com/NewYorkFBI",
      "account_role": "official"
    }
  ]
}
```

Field reference:

- **entity_id** — stable identifier. `BM-XXXX` for most records; `IE-XXX` for legacy enriched Ireland records.
- **entity_name** — institutional name in English where applicable.
- **native_name** — the institution's name in its native script or language, where different.
- **country** — primary country of operation. Some records use editorial groupings like `International`, `NGOs (cross-border)`, or `Migrant rescue` for entities not bound to a single state.
- **subdivision** — first-level administrative subdivision (state, province, autonomous region) where applicable.
- **category** — top-level type. One of: `government`, `media`, `law_enforcement`, `emergency`, `ngo`, `military`, `political_party`, `individual`, `judiciary`, `diplomatic`, `legislature`, `infrastructure`, `space`, `sports`, `other`.
- **subcategory** — finer-grained type, free-text.
- **languages** — ISO 639-1 codes for the institution's primary working languages.
- **risk_flags** — editorial framing of source character. Possible values: `state_media`, `state_affiliated`, `conflict_party`, `propaganda_outlet`, `terrorism_designation`. Empty array means no flags applied.
- **verification_status** — currently always `verified`. Reserved for future use.
- **reliability_tier** — currently always `1`. Reserved for future use.
- **accounts_verified_at** — ISO date when the account handles were last confirmed.
- **first_indexed** — ISO date when the entity first entered the Index.
- **accounts** — array of social media accounts. Each has `platform`, `display_handle`, `canonical_url`, `account_role`.

## Categories

Current category counts can vary; consult the live Index for current numbers. The "Top by source count" panel in the interface lists the top eight countries.

## Risk flags

Five flags currently in use:

- **state_media** — broadcaster or wire service controlled or directed by a state. Examples: RT, TASS, Xinhua.
- **state_affiliated** — institution with formal state ties whose editorial output is influenced by state interests.
- **conflict_party** — armed group, paramilitary unit, or military formation actively involved in armed conflict.
- **propaganda_outlet** — outlet whose editorial output is primarily disinformation or propaganda.
- **terrorism_designation** — entity formally designated by at least one major jurisdiction as a terrorist organisation.

A risk flag is not a judgment that the source should not be cited. It is a signal that the source requires editorial framing before use. Working journalists use risk-flagged sources every day; the Index marks them so the framing is explicit.

## Editorial standard

Every entry is written under [LST-001](https://signalandshadow.io/lst-001), the Signal & Shadow house standard for voice, structure, sourcing, and attribution.

Verification standard (working publication standard):

1. Institution exists.
2. Country attribution is correct.
3. Accounts plausibly belong to the institution.

We do not always confirm institutional control over an account through challenge-response; for that level of verification, consult the institution directly.

## Reporting issues

For corrections, missing institutions, or wrong attributions: open an issue on this repository, or email signalandshadow.io.

We do not currently accept user-submitted entries through the interface. The Index is editorially curated. Submissions are reviewed manually.

## Embedding

The interface is designed to be embedded via iframe. The recommended embed:

```html
<iframe
  src="https://YOUR-USERNAME.github.io/osint-source-index/"
  style="width: 100%; height: 100vh; min-height: 800px; border: 0;"
  title="OSINT Source Index"
  loading="lazy"
></iframe>
```

When embedded, URL state (filters, selected entity) lives on the iframe's URL rather than the parent page. Direct links to specific filters or records work via the iframe's source URL, not the embed URL.

## Local preview

This is a single-file build — open `index.html` directly in any modern browser. No server, no build step, no dependencies. The dataset is embedded; no separate fetch required.

## Deployment

The repository is structured for GitHub Pages. After enabling Pages on the repository, the Index is served from `https://USERNAME.github.io/REPO-NAME/`.

## Schema versioning

Schema version: `v1`. Recorded in `meta.schema` of the dataset.

Issue counter: `meta.issue` increments with each material update. Current issue at time of release: see `meta.issue` in the dataset.

## Acknowledgements

The Index is built and maintained by Signal & Shadow. Many entries draw on prior open-source work by Bellingcat, Forensic Architecture, the Berkeley Protocol, and the broader OSINT community.

For methodology, voice, and editorial standards see [signalandshadow.io](https://signalandshadow.io).
