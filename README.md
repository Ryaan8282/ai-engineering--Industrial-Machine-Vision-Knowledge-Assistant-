# Industrial Machine Vision Knowledge Assistant

> A planned retrieval-augmented generation (RAG) knowledge assistant to help students, beginner engineers, and researchers understand industrial machine vision using cited technical sources.

## Project Status

**AI Engineering semester project — Week 1 documentation stage.** This repository records project planning and will be expanded in later labs. The proposed RAG application has **not yet been implemented or evaluated**.

## Problem Statement

Industrial machine vision covers automated optical inspection (AOI), automated X-ray inspection (AXI), image processing, computer vision, and deep learning. Relevant technical information is distributed across research papers, equipment documentation, and practical technical guides, making it difficult for students and beginner engineers to find, understand, and compare inspection approaches efficiently.

The proposed solution is a domain-focused AI knowledge assistant that retrieves relevant information from approved technical documents and produces understandable, source-supported explanations.

## Evidence of the Problem

- *Enhancing printed circuit boards operational efficiency through multimodal RAG chatbots* (2026), https://doi.org/10.1016/j.array.2026.100881 — discussed in the Week 1 scope as relevant to understanding and accessing equipment documentation.
- *TechDocRAG: Relation-Preserving RAG for Technical Documents* (2026), https://doi.org/10.3390/ai7050161 — discussed in the Week 1 scope as relevant to structured technical document retrieval across text, figures, and tables.

These sources motivate the project; the Week 1 materials do not establish measured performance of this proposed assistant.

## Initial Related Work / Existing Approaches

| Study | Link | Limitation considered in Week 1 |
| --- | --- | --- |
| Multimodal RAG Chatbots for PCB Manufacturing (2026) | https://doi.org/10.1016/j.array.2026.100881 | Relies on confidential, equipment-specific documentation |
| Document GraphRAG (2025) | https://doi.org/10.3390/electronics14112102 | Complex implementation and document extraction challenges |
| TechDocRAG (2026) | https://doi.org/10.3390/ai7050161 | Depends on accurate document parsing |

## Engineering Gap / Limitation

Existing technical RAG approaches may be complex or tightly tied to particular equipment and document collections. This project explores a beginner-friendly, document-grounded assistant built around publicly accessible industrial machine vision knowledge. The practical gap and measurable targets will be refined in Topic 2.

## Project Objectives

- **O1:** Design a document-grounded AI assistant for industrial machine vision knowledge retrieval.
- **O2:** Develop a RAG-based question-answering system with source citations.
- **O3:** Evaluate retrieval relevance, answer accuracy, groundedness, and response time.

## Target Users

- Students learning industrial machine vision
- Beginner machine vision engineers
- Researchers exploring industrial inspection technologies

## Candidate Data Sources

1. Cognex — *Introduction to Vision Sensors*: https://www.cognex.cn/library/media/files/intro_to_vision_sensors_en.pdf
2. National Instruments — *A Practical Guide to Machine Vision Lighting*: https://www.ni.com/en/shop/choosing-the-right-hardware-for-your-vision-applications/a-practical-guide-to-machine-vision-lighting.html
3. *Deep Learning for Automated Visual Inspection in Manufacturing and Maintenance* (2024): https://doi.org/10.3390/asi7010011

These are **candidate sources**; their final selection, access conditions, and preparation are to be validated in later labs. Do not upload restricted or copyrighted copies without permission.

## Responsible AI Considerations

- **Hallucination:** Ground answers in retrieved documents and provide citations.
- **Incorrect citations:** Evaluate whether cited sources really support generated claims.
- **Outdated information:** Track source publication dates and plan for knowledge-base updates.

## Week 1 Deliverables

- [Group observation sheet — ChatGPT](docs/week1_observation_sheet.md)
- [Conceptual AI system map — ChatGPT](docs/week1_system_map.png)
- [Individual project scope](docs/week1_project_scope.md)

The ChatGPT observation and system map are **Topic 1 group exercises**, not the architecture of the proposed industrial knowledge assistant.

## Weekly Progress

| Week | Focus | Deliverables | Status |
| --- | --- | --- | --- |
| 1 | AI system observation, conceptual system map, and semester project scope | Observation sheet, system map, project scope, README | Documentation prepared; observation evidence review pending |
| 2 | Requirements, evaluation criteria, and V1 architecture | Topic 2 documentation and architecture diagram | Not started |
| 3 | Data ingestion, processing, validation, and lineage | Pipeline notebook, inventory, pipeline diagram, prepared data | Not started |

## Repository Notes

- Store project documentation under `docs/` and update this README weekly.
- Keep API keys, passwords, private material, and unlicensed source PDFs out of the public repository.
- Engineering decisions and test evidence will be documented in later topics.
