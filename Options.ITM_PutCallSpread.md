---
id: 58babbczzdg52u4iqlw64fb
title: ITM_PutCallSpread
desc: ""
updated: 1726665578926
created: 1726665553764
---

Selling an **in-the-money put credit spread** is an options strategy that involves selling a higher-strike **put option** and buying a lower-strike **put option** on the same stock with the same expiration date. The strategy generates a net credit (you receive money upfront) and is used when the trader expects the stock to remain above the short put strike price by expiration.

### How the In-the-Money Put Credit Spread Works:

1. **Selling a Higher-Strike Put** (Short Put):

   - You sell a put option with a strike price that is **in-the-money** (above the current stock price).
   - Selling this put option gives you the obligation to buy the stock at the strike price if the stock price is below that level at expiration.

2. **Buying a Lower-Strike Put** (Long Put):
   - You simultaneously buy a put option with a lower strike price to limit your downside risk.
   - This put option acts as insurance and caps the maximum loss on the trade.

The difference in premiums between the sold and bought put options creates a **net credit** for the trade.

### Example of Selling an In-the-Money Put Credit Spread:

Let’s say **XYZ stock** is currently trading at **$98**. You believe the stock will stay above **$95** by expiration but want to enter an in-the-money put credit spread for higher premium collection.

- **Sell a $100 strike put** for **$5.00 premium**.
- **Buy a $95 strike put** for **$2.00 premium**.

### Net Credit:

The difference between the premiums collected and paid is your net credit:
\[
\text{Net Credit} = \text{Premium Received from Selling} - \text{Premium Paid for Buying}
\]
\[
\text{Net Credit} = 5.00 - 2.00 = 3.00
\]
Since each option contract controls 100 shares, the total net credit is:
\[
\text{Total Net Credit} = 3.00 \times 100 = 300
\]
So, you receive **$300** upfront for entering this spread.

### Maximum Profit:

The maximum profit occurs if the stock price remains **above the short put strike price ($100)** by expiration. In this case, both puts expire worthless, and you keep the entire credit:
\[
\text{Maximum Profit} = \text{Net Credit} = 300
\]

### Maximum Loss:

The maximum loss is the difference between the strike prices of the two options minus the net credit received. This occurs if the stock price falls **below the lower strike price ($95)** by expiration:
\[
\text{Maximum Loss} = (\text{Strike Price Difference} - \text{Net Credit}) \times 100
\]
\[
\text{Maximum Loss} = (100 - 95 - 3) \times 100 = 2 \times 100 = 200
\]
So, the maximum loss is **$200**.

### Break-Even Point:

The break-even point is the stock price at which the trade neither makes nor loses money. It's calculated by subtracting the net credit from the short put strike price:
\[
\text{Break-Even Point} = \text{Short Put Strike} - \text{Net Credit}
\]
\[
\text{Break-Even Point} = 100 - 3 = 97
\]
At expiration, if the stock is trading at **$97**, the profit/loss will be $0.

### Summary:

- **Maximum Profit**: $300 (if the stock stays above $100).
- **Maximum Loss**: $200 (if the stock drops below $95).
- **Break-Even Price**: $97 (where the trade breaks even).

### Why Use an In-the-Money Put Credit Spread?

- **Higher Credit**: Selling in-the-money puts typically generates a higher credit compared to out-of-the-money spreads.
- **Defined Risk**: The long put limits your maximum loss.
- **Moderately Bullish View**: This strategy works well if you expect the stock price to remain flat or rise slightly but don’t want to risk significant downside.

This strategy allows you to profit from time decay and the expectation that the stock will stay above a certain price by expiration. However, be aware that it involves higher risk compared to out-of-the-money spreads because the sold put is in the money at the start of the trade.
