---
layout: default
title: Blog
---

[Home](/) | [Blog](/blog) | [Projects](/projects)

---

["Decomposition: Breaking the signal into components"](/Entry_STL)
*Updated: 16 February 2026*

Time series data can exhibit complex and rich patterns. It is often helpful to split a time series into several components - **trend**, **seasonality**, and **cycles** - known as "decomposition".

Here, I will describe some of the most common methods for time-series decomposition. I will introduce python libraries (e.g., Moving averages, STL, Prophet) that I use for decomposition. My goal by the end of this blog is for us to look at complex signal thru the lense of decomposition.

---

["Useful metrics to kickstart your analysis on time-series"](/Entry_TSFEATURES)

*Updated: 6 February 2026*

Time series data tells compelling stories about the past and hints at the future. Will housing prices in Australia continue rising? When does Australia see peak tourist arrivals? Understanding these patterns is vital for policy-making and business strategy.

While time series analysis can seem daunting, specialized tools like Python's `tsfeatures` package make it accessible. In this post, I'll share practical metrics for characterizing time series—tools I've used in my work and MSDS studies to as pre-cursor analysis towards building time-series models.

---

["Challenges on the use of Google Trends for research"](/Entry_GT)

*Updated: 1 February 2026*

Internet search volumes (Google Trends) have become popular proxies for estimating current period (also referred to as "nowcasting") macroeconomic indicators. In my work on machine learning models, I've seen firsthand how these high-frequency indicators (GT variables) can circumvent the publication lags of official statistics.

However, there is a trade-off. GT variables suffer from temporal 
instability, backend scaling issues, and time-varying relevance—challenges 
that can quietly undermine model performance if left unaddressed. In this blog, I highlight some potential pros and cons on the use of Internet searches (Google Trends) for research, drawing from my work on machine learning nowcasting models.


----