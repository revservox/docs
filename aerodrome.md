# Aerodrome Support

## Overview

Revert provides full support for Aerodrome concentrated liquidity (CL) positions on Base. Aerodrome is the leading DEX on Base, and its CL positions work similarly to Uniswap v3 positions but include additional gauge staking functionality for earning AERO token rewards.

For more information about Aerodrome, gauges, and veAERO, see the [official Aerodrome documentation](https://aerodrome.finance/docs).

## What are Aerodrome CL Positions?

Aerodrome CL positions are concentrated liquidity positions that allow you to provide liquidity within a specific price range, just like Uniswap v3. However, Aerodrome positions can also be staked in gauges to earn AERO rewards on top of trading fees.

## Gauge Manager (Revert-Staker)

The Gauge Manager is Revert's wrapper around Aerodrome's native gauge system. It enables all Revert features for your Aerodrome positions while maintaining gauge staking for AERO rewards.

### Why Use the Gauge Manager?

Staking your Aerodrome position via the Gauge Manager provides several benefits compared to staking directly with Aerodrome:

- **Access to Revert Lend**: Use your position as collateral for borrowing and leverage
- **AERO Autocompounding**: Automatically convert AERO rewards into additional liquidity
- **Auto-Compound Trading Fees**: Reinvest earned trading fees back into your position
- **Unified Management**: Manage staking, rewards, and position operations from a single interface

### Staking Workflow

To use Revert features with your Aerodrome position:

1. **Approve the Gauge Manager**: Grant permission for the Gauge Manager to manage your position NFT
2. **Stake Your Position**: Deposit your position into the gauge via the Gauge Manager
3. **Start Earning**: Your position now earns AERO rewards from the gauge
4. **Access Revert Features**: Use Revert Lend, autocompounding, and other features

### Unstaking

To unstake your position and return the NFT to your wallet:

1. Navigate to your position in the Revert interface
2. Select the unstake option
3. Confirm the transaction

Note: Some operations require unstaking first. The interface will guide you when this is necessary.

## AERO Rewards

### How Rewards Accrue

When your position is staked via the Gauge Manager, it earns AERO rewards based on:
- The amount of liquidity you provide
- The gauge's reward rate (determined by veAERO voting)
- How long your position has been staked

### Claiming Rewards

You can claim your earned AERO rewards at any time:
- **Manual Claim**: Withdraw AERO to your wallet
- **Autocompound**: Automatically swap AERO and add as liquidity to your position

### Enabling Autocompounding

To enable AERO autocompounding:

1. Navigate to your staked Aerodrome position
2. Enable the autocompound feature
3. The system will automatically compound your AERO rewards when optimal

See the [Auto-Compounder](auto-compounder/README.md) documentation for more details on how autocompounding works.

## Using Aerodrome Positions with Revert Lend

Staked Aerodrome positions can be used as collateral in Revert Lend:

- **Borrowing**: Use your position as collateral to borrow tokens - see [Borrowing](revert-lend/borrowing.md)
- **Leverage**: Amplify your position and earn more fees and AERO rewards - see [Leverage](revert-lend/leverage.md)
- **Continuous Rewards**: AERO rewards continue accruing even when your position is used as collateral

## Terminology

| Term | Definition |
|------|------------|
| Gauge Manager | The smart contract that manages staking in Aerodrome gauges for Revert |
| Revert-Staker | Alternative name for the Gauge Manager |
| AERO rewards | Token rewards earned from staking in Aerodrome gauges |
| AERO autocompounding | Automatically converting AERO rewards into LP liquidity |
| Fee compounding | Automatically reinvesting trading fees (distinct from AERO rewards) |
| CL positions | Concentrated liquidity positions on Aerodrome |
