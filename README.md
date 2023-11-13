# Delay-Embeddings-and-ML-Asset-Forecasting

# Overview #
An exploration into delay embeddings on time series data for the purpose of short term forecasting stock data. Final goal was to use delay embedding for stock at $x_t$ and predict price at $x_{t+60}$ using various regression ML algos. 

## Backround Research and Reasoning ##
Delay embeddings are a technique from the field of nonlinear dynamics that involves creating a higher-dimensional representation of a time series by embedding it in a space of delayed copies of itself. Each dimension of the embedding space represents a different time delay, and by choosing appropriate delays, it is possible to capture the underlying dynamics of the system. They can also help to reduce the impact of noise in the data. Due to financial data's high noise and non-linear patterns time delay embeddings seemed like a promising option for forecasting. 

## Data and Preprocessing ##
Minute by minute price data for apple stock was used as the foundational time series for this project. Data was aquired through AlphaAdvantage API (they were very kind in giving me academic access for this purpose). Only trading hours data were used (9:30am-4pm). Orginal time series plot showed obvious random walk pattern so first order differencing was applied. ![Graph](https://user-images.githubusercontent.com/106636917/232355508-6dd6aea3-64fa-4b82-9390-d84780013ba5.JPG)
Data was proven to be stationary by AdFuller test after the differencing. From here ACF was used to try and determine optimal tau value for embedding transformation.

![ACF](https://user-images.githubusercontent.com/106636917/232355827-a671b543-4ed2-45c6-8ba9-aa641446573e.JPG)


After testing entire dataset with ACF no significant lags were discovered so smaller windows of recent data were explored in the hopes of shorter term paterns emerging but similar results were found, lags were set to 600. Data is clearly white noise, but whats the fun in giving up now

## Delayed Embedding Creation ##
The GTDA package was used to create delayed embeddings. tau was set to 14 (highest significance value from acf) and dimensions were set to be 195 (giving the embeddings roughly a 7 day time range of information). These embeddings produced the following 3 dimensional point cloud.

![point_cloud](https://user-images.githubusercontent.com/106636917/232356769-cdfd1c00-59ac-4957-af59-89bcc504225c.JPG)

The structure shows no obvious signs of patterns, but topological analysis may yield some results (beyond my current knowledge of mathmatics) 

## Modeling and Results ##
The target used for forecasting was the asset price 60min from embedding point. Training data was 100k sequential samples, test data was the last 40 sequential minutes. 3 Common ML methods were tested for their application with the embeddings. The results are the following

Model Type    | R^2 on Test Data
------------- | -------------
Linear Regression  | -0.0982
XGBoost  | -0.1996
Random Forrest | -.0243

The results overall are lackluster but considering the high noise level in all financial data it seems like a promising start. Resdiuals were examined for all 3 models for serial correlation or dependence but all proved to be white noise. A small subet of linear regression resdiuals are below. 

![residuals](https://user-images.githubusercontent.com/106636917/232360776-984ad405-504f-4c76-9168-e67fc9198ca1.JPG)

## Further Research ##
Overall I was extremely limited compuationaly for this project. A more in-depth grid search and backtesting for model paramters optimization would almost certaintly yield better results. The non-constant variance in test data should also be explored 


