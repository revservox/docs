---
description: This applies to the now deprecated v1 auto-compounder
---

# Auto-compounder v1 FAQ

### Why should I use auto-compounding if I can do it manually?

The process of collecting fees, swapping them into the required ratio, and adding liquidity to a position requires separate contract interactions and is cumbersome to do manually. From a gas cost perspective, it is best to have some form of automation that bundles all the required actions into one transaction. For high fee APR positions, the optimal number of compounds can be several times a day.

Gas price fluctuates and the Compoundor protocol will incentivize auto-compounding of positions when gas prices are low.

Uncollected fees do not grow at a constant rate, so compounding manually at the optimal moments would require constant monitoring of the fee growths.

Peace of mind.

### What are the costs?

Two percent of the compounded fees. This amount is modifiable by the contract deployer (Revert), but can only be decreased and never increased.

### What modifiable parameters does the Compoundor protocol have?

* **totalRewardX64: T**otal reward paid to the protocol, including the compounder reward. This value starts at 2% (of the compounded fees) and can only be reduced, never increased.
* **compounderRewardX64:** Reward paid to compounder. Must always be less than **totalRewardX64.**&#x20;
* **maxTWAPTickDifference:** max amount of ticks the current tick may differ from the 60s Oracle TWAP tick to allow swaps. A sanity check to provide price manipulation protection.
*   _**TWAPSeconds**_: How many seconds should be used to calculate TWAP.



### What are the risks?

When you activate auto-compounding for a position you transfer it to the Compoundor contract. You are able to withdraw your position at any time, but you are subject to the following risks while your position is owned by the contract.

* There is smart-contract risk in the Compoundor protocol.
* Compounding fees will often require swapping some amount of the uncollected fees so that they are at ratio that maximizes the amount of new liquidity added for each position. The PNL for these swaps will depend on what happens with the asset pair prices, they can be negative, and the extra fees accrued from auto-compounding might not make up for that loss.

### Will my position be constantly auto-compounding

The way the Compoundor contract is implemented, there is an incentive for auto-compounding positions which have accumulated enough fees to pay for the gas cost. Anyone can trigger the auto-compounding function.

Additionally Revert is maintaining its own auto-compounding bot to ensure that positions are auto-compounding as frequently as possible.

### Wen token?

There are no plans for any token.

### How to manually withdraw my position from the Auto-compounder?&#x20;

A position in the auto-compounder contract is withdrawable by the owner at any time and can do so by interacting directly with the smart contract.\
Please follow the next steps to manually withdraw your position from the auto-compounder contract, in case our front-end is unavailable.

1. Visit the contract page for the chain block scanner where the position is located.&#x20;
   1. Block scanners: [Optimism](https://optimistic.etherscan.io/address/0x5411894842e610c4d0f6ed4c232da689400f94a1#writeContract), [Arbitrum](https://arbiscan.io/address/0x5411894842e610C4D0F6Ed4C232DA689400f94A1#writeContract), [Polygon](https://polygonscan.com/address/0x5411894842e610C4D0F6Ed4C232DA689400f94A1#writeContract), [BNB Chain](https://bscscan.com/address/0x98eC492942090364AC0736Ef1A741AE6C92ec790), [Base](https://basescan.org/address/0x4a8c2bdf0d8d2473b985f869815d9caa36a57ee4#writeContract), or [Mainnet](https://etherscan.io/address/0x5411894842e610C4D0F6Ed4C232DA689400f94A1#writeContract).
2.  Connect your wallet.<br>

    <figure><img src="../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>
3. Select the "WithdrawToken" function and fill out the form.&#x20;

<figure><img src="../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

*   **tokenId:** Is the NFT id of the position.&#x20;

    *   You can find it in Revert's UI.

        <figure><img src="../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>



    * Alternatively, use the "accountTokens" function from the "Read Contract" tab, in the block scanner (step 1).&#x20;
      * Insert the position owner address in the first input field and start looking for your positions by entering the number 0 in the second field and clicking on "Query".&#x20;
        *   (In case of having more than one position keep increasing the number until finding all the required IDs.)&#x20;

            <figure><img src="../.gitbook/assets/image (81).png" alt=""><figcaption></figcaption></figure>
* **to(address):** Is the destination address where your position is going to be transferred.

{% hint style="warning" %}
Be extra careful when filling out the "address" field. Once the position leaves the Auto-compounder contract is not on Revert's control anymore.
{% endhint %}

* **withdrawBalances:** Enter the word "true".
* **data:** Complete the field with "0x".

4\. Click on "Write" and sign the transaction on your wallet.&#x20;

By the end of this process, the position will be transferred outside the contract.&#x20;



### Why has my position not been compounded yet?

Compounding occurs when the unclaimed fees are more than 100x the gas cost of compounding, which varies by network and gas price. The compoundor [whitepaper](https://hackmd.io/@revert/BJcGIJQ35) explains the way it works:

We can estimate the costs of compounding fees using the auto-compounder on Mainnet (25 Gwei), Polygon (50 Gwei), Optimism (0.25 Gwei), BNB Chain (5 Gwei), and Arbitrum (0.2 Gwei). Therefore, assuming an ETH price of $1000, a MATIC price of $0.5 and a BNB price of $300, we can estimate the gas costs for compounding a position using the Compoundor contract on the same chains as shown below.

<table data-header-hidden><thead><tr><th width="136"></th><th width="100"></th><th width="95"></th><th width="106"></th><th width="103"></th><th></th><th></th></tr></thead><tbody><tr><td>Function</td><td>Gas cost</td><td>Mainnet</td><td>Optimism</td><td>Arbitrum</td><td>Polygon</td><td>BNB Chain</td></tr><tr><td>Auto-Compound</td><td>479,521</td><td>$11.99</td><td>$0.12</td><td>$0.10</td><td>$0.01</td><td>$0.72</td></tr></tbody></table>

For Optimism and Arbitrum, we used estimated Gwei amounts to avoid doing the L2 gas price calculation.\
\
For instance, given the above estimations, an Optimism position should have accrued at least a total of $12 worth of fees ($0.12\*100) to compound automatically.
