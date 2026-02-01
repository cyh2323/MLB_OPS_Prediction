# MLB OPS Prediction

This project predicts the **2024 OPS (On-base Plus Slugging)** for MLB batters using historical batting statistics from 2015 to 2023. The model uses **Ordinary Least Squares (OLS) regression** with NumPy, taking into account each player’s last season stats, career averages, and the number of seasons played.

## Dataset

The dataset is sourced from **MLB Batting Data (2015-2024)** on Kaggle. Relevant columns include:

- `Player` – Player name
- `Year` – Season year
- `Age` – Age during the season
- `Team` – Team code
- `Lg` – League (AL, NL, or 2LG)
- `G` – Games played
- `AB, H, 2B, 3B, HR, RBI` – Core batting stats
- `BA, OBP, SLG, OPS` – Rate statistics
- `Pos` – Primary fielding position

## Features Used

The regression uses the following features:

- **Last season stats:** `Last_Age`, `Last_OPS`, `Last_OBP`, `Last_SLG`, `Last_HR`
- **Career mean stats:** `Mean_OPS`, `Mean_OBP`, `Mean_SLG`, `Mean_HR`
- **Number of seasons played:** `Year_played`

The target variable is `OPS_2024`.

## Methodology

- **Estimation Method:** OLS regression using **pseudo-inverse** (`np.linalg.pinv`) to handle potential singular matrices due to correlated or missing features.
- **Reason for Pseudo-Inverse:** Some players may have identical or missing features; pseudo-inverse ensures a solution without matrix inversion errors.

## Results

**Coefficient Table:**

| Variable       | Coefficient |
|----------------|------------|
| Intercept      | 0.5992     |
| Last_Age       | -0.0057    |
| Last_OPS       | 19.1037    |
| Last_OBP       | -18.2073   |
| Last_SLG       | -19.3967   |
| Last_HR        | 0.0024     |
| Mean_OPS       | -12.7585   |
| Mean_OBP       | 12.2670    |
| Mean_SLG       | 13.1832    |
| Mean_HR        | 0.0014     |
| Year_played    | 0.0046     |

- Coefficients indicate the contribution of each feature to the prediction of OPS.

**Evaluation Metrics:**

- MSE: 0.0084
- RMSE: 0.0917
- R-squared: 0.2335

## Interpretation

This analysis shows that **last season OPS, OBP, and SLG are the most predictive** of a player's next season OPS, while career averages provide additional context. The coefficients indicate how each feature contributes to the prediction of OPS:

- Positive coefficients increase predicted OPS, negative coefficients decrease it.
- Last season rate stats (OPS, OBP, SLG) have the largest magnitude, meaning recent performance strongly affects predictions.
- Year_played and last season HR have small positive impacts.
- R-squared (~0.23) indicates that while the model captures some variation, there is substantial unexplained variability, which is typical for sports performance data.
