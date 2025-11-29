# Liquidations

### Position Health

In the Revert Lend protocol, the health of a position is determined by comparing the value of the collateral (the Uniswap v3 LP position) to the outstanding debt associated with the loan. A position is considered healthy if the collateral value exceeds the debt, ensuring that the loan is adequately secured. However, if the debt grows due to accumulating interest or if the collateral value decreases, the position may become unhealthy. When a position’s debt exceeds its collateral value, it becomes eligible for liquidation to protect the protocol and ensure that the loan is repaid.

<figure><img src="../.gitbook/assets/liquidation1.png" alt="" width="373"><figcaption></figcaption></figure>

### Who Can Liquidate?

Once a position is deemed unhealthy and enters liquidation mode, any account in the protocol can initiate the liquidation process. To do this, a user calls the liquidate function, repays the outstanding debt of the position, and, in return, receives a liquidation reward. This reward, known as the liquidation penalty, ranges from 2% to 10% of the debt value, depending on how close the debt is to the collateral value. This system incentivizes users to actively monitor the protocol and liquidate risky positions, helping maintain the stability and integrity of the lending pool.

### Liquidator Bots

The Revert Lend protocol offers an open-source liquidation bot as a reference implementation. The bot’s source code is available at the [Revert Finance Liquidator-js GitHub Repository](https://github.com/revert-finance/liquidator-js). This bot monitors the health of all positions within the protocol and initiates liquidations when a position becomes unhealthy—i.e., when its debt exceeds the collateral value. While the Revert team runs this bot as a backstop, we encourage other liquidators to also operate and participate in the liquidation process to enhance decentralization and the protocol’s resilience. Liquidation penalties range from 2% to 10%, depending on the position’s risk level.
