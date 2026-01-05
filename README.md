# 🐟 Derin Öğrenme ile Balık Türlerinin Sınıflandırılması

Bu proje, **MobileNetV2** mimarisini kullanarak derin öğrenme tabanlı bir balık sınıflandırma sistemi sunmaktadır. Çalışmanın temel amacı, 9 farklı balık türünü görüntüler üzerinden sınıflandırmak ve **veri artırma (data augmentation)** tekniklerinin model performansı üzerindeki etkisini analiz etmektir.

Proje kapsamında; veri artırma uygulanan (**aug**) ve uygulanmayan (**no_aug**) olmak üzere iki farklı eğitim stratejisi yürütülmüş, modellerin başarımları karşılaştırmalı olarak değerlendirilmiştir.

---

## 📂 Veri Seti Özellikleri

* **Toplam Görüntü Sayısı:** ~9.000
* **Sınıf Sayısı:** 9
* **Sınıf Başına Dağılım:** Her sınıf yaklaşık 1.000 görüntü içermektedir.
* **Veri Seti Bölümlemesi:**
* **Eğitim:** %64
* **Doğrulama (Validation):** %16
* **Test:** %20 (≈1.800 görüntü)


* **Ön İşleme:** Veri sızıntısını (data leakage) önlemek amacıyla, zemin gerçekliği (Ground-truth - GT) görüntüleri ön işleme aşamasında veri setinden çıkarılmıştır.
  
**Not:** Model, eğitim sürecinde yalnızca RGB (3 kanallı) görüntüler ile eğitilmiştir. Bu nedenle test aşamasında kullanılan dış kaynaklı görüntülerin de RGB formatında olması gerekmektedir. Özellikle .webp formatlı, alpha kanal içeren (RGBA) veya farklı renk profiline sahip (CMYK vb.) görüntüler, ön dönüştürme yapılmadan kullanıldığında hatalı veya düşük güvenli tahminlere yol açabilmektedir. Bu durumun önüne geçmek için test edilecek görüntülerin RGB formatına dönüştürülmesi önerilmektedir.

---

## 🐠 Sınıflandırılan Balık Türleri

Veri seti aşağıdaki balık türlerini içermektedir:

* Çaça (Black Sea Sprat)
* Çipura (Gilt-Head Bream)
* İstavrit (Horse Mackerel)
* Tekir (Red Mullet)
* Mercan (Red Sea Bream)
* Levrek (Sea Bass)
* Karides (Shrimp)
* Barbun (Striped Red Mullet)
* Alabalık (Trout)

---

## ⚙️ Model Mimarisi

* **Ana Omurga (Backbone):** MobileNetV2
* **Ön Eğitim:** ImageNet ağırlıkları kullanılmıştır.
* **Giriş Boyutları:**
* Veri Artırmasız Model: 224 × 224
* Veri Artırmalı Model: 160 × 160

* **Optimizasyon Algoritması:** Adam
* **Kayıp Fonksiyonu:** Kategorik Çapraz Entropi (Categorical Cross-Entropy)
* **Çıkış Katmanı:** Softmax (9 sınıf)
* **Veri Artırma:** Model mimarisine entegre edilmiş rotasyon, yakınlaştırma, çevirme ve kaydırma işlemleri uygulanmıştır.

---

## 🚀 Eğitim Stratejisi

İki ayrı model eğitilerek performans analizi yapılmıştır:

1. **Veri Artırmasız (Baseline) Model:** Yalnızca orijinal görüntülerle eğitilmiştir. Temiz test verileri üzerinde çok yüksek doğruluk değerlerine ulaşmaktadır.
2. **Veri Artırmalı Model:** Veri artırma teknikleriyle eğitilmiştir. Modelin genelleme yeteneği ve gürültülü verilere karşı dayanıklılığı artırılmıştır.

---

## 📊 Değerlendirme ve Bulgular

Modeller, eğitim sürecinde hiç görülmemiş olan **test veri seti** ile değerlendirilmiştir. Analizlerde aşağıdaki metrikler baz alınmıştır:

* Doğruluk (Accuracy)
* Kesinlik (Precision)
* Duyarlılık (Recall)
* F1-Skoru
* Karmaşıklık Matrisi (Raw & Normalized Confusion Matrix)

### Temel Sonuçlar:

* **Veri Artırmasız Model:** ~%100 test doğruluğu.
* **Veri Artırmalı Model:** ~%92 test doğruluğu.
* Elde edilen fark, veri artırmanın modelin genelleme kapasitesi üzerindeki doğrudan etkisini ortaya koymaktadır.

---

## 🔍 Veri Güvenilirliği (Data Leakage Check)

Deneysel doğruluğu sağlamak adına:

* Eğitim, doğrulama ve test setleri kesin çizgilerle ayrılmıştır.
* Dosya düzeyinde yapılan çakışma kontrolleriyle veri sızıntısı olmadığı teyit edilmiştir.
* Eğitim ve test aşamaları arasında ön işleme tutarlılığı korunmuştur.

---

## 🛠️ Kullanılan Teknolojiler

* Python
* TensorFlow / Keras
* NumPy
* Pandas
* Scikit-learn
* Matplotlib

---
 ## 🧠 Eğitilmiş Modeller
Eğitilen modellerin dosya boyutları GitHub'ın dosya boyutu sınırını aştığı için, modeller harici olarak Google Drive üzerinde  barındırılmaktadır.
---
- **No-Augmentation Model:** MobileNetV2, input size 224×224  
  🔗 [Download from Google Drive][(https://drive.google.com/drive/folders/1sP5-0nsiGLENyXN_cGaunnadIeFlXP_y?usp=drive_link)]

- **Augmentation Model:** MobileNetV2 with data augmentation, input size 160×160  
  🔗 [Download from Google Drive][(https://drive.google.com/drive/folders/1Eep8fYKBKcw0_6GP0hzI3WBcnRtEuhzU?usp=drive_link)]

---

## 📁 Proje Yapısı

├── outputs/
│   ├── <run_id>/
│   │   ├── no_aug/
│   │   │   ├── model/
│   │   ├── aug/
│   │   │   ├── model/
├── Fish_Dataset/
├── train.ipynb
├── test.ipynb
└── README.md
------------------------------------------------------------------------------------------------------------------------------
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
