# Auto-Range

Auto-Range automates the process of rebalancing your liquidity positions. When the token price moves and your position goes out-of-range by your selected percentage, Auto-Range springs into action. The system then automatically rebalances your position, by withdrawing the liquidity and recreating it with the same range width but centered around the current price, ensuring your liquidity stays in-range and collecting fees always.

<figure><img src=".gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

## Maximum Price Impact

During auto-range swaps, the contract cross-verifies with the pool's TWAP oracle to prevent potential price manipulation. While setting up an auto-exit position, you choose a maximum price impact for swaps. This determines the permissible deviation between the pool price at the time of execution and the actual swap price, accounting for the pool fee, swap price impact and possible slippage.

Revert bots perform swaps sourcing liquidity from the 0x protocol, considering the max price impact as the swap execution threshold. All swaps can be confirmed on-chain, with 0x ensuring optimal pricing and providing slippage protection when available.

When swaps are executed on auto-exit operations, the contract runs a check against the pool TWAP oracle to avoid price manipulations of the pool.

## Selecting a fee source

To set up auto-range on a position, you need to decide the source for paying protocol fees and gas costs. You have two options: a portion of the total position assets or a portion of the uncollected fees.

1. **Position Assets**: The protocol fee is 0.15%. Any percentage chosen above this will contribute to the gas budget. Note that if the gas budget is too low due to high gas prices at the time of auto-exit, the action won't trigger. Therefore, it's crucial to anticipate gas price fluctuations and allocate a sufficiently high percentage to ensure coverage. Surplus funds from the gas budget will not be spent and will be used as capital for the next position.
2. **Uncollected Fees**: The protocol fee here is 2% of the uncollected fees at execution. The selected percentage should exceed this fee and sufficiently cover potential gas cost increases. Any surplus funds from the gas budget will not be spent and will be used as capital for the next position.

## Left-over tokens

Given the fact, that swaps are executed via 0x as a swap aggregator and many other swaps may happen at the same time, it is impossible to calculate a swap which results in the exact proportion of tokens to be added to the new position. This may lead to a few left-over tokens after minting the new position. These will be sent to the position owner in the same transaction.

The operator (bots) are incentivized to maximize the capital added, because their gets their fees are calculated from the tokens added to the new position.
