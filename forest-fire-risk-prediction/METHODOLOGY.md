# Methodology Notes

This page summarises the methodology described in the graduation thesis. It is documentation, not a substitute for the original modelling code.

## Research question

Can multi-source environmental and historical-fire information help estimate whether a 2 km × 2 km grid cell in İzmir, Muğla, or Antalya will experience a fire within the following five days?

## Target definition

- **Spatial unit:** 2 km × 2 km grid cell
- **Temporal unit:** daily observations
- **Target:** `next_5d_fire`
- **Meaning:** whether a fire event is recorded in the same grid cell within the next five days

## Feature groups

- Historical fire detections and prior fire behaviour
- Meteorological observations and derived weather variables
- Topographic characteristics
- Land-cover features
- Satellite-derived vegetation indicators such as NDVI
- Human-proximity indicators, such as distance to roads and settlements, where available

## Models compared

- Random Forest
- XGBoost
- Balanced XGBoost
- LightGBM

The thesis reports city-specific Random Forest variants as the final selected models. The final classification threshold reported is 0.60.

## Evaluation

The reported evaluation includes accuracy, ROC-AUC, precision, recall, F1-score, and confusion matrices. Since forest fires are rare events, accuracy should not be interpreted alone.

## Reported headline metrics

| Study area | Accuracy | ROC-AUC | F1-score |
|---|---:|---:|---:|
| İzmir | 0.9588 | 0.9845 | 0.7927 |
| Muğla | 0.9752 | 0.9929 | 0.8666 |
| Antalya | 0.9649 | 0.9897 | 0.8253 |

## Reproducibility items still needed

Before the implementation can be independently reproduced, add and verify:

1. Exact date ranges and source versions for every dataset.
2. A feature dictionary with units and missing-value handling.
3. The spatial join/grid assignment rules.
4. The train/test split method and random seeds.
5. The complete preprocessing and model-training code.
6. Verified package versions and setup instructions.
7. Spatial and temporal holdout validation.

## Data stewardship and limitations

Check each source's licence and attribution requirements. Do not commit credentials, personal information, or restricted datasets. The project is a research prototype, not an official fire-warning service. It estimates grid-level short-term fire occurrence risk; it does not detect active fires or predict fire spread.
