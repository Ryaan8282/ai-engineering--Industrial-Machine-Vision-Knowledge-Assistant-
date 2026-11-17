# Topic 3 — Part B/C: Preparation Decisions, Executed Pipeline and Traceability

**Project:** Industrial Machine Vision Knowledge Assistant  
**Pathway:** **A — unstructured research PDF to source-traceable text JSONL.** The project is a *RAG knowledge assistant*, not a vision model trained on industrial defect images.  
**Status:** A local notebook run passed basic output, lineage and same-environment repeatability checks; Google Colab rerun and GitHub commit remain user actions. No RAG retrieval/LLM evaluation has been performed.

## C3 — Requirement-driven source decision

| Primary ID | Reason in data pipeline | Evidence location |
|---|---|---|
| **FR1** | The assistant needs approved industrial machine-vision technical material | Two named PDFs, `docs/week3_data_inventory.md` |
| **NFR3** | Text must be prepared for later retrieval and evaluation | `data/processed/prepared_text.jsonl`, Part B comparison below |
| **RAI2** | Technical responses must be traceable to genuine evidence | Title, DOI, page number and SHA-256 in each JSONL record; manifest links |

Supporting Topic 2 goals: FR3 (citations), FR4/RAI1 (limitations), RAI3 (source dates), NFR4 (reproducible updates). **Storing page metadata is not equivalent to measuring citation support or Hit@5.**

## B1/B2/B3 — Two preparations compared on the same actual PDFs

| Source PDF | Fixed slicing, 500 chars | Page-/block-aware, ≤500 chars | Boundary evidence |
|---|---:|---:|---|
| SRC-01 — Ren et al. (2022) | **308** chunks | **343** chunks | Fixed slicing: **176** alphanumeric mid-word boundaries; block-aware: **0** forced mid-word cuts |
| SRC-02 — Hütten et al. (2024) | **298** chunks | **320** chunks | Fixed slicing: **172** alphanumeric mid-word boundaries; block-aware: **0** forced mid-word cuts |
| **Combined** | **606** | **663** | Six retained chunks shorter than 60 characters are meaningful headings or table labels, not unreviewed page markers |

**Selected configuration:** `{"method": "paragraph-aware", "chunk_size": 500, "source_ids": ["SRC-01", "SRC-02"], "page_metadata": true, "cleanup_version": "v1.1-known-footer-and-orphan-tail"}`.

**Chosen benefit:** Keeps every chunk within a single actual PDF page; generally avoids cutting words; preserves source/page metadata needed for later evidence-linked answers. Specific recurring Springer markers (`1 3`, `Vol.:(0123456789)`) and certain running margin blocks are removed. Small tails from a *single long text block* are rebalanced around a word boundary. **This is not semantic chunking.**

**Trade-off:** More chunks than fixed slicing and possible isolation of meaningful section headings. PDF text order may still scramble two-column paragraphs and lose the relationship between figures, tables and captions. We retained meaningful short headings rather than deleting information, and deferred more thorough quality/fitness testing to Topic 4. This comparison measures **preparation artefacts only**; it is not a claim that retrieval is more accurate.

## B3 — Basic output acceptance checks

1. Both explicit source paths exist, are authentic readable PDFs and contain 31 and 38 pages.
2. Selected per-source and combined JSONL files exist and are nonempty.
3. All **663** JSONL records parse, contain nonempty text of **≤500 characters** and have a valid `record_id`, `source_title`, DOI, source hash and **1-based PDF page number**.
4. All recognized standalone `1 3`/volume marker records were removed, without discarding meaningful headings by length alone.
5. One record preview is printed. Basic validation passes **locally**; manual meaning, figure and table audits remain pending.

## B4 — Source lineage and provenance

- **Part B manifest** `data/week3_manifest.json`: two per-source mappings from exact PDF basename and SHA-256 → named output JSONL and SHA-256, plus the derived combined JSONL.
- **Part C manifest** `data/pipeline_v1/documents/pipeline_manifest.json`: selected PDF/text pathway, configuration, inspection counts, inputs, outputs, source↔output relationships, checksums, date/rights details, and basic output checks.
- **C1 repeatability** `data/pipeline_v1/documents/repeatability_evidence.json`: re-runs the same stage in the **same local environment**, comparing source identities/hashes, output hashes/size/counts and mappings. Result: **PASS locally**. This does not establish cross-platform stability or retrieval accuracy.

## C1 — Executable V1 pipeline (ETL + batch)

**Extract:** Open the two explicitly named PDF inputs with PyMuPDF and inspect all pages' text blocks.  
**Transform:** Perform limited whitespace/dehyphenation cleanup, skip explicitly recognized page furniture, compare two 500-character chunking methods, select paragraph-/block-aware chunks and attach provenance.  
**Load:** Write stable line-oriented JSONL to `data/processed/` (Part B) and `data/pipeline_v1/documents/` (Part C) and save manifests.

**Why ETL not ELT?** The corpus is two relatively static PDFs; meaningful text needs extraction and light cleanup before a downstream search store can use it. A vector index / language model is **not part of Topic 3**.  
**Why batch not streaming?** Sources are static versioned review papers; additions or updates can be ingested as explicit batch jobs. Live streaming or automatic online updates would be unjustified complexity.

## C3 — Stage contracts and failure responses

| Stage | Contract / evidence | Failure response |
|---|---|---|
| **Ingest** | Only two explicit approved PDF filenames in `data/raw/`, nonempty (>1 KiB), original SHA-256 | **Stop** when source is missing, incorrectly named, unexpectedly tiny or unauthorized |
| **Inspect** | Openable PyMuPDF, expected 31/38 pages, embedded text samples, no entirely empty-text pages | **Stop or flag** unreadable/scanned PDF, version mismatch or structurally broken text; later OCR only if separately justified |
| **Prepare** | Same chosen `paragraph-aware` ≤500-char configuration in Part B and C; source/page labels retained | **Stop** if unsupported method, no nonempty passages or impossible export |
| **Validate** | Source-specific and combined JSONLs parse, record counts match and each output SHA-256 is stored | **Stop** for empty/unreadable output or invalid source/page/hash metadata; flag weird headings/columns for later review |
| **Record lineage** | Every source maps to a distinct prepared output; combined output identified as derived | **Stop** if source fingerprint or mapping is missing/inconsistent |
| **Repeatability** | Rerun same inputs/config and compare hashes, record counts and mappings | **Flag** mismatch; timestamps may differ and are not tested for equality |

## C2 — Draw.io diagram and two failure points

`docs/week3_pipeline_diagram.png` (editable source: `.drawio`) shows **SOURCE → INGEST → INSPECT → PREPARE → VALIDATE → PREPARED OUTPUTS → RECORD LINEAGE**, plus two failure responses: (1) missing/invalid source PDF → stop and request valid PDF; (2) blank/garbled extracted text → stop and flag a manual layout/OCR review.

## C4 — Submission and responsible publishing

The selected docs/notebook and Part B/C outputs should go in the **same existing GitHub repository**. The original source PDFs are kept under `source_pdfs_local_only/` in the delivery ZIP for Colab upload; do not copy this folder to the public GitHub repository automatically. The papers identify CC BY 4.0, requiring attribution and respecting exclusions for separately credited figures. The prepared excerpts also retain attribution and DOI/page metadata.

**Not evaluated here:** The original Topic 2 thresholds (Hit@5, answer correctness, citation support, insufficient-evidence handling, latency, document-update time). Topic 3 verifies **data preparation**, not actual chatbot performance. AOI/AXI questions must be declined or qualified when these documents have insufficient evidence.
