# 🌍 Satellite Image Embedding Benchmarking and Clustering

## Overview
This project explores how pretrained computer vision models can be used to extract **embeddings from satellite imagery** and group similar image tiles using **unsupervised learning**.

The goal is to move beyond traditional supervised classification and build a **reproducible evaluation pipeline** for:

- embedding extraction  
- dimensionality reduction  
- clustering  
- model comparison  
- qualitative and quantitative evaluation  

---

## Objectives

- Convert satellite images into vector representations (embeddings)
- Compare pretrained models on representation quality
- Evaluate clustering performance using multiple metrics
- Identify patterns in land-use without relying on labels
- Build a reusable and extensible benchmarking workflow

---

## Dataset

This project uses the **EuroSAT dataset**, derived from Sentinel-2 satellite imagery.

- ~27,000 images  
- 10 land-use classes:
  - Forest  
  - Residential  
  - River  
  - Highway  
  - Industrial  
  - Crop fields  
  - Pasture  
  - Herbaceous vegetation  
  - Permanent crops  
  - Sea/lake  

---

## Methodology

### 1. Embedding Extraction
Images are passed through pretrained CNNs with classification heads removed:
- ResNet50 → 2048-dimensional embeddings  
- EfficientNet-B0 → 1280-dimensional embeddings  

---

### 2. Preprocessing
- Standardization using `StandardScaler`
- Dimensionality reduction using **PCA (2048 → 50 dimensions)**

---

### 3. Clustering
Two clustering methods are compared:

- **KMeans**
  - simple baseline
  - requires predefined number of clusters  

- **HDBSCAN**
  - density-based clustering
  - automatically determines cluster structure
  - identifies noise points  

---

### 4. Evaluation Metrics

| Metric | Description |
|------|------------|
| ARI | Agreement with true labels |
| NMI | Shared information between labels and clusters |
| Silhouette Score | Internal cluster separation |

---

### 5. Visualization
- UMAP projection for 2D visualization
- Cluster plots
- True-label comparison plots
- Sample images per cluster

---

## Model Comparison: ResNet50 vs EfficientNet-B0

### Why Compare These Models?

| Model | Strength |
|------|--------|
| ResNet50 | Strong baseline, widely used |
| EfficientNet-B0 | More parameter-efficient, often better feature representation |

---

## Benchmark Results

| Model | Clustering | ARI | NMI | Silhouette | Notes |
|------|------------|-----|-----|------------|------|
| ResNet50 | KMeans | ... | ... | ... | baseline |
| ResNet50 | HDBSCAN | ... | ... | ... | handles noise |
| EfficientNet-B0 | KMeans | ... | ... | ... | stronger features |
| EfficientNet-B0 | HDBSCAN | ... | ... | ... | best clustering |

👉 Replace `...` with values from your notebook output.

---

## Visual Results

### ResNet50

![ResNet50 KMeans](outputs/figures/resnet50_kmeans_umap.png)  
![ResNet50 HDBSCAN](outputs/figures/resnet50_hdbscan_umap.png)

---

### EfficientNet-B0

![EfficientNet KMeans](outputs/figures/efficientnetb0_kmeans_umap.png)  
![EfficientNet HDBSCAN](outputs/figures/efficientnetb0_hdbscan_umap.png)

---

## Key Insights

- EfficientNet often produces **more compact and separable embeddings**
- HDBSCAN outperforms KMeans in:
  - irregular cluster structures  
  - mixed land-use regions  
  - noisy satellite tiles  
- KMeans is useful as a **baseline**, but HDBSCAN provides more **realistic clustering**

---

## Why HDBSCAN is Often Superior

HDBSCAN is better suited for real-world satellite data because:

- no need to predefine number of clusters  
- handles varying density  
- identifies ambiguous samples as noise  
- adapts to complex embedding structures  

This is critical for satellite imagery, where regions are often mixed or transitional.

---

## Repository Structure

├── README.md
├── requirements.txt
├── notebooks/
│ ├── satellite_embedding_benchmark.ipynb
│ └── resnet_vs_efficientnet.ipynb
│
├── outputs/
│ ├── figures/
│ └── tables/
│
└── docs/
└── methodology.md


---

## Installation

```bash
pip install -r requirements.txt

Usage

Run the notebook in:

Google Colab or Jupyter

Steps:
Open notebook
Run all cells
View results
Export figures and tables

Outputs
Figures
UMAP cluster plots
True-label comparison plots
Tables

Model comparison results
Cluster assignments

🔗 Related Projects
NLP benchmarking: Twitter Sentiment Analysis
CNN baseline: Plant Seedling Classification
LLM system: DataPilot-AI


Future Work
Add Vision Transformers (ViT / CLIP)
Implement embedding fusion across models
Apply to real GeoTIFF satellite datasets
Build change detection pipeline
Add spatial clustering and geospatial mapping

Conclusion

This project demonstrates how embedding-based workflows can be used to:

discover structure in satellite imagery
evaluate pretrained models without supervision
build scalable pipelines for Earth observation

It provides a foundation for:
similarity search
anomaly detection
change detection
large-scale geospatial analysis

