---
layout: default
title: Blog
---

[Home](/) | [Research Blog](/blog) | [ART](/art)

---

["Linear Model: Autoregressive Integrated Moving Average (ARIMA)"](/Entry_ARIMA)

*Updated: 19 March 2026*

Model building is one of the most exciting and critical aspects of time-series forecasting. The key question we grapple with is: "What model best captures the underlying patterns in our time series?" To develop this intuition, we need to get our hands dirty and explore different modeling approaches.

In this blog, I discuss ARIMA — a linear model widely used in time-series forecasting in economics, finance, among others. We will explore the application of ARIMA to different time-series and how it performs against naive models. My goal is to provide a concise overview of the theoretical foundations while demonstrating practical applications using python packages such as Statsforescast and the NIXTLA.

<img src="images/Blog_ARIMA_4.png?raw=true"/>

---

["Forecaster's Toolbox: Residuals and Error metrics"](/Entry_Toolbox)

*Updated: 1 March 2026*

In the age of Do-It-Yourself (DIY) projects, it is essential to have a toolbox. We all have go-to tools that make our work easier. For me, that would be a drill or ratchet screw-driver.

For time-series forecasters, the common tools would be benchmark models, residuals, and error metrics. In this blog, I will discuss and share these tools. My goal is to introduce and review these foundational tools useful for us forecasters.

<img src="images/Blog_Toolbox_5.png?raw=true"/>

---

["Decomposition: Breaking the signal into components"](/Entry_STL)

*Updated: 16 February 2026*

Time series data can exhibit complex and rich patterns. It is often helpful to split a time series into several components - trend, seasonality, and cycles - known as "decomposition".

Here, I will describe some of the most common methods for time-series decomposition. I will introduce python libraries (e.g., Moving averages, STL, Prophet) that I use for decomposition. My goal by the end of this blog is for us to look at complex signal thru the lense of decomposition.

<img src="images/Blog_STL_3_STL.png?raw=true"/>

---

["Useful metrics to kickstart your analysis on time-series"](/Entry_TSFEATURES)

*Updated: 6 February 2026*

Time series data tells compelling stories about the past and hints at the future. Will housing prices in Australia continue rising? When does Australia see peak tourist arrivals? Understanding these patterns is vital for policy-making and business strategy.

While time series analysis can seem daunting, specialized tools like Python's `tsfeatures` package make it accessible. In this post, I'll share practical metrics for characterizing time series—tools I've used in my work and MSDS studies as pre-cursor analysis towards building time-series models.

<img src="images/Blog_TSFEATURES_5.png?raw=true"/>


---

["Challenges on the use of Google Trends for research"](/Entry_GT)

*Updated: 1 February 2026*

Internet search volumes (Google Trends) have become popular proxies for estimating current period (also referred to as "nowcasting") macroeconomic indicators. In my work on machine learning models, I've seen firsthand how these high-frequency indicators (GT variables) can circumvent the publication lags of official statistics.

However, there is a trade-off. GT variables suffer from temporal 
instability, backend scaling issues, and time-varying relevance—challenges 
that can quietly undermine model performance if left unaddressed. In this blog, I highlight some potential pros and cons on the use of Internet searches (Google Trends) for research, drawing from my work on machine learning nowcasting models.

<img src="images/Blog_GT3.png?raw=true"/>


----
