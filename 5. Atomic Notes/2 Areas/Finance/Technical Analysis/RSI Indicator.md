2025-10-26 11:26

TARGET DECK: [[technical analysis]] 
START
Basic
RSI Indicator
Back:
## Main
### 📐 **Definition**

The **RSI (Relative Strength Index)** measures the speed and change of price movements over a given time period — typically **14 periods**.
It is a **bounded oscillator** that moves between **0 and 100**.

![[Pasted image 20251026113124.png]]

### 📊 **How It Works**

1. **Calculate daily changes (Δ):**
    
    - If price increased → that’s a gain.
        
    - If price decreased → that’s a loss.
        
2. **Compute the average gain and loss** over _n_ periods (default: 14).
    
    - Use a **smoothed** average (like EMA style) for continuous RSI.
        
3. **Compute RS (Relative Strength):** 
    RS=Average GainAverage LossRS = \frac{\text{Average Gain}}{\text{Average Loss}}RS=Average LossAverage Gain​    
4. **Plug into RSI formula** above.

⚙️ **Interpretation**

|RSI Value|Market Condition|Typical Meaning|
|---|---|---|
|**> 70**|Overbought|Possible pullback or reversal down.|
|**< 30**|Oversold|Possible bounce or reversal up.|
|**50**|Neutral|Balanced buying and selling.|

### 💹 **Example (Step-by-Step)**

Say the last 14 closing prices show the following average changes:

- Average gain = 0.8%
    
- Average loss = 0.4%
    

Then:

RS=0.80.4=2RS = \frac{0.8}{0.4} = 2RS=0.40.8​=2 RSI=100−1001+2=66.67RSI = 100 - \frac{100}{1 + 2} = 66.67RSI=100−1+2100​=66.67

So RSI ≈ **67**, suggesting moderately strong upward momentum.


### 🧭 **Practical Use in Trading**

- **Divergence:**  
    Price makes a new high, but RSI doesn’t → possible trend reversal signal.
    
- **Centerline crossover:**  
    RSI crossing **50** often indicates momentum change.
    
- **Combination strategies:**  
    RSI used together with **Moving Averages**, **MACD**, or **Bollinger Bands** to confirm signals.




## References
https://www.vietcap.com.vn/kien-thuc/chi-so-rsi-la-gi-ung-dung-rsi-trong-dau-tu-chung-khoan

END

DELETE
ID: 
