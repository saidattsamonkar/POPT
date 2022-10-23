# Sortino Ratio NIFTY 50 Portfolio Optimization

## Description

This Project uses SciPy's SLSQP to optimize for Sortino Ratio and generate weights to actively manage NIFTY 50 Portfolio. When compared to Information Ratio and Sharpe Ratio, optimizing with Sortino Ratio gave the best results as it takes into consideration the standard deviations of only the portfolio drawdowns. 

![](https://github.com/saidattsamonkar/POPT/blob/main/Assets/Sortino.png | width=100)
<img src="https://github.com/saidattsamonkar/POPT/blob/main/Assets/Sortino.png" width="200" height="400" />


## Data 

The pool consists of equities which were in NIFTY 50 at the end of 2009. Equity data is fetched using the yfinance API.


## Steps 

1. Fetch equity returns data from t-1 to t-n
2. Optimize the data to get the Maximum Sortino Ratio (Rf is considered to be 0) subject to the following constraints
   - weights should be equal to 1 
   - Every equity in the portfolio should weigh less than the specified limit
   - Portfolio rebalance/turnover should be less than the specified limit
   - Sector weights should be less than the specified limits
3. Run simulation on the current month t, taking into account the transactional costs to rebalance the portfolio, and save the returns and update the new portfolio weights 


## Results

The optimized portfolio had superior returns delivering 28.69% higher mean monthly returns at the cost of 1.54% higher monthly mean standard deviation when compared to the benchmark from 2010-01 to 2022-09.

Simulation parameters:
- lookback period = 12 months
- max portfolio rebalance/turnover = 5%
- max equity weight = 5%
- max sector weight = 30%
- transaction cost = 1% of buy and sell during rebalancing

![](https://github.com/saidattsamonkar/POPT/blob/main/Assets/Sim.png)

The following graph shows the 24-month rolling IR of the Sortino optimized portfolio(red) and the 24-month rolling IR of an ideal portfolio(turquoise). The ideal portfolio was generated by passing the current month's data to the optimizer, so that we can generate the best possible portfolio from the equities available to us.


![](https://github.com/saidattsamonkar/POPT/blob/main/Assets/IR.png)

The optimized portfolio had 24-month rolling IR around 1.0 until the end of 2014 after which it started to dip. Tests done on updated Nifty 50 pool of of equities showed the dip can be explained by the lack of updates to the pool of equities. At the end of 2022-09 only 28 equities remained in the Nifty 50 out of the 50 we started with. The dip can also be explained by the dip in the ideal portfolio. 



