# Requirements Specification — Industrial Machine Vision Knowledge Assistant
**Version:** 1.1 — selected-source edition  
**Course:** AI Engineering — Topic 2 Lab  
**Scope:** Part A only (Sections 0–3)

> **Project status:** Proposed V1 requirements. The thresholds below are initial acceptance targets for later testing, not results already achieved.

## Section 0 — Project Framing & Application Scope Checkpoint (A0)

| Framing element | Refined project description |
|---|---|
| **Problem Evidence** | **Evidence 1:** Ren et al. (journal 2022; published online 2021) explain that machine-vision inspection depends on illumination, image acquisition, processing, and defect-analysis stages, making the technical workflow multidisciplinary ([SRC-01](https://doi.org/10.1007/s40684-021-00343-6), pp. 661–663). **Evidence 2:** Hütten et al. (2024) survey 196 open-access publications on deep learning for automated visual inspection and identify implementation challenges and varied inspection tasks ([SRC-02](https://doi.org/10.3390/asi7010011), pp. 1–5). These demonstrate that industrial machine vision has substantial, dispersed technical knowledge. They **do not** establish that student demand has been measured; the learner-facing gap is the proposed engineering application. |
| **Existing Approaches** | **1. Industrial machine-vision review (Ren et al., 2022):** Synthesizes lighting, acquisition, image-processing, and defect detection techniques; it is a reference document, not an interactive beginner Q&A tool ([SRC-01](https://doi.org/10.1007/s40684-021-00343-6)). **2. Deep-learning automated visual-inspection survey (Hütten et al., 2024):** Reviews approaches and applications across manufacturing and maintenance; it does not deliver source-cited conversational answers ([SRC-02](https://doi.org/10.3390/asi7010011)). **3. Document GraphRAG (2025):** Related work on structured retrieval for manufacturing document question answering, but more complex than the proposed modest V1 ([related work](https://doi.org/10.3390/electronics14112102)). These are background approaches, not claims that their authors tested our proposed application. |
| **Project / Engineering Gap** | Existing technical material spans several inspection stages and mixes accessible and advanced explanations. **Engineering opportunity (not a proven novel research gap):** a simple learner-oriented RAG assistant that retrieves from two approved, general academic PDFs, explains documented machine-vision concepts in plain English, and supplies verifiable passage-level citations with explicit evidence limitations. The application focuses on **knowledge access**, not improving defect-detection model accuracy. |
| **Objective O1** | To design a document-grounded AI assistant for industrial machine vision knowledge retrieval. |
| **Objective O2** | To develop a RAG-based question-answering system that provides understandable explanations with source citations. |
| **Objective O3** | To evaluate retrieval relevance, answer correctness, evidence grounding, response time and responsible behaviour. |
| **Intended Users** | Students learning industrial machine vision, beginner machine vision engineers and researchers exploring industrial inspection technologies. |
| **Supported Tasks** | Ask English-language technical questions; receive explanations about illumination modes, CCD/CMOS image acquisition, image preprocessing, traditional inspection approaches, defect detection/classification/localization/segmentation, and deep learning for industrial inspection **when supported by SRC-01/SRC-02**; request comparisons of documented concepts (e.g., bright-field versus dark-field lighting, conventional processing versus deep learning); receive original document titles, DOI links and page/section citations; receive a clear limitation message if the PDFs do not contain enough evidence. |
| **Information / Knowledge Domain** | **V1 approved knowledge scope:** Introductory industrial machine vision and automated visual inspection **as represented in the two selected peer-reviewed PDFs**, especially illumination, sensors/cameras, image acquisition, preprocessing, inspection algorithms, defect detection, and deep-learning methods. AOI and AXI are relevant terms from the Week 1 wider domain, but detailed AOI-versus-AXI explanations are **not guaranteed** by this limited corpus; the assistant must qualify or decline them if evidence is lacking. This is knowledge explanation, **not** execution of defect inspection. |
| **Operating Context** | Read-only educational/research prototype accessed through a simple conversational interface, using a curated collection of public technical documents. Intended for individual learning and technical reference, **not** production-line operation. |
| **Important Constraints** | One-semester timeframe; limited computing/API budget; English-language, read-only educational prototype; two actually supplied and checked open-access PDFs: **SRC-01 Ren et al. (2022), 31 pages** and **SRC-02 Hütten et al. (2024), 38 pages** (see source table and `docs/week2_source_inventory.md`). Both are labeled CC BY 4.0 in the PDFs; preserve attribution and inspect third-party-figure exceptions. PDF extraction may mis-order columns, captions, tables and formulas. No confidential manuals, personal data, unrestricted live browsing, or unsupported currentness claims. |
| **Explicit Out-of-Scope Tasks** | Detect or classify defects in uploaded images/video; control cameras, AOI/AXI machines or production equipment; provide authoritative safety-critical settings or autonomous manufacturing decisions; perform unrestricted live web research; use confidential industry documentation; make claims unsupported by the approved corpus. |
| **Evaluation Focus** | Can V1 retrieve relevant evidence and provide **correct, clear, verifiably cited answers** to in-scope questions, while acknowledging insufficient evidence or out-of-scope requests and responding within acceptable time? |

### Approved V1 PDF knowledge corpus (actual supplied files)

| Source ID | Approved paper | Publication / version | Verified file | Content role |
|---|---|---|---|---|
| **SRC-01** | Ren, Z., Fang, F., Yan, N., & Wu, Y. *State of the Art in Defect Detection Based on Machine Vision*. [DOI](https://doi.org/10.1007/s40684-021-00343-6) | **Journal volume 2022; online 26 May 2021** | 31-page English PDF, readable text | Fundamentals: optical illumination, CCD/CMOS imaging, image processing, defect inspection |
| **SRC-02** | Hütten, N., Alves Gomes, M., Hölken, F., Andricevic, K., Meyes, R., & Meisen, T. *Deep Learning for Automated Visual Inspection in Manufacturing and Maintenance: A Survey of Open-Access Papers*. [DOI](https://doi.org/10.3390/asi7010011) | **Published 22 January 2024** | 38-page English PDF, readable text | Survey of automated visual inspection, classification/localization/segmentation and deep learning |

**Source-selection continuity with Week 1:** Hütten et al. was already listed as a Week 1 source. Ren et al. **replaces the inaccessible, vendor-focused Cognex guide** in the V1 corpus. The National Instruments lighting resource remains an optional background website and is **not** counted as one of the two PDFs. This is a refinement of knowledge sources, **not** a change to the project title or its RAG goals. Both PDFs have been provided; actual application ingestion, retrieval and testing remain future work.

**Traceability intent:** O1 is supported by **FR1, FR2, NFR3**; O2 by **FR3, FR4, FR5, RAI1–RAI3**; O3 by **NFR1–NFR4 and the measurable RAI controls**. These IDs will be linked to evaluation criteria in Part B.

## Section 1 — Functional Requirements (A1)

| ID | Requirement — The system SHALL | Scope Boundary — SHALL NOT (where relevant) |
|---|---|---|
| **FR1** | **The system shall** answer beginner questions about **documented** industrial machine vision and automated visual inspection concepts using retrieved evidence from SRC-01/SRC-02. | Shall not present concepts outside the approved documents as established source-backed facts. |
| **FR2** | **The system shall** explain or compare documented inspection concepts (e.g., bright-field vs dark-field lighting; classification vs localization; traditional processing vs deep learning) when sufficient supporting passages are available. | Shall not make production-equipment recommendations, set inspection parameters, or invent AOI/AXI comparisons absent from the approved corpus. |
| **FR3** | **The system shall** provide a verifiable source title and document link for each document-grounded answer, with a page or section reference when available. | Shall not invent document titles, links, page numbers or citations. |
| **FR4** | **The system shall** identify questions outside its educational scope or lacking adequate supporting evidence and respond with a clear limitation or refusal, as appropriate. | Shall not generate unsupported answers or claim to operate industrial equipment. |
| **FR5** | **The system shall** present technical answers in understandable language for beginners and explain specialist terms when needed. | Shall not sacrifice technical accuracy merely to simplify an explanation. |

## Section 2 — Non-Functional Requirements (A2)

| ID | Quality Attribute | Requirement | Measurement Method | Metric | Proposed Threshold |
|---|---|---|---|---|---|
| **NFR1** | Performance | The system shall respond within a practical interactive latency for typical in-scope questions. | Time the complete query-to-answer process for a fixed set of **40 in-scope questions**, using the same V1 test environment. | **p90 end-to-end response latency** (seconds). | **≤ 10 seconds**. |
| **NFR2** | Correctness | The system shall provide technically correct answers consistent with the approved documents. | Compare responses to **40 source-verified reference answers** using a rubric; mark an answer correct only when its key factual claims agree with the source. | **Correct response rate** = correct answers / 40 × 100%. | **≥ 80%**. |
| **NFR3** | Retrieval relevance | The system shall retrieve passages relevant to the information needed for each supported question. | For the same **40 test questions**, annotate at least one relevant source passage per question and check whether a relevant passage appears among the first five retrieved results. | **Retrieval Hit@5** = questions with ≥ 1 relevant passage in top 5 / 40 × 100%. | **≥ 80%**. |
| **NFR4** | Maintainability | The system shall allow an approved document to be added or replaced and made available for subsequent questions without rebuilding the entire application. | Perform **3 controlled document-add/update trials** in the same environment; measure time from starting the update until the new document is searchable. | **Document update time** (minutes per trial). | **≤ 15 minutes in each trial**. |

**Testing note:** These are initial, measurable V1 acceptance targets, **not achieved results**. The planned 40-question evaluation set will contain only questions with source-verified answers from SRC-01/SRC-02; it will cover fundamentals, inspection tasks and documented comparisons. Separate targeted test sets are planned for 20 corpus-unanswerable questions, 10 out-of-scope requests, and 10 date-sensitive questions; three approved-document update trials are also planned. Out-of-scope handling is an evaluation of **FR4**, while insufficient-evidence handling is evaluated under **FR4/RAI1**. No implementation or testing is claimed.

## Section 3 — Responsible AI Requirements (A3)

| ID | Responsible AI Risk | Requirement | Measurement Method | Metric | Proposed Threshold |
|---|---|---|---|---|---|
| **RAI1** | Hallucination / unsupported technical answers | The system shall acknowledge insufficient evidence rather than invent technical information. | Test **20 questions** that cannot be answered from the approved corpus; manually check whether the response appropriately states the limitation without supplying invented facts. | **Appropriate insufficient-evidence response rate**. | **≥ 90%** (at least 18/20). |
| **RAI2** | Incorrect or misleading citations | The system shall provide citations for document-grounded answers and ensure the cited passages support their associated claims. | For the **40 in-scope test questions**, check (a) whether a citation is present and (b) whether the cited material actually supports the answer's key claims. | **Citation presence rate**; **citation-support rate**. | **100% citation presence** and **≥ 90% citation support**. |
| **RAI3** | Outdated or incomplete information | The system shall identify the source publication/revision date when available and avoid claiming that its information is current without evidence. | Review metadata for **all indexed documents** and test **10 date-sensitive questions** (e.g., about the latest inspection technologies); check that missing or old evidence is qualified. | **Available-date metadata coverage**; **appropriate recency-warning rate**. | **100% of available document dates recorded**; **100% of 10 recency cases appropriately qualified**. |

### Part A Reflection

**Which Responsible AI requirement will be the most difficult to measure or enforce technically? Why?**

**RAI2 (citation support)** will be the most difficult because including a reference does not prove that the reference supports every technical statement. Checking the actual meaning of cited passages—especially when evidence spans figures, tables or multiple sections—may require manual review and a clear evaluation rubric.

---

### References and knowledge-source attribution

**Approved PDF corpus (the documents the proposed V1 assistant will search):**
1. Ren, Z., Fang, F., Yan, N., & Wu, Y. (2022; online 2021). *State of the Art in Defect Detection Based on Machine Vision*. *International Journal of Precision Engineering and Manufacturing–Green Technology, 9*, 661–691. https://doi.org/10.1007/s40684-021-00343-6
2. Hütten, N., Alves Gomes, M., Hölken, F., Andricevic, K., Meyes, R., & Meisen, T. (2024). *Deep Learning for Automated Visual Inspection in Manufacturing and Maintenance: A Survey of Open-Access Papers*. *Applied System Innovation, 7*(1), 11. https://doi.org/10.3390/asi7010011

**Topic 1 related work informing the proposed RAG design (not necessarily part of the ingested corpus):**
3. *Enhancing printed circuit boards operational efficiency through multimodal retrieval-augmented generation chatbots: Bridging textual and visual documentation* (2026). https://doi.org/10.1016/j.array.2026.100881
4. *Document GraphRAG: Knowledge Graph Enhanced Retrieval Augmented Generation for Document Question Answering Within the Manufacturing Domain* (2025). https://doi.org/10.3390/electronics14112102
5. *TechDocRAG: Relation-Preserving Retrieval-Augmented Generation (RAG) for Technical Documents* (2026). https://doi.org/10.3390/ai7050161

**Copyright and reuse:** The two selected papers identify a CC BY 4.0 license. Attribute authors and publisher; check credit lines for third-party images if redistributing their figures. See `docs/week2_source_inventory.md` for local filenames, document quality and risks.
