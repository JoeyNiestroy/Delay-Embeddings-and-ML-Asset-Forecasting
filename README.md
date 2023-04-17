# Delay-Embeddings-and-ML-Asset-Forecasting

# Overview #
An exploration into delay embeddings on time series data for the purpose of short term forecasting stock data

## Data and Preprocessing #
Minute by minute price data for apple stock was used as the foundational time series for this project. Data was aquired through AlphaAdvantage API (they were very kind in giving me academic access for this purpose). Orginal time series plot showed obvious random walk pattern so first order differencing was applied. ![Graph](https://user-images.githubusercontent.com/106636917/232355508-6dd6aea3-64fa-4b82-9390-d84780013ba5.JPG)
Data was proven to be stationary by AdFuller test after the differencing. From here ACF was used to try and determine optimal tau value for embedding transformation.
![ACF]
(https://user-images.githubusercontent.com/106636917/232355827-a671b543-4ed2-45c6-8ba9-aa641446573e.JPG)


After testing entire dataset with ACF no significant lags were discovered so smaller windows of recent data were explored in the hopes of shorter term paterns emerging but similar results were found. Data is clearly white noise, but whats the fun in giving up now
