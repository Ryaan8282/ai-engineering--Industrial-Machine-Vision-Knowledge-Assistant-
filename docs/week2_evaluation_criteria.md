# Evaluation Criteria — Industrial Machine Vision Knowledge Assistant
**Version:** 1.1 — selected-source edition  
**Course:** AI Engineering — Topic 2 Lab  
**Scope:** Part B — Step B1: Define Evaluation Criteria  
**Based on:** `docs/week2_requirements.md` (Part A, Version 1.0)

> **Status:** Proposed V1 evaluation plan. Thresholds are acceptance targets for later testing, not measured results. Requirement IDs and existing targets are kept consistent with Part A.

## Part B — Evaluation Criteria Table

| Objective / Requirement ID | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Usefulness Threshold | User / Business Outcome |
|---|---|---|---|---|---|---|
| **O1 / NFR3** | **Retrieval relevance:** Relevant machine vision evidence is retrieved for supported questions. | Domain-specific capability | For **40 in-scope questions supported by SRC-01/SRC-02**, pre-identify at least one relevant page-anchored passage in the approved documents. Check whether a relevant passage appears among the **top 5** retrieved results. | **Retrieval Hit@5:** proportion of questions with ≥1 relevant passage in the top 5. | **≥80% (≥32/40)** | Learners can access appropriate technical evidence instead of searching multiple documents manually. |
| **O3 / NFR2** | **Answer correctness:** Technical statements match the approved documents. | Domain-specific capability | Compare answers to **40 reference answers verified against SRC-01/SRC-02**, using the 0/1 factual-correctness rubric below; an answer passes only if its key factual claims agree with the sources. | **Correct response rate:** correct answers / 40 × 100%. | **≥80% (≥32/40)** | Students and beginner engineers receive sufficiently reliable explanations of machine vision concepts. |
| **O2 / FR3 / RAI2** | **Citation presence and support:** Answers provide checkable sources that support the stated facts. | Instruction-following capability | Examine the same **40 document-grounded answers** for a verifiable document title and link (page/section when available), and manually check whether the cited evidence supports their key claims. | **Citation presence rate**; **citation-support rate** (fully supported answers / 40 × 100%). | **100% presence (40/40); ≥90% support (≥36/40)** | Users can verify explanations and identify unsupported technical claims. |
| **O2 / FR4 / RAI1** | **Insufficient-evidence handling:** The assistant acknowledges information it cannot support from the approved corpus. | Instruction-following capability | Ask **20 questions that cannot be adequately answered using SRC-01/SRC-02**. Check for a clear statement of insufficient evidence without fabricated technical facts. | **Appropriate insufficient-evidence response rate:** appropriate responses / 20 × 100%. | **≥90% (≥18/20)** | Reduces the risk of learners relying on invented technical information. |
| **O2 / FR4** | **Out-of-scope handling:** Requests beyond educational document QA receive an appropriate limitation or refusal. | Instruction-following capability | Test **10 clearly out-of-scope requests** (e.g., direct machine-operation instructions or image-defect classification). Record whether each response declines the unsupported action and appropriately redirects to the educational scope. | **Out-of-scope handling success rate:** appropriate refusals/redirects / 10 × 100%. | **≥90% (≥9/10)** — *additional criterion to test FR4’s separate scope boundary* | Reduces the risk of treating an educational assistant as industrial operational guidance. |
| **O3 / NFR1** | **Response latency:** Answers arrive within an acceptable interactive time. | Cost and latency | Measure end-to-end query-to-answer time for the **40 in-scope questions** in the same V1 test environment; calculate the 90th-percentile latency. | **p90 end-to-end response latency**, seconds. | **≤10 seconds** | Users can ask follow-up questions without excessive delay. |
| **O2 / FR5** | **Beginner-friendly clarity:** Answers explain specialist terms clearly without becoming difficult to follow. | Generation capability | A reviewer scores the same **40 in-scope answers** using the 1–5 clarity rubric below. A response passes clarity if it scores **4 or 5**. Assess factual accuracy separately under NFR2. | **Clarity pass rate:** responses rated ≥4/5 divided by 40 × 100%. | **≥80% (≥32/40)** *— new Part B target for FR5* | Learners can understand important concepts without extensive prior machine vision knowledge. |
| **O3 / RAI3** | **Information recency transparency:** Source dates and uncertainty about currentness are communicated appropriately. | Instruction-following capability | Review metadata for **all indexed documents** and ask **10 date-sensitive questions**. Check whether every available source publication/revision date is recorded, and whether each date-sensitive answer avoids unsupported claims of being current. | **Available-date metadata coverage**; **appropriate recency-warning rate**. | **100% of available dates recorded; 100% of 10 questions qualified appropriately** | Users can distinguish documented knowledge from unverified claims about the latest technology. |
| **O3 / NFR4** | **Document update time:** An approved source can be added or replaced without rebuilding the entire application. | Cost and latency | Run **3 controlled approved-document add/replace trials** in the same environment. Time each trial until the changed document becomes searchable; verify a retrieved hit and updated provenance. | **Time to searchable update** (minutes per trial); successful updated-source retrieval. | **≤15 minutes in each of 3 trials** — *aligned to Part A NFR4* | The knowledge base can incorporate new reference material without expensive rework. |

## Factual-correctness scoring rule (NFR2)

Score each answer **1 (pass)** only when the key factual statements accurately reflect the relevant passages in SRC-01/SRC-02 and the answer does not introduce a material unsupported factual claim. Otherwise score **0 (fail)**. An explicit, justified limitation is evaluated under FR4/RAI1 rather than counted as correct for an in-scope answerable question. Use a human reviewer to adjudicate borderline claims. This is a **planned rubric**, not a completed assessment.

## Optional Human-Judgement Rubric — Answer Clarity (FR5)

| Score | Description |
|---|---|
| **1 — Very unclear** | Difficult to understand; key terms are unexplained. |
| **2 — Unclear** | Heavy use of jargon; explanation is hard for a beginner to follow. |
| **3 — Adequate** | Main idea is understandable, but important terms or relationships need clearer explanation. |
| **4 — Clear (Pass)** | Well-organized, beginner-friendly explanation; important technical terms are explained. |
| **5 — Very clear (Pass)** | Clear and concise explanation with useful structure or simple examples where appropriate. |

**Evaluation-set note:** The **40 in-scope questions** are grounded in the two selected PDFs and reused across retrieval, correctness, citation, clarity and latency evaluations to maintain consistency. The 20 insufficient-evidence questions, 10 out-of-scope requests and 10 date-sensitive questions are separate targeted sets; three document update trials measure NFR4. **No evaluation has been performed yet.** The clarity and out-of-scope thresholds are Part B evaluation decisions because FR5 and FR4 define behaviours without numerical targets in Part A. NFR4 retains its existing ≤15-minute target.

## Part B Reflection

**Which evaluation criterion is most important for determining whether the AI application will be useful to its intended users? Why?**

**Answer correctness (O3 / NFR2)** is the most important because students and beginner engineers use the assistant to learn technical concepts. Clear or fast answers are not useful if their factual explanations are wrong. **Citation support (FR3 / RAI2)** is also essential because it enables users to verify the information against the approved documents.


## Testing and Scoring Protocol (planned; not yet executed)

1. **Prepare ground truth:** For each of the 40 in-scope questions, identify a source-verified reference answer and one or more relevant passages in the approved documents **before** running the assistant. Separate definitions, explanations and comparisons in the test set.
2. **Record retrieval and answers:** Save the top five passage IDs, cited source title/URL/page or section (where available), complete generated answer, start and end time, and a test-set version. Do not infer correctness from citation presence alone.
3. **Score consistently:** Hit@5 passes if at least one pre-annotated relevant passage occurs in the top five; correctness passes only if key technical claims agree with the source; citation support passes only if the cited passages support key claims; clarity passes at rubric scores of 4 or 5.
4. **Check exceptional cases:** Score 20 questions with insufficient corpus evidence separately from 10 out-of-scope requests; a response that invents operational advice is not a successful refusal. Review 10 date-sensitive answers against the dates actually recorded in the corpus.
5. **Test updates:** For each of three add/replace trials, record start time, finish time, source metadata and proof that the new or replaced document is retrieved from the updated index.
6. **Compute thresholds:** 40-item tests use 32/40 for 80%, 36/40 for 90%, and 40/40 for 100%; 20-item tests use 18/20 for 90%; 10-item out-of-scope tests use 9/10 for 90%. The p90 latency is calculated across the 40 end-to-end durations. **All are planned tests, not results.**

## PDF-bounded test-set design (planned, not conducted)

- **40 answerable in-scope prompts:** sample across optical illumination, image acquisition, image processing/inspection, and deep-learning-based inspection. Each must have a verified source passage and a reference answer from the approved PDFs; do not force 10 questions per topic if the documents cannot support them.
- **20 insufficient-evidence prompts:** deliberately ask for details not established in the two PDFs (e.g., unsupported technical specifications or a detailed AOI-versus-AXI comparison, if unavailable). Correct handling requires an explicit limitation rather than fabrication.
- **10 out-of-scope prompts:** request direct industrial machine operation, live product inspection, safety-critical process decisions, or unrestricted web browsing. Correct handling is refusal or scoped redirection.
- **10 date-sensitive prompts:** ask about the 'latest' equipment or current industrial state of the art. Correct handling uses the **online 2021 / journal 2022** and **2024** source dates and does not claim that the static corpus is up to date.
- **3 update trials:** add or replace an approved document and measure time until newly indexed evidence is retrievable. These trials require a future implementation; they have not been run.

**Important:** The evaluation assesses a **knowledge assistant**, not the accuracy of defect detectors described in the papers. The papers' inspection F1 scores or classification accuracies are **not** scores for this RAG project.
