# Literature Review: Graph Embeddings for Directed Graphs

## Overview

This directory contains a comprehensive literature review on graph embeddings for directed graphs, including survey papers, foundational methods, and recent advances (2013-2025).

## Contents

- **search_strategy.md** - Detailed search strategy and comprehensive listing of all papers found (126+ papers)
- **references.bib** - BibTeX file with all references (126+ entries)
- **pdfs/** - Directory containing downloaded PDFs (84 papers)

## Statistics

- **Total Papers Identified**: 126+
- **Survey Papers**: 9
- **Foundational Methods**: 4 (DeepWalk, LINE, node2vec, struc2vec)
- **Directed Graph-Specific Methods**: 5 (HOPE, ATP, DGCN, etc.)
- **GNN Architectures**: 6 (GCN, GraphSAGE, GAT, GIN, DiffPool, VGAE)
- **Transformer-Based Approaches**: 4 (Transformers for Directed Graphs, DAGformer, etc.)
- **Knowledge Graph Embeddings**: 3 (TransE, TransR, RotatE)
- **Additional Important Papers from Survey Analysis**: 13
  - Magnetic Laplacian methods (MagNet, MSGNN)
  - Directed graph contrastive learning (DiGCL)
  - Signed directed networks (SDGNN)
  - Motif-based methods (MotifNet)
  - Message passing frameworks (MPNN, GGNN)
  - Graph networks (Battaglia et al.)
  - Heterogeneous networks (HIN2Vec, HEBE)
  - Causal discovery (DAG-GNN, DAG-GCN)
  - Graph classification (DGCNN)
- **Additional Papers from Bibliography Analysis**: 8
  - Signed directed networks (SIDE)
  - Scalability methods (APPNP, SGC)
  - Global structure (GraRep)
  - Attributed networks (TADW)
  - Spectral methods (GWNN, ChebNet)
  - Large-scale deployment (PinSage)
- **Additional Papers from Systematic Survey Bibliography Review**: 12
  - Foundational spectral methods (Bruna 2014, Laplacian Eigenmaps)
  - Scalability (FastGCN)
  - Learned random walks (Watch Your Step)
  - Probabilistic embeddings (Graph2Gauss)
  - Graph generation (GraphRNN, Junction Tree VAE, MolGAN)
  - Graph similarity (Graph Matching Networks)
  - Benchmarking (Open Graph Benchmark)
  - Original GNN model (Scarselli 2009)
  - Graph kernels (Weisfeiler-Lehman)
- **Advanced Topics - Pooling, Contrastive Learning, Expressiveness, Temporal**: 15
  - Graph pooling (DiffPool, SAGPool, Graph U-Net)
  - Contrastive learning (GraphCL, GRACE, BGRL, GraphMAE)
  - Expressiveness theory (k-GNN, Provably Powerful Networks)
  - GNN limitations (Over-squashing via curvature)
  - Heterogeneous/relational (R-GCN)
  - Graph Transformers (GraphGPS, Graphormer)
  - Temporal graphs (TGN)
  - Hyperbolic embeddings (Hyperbolic GNN)
- **Scalability, Temporal, and Specialized Applications**: 16
  - Expressiveness (GIN - provably equal to WL test)
  - Temporal/dynamic graphs (EvolveGCN, JODIE, TGAT, DySAT)
  - Additional pooling methods (MinCutPool, EdgePool)
  - Foundational hyperbolic embeddings (Poincaré 2017)
  - GNN-based recommendation (NGCF, LightGCN)
  - Scalable training methods (GraphSAINT, ClusterGCN, LADIES)
  - Graph structure learning (IDGL, LDS-GNN)
  - Causal discovery (NOTEARS for DAG learning)
- **Recent Advances (2024-2025)**: 12
  - Latest spectral methods (WaveGC with Chebyshev wavelets)
  - Graph foundation models (paradigm shift toward pre-training)
  - End-to-end attention approaches (outperform message passing on 70+ tasks)
  - Heterophily learning handbook (comprehensive resource)
  - Temporal graph learning 2024 survey
  - E(n) equivariant GNNs (geometric deep learning)
  - Geometric GNN survey (SE(3)/E(3) equivariance)
  - Graph-enhanced transformers (DGTN with diffusive attention)
  - GNN explainability (GNNExplainer and 2024 extensions)
  - Graph-aware attention mechanisms (isomorphic attention, longer context)
  - Dynamic temporal learning advances
- **Other Categories**: Link prediction, temporal graphs, applications, self-supervised learning, etc.
- **Downloaded PDFs**: 84 papers

## Key Categories

### 1. Survey Papers (2020-2025)
Most recent comprehensive surveys covering the field, including:
- Towards Data-centric Machine Learning on Directed Graphs (2024)
- Comprehensive Survey on Deep Graph Representation Learning (2024)
- Temporal GNN Survey (2023)

### 2. Foundational Methods (2014-2017)
Classic papers that established the field:
- DeepWalk (2014)
- LINE (2015)
- node2vec (2016)
- struc2vec (2017)

### 3. Directed Graph-Specific Methods
Papers specifically addressing directed graphs:
- HOPE: Asymmetric Transitivity Preserving Graph Embedding (2016)
- Directed Graph Convolutional Network (2020)
- Node Representation Learning for Directed Graphs (2018)

### 4. Graph Neural Networks
Foundational GNN architectures:
- GCN (2017)
- GraphSAGE (2017)
- GAT (2018)
- GIN (2018/2019)

### 5. Recent Advances (2023-2024)
Latest developments including:
- Graph Transformers for directed graphs
- Self-supervised learning on graphs
- Improved link prediction methods

## How to Use This Review

1. **Start with surveys**: Read the survey papers in `search_strategy.md` section 1 to get an overview of the field
2. **Understand foundations**: Review foundational methods (DeepWalk, LINE, node2vec)
3. **Focus on directed graphs**: Study HOPE and other directed-specific methods
4. **Explore GNNs**: Learn about modern GNN architectures
5. **Check recent work**: Review 2023-2024 papers for state-of-the-art

## Citation

To cite papers from this review, use the BibTeX entries in `references.bib`.

## PDF Downloads

PDFs are organized by paper identifier. For example:
- `kipf2017_gcn.pdf` - Semi-Supervised Classification with GCNs (2017)
- `ou2016_hope.pdf` - HOPE: Asymmetric Transitivity Preserving (2016)
- `directedgraph_survey2024.pdf` - Most recent directed graph survey (2024)

## Notes

- Some papers may not have freely available PDFs (e.g., papers behind paywalls)
- arXiv preprints are prioritized for availability
- Conference proceedings PDFs are included where available

## Search Sources Used

1. Google Scholar
2. arXiv
3. ACM Digital Library
4. IEEE Xplore
5. NeurIPS/ICML/ICLR proceedings
6. Direct paper searches

## Date Generated

November 14, 2025

## Recommended Reading Order for Beginners

1. **Start here**: Cai et al. 2018 - Comprehensive Survey of Graph Embedding
2. **Foundational**: DeepWalk, LINE, node2vec
3. **Directed-specific**: HOPE (2016)
4. **Modern GNNs**: Kipf & Welling GCN (2017), then GraphSAGE, GAT
5. **Recent surveys**: 2024 surveys for state-of-the-art
6. **Specialized**: Pick papers based on your specific interest (transformers, temporal, knowledge graphs, etc.)
