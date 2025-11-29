# Uniswap v2 Positions

![Example](<../.gitbook/assets/image (23).png>)

### LP definitions

The following are definitions for the user to fully understand the concepts displayed on our analytics dashboards.

#### assets\_value:

Value in USD of the LP tokens detected as owned by the account, computed using the amount of underlying assets and current coingecko prices.

#### pool\_pnl:

Profit and loss for the LP position from only fees accrued and price divergence.\
\
&#xNAN;_`Pool PnL = value of current LP underlying tokens`_ \
&#x20;         _`- value of tokens deposited (at current price)`_ \
&#x20;         _`+ value of tokens withdrawn (at current price)`_

#### total\_pnl:

Profit and loss for the LP position from fees accrued, price divergence, gas costs, and reward incentives

```
Total PnL =   value of current LP underlying tokens
              - value of tokens deposited (at current price)
              + value of tokens withdrawn (at current price)
              + pending rewards at current prices
              + claimed rewards at current price
              - gas costs for all deposit and withdrawal transactions at current ETH price.
```

#### apr:

Annual percentage rate of returns given the current value of the underlying LP assets and deposits, withdrawals, gas costs, and staking rewards at current prices.

#### current\_assets:

The amount of underlying tokens corresponding to this LP position. Computed by taking all the pool LP tokens minted by the account, and subtracting any LP tokens that were burned for a withdrawal, as well as total current LP tokens for the pool, and the total amount of underlying assets.

#### invested\_assets:

The sum of all assets invested in the LP position, obtained from the respective mint transactions for the account and pool.

#### withdrawn\_assets:

The sum of all assets withdrawn out of the LP position, obtained from the respective burn transactions for the account and pool.

#### diffs:

The difference between the assets invested, subtracting the assets withdrawn, and the current assets in the LP position.\
\
&#xNAN;_`diffs = current assets - invested assets  + withdrawn asset`_

#### staking\_rewards:

The sum of all detected staking rewards (claimed and unclaimed) at current prices for the reward assets.

#### unclaimed\_rewards:

The sum of all detected unclaimed staking reward assets for the account and pool.

#### claimed\_rewards:

The sum of all detected claimed staking reward assets for the account and pool.

#### lp\_tokens:

LP tokens owned by the account. Computed by taking the LP tokens minted and subtracting any LP tokens that were burned for a withdrawal.

### Pool definitions

#### reserves:

USD value of the underlying token reserves for the pool.

#### volume:

USD value of the traded volume for the pool.

#### price\_divergence:

The running difference between the changes in prices (as percentages) for the underlying assets against the prices 30 days ago. Price divergences between a pair of assets can result in losses for liquidity providers.\
\
`Price Divergence = abs(token0_price_change_pct - token1_price_change_pt)`

