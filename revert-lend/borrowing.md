# Borrowing

### Depositing LP Position and Borrowing Tokens

In the Revert Lend protocol, users can deposit their Uniswap v3 or Aerodrome Liquidity Provider (LP) position as collateral and borrow tokens in a single step. The LP position, represented as an NFT, is transferred to the Vault contract, effectively locking it in the protocol. This collateral allows the user to borrow tokens from the lending pool immediately. The amount of tokens that can be borrowed is determined by the collateral value of the LP position, based on the lower of the two assets' collateral factors in the LP pair. Borrowed tokens are typically issued in a protocol-determined ERC-20 token, such as USDC, and are credited to the user's account for use in other investments or purposes. The LP position remains locked in the Vault as collateral until the loan is repaid.

### Using Aerodrome Positions as Collateral

Aerodrome positions on Base can be used as collateral, but must first be staked with the [Gauge Manager](../aerodrome.md). The staking requirement ensures the position is properly wrapped for use with Revert Lend.

When an Aerodrome position is used as collateral:
- AERO rewards continue to accrue while the position is collateralized
- You can claim or auto-compound AERO rewards at any time
- The position can be managed like any other collateralized position

<figure><img src="../.gitbook/assets/borrow 1.png" alt=""><figcaption></figcaption></figure>

### Accumulating Interest

After borrowing tokens, the debt begins to accumulate interest according to the protocol’s interest rate model. The interest is added to the loan balance over time, increasing the total amount that the borrower owes. This interest rate is dynamic, adjusting based on the supply and demand within the lending pool. Borrowers need to monitor their debt because the accumulating interest can impact the health of their loan, potentially leading to liquidation if the debt grows too large compared to the collateral value.

### Loan health

L**oan health** is a measure of how safely a loan is collateralized by the value of the associated Uniswap v3 Liquidity Provider (LP) position. A loan is considered "healthy" if the value of the collateral (the LP position), given collateral factors, is greater than the outstanding debt associated with that loan.

Loan health is determined by comparing the collateral's value to the debt:

* **Healthy Loan**: If the collateral value exceeds the debt, the loan is in good standing.
* **Unhealthy Loan**: If the debt exceeds the collateral value, the loan is at risk of liquidation.

When a loan becomes unhealthy, the position may be liquidated to cover the debt. The protocol uses a liquidation process to ensure that the debt is repaid, and any remaining value after the liquidation is returned to the original owner. Maintaining a healthy loan is crucial for avoiding liquidation and retaining control over the collateralized position.

<figure><img src="../.gitbook/assets/borrow2.png" alt="" width="375"><figcaption></figcaption></figure>
