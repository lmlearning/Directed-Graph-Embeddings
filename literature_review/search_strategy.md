# Literature Review: Graph Embeddings for Directed Graphs

## Search Strategy

### Keywords and Search Terms
- Primary: "directed graph embedding", "directed graph representation learning"
- Secondary: "graph neural network directed", "asymmetric graph embedding"
- Methods: "DeepWalk", "Node2Vec", "HOPE", "struc2vec", "GraphSAGE"
- Applications: "directed network embedding", "link prediction directed graph"

### Search Sources
1. Google Scholar
2. arXiv
3. ACM Digital Library
4. IEEE Xplore
5. NeurIPS/ICML/ICLR proceedings

### Inclusion Criteria
- Papers focusing on directed graph embeddings
- Survey papers on graph representation learning
- Foundational papers on graph embeddings (even if not directed-specific)
- Recent papers (2015-2025) with focus on state-of-the-art methods

### Search Phases
1. **Survey and Review Papers** - Get overview of the field
2. **Foundational Papers** - Seminal works in graph embeddings
3. **Directed-Specific Methods** - Papers specifically addressing directed graphs
4. **Recent Advances** - Latest developments (2020-2025)

---

## Papers Found

### 1. Survey Papers (2020-2025)

#### 1.1 **Towards Data-centric Machine Learning on Directed Graphs: a Survey** (2024)
- **Authors**: Recent comprehensive survey
- **Publication**: arXiv:2412.01849 (December 2024)
- **URL**: https://arxiv.org/abs/2412.01849
- **Summary**: Comprehensive review of directed graph learning from a data-centric perspective, exploring applications of directed GNNs across 10+ domains
- **Key Focus**: Directed graphs, heterogeneous graphs, hypergraphs

#### 1.2 **A Comprehensive Survey on Deep Graph Representation Learning** (2024)
- **Authors**: Wei Ju et al. (16 authors)
- **Publication**: arXiv:2304.05055 (updated Feb 2024); Neural Networks
- **URL**: https://arxiv.org/abs/2304.05055
- **Summary**: Systematically summarizes GNN architectures and advanced learning paradigms including supervised/semi-supervised learning, graph self-supervised learning, and graph structure learning
- **Key Focus**: Deep graph representation learning, GNN architectures, learning paradigms

#### 1.3 **A Survey on Graph Representation Learning Methods** (2024)
- **Authors**: Multiple authors
- **Publication**: ACM Transactions on Intelligent Systems and Technology, 2024
- **URL**: https://dl.acm.org/doi/10.1145/3633518
- **Summary**: Reviews graph-embedding methods in both traditional and GNN-based categories for both static and dynamic graphs
- **Key Focus**: Static and dynamic graphs, traditional and GNN-based methods

#### 1.4 **A Comprehensive Survey of Graph Embedding: Problems, Techniques and Applications** (2018)
- **Authors**: Multiple authors
- **Publication**: IEEE TKDE 2018; arXiv:1709.07604
- **URL**: https://arxiv.org/abs/1709.07604
- **Summary**: Comprehensive survey of graph embedding problems, techniques, and applications
- **Key Focus**: General graph embedding methods

#### 1.5 **Graph Representation Learning and Its Applications: A Survey** (2023)
- **Authors**: Multiple authors
- **Publication**: Sensors (Basel), April 2023
- **URL**: https://www.mdpi.com/1424-8220/23/8/4168
- **Summary**: Shows popularity trends of different graph representation learning models from 2010 to 2022
- **Key Focus**: GNN, GCN, Graph Transformer models

#### 1.6 **A review of graph neural networks: concepts, architectures** (2024)
- **Authors**: Multiple authors
- **Publication**: Journal of Big Data (2024)
- **URL**: https://journalofbigdata.springeropen.com/counter/pdf/10.1186/s40537-023-00876-4.pdf
- **Summary**: Comprehensive review of GNN concepts, architectures, training techniques, applications
- **Key Focus**: Holistic understanding of GNNs with literature from 2018-2023

#### 1.7 **Self-Supervised Learning of Graph Neural Networks: A Unified Review** (2023)
- **Authors**: Multiple authors
- **Publication**: IEEE TPAMI (February 2023)
- **URL**: Available on PMC
- **Summary**: Unified review of self-supervised learning methods for GNNs, categorizing SSL methods into contrastive and predictive models
- **Key Focus**: Self-supervised learning, contrastive learning on graphs

#### 1.8 **Knowledge Graph Embeddings Survey** (2024)
- **Authors**: Multiple authors
- **Publication**: arXiv:2410.14733 (October 2024)
- **URL**: https://arxiv.org/pdf/2410.14733
- **Summary**: Explores relation pattern modeling and dynamic KGE settings in directed graph structures
- **Key Focus**: Knowledge graphs as directed graphs, relation embeddings

#### 1.9 **Graph Neural Networks for temporal graphs: State of the art, open challenges** (2023)
- **Authors**: Multiple authors
- **Publication**: arXiv:2302.01018 (August 2023); TMLR
- **URL**: https://arxiv.org/abs/2302.01018
- **Summary**: First comprehensive overview of temporal GNN with novel taxonomy
- **Key Focus**: Temporal graphs (assumes directed graphs)

---

### 2. Foundational Methods (2014-2017)

#### 2.1 **DeepWalk: Online Learning of Social Representations** (2014)
- **Authors**: Stony Brook University researchers
- **Publication**: 2014
- **URL**: Paper from Stony Brook
- **Summary**: Introduces random walk-based graph embedding, treating walks as sentences for Word2Vec
- **Key Focus**: Random walks, unsupervised learning
- **Note**: Context graphs in DeepWalk make source/context roles indistinguishable in directed networks

#### 2.2 **node2vec: Scalable Feature Learning for Networks** (2016)
- **Authors**: Aditya Grover, Jure Leskovec (Stanford)
- **Publication**: KDD 2016
- **URL**: https://cs.stanford.edu/people/jure/pubs/node2vec-kdd16.pdf
- **Summary**: Extends DeepWalk with biased random walks; applies to any (un)directed, (un)weighted network
- **Key Focus**: Biased random walks, flexible exploration strategies

#### 2.3 **LINE: Large-scale Information Network Embedding** (2015)
- **Authors**: Tang et al.
- **Publication**: WWW 2015; arXiv:1503.03578
- **URL**: https://arxiv.org/abs/1503.03578
- **Summary**: Scalable for directed, undirected, and/or weighted networks; preserves first-order and second-order proximity
- **Key Focus**: Large-scale networks, millions of nodes/edges
- **Performance**: Can embed networks with millions of vertices and billions of edges in hours

#### 2.4 **struc2vec: Learning Node Representations from Structural Identity** (2017)
- **Authors**: Leo Ribeiro et al.
- **Publication**: KDD 2017; arXiv:1704.03165
- **URL**: https://arxiv.org/abs/1704.03165
- **Summary**: Captures structural identity regardless of network distance; uses hierarchy to measure node similarity at different scales
- **Key Focus**: Structural roles, structural identity
- **GitHub**: https://github.com/leoribeiro/struc2vec

---

### 3. Directed Graph-Specific Methods

#### 3.1 **HOPE: Asymmetric Transitivity Preserving Graph Embedding** (2016)
- **Authors**: Ou, Mingdong; Cui, Peng; Pei, Jian; Zhang, Ziwei; Zhu, Wenwu
- **Publication**: KDD 2016
- **URL**: https://www.kdd.org/kdd2016/papers/files/rfp0184-ouA.pdf
- **URL**: https://dl.acm.org/doi/10.1145/2939672.2939751
- **Summary**: Designed specifically for directed graphs; preserves asymmetric transitivity and high-order proximities
- **Key Focus**: Asymmetric transitivity, directed edges
- **Performance**: Outperforms state-of-art in reconstruction, link prediction, vertex recommendation
- **GitHub**: https://github.com/ZW-ZHANG/HOPE

#### 3.2 **ATP: Directed Graph Embedding with Asymmetric Transitivity Preservation** (2018)
- **Authors**: Related to HOPE
- **Publication**: arXiv:1811.00839 (AAAI 2019)
- **URL**: https://arxiv.org/abs/1811.00839
- **Summary**: Extension of asymmetric transitivity preserving methods
- **Key Focus**: Asymmetric transitivity in directed graphs

#### 3.3 **Node Representation Learning for Directed Graphs** (2018)
- **Authors**: Multiple authors
- **Publication**: arXiv:1810.09176
- **URL**: https://arxiv.org/abs/1810.09176
- **Summary**: Proposes maintaining separate embedding spaces for two distinct node roles induced by edge directionality
- **Key Focus**: Dual embeddings for directed graphs

#### 3.4 **Directed Graph Convolutional Network (DGCN)** (2020)
- **Authors**: Tong et al.
- **Publication**: arXiv:2004.13970 (April 2020)
- **URL**: https://arxiv.org/abs/2004.13970
- **Summary**: New GCN model for directed graphs using first- and second-order proximity
- **Key Focus**: Spectral-based convolution on directed graphs
- **Implementation**: PyTorch implementation available

#### 3.5 **A Benchmark on Directed Graph Representation Learning in Hardware Designs** (2024)
- **Authors**: Multiple authors
- **Publication**: arXiv:2410.06460 (October 2024)
- **URL**: https://arxiv.org/abs/2410.06460
- **Summary**: Evaluates 21 DGRL models using GNNs and graph transformers with positional encodings
- **Key Focus**: Hardware design applications, benchmark evaluation

---

### 4. Graph Neural Network Architectures

#### 4.1 **Semi-Supervised Classification with Graph Convolutional Networks** (2017)
- **Authors**: Thomas N. Kipf, Max Welling
- **Publication**: ICLR 2017; arXiv:1609.02907
- **URL**: https://arxiv.org/abs/1609.02907
- **Summary**: Foundational GCN paper; scalable approach using localized first-order approximation of spectral convolutions
- **Key Focus**: Semi-supervised learning, spectral methods
- **Impact**: Highly influential in graph neural networks
- **GitHub**: https://github.com/tkipf/gcn

#### 4.2 **GraphSAGE: Inductive Representation Learning on Large Graphs** (2017)
- **Authors**: William L. Hamilton, Rex Ying, Jure Leskovec
- **Publication**: NIPS 2017; arXiv:1706.02216
- **URL**: https://arxiv.org/abs/1706.02216
- **Summary**: Inductive framework that learns aggregation functions; generalizes to unseen nodes
- **Key Focus**: Inductive learning, sampling and aggregating
- **Project**: https://snap.stanford.edu/graphsage/
- **GitHub**: https://github.com/williamleif/GraphSAGE

#### 4.3 **Graph Attention Networks (GAT)** (2018)
- **Authors**: Petar Veličković, Guillem Cucurull, et al., Yoshua Bengio
- **Publication**: ICLR 2018; arXiv:1710.10903
- **URL**: https://arxiv.org/abs/1710.10903
- **Summary**: Uses masked self-attentional layers; assigns different weights to different neighbors
- **Key Focus**: Attention mechanisms on graphs
- **GitHub**: https://github.com/PetarV-/GAT

#### 4.4 **How Powerful are Graph Neural Networks? (GIN)** (2018)
- **Authors**: Xu et al.
- **Publication**: ICLR 2019; arXiv:1810.00826
- **URL**: https://arxiv.org/abs/1810.00826
- **Summary**: Proves GIN is as powerful as Weisfeiler-Lehman test; maximizes representational power
- **Key Focus**: Expressiveness, graph isomorphism
- **Theoretical**: Connection to WL-test

#### 4.5 **Hierarchical Graph Representation Learning with Differentiable Pooling (DiffPool)** (2018)
- **Authors**: Rex Ying et al.
- **Publication**: NeurIPS 2018; arXiv:1806.08804
- **URL**: https://arxiv.org/abs/1806.08804
- **Summary**: Differentiable graph pooling for hierarchical representations
- **Key Focus**: Graph classification, hierarchical pooling
- **Performance**: 5-10% accuracy improvement on benchmarks
- **GitHub**: https://github.com/RexYing/diffpool

#### 4.6 **Variational Graph Auto-Encoders (VGAE)** (2016)
- **Authors**: Thomas N. Kipf, Max Welling
- **Publication**: arXiv:1611.07308 (November 2016)
- **URL**: https://arxiv.org/abs/1611.07308
- **Summary**: VAE framework for unsupervised learning on graphs; GCN encoder + inner product decoder
- **Key Focus**: Unsupervised learning, link prediction
- **GitHub**: https://github.com/tkipf/gae

---

### 5. Transformer-Based Approaches for Directed Graphs (2023-2024)

#### 5.1 **Transformers Meet Directed Graphs** (2023)
- **Authors**: Multiple authors
- **Publication**: ICML 2023; arXiv:2302.00049
- **URL**: https://arxiv.org/abs/2302.00049
- **Summary**: Direction-aware positional encodings: (1) Magnetic Laplacian eigenvectors, (2) directional random walk encodings
- **Key Focus**: Direction-aware transformers
- **Performance**: 14.7% relative improvement on Open Graph Benchmark Code2

#### 5.2 **Transformers over Directed Acyclic Graphs (DAGformer)** (2023)
- **Authors**: Luo et al.
- **Publication**: NeurIPS 2023
- **URL**: https://openreview.net/forum?id=g49s1N5nmO
- **Summary**: Efficient attention mechanism for DAGs with positional encoding of partial order
- **Key Focus**: DAGs, computational efficiency
- **GitHub**: https://github.com/LUOyk1999/DAGformer

#### 5.3 **Directionality in Graph Transformers** (2024)
- **Authors**: Multiple authors
- **Publication**: ICLR 2024
- **URL**: https://openreview.net/forum?id=Yp01vcQSNl
- **Summary**: Dual encodings for source/target roles with directional attention module
- **Key Focus**: Edge directionality, dual encodings

#### 5.4 **Directed Acyclic Graph Neural Networks (DAGNN)** (2021)
- **Authors**: Thost et al.
- **Publication**: ICLR 2021; arXiv:2101.07965
- **URL**: https://arxiv.org/abs/2101.07965
- **Summary**: Processes information according to partial order flow in DAGs
- **Key Focus**: DAGs, partial ordering as inductive bias
- **GitHub**: https://github.com/vthost/DAGNN

---

### 6. Knowledge Graph Embeddings (Directed Relations)

#### 6.1 **TransE: Translating Embeddings for Modeling Multi-relational Data** (2013)
- **Authors**: Bordes et al.
- **Publication**: NIPS 2013
- **URL**: https://proceedings.neurips.cc/paper/2013/file/1cecc7a77928ca8133fa24680a88d2f9-Paper.pdf
- **Summary**: Translation-based model: h + r ≈ t for triplets (h, r, t)
- **Key Focus**: Knowledge graphs, directed relations
- **Limitation**: Cannot handle non-1-to-1 relationships well

#### 6.2 **TransR: Learning Entity and Relation Embeddings for Knowledge Graph Completion** (2015)
- **Authors**: Lin et al.
- **Publication**: AAAI 2015
- **URL**: https://www.aaai.org/ocs/index.php/AAAI/AAAI15/paper/view/9571
- **Summary**: Separate entity and relation spaces with projection matrices
- **Key Focus**: Relation-specific embeddings
- **Improvement**: Addresses TransE's limitation with complex relations

#### 6.3 **RotatE: Knowledge Graph Embedding by Relational Rotation in Complex Space** (2019)
- **Authors**: Sun et al.
- **Publication**: ICLR 2019; arXiv:1902.10197
- **URL**: https://arxiv.org/abs/1902.10197
- **Summary**: Models relations as rotations in complex vector space; handles symmetry, antisymmetry, inversion, composition
- **Key Focus**: Rotation in complex space, relation patterns
- **Performance**: State-of-the-art on multiple KG benchmarks
- **GitHub**: https://github.com/DeepGraphLearning/KnowledgeGraphEmbedding

---

### 7. Heterogeneous Network Embeddings

#### 7.1 **metapath2vec: Scalable Representation Learning for Heterogeneous Networks** (2017)
- **Authors**: Yuxiao Dong, Nitesh V. Chawla, Ananthram Swami
- **Publication**: KDD 2017
- **URL**: https://ericdongyx.github.io/papers/KDD17-dong-chawla-swami-metapath2vec.pdf
- **Summary**: Meta-path-based random walks for heterogeneous networks; includes metapath2vec++
- **Key Focus**: Heterogeneous networks, meta-paths
- **Performance**: Outperforms state-of-art in node classification, clustering, similarity search

---

### 8. Temporal and Dynamic Graph Methods (2023-2024)

#### 8.1 **TimeGNN: Temporal Dynamic Graph Learning for Time Series Forecasting** (2023)
- **Authors**: Multiple authors
- **Publication**: arXiv:2307.14680
- **URL**: https://arxiv.org/html/2307.14680
- **Summary**: Learns dynamic temporal graphs that are forward and directed
- **Key Focus**: Temporal graphs, time series forecasting

#### 8.2 **GraphMixer** (2023)
- **Authors**: Cong et al.
- **Publication**: 2023
- **Summary**: Shows RNN and self-attention not always necessary for dynamic link prediction; uses MLPs and mean-pooling
- **Key Focus**: Dynamic link prediction, simplicity

---

### 9. Link Prediction on Directed Graphs

#### 9.1 **Link Prediction Based on Graph Neural Networks** (2018)
- **Authors**: Muhan Zhang et al.
- **Publication**: NeurIPS 2018; arXiv:1802.09691
- **URL**: https://arxiv.org/abs/1802.09691
- **Summary**: GNN-based link prediction methods
- **Key Focus**: Link prediction, graph neural networks

#### 9.2 **Rethinking Link Prediction for Directed Graphs** (2025)
- **Authors**: Recent work
- **Publication**: arXiv:2502.05724
- **URL**: https://arxiv.org/html/2502.05724
- **Summary**: Recent advances including CoBA, BLADE, DirGNN, LightDiC, DUPLEX
- **Key Focus**: Directed link prediction, asymmetric losses

#### 9.3 **Evaluating Graph Neural Networks for Link Prediction** (2023)
- **Authors**: Multiple authors
- **Publication**: arXiv:2306.10453 (June 2023)
- **URL**: https://arxiv.org/abs/2306.10453
- **Summary**: Addresses current pitfalls and proposes new benchmarking
- **Key Focus**: Evaluation methodology

---

### 10. Applications

#### 10.1 **Influence Maximization in Social Networks** (2022)
- **Authors**: Multiple authors
- **Publication**: Information Sciences 2022
- **URL**: https://www.sciencedirect.com/science/article/abs/pii/S0020025522006697
- **Summary**: Uses struc2vec embeddings for influence maximization
- **Key Focus**: Social networks, influence propagation

#### 10.2 **Citation Network Embedding**
- **Venue**: Various
- **Summary**: Citation networks as DAGs; applications in paper recommendation and analysis
- **Key Focus**: Academic citation graphs
- **Example Dataset**: ogbn-arxiv (directed citation network)

#### 10.3 **Spectral Graph Convolution for Signed Directed Graphs** (2023)
- **Authors**: Multiple authors
- **Publication**: Neural Networks 2023
- **URL**: https://www.sciencedirect.com/science/article/pii/S0893608023002502
- **Summary**: Complex Hermitian adjacency matrix with magnetic Laplacian
- **Key Focus**: Signed directed graphs, spectral methods

---

### 11. Self-Supervised and Contrastive Learning on Graphs (2023-2024)

#### 11.1 **GTC: GNN-Transformer Co-contrastive Learning** (2024)
- **Authors**: Multiple authors
- **Publication**: arXiv:2403.15520 (2024)
- **URL**: https://arxiv.org/abs/2403.15520
- **Summary**: First work combining GNN and Transformer for cross-view contrastive learning
- **Key Focus**: Heterogeneous graphs, co-contrastive learning

#### 11.2 **Self-supervised Heterogeneous Graph Neural Network with Co-contrastive Learning** (2021)
- **Authors**: Multiple authors
- **Publication**: KDD 2021; arXiv:2105.09111
- **URL**: https://arxiv.org/abs/2105.09111
- **Summary**: Co-contrastive learning for heterogeneous graphs
- **Key Focus**: Heterogeneous graphs, self-supervised learning

---

### 12. Theoretical and Expressiveness

#### 12.1 **Beyond Message Passing: Physics-Inspired Paradigm for GNNs**
- **Publication**: The Gradient
- **URL**: https://thegradient.pub/graph-neural-networks-beyond-message-passing-and-weisfeiler-lehman/
- **Summary**: Discusses limitations of message passing and new paradigms
- **Key Focus**: Expressiveness, theoretical foundations

#### 12.2 **Dir-GNN: Machine Learning Model for Directed Graphs**
- **GitHub**: https://github.com/emalgorithm/directed-graph-neural-network
- **Summary**: Extends any MPNN to account for edge directionality via separate aggregations
- **Key Focus**: Directional message passing

#### 12.3 **Improving Graph Neural Networks by Learning Continuous Edge Directions** (2024)
- **Publication**: arXiv:2410.14109 (October 2024)
- **URL**: https://arxiv.org/html/2410.14109
- **Summary**: Recent work on continuous edge direction learning
- **Key Focus**: Edge directionality, expressive GNNs

---

### 13. Additional Important Papers from Survey Analysis

#### 13.1 **MagNet: A Neural Network for Directed Graphs** (2021)
- **Authors**: Zhang et al.
- **Publication**: NeurIPS 2021; arXiv:2102.11391
- **URL**: https://arxiv.org/abs/2102.11391
- **Summary**: GNN for directed graphs based on complex Hermitian matrix (magnetic Laplacian); encodes undirected structure in magnitude and directional info in phase
- **Key Focus**: Magnetic Laplacian, spectral methods for directed graphs
- **Innovation**: "Charge" parameter attunes spectral information to variation among directed cycles

#### 13.2 **MSGNN: Magnetic Signed Graph Neural Network** (2022)
- **Authors**: He, Perlmutter, Reinert, Cucuringu
- **Publication**: Learning on Graphs Conference (LoG) 2022
- **URL**: https://proceedings.mlr.press/v198/he22c.html
- **Summary**: Natural generalization of both signed Laplacian and magnetic Laplacian; effective for incorporating signed and directional information
- **Key Focus**: Signed directed graphs, spectral GNN

#### 13.3 **DiGCL: Directed Graph Contrastive Learning** (2021)
- **Authors**: Tong, Zekun; Liang, Yuxuan; et al.
- **Publication**: NeurIPS 2021
- **URL**: https://openreview.net/forum?id=s6JD_xBS31
- **Summary**: First contrastive learning framework for directed graphs; uses Laplacian perturbation for data augmentation
- **Key Focus**: Self-supervised learning on directed graphs
- **Innovation**: Multi-task curriculum learning from easy-to-difficult contrastive views
- **GitHub**: https://github.com/flyingtango/DiGCL

#### 13.4 **SDGNN: Learning Node Representation for Signed Directed Networks** (2021)
- **Authors**: Huang, Junjie; Shen, Huawei; Hou, Liang; Cheng, Xueqi
- **Publication**: AAAI 2021; arXiv:2101.02390
- **URL**: https://arxiv.org/abs/2101.02390
- **Summary**: Novel GNN for signed directed networks; reconstructs link signs, directions, and signed directed triangles
- **Key Focus**: Signed directed graphs, social network analysis
- **Theory**: Based on status theory and balance theory from sociology
- **GitHub**: https://github.com/huangjunjie-cs/SiGAT

#### 13.5 **DGCNN: Deep Graph CNN** (2018)
- **Authors**: Zhang, Muhan; Cui, Zhicheng; Neumann, Marion; Chen, Yixin
- **Publication**: AAAI 2018
- **URL**: https://muhanzhang.github.io/papers/AAAI_2018_DGCNN.pdf
- **Summary**: End-to-end deep learning architecture for graph classification; propagation-based graph convolution + novel SortPooling layer
- **Key Focus**: Graph classification, end-to-end learning
- **Innovation**: SortPooling layer sorts vertex representations instead of summing
- **GitHub**: https://github.com/muhanzhang/DGCNN

#### 13.6 **MotifNet: Motif-based Graph Convolutional Network for Directed Graphs** (2018)
- **Authors**: Monti, Federico; Otness, Karl; Bronstein, Michael M.
- **Publication**: IEEE Data Science Workshop 2018; arXiv:1802.01572
- **URL**: https://arxiv.org/abs/1802.01572
- **Summary**: Graph CNN for directed graphs exploiting local graph motifs; addresses limitation of spectral CNNs' assumption of undirected graphs
- **Key Focus**: Motif-based learning, directed graph convolution
- **Innovation**: Motif adjacency matrices from directed motifs

#### 13.7 **Gated Graph Sequence Neural Networks (GGNN)** (2016)
- **Authors**: Li, Yujia; Tarlow, Daniel; Brockschmidt, Marc; Zemel, Richard
- **Publication**: ICLR 2016; arXiv:1511.05493
- **URL**: https://arxiv.org/abs/1511.05493
- **Summary**: Modifies GNNs to use gated recurrent units and extends to output sequences
- **Key Focus**: Gated recurrence, sequence prediction on graphs
- **Applications**: Chemistry, natural language semantics, social networks, knowledge bases
- **GitHub**: Multiple implementations available

#### 13.8 **Neural Message Passing for Quantum Chemistry (MPNN)** (2017)
- **Authors**: Gilmer, Justin; Schoenholz, Samuel S.; Riley, Patrick F.; Vinyals, Oriol; Dahl, George E.
- **Publication**: ICML 2017; arXiv:1704.01212
- **URL**: https://arxiv.org/abs/1704.01212
- **Summary**: Unified framework for graph neural networks; reformulates existing models as Message Passing Neural Networks
- **Key Focus**: Message passing framework, molecular property prediction
- **Innovation**: Two-phase forward pass (message passing + readout); trivially extends to directed multigraphs
- **Impact**: State-of-the-art on molecular property prediction benchmarks

#### 13.9 **Relational Inductive Biases, Deep Learning, and Graph Networks** (2018)
- **Authors**: Battaglia, Peter W. et al. (27 authors from DeepMind, Google Brain, MIT, Edinburgh)
- **Publication**: arXiv:1806.01261 (June 2018)
- **URL**: https://arxiv.org/abs/1806.01261
- **Summary**: Presents "graph network" as building block with strong relational inductive bias; generalizes various graph neural network approaches
- **Key Focus**: Relational reasoning, combinatorial generalization, graph networks framework
- **Impact**: Highly influential position paper on structured representations in AI
- **Resources**: Open-source software library released

#### 13.10 **HIN2Vec: Heterogeneous Information Network Embedding** (2017)
- **Authors**: Fu, Tao-yang; Lee, Wang-Chien; Lei, Zhen
- **Publication**: CIKM 2017
- **Summary**: Neural network model capturing semantics in HINs via meta-paths; predicts meta-path instances between node pairs
- **Key Focus**: Heterogeneous networks, meta-path-based learning
- **Performance**: Outperforms state-of-art in node classification and link prediction

#### 13.11 **HEBE: HyperEdge-Based Embedding** (2017)
- **Authors**: Multiple authors
- **Publication**: 2017
- **Summary**: Generic framework for learning object embeddings with events in heterogeneous networks using hyperedges
- **Key Focus**: Event-based modeling, heterogeneous networks
- **Innovation**: Models proximity in events; robust to data sparseness and scalable

#### 13.12 **DAG-GNN: Directed Acyclic Graph Structure Learning with GNNs** (2019)
- **Authors**: Yu et al.
- **Publication**: ICML 2019
- **URL**: https://proceedings.mlr.press/v97/yu19a.html
- **Summary**: Generalizes NOTEARS algorithm for DAG structure learning using variational autoencoder framework
- **Key Focus**: Causal discovery, DAG structure learning
- **Applications**: Causal inference, structural equation models

#### 13.13 **DAG-GCN: Directed Acyclic Causal Graph Discovery** (2023)
- **Authors**: Multiple authors
- **Publication**: 2023
- **Summary**: Causal graph discovery from real-world data using GCNs; formulates DAG learning as continuous optimization
- **Key Focus**: Causal discovery, directed acyclic graphs
- **Performance**: Lowest structural Hamming distance on benchmark datasets

---

### 14. Additional Papers from Bibliography Analysis

#### 14.1 **SIDE: Representation Learning in Signed Directed Networks** (2018)
- **Authors**: Kim, Junghwan; Park, Haekyu; Lee, Ji-Eun; Kang, U
- **Publication**: WWW 2018
- **URL**: https://datalab.snu.ac.kr/side/
- **Summary**: General network embedding method representing both sign and direction of edges; formulates likelihood over direct and indirect signed connections
- **Key Focus**: Signed directed networks, trust/distrust relationships
- **Performance**: Linear scalability with optimization techniques
- **Code**: Available at project site

#### 14.2 **APPNP: Predict then Propagate** (2019)
- **Authors**: Klicpera; Bojchevski; Günnemann
- **Publication**: ICLR 2019; arXiv:1810.05997
- **URL**: https://arxiv.org/abs/1810.05997
- **Summary**: Fast approximation using relationship between GCN and PageRank; improved propagation based on personalized PageRank
- **Key Focus**: Large adjustable neighborhoods, scalability
- **Innovation**: Separates neural network transformation from propagation
- **GitHub**: https://github.com/benedekrozemberczki/APPNP

#### 14.3 **GraRep: Learning Graph Representations with Global Structural Information** (2015)
- **Authors**: Cao, Shaosheng; Lu, Wei; Xu, Qiongkai
- **Publication**: CIKM 2015
- **Summary**: Integrates global structural information via k-step relational information; preserves k-order proximity
- **Key Focus**: Global graph structure, higher-order proximity
- **Performance**: Outperforms state-of-art in clustering, classification, visualization
- **GitHub**: https://github.com/benedekrozemberczki/GraRep

#### 14.4 **TADW: Network Representation Learning with Rich Text Information** (2015)
- **Authors**: Yang, Cheng; Liu, Zhiyuan; Zhao, Deli; Sun, Maosong; Chang, Edward Y.
- **Publication**: IJCAI 2015
- **Summary**: Proves DeepWalk equivalence to matrix factorization; incorporates text features via inductive matrix factorization
- **Key Focus**: Text-attributed networks, matrix factorization
- **Innovation**: Theoretical connection between DeepWalk and matrix factorization
- **GitHub**: https://github.com/benedekrozemberczki/TADW

#### 14.5 **Graph Wavelet Neural Network (GWNN)** (2019)
- **Authors**: Xu, Bingbing; Shen, Huawei; Cao, Qi; Qiu, Yunqi; Cheng, Xueqi
- **Publication**: ICLR 2019; arXiv:1904.07785
- **URL**: https://arxiv.org/abs/1904.07785
- **Summary**: Leverages graph wavelet transform instead of graph Fourier transform; fast algorithm without eigendecomposition
- **Key Focus**: Spectral graph learning, computational efficiency
- **Advantages**: Sparse and localized wavelets, high interpretability
- **GitHub**: https://github.com/benedekrozemberczki/GraphWaveletNeuralNetwork

#### 14.6 **ChebNet: Spectral Filtering with Chebyshev Polynomials** (2016)
- **Authors**: Defferrard, Michaël; Bresson, Xavier; Vandergheynst, Pierre
- **Publication**: NIPS 2016; arXiv:1606.09375
- **URL**: https://arxiv.org/abs/1606.09375
- **Summary**: Generalizes CNNs to graphs using spectral graph theory; approximates spectral filters with Chebyshev polynomials
- **Key Focus**: Spectral methods, computational efficiency
- **Performance**: Linear computational complexity, universal to any graph structure
- **GitHub**: https://github.com/mdeff/cnn_graph

#### 14.7 **PinSage: Graph Convolutional Networks for Web-Scale Recommender Systems** (2018)
- **Authors**: Ying, Rex; He, Ruining; Chen, Kaifeng; Eksombatchai, Pong; Hamilton, William L.; Leskovec, Jure
- **Publication**: KDD 2018; arXiv:1806.01973
- **URL**: https://arxiv.org/abs/1806.01973
- **Summary**: Data-efficient GCN for web-scale recommendations; trained on 3B nodes and 18B edges at Pinterest
- **Key Focus**: Large-scale recommendation, industrial deployment
- **Innovation**: Random walk-based sampling, harder-and-harder training strategy
- **Performance**: 25-30% improvement in user engagement; 10,000x larger than typical GCNs

#### 14.8 **SGC: Simplifying Graph Convolutional Networks** (2019)
- **Authors**: Wu, Felix; Souza, Amauri; Zhang, Tianyi; Fifty, Christopher; Yu, Tao; Weinberger, Kilian
- **Publication**: ICML 2019; arXiv:1902.07153
- **URL**: https://arxiv.org/abs/1902.07153
- **Summary**: Removes nonlinearities and collapses weight matrices; resulting linear model = fixed low-pass filter + linear classifier
- **Key Focus**: Simplification, computational efficiency
- **Performance**: Competitive accuracy with 2 orders of magnitude speedup over FastGCN
- **GitHub**: https://github.com/Tiiiger/SGC

---

