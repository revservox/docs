# Liquidations

Liquidation is not an event that strikes from nowhere. It is a distance you can read and manage: the gap between your collateral value, after collateral factors, and your debt.

### Position health

A loan is healthy while the collateral value exceeds the debt. The gap closes from two directions: interest accrues into the debt continuously, and the collateral side moves with pool prices and divergence loss. When the debt crosses above the collateral value, the loan becomes liquidatable.

<figure><img src="../.gitbook/assets/liquidation1.png" alt="" width="373"><figcaption></figcaption></figure>

### What a liquidation costs you

Any account can liquidate an unhealthy loan: the liquidator repays your outstanding debt and receives collateral worth the debt plus a liquidation penalty. The penalty ranges from 2% to 10% of the debt value, scaling with how far the debt has run past the collateral value, so a loan caught just past the line costs far less than one deep underwater. Whatever value remains after debt and penalty is returned to you. You lose the penalty and the position, not everything.

### Liquidator bots

Liquidation is open and permissionless by design. Revert publishes an open-source reference bot at the [liquidator-js repository](https://github.com/revert-finance/liquidator-js) and runs it as a backstop, but anyone can operate one, and we encourage it: more independent liquidators means unhealthy debt is cleared faster and the lending pool stays solvent for everyone.
