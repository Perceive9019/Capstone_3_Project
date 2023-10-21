
# Electricity Demand Trends in Great Britain: A Time Series Exploration

![Electrical Grid](https://cdn.pixabay.com/photo/2023/05/16/15/34/wires-7997980_1280.jpg)

Explore the fascinating world of electricity demand in Great Britain using SARIMA and Prophet models. Uncover valuable insights into the nation's energy landscape.


## Introduction

Electricity demand forecasting is pivotal to the efficient operation and planning of any modern power grid. In an era where energy sustainability is of paramount importance, accurate demand forecasting ensures that energy production can be as efficient as possible, reducing waste and costs while maximizing the utilization of renewable resources.

For Great Britain, a region with a rich history of industrialization and a progressive approach to renewable energy adoption, understanding electricity demand patterns is more critical than ever. The National Grid ESO has been diligently gathering electricity demand data since 2009, with readings taken every 30 minutes, amounting to 48 entries daily. This consistent and extensive data collection presents a unique opportunity to apply advanced forecasting methods to gain deeper insights into future demand.

In this report, we employ two distinct forecasting methodologies: the Seasonal Autoregressive Integrated Moving Average (SARIMA) model and the Prophet model. Both have gained recognition for their capability to handle time series data effectively, but they each offer their nuances and advantages. By leveraging both models, we aim to provide a comprehensive analysis and forecast of Great Britain's electricity demand, comparing and contrasting the results obtained from each methodology.

The objective is not only to predict future short-term demands but to gauge the effectiveness of these models in the specific context of electricity demand forecasting for Great Britain. The insights derived will assist in better grid management, policy-making, and infrastructure planning.

Through the sections of this report, we will delve into the methodology used, the limitations faced during the analysis, the results obtained, and the recommendations of these findings for the broader electricity landscape of Great Britain.
## Data

We sourced the [National Grid ESO dataset](https://www.kaggle.com/datasets/albertovidalrod/electricity-consumption-uk-20092022/data) capturing electricity demand in Great Britain from 2009 onwards. This data is updated **twice and hour**, which means 48 entries per day. This makes this dataset ideal for time series forecasting.

![Time Series of Electricity Demand Over Time](https://github.com/Perceive9019/Capstone_3_Project/blob/main/4.%20_README_files/Time%20Series%20of%20Electricity%20Demand%20Over%20Time.jpg)
## Methodoloy

To understand the underlying patterns of electricity we had to consider both the historical data and the inherent seasonality present in the time series data. Therefore, our methodology combined rigorous data processing and the applications of two well-established forecasting models.

1. **Data Preprocessing**:
- **_Data Acquisition_**: The dataset was sourced from the National Grid ESO, capturing electricity demand in Great Britain from 2009 onwards. With 48 half-hourly entries per day, this amounted to a detailed time series dataset.
- **_Data Cleaning_**: An initial exploration revealed no presence of missing values or potential outliers. Such inconsistencies if present could adversely impact the quality of our forecasts. As such, missing data points were still addressed, and anomalies were rectified, ensuring that subsequent analyses were grounded in consistent and reliable data.
- **_Time Series Decomposition_**: A decomposition of the time series data was conducted to understand the underlying patterns. This revealed strong daily seasonal variations, affirming the existence of consistent seasonal patterns — a crucial observation for subsequent modeling.

![Fig. 1: Shows the  Seasonal Decomposition for the Month of January](https://github.com/Perceive9019/Capstone_3_Project/blob/main/4.%20_README_files/Seasonal%20Component%20for%20January%202021.jpg)

- **Data Transformation and Stationarity**: To ensure the effectiveness of time series forecasting models, especially SARIMA, it's imperative that the data exhibits stationarity (i.e., statistical properties like mean, variance, and autocorrelation are constant over time). Using the Augmented Dickey-Fuller (ADFuller) and KPSS tests, we ascertained that our time series data was non-stationary. Consequently, we applied differencing to transform the data, rendering it stationary. This step was crucial for the efficient functioning of the SARIMA model.

![Fig. 2: Shows the First Differencing of the ‘tsd’ column which we want to Forecast](https://github.com/Perceive9019/Capstone_3_Project/blob/main/4.%20_README_files/First%20Difference%20of%20tsd.jpg)

2. **SARIMA (Seasonal Autoregressive Integrated Moving Average)**:
- **_Model Selection_**: After visualizing the seasonal decomposition plot of our time series for the month of January, it became evident that the data exhibited significant seasonality. Given this observation, the SARIMA model, which inherently accounts for seasonality, was chosen as the best fit for this time series data.
- **_Parameter Optimization_**: The auto_arima function from the pmdarima library was employed to streamline the process of hyperparameter tuning. This function iteratively tested different combinations of the SARIMA parameters to identify the set that minimized the Akaike Information Criterion (AIC), a measure of the goodness of fit of an estimated statistical model. By doing so, we were able to determine the optimal parameters (p, d, q, P, D, Q) for our SARIMA model.
- **_Model Training and Forecasting_**: With the optimal parameters in hand, we partitioned our dataset into training (80%) and testing (20%) subsets. The SARIMA model was trained using the training data, following which forecasts were generated based on the test data. This split-sample validation method provided an empirical means to assess the out-of-sample forecasting capabilities of the SARIMA model.

3.  **Prophet Model**
Holiday Integration: One of the standout features of the Prophet model is its ability to incorporate holiday effects. We utilized the is_holiday column from our dataset to specify which days were holidays. By integrating this feature, we aimed to provide the model with more context, allowing it to take into account potential spikes or drops in electricity demand during holidays.

![Prophet Model Forecast Trend Component](https://github.com/Perceive9019/Capstone_3_Project/blob/main/4.%20_README_files/Prophet%20Forecast%20trend%20component.jpg)
![Prophet Model Forecast Daily component](https://github.com/Perceive9019/Capstone_3_Project/blob/main/4.%20_README_files/Prophet%20Forecast%20Daily%20component.jpg)
![Prophet Model Forecast Weekly component](https://github.com/Perceive9019/Capstone_3_Project/blob/main/4.%20_README_files/Prophet%20Forecast%20Weekly%20component.jpg)
![Prophet Model Forecast Yearly component](https://github.com/Perceive9019/Capstone_3_Project/blob/main/4.%20_README_files/Prophet%20Forecast%20Yearly%20component.jpg)
## Model Results

The time series analysis of Great Britain’s electricity demand provided insightful outcomes derived from using the SARIMA and Prophet models. Below is a thoughtful interpretation of the findings.

![Fig 3: SARIMAX Short Term Forecast](https://github.com/Perceive9019/Capstone_3_Project/blob/main/4.%20_README_files/SARIMAX%20Short-term%20Forecast.jpg)

- The forecasted data (in red ) stays close to the actual test data (in orange), especially in the early parts of the forecast (the beginning steps).
- As we move further into the forecast (towards the end of the 48 data points), we may expect the forecast to potentially diverge more from the test data since predicting further into the future is generally more uncertain. However, it is difficult to see that visually.
- Any discrepancies between the forecasted line and the actual test data line highlight areas where the model's predictions were off. We don't see that here.

![Fig 4: Prophet Model Forecast vs Actual Values](https://github.com/Perceive9019/Capstone_3_Project/blob/main/4.%20_README_files/Prophet%20Model%20Forecast%20vs%20Actual%20Values.jpg)

- The plot of the Prophet forecast is in blue (with uncertainty intervals in light blue) and the actual values from the test set are in red.
- This visual comparison gives a clear idea of how well the Prophet model has performed in predicting electricity demand in the test set's timeframe.
- The visual overlay of actual vs. forecasted values also provides a quick way to gauge model performance. Since the plots closely follow each other, it means the model is capturing the underlying patterns in the data.


![Model Results]([Model Results.jpg](https://github.com/Perceive9019/Capstone_3_Project/blob/main/4.%20_README_files/Model%20Results.jpg))

1. **SARIMA Model**: 
    - The SARIMA model showcased strong prediction abilities, achieving an RMSE of 411.27, representing only 1% of the data range. This low error shows high accuracy in its forecasts.

2. **Prophet Model**:
    - The Prophet model, which was fine-tuned with seasonal holiday patterns, yielded a higher RMSE of 10881.93. Although proficient at predicting demand trends, when compared to the SARIMA model's precision, the SARIMA model emerged as the more precise model.
## Limitations

1. **SARIMA Model Assumptions**:
- SARIMA assumes linearity and was limited to a subset of the data due to computational constraints. It might not fully capture the non-linear complexities of electricity demand.

2. **Prophet Model Simplifications**:
- The binary nature of holiday effects in the Prophet model oversimplifies their actual impact on electricity demand. It's important to consider other factors that affect demand during holidays.

3. **Long-term Predictions**:
- Long-term predictions for electricity demand, influenced by societal and technological trends, were not explored in this analysis. Further research is needed to understand future demand scenarios.
## Recommendations
1. Integration of Multiple Models
- While both SARIMA and Prophet demonstrated commendable forecasting capabilities, an ensemble approach like XGBoost—integrating forecasts from multiple models—could potentially enhance precision and account for diverse data characteristics.

2. Incorporating External Factors
- To further refine forecasts, it is essential to incorporate external factors such as severe weather conditions or major events that influence electricity demand fluctuations.

3. Periodic Retraining
- Models should be periodically retrained to remain attuned to the current state of the power system, accounting for any changes in demand patterns or system dynamics.
## Conclusion
Based on the time series analysis we conducted:

1. **Strong Seasonality**:
- The data exhibits strong daily, weekly, and yearly seasonality. This implies that electricity demand in Great Britain has consistent patterns that recur over time. For instance, there might be consistent spikes during certain times of the day, specific days of the week, or particular months of the year.

2. **Effect of Holidays**:
- By integrating holiday effects into the Prophet model, we observed that holidays influence electricity demand. This suggests that certain holidays or holiday periods may see a noticeable rise or fall in electricity demand.

3. **Model Predictions**:
- The SARIMA model, even when trained on a subset of the data, demonstrated robust forecasting capabilities. This suggests that short-term forecasts, based on recent trends, can be quite reliable. The Prophet model, on the other hand, while competent, had a higher RMSE when compared to SARIMA.

4. **Model Predictions**:
- The fact that we had to subset our data for the SARIMA model due to computational constraints means we primarily focused on more recent trends, which may or may not continue into the distant future.

**Considering the above points, we can infer that**:
- Electricity demand in Great Britain will continue to exhibit daily, weekly, and yearly seasonal patterns.
- Certain holidays or holiday periods will likely see variations in demand, and understanding these can be crucial for effective demand management.
- While our models provide a reliable forecast in the short-term, predicting further into the future is more uncertain, especially considering potential broader societal and technological shifts.

