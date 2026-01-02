# 🐟 Fish Classification with Deep Learning

This project implements a deep learning–based fish classification system using **MobileNetV2**.
The goal is to classify **9 different fish species** from images and to analyze the impact of **data augmentation** on model performance.

Both **augmentation (aug)** and **no-augmentation (no_aug)** training strategies are implemented, evaluated, and compared.

---

## 📂 Dataset

- Total images: ~9000  
- Number of classes: **9**
- Each class contains approximately **1000 images**
- Dataset is split as follows:
  - **Training:** ~64%
  - **Validation:** ~16%
  - **Test:** ~20% (≈1800 images)

Ground-truth (GT) images are removed during preprocessing to prevent data leakage.

---

## 🐠 Fish Classes

The dataset contains the following fish species:

- Black Sea Sprat  
- Gilt-Head Bream  
- Horse Mackerel  
- Red Mullet  
- Red Sea Bream  
- Sea Bass  
- Shrimp  
- Striped Red Mullet  
- Trout  

---

## ⚙️ Model Architecture

- Backbone: **MobileNetV2**
- Pretrained weights: **ImageNet**
- Input sizes:
  - **No Augmentation:** 224 × 224
  - **Augmentation:** 160 × 160
- Optimizer: **Adam**
- Loss function: **Categorical Cross-Entropy**
- Output layer: **Softmax (9 classes)**

Data augmentation (rotation, zoom, flip, translation) is applied **inside the model architecture** for the augmented version.

---

## 🚀 Training Strategy

Two separate models are trained:

### 1️⃣ No Augmentation Model
- Trained using original images only
- Serves as a baseline model
- Achieves very high accuracy on clean test data

### 2️⃣ Augmentation Model
- Trained with data augmentation techniques
- Improves robustness and generalization
- Slightly lower accuracy on clean test data but better generalization behavior

---

## 📊 Evaluation

Models are evaluated using the **test dataset**, which is completely unseen during training.

Evaluation metrics include:
- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix (raw and normalized)

### Key Results
- **No-Augmentation Model:** ~100% test accuracy  
- **Augmentation Model:** ~92% test accuracy  

The difference highlights the effect of data augmentation on model generalization.

---

## 🔍 Data Leakage Check

To ensure experimental correctness:
- Train, validation, and test sets are strictly separated
- File-level overlap checks confirm **no data leakage**
- Preprocessing consistency is strictly enforced between training and testing

---

## 🖼️ Visualization

The project includes:
- Visualization of sample images from each fish class
- Confusion matrices for both models
- Normalized confusion matrices for clearer interpretation

---

## 🛠️ Technologies Used

- Python
- TensorFlow / Keras
- NumPy
- Pandas
- Scikit-learn
- Matplotlib

---
## 🧠 Trained Models

The trained models exceed GitHub's file size limit and are therefore hosted externally on Google Drive.

- **No-Augmentation Model:** MobileNetV2, input size 224×224  
  🔗 [Download from Google Drive][(https://drive.google.com/drive/folders/1sP5-0nsiGLENyXN_cGaunnadIeFlXP_y?usp=drive_link)]

- **Augmentation Model:** MobileNetV2 with data augmentation, input size 160×160  
  🔗 [Download from Google Drive][(https://drive.google.com/drive/folders/1Eep8fYKBKcw0_6GP0hzI3WBcnRtEuhzU?usp=drive_link)]


## 📁 Project Structure

```text
├── outputs/
│   ├── <run_id>/
│   │   ├── no_aug/
│   │   │   ├── model/
│   │   │   └── history.csv
│   │   ├── aug/
│   │   │   ├── model/
│   │   │   └── history.csv
├── Fish_Dataset/
├── train.ipynb
├── test.ipynb
└── README.md
