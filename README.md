# Research-methods_PaperReading

## Dataset Description
- ### Import Data
    - Using yfinance to get "AAPL" stock's information .
- ### Data processing
    - Dataset contains "Close", "Volume" & "Date".
    - Period of data: 1 year.
## Approach
-   Calculating a corresponding maximum price movement
    -   $\Delta P_n = max \lbrace S_n - S_k, S_n - S_{k+1}, ..., S_n - S_{n-1} \rbrace$ 
-   For a fixed level α we select all the observations in the set
    -   $Q_{a}^{+}\left ( x \right ) = \lbrace \{ x:prob\left ( \Delta_{P}< x\right )< \alpha \ or\ prob\left ( \Delta_{P}>  x\right )> 1 - \alpha  \rbrace \}$
