# Introduction

![](.gitbook/assets/unknown.png)

Revert builds analytics and financial tools for liquidity providers in AMM protocols. A liquidity position is an investment, and we treat it like one: it deserves accounting-grade performance data, automation that executes while you sleep, and the ability to work as collateral without ceasing to earn.

AMMs are becoming a fundamental part of financial markets. That only works if the people providing the liquidity have open, transparent tools that let them see exactly what their capital is doing, which is what we build.

## What you can do with Revert

- **Know your real performance.** PnL, APR, ROI, and divergence loss for Uniswap v2, v3, and v4 positions and Aerodrome positions on Base, across Ethereum, Polygon, Arbitrum, Optimism, Base, and Unichain. Every number is computed from your position's full cash-flow history and defined precisely enough to recompute: see [How Revert measures performance](position-analytics/how-revert-measures-performance.md).
- **Manage everything in one place.** Add or withdraw liquidity, claim fees, and change ranges directly from the position page.
- **Automate the busywork.** [Auto-compound](auto-compounder/README.md) reinvests fees when it is profitable to do so, [Auto-Range](auto-range.md) keeps ranges tracking the price, and [Auto-Exit](auto-exit.md) gives a position a pre-committed way out.
- **Earn on Aerodrome.** Positions on Base are staked for you to earn AERO emissions, with [auto-compounding of rewards](aerodrome/aero-auto-compounding.md) back into the position.
- **Borrow without unwinding.** [Revert Lend](revert-lend/README.md) takes your Uniswap v3 or Aerodrome position as collateral for a USDC loan while it keeps earning.
- **Combine the tools deliberately.** The [Playbooks](playbooks/README.md) walk the decisions: when to compound versus collect, how to pick a range with evidence, and how to run a carry on staked collateral.

New to Aerodrome on Revert? Start with [Aerodrome on Base](aerodrome/README.md).
