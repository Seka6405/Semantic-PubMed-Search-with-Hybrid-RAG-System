# Semantic PubMed Search with Hybrid RAG

An AI-powered biomedical literature search system that helps users discover relevant PubMed research using semantic search, hybrid retrieval, result diversification, and RAG-based evidence summarization.

**GitHub Repository:** [Semantic-PubMed-Search-with-Hybrid-RAG-System](https://github.com/Seka6405/Semantic-PubMed-Search-with-Hybrid-RAG-System)

## Overview

Biomedical research queries often contain synonyms, complex clinical wording, or concepts that are difficult to express through exact keyword matching alone. This project combines traditional lexical retrieval with semantic embeddings to identify relevant research articles and present their evidence in a more accessible way.

The system is designed to support biomedical literature discovery by retrieving PubMed records, ranking them by relevance, reducing repetitive results, and summarizing evidence with links to source articles.

## Problem Statement

Traditional keyword-based literature search can miss relevant articles when the words used in a query differ from the terminology in an abstract. Long queries and complex Boolean expressions can also make search refinement difficult.

This project addresses these challenges through an approach that combines:

- LLM-assisted query planning and expansion
- PubMed / NCBI literature retrieval
- BM25 lexical search
- PubMedBERT-based semantic search
- Hybrid relevance ranking
- Maximal Marginal Relevance (MMR) reranking
- Evidence-focused summarization with source references

## Key Features

- **Biomedical literature search:** Retrieves research records through the PubMed / NCBI API.
- **Query planning:** Uses an LLM-based planner to expand natural-language questions into concepts, keywords, and synonyms.
- **Lexical retrieval:** Uses BM25 to rank documents containing relevant terms.
- **Semantic retrieval:** Uses PubMedBERT embeddings to identify articles with similar meaning, even when wording differs.
- **Hybrid ranking:** Combines lexical and semantic relevance to balance exact-term matching with contextual similarity.
- **Result diversification:** Applies MMR to reduce redundancy while preserving relevance.
- **Evidence summarization:** Generates summaries from retrieved biomedical content.
- **Source references:** Helps users trace results back to their original articles.
- **Web deployment:** Uses a modern web frontend and a containerized backend.

## How It Works

1. **Enter a query:** A user submits a biomedical research question.
2. **Plan the query:** An LLM-based planner extracts concepts, keywords, and related terms.
3. **Retrieve records:** The system searches PubMed / NCBI for relevant records and abstracts.
4. **Run lexical retrieval:** BM25 ranks articles by keyword relevance.
5. **Run semantic retrieval:** PubMedBERT embeddings represent the query and abstracts for semantic similarity matching.
6. **Combine rankings:** Hybrid scoring brings lexical and semantic results together.
7. **Rerank for diversity:** MMR selects relevant results while reducing near-duplicates.
8. **Summarize evidence:** The application presents selected evidence and source links through its interface.

## System Architecture

```text
User's biomedical question
             |
             v
    LLM-based query planner
             |
             v
   Query concepts and synonyms
             |
             v
    PubMed / NCBI API search
             |
       +-----+-----+
       |           |
       v           v
  BM25 lexical   PubMedBERT
   retrieval     embeddings
       |           |
       +-----+-----+
             |
             v
       Hybrid ranking
             |
             v
       MMR reranking
             |
             v
   Evidence selection and summary
             |
             v
     Web UI with source links
```

## Technology Stack

| Component | Technology |
|---|---|
| Biomedical literature | PubMed / NCBI API |
| Semantic embeddings | `pritamdeka/S-PubMedBERT-MS-MARCO` |
| Lexical retrieval | BM25 |
| Ranking | Hybrid lexical-semantic scoring |
| Diversification | Maximal Marginal Relevance (MMR) |
| Query planning / summarization | LLM API |
| Backend | Python API service, Docker |
| Frontend | Next.js, React, TypeScript |
| Frontend hosting | Vercel |
| Backend hosting | Azure Container Apps |
| Data storage | Azure Cosmos DB (NoSQL) |

*The stack above reflects the project documentation. Check the source folders and their dependency/configuration files for exact versions and current run commands.*

## Evaluation Results

The project documentation reports these results from a demo run:

| Metric | Reported value |
|---|---:|
| Precision@10 | 0.87 |
| Recall@10 | 0.95 |
| ROUGE-1 F1 | 0.45 |
| BERTScore F1 | 0.72 |
| End-to-end query time | 25.19 seconds |

These figures are reported demo results, not guaranteed performance for all queries. For formal reporting, document the evaluation dataset and relevance-judgment method and reproduce the measurements.

## Repository Structure

The repository includes separate frontend and backend source directories:

```text
Semantic-PubMed-Search-with-Hybrid-RAG-System/
├── medrag-frontend-main/
├── medrag_api-main/
├── .gitignore
├── LICENSE
└── README.md
```

Folder names may reflect the names of the source packages. Review each directory's own README, dependency files, and environment configuration for detailed setup instructions.

## Getting Started

The repository's documentation should be treated as the source of truth for exact setup commands. General steps:

1. Clone this repository.
2. Open the frontend and backend directories separately.
3. Follow the installation instructions and dependency files in each directory.
4. Configure required API keys, database credentials, and service endpoints using environment variables.
5. Start the backend and frontend using their documented commands.
6. Test with several biomedical questions and verify that results contain links to source articles.

### Clone the repository

```bash
git clone https://github.com/Seka6405/Semantic-PubMed-Search-with-Hybrid-RAG-System.git
cd Semantic-PubMed-Search-with-Hybrid-RAG-System
```

**Security:** Never commit API keys, access tokens, database credentials, or `.env` files. Use environment variables or your hosting provider's secret manager.

## Live Demo and Related Resources

- **GitHub repository:** [Semantic PubMed Search with Hybrid RAG System](https://github.com/Seka6405/Semantic-PubMed-Search-with-Hybrid-RAG-System)
- **Live application:** [Open the web app](https://medrag-frontend.vercel.app/login)
- **Demo video:** [Watch the demo](https://drive.google.com/file/d/1x7UYlHZy3r_EEDfQ_z4La_jVI2-85SuV/view?usp=sharing)
- **NCBI API documentation:** [NCBI APIs](https://www.ncbi.nlm.nih.gov/home/develop/api/)

## Future Improvements

- Create a reproducible evaluation dataset for biomedical queries.
- Compare BM25-only, semantic-only, and hybrid retrieval using the same test set.
- Improve caching, retries, rate-limit handling, and API timeouts.
- Add stronger checks to ensure summaries are grounded in cited articles.
- Measure latency for query planning, retrieval, reranking, and summarization separately.
- Expand automated tests for retrieval quality and API failure scenarios.

## References

- [Demystifying the Search Button](https://pmc.ncbi.nlm.nih.gov/articles/PMC4513072/)
- [Research Trend Visualization by MeSH Terms from PubMed](https://www.mdpi.com/1660-4601/15/6/1113)
- [MedGraph: Semantic Information Retrieval Using Knowledge Graph Embeddings](https://arxiv.org/abs/2112.06348)
- [NCBI API documentation](https://www.ncbi.nlm.nih.gov/home/develop/api/)

## Disclaimer

This project is intended for biomedical literature discovery and research support. It is not a medical device and does not provide a diagnosis or replace advice from qualified healthcare professionals.
