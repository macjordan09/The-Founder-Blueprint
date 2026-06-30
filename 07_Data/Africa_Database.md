# Africa Database

Purpose

The Africa Database is the canonical, versioned datastore that will be populated incrementally from every published story, brief, and research artifact. Its purpose is to turn one-off editorial intelligence into reusable, queryable assets that power reports, the AI intelligence product, data subscriptions, and downstream advisory work.

Core goals

- Capture entities and relationships surfaced in our journalism and research (companies, founders, investors, rounds, policies, deals, partnerships, etc.).
- Preserve provenance: every record must link back to source artifacts (URLs, snapshots, and brief IDs) and a method note explaining how the data was derived.
- Make assets discoverable and reusable: standard schema, consistent identifiers, and a taxonomy that supports cross-issue queries and comparisons.
- Enable productization: support exports (CSV/Parquet), APIs, dashboards, and ML-ready datasets.

Canonical entity list (minimum)

- Companies
- Founders
- Investors
- Funding rounds
- Countries
- Sectors
- Policies
- Reports (internal & external)
- Deals
- Partnerships
- Acquisitions

Ingestion principles

- Every story -> one or more database actions: create new entity, update existing record, or add a new relation (e.g., company X raised round Y).
- Source-first: when extracting a fact, always record the source URL, date accessed, snapshot reference, and the shortMethodology block used in the brief.
- Single source-of-truth: each entity has a canonical record stored in the database; editorial artifacts should reference (by canonical ID) the entity rather than re-creating it inline.
- Conservative writing: only add facts to the DB that meet editorial sourcing rules (primary source or triangulated). If a claim is single-source, mark its confidence accordingly.

Provenance and versioning

- Record: created_at, updated_at, source_refs (list of source IDs/URLs), source_snapshots (file hashes or permalinks), author, editor, and confidence level.
- Versioning: adopt immutable snapshots for each major update (store diffs or full snapshots). Keep a changelog per entity with timestamped entries describing updates and source evidence.

Identifiers & canonical keys

- Use GUIDs (UUIDv4) as internal canonical IDs (company_id, founder_id, investor_id, etc.).
- Also maintain human-friendly slugs for display (e.g., company-slug: "flutterwave-ng").
- External IDs: where available, store external identifiers (CRS, ORCID, ISIN, company registry numbers, AngelList/Crunchbase IDs) to aid cross-referencing.

Access & governance

- Sensitive data: avoid PII unless explicit consent and clear public interest; follow privacy rules in Research Methodology.
- Access tiers: maintain a clear ACL (public snapshot exports, internal-only metadata, paid-tier APIs).
- Ownership: assign a data steward to own the overall DB and per-entity owners for critical collections.

Storage & format recommendations

- Short term: canonical CSV/Parquet files stored in 07_Data/ with a Sources_Registry mapping. Keep generated snapshots in /data_snapshots/ with timestamps.
- Mid term: a managed relational DB (Postgres) or a document DB (Postgres + JSONB or Mongo) with an API layer for product features.
- Long term: a data warehouse (Snowflake / BigQuery) for analytics and the AI platform.

Linking editorial to data

- Every published brief must include a "DB actions" section listing the changes it makes to the Africa Database (e.g., "Add company: ABC Ltd; Add funding round: XYZ; Update country policy: tariff change on 2026-06-01").
- Maintain a simple ingestion script/process that reads DB actions from brief metadata and queues them for review and insertion.

Next steps

1. Create a Sources Registry (07_Data/Sources_Registry.md) to track snapshots, licenses, and access notes.
2. Define the detailed data model (see 07_Data/Data_Model.md) and a Taxonomy (07_Data/Taxonomy.md).
3. Build a minimal ingestion pipeline (manual CSV → canonical table → review) and iterate toward automation.
