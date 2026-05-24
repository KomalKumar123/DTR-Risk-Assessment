# AI-Based Risk Assessment for DTR Infrastructure Using Images

## Overview

This project proposes an explainable AI-assisted framework for preliminary risk assessment of Distribution Transformer Room (DTR) infrastructure using field images.

The system combines:

- CNN-based feature extraction
- Unsupervised learning
- Classical computer vision
- Heuristic engineering analysis

to estimate infrastructure risk from transformer installation images.

---

# Problem Statement

Given field images containing pole-mounted transformers and electrical infrastructure, the objective is to identify potentially unsafe installations using visual and structural cues.

Target classifications:

- Safe
- Risky
- Highly Risky

---

# Key Challenges

- No labeled public dataset
- Large installation variability
- Urban vs rural infrastructure differences
- Vegetation occlusions
- Dense electrical clutter
- Perspective distortion
- Lack of depth information

---

# Proposed Architecture

```text
Input Image
    ↓
Image Preprocessing
    ↓
ResNet50 Feature Extraction
    ↓
2048-D CNN Embeddings
    ↓
K-Means Clustering
    ↓
Feature Engineering
    ↓
Risk Scoring Engine
    ↓
Safe / Risky / Highly Risky
```

---

# Technologies Used

- Python
- PyTorch
- OpenCV
- Scikit-Learn
- NumPy
- Matplotlib
- Jupyter Notebook

---

# CNN Feature Extraction

A pretrained ResNet50 backbone was used as a feature extractor.

Instead of training a fully supervised classifier:
- the final classification layer was removed,
- intermediate embeddings were extracted,
- and infrastructure similarity analysis was performed using clustering.

The embeddings captured:

- Pole geometry
- Wiring density
- Transformer structure
- Environmental layout
- Vegetation distribution

---

# Unsupervised Clustering

K-Means clustering was applied on CNN embeddings to identify naturally occurring infrastructure groups.

Observed clusters included:

1. Urban roadside transformer installations
2. Elevated isolated transformer structures
3. Dense wiring / congested installations

---

# Feature Engineering

The system extracts interpretable engineering features instead of relying purely on black-box prediction.

## Extracted Features

| Feature | Purpose |
|---|---|
| Edge Density | Electrical clutter estimation |
| Green Pixel Ratio | Vegetation hazard estimation |
| Line Count | Structural congestion estimation |

---

# Risk Scoring

Final risk score:

```math
Risk Score =
0.35(Edge Density)
+
0.40(Green Ratio)
+
0.25(Line Count)
```

## Classification Thresholds

| Score Range | Classification |
|---|---|
| 0 – 30 | Safe |
| 31 – 60 | Risky |
| 61+ | Highly Risky |

---

# Sample Output

The system produces:

- Extracted feature values
- Risk score
- Final classification
- Visual inference output

Example:

```text
========== PREDICTION ==========

Edge Density : 0.1934
Green Ratio  : 0.0062
Line Count   : 479
Risk Score   : 32.21
Prediction   : Risky
```

---

# Dataset

A custom dataset of 28 DTR infrastructure images was collected from publicly available online sources.

Dataset diversity included:

- Urban transformers
- Rural installations
- Elevated structures
- Vegetation-heavy environments
- Congested electrical layouts

---

# Repository Structure

```text
DTR-Risk-Assessment/
│
├── dataset/
├── test_images/
├── outputs/
├── scripts.ipynb
├── report.tex
├── report.pdf
├── requirements.txt
└── README.md
```

---

# Running the Project

## Install dependencies

```bash
pip install -r requirements.txt
```

## Open notebook

```bash
jupyter notebook scripts.ipynb
```

Run all notebook cells sequentially.

---

# Limitations

- Small dataset size
- No expert-labeled validation data
- No true geometric height estimation
- Heuristic-based scoring
- No object localization stage

---

# Future Improvements

- YOLOv8-based transformer detection
- Pole/wire localization
- Monocular depth estimation
- Real-world annotated datasets
- Drone-based inspection systems

---

# Author

## Komal Kumar Naidu Bonu

- B.Tech CSE — GITAM University
- B.Sc Data Science — IIT Madras
