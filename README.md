# Boomer vs Zoomer
**An indepth analysis of a Cryptocurrency vs Commodity Portfolio** <Br/>
*Will an ETF Commodity Portfolio (Gold & Silver) outperform a Cryptocurrency Portfolio (Bitcoin & Ethereum)? Which portfolio is more volatile? Where do these portfolios lie on an efficient frontier? What is the optimal risky portoflio?*

---

## Required Installations

```bash

import os
import requests
import json
import pandas as pd
from dotenv import load_dotenv
import alpaca_trade_api as alpaca
import hvplot.pandas 
import datetime as dt 
import pandas_datareader as pdr
import numpy as np 
import matplotlib.pyplot as plt

```
---

## Data Sources
[Yahoo Finance](https://finance.yahoo.com/) <Br/>
[Portfolio Optimization Documentation](https://www.machinelearningplus.com/machine-learning/portfolio-optimization-python-example/)

---

## Financial Analysis Flow
**Pull in data from Yahoo Finance** <Br/>
```python
btc_df = pdr.DataReader('BTC-USD','yahoo',start_date, end_date) 
```


**Concatenate dataframes for the 2 respective portfolios** <Br/>
```python
cryptoport = pd.concat([btc_daily_rts,eth_daily_rts,], axis=1) 

cryptoport.sort_index(inplace=True) 
cryptoport.columns = ["Bitcoin Daily Returns", "Etherium Daily Returns"]
cryptoport
```

**Portfolio Solver** <Br/>
*Solver Setup* <Br/>
```python
crypto_p_ret = []
crypto_p_vol = [] 
crypto_p_weights = [] 

num_crypto_assets = len(crypto_assets.columns)
num_crypto_portfolios = 10000 
```

*Assign random weights, calculate standard deviation, calculate portfolio variance,calculate daily standard deviation, and calculate annual standard deviation (voltility)* <Br/>
```python
for portfolio in range(num_crypto_portfolios): 
    crypto_weights = np.random.random(num_crypto_assets) 
    crypto_weights = crypto_weights/np.sum(crypto_weights) 
    crypto_p_weights.append(crypto_weights) 
    crypto_returns = np.dot(crypto_weights, crypto_ind_er)                       
    crypto_p_ret.append(crypto_returns) 
    crypto_var = crypto_cov_matrix.mul(crypto_weights, axis=0).mul(crypto_weights, axis=1).sum().sum() 
    crypto_sd = np.sqrt(crypto_var)
    crypto_ann_sd = crypto_sd*np.sqrt(250) 
```
---

## Data Visualizations and Analysis
![commodity daily returns](https://github.com/BRichterman/Team7-Project-1/blob/main/Images/commodity%20daily%20returns%20vs%20spy.jpg)

![commodity pie](https://github.com/BRichterman/Team7-Project-1/blob/main/Images/commodity%20pie.jpg)

**Commodity Conlusion** <Br/>
Silver follows SPY (our baseline stock) trends more so than Gold. The ultimate commodity portfolio 100% favors Silver based on the last year of returns.

---

![crypto daily returns](https://github.com/BRichterman/Team7-Project-1/blob/main/Images/crypto%20daily%20returns%20vs%20spy.jpg)

![crypto pie](https://github.com/BRichterman/Team7-Project-1/blob/main/Images/crypto%20pie.jpg)

**Crypto Conclusion** <Br/>
Both Bitcoin and Ethereum trend more with eachother rather than trending with our baseline stock, SPY. The Cryptocurrency Portfolio also had higher daily returns than the Commodities Portfolio. The ultimate Crypto Portfolio favors Ethereum based on the last year of returns.
