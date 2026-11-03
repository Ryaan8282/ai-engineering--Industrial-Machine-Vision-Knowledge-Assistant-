# Evaluation Criteria — Industrial Machine Vision Knowledge Assistant
**Version:** 1.0  
**Course:** AI Engineering — Topic 2 Lab  
**Scope:** Part B — Step B1: Define Evaluation Criteria  
**Based on:** `docs/week2_requirements.md` (Part A, Version 1.0)

> **Status:** Proposed V1 evaluation plan. Thresholds are acceptance targets for later testing, not measured results. Requirement IDs and existing targets are kept consistent with Part A.

## Part B — Evaluation Criteria Table

| Objective / Requirement ID | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Usefulness Threshold | User / Business Outcome |
|---|---|---|---|---|---|---|
| **O1 / NFR3** | **Retrieval relevance:** Relevant machine vision evidence is retrieved for supported questions. | Domain-specific capability | For **40 in-scope questions**, pre-identify at least one relevant passage in the approved documents. Check whether a relevant passage appears among the **top 5** retrieved results. | **Retrieval Hit@5:** proportion of questions with ≥1 relevant passage in the top 5. | **≥80% (≥32/40)** | Learners can access appropriate technical evidence instead of searching multiple documents manually. |
| **O3 / NFR2** | **Answer correctness:** Technical statements match the approved documents. | Domain-specific capability | Compare answers to **40 source-verified reference answers**, using the factual-correctness rubric in Part A; an answer passes only if its key factual claims agree with the sources. | **Correct response rate:** correct answers / 40 × 100%. | **≥80% (≥32/40)** | Students and beginner engineers receive sufficiently reliable explanations of machine vision concepts. |
| **O2 / FR3 / RAI2** | **Citation presence and support:** Answers provide checkable sources that support the stated facts. | Instruction-following capability | Examine the same **40 document-grounded answers** for a verifiable document title and link (page/section when available), and manually check whether the cited evidence supports their key claims. | **Citation presence rate**; **citation-support rate** (fully supported answers / 40 × 100%). | **100% presence (40/40); ≥90% support (≥36/40)** | Users can verify explanations and identify unsupported technical claims. |
| **O2 / FR4 / RAI1** | **Insufficient-evidence handling:** The assistant acknowledges information it cannot support from the approved corpus. | Instruction-following capability | Ask **20 questions that cannot be answered from the corpus**. Check for a clear statement of insufficient evidence without fabricated technical facts. | **Appropriate insufficient-evidence response rate:** appropriate responses / 20 × 100%. | **≥90% (≥18/20)** | Reduces the risk of learners relying on invented technical information. |
| **O3 / NFR1** | **Response latency:** Answers arrive within an acceptable interactive time. | Cost and latency | Measure end-to-end query-to-answer time for the **40 in-scope questions** in the same V1 test environment; calculate the 90th-percentile latency. | **p90 end-to-end response latency**, seconds. | **≤10 seconds** | Users can ask follow-up questions without excessive delay. |
| **O2 / FR5** | **Beginner-friendly clarity:** Answers explain specialist terms clearly without becoming difficult to follow. | Generation capability | A reviewer scores the same **40 in-scope answers** using the 1–5 clarity rubric below. A response passes clarity if it scores **4 or 5**. Assess factual accuracy separately under NFR2. | **Clarity pass rate:** responses rated ≥4/5 divided by 40 × 100%. | **≥80% (≥32/40)** *— new Part B target for FR5* | Learners can understand important concepts without extensive prior machine vision knowledge. |
| **O3 / RAI3** | **Information recency transparency:** Source dates and uncertainty about currentness are communicated appropriately. | Instruction-following capability | Review metadata for **all indexed documents** and ask **10 date-sensitive questions**. Check whether every available source publication/revision date is recorded, and whether each date-sensitive answer avoids unsupported claims of being current. | **Available-date metadata coverage**; **appropriate recency-warning rate**. | **100% of available dates recorded; 100% of 10 questions qualified appropriately** | Users can distinguish documented knowledge from unverified claims about the latest technology. |

## Optional Human-Judgement Rubric — Answer Clarity (FR5)

| Score | Description |
|---|---|
| **1 — Very unclear** | Difficult to understand; key terms are unexplained. |
| **2 — Unclear** | Heavy use of jargon; explanation is hard for a beginner to follow. |
| **3 — Adequate** | Main idea is understandable, but important terms or relationships need clearer explanation. |
| **4 — Clear (Pass)** | Well-organized, beginner-friendly explanation; important technical terms are explained. |
| **5 — Very clear (Pass)** | Clear and concise explanation with useful structure or simple examples where appropriate. |

**Evaluation-set note:** The 40 in-scope questions are reused across retrieval, correctness, citation, clarity and latency evaluations to maintain consistency. The 20 insufficient-evidence questions and 10 date-sensitive questions are separate targeted sets. **No evaluation has been performed yet.** The clarity threshold is newly specified here because FR5 in Part A described the expected behaviour but did not assign a numeric threshold.

## Part B Reflection

**Which evaluation criterion is most important for determining whether the AI application will be useful to its intended users? Why?**

**Answer correctness (O3 / NFR2)** is the most important because students and beginner engineers use the assistant to learn technical concepts. Clear or fast answers are not useful if their factual explanations are wrong. **Citation support (FR3 / RAI2)** is also essential because it enables users to verify the information against the approved documents.
