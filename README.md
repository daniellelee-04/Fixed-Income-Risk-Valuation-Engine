# Fixed Income Risk and Valuation Engine

### Why I built this
As an accountancy student, I wanted to move beyond static spreadsheets and build something that handles live market volatility. Most bond models I’ve seen in class are based on fixed inputs, so I designed this engine to pull real-time Treasury data and run "what-if" simulations that actually reflect current macro conditions.

### The Logic Behind the Model
* **The Yield Curve:** I used yfinance to get live Treasury yields. To fill in the gaps for maturities like the 1-year and 20-year, I manually integrated futures data and used PCHIP interpolation. I chose PCHIP because it creates a smoother, more realistic curve than a simple straight-line approach, which can give unrealistic results for mid-term bonds.
* **Credit Spreads:** Since corporate bond data is harder to find for free, I used Equity Beta as a risk proxy. The logic is that a company with a higher beta (like Amazon) should carry a higher credit spread than a more stable company. 
* **Duration:** I calculated effective duration to measure sensitivity. It’s one thing to know a bond is "long-term," but seeing that a Disney bond might drop 8% because rates move 1% really puts the risk into perspective.

### Stress Testing Results
I ran 1,000 simulations using a Monte Carlo approach to see what the worst-case scenario might look like. I also added a 1% probability of a default event with a 40% recovery rate to ensure the "tail risk" was accounted for.

---

### Internal Memo: Portfolio Risk Assessment
**Date:** January 8, 2026

**Executive Summary**
The portfolio is currently valued at $497.26. Based on the simulations, the risk level is Conservative. The 95% Value-at-Risk (VaR) is $0.78. This means there is a 5% chance the portfolio will lose more than $0.78 over the next year based on current interest rate volatility.

*Note: This VaR figure reflects interest rate sensitivity, it does not include the potential 60% capital loss from the modeled 1% default event, which is treated as a separate tail-risk scenario.*

**Key Vulnerabilities**
The biggest issue right now is the Disney (DIS) position. Because it has such a long duration (7.64 years), it acts as a massive lever for interest rate risk. If the Fed stays hawkish and rates go up, this asset will drag down the entire portfolio's performance.

**My Recommendation**
We should "shorten" the portfolio. I’d suggest cutting the Disney and Amazon positions by about 20% each and moving that cash into 3-month Treasury bills. This would bring our overall duration down from 4.44 to a safer target of around 3.0, protecting our capital better if rates continue to climb.
