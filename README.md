# CS5260Assignment
# Forex VWAP(Volume Weighted Average Price)  Machine Learning Solution
## This notebook demonstrates Machine Learning solution to predict VWAP Volume pattern for given currency pair based on historic currenypair volume data
# Problem Formulation
## The primary input to the VWAP algorithm is the volume profile. In fact, other algorithms, like arrival price algorithms and open/close algorithms, often utilize them as well. Volume profiles give an algorithm information on historical volume patterns. Algorithms generally use this information by trading more when volumes are typically high (e.g., near the close) and less when they are typically light (e.g., mid-day)
# Data Set
## In this example, we will use Historical Currency price dataset provided from FOREX Tester APP, available here: https:https://forextester.com/data/datasources.

The dataset contains Hourly pricing data on EURUSD Currency Pair daily for 201804. Initial development and proof of concept is done using EURUSD curreny data but plan to extend across all major G10 Currency pairs.

