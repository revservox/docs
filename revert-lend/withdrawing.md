# Withdrawing

Redeem your rlUSDC and you receive USDC at the current exchange rate: your principal plus your share of the interest accrued since you deposited.

<figure><img src="../.gitbook/assets/Captura de pantalla 2024-08-30 a la(s) 12.14.05 p.m..png" alt=""><figcaption></figcaption></figure>

### When the pool is heavily utilized

Your USDC is not sitting idle: it is lent out, which is where the yield comes from. If most of the pool is currently borrowed, there may not be enough idle liquidity to fill your full withdrawal immediately. The protocol does not pretend otherwise, and it does not guarantee instant exit at high utilization.

What restores liquidity is the interest rate model. A drained pool pushes the borrow rate up, which makes carrying debt more expensive and repayment more attractive, and makes lending more attractive at the same time. Repayments and new deposits refill the idle buffer, and your withdrawal can complete. If you anticipate needing fast access to your funds, watch the pool's utilization: it is the single number that determines how quickly you can exit.
