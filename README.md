# 🧠 Neurodyad Brain-to-Brain Decoder: Pre-Task Submission
### GSoC 2026 | ML4SCI | NeuroDyads Project

This repository contains the pre-task submission for the **NeuroDyads** project. The goal of this analysis is to decode affective states (Positive vs. Negative) from a 128-channel synchronized dyadic EEG matrix using latent manifold learning.

[![GitHub Repository](https://img.shields.io/badge/GitHub-neurodyad__test__nb-181717?logo=github)](https://github.com/0mM1shra/neurodyad_test_nb)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-3776AB?logo=python)](https://www.python.org/)

---

## 🚀 Project Overview
Decoding human emotion during live interaction is challenging due to the high non-stationarity of EEG and the complex "neural handshake" between two participants. This project utilizes **CEBRA**, a contrastive learning framework, to identify stable neural manifolds that characterize these emotional interactions.

### **Key Achievements**
* **Dual-Validation:** Implemented both Random and Continuous (Block) validation to eliminate temporal leakage.
* **Accuracy:** Achieved a statistically significant **75.33% Block-Validated Accuracy** (a 25.33% lift over chance).
* **Robust Preprocessing:** Developed an automated "CERN-Spec" pipeline (ICA-Infomax, RANSAC, and 150µV Amplitude Sensing).

---

## 📁 Repository Structure
* [`neurodyad_test_submission.ipynb`](neurodyad_test_submission.ipynb): The main analysis notebook containing preprocessing, manifold training, and 3D visualizations.
* [`requirements.txt`](requirements.txt): Manifest of all dependencies required to replicate the environment.

---

## 🛠️ The Preprocessing Pipeline
To extract a high-fidelity signal, the raw data underwent a rigorous cleaning process:
1.  **High-Pass Filtering (1.0 Hz):** Attenuated DC drift and slow-wave biological artifacts.
2.  **PyPrep & RANSAC:** Automated identification and interpolation of bad electrodes to maintain a 128-channel stack.
3.  **ICA & ICLabel:** Muted eye-blinks and myogenic noise while preserving temporal continuity for CEBRA.
4.  **Amplitude Thresholding:** Zero-masked segments >150µV to prevent motor transients from dominating the latent space.

---

## 📊 Performance Report

| Validation Method | Main Model | Shuffled Control |
| :--- | :---: | :---: |
| **Random (Shuffled) Acc** | **75.54%** | 49.30% |
| **Continuous (Block) Acc** | **75.33%** | 50.62% |
| **Goodness-of-Fit (Loss)** | **6.1130** | 6.2383 |

The near-identical performance between Random and Block validation (0.21% delta) confirms that the model has identified a **stable global neural biomarker** rather than overfitting to local temporal correlations.

---

## 🎨 Manifold Visualization
The latent space (3 dimensions) reveals a distinct "Dual-Lobe" topology. 
* **Main Model:** Shows clear, energy-efficient separation between Positive and Negative affect centroids across Isometric, Top, and Side views.
* **Control Model:** Exhibits a stochastic "ball of yarn" structure (loss: 6.2383, accuracy: ~50%), validating that the Main Model's separation is biologically driven.

---

## ⚙️ Installation & Usage

1. **Clone the repo:**
   
       git clone https://github.com/0mM1shra/neurodyad_test_nb.git
       cd neurodyad_test_nb

2. **Install dependencies:**
   
       pip install -r requirements.txt

3. **Run the notebook:**
   
   Open `neurodyad_test_submission.ipynb` in your preferred Jupyter environment.

---

## 🔮 Reflection & Future Work
* **Limitation:** This is a "Private Language Decoder" (N=1 dyad). Accuracy may vary across different pairs due to inter-subject variability.
* **Scaling:** Future work involves **CEBRA-Multi** for manifold alignment across multiple dyads to find universal affective signatures.
* **Depth:** Integrating **Source Reconstruction (sLORETA)** to map these 3D dynamics to specific cortical regions like the Amygdala and PFC.

---
**Author:** Om Mishra  
**Target:** ML4SCI / GSoC 2026 Submission
