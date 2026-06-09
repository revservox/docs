# Auto-compounder

## The basics

LP positions in Uniswap V3 earn fees while swaps happen within their selected price ranges. However, these fees do not accumulate inside the pool, but in a separate balance for each position. One consequence of this is that fees are not compounded automatically as liquidity back into the position.&#x20;

If a liquidity provider wants to compound accrued fees back into their position, they need to collect these fees, possibly swap them to the correct ratio given the position range and current pool tick, and add these possibly swapped amounts back into the position.

The Revert auto-compounder allows LPs to automate the compounding of the accrued fees in exchange for a fixed percentage of the compounded fees. This serves to incentivize a maximum number of compounds at optimal times with regards to gas costs.

Depending on the fee APR and size of your position this can significantly improve your returns.

![](<../.gitbook/assets/Group 260 (1).png>)

Auto-compounding functionality is provided by the Revert Compoundor protocol. \
\
Positions managed by the Compoundor contract can be auto-compounded at any time by the operator account. The _**autoCompound**_ function takes any uncollected fees for a position, optionally swaps them to a determined ratio given the position range and the current pool price, and adds it as liquidity to the position.

A small fraction of the _collected-and-compounded_ fees are paid to the protocol and to compensate the accounts call the auto-compound function for their gas costs incurred. This performance fee is set to 2%.

**Aerodrome AERO rewards**

On Aerodrome positions on Base, auto-compounding reinvests the position's emitted **AERO rewards** rather than swap fees. The mechanics and fees differ slightly, see [AERO auto-compounding](../aerodrome/aero-auto-compounding.md).

**Rebasing tokens support**

The protocol is not intended to work with any kind of deflationary, rebasing, fee-on-transfer, or any non-standard erc20 behavior tokens.
