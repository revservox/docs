# The staked-collateral carry

A staked Aerodrome position earns AERO emissions. Used as Lend collateral, it keeps earning them while backing a USDC loan. The spread between the rewards APR and the borrow rate is a carry you can run deliberately, and this page is the operational checklist for running it: what to check before entering, what to watch while it is on, and the three triggers for taking it off. The mechanics live on [Using staked positions as collateral](../aerodrome/staked-lp-as-collateral.md); this is the decision layer.

## Before entering

1. **Confirm the income leg.** The pool's rewards APR is your collateral's yield; while staked it earns no swap fees, so this one number is the entire earning side. Remember it is a pool-wide estimate that assumes even liquidity distribution: your realized rate depends on your concentration relative to the rest of the pool's staked liquidity, and on staying in range.
2. **Confirm the cost leg.** The USDC borrow rate floats with utilization. Check it at current utilization and ask what it becomes if utilization rises.
3. **Size the borrow for the move you consider normal.** Your loan health absorbs pool price moves and divergence loss before liquidation becomes possible. Borrow so that an ordinary week in this pair leaves comfortable distance. The collateral factor caps what you can take; it is not a target.

## While the carry is on

Watch three things, roughly in order of how fast they change:

- **Range.** A staked position that drifts out of range earns nothing while the debt keeps accruing interest. The carry flips negative automatically, with no price crash and no rate spike required. This is the most common way the trade quietly dies.
- **The weekly epoch.** Emissions are re-voted every week, and the rewards APR moves with the vote and with the AERO price. The income leg you entered with is not the income leg you hold.
- **Loan health.** Interest compounds into the debt continuously; the collateral side moves with the pool. The [liquidation](../revert-lend/liquidations.md) penalty runs 2% to 10% of the debt, which prices exactly what inattention costs here.

Auto-compounding the AERO back into the position grows your collateral, which widens your liquidation distance over time: the carry partially defends itself if you let it.

## Unwind triggers

Decide these before entering, not during the event:

- **Carry compression.** Borrow rate up, rewards APR down, or AERO weakness: when the spread no longer pays for the liquidation risk you are warehousing, the trade is over even if nothing has gone wrong yet.
- **Range break you do not expect to mean-revert.** Out of range, the position is a non-earning asset securing an interest-bearing debt. Either move the range or close the loop.
- **Loan health approaching your floor.** Repay partially from the position itself if needed: see [Repaying](../revert-lend/repaying.md). Your floor should be a number you wrote down on day one.

The honest summary: this trade pays you a floating spread for warehousing liquidation risk and AERO price risk. Run it when both legs are visible to you and the exit rules are pre-committed; skip it when you would be checking the position page once a week and hoping.
