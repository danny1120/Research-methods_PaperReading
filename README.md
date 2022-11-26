# Thesis_Introduction_PaperReading

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
