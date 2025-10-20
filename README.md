# NBA Second Half Total Prediction

Machine learning model to predict NBA second-half point totals and compare against Vegas betting lines.

## Quick Start
```bash
pip install -r requirements.txt

# Unzip the pre-computed features (saves ~1 hour of processing)
unzip nba_features_with_target.csv.zip

jupyter notebook nba_modeling_pipeline.ipynb
```

**Start from the "Model Training" section** - feature engineering is already done.

## Important Notes

**This repo uses pre-collected data files instead of live NBA API calls**

The notebook contains NBA API collection code, but you should **skip those cells** and use the included CSV files. The API calls:
- Are unreliable (random failures requiring multiple passes)
- Take hours to complete
- Pull extra data we don't use (injuries, starter/bench stats, etc.)

**Start from the "Feature Engineering" section of the notebook, or skip directly to "Model Training" since the pre-computed features are included.**

## Time-Saving Tip

Feature engineering takes approximately 1 hour to run. The pre-computed dataset (`nba_features_with_target.csv.zip`) is included - just unzip it and skip directly to modeling.

## Data Files Included

All CSV files are in the root directory:
- `nba_games_2021_to_2024.csv`
- `betting_data.csv`
- `*_COMBINED.csv` files (box scores, team stats, etc.)
- `nba_features_with_target.csv.zip` (pre-computed features)

## Key Results

**Model vs Vegas Line (2022-23 Test Season)**:
- Vegas: MAE 9.738, RMSE 12.618
- Our Model: MAE 9.735, RMSE 12.601
- **Result**: Marginal improvement - Vegas is very accurate

**Betting Threshold Test**:
- Best threshold (1.25 pt edge): 51.9% win rate, -1% ROI
- **Conclusion**: Not profitable for betting even with a 0.35% rakeback

## Key Insights

1. **Vegas is extremely accurate** - professional oddsmakers are hard to beat
2. **Feature engineering matters** - 1,300+ features compressed to 30 via PCA (likely due to features being derivatives of a relatively small number of stats)
3. **Second-half prediction is inherently difficult** - lots of variance even without considering things like injuries
4. **Data quality was challenging** - NBA API required multiple retry passes to get complete data, might be able to optimize this process better

## What's In This Project

- **Feature Engineering**: Rolling player/team stats (7/14/30 day windows), schedule factors, opponent adjustments, halftime state features
- **Models**: XGBoost baseline, Residual model (predicts deviation from Vegas line), PCA-reduced version
- **Evaluation**: Model comparison, betting threshold optimization, holdout validation

## Requirements

See `requirements.txt` - main packages:
- pandas, numpy
- scikit-learn
- xgboost
- jupyter

## License

This is a personal project for educational purposes.
