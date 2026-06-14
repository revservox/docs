# Backtest before funding

Range width is the biggest decision you make when opening a concentrated-liquidity position, and most LPs make it by instinct. You do not have to: the position creation flow includes a backtester that replays your exact range against the pool's history before you commit capital.

## The trade-off you are pricing

A tighter range concentrates your liquidity, which raises your share of fees while the price is inside it, and raises everything else too: time spent out of range earning nothing, divergence loss when the price crosses your bounds, and rebalancing frequency. A wider range earns a lower rate more reliably. Neither is better in general. Which is better for a specific pool depends on how that pool's price actually moves, which is an empirical question, and empirical questions deserve data.

## Using the backtester

In [Create Position](../initiator/README.md), set your candidate range and run the backtester. It replays the position against the pool's historical data and reports projected fees earned, impermanent loss or gain, and the result compared against simply holding the tokens. Run it for the tight version and the wide version of the range you are considering, and compare the net outcomes, not the fee numbers alone: a range that earned triple the fees and lost more than the difference to divergence is the worse trade dressed as the better one.

Two caveats to keep in front of you:

- **Accuracy correlates with time in range.** The technique is built on periodic pool snapshots, and it is most reliable for ranges that would have stayed in range most of the period. Results for very tight ranges carry more uncertainty, which is exactly when you should be most skeptical of a flattering number.
- **Fee dilution.** The backtest assumes historical volume against historical liquidity. Adding large capital to a small pool dilutes the fee rate for everyone, including you: adding $10M to a $5M pool will not earn what the history suggests. The creation flow flags this.

## The discipline

A backtest is history, not a forecast. What it actually gives you is a falsifiable baseline: how this range would have behaved in regimes the pool has already seen. If a range only works in the backtest's calmest stretch, you have learned what conditions you are betting on, and that knowledge is the real product. Fund the position when you can say which regime you expect, not just which number you liked. Once funded, the position page tells you whether reality is tracking the test: see [How Revert measures performance](../position-analytics/how-revert-measures-performance.md).
