# Rare Events Analysis for High-Frequency Equity Data

## Abstract
In this work present a methodology to detect rare events which are defined as large price movements relative to the volume traded, and provide methods to calibrate trading rules based on the detection of these events and illustrate for a particular trading rule.
The methodology that we have developed is based on nonparametric statistics and makes no assumption about the distribution of the random variables in the study.

## Keywords 
High-frequency trading,  Average daily volume,  Trading strategy

## Dataset Description
- ### Import Data
    - Using yfinance to get "AAPL" stock's information .
- ### Data processing
    - Dataset contains stock's "Close", "Volume" & "Date".
    - Period of data: 1 year.
## Approach
-   ### Method
    -   #### Using for loop to get difference of close price and the date of maximum and minimum close price , under the conditions that v_sum < V0.
    -   ##### Calculating a corresponding maximum price movement.
        -   $\Delta P_n = max \lbrace S_n - S_k, S_n - S_{k+1}, ..., S_n - S_{n-1} \rbrace$ 
    -   ##### For a fixed level α we select all the observations in the set.
        -   $Q_{a}^{+}\left ( x \right ) = \lbrace \{ x:prob\left ( \Delta_{P}< x\right )< \alpha \ or\ prob\left ( \Delta_{P}>  x\right )>         1 - \alpha  \rbrace \}$
    -   ##### Restrict the distribution conditional.
        -    V0 be constant in time and dependent only on the equity.
        -    V0 = mean of the volume and times lens of data.
    -   ##### The maximum price movement given the cumulative volume between two trades is less than a value V0, which is specific for each equity.
        -   v_sum $=\lbrace V_k + V_{k+1} +... V_n < V_{0} \rbrace$ 
        

## Acknowledgements
D.Bozdog, I.Florescu, K.Khashanah, J.Wang, "Rare Events Analysis of High-Frequency Equity Data", in Wilmott Journal, pp. 74-81, 2011.

## Python method
### Pakage import
```python
!pip install yfinance
from pandas.core.indexes.extension import deprecate_ndim_indexing
import pandas as pd
import numpy as np
import math
import yfinance as yf
```
### Get stock info - using Apple Inc's stock
```python
msft = yf.Ticker("AAPL")

msft.info
```
### Get historical market data
```python
hist = msft.history(period="1y")                                                            #,  start = "2021-11-08" , end = "2022-11-08" 加上這串可以指定時段
hist['Date'] = hist.index                                                                   #將index 移到 Columns
data=hist[["Close", "Volume", "Date"]]                                                      #收盤價格， 交易量
```
### Data processing
```python
ddate = list(hist[["Date"]].iloc[:, 0])                                                     #交易日期
close = list(hist[["Close"]].iloc[:, 0])                                                    #收盤價格
volume = list(hist[["Volume"]].iloc[:, 0])                                                  #成交量
n = (len(close))                                                                            #收盤價格總數
```
### Finding Max(delta(p))

#### Steps
- First. Giving two empty list for delta(p) and date of Max(delta(p)).
- Second. Using for loop range started from last record(251) to first record(1).
- Third. Using another for loop range started from Penultimate record(250) to first record(1).
- Fourth. Initialization v_sum in every loop.
- Fifth. Setting conditional v_sum < V0. 
- Sixth. Input close price subtraction to empty list that we built before.
- Seventh. Input max(close) and min(close) date to empty list that we built before.
    - The reason that I use max(close) and min(close) to represent date, because Max(delta(p)) is subtraction of max(close) and min(close).

```python
V0 = np.mean(volume)*(len(data)/4) 

s_diff = []
s_date = []
for h in range(n-1, 0, -1):                                                                  #251-0 一定要用-1因為默認0開始
  for i in range(n-2, 0, -1):                                                                #250-0
    v_sum = 0                                                                                #初始化 v_sum
    if (v_sum < V0):                                                                         #若v_sum小於V0
      v_sum = v_sum + data.iloc[i, 1]                                                        #累加 v_sum
      s_diff.append(close[h]-close[i])                                                       #價差相減 append回傳至集合 後面日期-前面日期
      s_date.append([(ddate[(close.index(max(close)))]), (ddate[(close.index(min(close)))])])# max(close), min(close)位置帶出date
    else:
      v_sum = 0                                                                              #若v_sum大於V0 初始化v_sum
      break                                                                                  #跳出迴圈

print(max(s_diff))                                                                           #print max(delta(p))
print(s_date[0])                                                                             #print max(delta(p))之date)
```

#### Result:
Max(delta(p)) = 51.295257568359375

### Verify

```python

print((max(close))-(min(close)))

```
#### Result:
Max(delta(p)) = 51.295257568359375














