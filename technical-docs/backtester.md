# Backtester

We’ve published the [backtester code](https://github.com/revert-finance/revert-backtester) as a [ClojureScript](https://clojurescript.org/) library under the MIT license.

{% embed url="https://github.com/revert-finance/revert-backtester" %}

The backtesting technique for Uniswap v3 LP positions that we use, relies on periodic pool snapshot data, such as that provided by the Uniswap v3's subgraph _poolHourData_ entities.&#x20;

This technique is fairly accurate, though the accuracy will be correlated with the proportion of time that a position would have been in range given its selected price ranges. It also has the advantage of being pretty fast.&#x20;

When the Initiator backtester was launched we ran an accuracy test to check its performance, the results can be found in [this post](https://medium.com/@revert_finance/presenting-the-initiator-3450f63d6b7e).
