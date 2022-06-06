# currencyStratBacktest - First Draft
USDZAR currency strategy backtest + analysis

## What the project does?
This program backtests a long-short currency strategy that trades the USDZAR.

The trading signal is based on the 15-day historical moving average of USDZAR price. The portfolio goes long returns when the current price is above the 15-day MA and goes short returns when it is below.

The program sizes the position using 90-day historical vol of returns (see AHL's video on volatility scaling for more info: https://www.youtube.com/watch?v=ZJXsoZprTn8)

It also computes some important properties that characterise the strategy:
  - Sharpe ratio
  - Max drawdown period
  - Max drawdown
  
## Methodology
This strategy computes the cumulative USD and ZAR balances and adjusts them based on the long or short trading signal. It computes the portfolios NAV at every timestep based on spot rates and net USD or RAND positions.

## Important results
1. Very volatile strategy
    - Large max drawdown window ~ 8 months. Maintaining a losing position for this long would be difficult

2. Largest drawdown los of ~6x one's funds

3. We note that the strategy's E(ret) and Sharpe are greatly improved by scaling the position with volatility
    - Using other schemes, such as scaling with signal strength worsen performance. Scaling the signal with the inverse of volatility also worsens    performance. The result of this, is that scaling with using a signal/ noise metric also worsens performance

4. We see oberve periods of appreciable underperformance when the USDZAR exhibits trending behaviour

## Imporvements next time
This strategy computes the cumulative USD and ZAR balances and adjusts them based on the long or short trading signal. It computes the portfolios NAV at every timestep based on spot rates and net USD or ZAR positions. 

This approach can be greatly simplified by considering return and not USD and ZAR balances at each timestep. Instead of building up cash balances in ZAR or USD bank accounts and profiting from this, a simpler approach could be to take whatever profits one makes from holding the USDZAR contract and being exposed to its return and closing out positions at the end of each day instead of having an accumulating exposure.

## Observations
1. Visual inspection of the graphs and of the USDZAR reveals that it most frequently trades in a range. This may imply that it tends to be a mean-reverting signal.

## Outstanding questions
1.  Could it be the case that volatility increases the likelihood of mean-reversion, which is why scaling position size with volatility works
    - It may well be the case that trading into volatility by scaling positions proportionally with volatility works well with range-bounded signals

