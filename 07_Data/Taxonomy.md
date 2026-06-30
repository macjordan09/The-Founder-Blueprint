# Taxonomy

Purpose

A shared taxonomy ensures consistent labeling across briefs, the database, newsletters, and product features. It enables reliable aggregation and cross-issue analysis.

Core taxonomy components

1. Country codes
- Use ISO 3166-1 alpha-3 (e.g., NGA, KEN, ZAF). Store iso2 as needed (NG, KE, ZA).

2. Sector taxonomy (high → low)
- Tech
  - Fintech
  - Healthtech
  - Edtech
  - Agritech
  - Mobility & Logistics
  - Marketplaces
  - SaaS / B2B Platforms
- AI & Data
  - Models & Infrastructure
  - Applied AI (health, finance, agriculture)
- Infrastructure
  - Telecom
  - Energy (grid, renewables)
  - Transport & Logistics
- Manufacturing
  - FMCG production
  - Light manufacturing
- Finance & Capital
  - VC & PE
  - Banks & Payments
  - Remittances / Diaspora capital
- Public Sector & Policy
  - Digital government
  - Regulation & compliance
  - Trade & tariffs
- Other (use tags for emergent categories)

3. Funding stage tags
- pre-seed, seed, series_a, series_b, series_c, growth, debt, grant

4. Policy types
- Regulation, Tax policy, Subsidy, Trade policy, Labor policy, Data privacy, Licensing, Public procurement

5. Deal types
- equity_investment, grant, acquisition, partnership, joint_venture, procurement_contract

6. Confidence & provenance tags
- confidence_high (triangulated / primary sources)
- confidence_medium (single reputable secondary source)
- confidence_low (single local source / tip)
- provenance_primary, provenance_secondary, provenance_interview, provenance_dataset

7. Audience / Product tags (for newsletter & GTM)
- audience_investor, audience_founder, audience_diaspora, audience_corporate
- product_newsletter, product_report, product_membership, product_data

8. Temporal & geography tags
- time_period_quarter (e.g., Q2-2026)
- region (West Africa, East Africa, Southern Africa, North Africa, Central Africa)

Tagging rules & best practices

- Prefer controlled vocabulary values from the taxonomy for core fields (country_id, sector_id, policy_type, deal_type, funding_stage).
- Use free-form tags sparingly; map emergent tags back into the taxonomy quarterly.
- For sector classification, allow multiple sector tags per entity but require one primary sector.
- When tagging confidence, always capture the reason in the source_refs notes (e.g., "single-source: local press release, not company filing").

Mapping to newsletter categories

- Match the newsletter content pillars to sector and audience tags so briefs can be filtered and subscribers can opt-in to categories (e.g., AI, VC, Energy, Digital government, Diaspora capital).

Taxonomy governance

- Maintain taxonomy in a versioned YAML/JSON file in 07_Data/taxonomy.yaml for programmatic use.
- Quarterly review: reconcile new tags, add parent sectors, and archive unused tags.
- Owner: assign a taxonomy steward responsible for consistency and mapping across products.

Next steps

1. Commit taxonomy as a machine-readable file (07_Data/taxonomy.yaml) derived from this doc. 
2. Start tagging existing briefs and database entries using the taxonomy and record mismatches for review.
3. Build small utilities to validate incoming DB actions against the taxonomy (reject or flag unknown tags).
