# How to Create a Position

Creating a position with Revert is a discovery-first process that lets you find the best pools before opening positions.

## Browse Pools

Start by browsing available liquidity pools across multiple protocols and networks.

### Network & Token Filters

- **Any network** - Select specific networks (Ethereum, Polygon, Arbitrum, Optimism, Base, Unichain)
- **Any tokens** - Filter by token pairs
- **+ filters** - Opens advanced filtering panel

Click the **"+ filters"** button to access additional filtering options:

- **Exchanges** - Filter by specific exchanges/protocols (Uniswap V3, V4, Aerodrome)
- **Pool address** - Search for a specific pool by contract address
- **TVL** - Set minimum and maximum Total Value Locked range (in USD)
- **Fees APR** - Filter by fee APR percentage range
- **Fees/TVL** - Filter by fee efficiency ratio
- **Pool age** - Filter by pool age in days

Click **"Apply"** to activate filters or **"Clear"** to reset them.

### Quick Filters

- **Rewards** - Pools with active reward programs
- **Trending** - Popular pools by volume or new positions
- **New pools** - Recently created pools
- **Loan** - Pools with lending/borrowing support

### Pool Metrics

Each pool row displays:

- **Pool/Fee Tier** - Token pair and fee percentage (e.g., WETH/USDC 0.05%)
- **TVL** - Total Value Locked in the pool
- **Volume** - Trading volume for the selected time period
- **Fees** - Total fees generated
- **Fees/TVL** - Fee efficiency ratio
- **Age** - How long the pool has existed
- **Fees APR** - Annual percentage rate from trading fees
- **Rewards APR** - Annual percentage rate from external rewards (if available)

## Select a Pool

Click the expand button (▼) on any pool row to view details and create a position.

The expanded view shows:

### Pool Overview

- **Price Chart** - Historical price movement for the token pair
- **TVL/Volume/Fees Graphs** - Performance metrics over time
- **Current Prices** - Real-time prices for both tokens
- **Top Positions** - Existing positions in this pool showing their ranges, sizes, and performance

### Create Position Panel

On the right side, you'll see the position creation interface.

## Configure Your Position

### Amounts to Deposit

1. Select **"Same Tokens"** to deposit both tokens at current ratio, or choose a single token to swap
2. Toggle **"Use prices ratio"** - When enabled, forces deposits to use the exact current pool ratio without performing any swap
3. Enter amounts for each token (use **MAX** button to deposit full balance)
4. Adjust **deposit slippage** if needed (default 1.0%)

{% hint style="info" %}
If "Use prices ratio" is disabled and you enter custom amounts, Revert may swap tokens to achieve the required ratio (0.65% swap fee applies).
{% endhint %}

### Price Range Selection

Choose the price range where your liquidity will be active:

#### Preset Buttons

- **MIN** - Full range from minimum to current price
- **1%** - ±1% from current price (very concentrated)
- **5%** - ±5% from current price
- **10%** - ±10% from current price
- **20%** - ±20% from current price
- **FULL** - Full range (all prices)

#### Manual Entry

Enter specific prices for your minimum and maximum range. The visual graph shows:

- Current pool price
- Your selected **NEW MIN** and **NEW MAX** prices
- Where your liquidity will be active (green area)

### Swap Preview

If swapping tokens, you'll see:

- Swap amounts and direction
- 0.65% swap fee
- Slippage tolerance (adjustable, default 0.50%)

## Run Backtester (Optional)

Click **"Run backtester"** to simulate how your position would have performed historically with the selected parameters.

The backtester shows:

- Projected fees earned
- Impermanent loss/gain
- Comparison vs. holding tokens

{% hint style="info" %}
**Fee dilution** refers to the dilution effect of adding more capital to a pool (assuming volume had remained constant). e.g., adding 10M to a 5M pool might reduce APR considerably more than adding 50k.
{% endhint %}

## Create Position

Review the **Transaction summary** showing:

- Expected amounts to add
- Minimum amounts after slippage
- Estimated gas costs

Click **"Create [TOKEN/TOKEN] position"** to confirm and create your position.

After approving token permissions (if needed), the transaction will create your position NFT directly with the protocol's contracts.
