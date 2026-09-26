# Sensor Fusion Tabanlı Karar Destek ve Tehdit Önceliklendirme Sistemi

Endüstri mühendisliği kapsamında hazırlanmış bir **veri füzyonu + çok kriterli karar verme (ÇKKV)
tabanlı karar destek sistemi** prototipidir. Birden fazla sensörden (radar, IR, görüntü/EO) gelen
gürültülü ölçümler **Kalman filtresi** ile füzyonlanır; elde edilen füzyon çıktıları (mesafe, hız,
güven skoru) ve nesne tipi risk katsayısı **TOPSIS** yöntemiyle tek bir **öncelik skoruna**
dönüştürülerek nesneler tehdit önceliğine göre sıralanır.

> Tüm veriler **sentetik / simüle edilmiştir**; gerçek bir sensör, silah veya operasyonel sistemle
> bağlantısı yoktur. Amaç, veri füzyonu ve ÇKKV yöntemlerinin uçtan uca bir karar destek sistemi
> içinde nasıl bütünleştirilebileceğini göstermektir.

## Proje Sahibi
Ceren Gündüz — Endüstri Mühendisliği, 4. Sınıf

## İçerik

- `sensor_fusion_tehdit_onceliklendirme.ipynb` — tüm analiz tek notebook içinde (veri üretimi,
  füzyon, ÇKKV, görselleştirme).
- `ham_sensor_olcumleri.png` — füzyon öncesi ham sensör ölçümleri (örnek nesne).
- `tehdit_onceliklendirme.png` — TOPSIS öncelik skorlarına göre sıralanmış nesneler.
- `mesafe_hiz_dagilimi.png` — mesafe–hız uzayında öncelik skoruna göre renklendirilmiş dağılım.

## Yöntem

1. **Sentetik çok sensörlü veri üretimi:** 6 nesne için radar, IR ve görüntü sensöründen 10 zaman
   adımı boyunca gürültülü mesafe/hız ölçümleri üretilir; her sensörün gürültü seviyesi farklıdır.
2. **Sensör füzyonu (Kalman Filtresi):** 1D sabit hız modeli ile 3 sensörün mesafe ölçümleri ardışık
   olarak güncellenir, tek bir mesafe/hız tahmini ve sensörler-arası tutarlılığa dayalı bir
   **füzyon güven skoru** üretilir.
3. **TOPSIS ile önceliklendirme:** Mesafe (maliyet kriteri), hız, füzyon güven skoru ve nesne tipi
   risk katsayısı (fayda kriterleri) ağırlıklandırılarak (0.30 / 0.25 / 0.20 / 0.25) her nesne için
   0–1 aralığında bir öncelik skoru hesaplanır.
4. **Karar destek panosu:** Sonuçlar yatay bar grafiği ve mesafe–hız dağılım grafiği ile
   görselleştirilir.

## Nasıl Çalıştırılır

```bash
pip install numpy pandas matplotlib jupyter
jupyter notebook sensor_fusion_tehdit_onceliklendirme.ipynb
```

## Geliştirme Fikirleri

- Çoklu hedef takibi için Extended/Unscented Kalman Filtresi ve veri ilişkilendirme (data
  association) eklenmesi
- TOPSIS yanında AHP ile kriter ağırlıklarının uzman görüşüyle belirlenmesi
- Gerçek zamanlı akan veri için Plotly Dash / Streamlit tabanlı canlı bir dashboard
