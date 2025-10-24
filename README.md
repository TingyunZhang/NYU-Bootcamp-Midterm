# NYU-Bootcamp-Midterm

## Executive Summary: Sentiment, Risk, and Investor Behavior—An Exploratory Study on Tesla (TSLA)
### 1. Introduction
The modern financial market is increasingly shaped by the flow of online information. From Reddit threads, investor sentiment now moves markets faster than ever before. This project investigates how social-media-driven sentiment relates to Tesla’s stock performance and downside risk. Specifically, the goal is to explore whether changes in public mood can explain or even predict variations in Tesla’s volatility, crash likelihood, and risk-adjusted investor welfare.

Tesla, Inc. (ticker: TSLA) offers a compelling case for such analysis. As one of the most publicly discussed and traded companies, Tesla’s stock has historically been influenced not only by earnings and fundamentals but also by the behavior of its online fanbase. Between July 2021 and July 2022, a period marked by major corporate announcements, product updates, and broad market volatility, Tesla’s price movement reflected the complex interplay between optimism, speculation, and fear.

### 2. Research Motivation

The project’s central question is:
Does investor sentiment, as expressed on Reddit, influence Tesla’s market risk and crash probability?

To answer this, several related objectives were pursued:
Explore sentiment dynamics: Quantify and visualize how investor mood fluctuates over time and whether it aligns with changes in Tesla’s stock returns.

1. Characterize downside risk: Use downside semivariance and crash indicators to measure periods of heightened negative volatility.

2. Test sentiment–risk relationships: Evaluate statistically whether lower sentiment predicts higher downside risk and higher probability of extreme losses.

3. Model “disaster intensity”: Apply a Poisson–Normal Mixture (PNM) model to decompose Tesla’s returns into normal daily fluctuations and rare, jump-like “disaster” events.

4. Assess investor welfare: Estimate how changes in sentiment alter the risk-adjusted welfare of a representative investor, using a constant-relative-risk-aversion (CRRA) framework.

By combining exploratory visualization and quantitative modeling, the study bridges behavioral finance and modern risk theory.

## 3. Data Source
### 3.1 Market Data (Yahoo Finance)

Using the yfinance API, the script retrieved Tesla’s daily adjusted closing prices, trading volume, and returns from January 2021 to December 2022. Returns were computed as daily percentage changes in adjusted close prices.

These variables provide the market backbone for merging with sentiment information and constructing financial risk measures such as downside semivariance and crash indicators.

3.2 Reddit Sentiment Data (Kaggle Dataset)

The Reddit dataset includes every post and comment mentioning “TSLA” between July 5, 2021, and July 4, 2022. Each record includes: create_utc: the timestamp of the post or comment, sentiment: a sentiment score (positive = optimism, negative = pessimism), score: the Reddit upvote score (a measure of engagement).

The analysis first converted timestamps into readable datetime format and extracted daily averages.
This produced a daily sentiment index representing collective investor mood toward Tesla.

3.3 Merging and Derived Variables

The sentiment and market datasets were merged on the common date variable, resulting in a combined panel of TSLA’s stock price, daily average sentiment, stock returns, and volume. Several derived features were created:

1. Downside Semivariance (7-day rolling): Captures average negative deviation from the mean, measuring only downside risk.

2. Crash Indicator: Binary variable equal to 1 if the daily return < –5%, 0 otherwise.

3. Lagged Sentiment (1-day, 3-day): Measures the delayed effect of sentiment on market risk.

This preprocessing stage ensured that both behavioral (sentiment) and financial (risk) dimensions were aligned on a comparable temporal scale.

### 4. Exploratory Data Analysis

4.1 Sentiment vs. Volume

A scatter plot of average daily sentiment against trading volume revealed a negative correlation, showing that as sentiment became more positive, Tesla’s trading volume tended to decrease.
