# Configuration parameters

The initial configuration of Revert Lend supported tokens and parameters was defined by using the risk framework from [Anthias](https://www.anthias.xyz/) described in detail in this document (TODO link).

### Supported Chains and Tokens

Currently Revert Lend is available on `Arbitrum`.&#x20;

The lend token is `USDC`

The supported collateral tokens are: `USDC, USDC.e, USDT, DAI, WETH, WBTC, ARB, wstETH`.&#x20;

### Collateral factors

To decide the collateral factor of a LP position, the lower collateral factor of the two tokens is applied.

<table><thead><tr><th width="191">Token</th><th>Collateral factor</th></tr></thead><tbody><tr><td><code>USDC</code></td><td>85.0%</td></tr><tr><td><code>USDC.e</code></td><td>85.0%</td></tr><tr><td><code>USDT</code></td><td>85.0%</td></tr><tr><td><code>DAI</code></td><td>85.0%</td></tr><tr><td><code>WETH</code></td><td>77.5%</td></tr><tr><td><code>WBTC</code></td><td>77.5%</td></tr><tr><td><code>ARB</code></td><td>60%</td></tr><tr><td><code>wstETH</code></td><td>72.5%</td></tr></tbody></table>







