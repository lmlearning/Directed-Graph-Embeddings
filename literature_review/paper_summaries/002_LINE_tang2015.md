# Paper Summary: LINE (Large-scale Information Network Embedding)

## Bibliographic Information
- **Paper Title:** LINE: Large-scale Information Network Embedding
- **Authors:** Jian Tang, Meng Qu, Mingzhe Wang, Ming Zhang, Jun Yan, Qiaozhu Mei
- **Affiliations:** Microsoft Research Asia, Peking University, University of Michigan
- **Venue/Year:** WWW 2015 (May 18-22, 2015, Florence, Italy)
- **DOI/URL:** http://dx.doi.org/10.1145/2736277.2741093
- **arXiv/Publication ID:** arXiv:1503.03578v1 [cs.LG]

## High-Level Summary
**Core Idea:** LINE addresses the fundamental challenge of embedding very large information networks (millions of nodes, billions of edges) into low-dimensional vector spaces by preserving both first-order proximity (direct pairwise connections) and second-order proximity (shared neighborhood structures). The method employs a novel edge-sampling algorithm that addresses gradient explosion in weighted networks and achieves O(dK|E|) time complexity, enabling it to process networks with 2 million nodes and 1 billion edges in under 3 hours on a single machine while outperforming baselines on word analogy, document classification, and node classification tasks.

---

## 1. Introduction and Motivation

### Problem Context
**Domain:** Graph embedding, network representation learning, dimensionality reduction for large-scale information networks including social networks, language networks, citation networks, and the World Wide Web.

**Existing Approaches and Limitations:**
- **Classical methods** (MDS, IsoMap, Laplacian Eigenmap): O(|V|²) or higher complexity, cannot scale to millions of nodes
- **Graph Factorization (2013)**: Indirect approach not designed for networks, lacks clear network-specific objective, only works for undirected graphs
- **DeepWalk (2014)**: Lacks clear objective function, only preserves second-order proximity, applies only to unweighted networks, uses random walks (depth-first search analogy) which may introduce noise

**Gap:** Most existing methods either (1) don't scale beyond thousands of nodes, (2) ignore edge weights which are critical in many networks, (3) only preserve local proximity missing global structure, or (4) lack principled objective functions.

### Specific Problem Being Addressed
**Research Questions:**
1. How can we preserve both local (first-order) and global (second-order) network structures in embeddings?
2. How can we efficiently optimize embeddings for networks with millions/billions of edges and highly divergent edge weights?
3. How can we design a method applicable to arbitrary network types: directed, undirected, weighted, unweighted?

**Why It Matters:**
- Real-world networks are massive: Twitter has 175M users, ~20B edges (2012)
- Many legitimate connections are unobserved (sparsity problem) - first-order proximity alone is insufficient
- Edge weights often vary dramatically (e.g., word co-occurrences: 1 to 100,000+), causing gradient explosion in standard SGD
- Applications include visualization, node classification, link prediction, recommendation systems

### Key Contributions
1. **Novel network embedding model (LINE)** suitable for arbitrary network types with carefully designed objectives preserving both first-order and second-order proximity
2. **Edge-sampling algorithm** that addresses classical SGD limitations on weighted networks, improving both effectiveness and efficiency
3. **Scalability demonstration**: Embedding of networks with millions of vertices and billions of edges in hours on single machine
4. **Empirical validation** across diverse real-world networks (language, social, citation) showing superior performance over competitive baselines

---

## 2. Related Work

### Taxonomy of Prior Work

**Classical Graph Embedding Methods:**
- **Multidimensional Scaling (MDS)**: Embedding via distance preservation, O(|V|²+) complexity
- **IsoMap**: Global geometric framework for nonlinear dimensionality reduction, O(|V|²+)
- **LLE (Locally Linear Embedding)**: Local structure preservation, O(|V|²+)
- **Laplacian Eigenmap**: Spectral embedding via graph Laplacian eigenvectors, O(|V|²+)
- **Common limitation**: All require eigenvector computation with at least quadratic complexity, unsuitable for large networks

**Recent Scalable Methods:**
- **Graph Factorization (Ahmed et al. 2013)**:
  - Matrix factorization on affinity matrix with SGD optimization
  - **Limitation**: Objective not designed for networks, doesn't preserve global structure, only undirected graphs, only preserves first-order proximity

- **DeepWalk (Perozzi et al. 2014)**:
  - Truncated random walks for social network embedding
  - **Limitation**: No clear objective function, only second-order proximity, only unweighted networks, depth-first search strategy via random walks less suitable than breadth-first for second-order proximity

### How This Paper Differs
**Key Distinctions:**
1. **Explicit dual-proximity objective**: LINE has principled objectives for both first-order (local) and second-order (global) proximity vs. DeepWalk's implicit approach
2. **Handles weighted networks**: Edge-sampling algorithm enables effective learning on weighted graphs vs. DeepWalk/GF limitations
3. **Breadth-first vs. depth-first**: LINE uses direct neighborhood (breadth-first) for second-order proximity vs. DeepWalk's random walk (depth-first) approach
4. **Directed graph support**: LINE(2nd) works on directed graphs vs. Graph Factorization's undirected-only limitation
5. **Scalability**: Linear O(dK|E|) complexity with efficient edge sampling vs. classical methods' quadratic complexity

---

## 3. Methodology

### Problem Definition

**Definitions:**

**Definition 1 (Information Network):** G = (V, E) where V = vertices (data objects), E = edges (relationships). Each edge e = (u, v) has weight w_uv > 0. If undirected: (u,v) ≡ (v,u) and w_uv ≡ w_vu. If directed: (u,v) ≢ (v,u) and w_uv ≢ w_vu.

**Definition 2 (First-order Proximity):** Local pairwise proximity between vertices. For edge (u, v), weight w_uv indicates first-order proximity. If no edge observed, first-order proximity = 0.

**Definition 3 (Second-order Proximity):** Similarity between neighborhood network structures. For vertices u and v with first-order proximity vectors p_u = (w_u,1, ..., w_u,|V|) and p_v, second-order proximity is determined by similarity between p_u and p_v. If no vertex is linked from/to both u and v, second-order proximity = 0.

**Definition 4 (Large-scale Information Network Embedding):** Given G = (V, E), learn function f_G: V → R^d where d ≪ |V|, preserving both first-order and second-order proximity.

### Architecture/Framework

**LINE with First-order Proximity:**
- Applicable to undirected networks only
- Each vertex v_i represented by single vector u_i ∈ R^d
- Joint probability for edge (i, j):
  ```
  p₁(v_i, v_j) = 1 / (1 + exp(-u_i^T · u_j))
  ```
- Empirical distribution: p̂₁(i, j) = w_ij / W where W = Σ_{(i,j)∈E} w_ij
- Objective (KL-divergence minimization):
  ```
  O₁ = -Σ_{(i,j)∈E} w_ij log p₁(v_i, v_j)
  ```

**LINE with Second-order Proximity:**
- Applicable to both directed and undirected networks
- Each vertex has TWO representations:
  - u_i: vertex representation (when treated as vertex)
  - u'_i: context representation (when treated as context/neighbor)
- Conditional probability of context v_j generated by vertex v_i:
  ```
  p₂(v_j|v_i) = exp(u'_j^T · u_i) / Σ_{k=1}^{|V|} exp(u'_k^T · u_i)
  ```
- Empirical distribution: p̂₂(v_j|v_i) = w_ij / d_i where d_i = Σ_{k∈N(i)} w_ik (out-degree)
- Objective with vertex importance λ_i = d_i:
  ```
  O₂ = -Σ_{(i,j)∈E} w_ij log p₂(v_j|v_i)
  ```

**LINE (1st+2nd):**
- Train LINE(1st) and LINE(2nd) separately
- Concatenate embeddings: [u_i^{(1st)}; u_i^{(2nd)}] for each vertex
- Re-weight dimensions based on training data (supervised tasks)

### Technical Breakdown

**Optimization via Negative Sampling:**
Computing p₂(·|v_i) requires summing over all |V| vertices (expensive). Solution: negative sampling with K negative edges per observed edge.

For each edge (i, j), optimize:
```
log σ(u'_j^T · u_i) + Σ_{n=1}^K E_{v_n~P_n(v)}[log σ(-u'_n^T · u_i)]
```
where:
- σ(x) = 1/(1 + exp(-x)) is sigmoid function
- P_n(v) ∝ d_v^{3/4} is noise distribution (same as word2vec)
- First term: observed edges; Second term: negative samples

**Edge-Sampling Algorithm:**

**Problem:** Direct SGD gradient for edge (i,j):
```
∂O₂/∂u_i = w_ij · ∂log p₂(v_j|v_i)/∂u_i
```
Gradient multiplied by w_ij causes explosion when weights diverge (e.g., word co-occurrences ranging from 1 to 100,000).

**Solution:**
1. Sample edges with probability proportional to weights
2. Treat sampled edges as binary (weight = 1) for gradient computation
3. Overall objective function remains unchanged
4. No gradient explosion since all sampled edges have equal weight

**Alias Table Method:**
- Preprocessing: O(|E|) time to build alias table
- Sampling: O(1) time per sample
- Enables efficient weighted edge sampling

**Overall Algorithm:**
1. Build alias table from edge weights
2. For each iteration:
   - Sample edge (i,j) from alias table
   - Sample K negative edges from P_n(v)
   - Update u_i, u'_j, and negative context vectors
   - Use Asynchronous SGD (ASGD) for parallelization
3. Learning rate: ρ_t = ρ₀(1 - t/T) where ρ₀ = 0.025

**Complexity Analysis:**
- Each step: O(dK) time (d = dimension, K = negative samples)
- Total iterations: O(|E|)
- **Overall: O(dK|E|)** - linear in number of edges
- Space: O(d|V|) for embeddings

### Theoretical Foundations

**First-order vs. Second-order Proximity:**

**Intuition for first-order:** Direct connections indicate similarity
- Social networks: Friends share similar interests
- Web: Linked pages discuss similar topics
- Limitation: Most legitimate links are unobserved (sparsity)

**Intuition for second-order:** Shared neighbors indicate similarity
- Sociological theory: "Degree of overlap of two people's friendship networks correlates with strength of ties between them" (Granovetter 1973)
- Linguistic theory: "You shall know a word by the company it keeps" (Firth 1957)
- Example: In Figure 1, vertex 5 and 6 have no direct link but share many neighbors → should be close in embedding space

**Why both proximities are needed:**
- First-order: Captures observed strong ties (local structure)
- Second-order: Addresses sparsity, captures global structure through neighborhood similarity
- Experimental evidence: LINE(1st+2nd) significantly outperforms either alone

**Handling Low-Degree Vertices:**
For vertices with small degrees, second-order proximity is inaccurate (few contexts). Solution: expand neighborhood by adding second-order neighbors (neighbors of neighbors):
```
w_ij = Σ_{k∈N(i)} (w_ik · w_kj) / d_k
```
Add subset of {j} with largest w_ij to neighborhood of low-degree vertex i.

**New Vertices (Out-of-sample extension):**
For new vertex i with known connections to existing vertices, minimize:
```
-Σ_{j∈N(i)} w_ji log p₁(v_j, v_i)  or  -Σ_{j∈N(i)} w_ji log p₂(v_j|v_i)
```
Update only u_i, keep existing embeddings fixed.

---

## 4. Evaluation and Experiments

### Experimental Goals
1. Demonstrate scalability to million-node, billion-edge networks
2. Compare effectiveness against state-of-the-art baselines across diverse network types
3. Validate edge-sampling algorithm vs. standard SGD
4. Analyze first-order vs. second-order proximity contributions
5. Study performance under varying network sparsity

### Datasets

| Network | Type | \|V\| | \|E\| | Avg. Degree | #Labels | #Train |
|---------|------|-------|-------|-------------|---------|--------|
| **Wikipedia** | undirected, weighted | 1,985,098 | 1,000,924,086 | 504.22 | 7 | 70,000 |
| **Flickr** | undirected, binary | 1,715,256 | 22,613,981 | 26.37 | 5 | 75,958 |
| **Youtube** | undirected, binary | 1,138,499 | 2,990,443 | 5.25 | 47 | 31,703 |
| **DBLP(AuthorCitation)** | directed, weighted | 524,061 | 20,580,238 | 78.54 | 7 | 20,684 |
| **DBLP(PaperCitation)** | directed, binary | 781,109 | 4,191,677 | 10.73 | 7 | 10,398 |

**Wikipedia:** Word co-occurrence network from English Wikipedia. 5-word sliding window, frequency ≥ 5.

**Flickr/Youtube:** Social networks from user connections.

**DBLP:** Author citation network (# papers by author A cited by author B), Paper citation network.

### Baseline Methods
1. **Graph Factorization (GF)**: Matrix factorization via SGD, undirected graphs only
2. **DeepWalk**: Random walk-based embedding, unweighted graphs only
3. **SkipGram**: State-of-the-art word embedding (Wikipedia text only, not network)
4. **LINE-SGD(1st/2nd)**: LINE with standard SGD (no edge sampling) - demonstrates gradient explosion problem
5. **LINE(1st)**: First-order proximity only
6. **LINE(2nd)**: Second-order proximity only
7. **LINE(1st+2nd)**: Concatenation of LINE(1st) and LINE(2nd)

### Evaluation Metrics

**Word Analogy Task:**
- Given (a, b) and c, find d such that a:b → c:d
- Example: "China":"Beijing" → "France":"Paris"
- Solution: d* = argmax_d cos((u_b - u_a + u_c), u_d)
- Categories: Semantic and Syntactic
- Metric: Accuracy (%)

**Document Classification:**
- Represent document as average of word embeddings
- Train one-vs-rest logistic regression (LibLinear)
- Metrics: Micro-F1, Macro-F1
- 7 Wikipedia categories: Arts, History, Human, Mathematics, Nature, Technology, Sports

**Node Classification (Multi-label):**
- Train on varying percentages of labeled nodes (1%-90%)
- One-vs-rest logistic regression
- Metrics: Micro-F1, Macro-F1
- Average over 10 runs with different training samples

### Implementation Details
- **Dimension:** d = 200 (Wikipedia), d = 128 (other networks)
- **Negative samples:** K = 5
- **Total samples:** T = 10B (LINE 1st/2nd), T = 20B (GF)
- **Learning rate:** ρ₀ = 0.025, ρ_t = ρ₀(1 - t/T)
- **DeepWalk:** window=10, walk length=40, walks per vertex=40
- **Normalization:** ||w||₂ = 1 for all embeddings
- **Hardware:** Single machine, 1T memory, 40 CPU cores @ 2.0GHz, 16 threads

---

## 5. Results and Analysis

### Main Quantitative Results

**Table: Word Analogy on Wikipedia**

| Algorithm | Semantic (%) | Syntactic (%) | Overall (%) | Time |
|-----------|--------------|---------------|-------------|------|
| GF | 61.38 | 44.08 | 51.93 | 2.96h |
| DeepWalk | 50.79 | 37.70 | 43.65 | 16.64h |
| SkipGram | 69.14 | 57.94 | 63.02 | 2.82h |
| LINE-SGD(1st) | 9.72 | 7.48 | 8.50 | 3.83h |
| LINE-SGD(2nd) | 20.42 | 9.56 | 14.49 | 3.94h |
| LINE(1st) | 58.08 | 49.42 | 53.35 | 2.44h |
| **LINE(2nd)** | **73.79** | **59.72** | **66.10** | **2.55h** |

**Key findings:**
- LINE(2nd) outperforms state-of-the-art SkipGram (66.10% vs. 63.02%)
- LINE-SGD performs terribly due to gradient explosion from divergent edge weights
- Edge-sampling treatment dramatically improves performance
- 6.5× faster than DeepWalk

**Wikipedia Page Classification (Micro-F1 at different training percentages):**

| Method | 10% | 30% | 50% | 70% | 90% |
|--------|-----|-----|-----|-----|-----|
| GF | 79.63 | 80.94 | 81.38 | 81.63 | 81.78 |
| DeepWalk | 78.89 | 80.41 | 80.92 | 81.21 | 81.42 |
| LINE(1st) | 79.67 | 80.94 | 81.40 | 81.61 | 81.67 |
| LINE(2nd) | 79.93 | 81.31 | 81.80 | 82.00 | 82.17 |
| **LINE(1st+2nd)** | **81.04** | **82.58** | **83.16** | **83.52** | **83.74** |

Significantly outperforms all baselines (p < 0.01).

**Flickr Social Network (Micro-F1):**

| Method | 10% | 50% | 90% |
|--------|-----|-----|-----|
| GF | 53.23 | 54.32 | 54.48 |
| DeepWalk | 60.38 | 61.13 | 61.22 |
| DeepWalk(256d) | 60.41 | 61.69 | 61.83 |
| LINE(1st) | 63.27 | 63.96 | 64.10 |
| LINE(2nd) | 62.83 | 63.55 | 63.69 |
| **LINE(1st+2nd)** | **63.20** | **64.53** | **64.74** |

**Youtube Network (Micro-F1, with reconstructed network in parentheses):**

| Method | 1% | 5% | 10% |
|--------|-----|-----|-----|
| DeepWalk(256d) | 39.94 | 44.47 | 45.81 |
| LINE(1st) | 35.43 | 40.77 | 42.21 |
|  | (36.47) | (41.33) | (42.73) |
| LINE(2nd) | 32.98 | 41.08 | 43.34 |
|  | (36.78) | (43.90) | (45.67) |
| **LINE(1st+2nd)** | **39.01** | **44.62** | **46.08** |
|  | **(40.20)** | **(45.19)** | **(46.43)** |

Note: Reconstructed network adds neighbors-of-neighbors for low-degree vertices.

**Citation Networks:**

DBLP(AuthorCitation) - Micro-F1:
- DeepWalk: 63.98% → 64.90% (10% → 90% training)
- LINE(2nd): 62.49% → 63.77%
- LINE(2nd) on reconstructed: **64.69%** → **66.05%** (significantly better)

DBLP(PaperCitation) - Micro-F1:
- DeepWalk: 52.83% → 55.90%
- LINE(2nd): **58.42%** → **61.79%** (significantly better, p < 0.01)
- LINE(2nd) reconstructed: **60.10%** → **62.80%**

### Ablation Studies

**First-order vs. Second-order Proximity:**

Table 4 shows most similar words using 1st vs. 2nd order:
- **"good"**
  - 1st: luck, bad, faith, assume, nice (mixed syntactic/semantic)
  - 2nd: decent, bad, excellent, lousy, reasonable (semantic synonyms)
- **"graph"**
  - 1st: graphs, algebraic, finite, symmetric, topology
  - 2nd: graphs, subgraph, matroid, hypergraph, undirected (graph-theoretic terms)

**Finding:** Second-order proximity captures semantic similarity better; first-order captures mix of syntactic and semantic.

**Network Sparsity Analysis (Flickr):**
- Very sparse network: LINE(1st) > LINE(2nd)
- As density increases: LINE(2nd) begins to outperform LINE(1st)
- Reason: Second-order proximity requires sufficient neighborhood size

**Performance by Vertex Degree (Youtube):**
- Categorized vertices by degree: (0,1], [2,3], [4,6], [7,12], [13,30], [31,+∞)
- LINE(2nd) < LINE(1st) for degree group (0,1]
- LINE(2nd) ≥ LINE(1st) for higher degree groups
- On reconstructed network: LINE(2nd) outperforms DeepWalk across all groups

### Qualitative Observations

**Network Visualization:**
Co-author network from DBLP: WWW/KDD (data mining), NIPS/ICML (ML), CVPR/ICCV (vision)
- 18,561 authors, 207,074 edges
- Embeddings → t-SNE for 2D visualization
- **GF:** Communities not well-separated, poor clustering
- **DeepWalk:** Better than GF but high-degree vertices cluster tightly in center (noise from random walks)
- **LINE(2nd):** Clear community separation, meaningful layout, nodes with same color (community) distributed closely

**Efficiency and Scalability:**
- **Speedup vs. threads:** Nearly linear speedup (5-15 threads tested)
- **Classification performance vs. threads:** Stable Micro-F1 regardless of thread count
- **Convergence:** LINE(1st) and LINE(2nd) converge much faster than DeepWalk
- **Dimension sensitivity:** Performance drops when d becomes too large (overfitting)

---

## 6. Discussion and Implications

### Main Findings

1. **Second-order proximity is more powerful than first-order for semantic tasks** but requires sufficient neighborhood density. On dense networks (Wikipedia), LINE(2nd) > LINE(1st). On sparse networks (Youtube), LINE(1st) may outperform until neighborhoods are expanded.

2. **Edge-sampling algorithm is critical for weighted networks.** LINE-SGD performs terribly (8.50% word analogy) while LINE(2nd) achieves 66.10% - a 7.8× improvement. Gradient explosion from divergent weights prevents learning without sampling.

3. **Combining both proximities is highly effective.** LINE(1st+2nd) significantly outperforms individual components across supervised tasks (Wikipedia classification: 83.74% vs. 82.17% for LINE(2nd) alone).

4. **Breadth-first (direct neighbors) superior to depth-first (random walks) for second-order proximity.** LINE(2nd) outperforms DeepWalk on most tasks despite DeepWalk's neighborhood expansion via random walks.

5. **Scalability achieved without sacrificing effectiveness.** LINE processes billion-edge networks in hours while outperforming slower baselines.

### Limitations Acknowledged by Authors

1. **Handling very sparse networks:** Second-order proximity degrades when average degree is very low (e.g., Youtube with avg. degree 5.25). Requires network reconstruction (adding 2nd-order neighbors).

2. **Low-degree vertices:** Difficult to accurately embed vertices with very few connections. Proposed solution (adding neighbors-of-neighbors) is heuristic.

3. **New vertex embedding:** If no connections observed, must resort to auxiliary information (e.g., text) - not addressed in paper.

4. **Simple concatenation for combining proximities:** LINE(1st+2nd) uses simple concatenation + reweighting. More principled joint optimization left as future work.

5. **Dimension weighting in unsupervised settings:** For LINE(1st+2nd) in unsupervised tasks, unclear how to optimally weight the two representations.

### Connections to Broader Literature

**Relationship to word2vec:**
- LINE(2nd) with negative sampling is analogous to Skip-Gram with negative sampling
- Levy & Goldberg (2014) showed Skip-Gram implicitly factorizes PMI matrix
- LINE(2nd) can be seen as matrix factorization of network proximity matrix

**Comparison to spectral methods:**
- Classical methods (Laplacian Eigenmap) preserve first-order proximity via spectral decomposition
- LINE preserves both first and second-order but via optimization, not eigen-decomposition
- O(dK|E|) vs. O(|V|²) - fundamentally different scalability

**Sociological foundations:**
- Granovetter's "strength of weak ties" (1973): Shared friends indicate relationship strength
- LINE's second-order proximity formalizes this intuition mathematically

**Linguistic foundations:**
- Firth's distributional hypothesis (1957): "You shall know a word by the company it keeps"
- LINE(2nd) for language networks directly implements this principle

### Impact on Field

**Methodological contributions:**
1. Edge-sampling algorithm - broadly applicable to any network learning method with weighted edges
2. Explicit formulation of first vs. second-order proximity - clarifies what different methods preserve
3. Demonstrated importance of preserving multiple types of proximity

**Practical impact:**
- Scales to real-world network sizes (billions of edges)
- Applicable to diverse network types (directed, undirected, weighted)
- Outperforms state-of-the-art on multiple tasks and domains

---

## 7. Conclusion and Future Work

### Main Conclusions

The LINE model successfully addresses the challenge of embedding very large information networks through three key innovations:
1. **Dual-proximity objective** preserving both local (first-order) and global (second-order) network structures
2. **Edge-sampling algorithm** enabling efficient optimization on weighted networks without gradient explosion
3. **Linear scalability** O(dK|E|) achieving embedding of billion-edge networks in hours

Experimental validation across language networks (2M nodes, 1B edges), social networks (1.7M nodes, 22M edges), and citation networks demonstrates:
- Superior effectiveness vs. state-of-the-art (66.10% word analogy vs. SkipGram 63.02%)
- Significant improvements in classification tasks (83.74% Micro-F1 vs. baseline 81.78%)
- 6.5× speedup over DeepWalk while maintaining higher accuracy
- Applicability to diverse network types: directed, undirected, weighted, unweighted

### Future Directions Proposed

1. **Higher-order proximity:** Investigate proximity beyond first and second order
   - Third-order: Vertices with similar second-order neighborhoods
   - General k-order proximity formulation

2. **Heterogeneous information networks:**
   - Vertices with multiple types (e.g., users, items, tags)
   - Edges with multiple types (e.g., friendship, authorship, citation)
   - Type-specific embeddings

3. **Joint optimization of first and second-order:**
   - Current approach: Train separately then concatenate
   - Proposed: Single objective combining both proximities
   - Automatic balancing of two components

4. **Auxiliary information for new vertices:**
   - Content features (text, images)
   - Temporal patterns
   - Transfer learning from related networks

5. **Dynamic networks:**
   - Incremental updates as network evolves
   - Time-evolving embeddings
   - Forgetting mechanisms for outdated information

6. **Theoretical analysis:**
   - Convergence guarantees for edge-sampling algorithm
   - Approximation bounds for truncated embeddings
   - Conditions under which first vs. second-order dominates

### Open Questions

1. **Optimal neighborhood expansion strategy:** When and how to add higher-order neighbors for sparse networks?

2. **Automatic dimension selection:** How to choose embedding dimension d for different network types/sizes?

3. **Multi-scale representations:** Can we learn hierarchical embeddings capturing structure at multiple resolutions?

4. **Privacy-preserving embeddings:** How to embed networks while protecting sensitive connection information?

---

## Additional Notes

### Code and Reproducibility
- **Source code:** https://github.com/tangjianpku/LINE
- **Open source:** Publicly available implementation
- **Datasets:** Flickr, Youtube publicly available; Wikipedia extractable; DBLP from ArnetMiner

### Key Equations Reference

**First-order proximity:**
```
p₁(vᵢ, vⱼ) = 1 / (1 + exp(-uᵢᵀ·uⱼ))
O₁ = -Σ_{(i,j)∈E} wᵢⱼ log p₁(vᵢ, vⱼ)
```

**Second-order proximity:**
```
p₂(vⱼ|vᵢ) = exp(u'ⱼᵀ·uᵢ) / Σₖ exp(u'ₖᵀ·uᵢ)
O₂ = -Σ_{(i,j)∈E} wᵢⱼ log p₂(vⱼ|vᵢ)
```

**Negative sampling:**
```
log σ(u'ⱼᵀ·uᵢ) + Σₙ₌₁ᴷ 𝔼_{vₙ~Pₙ(v)}[log σ(-u'ₙᵀ·uᵢ)]
where Pₙ(v) ∝ dᵥ^{3/4}
```

**Complexity:** O(dK|E|) where d = dimension, K = negative samples, |E| = edges

### Significance for Directed Graphs

While LINE(1st) only applies to undirected graphs, **LINE(2nd) naturally handles directed graphs:**
- Each vertex has source representation (uᵢ) and target representation (u'ᵢ)
- For directed edge (i → j): Models P(target j | source i)
- Preserves asymmetric transitivity: Nodes with similar out-neighborhoods are similar
- Demonstrated on DBLP citation networks (directed)

This makes LINE particularly relevant for directed graph embedding research.
