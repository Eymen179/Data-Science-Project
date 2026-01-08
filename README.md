# Titanic Hayatta Kalma Tahmini - Proje Raporu

*Ders:* Temel Makine Öğrenmesi (Deep Learning Project)
*Konu:* Titanic Veri Seti Üzerinde Sınıflandırma Analizi

---

## 1. Proje Özeti
Bu projenin amacı, Titanic felaketindeki yolcuların demografik (yaş, cinsiyet) ve seyahat (bilet sınıfı, biniş limanı) bilgilerini kullanarak hayatta kalıp kalamayacaklarını tahmin eden bir makine öğrenmesi modeli geliştirmektir. Proje, veri temizleme, görselleştirme, modelleme ve değerlendirme aşamalarından oluşmaktadır.

## 2. Veri Seti
Kullanılan veri seti: *Titanic - Machine Learning from Disaster*
- *Kaynak:* [DataScienceDojo GitHub](https://github.com/datasciencedojo/datasets/blob/master/titanic.csv)
- *Satır Sayısı:* 891
- *Özellikler:* Yolcu ID, Hayatta Kalma (Hedef), Bilet Sınıfı, İsim, Cinsiyet, Yaş, Kardeş/Eş Sayısı, Ebeveyn/Çocuk Sayısı, Bilet No, Ücret, Kabin, Biniş Limanı.

## 3. Metodoloji ve İşlemler

### A) Veri Ön İşleme (Preprocessing)
Doğru bir model kurmak için ham veri üzerinde şu işlemler yapıldı:
1.  *Eksik Veriler:*
    - Age (Yaş) sütunundaki eksikler, tüm yolcuların yaş ortalaması ile dolduruldu.
    - Embarked (Biniş Limanı) sütunundaki 2 eksik veri, en çok tekrar eden (mode) değer ile dolduruldu.
    - Cabin (Kabin) sütunu, verilerin %77'si eksik olduğu için veri setinden çıkarıldı.
2.  *Özellik Seçimi:*
    - Modelin öğrenmesine katkısı olmayan PassengerId, Name (İsim) ve Ticket (Bilet No) sütunları çıkarıldı.
3.  *Kategorik Dönüşüm:*
    - Sex (Cinsiyet): Kadın (1) ve Erkek (0) olarak sayısallaştırıldı.
    - Embarked (Liman): One-Hot Encoding yöntemiyle sayısal sütunlara dönüştürüldü.

### B) Modelleme
- *Algoritma:* Random Forest Classifier (Rastgele Orman Sınıflandırıcısı)
- *Parametreler:* 100 Karar Ağacı (n_estimators=100)
- *Eğitim/Test Ayrımı:* Verinin %70'i eğitim, %30'u test için ayrıldı.

## 4. Analiz Sonuçları

### Model Performansı
Modelimiz test verisi üzerinde *%79.10 Doğruluk (Accuracy)* oranına ulaşmıştır.

*Detaylı Sınıflandırma Raporu:*
| Durum | Kesinlik (Precision) | Duyarlılık (Recall) | F1-Skoru |
| :--- | :---: | :---: | :---: |
| *Hayatta Kalamayan (0)* | 0.81 | 0.84 | 0.82 |
| *Hayatta Kalan (1)* | 0.76 | 0.72 | 0.74 |

### Görselleştirmeler

#### 1. Karışıklık Matrisi (Confusion Matrix)
Modelin tahminlerinin ne kadarının doğru olduğunu gösterir.
![Confusion Matrix](./outputs/confusion_matrix.png)

#### 2. Cinsiyete Göre Hayatta Kalma
Kadınların hayatta kalma oranının erkeklere göre belirgin şekilde yüksek olduğu görülmüştür.
![Survival by Sex](./outputs/survival_by_sex.png)

#### 3. Korelasyon Matrisi
Özellikler arasındaki ilişkiyi gösterir. Sex (Cinsiyet) ve Survived (Hayatta Kalma) arasında güçlü bir ilişki gözlemlenmiştir.
![Correlation Matrix](./outputs/correlation_matrix.png)

## 5. Sonuç
Geliştirilen Random Forest modeli, Titanic yolcularının hayatta kalma durumunu %79 başarı oranıyla tahmin edebilmektedir. Yapılan analizler sonucunda, *cinsiyetin* hayatta kalma üzerinde en belirleyici faktör olduğu (kadınların öncelikli kurtarıldığı) ve *bilet sınıfının* da etkili olduğu görülmüştür.
