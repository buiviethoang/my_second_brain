2025-10-26 11:19

TARGET DECK: [[technical analysis]]
START
Basic
Moving Average
Back:
## Main
**Moving Averages** are one of the most fundamental tools in data analysis, finance, and time series forecasting — especially useful for smoothing fluctuations and identifying trends.

### 🧩 **Definition**

A **moving average (MA)** calculates the average value of a dataset over a specified number of periods and continuously updates (“moves”) as new data becomes available.

Mathematically:

MAt=1n∑i=0n−1Pt−iMA_t = \frac{1}{n} \sum_{i=0}^{n-1} P_{t-i}MAt​=n1​i=0∑n−1​Pt−i​

where

- MAtMA_tMAt​ = moving average at time _t_,
    
- nnn = number of periods,
    
- Pt−iP_{t-i}Pt−i​ = value at time _t-i_ (e.g., closing price).


📊 **Types of Moving Averages**

| Type                                 | Formula / Concept                                | Use Case                                                   |
| ------------------------------------ | ------------------------------------------------ | ---------------------------------------------------------- |
| **Simple Moving Average (SMA)**      | Average of the last _n_ data points.             | Smoothing short-term fluctuations.                         |
| **Weighted Moving Average (WMA)**    | Recent data is given more weight.                | Emphasizes recent trends.                                  |
| **Exponential Moving Average (EMA)** | Applies exponential weights, decaying with time. | Common in trading — reacts faster to recent price changes. |
| **Cumulative Moving Average (CMA)**  | Average of all data up to the current point.     | Tracks long-term trend with minimal noise.                 |
### ⚙️ **Applications**

- 📈 **Finance:** Trend following, support/resistance levels, crossover strategies (e.g., 50-day vs 200-day MA).
    
- 🔬 **Signal Processing:** Noise reduction in data streams.
    
- 📉 **Forecasting:** Predicting short-term trends in demand or prices.
    
- 💻 **Data Science:** Feature smoothing in time-series models.


## References
https://www.vietcap.com.vn/kien-thuc/duong-trung-binh-dong-ma-moving-average-va-cach-su-dung

END

DELETE
ID: 
