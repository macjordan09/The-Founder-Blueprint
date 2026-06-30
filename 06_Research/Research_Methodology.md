# Research Methodology

Purpose

This document defines how we collect, evaluate, and present evidence. The goal is reproducible, defensible intelligence that decision-makers can trust.

Evidence hierarchy (preferred → less preferred)

1. Primary sources: official filings, government statistics, company financials, regulatory texts, raw datasets from authoritative sources.
2. Peer-reviewed research and validated academic datasets.
3. Reputable institutional reports (multilaterals, large consultancies, reputable NGOs) when methodology is transparent.
4. Independent local sources and expert interviews (preferably recorded or with written notes and provenance).
5. High-quality journalism from established outlets (useful for leads but require triangulation).
6. Social posts, rumours, or anonymous tips (use only as leads and never as final evidence).

Data provenance & reproducibility

- Record: source URL, author, publication date, dataset name, license, and any transformation steps taken (cleaning, aggregation, assumptions).
- Version control: save copies or snapshots of critical datasets and include file hashes or permalinks where possible.
- Code & analysis: store code/notebooks used to produce charts or figures in a linked repository (public or private) with instructions to reproduce.

Interview best practices

- Consent: obtain explicit consent for attribution; if the source requests anonymity, record the reason and a short provenance note (role, organization, time).
- Note-taking: capture direct quotes, timestamps, and context. Add interviewer name and date.
- Sampling: document how interview subjects were selected and any biases this introduces.

Collection methods

- Datasets: prefer API/public download where available; document queries used, date ranges, and filtering.
- Reports: link to full report and cite the specific page/section used.
- Alerts & feeds: maintain a curated list of RSS, Google alerts, and data feeds that researchers can use for sourcing.

Analysis & uncertainty

- Triangulation: corroborate claims across at least two independent sources when possible.
- Uncertainty quantification: report confidence qualitatively (High / Medium / Low) and quantitatively where feasible (confidence intervals, margin of error).
- Avoid over-precision: when source data is coarse or estimated, present ranges and clearly state assumptions.

Metrics & definitions

- Create a master metrics glossary in 07_Data that defines every metric used in briefs (e.g., "monthly active users" definition and data source).

Templates for methodology sections

Include a shortMethodology block with:
- Data sources: list + links
- Date ranges
- Transformations / filters applied
- Key limitations and biases

Example shortMethodology

Data sources: National telecom regulator (mobile subscriptions by month, 2018–2025), World Bank WDI (GDP), company press releases for funding rounds.
Date range: Jan 2018–Mar 2026
Transformations: aggregated monthly subscriptions to quarterly; excluded outlier months where regulator data was incomplete.
Limitations: telecom regulator updates lag by ~30 days; company funding rounds are subject to confirmation from filings.

Governance & ethics

- Respect privacy and data-use licenses.
- Avoid publishing personally identifiable information unless consented and necessary for the public interest.
- Disclose conflicts of interest and funding sources for research.

Linking research to product

- Every featured brief must include the shortMethodology block and link to datasets and reproducible analysis where feasible.
- Store canonical datasets and metric definitions in 07_Data for reuse and to reduce duplicated effort.
