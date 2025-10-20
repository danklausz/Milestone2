# NBA Second Half Total Prediction

Machine learning model to predict NBA second-half point totals and compare against Vegas betting lines.

## Quick Start
```bash
pip install -r requirements.txt
jupyter notebook nba_modeling_pipeline.ipynb
```
## Important Notes

**This repo uses pre-collected data files instead of live NBA API calls**

The notebook contains NBA API collection code, but you should **skip those cells** and use the included CSV files in the `data/` folder. The API calls:
- Are unreliable (random failures requiring multiple passes)
- Take hours to complete 

**Start from the "Feature Engineering" section of the notebook.**

## Data Files Required

Place these in the `data/` folder:
- `nba_games_2021_to_2024.csv`
- `betting_data.csv`
- `*_COMBINED.csv` files (box scores, team stats, etc.)

## Key Results

**Model vs Vegas Line (2022-23 Test Season)**:
- Vegas: MAE 9.738, RMSE 12.618
- Our Model: MAE 9.735, RMSE 12.601
- **Result**: Tiny improvement - Vegas line is very good

**Betting Threshold Test**:
- Best threshold (1.25 pt edge): 51.9% win rate, -1% ROI
- **Conclusion**: Not profitable for betting even with a 0.35% rakeback

## Key Insights

1. **Vegas is extremely accurate**
2. **Feature engineering matters** - 1,300+ features compressed to 30 via PCA (likely due to features being derivatives of a relatively small number of stats)
3. **Second-half prediction is inherently difficult** - Lots of variance! Even without considering things like injuries.
4. **Obtaining was challenging** - NBA API required multiple retry passes to get complete data, might be able to optimize this process better

## What's In This Project

- **Feature Engineering**: Rolling player/team stats, schedule factors, opponent adjustments
- **Models**: XGBoost baseline, Residual model (predicts deviation from Vegas), PCA version
- **Evaluation**: Model comparison, betting simulation, holdout validation

## Requirements

See `requirements.txt`

## License

This is a personal project for educational purposes.
