#### Data Set Information:

##### This database contains 8 attributes related to Hourly price statistics for Major G10 FX Currencies against USD. Histroical Price and Volume data captured for all business dates for April-2018 at hourly interval.

#### Attribute Information
##### Currency Volume Dataset: CurrencyPair price volume data
- Ticker(CurrencyPair)
- BusinessDate
- Hour
- Open
- High 
- Low
- Close
- Vol


######Ticker field contains CurrencyPair for the price volume data.Dataset contains  FX Price Volume data for G10 currency against USD  captured at hourly interval for all business dates in April-2018
###### BusinessDate field contains Date of the price data in YYYYMMDD format
###### Hour represents time of the interval in (HH:MM) format
###### Open contains opening data at the begining of the interval
###### High contains Highest price data for the interval
###### Low contains Lowest price data for the interval
###### Close contains Closing Price data for the interval
###### Volume contains FX Volume traded during the interval for the currencypair
###### avg_price is a computed column , contains avg of open, close, high and low price data
###### PV is a computed colume , contains avg_price*volume data
###### VWAP is a volume weighted avg price for the Business Date, computed as sum(PV)/sum(volume) by ticker, business date

##### Currency Trade Dataset: CurrencyPair Trade data
- Ticker(CurrencyPair)
- BusinessDate
- Hour
- Price
- High 
- Low
- Close
- Vol
- Trend

##### The "Trend" field refers to,  the direction of the currency price, whether it is trending up (higher then the VWAP) or down (Lower then  VWAP). trend direction, along with other indicators such as moving 200 days avg are used in algorithmic trading strategy.
