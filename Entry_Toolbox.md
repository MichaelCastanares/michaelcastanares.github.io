---
layout: default
title: Blog
---

[Home](/) | [Research Blog](/blog)

---
### "Forecaster's Toolbox: Residuals and Error metrics"
*1 March 2026*

In the age of Do-It-Yourself (DIY) projects, it is essential to have a toolbox. We all have go-to tools that make our work easier. For me, that would be a drill or ratchet screw-driver.

For time-series forecasters, the common tools would be benchmark models, residuals, and error metrics. In this blog, I will discuss and share these tools. My goal is to introduce and review these foundational tools useful for us forecasters.

**Data**. We will be using the AUD/PH Exchange rate daily series source from the [Reserve Bank of Australia](https://www.rba.gov.au/statistics/historical-data.html#exchange-rates).

<img src="images/Blog_Toolbox_1.png?raw=true"/>

*Source: Reserve Bank of Australia*

### A. Simple models

`Statsforecast` python package offers simple benchmark models such as: Naive, Seasonal Naive, Random walk with drift, and historical average. We can use these models as benchmarks when comparing performance of novel Machine Learning models.

**Simple Naïve Model** uses the current value as its forecast for the next time-step, $t+1$, and is written as

$$ \hat{Y}_{t+1} = Y_t $$

**insight:**. If someone asks me what will be the AUD/PH exchange rate tomorrow, my guess would be that it will be the same value as today - a naive guesstimate. Usually time series tend to have "memory" and depend on the previous value. Unless there are certain surprises/shocks, we can say that tomorrow's exchange rate would just be "around" the 40Php/1AUD mark - here the range is determined by the forecaster's confidence, e.g., say within 38 - 42 Php. This prediction range may be narrowed (more precise) by having models for exchange rate that accounts for economic factors together with forecaster's judgement.

**Seasonal Naïve Model** uses the value from the past season as forecast for the next time-step determined by the seasonal lag, $k$.

$$ \hat{Y}_{t+1} = Y_{t-k} $$

**insight**. Seasonal Naive are useful particularly for time-series that exhibit regular/seasonal patterns. Take for example the Australian Beer Production series with seasonal lag k = 4 Quarters or one year. It is a reasonable guesstimate that the next quarter Q3 2007 production level will be similar to that of the past year Q3 2006.

<img src="images/Blog_Toolbox_6.png?raw=true"/>

**Random Walk with Drift**. This is an extension of the Naïve model with a drift, $\delta$ and error term, $\epsilon_t$. The next time-step forecast is given by

$$ \hat{Y}_{t+1} = \delta + Y_t + \epsilon_t$$

The constant drift term will either produce and upward ($\delta >0$) or downward trend ($\delta < 0$). The error term is assumed to be from a white noise distribution $N(0,\sigma^2)$ with zero-mean and variance $\sigma^2$.

**insight**. We can reconstruct a random walk model using by randomly sampling the $\epsilon_t$ from a white noise distribution. We can apply recursion equation above and create different "realizations/paths" for $Y$, i.e., a combination of sequence $[Y_{t+1},Y_{t+2},Y_{t+3},...]$. (see example code)


> Lets apply this concepts to the AUD/Php Exchange rate time series.
>
> **Exchange rate**. For the exchange rate dataset, we split the series into train (December 2024 and earlier) and test set (January 2025). Since most of the naive models only require past values, there is no need not carry out any fitting - I will cover model fitting in the next few blog post.
>
>
> <img src="images/Blog_Toolbox_1.png?raw=true"/>
>
> *Source: Reserve Bank of Australia*
> 
> Now say that today is 31 January 2026. We are asked what would be our forecast of the AUD/PHP exchange rate for the next 20-days. We can apply the simple models (Naive, Seasonal Naive, and RWD) to make the forecast (see Figure below). Overlying the forecast with the test set, we can observe that estimates of the RWD and Naive model are higher compared to actual. The Seasonal Naive (with 7-day period) seems the capture the movement of the exchange rate but with a larger swing (amplitude).
>
> <img src="images/Blog_Toolbox_3.png?raw=true"/>
> 
> *Source: Reserve Bank of Australia; Author's estimates*
> 


Having established our benchmark models, let's now examine how we evaluate their performance.

### B. Residuals
**Residuals**. This is "what is left" after fitting a model to the data - i.e., the difference between the actual(observed values, $Y_t$) with the fitted values, $\hat{Y}_t$.

$$ e_t = Y_t - \hat{Y}_t$$

The same notation is used when we compare an actual value against the model prediction which is called the "prediction error".

**insights**. We can use Residual Diagnostics to assess the quality of the model. The residuals should have properties of a random noise (normally distributed and no serial correlation). We can use a distribution statistics and Auto-correlation function to visualize and test these properties.

Real-world time series often have shocks and surprises (patterns that were not found in the train set). These shocks will end up as part of the residuals unless accounted for.

> Going back to our example, ACF plot and statistical tests show that the residuals of the Naive model show is not auto-correlated; however, the residuals are not normally distributed.
> 
> <img src="images/Blog_Toolbox_2.png?raw=true"/>
> 
> *Source: Reserve Bank of Australia; Author's estimates*
> 


### C. Error metrics
**Scale-dependent errors**. These are forecast errors that have the same scale as the data (inheriting the same unit of measure). Mean Absolute Error (MAE) and Root-Mean-Squared Error (RMSE) are some common examples

$$\mathrm{MAE} = \frac{1}{n}\sum_{t=1}^n{Y_t - \hat{Y}_t} $$

$$\mathrm{RMSE} = \sqrt{\frac{1}{n}\sum_{t=1}^n{(Y_t - \hat{Y}_t)^2}} $$

**insight**. I personally prefer MAE in reporting model performance to stakeholders as it is both easy to understand and compute. It provides a direct measure of how far I'm off in absolute terms.

However, for optimizing a forecast model, the choice of error metric will yield different model results. A model optimized using MAE will lead to forecast close to the median value - less sensitive to data outliers. In contrast, optimizing using RMSE will lead to forecast close to the mean value - more sensitive to the presence of data outliers [Hyndman et al].

**Percentage Errors**.

The Mean Absolute Percentage Error is a popular measure of percentage error. 

$$ \mathrm{MAPE} = \frac{100}{n} \sum{\frac{|Y_t - \hat{Y}_t|}{|Y_t|}} $$

Research paper often use MAPE to report improvement of models from benchmark. In my experience, these values may be inflated particularly when the actual values are small (close to zero). Thus, its also important to read both MAPE in the conmathrm of the actual values.

As pointed by [Hyndman], MAPE tends to be bias towards under-estimate ($\hat{Y}_t < \hat{Y}$). To avoid this assymetry, it is suggested to use Scaled MAPE (sMAPE).

$$ \mathrm{sMAPE} = \frac{100}{n} \sum{\frac{2|Y_t - \hat{Y}_t|}{|Y_t + \hat{Y}_t|}} $$


**Directional Accuracy**

The Mean Directional Accuracy (MDA) is another metric we can use to assess the quality of our model. Aside from minimizing the residuals, forecasters/stakeholders want to get a sense of whether the indicator (GDP growth, inflation, etc) or indices (sentiment) is going up or down. MDA compares the forecast direction (up or down) relative to the actual direction [Wikipedia],

$$ \frac{1}{N}\sum_t{1_{sgn (A_t - A_{t-1})=sgn (F_t-A_{t-1})}} $$

The MDA takes up a values from [0,1]. Alternatively, I interpret it as "the fraction of times when the forecast moves with the direction of the actual indicator".

**insight**. MDA can be useful to investigate bias in the forecast. For example, one analysis I had showed a high RMSE but with high MDA. It turns out that there was a timepoint with a large error (data point measured during crisis - covid) that biased the error.This experience reminded me not to rely on a few metrics but check whether the results are robust and consistent. On the other end when you have a good forecasting model (lower RMSE), the residuals tend to be randomly distribution resulting also to a lower MDA. 

> We can examine at the histogram (or Kernel Density Estimate) and statistics of the forecast errors across difference models. We find that indeed the RWD and Naive model show over-estimation (Bias > 0). Meanwhile, the Seasonal Naive model shows slight under-estimation (Bias <0) but larger Mean Absolute Error. 
> 
> <img src="images/Blog_Toolbox_4.png?raw=true"/>
> 
> *Source: Reserve Bank of Australia; Author's estimates*


**D. Monte-Carlo Simulation**. 
While Python libraries offer a suite models that we can use, we can also produce forecast using monte-carlo simuations. Here I simulate a random walk with drift model (using Geometric Brownian Motion) and created 1,000 possible "paths" of forecast. The approach is to model the incremental change of the prices day-by-day, `log_returns`.

$$
\mathrm{log returns} = \log{P_t} - \log{P_{t-1}}
$$

<<<<<<< HEAD
We estimate the statistic (i.e., $\mu$ - drift per day, and $\sigma$ - volatility per day) from the train set: $\mu = \mathrm{mean(log returns)}, \sigma = \sqrt{\mathrm{var(log returns)}}$.
=======
 We estimate the statistic (i.e., $\mu$ - dift per day, and $\sigma$ - volatility per day) from the train set. $
\mu = \\mathrm{mean(log returns)}, \sigma = \sqrt{\\mathrm{var(log returns)}}$.
>>>>>>> 42db985c1066aa848e01576a37acd0423ad4b220

Using the fitted statistic, we calculate the drift and diffusion coefficients. We simulate a random walk path, $Z$, by drawing 20 values from a normal distribution.

$$
\mathrm{drift} = (\mu - \sigma^2/2) * dt
$$
$$
\mathrm{diffusion} = \sigma * \sqrt{dt} * Z
$$

The corresponding log_returns for each time-step is
$$
\mathrm{log\_ returns} = \mathrm{drift} + \mathrm{diffusion}
$$

We then propagate the initial price, $P_{t=0}$, by taking the cumulative sum, $
\mathrm{cum-log\ returns}_t = \sum_{i=0}{\mathrm{log\ returns}_i}^t$.

The resulting price path is
$$
P^{(k)} = P_{t=0} * \exp{\{\mathrm{cum-log\ returns}_t\}}
$$

> Back to our example, we can create several price paths, $P^{(k)}$ by iterating this process (see sample 50 paths below). In addition, we can generate say 1,000 possible paths take the percentiles to draw a confidence band. In our example, the AUD/PHP exchange rate of the test set is within 80% confidence band of forecast from our monte-carlo model.
><img src="images/Blog_Toolbox_5.png?raw=true"/>
> *Source: Reserve Bank of Australia; Author's estimates*
>


**Final thoughts**

This toolbox of simple benchmark models, residual diagnostics, and error metrics provides forecasters with standard tools to evaluate and validate their predictions. While simple models like Naïve and Random Walk with Drift may not capture all the complexities of real-world time series, they serve as important baselines against novel and machine learning models. In addition, monte-carlo simulations also provide a framework to forecasting by modelling the dynamics of the data. By combining multiple error metrics and diagnostic tools, forecasters can build confidence in their models and communicate uncertainties effectively to stakeholders.



Codes used to generate the figures may be found here: [View Code Repository on GitHub](https://github.com/MichaelCastanares/Github/tree/c2de492c5bb9f1a0e83da1ed738454e6a086bd01/TS_Toolbox)

Disclaimer of AI use: Claude Sonnet was used to improve the flow of the discussion.

references:

https://otexts.com/fpppy/nbs/05-toolbox.html

Hyndman, R.J., & Athanasopoulos, G. (2021). *Forecasting: principles and practice* (3rd ed.). OTexts. https://otexts.com/fpppy/nbs/05-toolbox.html

Wikipedia. Mean Directional Accuracy. https://en.wikipedia.org/wiki/Mean_directional_accuracy
