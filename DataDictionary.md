#### CurrencyPair_Volume Data Set Information:

##### CurrencyPair_Volume dataset contains 8 attributes related to Hourly price statistics for Major G10 FX Currencies against USD. Histroical Price and Volume data captured for all business dates for April-2018 at hourly interval.

#### Attribute Information
##### CurrencyPair Volume Dataset: CurrencyPair price volume data
- Ticker(CurrencyPair)
- BusinessDate
- TimeBucket
- Open
- High 
- Low
- Close
- Volume




##### Currency Trade Dataset contains 4 attributes: CurrencyPair Trade data
- Ticker(CurrencyPair)
- BusinessDate
- TimeBucket
- TradeTime 
- TradePrice 

######Ticker field contains CurrencyPair for the price volume data.Dataset contains  FX Price Volume data for G10 currency against USD  captured at Minute interval for selected business dates in April-2018
###### BusinessDate field contains Date of the price data in YYYYMMDD format
###### TimeBucket represents Hourly time bucket of the interval in (HH:MM) format
###### TradeTime represents trade execution time
###### TradePrice represents Execution Price of the trade

#####VWAP ML Model Defination: VWAP ML Model contains 15 attributes
##### The Goal  is the "Trend" field refering to the direction of the market direction whether it is a Bull(Rising) market or Bear(Falling) market, whether it is trending up (higher then the VWAP) or down (Lower then  VWAP).
Dataset contains data for 5 currency pairs (EURUSD, AUDUSD, NZDUSD, USDJPY, USDCHF), 
Model will be trained with 70, 30 split using real time data. Model will also be validated by eliminating ticker(currency pair identifier) as golden holdout

- Ticker(CurrencyPair)
- BusinessDate
- TimeBucket
- Open
- High 
- Low
- Close
- Volume
- Avg_Price
- PV(PriceVolume)
- Consolidated_PV ( Sum of PV by Ticker, BusinessDate)
- VWAP (VolumeWeightedAvgPrice) = Consolidated_PV/Volume
- TradeTime
- TradePrice
- Trend


######Ticker field contains CurrencyPair for the price volume data.Dataset contains  FX Price Volume data for G10 currency against USD  captured at hourly interval for all business dates in April-2018
###### BusinessDate field contains Date of the price data in YYYYMMDD format
###### TimeBucket represents time bucket of the interval in (HH:MM) format
###### Open contains opening data at the begining of the interval
###### High contains Highest price data for the interval
###### Low contains Lowest price data for the interval
###### Close contains Closing Price data for the interval
###### Volume contains FX Volume traded during the interval for the currencypair
###### avg_price is a computed column , contains avg of open, close, high and low price data
###### PV is a computed colume , contains avg_price*volume data
###### VWAP is a volume weighted avg price for the Business Date, computed as sum(PV)/sum(volume) by ticker, business date
