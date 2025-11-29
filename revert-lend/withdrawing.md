# Withdrawing

### Withdrawing Lent Tokens

When a lender decides to withdraw their lent tokens from the Revert Lend protocol, they can do so by redeeming their rlTokens. rlTokens represent the lender's share of the lending pool and accrue value as borrowers repay loans with interest. Upon withdrawal, the lender exchanges their rlTokens for the corresponding amount of the underlying asset, such as USDC, from the lending pool. The amount received will be based on the current exchange rate, which reflects the accumulated interest and overall performance of the pool.

<figure><img src="../.gitbook/assets/Captura de pantalla 2024-08-30 a la(s) 12.14.05 p.m..png" alt=""><figcaption></figcaption></figure>

### What Happens If There Are Not Enough Tokens Available

In situations where the lending pool does not have enough available tokens to fulfill a withdrawal request, the lender may encounter a liquidity shortage. This can happen if a large portion of the pool’s assets are currently lent out to borrowers. The protocol does not guarantee immediate liquidity, as it relies on the interest rate model to manage liquidity levels dynamically.

If there’s insufficient liquidity, the lender may need to wait until more tokens become available—either through borrowers repaying their loans or new lenders adding assets to the pool. The protocol’s interest rate model will respond to the liquidity shortage by increasing interest rates, incentivizing borrowers to repay their loans faster and encouraging other lenders to contribute more assets to the pool, thereby restoring liquidity.
