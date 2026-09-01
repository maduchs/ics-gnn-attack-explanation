# ICS/Network Attack Detection with Graph Neural Networks and RAG-Based Explanation

Code accompanying an MSc dissertation evaluating Graph Deviation Networks (GDN) and Temporal
Graph Convolutional Networks (T-GCN) for attack detection across four heterogeneous datasets:
BATADAL, SWaT, WADI, and UNSW-NB15, with a retrieval-augmented explanation layer built on top
of the BATADAL and SWaT detectors.

## Repository structure
ics-gnn-attack-explanation/
├── README.md
├── requirements.txt
├── .gitignore
└── notebooks/
├── batadal_pipeline.ipynb
├── swat_pipeline.ipynb
├── wadi_pipeline.ipynb
├── unsw15_pipeline.ipynb
├── batadal_rag_explanation.ipynb
└── swat_rag_explanation.ipynb

text

## What's here

**Detection pipelines** (`notebooks/`), one per dataset. Each trains classical baselines
(Random Forest, and where applicable Isolation Forest and Gradient-Boosted Trees) alongside GDN
and T-GCN, comparing correlation-based and Granger-causal graph construction, and evaluates
under an attack-disjoint, leakage-free split rather than a random row split.

- `batadal_pipeline.ipynb`
- `swat_pipeline.ipynb`
- `wadi_pipeline.ipynb`
- `unsw15_pipeline.ipynb`

**RAG explanation layers**, built on top of the BATADAL and SWaT detection pipelines. Each
retrieves a subgraph (implicated sensors, causal or correlated neighbours, and known attack
patterns) from a Neo4j knowledge graph and generates a natural-language explanation for a
flagged detection via the Groq API, with a lightweight automated quality check.

- `batadal_rag_explanation.ipynb`
- `swat_rag_explanation.ipynb`

## Setup

```bash
pip install -r requirements.txt
```

The RAG notebooks additionally need:
- A Neo4j instance (AuraDB free tier or local Docker/Desktop)
- A Groq API key

Both are entered via `getpass` at runtime. No credentials are stored in these notebooks.

## Datasets

Not included here due to size and licensing. Expected sources:
- BATADAL: [iTrust, SUTD](https://www.sutd.edu.sg/itrust/itrust-labs/datasets/dataset-characteristics/batadal/)
- SWaT: [iTrust, SUTD](https://itrust.sutd.edu.sg/testbeds/secure-water-treatment-swat/)
- WADI: [iTrust, SUTD](https://itrust.sutd.edu.sg/testbeds/water-distribution-wadi/)
- UNSW-NB15: [UNSW Canberra Cyber](https://research.unsw.edu.au/projects/unsw-nb15-dataset)

## Context

This repository extends detection work originally scoped in an earlier research proposal
(Cyber Security Research Methods module) into a full cross-dataset evaluation with an added
explanation layer, submitted as an MSc dissertation.
