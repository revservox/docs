# How Revert measures performance

Every number on a position page is computed from the position's full cash-flow history: deposits, withdrawals, fee collections, reward claims, gas costs, and the current state of the position. Each flow is recorded with its token amounts and the prices at the time it happened. Nothing is sampled or approximated from charts. This page defines each metric precisely, so you can recompute any of them and know exactly what you are looking at.

## The benchmark

PnL is always measured against a benchmark, selectable from the reference dropdown on the position page:

- **HOLD** (default): what you would have if you had kept the deposited tokens in your wallet. All flows are valued at current prices, so pure price movement cancels out and what remains is the pool's actual contribution: fees, rewards, and divergence.
- **USD**: what you would have if you had kept the dollars instead of buying the tokens. Flows are valued at their historical prices.
- **ETH**: the same comparison, denominated in ETH.
- **token0 / token1**: everything denominated in one of the pair's tokens.

Changing the benchmark changes PnL, APR, and ROI together. The question each answers is different: HOLD isolates what providing liquidity earned you versus holding; USD measures it against having stayed in cash.

## The metrics

**Pooled assets.** The position's current token amounts valued at current prices. Principal only: uncollected fees and unclaimed rewards are tracked separately.

**Total PnL** (header). Everything the position has earned or lost against the benchmark:

```
total PnL = divergence + fees (collected + uncollected)
          + rewards (claimed + unclaimed) - gas costs
```

**Pool PnL** (Performance panel, "excluding gas"). The pool's own contribution, with gas and incentive rewards stripped out:

```
pool PnL = divergence + fees (collected + uncollected)
```

The two differ exactly by rewards minus gas. On a staked Aerodrome position, where income arrives as AERO rather than fees, total PnL carries the rewards and pool PnL does not. Compare them and you can read where your return actually comes from.

**Divergence loss.** Pool PnL minus fees. This is the cost of the pool's price action: what rebalancing your inventory against the market cost you relative to the benchmark. It is reported as its own line rather than hidden inside PnL, because a position with strong fee income and worse divergence is a different trade than one with modest fees and none.

**Total APR** (header). Total PnL annualized over the position's life:

```
APR = total PnL / time-weighted average balance / years elapsed * 100
```

The denominator is the time-weighted average of capital actually in the position, so adding or removing liquidity mid-life does not distort the rate. Years elapsed runs from the first mint. Income counts fees and rewards; gas is subtracted.

**Fee APR.** The same annualization with only fees in the numerator. On a staked Aerodrome position this trends toward zero by design; the income shows up in rewards instead. See [Staking & AERO rewards](../aerodrome/staking-and-rewards.md).

**ROI.** Total PnL divided by what you put in (net deposits plus gas), not annualized. APR tells you the rate; ROI tells you the cumulative result.

**Avg daily fees.** Total fees (collected plus uncollected, at current prices) divided by position age in days.

**Age.** Time since the position's first mint.

**Rewards APR** (pool-level, Aerodrome). Annualized gauge emissions, valued at the reward-token price, divided by pool TVL:

```
rewards APR = (rewards per second * AERO price * seconds per year / pool TVL) * 100
```

This is a pool-wide reference rate, not a floor: it assumes liquidity is evenly distributed, and your realized rate depends on where your liquidity sits. A staked position concentrated tighter than the rest of the pool's staked liquidity earns more than this while in range; a wider one earns less; one parked out of range earns nothing. Emissions are re-voted weekly, so this number moves with each epoch.

## Reading them together

The metrics are designed to be cross-examined:

- **Fee APR high, total APR low**: divergence is eating the fee income. Check the divergence loss line and the price chart.
- **Total PnL positive, pool PnL negative**: the pool itself lost against the benchmark and rewards carried the position. Your return depends on the reward token's price holding up.
- **APR strong, ROI small**: the rate is good but it has not compounded long enough, or the position is young. Age tells you which.

If a number on the position page does not reconcile with these definitions, that is a bug, and we want to hear about it.
