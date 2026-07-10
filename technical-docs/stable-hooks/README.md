# Stable Hooks

Stable Hooks is Revert's StableSwap AMM for Uniswap v4. Each deployment is a single hook contract that replaces v4's constant-product pricing with a Curve-style StableSwap invariant for a fixed set of 2 to 4 correlated assets (stablecoins, liquid-staking tokens, wrapped assets).

Source: [github.com/revert-finance/stableswap-hooks](https://github.com/revert-finance/stableswap-hooks) (BUSL-1.1).

## Architecture

One `StableSwapHooks` contract is, at the same time:

* **The AMM.** It overrides `beforeSwap` with `beforeSwapReturnDelta`, computes swap amounts with StableSwap math, and settles against its own reserves. The v4 core pool never executes any swap math.
* **The liquidity token.** The hook itself is an ERC-20. Deposits and withdrawals are proportional across all pool assets; there are no ranges, ticks, or position NFTs.
* **The fee accountant.** The LP fee is fixed at deployment and encoded in `PoolKey.fee`. Hook and protocol fees are carved out of the gross LP fee and accrue inside the contract until withdrawn to fixed collector addresses.

At deployment the hook initializes **every pairwise v4 pool** for its currency set: a 4-asset hook registers 6 pairwise pools, all drawing on one shared set of reserves. Reserves are held as ERC-6909 claims on the `PoolManager`.

Key parameters:

| Parameter | Where | Notes |
| --- | --- | --- |
| Currencies | `currencies(i)`, `currenciesLength()` | 2 to 4, sorted ascending by address. Native ETH supported as `address(0)`. |
| LP fee | `lpFeePercentage()`, also `PoolKey.fee` | Scaled by `FEE_PRECISION = 1e6` (e.g. `500` = 0.05%). Immutable per hook. |
| Hook / protocol fee | `hookFeePercentage()`, `protocolFeePercentage()` | Percentages of the gross LP fee, set by the factory owner. |
| Amplification | `getCurrentAmp()` | Higher A prices tighter around the reference ratio. Changed only by gradual ramping (`AmpRampStarted` / `AmpRampStopped` events). |
| Rate oracles | `rateOracles(i)` | Optional per-asset on-chain redemption-rate reads (e.g. wstETH `stEthPerToken`) so yield-bearing assets are priced at their true ratio. Zero config for plain 1:1 assets. |
| Tick spacing | `TICK_SPACING()` | Always `1`. Required in the `PoolKey`, otherwise unused. |

## Pool deployment

Pools are deployed permissionlessly through `StableSwapHooksFactory.deploy(...)`. The factory validates the creation bytecode against a stored hash and deploys via CREATE2; a valid hook address requires off-chain salt mining (see `script/hookMiner.demo.js` in the repo). Every deployment emits `StableSwapHooksDeployed(sender, hook)`.

## Liquidity

* `quoteAddLiquidity(amounts)` returns expected shares and the actual amounts a proportional deposit will consume; pass minimums into `addLiquidity(amounts, minAmounts, minShares)`.
* `quoteRemoveLiquidity(shares)` previews proportional withdrawal amounts for `removeLiquidity(shares, minAmounts)`.
* The first deposit permanently locks `MINIMUM_LIQUIDITY` to a dead address.
* Net LP fees stay in reserves, so fees compound into the value of every LP share automatically. There is no claim step.

## Security

The contracts were independently audited by PeckShield and went through a public audit competition on Cantina.

## For integrators

If you route or aggregate swaps, see [Integrating swaps](integrating-swaps.md). The short version: pools are quoted and executed through the standard v4 stack (Quoter, Universal Router), but all pricing state lives in the hook, not in the core pool's slot0 or tick data.
