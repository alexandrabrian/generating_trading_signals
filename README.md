# Predicting Trading Signals using KPCA and SVR

Alexandra Brian

see iPython notebooks for raw code for each pipeline.

## Introduction

### Problem Statement: 
All investors seek to predict stock positions (buy, hold and sell) that generate a profitable return. There are many different methods employed to accomplish this goal, such as fundamental, sentiment  and technical analysis. Financial forecasting has many challenges because financial time series data are noisy, non-stationary and volatile. Due to the many features and noisy features associated with historical pricing data many investors have turned to machine learning, statistical and computational perspectives.   

### Solution Statement: 
This study aims to reduce the inherently noisy nature of the features associated with the time-series data by employing machine learning algorithms. Because the data is nonlinear we will use Kernel Principal Component Analysis (KPCA) to reduce the number of features. This study will also employ Support Vector Regression (SVR) because it has shown to be more robust against noise and uses a kernel trick to deal with non-linearity of the data. The goal of this project is to accuratly predict the trading signal with a model using machine learning algorithms. Here, we will be attemping to First, naive Principal Component Analysis (PCA) and Linear Regression will be used for our benchmark. Next, KPCA and SVR will be used as our model.

### Domain and Data:
This project uses historical pricing data from the S&P500 with the following terms:

- `Close` : A securities closing price on a specified day of trading.
- `Open`: The price of a stock on a given day.
- `High`: The highest price at which a stock traded during the course of a day. 
- `Low`: The lowest price a stock traded during the course of a day. 

#### Feature engineering:
We use the historical pricing data to generate 47 features, technical indicators (TI), that include the following with different hyperparameters:

- Moving Average
- Exponential Moving Average
- Momentum
- Rate of Change
- Average True Range
- Bollinger Bands
- Pivot Points, Supports and Resistances
- Stochastic oscillator %K
- Stochastic oscillator %D
- Trix
- Average Directional Movement Index
- MACD, MACD Signal and MACD difference
- Mass Index
- KST Oscillator
- Relative Strength Index
- True Strength Index
- Accumulation/Distribution
- Chaikin Oscillator
- Money Flow Index and Ratio
- On-balance Volume
- Force Index
- Coppock Curve
- Standard Deviation

     
### Creating Targets:
In order to create the targets for the model we will use Piecewise linear representation (PLR) to generate trading signals. 


![](doc/img/trading_signal_2.png)


### Metric
We will use two metrics, mean squared error to score and compare our models. We will use mean squared error to measure the difference between the estimator (y_test) and what is estimated (y_pred).

## Methods

### Building the Benchmark: 

1. Train, Test, Split
2. Create a Pipeline:
	- Standardize data 
	- Naive PCA
	- Linear Regression

#### Benchmark Results on APPL:  

Mean squared error: 0.07


#### Benchmark Results For APPL using CVS, WFC TI's:  

Mean squared error: 0.33


### GridSearch tuned KPCA and SVR
1. Train, Test, Split
2. Create Pipeline:
	-  Standardize data
	- KPCA
	- SVR
3. GridSearch:
	- Tuned Hyperparameters:
		- KPCA:
			- Kernels: (rbf, sigmoid, cosine) 
			- n_components: (2-11)
			- Gamma: (10 evenly spaced numbers .1-1) 
		- SVR:
			- Kernels: (rbf, sigmoid)
			- C: (0.001, 0.01, 0.1, 1.0, 10.0)

### Results on APPL

Mean squared error: 0.19

### Results on APPL using CVS, WFC TI's

Mean squared error: 0.11


### Conclusion

The benchmark using naive PCA and Linear Regression has outperformed the Gridsearch with KPCA and SVR, which suggests we should look further into improving our model. 

#### Possible future steps:
1. Create a function that calculates our epsilon for calculating our trading signals with PLR.
1. Use different models instead of SVR
1. Add more stocks to our analysis
1. Possibly use clustering of companies to create new feature used to predict movement 
1. Categorize trading signals into 3 categories:
	 - Buy (1) 
	- Hold (0)
	- Sell  (-1) 
1. Go through technicals to check accuracy or improve hyperparameters
