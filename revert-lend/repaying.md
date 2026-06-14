# Repaying

Repay in full whenever you want: there is no schedule and no penalty for early repayment, and your debt is simply the borrowed amount plus accrued interest, tracked by the debt exchange rate. Partial repayments work too, with one constraint: a partial repayment must leave your remaining debt at or above the vault's minimum loan size. To clear a balance below that, repay in full. Every repayment reduces your debt directly.

<figure><img src="../.gitbook/assets/repay1.png" alt=""><figcaption></figcaption></figure>

### Repaying from the collateral

You do not need outside funds to deleverage. Part of the position itself can be swapped into the borrowed token and used to repay, atomically in a single transaction. This is the lever that lets you cut debt in response to market moves without touching your wallet.

<figure><img src="../.gitbook/assets/repay2.png" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/repay3.png" alt="" width="563"><figcaption></figcaption></figure>

### Closing out

Once the debt is fully repaid, including accrued interest, the position is released from the vault back to your full control: manage it, move it, or withdraw it as you see fit.
