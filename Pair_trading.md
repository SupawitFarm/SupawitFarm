## Introduction
Pair trading strategy is a market-neutral approach used in quantitative trading, where two highly correlated securities are bought and sold simultaneously. This strategy capitalizes on temporary dislocations in the relationship between the pair, banking on a reversion to their historical mean. It requires significant data analysis and risk management, with the flexibility to be applied across different markets and asset types. Overall, it's a sophisticated strategy aimed at exploiting market inefficiencies through rigorous quantitative analysis

## Data Preparation
Firstly, I import necessary libraries, define a list of stock symbols in the SET50 index, and use Yahoo Finance to download historical data for these stocks from 2020 to 2022. The data is then manipulated into a pivot table where each column represents a different stock and each row represents a different date, thereby preparing the data for implementing a pair trading strategy.
```python
#import libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import statsmodels.tsa.stattools as ts
import statsmodels.tsa.vector_ar.vecm as vm
from statsmodels.regression.linear_model import OLS
from yahooquery import Ticker

#list of stock in SET50 index
stock_list = ['ADVANC.bk', 'AOT.bk', 'AWC.bk', 'BANPU.bk', 'BBL.bk', 'BDMS.bk', 'BEM.bk', 'BGRIM.bk', 
              'BH.bk', 'BTS.bk', 'CBG.bk', 'CENTEL.bk', 'COM7.bk', 'CPALL.bk', 'CPF.bk', 'CPN.bk', 
              'CRC.bk', 'DELTA.bk', 'EA.bk', 'EGCO.bk', 'GLOBAL.bk', 'GPSC.bk', 'GULF.bk', 'HMPRO.bk', 
              'INTUCH.bk', 'IVL.bk', 'JMART.bk', 'JMT.bk', 'KBANK.bk', 'KTB.bk', 'KTC.bk', 'LH.bk', 
              'MINT.bk', 'MTC.bk', 'OR.bk', 'OSP.bk', 'PTT.bk', 'PTTEP.bk', 'PTTGC.bk', 'RATCH.bk', 
              'SAWAD.bk', 'SCC.bk', 'SCGP.bk', 'TIDLOR.bk', 'TISCO.bk', 'TOP.bk', 'TRUE.bk', 'TTB.bk', 'TU.bk']
