---
layout: default
title: Blog
---

[Home](/) | [Blog](/blog) | [Projects](/projects)

---

### "Useful metrics to kickstart your analysis on time-series"
*Updated: 6 February 2026*

Time series data tells compelling stories about the past and hints at the future. Will housing prices in Australia continue rising? When does Australia see peak tourist arrivals? Understanding these patterns is vital for policy-making and business strategy.

While time series analysis can seem daunting, specialized tools like Python's `tsfeatures` package make it accessible. In this post, I'll share practical metrics for characterizing time series—tools I've used in my work and MSDS studies to as pre-cursor analysis towards building time-series models.

Before diving in, test your intuition with the figure below. What patterns do you notice? What research questions emerge?

<img src="images/Blog_TSFEATURES_1.png?raw=true"/>

The time-series is the "number of nights stayed" by Australian resident in a particular state. The data is sourced from the National Visitor Survey (Tourism Research Australia)

**The Metrics** 

**Decomposition.** A time-series can be decomposed into three components: Trend, Seasonal/Cyclic, and Innovations/Noise. The decomposition can either be linear or multiplicative. A linear decomposition can be written as

<img src="images/Blog_TSFEATURES_eq1.png?raw=true"/>

**Seasonality, and Cyclicity.** A time series is seasonal when it exhibits a regular, fixed pattern that aligns with the calendar (e.g., quarterly, annual) or weather  (e.g., summer, winter). Meanwhile, cyclic series exhibits patterns that follows other than calendar dates or season (e.g., business cycles, market cycles in Economics).

*Insights:* Seasonal and cyclic patterns in the series are straight forward to model due to their regularity. Take the tourism data of Tasmania. Plotting the seasonal plot (stacking the time-series per year) shows that most tourist visits happen during January (Summer). Meanwhile, September (start of spring) show the least volume of tourist visits - suitable for those who want to avoid the crowd.

<img src="images/Blog_TSFEATURES_2.png?raw=true"/>



**Trend.** Trend describes the general long-term movement of the time series whether its increasing, decreasing, or no change. As human, we also tend to think (or follow a straight path). We should be weary that when seeing an increasing series follow several paths (in the time steps): linearly increase, exponentially increase, exponential decrease, or remains the same.

*Insights:* A simple way to extract a trend in the series is to take a moving average (MA). MA smoothens out the series removing high frequency changes. One can control the smoothness using the window size - larger window size results to a more smoother series revealing long-term trend.

In `tsfeatures`, we can calculate the strength of trend and seasonality. The mathematical definitions of the metrics is descrived in Hyndman's book (https://otexts.com/fpp2/seasonal-strength.html). A parametric plot of the strength of trend and seasonality can be a straightforward analysis to assess several time series.

<img src="images/Blog_TSFEATURES_3.png?raw=true"/>

**Auto-correlation.** It's akin to "memory of the time series" - to what extent do past (or lagged) values are linearly related to the present values. Consider the simple example (an AR1 relation)

$$y_t = \alpha y_{t-1} + \varepsilon$$

Where $\alpha$ (the AR1 coefficient) captures the influence of the previous time step.

This is common but powerful relation which says that the present value is determined by a factor $\alpha$ of the recent past value ,$y_{t-1}$, and some noise, $\eta$. The AR1 coefficient, $\alpha$ can be estimated using an auto-correlation function (taking lag = 1)

*Insights:* In my work, I found that AR1 is typically a good baseline model that is hard to beat. It is elegant, powerful, and easy to explain. 


**Stationarity.** A series is stationary when its statistical properties (mean, variance) don't change over time. Most (linear) forecasting/statistical models assume/requires that the series is stationary. Statistical test for stationarity are Augmented Dickey-Fuller test and KPSS test.

*Insights:* Real-world time series are typically non-stationary. Preprocessing steps—such as taking first differences or computing annual growth rates—are often necessary before applying statistical models. Interestingly, complex machine learning models (e.g., Neural Networks, XGBoost) can handle non-stationary data directly.

<img src="images/Blog_TSFEATURES_4.png?raw=true"/>

The figure illustrates an iterative 3-step process: transform series, compute statistic, and explore. For Australian Housing prices, we calculate annual growth rates and apply ADF/KPSS tests for stationarity. Results show NSW and Victoria are stationary, while Queensland and ACT require additional transformations before linear modeling.

**Entropy.** This refers to the predictability (randomness) of the data. A Shannon spectral entropy metric has a value 0 for series with clear trend and seasonality and value close to 1 for noisy series.

*Insights:* Use entropy to assess data quality and preprocessing effectiveness. Lower entropy after cleaning indicates better signal extraction.

**Sample analysis.** Applying these tools to Queensland's tourism data reveals: a strong upward trend (trend strength = 0.82, visible in the 8-quarter moving average) and moderate seasonality (seasonal strength = 0.59). The series appears non-stationary visually and shows modest lag-1 autocorrelation (x_acf1 = 0.543)

<img src="images/Blog_TSFEATURES_5.png?raw=true"/>

**Final thoughts.** Understanding time series characteristics before modeling is essential. The metrics discussed here (decomposition, seasonality, trend, autocorrelation, stationarity, and entropy) provide a framework to kickstart the analysis. Researchers can capitalize python tools such as tsfeatures for their Exploratory Data Analysis. 

Codes used to generate the figures may be found here: [View Code Repository on GitHub](https://github.com/MichaelCastanares/Github/tree/main/TS_Metrics)

Disclaimer of AI use: Claude Sonnet was used to improve the flow of the discussion.

References:

"tsfeatures". Calculates various features from time series data. Python implementation of the R package tsfeatures. https://github.com/Nixtla/tsfeatures

Hyndman R, Athanasopoulos G, Garza A, Challu C, Mergenthaler M, Olivares K. 2026. "Forecasting: Principles and Practice, the Pythonic Way". https://otexts.com/fpppy/
