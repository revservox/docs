# Auto-compounder

Auto-compounder functionality for Uniswap v3 is provided by the **Revert Compoundor protocol** which allows for the automation through awarding executors (compoundors) a small fee to compensate for their gas costs, and a simple mechanism that incentivizes the compounding of positions as close to optimal as possible.\
\
Unlike its predecessor, in Uniswap v3, swap fees taken by the protocol for LPs do not accumulate inside the pool, but in a separate balance for each position. One consequence of this is that fees are not compounded automatically back into the position. \
\
Manual compounding of fees is possible, but it is a cumbersome process composed of the following steps:

1. Collecting fees via the NFT Manager contract.
2. Checking the amount**s** of token0/token1 required to swap so as to maximize the amount of liquidity added to the position.
3. Perform the swap without getting sandwiched.
4. Add the swapped amounts as liquidity to the position.

\
**Costs associated with compounding fees**\
\
Given the above described contract interactions, compounding fees can result in high gas costs. The decision of when to compound fees falls on a protocol mechanism that incentivizes frequency of compounding fees without the costs being a significant portion of the collected fees.\
\
The protocol allows a designated operator account, at any point, to call the autoCompound function. The operator will have to pay for the gas costs of making this transaction, and in exchange the protocol gets 2% of the uncollected fees compounded into the position.

### Protocol Roles

#### **Position owners**

Any account that adds his Uniswap v3 position to the Compounder contract and benefits from auto-compounding.

#### **Compoundors**

Any account that participates in auto-compounding positions deposited in the Compounder contract. Compoundors monitor collected fees, token prices and gas price to decide when to execute auto-compound operations, and win a part of the compounded fees as a reward (and to account for the gas cost of calling the auto-compounding function).&#x20;

#### **Contract deployer**

