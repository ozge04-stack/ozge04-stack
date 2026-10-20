<div align="center">

# AI-Assisted Forest Fire Risk Prediction & Decision Support

**Multi-source environmental data · Machine learning · Geospatial risk mapping**

Graduation project for short-term forest-fire risk prediction in **İzmir, Muğla, and Antalya, Türkiye**.

[English](#project-overview) · [Türkçe](#türkçe)

![Project workflow](./assets/project-workflow.svg)

</div>

## Project overview

Forest fires are influenced by interacting weather, terrain, vegetation, land-cover, historical-fire, and human-activity factors. This project combines multiple environmental data groups to estimate whether a **2 km × 2 km grid cell** may experience a fire within the following **five days**.

The modelling workflow is connected to a Streamlit-based decision-support interface designed to display grid-level risk scores and highlight higher-risk cells.

> **Responsible use:** This is a research prototype, not an official warning service. It should not be used as the sole basis for emergency response or public-safety decisions.

## At a glance

| Item | Description |
|---|---|
| Study areas | İzmir, Muğla, Antalya — Türkiye |
| Spatial unit | 2 km × 2 km grid cells |
| Prediction horizon | Fire occurrence within the next 5 days |
| Target variable | `next_5d_fire` |
| Models compared | Random Forest, XGBoost, Balanced XGBoost, LightGBM |
| Final model family | City-specific Random Forest variants |
| Decision threshold | 0.60 |
| Interface | Streamlit map-based decision-support prototype |

## Methodology

1. **Multi-source data preparation:** historical fire detections, weather, terrain, land cover, NDVI, and human-proximity features.
2. **Spatial-temporal modelling table:** daily observations aligned to 2 km × 2 km grid cells.
3. **Target engineering:** `next_5d_fire` indicates whether a fire occurs in the same grid cell during the following five days.
4. **Model comparison:** Random Forest, XGBoost, Balanced XGBoost, and LightGBM.
5. **Evaluation:** accuracy, ROC-AUC, precision, recall, F1-score, and confusion matrices.
6. **Decision-support interface:** city/date selection and grid-level risk visualisation.

### Data sources and feature groups

| Group | Role | Reference |
|---|---|---|
| Historical fire activity | Past fire detections and spatial-temporal patterns | [NASA FIRMS](https://firms.modaps.eosdis.nasa.gov/) |
| Weather | Temperature, precipitation, wind, and derived weather indicators | [Open-Meteo Historical API](https://open-meteo.com/en/docs/historical-weather-api) |
| Forecast weather | Current/future weather inputs where used by the interface | [Open-Meteo Forecast API](https://open-meteo.com/en/docs) |
| Topography | Elevation and terrain-derived characteristics | [OpenTopography](https://opentopography.org/) |
| Vegetation | NDVI-based vegetation condition indicators | Satellite-derived vegetation data |
| Land cover | Grid-level land-cover characteristics | Processed geospatial layers |
| Human proximity | Distance-based indicators for settlements, roads, and selected activity locations | [OpenStreetMap](https://www.openstreetmap.org/) and processed layers where applicable |

Check each provider's current terms, licences, coverage, and attribution requirements before reusing data.

## Reported final results

The thesis reports city-specific final models and a decision threshold of **0.60**.

![Reported model metrics](./assets/model-results.svg)

| Study area | Selected feature configuration | Accuracy | ROC-AUC | F1-score |
|---|---|---:|---:|---:|
| İzmir | Common + Road + NDVI Random Forest | 0.9588 | 0.9845 | 0.7927 |
| Muğla | Common + Road + NDVI Random Forest | 0.9752 | 0.9929 | 0.8666 |
| Antalya | NDVI Random Forest | 0.9649 | 0.9897 | 0.8253 |

Random Forest variants provided the strongest final results among the compared approaches in the reported experiments. The selected feature configuration varied by city.

**Interpretation note:** Accuracy can be misleading when fire events are rare. ROC-AUC and F1-score are included to provide additional perspectives, but real-world generalisation still requires careful spatial and temporal validation.

## Decision-support concept

The interface was designed to let a user choose a study area and date, inspect grid-level risk scores on a map, and review high-risk grid cells. The current public repository contains project documentation and illustrative diagrams; it does **not** yet include the complete executable Streamlit application, trained model files, or source datasets.

## Technology and methods

- **Python** — data processing and modelling
- **pandas / NumPy** — tabular data preparation
- **scikit-learn** — model training and evaluation
- **Random Forest, XGBoost, Balanced XGBoost, LightGBM** — model comparison
- **GIS / geospatial processing** — grid-based spatial analysis
- **Remote sensing concepts** — NDVI and land-cover features
- **Streamlit** — decision-support interface

Package versions should be captured from the original working environment before the project is made reproducible.

## Repository contents and reproducibility

This repository currently includes a public-facing explanation of the research, reported headline results, and SVG diagrams. It does not contain the full modelling code, raw data, trained model binaries, or a tested dependency file. Therefore, the project cannot yet be reproduced or launched from this repository alone.

Recommended next additions:

- `notebooks/`: cleaned, reproducible notebooks for data preparation and model evaluation
- `src/`: reusable feature-engineering and modelling modules
- `app/`: the Streamlit application source
- `data_dictionary.md`: definitions, units, and source of each feature
- `requirements.txt`: verified package versions
- `tests/`: validation tests for preprocessing and prediction logic

Do not publish API keys, personal information, restricted data, or large raw datasets. Check academic-sharing permissions before publishing the full thesis or original data.

## Limitations and future work

- Validate generalisation using spatial and temporal holdout strategies.
- Assess probability calibration and prediction uncertainty.
- Document data periods, feature definitions, preprocessing, random seeds, and split strategy.
- Add explainability (for example, SHAP) only after verifying the implementation and assumptions.
- Track source timestamps and provide clear map legends before any operational use.

Historical test performance does not guarantee future operational performance. This project estimates grid-level short-term fire occurrence risk; it does not detect active fires or predict fire spread.

---

## Türkçe

### Proje özeti

Bu bitirme projesi, **İzmir, Muğla ve Antalya** için çok kaynaklı çevresel veriler kullanarak kısa vadeli orman yangını riskini tahmin etmeyi ve sonuçları harita tabanlı bir karar destek arayüzünde sunmayı amaçlar.

Çalışma alanları **2 km × 2 km grid hücrelerine** ayrılmıştır. `next_5d_fire` hedef değişkeni, ilgili hücrede seçilen tarihten sonraki **beş gün içinde yangın meydana gelip gelmediğini** ifade eder.

NASA FIRMS yangın kayıtları; meteorolojik değişkenler, topografya, arazi örtüsü, NDVI ve beşerî faktörlerle ilgili değişkenlerle bir araya getirilmiştir. Random Forest, XGBoost, Balanced XGBoost ve LightGBM algoritmaları karşılaştırılmış; accuracy, ROC-AUC, precision, recall ve F1-skoru gibi metrikler değerlendirilmiştir.

### Şehir bazlı final sonuçlar

| Şehir | Seçilen model | Accuracy | ROC-AUC | F1-skoru |
|---|---|---:|---:|---:|
| İzmir | Common + Road + NDVI Random Forest | 0,9588 | 0,9845 | 0,7927 |
| Muğla | Common + Road + NDVI Random Forest | 0,9752 | 0,9929 | 0,8666 |
| Antalya | NDVI Random Forest | 0,9649 | 0,9897 | 0,8253 |

Final karar eşiği **0,60** olarak kullanılmıştır. En iyi öznitelik yapılandırması şehre göre değişmiştir.

### Sınırlılıklar

Bu depo şu anda proje dokümantasyonunu ve açıklayıcı SVG diyagramlarını içerir. Tam modelleme kodu, ham veri setleri, eğitilmiş model dosyaları ve test edilmiş bağımlılık listesi dahil değildir. Dolayısıyla uygulama bu depodan henüz doğrudan çalıştırılamaz.

Bu çalışma bir araştırma prototipidir; resmî yangın uyarı sistemi değildir ve acil durum kararlarında tek başına kullanılmamalıdır.

## References

- [NASA FIRMS](https://firms.modaps.eosdis.nasa.gov/)
- [Open-Meteo](https://open-meteo.com/)
- [OpenTopography](https://opentopography.org/)
- [OpenStreetMap](https://www.openstreetmap.org/)

**Özge Çakır** · Industrial Engineering · Data Analytics · Process Improvement  
[GitHub profile](https://github.com/ozge04-stack)
