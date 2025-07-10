# 🫁 Lung Cancer Classification using Deep Learning Ensemble

This project focuses on classifying lung histopathological images into different cancer types using **deep learning** and an **ensemble learning strategy**. By leveraging multiple CNN architectures and stacking their predictions into a **Logistic Regression** meta-classifier, the system improves diagnostic accuracy and robustness — a valuable contribution to **clinical decision-making in oncology**.

---

## 📌 Overview

### 🎯 Objective:
Classify histopathology lung tissue images into the following categories:
- `Lung Adenocarcinoma` (Malignant)
- `Lung Benign Tissue`
- `Lung Squamous Cell Carcinoma` (Malignant)

### 🧠 Solution Strategy:
1. Train three individual CNN models:
   -  **EfficientNetB0** (Fine-tuned)
   -  **VGG16** (Pretrained)
   -  **InceptionV3** (Pretrained)

2. Perform **Stacking Ensemble**:
   - Extract softmax predictions from each model
   - Feed them into a **Logistic Regression** meta-classifier
   - Output final prediction using ensemble confidence

---

## 📊 Dataset

- 📚 **Name**: [LC25000 Dataset (PMC10045080)](https://pmc.ncbi.nlm.nih.gov/articles/PMC10045080/)
- 🗂 **Subset Used**: Lung images only
- 🏷 **Classes**:
  - `lung_aca` — Lung Adenocarcinoma (Malignant)
  - `lung_bnt` — Benign Lung Tissue
  - `lung_scc` — Lung Squamous Cell Carcinoma (Malignant)
- 🖼 **Image Format**: `.jpeg`
- 📐 **Resized To**: `224 x 224` pixels

---

## ⚙️ Workflow Summary

### 1. 🧹 Preprocessing
- Resize all input images to `224 x 224`
- Normalize pixel intensities to [0, 1]
- Encode class labels
- Apply image augmentation:
  - Random flipping
  - Rotation
  - Zoom
- Split dataset into training, validation, and test sets

---

### 2. 🧠 Model Training

| Model         | Frozen Base | Custom Layers Added                     |
|---------------|-------------|------------------------------------------|
| EfficientNetB0|   Yes       | GAP → Dropout(0.5) → Dense (Softmax)     |
| VGG16         |   Yes       | Flatten → Dense(256) → Dropout(0.5) → Dense (Softmax) |
| InceptionV3   |   Yes       | GAP → Dense(1024) → Dropout(0.5) → Dense (Softmax)   |

- Loss: `Categorical Cross-Entropy`
- Optimizer: `Adam`
- Metric: `Accuracy`

---

### 3. 🔗 Stacking Ensemble

- **Input**: Softmax probabilities from EfficientNetB0, VGG16, InceptionV3
- **Meta-model**: `Logistic Regression`
- **Output**: Final predicted class
- Improves generalization and minimizes overfitting of individual CNNs

---

### 4. 📈 Evaluation

- 📊 Accuracy, F1-score, Confusion Matrix
- 🔍 Visual inspection of **actual vs predicted** class
  
---

