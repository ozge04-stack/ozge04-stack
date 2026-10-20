# Yapay Zekâ Destekli Orman Yangını Risk Tahmini ve Karar Destek Sistemi

**Çok kaynaklı çevresel veri · Makine öğrenmesi · Coğrafi risk haritalama**

İzmir, Muğla ve Antalya için kısa vadeli orman yangını riskini tahmin etmeyi amaçlayan Endüstri Mühendisliği bitirme projesi.

[English README](./README.md) · [Metodoloji notları](./METHODOLOGY.md)

![Proje iş akışı](./assets/project-workflow.svg)

## Proje amacı

Orman yangını riski tek bir meteorolojik değişkenle açıklanamaz. Bu çalışmada geçmiş yangın kayıtları; meteorolojik, topografik, arazi örtüsü, bitki örtüsü (NDVI) ve beşerî faktörlerle ilgili değişkenlerle birleştirilerek kısa vadeli tahmin yaklaşımı geliştirilmiştir.

Çalışma alanları **2 km × 2 km grid hücrelerine** ayrılmıştır. `next_5d_fire` hedef değişkeni, ilgili hücrede seçilen tarihten sonraki **beş gün içinde yangın meydana gelip gelmediğini** ifade eder.

## Veri kaynakları ve değişken grupları

- **Yangın kayıtları:** [NASA FIRMS](https://firms.modaps.eosdis.nasa.gov/)
- **Meteoroloji:** [Open-Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api) ve [Forecast API](https://open-meteo.com/en/docs)
- **Topografya:** [OpenTopography](https://opentopography.org/)
- **Bitki örtüsü:** Uydu tabanlı NDVI göstergeleri
- **Arazi örtüsü:** Grid düzeyinde arazi örtüsü özellikleri
- **Beşerî faktörler:** [OpenStreetMap](https://www.openstreetmap.org/) ve işlenmiş coğrafi katmanlar

## Modelleme yaklaşımı

Random Forest, XGBoost, Balanced XGBoost ve LightGBM algoritmaları karşılaştırılmıştır. Değerlendirmede accuracy, ROC-AUC, precision, recall ve F1-skoru gibi metriklerden yararlanılmıştır. Final karar eşiği 0,60 olarak raporlanmıştır.

## Şehir bazlı final sonuçlar

![Model sonuçları](./assets/model-results.svg)

| Şehir | Seçilen model | Accuracy | ROC-AUC | F1-skoru |
|---|---|---:|---:|---:|
| İzmir | Common + Road + NDVI Random Forest | 0,9588 | 0,9845 | 0,7927 |
| Muğla | Common + Road + NDVI Random Forest | 0,9752 | 0,9929 | 0,8666 |
| Antalya | NDVI Random Forest | 0,9649 | 0,9897 | 0,8253 |

## Karar destek sistemi

Projenin Streamlit tabanlı arayüzü, şehir ve tarih seçimiyle grid bazlı risk haritası ve yüksek riskli hücrelerin incelenebilmesi amacıyla tasarlanmıştır.

## Depo içeriği ve sınırlılıklar

Bu depo şu anda proje dokümantasyonunu, metodoloji notlarını ve açıklayıcı SVG diyagramlarını içerir. Tam modelleme kodu, ham veri setleri, eğitilmiş model dosyaları ve test edilmiş bağımlılık listesi dahil değildir. Dolayısıyla uygulama bu depodan henüz doğrudan çalıştırılamaz.

Bu çalışma bir araştırma prototipidir; resmî yangın uyarı sistemi değildir ve acil durum kararlarında tek başına kullanılmamalıdır. Tarihsel test performansı gelecekte aynı başarının garanti edildiği anlamına gelmez.

## İletişim

**Özge Çakır** · Endüstri Mühendisliği · Veri Analitiği · Süreç İyileştirme

[GitHub profili](https://github.com/ozge04-stack)
