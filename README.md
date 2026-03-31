# LM-JEPA for Squared Amplitude Calculation

This repository contains the implementation of a **Joint-Embedding Predictive Architecture (JEPA)** designed to disentangle and classify $U(1)$ (Electromagnetism) and $SU(3)$ (Strong Force) gauge symmetries from symbolic squared amplitudes.

##  Objectives
* **Latent Disentanglement:** Map high-dimensional symbolic physics strings into a structured latent space where different gauge theories form distinct clusters.
* **Robustness under Information Loss:** Evaluate model performance across varying masking ratios (20%–80%) to identify the "Information Collapse Threshold".
* **Interpretability:** Utilize Saliency Mapping to identify which mathematical tokens (indices, color factors) drive the model’s physical "understanding".

##  What I Did
1.  **Preprocessing (ULTRA_v2):** Developed a custom **Local Structural Normalization** script to canonicalize symbolic indices and ensure consistent tokenization of $U(1)$ and $SU(3)$ amplitudes.
2.  **Architecture Engineering:** Implemented a Transformer-based JEPA with a **Context Encoder** and a **Target Encoder** updated via **Exponential Moving Average (EMA)** to prevent latent collapse.
3.  **Masking Strategy:** Impplemented baseline **Random Block Masking**, intend to propose **Saliency-Informed Masking** to preserve critical "Symmetry DNA" tokens.

---

## Tasks & Results

### **Common Task 1.2: Latent Space Topology**
* **Evaluation Metric:** Inter-theory Manifold Distance (Euclidean) and t-SNE Cluster Separation.
* **Result:** Achieved a **3.77 Manifold Distance** with clearly defined, non-overlapping clusters for QED and QCD.
* **Key Takeaway:** The JEPA objective effectively prevents dimensional collapse, allowing the model to learn global physical invariants rather than just string lengths.

### **Specific Task 2.5: Complexity Analysis**
* **Evaluation Metric:** Disaggregated Recall and Mean Accuracy vs. Mathematical Complexity.
* **Result:** Identified a critical **0.28 Recall Bottleneck for QCD** at 60% masking, despite maintaining 1.00 Precision.
* **Key Takeaway:** High-entropy $SU(3)$ samples require **Saliency-Informed Masking** because random masking often removes the sparse color-flow tokens essential for theory identification.

---

## Model Performance Summary

| Metric | $U(1)$ (QED) | $SU(3)$ (QCD) | Significance |
| :--- | :--- | :--- | :--- |
| **Latent Classification Accuracy** | **98.2%** | **98.2%** | Confirms high-fidelity theory separation in the latent manifold. |
| **Precision** | 0.66 | **1.00** | High reliability in QCD identification. |
| **Recall** | **1.00** | 0.28 | Identified "Information Collapse" in QCD at 60% masking. |
| **F1-Score** | 0.80 | 0.44 | Baseline for GSoC optimization. |
| **Manifold Distance** | -- | **3.77** | Proof of latent disentanglement. |
| **Centroid Separation** | -- | **Verified** | $SU(3)$ and $U(1)$ centroids are statistically distinct in hyperspace[cite: 1, 2, 3]. |
| **Max Masking Acc.** | 100% | 72% | Defines the 40% "Symmetry Collapse" point. |

---

## Key Research Insights & Bottlenecks
* **The 40% Threshold:** Beyond 40% random masking, the model begins to "leak" QCD samples into the QED manifold due to the loss of specific $SU(3)$ indices.
* **Symmetry DNA:** Saliency maps confirm that the model prioritizes **Lorentz indices** and **Color factors** over common operators, proving it is learning physics, not just syntax.
* **Complexity Sensitivity:** Identified a performance decay as mathematical complexity (character count) increases, establishing the "Extreme" complexity zone as a core target for future architectural refinements.

Link to download the Model weights : https://drive.google.com/drive/folders/1x2gOHXNKExrnzvz6dJD2kCHStf7acbAD?usp=drive_link
