# Detecting staked LP tokens

An initial naive approach to take when counting LP tokens an account owns would be to simply check the balance the account currently holds. The Uniswap subgraph makes this particularly easy. The problem with this approach is that many times LP tokens are staked in various contracts that provide reward incentives, at which point the tokens are not held by the account.

A different approach that addresses this issue is to compute the LP tokens that have been “minted” and “burned” by the account, when depositing and withdrawing assets from the pool. This addresses the problem of LP tokens being staked in any unknown contract, however, it comes with some important caveats:

1. If an account transfers LP tokens to a different account, or contract, in a way that would imply relinquishment of ownership, they would still appear as being owned by the original minter account.
2. If an account receives LP tokens from a different minter account, they are (currently) not counted as being owned by the receiving account.

The first issue is easy to address in a manual fashion by providing an option to “ignore” the LP position in question. The second issue can be addressed by accounting for received LP transfers, and differentiating these from transfers that might be the result of unstakings, which we are currently working on.

It’s almost certain that our approach will evolve over time as changing practices with regard to staking contracts, feedback from users, and our own experience will improve our solution to the problem described.
