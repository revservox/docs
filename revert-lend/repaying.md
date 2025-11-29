# Repaying

### Repaying

When repaying a loan in the Revert Lend protocol, the borrower needs to return the amount of tokens they initially borrowed, along with any interest that has accrued. The total repayment amount is determined by the current debt exchange rate, which includes the accumulated interest. Borrowers can make full or partial repayments, depending on their preference. With each repayment, the borrower’s outstanding debt is reduced by the amount repaid.

<figure><img src="../.gitbook/assets/repay1.png" alt=""><figcaption></figcaption></figure>

### Repaying Using Collateral and Swapping Atomically

In some cases, borrowers may choose to repay their loan using the collateral itself. This process can be done atomically, meaning the collateral is swapped directly for the borrowed tokens within a single transaction. The protocol allows for such operations using the LeverageTransformer contract. By swapping part of the collateral for the borrowed tokens, the borrower can effectively reduce their debt without needing additional outside funds.

<figure><img src="../.gitbook/assets/repay2.png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/repay3.png" alt="" width="563"><figcaption></figcaption></figure>

### Fully Repaying Loan and Withdrawing LP Position from Vault

Once the loan is fully repaid, including all accrued interest, the borrower’s obligations are considered fulfilled. At this point, the collateralized LP position, which had been locked in the Vault contract, is released. The borrower can then withdraw their Uniswap v3 LP position from the Vault. This gives them back full control over their LP assets, allowing them to manage, trade, or reinvest the position as they see fit.
