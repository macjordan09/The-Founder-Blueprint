# 90-Day Execution Plan

Purpose

A focused, timeboxed plan to move from concept to initial product-market validation, audience growth, and a minimal data foundation. Prioritize creating repeatable processes for editorial, data ingestion, and customer research so the operation can scale after day 90.

North-star for 90 days

- Publish a repeatable, trust-first Africa Intelligence Brief (10 issues) and validate core audience engagement among investors, founders, and diaspora professionals.
- Ship Founder Blueprint v1 (repo + templates) and a landing page with newsletter signup.
- Build a minimal, versioned Africa Database capturing companies, founders, investors, and funding rounds from published briefs and pilot interviews.

Quarter goals (90 days)

1. Product & Editorial
- Complete Founder Blueprint v1 (core docs, templates, featured brief template) — DONE.
- Publish 10 newsletter issues (weekly cadence) and collect feedback.
- Publish 3 deep-dive featured briefs (500–1,000 words each) with full sources and DB actions.
- Launch Week 0 and iterate format for first 4 issues.

2. Data & Infrastructure
- Create Africa Database initial schema and sources registry — DONE (Data model & taxonomy committed).
- Ingest at least 50 canonical source snapshots and create 30 minimal DB records (companies/founders/rounds) tied to briefs.
- Implement a manual ingestion workflow (CSV/Notion → review → DB) and a simple change-log for entity updates.

3. Customer & Research
- Interview 10 African founders or investors (or a mix) and log notes against problem hypotheses.
- Run outreach to seed 200–500 initial newsletter signups from our networks (investors, founders, diaspora).
- Measure time-to-decision and trust metrics via a short survey to pilot users.

4. Growth & Brand
- Create basic landing page + signup (static, one-file ready to host).
- Define brand architecture (name lock, logo ideas, messaging pillars) and commit to 04_Brand assets.
- Test audience response through targeted outreach and A/B subject-line tests for the newsletter.

Week-by-week plan

Weeks 0–2 (Setup & Launch)
- Finalize Week 0 newsletter and landing page; publish Issue 0.
- Seed outreach to 50–100 high-priority contacts (investors, founders, diaspora). Track responses.
- Begin interview scheduling for 10 target stakeholders.
- Ingest 10 source snapshots into Sources_Registry and create first 10 DB records.

Weeks 3–6 (Iterate & Scale Content)
- Publish Issues 1–4; iterate format based on open/click and qualitative feedback.
- Publish at least 1 deep-dive featured brief; map DB actions and add to ingest queue.
- Run initial sponsor outreach for newsletter sponsorship pilot.
- Complete 5 stakeholder interviews; synthesize common themes into 02_Problem/Customer_Research.md updates.

Weeks 7–10 (Productize & Monetize Tests)
- Publish Issues 5–8; ramp outreach and referral asks in each issue.
- Publish 1–2 additional deep-dive briefs with reproducible methodology and datasets.
- Pilot first paid offer (paid briefing or premium brief) with 1–2 early customers.
- Reach 200–500 subscribers target via continued outreach and syndication.

Weeks 11–13 (Consolidate & Measure)
- Publish Issues 9–10 and compile a 90-day retrospective brief on lessons learned and top signals.
- Complete 10 interviews; publish a synthesis article summarizing insights.
- Reach ingestion target: 30 DB records and 50 snapshots; document the manual ingestion process for handoff.
- Review metrics and decide next product moves (membership pilot, data subscription, AI prototype).

Owners & roles (recommended initial team)

- Founder / Editor (owner): overall strategy, final editorial signoff, outreach to primary cohort.
- Researcher: source collection, fact-checking, DB action proposals, interview note-taking.
- Data steward / Engineer (part-time): set up Sources_Registry, CSV templates, and ingestion scripts.
- Designer / Branding (contract): landing page, newsletter template, brand assets.

Deliverables (by day 90)

- 10 newsletter issues published and archived in 02_Problem/samples/ or Resources/newsletter_archive/.
- 3 featured briefs with full sources and DB actions.
- Landing page + signup live (HTML + copy in repo).
- Africa Database: taxonomy.yaml, Data_Model.md, Sources_Registry.md, and ~30 seeded records (CSV snapshots).
- 10 stakeholder interview notes stored in 02_Problem/interviews/ with provenance.
- Metrics dashboard (simple CSV or Notion board) tracking subscribers, opens, clicks, interviews completed, DB records created, and paid pilot conversions.

Success metrics (end of 90 days)

- Publish consistency: 10 issues (weekly) with average open rate >= 30% and CTR >= 8% (benchmarks to iterate).
- Audience growth: 200–500 engaged subscribers from target cohorts.
- Research output: 3 reproducible featured briefs and 30 DB records created from briefs/interviews.
- Customer validation: 10 interviews completed; >= 3 pilot users express willingness to pay for a premium brief or advisory.
- Data foundation: Sources_Registry populated with 50 snapshots and 30 DB records; manual ingestion process documented.

Risks & mitigations

- Risk: inconsistent publishing cadence. Mitigation: batch-produce 2–3 issues in advance and recruit 2–3 contributors to share load.
- Risk: low early engagement. Mitigation: hyper-target outreach to trusted networks and request introductions; iterate subject lines and preview copy.
- Risk: sourcing gaps for DB. Mitigation: prioritize high-signal, public sources (regulator notices, company announcements) and mark single-source items with confidence flags.
- Risk: monetization harms trust. Mitigation: keep editorial independence, clearly label sponsored content, and separate sponsorship ops from editorial control.

Dependencies

- Landing page hosting and email provider account (Mailchimp / ConvertKit / Buttondown).
- Initial outreach list (founder/investor/diaspora contacts).
- Basic snapshot storage (S3 or repo folder for small scale) and a Sources_Registry.
- Lightweight tooling (CSV templates, Notion/Google Sheet for ingestion review).

Next immediate actions (I can do now)

1. Commit this 90-day plan to 12_Roadmap/90-Day.md on Claude-Worlspace.
2. Draft the Week 0 newsletter and landing page copy and commit samples to 02_Problem/samples/ and Resources/landing_page/.
3. Create Sources_Registry.md and seed with 10 snapshots for initial ingestion.
4. Draft the outreach email template for investor/founder/diaspora cohorts and an interview scheduling doc.

Tell me which of the immediate actions you'd like me to take next; I can commit the 90-day plan now if you say "Commit".