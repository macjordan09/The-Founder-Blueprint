# Data Model

Purpose

This file defines the canonical schema for the core entities we will capture. Fields are intentionally practical: enough structure to join and query, while keeping flexibility for additional attributes.

Storage note: field types are shown in parentheses. Choose Postgres (relational) with JSONB columns for flexible attributes, or a columnar store for analytics exports.

1) Companies
- company_id (UUID) — canonical internal id
- name (string)
- slug (string)
- country_id (FK) — primary country of registration/operation (ISO3)
- headquarters_city (string)
- founded_date (date) — null if unknown
- status (enum: active / inactive / acqui/red / closed)
- short_description (text)
- sectors (array of sector_ids)
- website (url)
- external_ids (json) — {crunchbase: id, angelList: id, rgt_company_number: ...}
- founders (array of founder_ids)
- last_known_funding_round_id (FK)
- revenue_range (string) — if sourced
- employee_count (int) — if sourced
- source_refs (array of source_ref_ids)
- created_at, updated_at

2) Founders
- founder_id (UUID)
- full_name (string)
- slug (string)
- known_titles (array) — e.g., ["CEO", "Co-founder"]
- companies_founded (array of company_ids)
- country_of_residence (ISO3)
- external_ids (json) — {linkedin: url, orcid: ...}
- bio_short (text)
- source_refs, created_at, updated_at

3) Investors
- investor_id (UUID)
- name (string)
- type (enum: individual / vc / fund / angel_group / corporate)
- country_id (ISO3)
- typical_stage (enum: pre-seed / seed / seriesA / growth)
- portfolio_companies (array of company_ids)
- external_ids (json)
- source_refs, created_at, updated_at

4) FundingRounds
- round_id (UUID)
- company_id (FK)
- announced_date (date)
- round_type (enum: pre-seed / seed / series A / B / C / growth / debt / grant)
- amount (numeric)
- currency (string, ISO4217)
- lead_investor_id (investor_id)
- participating_investors (array of investor_ids)
- funding_stage_tags (array)
- source_refs, created_at, updated_at

5) Countries
- country_id (ISO3)
- name (string)
- iso2 (string)
- iso3 (string)
- region (string)
- population (numeric)
- gdp (numeric)
- primary_data_sources (array of source_refs)
- created_at, updated_at

6) Sectors
- sector_id (UUID)
- name (string)
- parent_sector_id (nullable)
- tags (array)
- created_at, updated_at

7) Policies
- policy_id (UUID)
- title (string)
- country_id (ISO3)
- effective_date (date)
- summary (text)
- full_text_url (url)
- policy_type (enum: regulation / tax / subsidy / trade / labor / data_privacy / other)
- status (proposed / enacted / repealed)
- source_refs, created_at, updated_at

8) Reports
- report_id (UUID)
- title (string)
- authors (array)
- publish_date (date)
- summary (text)
- dataset_refs (array)
- brief_id (if internal brief)
- source_refs, created_at, updated_at

9) Deals
- deal_id (UUID)
- parties (array of company_ids or investor_ids)
- deal_type (partnership / commercial / JV / procurement)
- announced_date (date)
- value (numeric) — if reported
- terms (text)
- source_refs, created_at, updated_at

10) Partnerships / Acquisitions
- partnership_id / acquisition_id (UUID)
- acquirer_id (company_id or investor_id)
- target_id (company_id)
- announced_date (date)
- value, terms, source_refs, created_at, updated_at

Reference tables
- source_refs
  - source_ref_id (UUID)
  - url (string)
  - title (string)
  - publisher (string)
  - accessed_date (date)
  - snapshot_path / file_hash
  - license
  - notes

- tags
  - tag_id, name, description, taxonomy_path

Relationships and joins

- Companies ↔ Founders (many-to-many)
- Companies ↔ FundingRounds (one-to-many)
- FundingRounds ↔ Investors (many-to-many)
- Companies ↔ Deals / Partnerships (many-to-many)
- Policies ↔ Countries (many-to-one)

Examples (illustrative minimal records)

Company sample (JSON-like)
{
  "company_id": "uuid-1234",
  "name": "Example Fintech Ltd",
  "slug": "example-fintech-ng",
  "country_id": "NGA",
  "founded_date": "2018-06-01",
  "sectors": ["sector-payments"],
  "founders": ["founder-1", "founder-2"],
  "source_refs": ["src-45", "src-67"]
}

Funding round sample
{
  "round_id": "uuid-5678",
  "company_id": "uuid-1234",
  "announced_date": "2025-11-12",
  "round_type": "series A",
  "amount": 5000000,
  "currency": "USD",
  "lead_investor_id": "investor-1",
  "source_refs": ["src-90"]
}

Implementation notes

- Normalize core join tables but keep a denormalized view for analytics exports to speed up dashboard queries.
- Index commonly queried fields (company slug, country_id, round dates).
- Store raw JSON of original scraped/extracted payloads to aid audits and debugging.
- Provide a CHANGELOG table capturing who changed what and why (with source_refs for each change).
