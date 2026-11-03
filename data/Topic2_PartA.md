# Requirements Specification — Industrial Machine Vision Knowledge Assistant
**Version:** 1.0  
**Course:** AI Engineering — Topic 2 Lab  
**Scope:** Part A only (Sections 0–3)

> **Project status:** Proposed V1 requirements. The thresholds below are initial acceptance targets for later testing, not results already achieved.

## Section 0 — Project Framing & Application Scope Checkpoint (A0)

| Framing element | Refined project description |
|---|---|
| **Problem Evidence** | **Evidence 1:** Industrial equipment manuals can contain lengthy and complex text and visual material, making retrieval and interpretation challenging. An industrial PCB-documentation chatbot study evaluates RAG methods for this problem. [Study (2026)](https://doi.org/10.1016/j.array.2026.100881). **Evidence 2:** In technical documents, supporting facts may be spread across clauses, tables, figures and procedures; flattening them into independent chunks can break evidence relationships. [TechDocRAG (2026)](https://doi.org/10.3390/ai7050161). These sources establish a technical-document retrieval problem; they do **not**, by themselves, prove unmet demand among students. |
| **Existing Approaches** | **1. Multimodal RAG chatbots for PCB manufacturing (2026):** Study of LongRAG/GraphRAG and text-plus-visual equipment-manual question answering; uses confidential domain-specific manuals. [Source](https://doi.org/10.1016/j.array.2026.100881). **2. Document GraphRAG (2025):** Uses document structure and knowledge graphs to improve manufacturing-related document QA. [Source](https://doi.org/10.3390/electronics14112102). **3. TechDocRAG (2026):** Preserves relationships between technical text, tables, figures and other evidence for question answering. [Source](https://doi.org/10.3390/ai7050161). |
| **Project / Engineering Gap** | A practical application opportunity exists for a **beginner-oriented, source-grounded knowledge assistant** using **public industrial machine vision documents**. V1 will focus on accessible explanations, relevant retrieval and checkable citations rather than novel RAG algorithms. This is a proposed engineering gap, not a claim of proven research novelty. |
| **Objective O1** | To design a document-grounded AI assistant for industrial machine vision knowledge retrieval. |
| **Objective O2** | To develop a RAG-based question-answering system that provides understandable explanations with source citations. |
| **Objective O3** | To evaluate retrieval relevance, answer correctness, evidence grounding, response time and responsible behaviour. |
| **Intended Users** | Students learning industrial machine vision, beginner machine vision engineers and researchers exploring industrial inspection technologies. |
| **Supported Tasks** | Ask natural-language questions; obtain definitions and explanations; compare inspection technologies where sources permit; retrieve information on cameras, vision sensors, lighting, AOI/AXI concepts and basic inspection algorithms; receive document references; identify when available evidence is insufficient. |
| **Information / Knowledge Domain** | **In scope:** Introductory industrial machine vision knowledge from approved public documents: image acquisition, sensors, lighting, inspection concepts, AOI/AXI and introductory computer-vision/AI methods. The system **explains** these topics; it does not execute inspection algorithms. |
| **Operating Context** | Read-only educational/research prototype accessed through a simple conversational interface, using a curated collection of public technical documents. Intended for individual learning and technical reference, **not** production-line operation. |
| **Important Constraints** | One-semester development time; limited computing/API budget; at least **two publicly accessible PDF documents** for the corpus; appropriate copyright and redistribution permissions; no confidential industrial manuals or personal data; possible limitations in extracting figures, tables and complex layouts; English-language V1. Candidate sources: [Cognex vision sensors PDF](https://www.cognex.cn/library/media/files/intro_to_vision_sensors_en.pdf), [Hütten et al. visual inspection survey (2024)](https://doi.org/10.3390/asi7010011), and [NI machine vision lighting guide (web article)](https://www.ni.com/en/shop/choosing-the-right-hardware-for-your-vision-applications/a-practical-guide-to-machine-vision-lighting.html). **The NI guide is not a PDF; it does not count toward the two-PDF minimum unless a permitted PDF is obtained.** Do not commit source PDFs publicly without checking redistribution rights. |
| **Explicit Out-of-Scope Tasks** | Detect or classify defects in uploaded images/video; control cameras, AOI/AXI machines or production equipment; provide authoritative safety-critical settings or autonomous manufacturing decisions; perform unrestricted live web research; use confidential industry documentation; make claims unsupported by the approved corpus. |
| **Evaluation Focus** | Can V1 retrieve relevant evidence and provide **correct, clear, verifiably cited answers** to in-scope questions, while acknowledging insufficient evidence or out-of-scope requests and responding within acceptable time? |

**Traceability intent:** O1 is supported by **FR1, FR2, NFR3**; O2 by **FR3, FR4, FR5, RAI1–RAI3**; O3 by **NFR1–NFR4 and the measurable RAI controls**. These IDs will be linked to evaluation criteria in Part B.

## Section 1 — Functional Requirements (A1)

| ID | Requirement — The system SHALL | Scope Boundary — SHALL NOT (where relevant) |
|---|---|---|
| **FR1** | **The system shall** answer questions about introductory industrial machine vision topics (e.g., image acquisition, vision sensors, lighting and inspection methods) using information from the approved document collection. | Shall not present information absent from the approved sources as established fact. |
| **FR2** | **The system shall** explain or compare documented machine vision concepts (e.g., AOI vs AXI or bright-field vs dark-field lighting) when sufficient source evidence is available. | Shall not select production equipment, set machine operating parameters or make autonomous inspection decisions. |
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

**Testing note:** These are initial, measurable V1 acceptance targets. The 40-question evaluation set will cover definitions, technical explanations and comparisons from the approved corpus. The actual measurements will be collected later; none have yet been performed.

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

### References (for Project Framing)
1. *Enhancing printed circuit boards operational efficiency through multimodal retrieval-augmented generation chatbots: Bridging textual and visual documentation* (2026). https://doi.org/10.1016/j.array.2026.100881
2. *Document GraphRAG: Knowledge Graph Enhanced Retrieval Augmented Generation for Document Question Answering Within the Manufacturing Domain* (2025). https://doi.org/10.3390/electronics14112102
3. Lee & Choi, *TechDocRAG: Relation-Preserving Retrieval-Augmented Generation (RAG) for Technical Documents* (2026). https://doi.org/10.3390/ai7050161
