# Automation

Purpose

Define how editorial, data, and AI workflows will be automated to scale content production and database population while preserving editorial control and auditability.

Automation goals

- Reduce manual extraction time for DB actions and source snapshotting.
- Automate signal detection (alerts) for high-priority topics (funding rounds, regulatory changes, M&A).
- Provide editor-facing tools to review and approve machine-suggested DB actions and brief drafts.

Key automation components

1. Ingestion & snapshotting
- RSS / feed watchers, targeted scrapers, and partner API connectors to pull candidate source documents.
- Snapshot storage: store HTML/PDF snapshots and compute file hashes; register snapshots in the Sources_Registry.

2. Retriever & vectorization
- For every snapshot and brief, extract text and metadata; create embeddings and index them in a vector store for RAG.
- Maintain a lightweight retriever that returns the top-k most relevant docs with relevance score and metadata (url, date, source_ref_id).

3. DB action extraction pipeline
- Use the "Generate DB actions" prompt to propose entity updates from briefs. Output JSON actions to a review queue.
- Provide an editor UI that shows the brief, the proposed DB actions, and source highlights; editors can accept/reject/modify actions.

4. Alerts & signal detection
- Rule-based alerts (e.g., new funding announcement with keywords + currency amounts) plus ML classifiers for emergent patterns.
- Deliver alerts to Slack/email and tag potential DB actions.

5. Drafting assistance
- Auto-generate first-pass summaries and short signal items from retrieved sources for editors to refine.
- Provide fillable featured brief templates pre-populated with extracted facts and suggested analysis bullets.

Human-in-the-loop governance

- Every automated DB action must be reviewed by an editor before insertion to the canonical DB unless confidence is High and source is primary and machine check passes.
- Log editor decisions for model retraining: accepted/rejected actions become training data.

MVP automation plan (first 90 days)

1. Build snapshotter + Sources_Registry and a small set of scrapers/feeds for high-priority sources (top news sites, regulator pages, press release feeds).
2. Implement a vector store + simple retriever and run RAG prompts to answer a small canonical question set; store results and evaluate.
3. Implement DB action extraction for funding rounds and companies; surface proposed actions in a Notion/CSV review queue for editors.

Operational considerations

- Monitoring & observability: track ingestion failures, retriever recall, model latency, and editor approval rates.
- Retraining loop: periodically fine-tune or refine prompts using accepted DB actions and corrected outputs.
- Cost control: monitor embedding and model usage costs; implement caching for common queries and pre-computed brief fragments.

Tech stack suggestions

- Scraping / ingestion: Python (requests, beautifulsoup, newspaper), Airbyte for connectors
- Snapshot storage: S3-compatible storage with versioning
- Vector store: FAISS (self-hosted) or Pinecone/Weaviate for managed option
- Models: OpenAI / Anthropic for prototype; evaluate open models (Llama-like) for cost-sensitive production
- Orchestration: Airflow / Prefect for pipelines, lightweight web UI for editor review (Flask/FastAPI + simple React)

Security & access

- Protect API keys and rate-limit external access.
- Implement role-based access in the editor UI (researcher, editor, approver).
- Encrypt snapshots and backups and maintain retention policies aligned with licenses.

Metrics to monitor

- Editorial time saved per brief (hours)
- % of DB actions auto-proposed vs accepted
- Retriever recall on canonical Q&A (test set)
- Mean editor review time per DB action
- Cost per published brief (compute + human)

Next steps I can implement

- Commit these AI files to the repo (I’m ready to push).
- Draft the initial prompt regression test suite and a small set of canonical Q&A pairs for evaluation.
- Create a simple snapshotter script and Sources_Registry template to start ingesting.
