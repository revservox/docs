# Leverage

Leverage turns borrowing power into position size: borrow USDC against your position, swap it into the pool's tokens, and add them back to the same position, all in a single transaction. The result is a larger position earning on borrowed capital, with debt interest accruing until the loop is unwound.

### The loop

1. **Borrow** against the position's collateral value, up to the pair's collateral factor.
2. **Swap** the borrowed USDC into the position's tokens at the ratio the range requires.
3. **Reinvest** the proceeds into the same position, increasing its liquidity.

Each pass increases both the position and the debt, so the available headroom shrinks with every iteration: the collateral factor caps how far the loop can go. Unwinding works the same way in reverse, removing liquidity, swapping, and repaying in one transaction. See [Repaying](repaying.md).

<figure><img src="../.gitbook/assets/leverage1.png" alt=""><figcaption></figcaption></figure>

### What leverage actually does

Leverage scales both sides of your trade. Fee income grows with the larger position; so do divergence loss and the debt's interest cost. The carry works while the position's income rate exceeds the borrow rate, and the borrow rate floats. A levered position also sits closer to liquidation than an unlevered one by construction: the same price move that dents an unlevered position can end a levered one. Size the loop so that the moves you consider normal for the pair leave your loan health intact. See [Liquidations](liquidations.md).
