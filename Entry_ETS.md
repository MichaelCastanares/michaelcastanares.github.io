---
layout: default
title: Blog
---

[Home](/) | [Research Blog](/blog)

---
### "Linear Model: Exponential Smoothing"
*In Progress*
In our previous blog ARIMA, Naive models were robust and to some extent, hard to beat.





**Data**. We will analyze three time series, namely:
1. AUD/PH Exchange rate daily series from [Reserve Bank of Australia](https://www.rba.gov.au/statistics/historical-data.html#exchange-rates);
2. AU inflation rate from [Reserve Bank of Australia](https://www.rba.gov.au/statistics/tables/xls/g01hist.xlsx?v=2026-03-08-20-14-13); and
3. Crude oil prices downloaded from [Federal Reserve Bank of St. Louis](https://fred.stlouisfed.org/series/DCOILWTICO).

These macroeconomic indicators are important metrics that capture economic conditions. In particular, crude oil prices has been surging (as of this writing) due to the War/Conflict in the middle east. Forecasting trends of crude oil prices amid this war crisis will support policymakers, economic managers, business, and consumers in making sound and effective decisions.


### A. Theoretical Foundations

Attribution: Please note that most of the theoretical discussions as follows were lifted from Hyndman, R. J., & Athanasopoulos, G. (n.d.). I have modified some notations to be consistent with my previous blog posts.

**A.1 Simple Exponential Smoothing (SES)**. The forecasts are calculated as a weighted average, where the weights decrease *exponentially* from past observations. In other words, recent observations have higher influences to the forecast (similar to Naive model) while distant past observations have lesser influence to the forecast.

$$
\hat{Y}_{t+1|t}  = \alpha Y_t + \alpha(1-\alpha) Y_{t-1} + \alpha(1-\alpha)^2 Y_{t-2} + \ldots,
$$

where $0 \le \alpha \le 1$ is the smoothing parameter. Note that $Y_1, Y_2, \ldots, Y_{t-1}, Y_{t}$ are the observed values.

The SES can also be expressed in terms of its components. Considering a series which has no clear trend and seasonality, we can model the level using SES. The component forms is

$$
\begin{aligned}
\text{Forecast eqn}: \hat{Y}_{t+h|t} &= l_t\\
\text{level eqn}: l_t &= \alpha Y_t + (1-\alpha)l_{t-1}, 
\end{aligned}
$$
where $l_t$ is the level (or the smoothed value) of the series at time $t$.

**A.2 Holt's linear trend method (HLT)**. This model is an extension of SES to forecast a series with trend. The Component representation of Holt's linear trend method is given as

$$
\begin{aligned}
\text{Forecast eqn}: \hat{Y}_{t+h|t} &= l_t + hb_t\\
\text{level eqn}: l_t &= \alpha Y_t + (1-\alpha)(l_{t-1} + b_{t-1})\\
\text{trend eqn}: b_t &= \beta^*(l_t-l_{t-1}) + (1-\beta^*)b_{t-1},
\end{aligned}
$$
where $l_t$ is the estimated level of the series at time $t$, $h$ is the time-step horizon, $b_t$ is the estimated trend (slope) of the series, $0 \le \alpha \le 1$ is the smoothing parameter, and $0 \le \beta^* \le 1$ is the smoothing parameter for the trend.

**A.3 Damped trend methods**. This is a modification of the HLT method which introduced a parameter that dampens the trend at longer forecast horizon. HLT method assumes a constant (increasing/decreasing) trend indefinitely leading to over-forecast. With the damped trend method, the trend coverges to a flat line at longer horizon.

$$
\begin{aligned}
\text{Forecast eqn}: \hat{Y}_{t+h|t} &= l_t + (\phi + \phi^2 + \ldots + \phi^h)b_t\\
\text{level eqn}: l_t &= \alpha Y_t + (1-\alpha)(l_{t-1} + \phi b_{t-1})\\
\text{trend eqn}: b_t &= \beta^*(l_t-l_{t-1}) + (1-\beta^*)\phi b_{t-1},
\end{aligned}
$$
where $\phi$ is the damping parameter.

For $\phi=1$, the damped trend is the same as the HLT method. 

$$
\text{Forecast eqn}: \hat{Y}_{t+h|t} = l_t + (1 + 1^2 + \ldots + 1^h)b_t\\ = l_t + hb_t
$$

For $0 \le \phi < 1$, we find that the forecast converges to
a constant for $h \to \infty$.
$$
    \hat{Y}_{t+h|t} \to l_t + \phi b_t/(1-\phi)
$$

**A.4 Method with Seasonality: HLT additive method**.
Holt and Winters extended the Holt's method to model seasonality. The HLT additive model assumes that the seasonl variation is roughly constant throughout the series. The seasonal component is expressed in absolute terms in the scale of the observed series. The component form of HLT additive method is

$$
\begin{aligned}
\text{Forecast eqn}: \hat{Y}_{t+h|t} &= l_t + hb_t + s_{t+h-m(k+1)}\\
\text{level eqn}: l_t &= \alpha(y_t - s_{t-m}) + (1-\alpha)(l_{t-1}+b_{t-1})\\
\text{trend eqn}: b_t &= \beta^*(l_t-l_{t-1}) + (1-\beta^*)\phi b_{t-1} \\
\text{seasonal eqn}: s_t &= \gamma (y_t - l_{t-1} - b_{t-1}) + (1-\gamma)s_{t-m}
\end{aligned}
$$
where $k$ is the integer part of $(h-1)/m. The level $l_t$ is the weighted average of the seasonally-adjusted observation $(y_t - s_{t-m})$ and the non-seasonal previous estimate $(l_{t-1} + b_{t-1})$. 

**A.5 Method with Seasonality: HLT multiplicative method**. Similarly, for multiplicative seasonality, the HLT component form is expressed as
$$
\begin{aligned}
\text{Forecast eqn}: \hat{Y}_{t+h|t} &= (l_t + hb_t)s_{t+h-m(k+1)}\\
\text{level eqn}: l_t &= \alpha\frac{y-t}{s_{t-m}} + (1-\alpha)(l_{t-1}+b+{t-1})\\
\text{trend eqn}: b_t &= \beta^*(l_t-l_{t-1}) + (1-\beta^*)b_{t-1} \\
\text{seasonal eqn}: s_t &= \gamma \frac{y_t}{(l_{t-1} + b_{t-1})} + (1-\gamma)s_{t-m}
\end{aligned}
$$


### B. Applications


### Final thoughts

This analysis demonstrates that while ARIMA models provide a theoretically grounded framework for time-series forecasting, simpler approaches like the Naive model often provide competitive or superior performance. The key insight is not that ARIMA should be dismissed, but rather gain intuition on how it works and why it did not work. I think the best way to learn is to be exposed with different models.

Codes used to generate the figures may be found here: [View Code Repository on GitHub](https://github.com/MichaelCastanares/Github/tree/main/TS_ARIMA)


Disclaimer of AI use: Claude Sonnet was used to improve the flow of the discussion.


### Reference:

Hyndman, R. J., & Athanasopoulos, G. (n.d.). Exponential smoothing. In Forecasting: Principles and practice (3rd ed.). Retrieved from https://otexts.com/fpppy/nbs/08-exponential-smoothing.html


