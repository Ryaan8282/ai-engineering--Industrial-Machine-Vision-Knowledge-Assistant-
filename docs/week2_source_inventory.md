# Week 2 Source Inventory — Selected Knowledge PDFs

**Project:** Industrial Machine Vision Knowledge Assistant  
**Status:** Two source PDFs supplied by the project author and checked for file readability and extractable text. No ingestion, indexing or testing has been performed.  
**Purpose:** Support the Topic 2 corpus decision and Topic 3 preparation. This inventory is supplementary, not one of the four compulsory Week 2 files.

| Field | SRC-01 | SRC-02 |
|---|---|---|
| Title | State of the Art in Defect Detection Based on Machine Vision | Deep Learning for Automated Visual Inspection in Manufacturing and Maintenance: A Survey of Open-Access Papers |
| Authors | Zhonghe Ren, Fengzhou Fang, Ning Yan, You Wu | Nils Hütten, Miguel Alves Gomes, Florian Hölken, Karlo Andricevic, Richard Meyes, Tobias Meisen |
| Journal citation | *International Journal of Precision Engineering and Manufacturing–Green Technology* 9, 661–691 (2022) | *Applied System Innovation* 7(1), 11 (2024) |
| Online publication | 26 May 2021 | 22 January 2024 |
| DOI | https://doi.org/10.1007/s40684-021-00343-6 | https://doi.org/10.3390/asi7010011 |
| Actual uploaded PDF | 31 pages | 38 pages |
| License indicated in paper | Creative Commons Attribution 4.0 | Creative Commons Attribution 4.0 |
| Initial topic coverage | Machine vision system components, illumination, CCD/CMOS, preprocessing and defect detection | Deep learning, industrial automated visual inspection, classification/localization/segmentation, implementation challenges |
| Expected PDF extraction issues | Two-column reading order; captions, tables, equations, references | Two-column reading order; figures, charts, tables, lengthy references |
| Suitability | Initial fundamental source for retrieval, not an autonomous inspection system | Academic review for source-grounded explanation, not AI-training data for the chatbot |

## Original Week 1 versus refined Week 2

- **Preserved from Week 1:** Hütten et al. (2024) was already identified as a project data source.
- **Replaced for the approved corpus:** Cognex *Introduction to Vision Sensors* had a broken source link and was vendor-focused; the selected Ren et al. machine-vision survey supplies broader academic grounding.
- **Not counted as one of the two PDFs:** National Instruments' *A Practical Guide to Machine Vision Lighting* is a web article.
- **Project scope stays unchanged:** RAG text Q&A with cited explanations of industrial machine vision topics for learners; no industrial machine operation, image upload classification, production decision-making or unrestricted live web browsing.

## Licenses and citation responsibility

Both source papers contain Creative Commons Attribution 4.0 language. See https://creativecommons.org/licenses/by/4.0/ . Credit authors, title, journal, DOI and license, identify changes when applicable, and check any third-party material credit lines before redistributing individual figures. This ZIP contains local-use source copies so the project can proceed without broken external download links. **Only commit the Markdown and diagram files to a public repository by default; assess source-PDF redistribution requirements separately.**

## Suggested initial supported-question families (after ingestion)

1. What are the main parts of a typical machine-vision inspection system? (SRC-01)
2. Why do illumination modes affect defect visibility? (SRC-01)
3. How do camera sensors and acquisition fit into a vision workflow? (SRC-01)
4. How do classification, localization and segmentation differ in AVI? (SRC-02)
5. Which kinds of deep-learning approaches are discussed for industrial visual inspection? (SRC-02)

**Limitation:** Detailed AOI/AXI differences, model-selection recommendations for real factories and claims about the newest products may be unanswerable from this narrow initial corpus. Such questions should receive an evidence limitation or a qualified answer, not an invented source citation.
