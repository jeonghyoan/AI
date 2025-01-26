# BA Term Project Report

**Project Duration:** Oct 2022 - Nov 2022

---

## Topic
**Predicting the price of cabbage to help consumers make decisions.**

- Multi-linear regression models tend to be overfitted, which increases the generalization error for new data.
- To address this issue, I utilized Ridge and Lasso regression techniques.

---

## Data
The dataset includes the following variables:
- Daily: Cabbage Price, Temperature, Rainfall
- Monthly: Imports and Exports, Consumer Price Index
- Yearly: Production per Area

---

## Preprocessing
- **Data Loading:** Loaded various datasets and removed commas from CSV files.

- **Cabbage Price Data:** Combined multiple daily cabbage price CSV files into a single DataFrame.

- **Renaming Columns:** Changed key column names for clarity, such as renaming '날짜' to '구분' in the rainfall data.

- **Merging Data:** Merged daily cabbage price data with temperature and rainfall data on '구분', extracted 'Year', 'Month', and 'Day', and dropped the '구분' column.

- **Production Data:** Renamed columns in the yearly production data and merged it with the daily dataset.

- **Consumer Price Index Processing:** Converted '시점' into 'Year' and 'Month', correcting October from '1' to '10', then merged.

- **Trade Data Processing:** Dropped rows with NA values, extracted 'Year' and 'Month' from '년월', and merged into the main dataset.

- **Data Cleaning:** 
  - Converted '수입액' and '수입량' to integers, removed rows with zero values, and merged.
  - Removed unnecessary features due to high VIF scores, including '최저기온(℃)', '최고기온(℃)', '생산면적 (ha)', '수입액($1000)', '수출액($1000)', and '강수량(mm)' due to low importance and excessive outliers.

- **Handling Missing Values:** Filled missing '생산량' values with the minimum production value.

- **Seasonal Column Creation:** Changed 'Month' to represent seasons, renamed to '계절', and created sine and cosine transformations. (to reflect cyclical properties instead of one-hot encoding.)
- 
- **Final Cleanup:** Dropped unnecessary columns. (Year, Day, 지점, 계절)
---

## Ridge & Lasso Regression: Cross Validation (Hyperparameter Tuning)
For each model, we determined the hyperparameter (degree, alpha) that yielded the highest verification score.

| Model  | Alpha          | Degree |
|--------|----------------|-------|
| Lasso  | 0.2811 | 5     |
| Ridge  | 0.1930 | 5     |

---

## Evaluation
We evaluated the performance on the test set using the best hyperparameters determined for each model.

| Metric     |      Lasso      |      Ridge      |
|------------|------------------|------------------|
| R² Score   |      0.9110      |      0.9096      |
| MSE        | 2,160,094.5365   | 2,193,466.1081   |
| RMSE       |    1,469.7260    |    1,481.0355    |
| MAE        |     818.3509     |     823.4675     |


---

## Conclusion
- Performance Comparison: Both models perform well, but Lasso regression shows a slight advantage in all evaluated metrics.
- Generalization: Lasso may generalize better to new data, potentially providing more reliable predictions for cabbage prices based on the features used in this study.
