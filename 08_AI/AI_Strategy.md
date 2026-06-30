# AI Strategy

Vision

Build an intelligence assistant that answers questions about African innovation, capital, technology, policy, and business using our verified, versioned Africa Database and editorial artifacts. The assistant should be trustworthy (source-tagged), decision-focused, and auditable — becoming the primary interface for subscribers and customers to ask multi-step, evidence-based questions.

Long-term product

- An AI-powered query assistant (chat + API) that returns concise, sourced answers, produces decision checklists, generates reproducible briefs, and surfaces provenance (source links, snapshots, method notes).
- Tighter product integrations: alerts, automated country/sector briefs, signals feeds, and a private-query API for enterprise customers.

Phased roadmap

Phase 0 — Foundations (0–3 months)
- Define data contracts and begin mapping editorial artifacts to DB actions.
- Build reproducible prompt templates and internal tooling for RAG (retrieval-augmented generation) experiments using local snapshots and brief metadata.
- Run internal pilots: answer 20 curated user questions and evaluate recall, faithfulness, and provenance.

Phase 1 — Productize RAG answers (3–9 months)
- Implement a lightweight RAG stack: vector store (FAISS/Pinecone), retriever, and prompt templates that inject retrieved sources into model prompts.
- Expose an internal QA endpoint for editors and pilot users; ensure every answer is accompanied by source_refs and confidence.
- Add human-in-the-loop verification workflows and a UI for editors to correct/add sources.

Phase 2 — Assistant & Workflows (9–18 months)
- Build a public-facing assistant (chat UI + enterprise API) that can:
  - Answer topic queries with source links.
  - Generate short featured briefs and DB actions automatically for editor review.
  - Produce decision checklists and investor due-diligence rubrics.
- Implement rate limits, usage tiers, and audit logs for paid customers.

Phase 3 — Platform & Automation (18+ months)
- Scale the assistant with continuous ingestion, automated tagging, and higher-quality ML models (fine-tuned on our brief corpus and validated Q&A pairs).
- Offer enterprise features: private dataset ingestion, advanced alerting, custom taxonomy mapping, and model explainability tools.
- Explore advanced monetization: per-query billing, SLAed APIs, and embedded intelligence inside partner workflows.

Data & model governance

- Source-first policy: the assistant must always cite primary or triangulated sources for major claims. If the answer relies on inference, label it clearly and provide supporting evidence.
- Model selection: start with widely-used LLMs (open or commercial) for prototyping; evaluate fine-tuning or retrieval-augmented fine-tuning once we have a corpus of labeled Q&A and briefs.
- Privacy & PII: do not surface unpublished PII. Respect consent from interviews and local experts; redact or anonymize as required.
- Auditability: store (question, retrieved docs, prompt, model response, user feedback) for every session to enable audits and continuous improvement.

Evaluation metrics

- Faithfulness / Hallucination rate: percent of assertions in answers that are verifiable in the cited sources.
- Source coverage: percent of answers that include at least one primary source.
- User trust: percent of pilot users rating answers as "trusted" or "highly reliable".
- Precision of DB actions: percent of automatically extracted DB actions that pass editorial review.
- Latency & availability for product SLAs.

Security & compliance

- API keys, role-based access control, and rate limits for paid tiers.
- Data licensing: ensure we have the right to index and serve any paid/third-party datasets used in responses.
- Legal: when offering investment-related advice, include disclaimers and limit the assistant to informational/educational outputs unless using paid advisory workflows.

Team & resourcing

- AI lead / ML engineer for model infra and fine-tuning
- Research engineer / data engineer for DB ingestion, vector store, and pipelines
- Editor / subject-matter reviewer to provide labeled Q&A and ground-truth
- Product manager for design of assistant workflows and enterprise features

Open questions to resolve early

- Which vector store / model vendor for production (Pinecone, Weaviate, FAISS + self-hosted)?
- Fine-tuning vs prompt-engineering tradeoffs given dataset size and privacy constraints.
- Pricing and throttling model for enterprise API access.


