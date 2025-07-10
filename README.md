# 🫁 Lung Cancer Classification using Deep Learning Ensemble

This project classifies lung histopathology images into multiple cancer types using deep learning and ensemble learning techniques. By stacking predictions from CNN architectures into a logistic regression meta-classifier, it improves diagnostic performance and supports clinical decision-making in oncology.

---

## 📌 Overview

- **Goal**: Classify lung histopathology images into:
  - `Lung Adenocarcinoma` (malignant)
  - `Lung Benign Tissue`
  - `Lung Squamous Cell Carcinoma` (malignant)

- **Approach**:
  - ✅ Train three CNN models:
    - EfficientNetB0 (fine-tuned)
    - VGG16 (pretrained)
    - InceptionV3 (pretrained)
  - ✅ Use **stacking ensemble**:
    - Combine their predictions
    - Feed into **Logistic Regression** as meta-classifier

---

## 🧬 Dataset

- **Name**: [LC25000 Dataset](https://pmc.ncbi.nlm.nih.gov/articles/PMC10045080/)
- **Subset used**: **Lung only** (`lung_aca`, `lung_bnt`, `lung_scc`)
- **Classes**:
  - `lung_aca` – Lung Adenocarcinoma (malignant)
  - `lung_bnt` – Benign Lung Tissue
  - `lung_scc` – Lung Squamous Cell Carcinoma (malignant)
- **Image Format**: `.jpeg`, 250x250 color histopathology images

---

## ⚙️ Workflow Summary

1. **Data Preprocessing**:
   - Resize images to match model input (224x224 or 299x299)
   - Normalize pixel values
   - Encode class labels
   - Apply augmentation (flip, rotate, zoom)
   - Split into train, validation, test sets

2. **Model Training**:
   - Load each pretrained model (EfficientNetB0, VGG16, InceptionV3)
   - Fine-tune or freeze appropriate layers
   - Train with categorical cross-entropy loss
   - Save predictions

3. **Stacking Ensemble**:
   - Use predictions of all 3 models as features
   - Train a **Logistic Regression** classifier on them
   - Final prediction based on meta-model output

4. **Evaluation**:
   - Accuracy, F1-score, Confusion Matrix
   - ROC-AUC for multi-class
   - Visualizations using Grad-CAM (optional)

---
