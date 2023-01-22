# CS5260Assignment
# Forex VWAP(Volume Weighted Average Price)  Machine Learning Solution
### This repository contains the source code for:
- Machine Learning solution to predict VWAP Volume pattern for given currency pair based on historic currenypair volume data
## Problem Formulation
#### In this example, we will implement prediction of Pricing trend (Upward, Downward) using VWAP Pricing Algorithm. The primary input to the VWAP algorithm is the volume profile. Volume profiles give an algorithm information on historical volume patterns. Algorithms generally use this information by trading more when volumes are typically high (e.g., near the close) and less when they are typically light (e.g., mid-day)
## Data Set
#### In this example, we will use Historical Currency price dataset provided from FOREX Tester APP, available here: https:https://forextester.com/data/datasources.
#### The dataset contains Hourly pricing data on EURUSD Currency Pair daily for 201804. Initial development and proof of concept is done using EURUSD curreny data but plan to extend across all major G10 Currency pairs.
## Repository Folder Structure
- src Folder: The source code folder
- test Folder: Unit tests, integration tests… go here.
- .config Folder: It should local configuration related to setup on local machine.
- .build Folder: This folder should contain all scripts related to build process (PowerShell, Docker compose…).
- dep Folder: This is the directory where all your dependencies should be stored.
- doc Folder: The documentation folder
- res Folder: For all static resources in your project. For example, images.
- samples Folder: Providing “Hello World” & Co code that supports the documentation.
- tools Folder: Convenience directory for your use. Should contain scripts to automate tasks in the project, for example, build scripts, rename scripts. Usually contains .sh, .cmd files for example.
## Development Guide
### Dependencies
```
  import seaborn as sns
  import matplotlib.pyplot as plt

  #machine learning
  from sklearn.model_selection import train_test_split, GridSearchCV
  from sklearn.linear_model import LogisticRegression
  from sklearn.ensemble import RandomForestClassifier
  from sklearn.pipeline import Pipeline 
  from sklearn.compose import ColumnTransformer, make_column_selector
  from sklearn.impute import SimpleImputer
  from sklearn.preprocessing import OneHotEncoder, LabelBinarizer, StandardScaler
  from sklearn import config_context
  from sklearn.metrics import classification_report, confusion_matrix, ConfusionMatrixDisplay
```
## Approach
### Data Structure
#### fx_volume data consist of Pricing data at hourly interval
- CurrencyPair Ticker
- BUSINESSDATE AS DTYYYYMMDD
- HOUR as TIME
- OPEN PRICE
- HIGH PRICE
- LOW PRICE
- CLOSING PRICE
- VOLUME

### Model 
- Here we first load the fx_volume data into python into pandas dataframe
```
  <class 'pandas.core.frame.DataFrame'>
  RangeIndex: 507 entries, 0 to 506
  Data columns (total 8 columns):
    #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
    0   <TICKER>      507 non-null    object 
    1   <DTYYYYMMDD>  507 non-null    int64  
    2   <TIME>        507 non-null    object 
    3   <OPEN>        507 non-null    float64
    4   <HIGH>        507 non-null    float64
    5   <LOW>         507 non-null    float64
    6   <CLOSE>       507 non-null    float64
    7   <VOL>         507 non-null    int64  
  dtypes: float64(4), int64(2), object(2)
```
- Next, Add additional column avg_price to the dataset, compute Avg Price as average of High,Low,Open and Close by currencypair, Date and time dimension
- Next, Add additional column PV to the dataset, compute PV as avg_price*Volume
- Next , compute Cumulative Volume(Sum) and number of data points (count) by summing across currency pair, Date
- VWAP value can be determined as PV(avg_price*volume)/cumulative volume
```  
Data columns (total 10 columns):
 #   Column        Non-Null Count  Dtype  
---  ------        --------------  -----  
 0   <TICKER>      507 non-null    object 
 1   <DTYYYYMMDD>  507 non-null    int64  
 2   <TIME>        507 non-null    object 
 3   <OPEN>        507 non-null    float64
 4   <HIGH>        507 non-null    float64
 5   <LOW>         507 non-null    float64
 6   <CLOSE>       507 non-null    float64
 7   <VOL>         507 non-null    int64  
 8   <AVG_PRICE>   507 non-null    float64
 9   <PV>          507 non-null    float64
 10  <VWAP>        507 non-null    float64
```
- VWAP trend can be determined by direction of VWAP value over time, rising VWAP would indicate upward trend, Falling VWAP would indicate downward trend
### Confusion matrix
> The key input to these profiles are past volume data. But the methods used to construct these profiles vary across Implementation to Implementation. 
> Most algorithm  use one of two general approaches to volume profile estimation. The first involves estimating volume profiles on a symbol-level, where only past data for that symbol is used to estimate the volume profile. Given the noise in volume data, profiles are created by typically averaging over a relatively long period (e.g., several months). The benefit of this approach is that it can pick up symbol-specific nuances. The downside, though, is that even over a long period, the number of observations is relatively small. A year’s worth of data, for example, provides only 252 data points per stock. And going over longer periods risks using “stale” data, data that may not represent current volume patterns. And the problem is even more severe for less actively traded stocks, where the volume profiles can be particularly problematic to estimate on a symbol-by-symbol level.

> The second approach uses group-level rather than symbol-level profiles. For example, the profiles of all low-volume Nasdaq stocks could be averaged together to create a common volume profile that is applied to all low-volume Nasdaq stocks. The benefit of this approach is that it reduces variability in volume profiles by averaging over the profiles of similar symbols. This way, variability can be reduced via incorporating more data, but without having to use potentially outdated data, as is the case in the first approach. This grouping methodology is particularly effective when dealing with less actively traded assets, whose profiles can be quite jagged each day. In fact, few (if any) VWAP algorithms rely on the symbol-level approach alone. Algo providers who use symbol-level profiles typically use them only for the most actively traded symbols and rely on grouped profiles for less actively traded ones. The downside of this method, though, is defining what we mean by “similar” stocks. Should we group by market cap? By industry? By liquidity? By all of the above? And how many groups should we have? This involves considerable research, to ensure that stocks within a group are, in fact, similar. And, even then, within any group, there may be stocks that have distinct symbol-level variation that makes the group-level profile inappropriate.

# References
[VWAP Algorithm Machine Learning application]([https://pages.github.com/](https://www.bacidore.com/post/volume-profile-estimation-a-machine-learning-application))
