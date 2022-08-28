# Hedge Fund Barrier Option

A hedge fund barrier call option is a note whose payoff is based on a basket of hedge funds. The deals are structured so that once the barrier hit, the funds in the basket are sold off, with the realized fund value depending on the redemption period of each fund. 

The difference between the redeemed value of the basket of funds and the strike price of
the call (usually set at 75% of the notional) is forwarded to the investor. When the redeemed basket value falls below the strike price the investor loses money on the deal.

By construction, the probability of this happening is very small: no fund may make up more than _ 5% of the basket by value, so for the basket to fall below the strike price requires that at least 5 funds experience a serious downturn. 

Since the funds in a basket are generally spread over a variety of strategies, the probability of experiencing a loss under to an individual deal under normal market conditions is small enough that traditional VAR measurements result in zero economic capital.

Nevertheless, when the entire portfolio is considered, there should be a quantifiable level of market risk. We have performed a detailed analysis of the expected losses to a small number of deals, and scaled the results to estimate the economic capital of the portfolio.


The market risk associated with an individual deal is small–the economic capital typically vanishes since the probability of a loss is small enough (< 0.03%) that there are no losses at the 99.93rd percentile. This will not be the case when considering the entire portfolio, since while the probability of a loss to each contract is small there are 130 contracts. (If the average loss probability for all individual deals is larger than _ 0.0005%, then ignoring correlations between deals, there should be capital on the portfolio.)

The goal here is to estimate the market risk of the entire portfolio of such deals through analysis of a small representative sample of the portfolio and scaling up to the entire portfolio. While simulating the entire portfolio would result in a more accurate determination of the capital, the result is small enough that the dominant risk factors likely arise from sources other than market risk, and an order-of magnitude determination is likely sufficient.

The methodology is straightforward: Each representative deal is simulated with a given number N of Monte-Carlo simulation paths to determine the loss distribution as a fraction of the initial basket level. Each deal in a class is assumed to have the same number of losses, identically distributed as a fraction of the starting basket level of the deal, from which dollar values of the losses for each deal are determined. 

The aggregate of the dollar-value losses from all deals then represents the loss distribution of the entire portfolio in N simulations, and the 99.93rd percentile loss to the portfolio is then determined.

This should give a measure of the relative risk of each deal–the smaller the leverage-ratio, the smaller the risk. (This gives the ratio of the volatile portion of the basket to the current option value.) What this does not capture is the relative volatilities of each deal, which are perhaps as important for assessing risk, but are less readily available. 

In generating the loss distributions for the representative deals, we assumed that the fund returns were correlated and log-normally distributed. The funds were simulated with a relatively short time interval (roughly 1 week) until the barrier was hit or the one year horizon expired. 

If the barrier was hit the basket is to be sold off, and the funds were simulated in monthly intervals and the final values of each fund picked off of the resulting flows based on their redemption periods. If the sum of the final fund values (and any cash holdings) is less than the strike price of the deal, then there is a loss to the investor.

These are similar to the barrier options (see https://finpricing.com/lib/EqBarrier.html), except that the leverage ratio may be readjusted (‘releveraging’) if the basket value crosses a barrier–either upwards or downwards. These deals should therefore be less risky than ordinary barrier options, and we have shown the effect of including them in the loss aggregation as if they were ordinary barrier options.



