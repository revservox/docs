# Compound or collect

Every fee your position earns sits in a separate balance until you do something with it. You have two options: collect it as income, or compound it back into the position as liquidity. The right answer depends on three numbers: your fee APR, your position size, and your chain's gas cost.

## What compounding buys you

Compounded fees become principal, and principal earns fees. The improvement is the difference between simple and compound growth, and it only materializes if compounding happens often, which is what the [Auto-compounder](../auto-compounder/README.md) automates: compounds fire when the pending fees justify the gas.

## The numbers

For illustration, take a $10,000 position earning a 20% fee APR ($2,000 per year in fees), with the auto-compounder's 2% performance fee, of which half goes to the executor who pays the gas. A compound fires when the executor's share of pending fees covers the gas cost:

- **On Base** (gas well under $1), compounds fire at a few dollars of pending fees: hundreds of compounds per year, effectively continuous. Projected APY is about 21.7% versus the 20% simple rate. Compounding is close to free money here.
- **On mainnet** (call it $12 of gas), a compound fires only once pending fees reach about $1,200. That is fewer than two compounds per year: APY around 20.4%. Still positive, but thin.
- **The same setup at $1,000 position size on mainnet** never compounds at all: the position earns $200 a year in fees and the trigger is $1,200. Activating the auto-compounder costs you nothing in this case (it simply never fires), but it also does nothing.

The pattern: compounding improvement scales with fee APR, position size, and cheap gas. On L2s and Base it is nearly always worth it. On mainnet, do the arithmetic above with your own numbers first; the [performance improvement](../auto-compounder/performance-improvement.md) page has the full formulas.

## When to collect instead

- **You want the income.** Compounding grows your LP exposure; collecting realizes it. If the position is your yield source rather than your growth vehicle, collect.
- **You want to cap exposure to the pair.** Compounded fees are capital newly exposed to divergence loss. If you would not add fresh money to this pool today, reconsider compounding into it either.
- **The position is about to change.** If a range move or exit is coming, there is little point compounding fees you are about to reposition anyway.

On Aerodrome the same logic applies to AERO emissions instead of swap fees, with one extra variable: compounding converts AERO into pool tokens at the current price, which also closes your exposure to AERO price moves. See [AERO auto-compounding](../aerodrome/aero-auto-compounding.md).
