# V1 Architecture, Architecture Decisions & Traceability — Industrial Machine Vision Knowledge Assistant
**Version:** 1.1 — selected-source edition  
**Course:** AI Engineering — Topic 2 Lab  
**Scope:** Part C (C1–C4)  
**Based on:** `docs/week2_requirements.md` (Part A) and `docs/week2_evaluation_criteria.md` (Part B)

> **Status:** Proposed conceptual V1 architecture. No system has been implemented or evaluated. Requirement metrics and thresholds are future acceptance targets, not observed results.

## C1 — Start with the Simplest Architecture

**Baseline:** Learner → Application Interface → Language Model Service → Answer.

This baseline can generate fluent responses, but it **cannot reliably satisfy** the project's document-grounding, retrieval, verifiable citation, insufficient-evidence, document-update, and recency-transparency requirements. Therefore, V1 adds only the capabilities justified below.

**Revised conceptual flow:** Learner → Application Interface → Scope Screening → Knowledge Retrieval → Evidence Sufficiency & Recency Checks → Language Model Service → Citation & Answer Checks → Answer with Sources / Appropriate Limitation.

**Knowledge preparation:** Approved Public Machine Vision PDFs **or approved document additions/replacements** → Document Ingestion & Source Metadata → Searchable Knowledge Index → Knowledge Retrieval. Updates pass through ingestion and provenance capture before reindexing.

**Evaluation:** A separate V1 evaluation point measures retrieval, accuracy, citation quality, clarity, insufficient-evidence handling, out-of-scope handling, recency behaviour, latency, and document-update time. It is not a production auto-grading system.

## C2 — Architecture Needs Derived from Requirements

| Requirement ID | What does the requirement need? | Architecture Response |
|---|---|---|
| **FR1 / FR2 / NFR3** | Answer and compare introductory industrial machine vision concepts using relevant approved evidence; Hit@5 ≥80%. | The two approved peer-reviewed PDFs (SRC-01 Ren et al., 2022; SRC-02 Hütten et al., 2024), document processing, a searchable index, and evidence retrieval (top-five results available for evaluation). |
| **FR3 / RAI2** | Verifiable source title and link, page/section where available; 100% citation presence and ≥90% supported answers. | Source provenance metadata attached to retrieved passages; citation formatting and evidence-support checks before displaying the answer. |
| **FR4 / RAI1** | Handle **two different** conditions: ≥90% appropriate replies on 20 corpus-unanswerable questions; ≥90% correct refusal/redirect on 10 out-of-scope requests (Part B additional criterion). | Query scope screening and evidence-sufficiency checking each route to an appropriate limitation response; they are evaluated separately. |
| **FR5** | Beginner-friendly explanations that explain technical terms without compromising accuracy. | Language model guidance for plain-language explanations, with final answer formatting and later human clarity review. |
| **NFR2** | Technically correct answers in ≥80% of 40 source-verified tests. | Grounded answer generation using retrieved passages; separate reference-answer evaluation and manual scoring. |
| **NFR1** | Interactive speed: p90 end-to-end latency ≤10 seconds over 40 in-scope questions. | A short query-to-answer path and an evaluation timer around the full interaction; no mandatory extra model calls. |
| **NFR4** | Approved PDFs must be added/replaced and searchable within 15 minutes in each of three trials. | **Both new and replacement documents enter the ingestion/metadata stage before the index is updated**; record timestamps and verify source retrieval. |
| **RAI3** | Preserve all available publication/revision dates; appropriately qualify all 10 date-sensitive test questions. | Capture source publication/revision metadata when available and perform recency/uncertainty checks before answering. |

## C3 — V1 Conceptual Architecture Diagram

**Diagram:** `docs/week2_architecture_v1.png` (also provided as editable `week2_architecture_v1.drawio`).

**Principal information flows**
1. The learner submits an English-language question through the application interface.
2. A scope control checks whether the request is educational and in the approved industrial machine vision domain. **Out-of-scope requests** lead to a limitation/refusal without querying the model for operational advice (FR4).
3. The **two approved source PDFs (SRC-01/SRC-02)**, including later approved additions/replacements, pass through **document ingestion and metadata extraction** before updating the searchable index. Retrieval then returns passages **with source title, link, page/section when available, and date metadata when available**.
4. Evidence and recency controls determine whether enough support exists and whether a time-sensitive answer needs a caveat. **Insufficient evidence** leads to an explicit limitation response (a different case from out-of-scope refusal).
5. The language model drafts a beginner-friendly technical explanation **only from retrieved evidence**.
6. Citation/answer checks ensure a traceable source is displayed and reject or qualify unsupported statements before a response is returned.
7. A separate, offline evaluation process later checks the performance targets defined in Parts A and B, including **10 out-of-scope tests and three document-update trials**; it does **not** imply the targets are already met.

**Boundary:** The system is an educational text question-answering assistant supported by exactly two initial peer-reviewed source PDFs. Detailed AOI/AXI coverage is not presumed and requires supporting passages. It does **not** inspect PCB images, control cameras or industrial machines, make manufacturing decisions, use private manuals, or browse the unrestricted live web.

## C4 — Architecture Decision Record (ADR)

| Decision | Requirement / Constraint | Alternatives Considered | Selected Option | Trade-off Accepted |
|---|---|---|---|---|
| **ADR-01: Use document-grounded knowledge retrieval** | FR1, FR2, NFR2, NFR3; public, verifiable sources. | Model-only answers; static keyword lookup; retrieved-document approach. | SRC-01/SRC-02 → document ingestion → searchable index → passage retrieval → grounded generation. | More document processing and index maintenance than model-only Q&A, in exchange for relevant and traceable evidence. |
| **ADR-02: Separate scope and evidence controls** | FR4, RAI1, RAI3; no unsupported technical or currentness claims. | Prompt instructions alone; one scope check only; explicit scope plus evidence/recency controls. | Scope screening before retrieval and evidence-sufficiency/recency checks after retrieval. | May refuse some answerable questions and adds processing, but reduces unsupported answers and false claims of currentness. |
| **ADR-03: Track source provenance and check citations** | FR3, RAI2; title/link and page/section when available; measurable support. | Unreferenced answers; append document links without passage tracking; passage-level source metadata. | Preserve provenance with retrieved passages and run citation/answer checks. | Extra metadata and validation effort; manual audits are still needed because a citation alone does not guarantee support. |
| **ADR-04: Keep ingestion repeatable and model-agnostic** | NFR4, NFR1; semester timeframe and restricted budget. | Hard-code fixed documents and rebuild; repeatable update flow and generic model service. | Replaceable approved-document ingest/index update and generic language model service. | Initial ingestion design work and possible update errors, but easier testing and updates without locking into one vendor. |

### Initial Requirements Traceability Matrix

| Objective | Requirement | Evaluation Criterion / Target | Architecture Element | Later Evidence (not yet collected) |
|---|---|---|---|---|
| **O1** | FR1, FR2, NFR3 | Relevant technical evidence; **Hit@5 ≥80% (≥32/40)**. | SRC-01/SRC-02, ingestion, searchable index, retrieval. | Annotated 40-question retrieval test and top-five passage results. |
| **O2** | FR3, RAI2 | **100% citation presence (40/40); ≥90% support (≥36/40)**. | Passage provenance; citation and answer check. | Citation audit for 40 grounded answers with source/claim verification. |
| **O2** | **FR4, RAI1** | **≥90% proper insufficient-evidence handling (≥18/20)**. | Evidence-sufficiency check; limitation response. | Results of 20 corpus-unanswerable questions. |
| **O2** | **FR4** | **≥90% appropriate out-of-scope handling (≥9/10)**. | Scope screening; refusal/redirect to the educational boundary. | Results of 10 out-of-scope requests. |
| **O2** | FR5 | **Clarity pass rate ≥80% (≥32/40)** under Part B's 1–5 rubric. | Language-model explanation guidance; answer formatting. | Human clarity scores for 40 answers (rating 4 or 5 passes). |
| **O3** | NFR2 | **Correct response rate ≥80% (≥32/40)**. | Evidence-backed generation and evaluation point. | Source-verified reference answers and a 40-question correctness rubric. |
| **O3** | NFR1 | **p90 latency ≤10 seconds**. | Efficient interaction path; end-to-end evaluation timer. | Timed results for the same 40 in-scope questions. |
| **O3** | **NFR4** | **≤15 minutes in each of 3 document-update trials**. | Approved update → ingestion/metadata → searchable index update. | Timestamped 3-trial document-add/replace log plus proof of retrieval from the updated index. |
| **O3** | RAI3 | **100% available dates recorded; 10/10 recency cases qualified appropriately**. | Publication/revision metadata; recency control; answer caveat. | Index metadata audit and responses to 10 date-sensitive questions. |

### Final V1 Architecture Review

- [x] Every major V1 component maps to at least one FR, NFR, RAI control, or evaluation need.
- [x] Public document sources, passage provenance, citation checks, scope/evidence/recency controls, and an evaluation point are represented.
- [x] No specific LLM, vector database, UI framework, guardrail product, or deployment service is locked in at the conceptual V1 stage.
- [x] No image defect detection, manufacturing operation, or unauthorized document use is added to the scope.
- [x] Part A IDs and Part B measures are used consistently; all thresholds remain proposed, not measured.

### Part C Reflection

**Which architecture decision involved the most important trade-off? Which requirement drove the decision, and what trade-off did you accept?**

**ADR-01 (document-grounded retrieval)** is the most important. FR1/FR2, NFR2/NFR3, and FR3/RAI2 require correct, relevant, checkable answers. I accept the added document-processing and indexing complexity because a model-only chatbot could not reliably provide evidence grounded in the approved machine vision documents.

### Reference documents (already identified in Part A)

- PCB manufacturing multimodal RAG chatbot (2026): https://doi.org/10.1016/j.array.2026.100881
- Document GraphRAG in manufacturing (2025): https://doi.org/10.3390/electronics14112102
- TechDocRAG for technical documents (2026): https://doi.org/10.3390/ai7050161

**Selected corpus note:** The two required public PDFs are now **supplied and verified as readable**: SRC-01 Ren et al. (2022, 31 pages) and SRC-02 Hütten et al. (2024, 38 pages). The unavailable Cognex guide is not used. The NI lighting website is not a counted PDF. Extraction, indexing, AI responses and measured evaluation have **not** yet been implemented. See `docs/week2_source_inventory.md`.

### How the selected knowledge corpus justifies V1 components

- **SRC-01** discusses a typical inspection chain (illumination → acquisition → processing/defect detection) and includes multi-column technical text, diagrams and illumination tables. This justifies structured extraction and source-page metadata, rather than sending unprocessed PDFs directly to an LLM.
- **SRC-02** synthesizes 196 automated-visual-inspection papers and includes tables, charts and sections on DL models and inspection tasks. This requires retrieval across long documents and a plain-English summarization capability.
- **Both** have fixed publication dates, so RAI3 recency caveats are necessary. They do not authorize broad claims about latest equipment or detailed AOI/AXI capabilities in the absence of source evidence.

The proposed application answers **text questions about industrial machine vision knowledge**. It does not perform real-time image analysis or train a defect detector.
