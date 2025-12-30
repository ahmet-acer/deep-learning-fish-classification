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
