# 🐟 Deep Learning Fish Classification

Bu projede MobileNetV2 kullanılarak 9 farklı balık türü sınıflandırılmıştır.
Model TensorFlow/Keras ile eğitilmiş ve Grad-CAM ile görsel açıklanabilirlik sağlanmıştır.

## 📌 Kullanılan Teknolojiler
- Python
- TensorFlow / Keras
- MobileNetV2
- Grad-CAM
- Matplotlib, Seaborn
- Scikit-learn

## 📂 Veri Seti
Fish Dataset  
Her sınıftan görüntüler klasör yapısına göre etiketlenmiştir.

## 🧠 Model
- Önceden eğitilmiş MobileNetV2
- Transfer Learning
- EarlyStopping & ReduceLROnPlateau
- ModelCheckpoint (.keras formatı)

## 📊 Değerlendirme
- Accuracy
- F1-score
- Confusion Matrix
- Grad-CAM görselleştirmeleri

## Eğitilmiş Model
Eğitilmiş model dosyası GitHub'ın dosya boyutu sınırını aştığı için buraya yüklenememiştir.

Modeli şu bağlantıdan indirebilirsiniz:(https://drive.google.com/file/d/1Y18Iqr5mNig2giHBdg6zJekNbqrDadTG/view?usp=drive_link)


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
