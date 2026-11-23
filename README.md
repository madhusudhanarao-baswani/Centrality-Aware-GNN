# Centrality-Aware Graph Neural Networks with Centrality–Similarity Fusion for Link Prediction

## Overview

This repository presents a **Centrality-Aware Graph Neural Network (CA-GNN)** framework for link prediction in complex networks. The proposed approach integrates graph neural network representation learning with node centrality profiles to estimate the likelihood of missing or future links.

The framework combines GNN-based link probabilities with centrality-profile cosine similarity through a validation-guided fusion mechanism.

## Key Features

- Centrality-aware node feature construction using Degree, Closeness, Betweenness, and Eigenvector Centrality.
- Two-layer Graph Convolutional Network (GCN) for learning node representations.
- Multilayer Perceptron (MLP) decoder for link prediction.
- Cosine similarity between normalized centrality profiles.
- Validation-guided Centrality–Similarity Fusion.
- Enhanced network construction using predicted links.
- Louvain community detection and modularity analysis.

## Proposed Methodology

The framework consists of the following stages:

1. **Graph Preprocessing:** Convert the input graph into a simple, undirected, unweighted network.
2. **Data Splitting:** Divide observed edges into training (80%), validation (10%), and testing (10%) sets, with a 1:1 positive-to-negative sampling ratio.
3. **Centrality Computation:** Calculate four centrality measures using the training graph.
4. **GNN Representation Learning:** Train a GCN encoder with an MLP-based link decoder.
5. **Centrality Similarity:** Compute cosine similarity between candidate nodes' centrality vectors.
6. **Score Fusion:** Combine GNN link probabilities and centrality similarity using a validation-selected coefficient.
7. **Evaluation:** Evaluate performance using AUROC, AUPR, Precision, Recall, and F1-score.
8. **Network Enhancement:** Construct an enhanced network and analyze its community structure.

## Centrality–Similarity Fusion

The final link prediction score is calculated as:

\[
S_{CS}(u,v)=\alpha S_{GNN}(u,v)+(1-\alpha)S_C(u,v)
\]

where:

- \(S_{GNN}(u,v)\) is the GNN decoder's predicted link probability.
- \(S_C(u,v)\) is the cosine similarity between node centrality profiles.
- \(\alpha\) is the fusion coefficient selected using validation AUPR.

## Evaluation Datasets

The framework is evaluated on eight complex networks:

| Dataset |
|---|
| CA-AstroPh |
| CA-CondMat |
| CA-Erdos992 |
| CA-GrQc |
| CA-HepPh |
| CA-HepTh |
| Email-Eu-core |
| Inf-Power |

## Experimental Results

Average performance across eight evaluation datasets:

| Method | AUROC | AUPR | Precision | Recall | F1 |
|---|---:|---:|---:|---:|---:|
| Common Neighbors | 0.8992 | 0.8820 | 0.8492 | 0.8754 | 0.8334 |
| Adamic–Adar | 0.9058 | 0.8927 | 0.8508 | 0.8744 | **0.8437** |
| CA-GNN Decoder | 0.8973 | 0.8804 | 0.8656 | 0.8596 | 0.7355 |
| Centrality Cosine Only | 0.9193 | 0.9001 | 0.8209 | 0.9075 | 0.6776 |
| **Proposed Fusion** | **0.9524** | **0.9380** | **0.8917** | **0.9253** | 0.8365 |

The proposed fusion achieves the highest average AUROC, AUPR, Precision, and Recall among the evaluated methods. Adamic–Adar achieves the highest average F1-score.

These results represent the reported experimental configuration; repeated-run statistical significance has not been established.

## Technologies Used

- Python
- PyTorch
- PyTorch Geometric
- NetworkX
- NumPy
- scikit-learn

## Authors

**Madhusudhana Rao Baswani**  
**Dr. Prasanthi Boyapati** (Corresponding Author)

Department of Computer Science and Engineering  
SRM University-AP, Amaravati, Andhra Pradesh, India

## Citation

If you use this research or its implementation, please cite the associated manuscript once its publication details are available.

## License

Please refer to the repository's LICENSE file, if provided, for reuse permissions.
