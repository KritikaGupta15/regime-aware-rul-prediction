# Regime-Aware Deep Learning for Predictive Maintenance (Hybrid SAMB-GRU)

Remaining Useful Life (RUL) prediction on the NASA C-MAPSS turbofan dataset using a dual-head  
**Shared Attention Multi-Branch GRU (SAMB-GRU)** architecture with **KMeans-based regime-aware normalization**.

**Authors:** Nikhil Barot, Rasha S. Gargees, Kritika Gupta  
Department of Computer Science, Central Michigan University

---

## 🚀 Overview

This repository contains experiments, notebooks, and documentation for our IEEE-published work:  
**“Regime-Aware Deep Learning Framework for Predictive Maintenance in Industrial Systems.”**

The model integrates convolutional feature extraction, bidirectional sequence modeling, temporal attention, and regime-aware preprocessing to improve RUL prediction robustness across varying operating conditions.

---

## 🔧 Architecture Highlights

- **Shared Encoder Pipeline**
  - `Conv1D` → `LayerNorm` → `BiGRU` → `LayerNorm` → **Temporal Attention**
- **Dual-Head Output**
  - **RUL Regression Head**
  - **Unsupervised Diagnostic Probes**  
    - Fan/LPC  
    - HPC/Core  
    - Turbine
- **Regime-Aware Normalization**
  - KMeans clustering (`k = 6`) on operating settings  
  - Per-regime StandardScaler normalization  
  - Prevents environmental–degradation signal conflation
- **Leakage-Free Evaluation**
  - Engine-level train/validation splits  
  - No cycle-level leakage
- **PHM08-Aligned Loss**
  - Inverse-RUL sample weighting  
  - Penalizes late predictions more heavily

---

## 📊 Experimental Results  
*(mean ± std over seeds 42, 123, 2026)*

| Dataset | RMSE | R² | PHM Penalty |
|--------|------|------|-------------|
| **FD001** | 13.73 ± 0.44 | 0.8825 ± 0.0076 | 319.3 ± 46.4 |
| **FD002** | 15.07 ± 0.27 | 0.8757 ± 0.0044 | 901.3 ± 69.0 |
| **FD003** | 13.48 ± 0.30 | 0.8814 ± 0.0053 | 283.5 ± 23.7 |
| **FD004** | 15.42 ± 0.75 | 0.8695 ± 0.0125 | 1041.2 ± 96.9 |

---

## 📁 Repository Structure

├── notebooks/        # FD001 and FD004 experiments
├── paper/            # Manuscript, figures, and supplementary material
└── data/             # Place CMAPSS dataset files here
