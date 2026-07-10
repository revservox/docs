# Integrating swaps

This page is for aggregators, solvers, and routers that want to source liquidity from Stable Hooks pools. It covers pool discovery, quoting, execution, indexing, and the ways these pools differ from vanilla v4 pools.

**TL;DR:** integration is standard Uniswap v4. Build the `PoolKey`, quote with the v4 `Quoter`, execute through the Universal Router with empty `hookData`. The one thing you must not do is price these pools from core pool state: `slot0` and tick data are meaningless here (see [What not to do](#what-not-to-do)).

## Pool discovery

1. Watch the factory for deployments:

```solidity
event StableSwapHooksDeployed(address indexed _sender, address indexed _hook);
```

2. For each hook, enumerate its assets and parameters:

```solidity
uint256 n = hook.currenciesLength();          // 2 to 4
Currency c = hook.currencies(i);              // sorted ascending; address(0) = native ETH
uint256 lpFee = hook.lpFeePercentage();       // scaled by 1e6; also the PoolKey.fee value
int24 spacing = hook.TICK_SPACING();          // always 1
```

3. A hook with `n` assets registers all `n * (n - 1) / 2` pairwise pools at deployment. Every pair is a routable pool; all pairs of one hook draw on the same shared reserves. You can verify a candidate pool id with `hook.isValidPoolId(poolId)`.

The `PoolKey` for any pair (with `currency0 < currency1`):

```solidity
PoolKey memory poolKey = PoolKey({
    currency0: currency0,
    currency1: currency1,
    fee: uint24(hook.lpFeePercentage()),
    tickSpacing: hook.TICK_SPACING(),
    hooks: IHooks(address(hook))
});
```

## Quoting

### On-chain: v4 Quoter

The standard v4 `Quoter` simulates the full swap including the hook, so it returns correct amounts with no special handling:

```solidity
(uint256 amountOut,) = quoter.quoteExactInputSingle(
    IV4Quoter.QuoteExactSingleParams({
        poolKey: poolKey,
        zeroForOne: true,
        exactAmount: uint128(amountIn),
        hookData: bytes("")
    })
);
// quoteExactOutputSingle works the same way for exact-output amounts.
```

### Off-chain: replicating the math

For indicative pricing without RPC simulation, replicate the hook's math from four reads:

1. **Reserves:** `hook.reserves(i)` for each currency index.
2. **Amplification:** `hook.getCurrentAmp()` (interpolates during ramps).
3. **Rates:** each reserve is scaled by a per-currency rate before the invariant math. The static rate is `10^(36 - decimals)` (native ETH counts as 18 decimals). If `hook.rateOracles(i)` has a non-zero oracle, the effective rate is `staticRate * fetchedRate / 1e18`, where `fetchedRate` is a `staticcall` to the configured selector (e.g. wstETH's `stEthPerToken()`). See `Base._getRate` and `StableSwapMath.scaleTo` in the repo.
4. **Fees:** for exact input, compute the raw StableSwap output first, then deduct the gross LP fee from the output: `fee = ceil(rawAmountOut * lpFeePercentage / 1e6)`, `amountOut = rawAmountOut - fee`. For exact output, the fee is added to the input instead. The hook/protocol split within the LP fee does not affect trader amounts.

The invariant and target-reserve computation are in `src/libraries/StableSwapMath.sol` (`getInvariant`, `getTargetReserves`); the swap flow that composes them is `src/Swap.sol`. Cache invalidation: reserves change on every swap and liquidity event (see [Indexing](#indexing)); amp changes only during announced ramps; oracle rates drift slowly (staking yield).

## Execution

Swaps route through the Universal Router with the ordinary v4 action encoding:

```solidity
bytes memory actions = abi.encodePacked(
    uint8(Actions.SWAP_EXACT_IN_SINGLE), uint8(Actions.SETTLE_ALL), uint8(Actions.TAKE_ALL));

bytes[] memory params = new bytes[](3);
params[0] = abi.encode(IV4Router.ExactInputSingleParams({
    poolKey: poolKey,
    zeroForOne: true,
    amountIn: uint128(amountIn),
    amountOutMinimum: amountOutMin,   // slippage protection
    hookData: bytes("")
}));
params[1] = abi.encode(poolKey.currency0, amountIn);  // SETTLE_ALL
params[2] = abi.encode(poolKey.currency1, 0);         // TAKE_ALL

bytes memory commands = abi.encodePacked(uint8(Commands.V4_SWAP));
bytes[] memory inputs = new bytes[](1);
inputs[0] = abi.encode(actions, params);
universalRouter.execute(commands, inputs, deadline);
```

Notes:

* Exact output uses `SWAP_EXACT_OUT_SINGLE` with `amountInMaximum`.
* Native ETH: pass value with the call; for exact-output swaps send `amountInMaximum` and append a `Commands.SWEEP` to recover the unused remainder.
* `hookData` is always empty. The hook takes no per-swap parameters.
* Slippage is enforced by the router's `amountOutMinimum` / `amountInMaximum`, exactly as for any v4 pool.

## What not to do

These pools are custom-curve pools. The v4 core pool exists only as a settlement shell:

* **Do not price from `slot0`.** Every pairwise pool is initialized at `sqrtPriceX96 = 1 << 96` (a 1:1 price) and never moves, because the hook consumes 100% of `amountSpecified` in `beforeSwap` (via `beforeSwapReturnDelta`) and core swap math runs on zero.
* **Do not read tick data or core liquidity.** Native liquidity positions are blocked (`beforeAddLiquidity` / `beforeRemoveLiquidity` revert), so in-range liquidity is always zero. Depth lives in `hook.reserves(i)`.
* **Do not apply core LP-fee math.** The fee in `PoolKey.fee` is charged by the hook's own math as described above, not by the core fee mechanism.
* **Do not assume pairwise independence for large flows.** All pairs of one hook share reserves, so a large swap on one pair shifts quotes on every other pair of the same hook.

## Indexing

Emitted by the hook:

```solidity
event StableSwap(
    address indexed _sender,
    Currency indexed _currencyIn,
    Currency indexed _currencyOut,
    uint256 _amountIn,
    uint256 _amountOut,
    uint256 _lpFees,
    uint256 _hookFees,
    uint256 _protocolFees
);

event LiquidityAdded(address indexed _sender, uint256[] _amounts, uint256 _shares);
event LiquidityRemoved(address indexed _sender, uint256[] _amounts, uint256 _shares);
event AmpRampStarted(
    address indexed _sender, uint256 _currentAmp, uint256 _nextAmp, uint256 _currentTime, uint256 _nextAmpTime
);
event AmpRampStopped(address indexed _sender, uint256 _currentAmp, uint256 _currentTime);
```

`StableSwap` fires on every swap with the full fee breakdown, so volume and fee analytics need no core-pool event parsing. Reserve state can always be re-read from `hook.reserves(i)`.

## Deployments

Launch deployments and addresses will be listed on the [Contract Addresses](../../resources/contract-addresses.md) page when live. For integration questions or early access to deployment details, reach out on [Discord](https://discord.gg/HXfxKHrRmf).

## Security

The contracts were independently audited by PeckShield and went through a public audit competition on Cantina. Source and tests: [github.com/revert-finance/stableswap-hooks](https://github.com/revert-finance/stableswap-hooks).
