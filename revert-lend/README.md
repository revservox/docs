# Revert Lend

Revert Lend is lending built for liquidity providers. Your LP position becomes collateral without stopping being an LP position: it keeps earning, you keep managing it, and the automation tools keep working on it while it backs your loan.

Use Uniswap v3 positions, or [Aerodrome positions on Base](../aerodrome/README.md), as collateral to borrow USDC. Aerodrome collateral stays staked in its gauge, keeps earning AERO, and can auto-compound while the loan is open. Lend is integrated directly into the normal position management UI: there is no separate app to learn.

### What you can do

- Borrow USDC against your LP position: [Borrowing](borrowing.md)
- Lend USDC and earn the interest borrowers pay: [Lending](lending.md)
- Repay any amount at any time, with outside funds or from the collateral itself: [Repaying](repaying.md)
- Withdraw your lent USDC: [Withdrawing](withdrawing.md)
- Lever a position in a single transaction: [Leverage](leverage.md)
- Understand how unhealthy loans are closed: [Liquidations](liquidations.md)

### Automation keeps working

Auto-Range and Auto-Compound work on collateralized positions the same way they do on any other position. For Aerodrome collateral this includes [AERO auto-compounding](../aerodrome/aero-auto-compounding.md).
