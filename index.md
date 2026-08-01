---
layout: default
title: Portfolio
---

[Home/Research Blog](/) | [ART](/art) | [AboutMe](/resume)

----

["AI in Education: Machine Learning-based Revised Bloom Taxonomy Classifiers](/Entry_BloomTaxonomy)

*Updated: 26 July 2026*

The surge in AI-generated educational materials has outpaced our capacity to validate their pedagogical quality. How do we ensure that AI-generated questions are aligned with Pedagogical Frameworks? In this blog, I demonstrate building ML models to assess the cognitive levels of text using the revised Bloom Taxonomy framework and public dataset.

<img src="images/Blog_Bloom_app.png?raw=true"/>

---

["Anylogic: Consumer Market Simulation"](/Entry_Anylogic)

*Updated: 7 May 2026*

In this blog, I demonstrate an example Agent-Based consumer market model using Anylogic Software. Simulation provides a risk-free environment to find new solutions and understand dynamic systems. My goal is to share some insights to these questions based on the simulation model I built using AnyLogic software.

<img src="images/Anylogic_Sim2.gif?raw=true"/>

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

#### Nowcasting Philippine Household Consumption: An Alternative
Approach using Google Trends and XGBoost Model

**Abstract.** This study aims to develop a model for nowcasting household consumption in the Philippines using alternative data and machine learning model. In particular, we utilize Google search queries and Extreme Gradient Boosting (XGBoost) to nowcast household consumption. Our results indicate that XGBoost model outperforms benchmark autoregressive models. Shapley Additive explanations suggest that the top features of the XGBoost model are lags of household consumption and Google searches related to travel. Overall, we demonstrate the potential use of Google Trends in capturing the likely trends in household spending in the near term.

<img src="images/Paper_XGBoost.gif?raw=true"/>

---

#### A Machine Learning Approach to Constructing A Weekly GDP Tracker using Google Trends

**Abstract.** High frequency and granular data are integral in crafting prompt and appropriate measures toward mitigating impact of economic headwinds. We construct a near real-time Gross Domestic Product (GDP) growth tracker that capitalizes on available high frequency alternative data and state-of-the-art machine learning models. The tracker serves as a complementary surveillance tool for monitoring economic activity.<a href = "https://www.bsp.gov.ph/Media_And_Research/Publications/EN23-02.pdf"> Link to paper </a>

<img src="images/Paper_Tracker.gif?raw=true"/>


---

#### Efficient multi-site two-photon functional imaging of neuronal circuits

**Abstract.** Two-photon imaging using high-speed multi-channel detectors is a promising approach for optical recording of cellular membrane dynamics at multiple sites. A main bottleneck of this technique is the limited number of photons captured within a short exposure time (~1ms). Here, we implement temporal gating to improve the two-photon fluorescence yield from holographically projected multiple foci whilst maintaining a biologically safe incident average power. We observed up to 6x improvement in the signal-to-noise ratio (SNR) in Fluorescein and cultured hippocampal neurons showing evoked calcium transients. With improved SNR, we could pave the way to achieving multi-site optical recording of fluorogenic probes with response times in the order of ~1ms. <a href = "https://opg.optica.org/directpdfaccess/9c09904e-8606-494b-b94feaf3d11cd06c_355616/boe-7-12-5325.pdf?da=1&id=355616&seq=0&mobile=no"> Link to paper </a>

<img src="images/Paper_BMX_Gating.gif?raw=true"/>

---

<p style="font-size:11px">Page template forked from <a href="https://github.com/evanca/quick-portfolio">evanca</a></p>
