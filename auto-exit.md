# Auto-Exit

Auto-Exit lets you pre-configure a position so that the liquidity is automatically withdrawn when the pool price reaches a predetermined value. Moreover, you can optionally configure the system to swap from one token to the other on withdrawal, providing a safety net for your investments akin to a stop-loss order.

<figure><img src=".gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

## Maximum Price Impact

During auto-exit swaps, the contract cross-verifies with the pool's TWAP oracle to prevent potential price manipulation. While setting up an auto-exit position, you choose a maximum price impact for swaps. This determines the permissible deviation between the pool price at the time of execution and the actual swap price, accounting for the pool fee, swap price impact and possible slippage.

Revert bots perform swaps sourcing liquidity from the 0x protocol, considering the max price impact as the swap execution threshold. All swaps can be confirmed on-chain, with 0x ensuring optimal pricing and providing slippage protection when available.

When swaps are executed on auto-exit operations, the contract runs a check against the pool TWAP oracle to avoid price manipulations of the pool.



## Selecting a fee source

To set up auto-exit on a position, you need to decide the source for paying protocol fees and gas costs. You have two options: a portion of the total position assets or a portion of the uncollected fees.

1. **Position Assets**: The protocol fee is 0.15%. Any percentage chosen above this will contribute to the gas budget. Note that if the gas budget is too low due to high gas prices at the time of auto-exit, the action won't trigger. Therefore, it's crucial to anticipate gas price fluctuations and allocate a sufficiently high percentage to ensure coverage. Surplus funds from the gas budget are returned to your wallet upon triggering the auto-exit.
2. **Uncollected Fees**: The protocol fee here is 2% of the uncollected fees at execution. The selected percentage should exceed this fee and sufficiently cover potential gas cost increases. Any excess in this scenario is also returned to your wallet upon triggering the auto-exit.

## Left-over tokens

When auto-exit is configured to be executed when a position is still in-range there may be slippage when removing the liquidity. This may lead to a few left-over tokens after swapping, because not all available tokens may be swapped. These will be sent to the position owner in the same transaction.

However, the operator (bots) are incentivized to maximize the capital used, because when swapping is configured, their fee is derived from the tokens which are successfully swapped to the target token.

## Aerodrome Support

Auto-Exit is not currently supported for Aerodrome positions on Base.

