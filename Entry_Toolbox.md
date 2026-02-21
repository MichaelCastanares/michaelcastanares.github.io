"Forecaster's Toolbox: Residuals and Error metrics"
(in progress)

In the age of Do-It-Yourself (DIY) projects, it is often important to have our own toolbox. While we find standard items in a toolbox such as pliers, screwdrivers, hammers, we all have specialized/particular go-to tools that would make our work easier. For me, that would be a drill or racquet screw-driver.

For time-series forecasters, the common tools would be benchmark models, residuals, and error metrics. In this blog, I will discuss and share these tools. My goal is to review these foundational tools that may be useful for forecasting.

Errors and how we measure them are important in building models, whether panel or time-series data. From my previous work, we often track the errors of our Machine Learning models and regularly assess their performance during model retraining.

**Data**. We will be using two datasets: (A) AUD/PH Exchange rate daily series source from the [Reserve Bank of Australia](https://www.rba.gov.au/statistics/historical-data.html#exchange-rates) and (B)  (?).


### A. Simple models

`Statsforecast` python package offers simple models that can be used as benchmark such ash Naive, Seasonal Naive, Random walk with drift, and historical average.

**Simple Naïve Model** uses the current value as it forecast for the next time-step, $t+1$, and is written as

$$ \hat{Y}_{t+1} = Y_t $$

**insight:**. If someone asks me what will be the AUD/PH exchange rate tomorrow, my guess would be that it will be the same as today. Usually time series tend to have "memory" and depend on the previous value. Unless there are certain surprises/shocks, we can say that tomorrow's exchange rate would just be "around" the 40Php/1AUD mark - here the range may be determined by the forecaster's confidence, e.g., say within 38 - 42 Php. Having models for exchange rate (that accounts for economic factors) together with forecaster's judgement will narrow the prediction range.

**Seasonal Naïve Model** uses the value from the past season as forecast for the next time-step,

$$ \hat{Y}_{t+1} = Y_{t-k} $$

**insight**. Seasonal Naive are useful particular for time-series that exhibit regular/seasonal patters. For example, the Australian Beer Production series with seasonal lag k = 4 Quarters or one year. It is better to assume that the next quarter Q3 2024 production level will be similar to that of the past year Q3 2023.


**Random Walk with Drift**. This is an extension of the Naïve model with a drift, $\delta$ and error term, $\epsilon_t$. The next time-step forecast is given by

$$ \hat{Y}_{t+1} = \delta + Y_t + \epsilon_t$$

The constant drift term will either produce and upward ($\delta >0$) or downward trend ($\delta < 0$). The error term is assumed to be from a white noise distribution $N(0,\sigma^2)$ with zero-mean and variance $\sigma^2$.



### B. Residuals
**Residuals**. In the context of time-series, residuals is "what is left" after fitting a model to the data - i.e., the difference between the actual(observed values, $y_t$) with the fitted values, $\hat{y}_t$.

$$ e_t = y_t - \hat{y}_t$$

The same notation is used when we compare an actual value against the model prediction which is called the "prediction error".

**insights**. Residual Diagnostics is an approach to assess the quality of the model. The residuals should have properties of a random noise (normally distributed and no serial correlation). We can use a distribution statistics and Auto-correlation function to visualize and test these properties.

Real-world time series often have shocks and surprises (patterns that were not found in the train set). These shocks will end up as part of the residuals unless accounted for.



### B. Error metrics
**Scale-dependent errors**. These are forecast errors that have the same scale as the data (inheriting the same unit of measure). Mean Absolute Error (MAE) and Root-Mean-Squared Error (RMSE) are some common examples

$$\text{MAE} = \frac{1}{n}\sum_{t=1}^n{y_t - \hat{y}_t} $$

$$\text{RMSE} = \sqrt{\frac{1}{n}\sum_{t=1}^n{(y_t - \hat{y}_t)^2}}

**insight**. I personally prefer MAE in reporting model performance to stakeholders as it is both easy to understand and compute. It provides a direct measure of how far I'm off in absolute terms.

However, for optimizing a forecast model, the choice of error metric will yield different results. A model optimized using MAE will lead to forecast close to the median value - less sensitive to data outliers. In contrast, optimizing using RMSE will lead to forecast close to the mean value - more sensitive to the presence of data outliers.

**Percentage Errors**.

**insights**. 


### C. Models
Brief description of the models.


**Final thoughts**



Codes used to generate the figures may be found here: [View Code Repository on GitHub]()

Disclaimer of AI use: Claude Sonnet was used to improve the flow of the discussion.

references:

https://otexts.com/fpppy/nbs/05-toolbox.html