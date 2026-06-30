# Prompt Library

Purpose

A living library of high-quality prompt templates and patterns used across editorial workflows, RAG, and the assistant. Prompts should be versioned and tested against a small suite of canonical Q&A pairs.

General rules

- Include an instruction header: goal, tone (neutral/decision-focused), and output format.
- Instruct the model to always produce a short "Sources" section with inline links corresponding to retriever results.
- Limit generation length and require a confidence score or label (High / Medium / Low) per assertion.
- Add a final step: "If you are unsure, say 'I don't know' and list recommended next steps to verify." Avoid invented facts.

Core prompt templates

1) Short answer + sources (RAG)
Instruction:
You are an evidence-first intelligence assistant. Using the provided source documents (numbered), answer the user's question in 3–6 sentences. Provide a concise decision recommendation. After the answer, list the sources used by number with URL and publication date. Label any inference as "Opinion".
Output format:
- Answer (3–6 sentences)
- Recommendation (1 sentence)
- Sources:
  1. [Title] (URL) — date
  2. ...

2) Generate DB actions from brief (Extraction)
Instruction:
Given the featured brief and its sources, extract structured DB actions in JSON: a list of entities to create/update (company, funding_round, policy, partnership). For each action include: action_type (create/update), entity_type, canonical_fields, source_refs (list of source_ref_ids or URLs), confidence (high/medium/low). Only include actions supported by sources.
Output format: JSON array.

3) Fact-check assistant
Instruction:
You are a fact-check assistant. Given a candidate claim and a set of sources, indicate whether the claim is: Verified (supported by source), Contradicted (source says otherwise), or Unverifiable (no supporting evidence). Provide the exact quote or datapoint and the source citation.
Output format: JSON with {claim, verdict, evidence: [{quote, source_url, location}], confidence}

4) Taxonomy classifier
Instruction:
Classify the entity/text into taxonomy tags. Provide one primary sector and up to 3 secondary tags from the taxonomy list. If uncertain, return "sector: other" and a short reason.
Output format: JSON {primary_sector, secondary_sectors: [], confidence}

5) Brief summarizer (500 words → 150 words)
Instruction:
Summarize the following brief to 150 words, preserving all source citations inline (use [n] numbering based on sources provided). Keep tone neutral and decision-focused.
Output: 150-word summary + Sources mapping.

Prompt engineering & testing

- Store prompt templates under 08_AI/prompt_versions/ with metadata: creation_date, author, model tested with, and sample inputs/outputs.
- Maintain a regression test suite (a small file with canonical Q&A) to detect prompt drift after model or template updates.

Prompt examples (short)

- Investor diligence checklist prompt: "Given sources [1..n] about Company X, list 5 key diligence questions an investor should ask and what evidence would satisfy each question."
- Policy explain prompt: "Summarize the policy change and list the direct implications for a fintech company operating in country Y."


