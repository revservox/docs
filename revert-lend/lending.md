# Lending

The other side of every loan is a lender earning the interest. Deposit USDC into the lending pool and you receive rlUSDC, a vault share following the ERC-4626 standard. Your yield is the interest borrowers pay, denominated in USDC: no lockups, no reward emissions to sell.

<figure><img src="../.gitbook/assets/Captura de pantalla 2024-08-30 a la(s) 12.10.14 p.m..png" alt=""><figcaption></figcaption></figure>

### How the yield accrues

rlUSDC appreciates against USDC. The exchange rate starts at 1 and rises as borrowers pay interest into the pool; redeeming your shares later returns more USDC than you deposited. For illustration: deposit 10,000 USDC at an exchange rate of 1.00 and you hold 10,000 rlUSDC. If accrued interest has moved the rate to 1.06 when you redeem, your shares return 10,600 USDC.

Your realized rate depends on utilization: interest is only paid on the portion of the pool that is actually borrowed. High utilization means more interest per deposited dollar, but also less idle liquidity, which matters when you want out: see [Withdrawing](withdrawing.md).
