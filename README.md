# Health RAG Pipeline

## Project Overview

This project was developed as part of **Enterprise Knowledge Retrieval for Pharma & Healthcare Research**.

The goal of the project is to build a **hybrid healthcare retrieval system** that can search across:

- biomedical research text
- clinical-style image data
- multimodal text and image evidence

The notebook in this repository implements a retrieval pipeline that starts with classical information retrieval methods, extends to dense semantic retrieval, adds two-stage re-ranking, and finally explores multimodal retrieval using chest X-ray images.

Primary implementation file:

- [health_rag_pipeline.ipynb](/Users/sanketpanchalwar/code-library/git-projects/health-rag-pipeline/health_rag_pipeline.ipynb)

## Problem Statement

Healthcare and pharma research teams often need to retrieve relevant scientific and clinical information quickly. Traditional keyword search works well for exact terminology, but it struggles when:

- the query and document use different medical vocabulary
- the same condition is described in multiple ways
- information must be retrieved across both text and images

This project addresses that problem by combining:

- sparse retrieval methods such as TF-IDF and BM25
- dense retrieval using Sentence-BERT embeddings
- re-ranking with a cross-encoder
- multimodal retrieval using CLIP-style shared embeddings

## Objectives

The project was designed to:

- build a healthcare-focused retrieval pipeline over PubMed-style biomedical text
- compare classical and neural retrieval approaches
- evaluate ranking quality using standard IR metrics
- extend retrieval to chest X-ray images
- demonstrate how multimodal retrieval supports healthcare knowledge discovery

## Dataset Used

### 1. Biomedical Text Corpus

The notebook uses a sampled biomedical literature collection based on PubMed / PMC-style healthcare research content, focused on themes such as:

- oncology
- immunotherapy
- drug interactions

### 2. NIH Chest X-ray Sample

The multimodal section uses a local sample from the NIH Chest X-ray dataset stored in:

- [chest_xray_samples](/Users/sanketpanchalwar/code-library/git-projects/health-rag-pipeline/chest_xray_samples)

Included supporting files:

- [Data_Entry_2017_v2020.csv](/Users/sanketpanchalwar/code-library/git-projects/health-rag-pipeline/chest_xray_samples/Data_Entry_2017_v2020.csv)
- [BBox_List_2017.csv](/Users/sanketpanchalwar/code-library/git-projects/health-rag-pipeline/chest_xray_samples/BBox_List_2017.csv)

These files provide image metadata and labels that help connect image content to medically meaningful captions and categories.

## Project Workflow

The notebook is organized into five major phases.

### Phase 1: Classical Information Retrieval

This phase establishes the foundation of the system using traditional IR techniques:

- text preprocessing
- inverted index construction
- positional index construction
- Boolean retrieval
- TF-IDF ranking
- BM25 ranking

This stage shows how lexical matching works well for exact terms and phrase-based search.

### Phase 2: Dense Retrieval

This phase introduces semantic search using neural embeddings:

- Sentence-BERT document embeddings
- cosine similarity retrieval
- dot-product retrieval
- a conceptual ColBERT-style late interaction demonstration

Dense retrieval helps solve the vocabulary mismatch problem, which is especially common in biomedical search.

### Phase 3: Two-Stage Re-ranking

This phase combines speed and accuracy:

- Stage 1 retrieves candidates with BM25 or dense retrieval
- Stage 2 re-ranks them with a cross-encoder

This design mirrors modern production retrieval systems, where fast candidate generation is followed by more expensive semantic ranking.

### Phase 4: Evaluation

The notebook evaluates retrieval quality using a small manual relevance judgment set and standard ranking metrics:

- Precision@K
- Recall@K
- Mean Reciprocal Rank (MRR)
- nDCG@10

This makes the assignment more realistic because it moves beyond building the pipeline into measuring retrieval effectiveness.

### Phase 5: Multimodal Retrieval

The final phase extends the system to support both text and images:

- chest X-ray image loading and metadata preparation
- CLIP-based image and text embeddings
- late fusion of text and image retrieval scores
- visualization of multimodal retrieval results

This phase demonstrates how a retrieval pipeline can move toward real-world healthcare AI use cases involving mixed data modalities.

## Methods and Models Used

The main methods used in the project are:

- `TF-IDF`
- `BM25`
- `Sentence-BERT`
- `Cross-Encoder`
- `ColBERT-style late interaction`
- `CLIP-based multimodal embeddings`

Representative model choices in the notebook include:

- `all-MiniLM-L6-v2`
- `cross-encoder/ms-marco-MiniLM-L-6-v2`
- `clip-ViT-B-32` for multimodal representation

## Key Findings

The notebook’s summary highlights the following conclusions:

- BM25 performs better than TF-IDF for medical text retrieval
- dense retrieval improves semantic matching when exact terms differ
- cross-encoder re-ranking improves ranking quality further, especially for top results
- multimodal late fusion enables retrieval across both text and image evidence

The central retrieval challenge identified in the assignment is **vocabulary mismatch**, and the dense retrieval stages directly help address it.

## What I Learned From This Project

This assignment helped strengthen understanding of both information retrieval fundamentals and modern retrieval-augmented AI concepts.

### Core Concepts Learned

- the difference between sparse and dense retrieval
- how inverted and positional indexes support fast search
- why BM25 is often stronger than plain TF-IDF
- how semantic embeddings improve retrieval quality
- how cross-encoders differ from bi-encoders
- how evaluation metrics like MRR and nDCG reflect ranking quality
- how multimodal embedding spaces allow text-to-image retrieval

### Practical Skills Developed

- preprocessing and indexing domain-specific text
- comparing retrieval strategies experimentally
- designing a two-stage retrieval architecture
- working with biomedical and imaging datasets together
- evaluating search systems using relevance judgments
- building a notebook-based prototype for healthcare retrieval

## Why This Project Matters

This project is a strong introduction to retrieval systems in the healthcare domain because it connects theory to practice across:

- search and ranking
- semantic retrieval
- model-based re-ranking
- multimodal AI

It also reflects real enterprise use cases where analysts, researchers, or clinicians may need to retrieve evidence from multiple sources quickly and accurately.

## Repository Structure

```text
health-rag-pipeline/
├── health_rag_pipeline.ipynb
├── requirements.txt
├── .gitignore
└── chest_xray_samples/
    ├── BBox_List_2017.csv
    ├── Data_Entry_2017_v2020.csv
    └── images/
```

## How to Run

### 1. Create and activate a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Launch Jupyter

```bash
jupyter notebook
```

Then open:

- `health_rag_pipeline.ipynb`

## Dependency Notes

The notebook downloads some resources at runtime, including:

- NLTK tokenization and lexical resources
- transformer models used for dense retrieval and re-ranking
- optional multimodal model weights

Because of this, the first run may take longer than later runs.

## Suggested Future Improvements

If this project is extended further, strong next steps would be:

- move notebook logic into modular Python scripts
- add a reproducible environment file with pinned versions
- save intermediate embeddings and indexes for faster reruns
- add a small demo interface for interactive querying
- expand evaluation with more queries and stronger relevance labels
- improve multimodal retrieval with better caption generation and fusion strategies

## Conclusion

This project demonstrates a complete learning journey from basic indexing and ranking to semantic and multimodal retrieval in healthcare. It shows how modern retrieval systems can be built incrementally, evaluated carefully, and adapted to domain-specific challenges such as biomedical vocabulary and mixed text-image evidence.
