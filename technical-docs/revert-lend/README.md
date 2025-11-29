# Revert Lend

Revert Lend is a decentralized peer-to-pool lending protocol designed for Automated Market Maker Liquidity Providers. It allows users to collateralize their Uniswap v3 liquidity provider positions, in the form of the Uniswap NFTManager NFTs, and obtain loans in a protocol-determined ERC-20 token. The protocol is specifically designed to allow Liquidity Providers to maintain control over the capital in their positions while they are collateralized. This feature facilitates uninterrupted management and optimization of LP positions, catering to the dynamic needs of liquidity providers.

### Main Contracts

#### V3Vault

The `V3Vault` contract allows users to deposit a specific ERC20 token (e.g., USDC) to earn interest or borrow against their LP positions. The contract manages collateral LP positions, calculates interest rates, and handles liquidations to ensure the safety and liquidity of the lending pool.

#### V3Oracle

The `V3Oracle` contract is designed to calculate the value of Uniswap V3 LP positions for use in the `V3Vault`. It integrates both Chainlink price feeds and Uniswap V3 Time-Weighted Average Price (TWAP) oracles, providing a fallback mechanism in case one fails. The contract ensures accurate and reliable pricing by cross-verifying between the oracles and can operate in various modes depending on the situation. This setup enhances the security and reliability of the `V3Vault` by preventing manipulation and ensuring that collateral values are accurate and up-to-date.

#### InterestRateModel

The `InterestRateModel` contract is used in a vault to calculate both borrow and supply interest rates based on the utilization of available liquidity. It dynamically adjusts the rates using a base rate, a multiplier for utilization below a specified "kink" level, and a jump multiplier for utilization above the kink. This allows the vault to effectively manage interest rates, ensuring stability and incentivizing appropriate borrowing and lending behavior. The model is customizable, allowing the owner to update parameters to adapt to changing market conditions.

### V3Vault functions

These external functions are&#x20;

* **`deposit(uint256 assets, address receiver)` & `mint(uint256 shares, address receiver)`**
  * Allows users to deposit assets into the vault or mint new shares, with the possibility of using permit2 for signature-based approval.
* **`withdraw(uint256 assets, address receiver, address owner)` & `redeem(uint256 shares, address receiver, address owner)`**
  * Allows users to withdraw assets or redeem shares from the vault.
* **`create(uint256 tokenId, address recipient)` & `createWithPermit(uint256 tokenId, address recipient, uint256 deadline, uint8 v, bytes32 r, bytes32 s)`**
  * Enables users to create new collateralized positions by transferring a Uniswap V3 NFT to the vault, with or without permit-based approval.
* **`onERC721Received(address, address from, uint256 tokenId, bytes calldata data)`**
  * Handles the receipt of Uniswap V3 NFTs, creating or modifying a loan.
* **`approveTransform(uint256 tokenId, address target, bool isActive)`**
  * Allows an address to transform a loan on behalf of the owner (this is used when using Auto-Range or Auto-Compound funcionality)
* **`transform(uint256 tokenId, address transformer, bytes calldata data)`**
  * Allows a whitelisted transformer contract to modify a loan.
* **`borrow(uint256 tokenId, uint256 assets)`**
  * Allows users to borrow assets against their collateralized Uniswap V3 position.
* **`decreaseLiquidityAndCollect(DecreaseLiquidityAndCollectParams calldata params)`**
  * Decreases the liquidity of a Uniswap V3 position and collects the resultant assets, while ensuring the loan remains healthy.
* **`repay(uint256 tokenId, uint256 amount, bool isShare)` & `repay(uint256 tokenId, uint256 amount, bool isShare, bytes calldata permitData)`**
  * Allows users to repay their loans, either by specifying assets or debt shares, with an option for permit-based approval.
* **`liquidate(LiquidateParams calldata params)`**
  * Liquidates a loan that has become under-collateralized, transferring the collateral to the liquidator and handling any shortfall with reserves.
* **`remove(uint256 tokenId, address recipient, bytes calldata data)`**
  * Removes a fully repaid collateral position from the vault.

### Additional contracts

#### LeverageTransformer

The `LeverageTransformer` contract is designed to provide leverage and deleverage functionalities for positions held in the `V3Vault`. It allows users to borrow additional funds, swap them for the underlying assets of a Uniswap V3 position, and add liquidity in a single transaction, effectively leveraging their position. Conversely, it also enables users to reduce leverage by removing liquidity, swapping the underlying assets back to the borrowed asset, and repaying the loan. This contract integrates tightly with the `V3Vault`, making it easier for users to manage leveraged positions efficiently and securely in a single transaction.

#### FlashloanLiquidator

The `FlashloanLiquidator` contract facilitates the atomic liquidation of under-collateralized loans within the `V3Vault` using a Uniswap V3 flash loan. It allows a liquidator to borrow the necessary funds instantly, liquidate a position, and then repay the flash loan within a single transaction. The contract also supports swapping collateral tokens back to the asset used for liquidation, ensuring the liquidator receives a reward. This process ensures that liquidations are efficient, secure, and require minimal upfront capital from the liquidator.

