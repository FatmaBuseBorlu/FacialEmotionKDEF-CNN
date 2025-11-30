# 🎭 KDEF Veri Seti ile CNN Tabanlı Duygu Tanıma

Bu proje, **Karolinska Directed Emotional Faces (KDEF)** veri setini kullanarak yüz ifadelerinin otomatik olarak tanınması için derin öğrenme tabanlı bir çözüm sunar. Yedi temel insan duygusu sınıflandırılmaktadır  

Happy, Sad, Angry, Disgust, Surprise, Fear ve Neutral  

Model, sıfırdan eğitilmiş bir evrişimsel sinir ağıdır (CNN).

[![Live Demo](https://img.shields.io/badge/Live-Demo-green?style=for-the-badge)](https://buzyy-emotion-recognition-app.hf.space)

> 🔬 Bu notebook, GPU hızlandırması için **Google Colab** üzerinde geliştirilmiş ve çalıştırılmış olup **GitHub** üzerinde barındırılmaktadır.  
> 📎 Makale tabanlı doğrulama referansı: *Goeleven ve ark., 2008*  [DOI:10.1080/02699930701626582](https://doi.org/10.1080/02699930701626582)

---

## 🧠 Veri Seti  KDEF Bilimsel Olarak Doğrulanmış

**Karolinska Directed Emotional Faces** veri tabanı, 70 oyuncunun (35 kadın, 35 erkek) yüz ifadelerini içeren 490 adet yüksek kaliteli renkli görüntü bulundurur. Her birey 7 duyguyu 5 farklı açıdan sergileyecek şekilde fotoğraflanmıştır.

✅ Tüm ifadeler şu açılardan doğrulanmıştır  
- **Duygu tanıma doğruluğu** (ortalama doğru tanıma oranı yaklaşık yüzde 72)  
- **Algılanan duygusal şiddet düzeyi**  
- **Uyarılma düzeyi**  SAM (Self Assessment Manikin) temelli değerlendirme

📌 Bu projede **frontal (A serisi)** görüntüler kullanılmış ve şu 7 etiket altında toplanmıştır  

`['angry', 'disgust', 'fear', 'happy', 'neutral', 'sad', 'surprise']`

---

## 🧰 Teknolojiler ve Kütüphaneler

- Python 3.10  
- TensorFlow ve Keras  
- OpenCV  görüntü yükleme ve işleme  
- Scikit learn  değerlendirme metrikleri  
- Google Colab  GPU destekli eğitim ortamı  

---

## 🏗️ Proje Aşamaları

1. **Veri Setinin Hazırlanması**  
   - `kagglehub` üzerinden indirildi  
   - Görüntüler `(96x96)` boyutuna yeniden ölçeklendi ve gri seviyeye dönüştürüldü  
   - Az temsil edilen sınıflar için veri dengeleme uygulandı

2. **Model Mimarisi**  
   - `Conv2D`, `MaxPooling`, `Dropout`, `Dense` katmanlarından oluşan özelleştirilmiş CNN  
   - Dropout ve early stopping ile düzenlileştirme  
   - 50 epoch boyunca eğitim  `ReduceLROnPlateau` ile öğrenme oranı dinamik olarak düşürüldü

3. **Değerlendirme**  
   - Eğitim ve doğrulama için accuracy ve loss eğrileri  
   - Confusion matrix  
   - Classification report  precision, recall ve F1 skorları

4. **Görselleştirme**  
   - Test tahminleri ile gerçek etiketlerin karşılaştırılması  
   - Duygu bazlı performans analizi

---

## 📈 Model Sonuçları

- 🧪 **Eğitim doğruluğu** yaklaşık yüzde 95  
- 🧪 **Doğrulama doğruluğu** yaklaşık yüzde 88  
- 📉 Aşırı öğrenme dropout ve early stopping ile kontrol altında tutuldu  
- 📊 **En iyi performans** Happy sınıfında, F1 skoru 0.90 üzeri  
- ⚠️ En çok karışan sınıflar  Fear  Surprise ve Sad  Neutral

---

## 📊 Confusion Matrix

Aşağıdaki confusion matrix, modelin her duygu kategorisini ne kadar doğru sınıflandırdığını göstermektedir.

![Confusion Matrix](./docs/confusion_matrix.png)

- En yüksek doğrulukla tahmin edilen sınıf  **Happy**  
- En çok karıştırılan sınıflar  **Fear ↔ Surprise** ve **Sad ↔ Neutral**

---

## 🖼️ Örnek Tahminler

Aşağıdaki tablo, rastgele seçilmiş bazı test örnekleri için gerçek ve tahmin edilen duyguları göstermektedir.

<table>
  <thead>
    <tr>
      <th>Görüntü</th>
      <th>Gerçek Etiket</th>
      <th>Tahmin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><img src="./docs/sample_1_disgust_disgust.png" width="120"/></td>
      <td>Disgust</td>
      <td>Disgust</td>
    </tr>
    <tr>
      <td><img src="./docs/sample_1_sad_fear.png" width="120"/></td>
      <td>Sad</td>
      <td>Fear 😬</td>
    </tr>
    <tr>
      <td><img src="./docs/sample_2_fear_fear.png" width="120"/></td>
      <td>Fear</td>
      <td>Fear</td>
    </tr>
    <tr>
      <td><img src="./docs/sample_3_surprise_fear.png" width="120"/></td>
      <td>Surprise</td>
      <td>Fear 😬</td>
    </tr>
    <tr>
      <td><img src="./docs/sample_3_neutral_neutral.png" width="120"/></td>
      <td>Neutral</td>
      <td>Neutral</td>
    </tr>
  </tbody>
</table>

<sub>*(Tüm örnekler, model çıkarımı sırasında rastgele seçilerek üretilmiştir.)*</sub>

---

## 🚀 Nasıl Çalıştırılır

Projeyi **Google Colab** üzerinde tamamen çalıştırmak için aşağıdaki rozete tıklayabilirsiniz  

<a href="https://colab.research.google.com/github/FatmaBuseBorlu/KDEF/blob/main/KDEF.ipynb" target="_blank">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open in Colab"/>
</a>

> Veri setini `kagglehub` üzerinden indirebilmek için Kaggle API anahtarı yapılandırılmalıdır.

---

## 📎 Kaynaklar

- Goeleven, E., De Raedt, R., Leyman, L., & Verschuere, B. 2008  
  *The Karolinska Directed Emotional Faces  A validation study*  Cognition & Emotion, 22(6), 1094 1118  
  [DOI 10.1080/02699930701626582](https://doi.org/10.1080/02699930701626582)

---

## 🪪 Lisans

Bu proje [MIT License](./LICENSE) kapsamında yayımlanmıştır.  
KDEF görsellerinin kullanımı akademik ve ticari olmayan lisansa tabidir. Resmi koşullar için [facialstimuli.com](http://www.facialstimuli.com) ile iletişime geçilmelidir.
