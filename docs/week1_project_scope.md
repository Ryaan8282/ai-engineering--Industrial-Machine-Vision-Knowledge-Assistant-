# Week 1 Project Scope — Industrial Machine Vision Knowledge Assistant

## Project Name

Industrial Machine Vision Knowledge Assistant

## Domain

Artificial Intelligence / Industrial Machine Vision / Intelligent Manufacturing

## Problem Statement

Industrial machine vision involves various technologies, including Automated Optical Inspection (AOI), Automated X-ray Inspection (AXI), image processing, computer vision, and deep learning. Technical information about these technologies is distributed across research papers, industrial documentation, and technical guides, making it challenging for students and beginner engineers to efficiently understand and compare different inspection methods.

This project aims to develop an AI-powered knowledge assistant using Retrieval-Augmented Generation (RAG) to retrieve relevant information from technical documents and provide accurate, understandable, and source-supported explanations about industrial machine vision.

## Evidence of the Problem

**Evidence 1:** Industrial equipment manuals contain complex technical information, making information retrieval and interpretation challenging.

- **Source / citation:** *Enhancing printed circuit boards operational efficiency through multimodal RAG chatbots* (2026).
- **Link:** https://doi.org/10.1016/j.array.2026.100881

**Evidence 2:** Conventional RAG systems may struggle to retrieve related information distributed across tables, figures, and text.

- **Source / citation:** *TechDocRAG: Relation-Preserving RAG for Technical Documents* (2026).
- **Link:** https://doi.org/10.3390/ai7050161

## Initial Related Work (at least 3)

1. **Study / solution 1:** Multimodal RAG Chatbots for PCB Manufacturing (2026)
   - **Source / citation:** https://doi.org/10.1016/j.array.2026.100881
   - **Key limitation:** Uses confidential, equipment-specific documentation.

2. **Study / solution 2:** Document GraphRAG (2025)
   - **Source / citation:** https://doi.org/10.3390/electronics14112102
   - **Key limitation:** Complex implementation and document extraction challenges.

3. **Study / solution 3:** TechDocRAG (2026)
   - **Source / citation:** https://doi.org/10.3390/ai7050161
   - **Key limitation:** Depends on accurate document parsing.

## Engineering Gap / Limitation

Existing technical RAG approaches can be complex or equipment-specific. A beginner-friendly, document-grounded assistant focused on publicly available industrial machine vision knowledge remains a useful application opportunity.

## Initial Project Objectives (2–3)

- **O1:** To design a document-grounded AI assistant for industrial machine vision knowledge retrieval.
- **O2:** To develop a RAG-based question-answering system with source citations.
- **O3:** To evaluate retrieval relevance, answer accuracy, groundedness, and response time.

## Target Users

- Students learning industrial machine vision.
- Beginner machine vision engineers.
- Researchers exploring industrial inspection technologies.

## Data Sources (at least 2)

1. **Source 1:** Cognex — *Introduction to Vision Sensors*  
   https://www.cognex.cn/library/media/files/intro_to_vision_sensors_en.pdf
2. **Source 2:** National Instruments — *A Practical Guide to Machine Vision Lighting*  
   https://www.ni.com/en/shop/choosing-the-right-hardware-for-your-vision-applications/a-practical-guide-to-machine-vision-lighting.html
3. **Source 3:** *Deep Learning for Automated Visual Inspection in Manufacturing and Maintenance* (2024)  
   https://doi.org/10.3390/asi7010011

## Similar to EduAdvisor

Both use RAG to retrieve document information and generate answers supported by citations.

## Different from EduAdvisor

EduAdvisor focuses on academic information, while this project focuses on industrial machine vision technologies and technical knowledge.

## Responsible AI Risks (at least 2)

**Risk 1 — Hallucination:** Incorrect technical explanations may mislead users.

- **Mitigation:** Ground answers in reliable documents and provide citations.

**Risk 2 — Incorrect Citations:** Generated answers may not match their cited sources.

- **Mitigation:** Evaluate citation accuracy and answer groundedness.

**Risk 3 — Outdated Information:** Technical documents may contain outdated information.

- **Mitigation:** Track publication dates and update the knowledge base.
