# Topic 3 — Part A: Data Needs, Inspection and Source Inventory

**Project:** Industrial Machine Vision Knowledge Assistant  
**Use case:** A beginner-oriented, document-grounded RAG assistant explaining industrial machine-vision concepts using evidence from approved research papers.  
**Actual selected pathway:** A — **PDF/TXT document preparation**, specifically two academic PDFs. This is **not** training or validating a defect classifier.

**Execution status:** Both exact uploaded PDFs were inspected and processed locally using the notebook in `notebooks/week3_pipeline.ipynb`. The local preparation produces **663** page-labelled text chunks (see manifests for traceable evidence). **Google Colab execution has not been independently verified** and must be performed by the student. These counts are data-preparation observations, not RAG accuracy results.

## A1 — Three primary Topic 2 requirements and data needs

| Topic 2 requirement | Needed information / representation | Actual source(s) | Suitability / constraint |
|---|---|---|---|
| **FR1 — Answer industrial machine-vision questions from approved documents** | Definitions and explanations about illumination, image acquisition, image processing and industrial visual inspection | SRC-01 Ren et al.; SRC-02 Hütten et al. | Peer-reviewed papers with readable text; not an unrestricted or exhaustive machine-vision encyclopedia |
| **NFR3 — Relevant retrieval** | Text passages split into coherent, traceable units | PDF text blocks converted to page-labelled JSONL | Preparation supports later retrieval; **Hit@5 ≥80% has not been tested** |
| **RAI2 — Verifiable citation support** | Source titles, DOI URLs, publication metadata, page numbers, file checksums | Per-PDF metadata and per-chunk fields | Enables future citation audits; does not by itself establish correct citations or answer grounding |

**Linked controls for later stages:** FR3 (source display), FR4/RAI1 (out-of-scope or unsupported questions), RAI3 (date transparency), and NFR4 (repeatable document updates). The primary A1 mapping is intentionally focused on the three IDs above.

## A2–A4 — Actual data inventory

| Source ID | Exact local filename and stable URL | Type / purpose | Version / owner | Access and rights | Observed inspection |
|---|---|---|---|---|---|
| **SRC-01** | `ren_2022_machine_vision_defect_detection.pdf` — https://doi.org/10.1007/s40684-021-00343-6 | **PDF**: overview of optical illumination, acquisition, processing and machine-vision defect-detection methods | Zhonghe Ren, Fengzhou Fang, Ning Yan, You Wu; journal volume **2022**, first online **26 May 2021** | Paper identifies **CC BY 4.0**; retain citation and check separately credited figures | **31 pages**, **153,138** extracted characters, **0** pages with empty text; relevant visual diagram on page 2 |
| **SRC-02** | `huetten_2024_deep_learning_visual_inspection.pdf` — https://doi.org/10.3390/asi7010011 | **PDF**: survey of deep-learning methods and industrial automated visual inspection | Nils Hütten et al.; *Applied System Innovation* **2024**, published **22 January 2024** | Paper identifies **CC BY 4.0**; retain citation and check separately credited figures | **38 pages**, **141,860** extracted characters, **0** pages with empty text; 196-paper literature survey described on page 1 |

**Where files live:** The original PDF copies are provided under `source_pdfs_local_only/` in the delivery ZIP and should be placed temporarily in Colab under `data/raw/`. Prepared records are exported to `data/processed/` and `data/pipeline_v1/documents/`. **The `data/raw/` PDFs are not included in the default GitHub-copy instructions.**

## Two representative source inspections (A3)

1. **SRC-01 / Ren et al., PDF page 2:** The paper's diagram and surrounding text identify optical illumination, image acquisition, and image-processing/defect-detection as major industrial inspection stages. This provides technical domain knowledge for the assistant; the assistant itself will not perform those stages on camera images.
2. **SRC-02 / Hütten et al., PDF page 1:** The abstract describes a review of 196 open-access papers and the relationship of convolutional networks, transformers and training approaches to automated visual inspection. It supplies *conceptual explanations*, not labeled image data.

**Data types:** Original files are **unstructured PDF documents**; prepared output is **semi-structured JSON Lines** (`record_id`, `source_id`, `source`, `source_title`, `source_url`, `source_sha256`, `publication`, `publication_date`, `page`, `processing`, `text`). PDF *page* labels are preserved, not inferred from surrounding text.

## Observed issues and what was done about them

- **Repeated page furniture:** The text extraction originally produced orphan records such as `1 3` from the Springer paper. The revised pipeline suppresses that exact repeating marker and `Vol.:(0123456789)` (plus margins on pages after the title); this is a narrow, documented heuristic.
- **Short but meaningful chunks:** The final records still contain **5** SRC-01 and **1** SRC-02 chunks shorter than 60 characters. These are meaningful headings/table labels, **not** indiscriminately deleted. Long-block orphan tails were rebalanced at word boundaries where possible.
- **Figures, tables, equations and columns:** PyMuPDF extracts *embedded text*, not images. Multi-column ordering, mathematical formatting, captions and figure/table relationships can be imperfect. A later manual quality audit and possibly richer layout extraction are still necessary.
- **Source coverage:** The initial two-paper corpus is strong on inspection systems and deep learning but is **not guaranteed to answer detailed AOI-versus-AXI questions**. If no supported passage exists, future FR4/RAI1 behaviour must acknowledge insufficient evidence.
- **Publication age:** The two fixed papers provide historical documented knowledge only. They must not be represented as up-to-date reports of current industrial technology without qualification (RAI3).
- **Access:** Both PDFs are academic open-access papers. If publishing copied or derived content, credit the source and licence; separately credited third-party illustrations may have additional rights limitations.

## Local Part A/B checkpoint

- Input existence, exact filename, PDF readability and two distinct source samples: **PASS locally**.
- Combined page count: **69** (31 + 38).
- Part B prepared output: **663** nonempty page-labelled JSONL records (SRC-01: **343**, SRC-02: **320**).
- This inspection does **not** show actual RAG answer correctness, retrieval Hit@5 or citation-support rates.
