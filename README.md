# SeoulBikeSharing Dataset Analysis - README

## Overview
This project focuses on analyzing the **SeoulBikeSharing** dataset to predict the number of rented bikes based on various environmental, seasonal, and temporal factors. By applying regression modeling techniques, we aim to uncover key insights about bike-sharing patterns in Seoul and identify the variables most influential in predicting bike demand.

## Dataset Description
The dataset consists of **14 variables**, with **Rented Bike Counts** as the dependent variable. The independent variables include:

- Date
- Hour
- Temperature
- Humidity
- Windspeed
- Visibility
- Dew Point Temperature
- Solar Radiation
- Rainfall
- Snowfall
- Seasons (Winter, Spring, Summer, Autumn)
- Functional Day (Non-Functional Hour and Functional Hour)

To facilitate regression modeling, dummy variables were created for categorical features:
- **Seasons**: Dum_Winter, Dum_Spring, Dum_Summer
- **Holiday**: IsHoliday (1 = Holiday, 0 = No Holiday)
- **Functioning Day**: IsFunctionalDay (1 = Yes, 0 = No)
- **Snowfall**: SnowfallDummy (1 = Snowfall, 0 = No Snowfall)

## Exploratory Data Analysis (EDA)
### Key Visualizations:
1. **Histogram - Rented Bike Count by Hour** (Figure B1):
   - Bike demand peaks at **8 AM** and **6 PM**.
   - The histogram shows a bimodal, left-skewed distribution.

2. **Scatter Plot - Temperature vs. Bike Rentals** (Figure B2):
   - A positive correlation exists between temperature and bike rentals, peaking between **20°C to 40°C**.
   - Bike demand significantly drops when the temperature falls below **0°C**.

3. **Boxplots & Frequency Tables**:
   - **Functional vs. Non-Functional Days**: 96.63% of bikes are rented on functional days (Figure B3.1, B3.2).
   - **Snowfall vs. No Snowfall**: Bike demand drastically decreases on days with snowfall (Figure B4.1, B4.2).

4. **Scatterplot Matrix** (Figure B5):
   - No strong linear relationships observed between Rented Bike Count and other variables.
   - Key insights:
     - Lower demand during colder periods.
     - Higher demand around **8 AM** and **6 PM**.
     - Rainfall decreases bike rentals.

5. **Multicollinearity Check**:
   - High correlation (~0.91) between **Temperature** and **Dew Point Temperature**. The latter was removed from the analysis to avoid multicollinearity.

## Linear Regression Analysis
The dataset was split into **80% training** and **20% testing** subsets. Three model selection techniques were employed:
1. **Forward Selection**
2. **Backward Elimination**
3. **Stepwise Selection**

The final model selected includes:
```
Rented Bike Count = Hour + Temperature + Humidity + Wind_Speed + Solar_Radiation + Rainfall + Dum_Winter + Dum_Spring + Dum_Summer + IsHoliday + IsFunctionalDay
```

### Outlier Removal:
Using diagnostic plots (e.g., Cooks Distance) to identify and remove influential data points, the dataset was reduced from **8760 to 8156 observations**. This improved the adjusted R-squared from **0.5500 to 0.5117**, ensuring a more robust model.

### Model Validation:
Both **backward elimination** and **stepwise selection** produced identical models, reinforcing the reliability of our final model. The model's predictive power was verified using RSME and R-squared metrics for both training and test data.

## Final Model Equation
```
Rented Bike Count = -188.39 + 27.259 * Hour + 26.108 * Temperature - 7.9786 * Humidity + 18.085 * Wind_Speed - 79.748 * Solar_Radiation - 59.924 * Rainfall - 366.1 * Dum_Winter + 144.83 * Dum_Spring + 154.57 * Dum_Summer - 120.09 * IsHoliday + 931.43 * IsFunctionalDay
```

## Key Insights:
- **Time of Day**: Peak bike demand at **8 AM** and **6 PM**.
- **Weather Impact**: Wind speed and visibility positively influence demand, while humidity and solar radiation have negative effects.
- **Seasonal Variations**: Bike demand decreases in winter and increases in spring and summer.
- **Functional Days**: Bike demand surges on functional days, especially when there's no holiday.

## Conclusion
This analysis sheds light on the critical factors that affect bike-sharing demand in Seoul. By addressing multicollinearity and refining our model, we provide a robust framework for predicting future bike rentals based on time, weather, and seasonal conditions.
