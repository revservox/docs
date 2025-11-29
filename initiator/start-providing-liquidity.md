# Start providing liquidity

The initiator works like a 4 step wizard that enables users to select each of the important parameters and understand how the proposed setup would have performed in a given time-frame. Finally it allows users to initiate the position given their selection and start providing liquidity.

![Selecting pair and fee tier](<../.gitbook/assets/image (10).png>)

#### select pair&#x20;

After selecting the network and protocol, the first step is to choose a pair of tokens which define the pool where you want to add liquidity.

#### select fee tier

Uniswap v3 allows pools to be created with different fee tiers. Users must select a fee tier at this point, though once the rest of the parameters have been selected, they can come back and quickly switch between the different fee tiers to see the effects on the backtesting simulation.

![Price range selection and amount input](<../.gitbook/assets/image (29).png>)

#### select price ranges

Use the price inputs to enter the minimum and maximum range you want to provide liquidity for. Updating the values will immediately update the charts to give you an idea how the historic price action, and current liquidity, look in the context of your selected range.

#### amounts to deposit

In this step the user is required to input the amount of assets they want to provide liquidity with. Having previously selected the price range, the initiator will calculate the corresponding amount of the other token that must be deposited.&#x20;

![](<../.gitbook/assets/image (17).png>)

#### run backtester

Running the backtester having selected a position's parameters gives a user an idea how that position would have performed over the last 30 days. By default, the position performance is against HODL (holding both assets outside of the pool), but the backtester also offers the possibility to compare the position against holding either of the assets instead of the pair. So a user can, for example, compare the performance of a positions against holding only ETH.

{% hint style="info" %}
**Fee dilution** refers to the dilution effect of adding more capital to a pool (assuming volume had remained constant). e.g., adding 10M to a 5M pool might reduce APR considerably more than adding 50k.
{% endhint %}

**Initiating**

After approving permissions to tokens, if required, click o the green **"Initiatie position"** button to initiate the position and start providing liquidity.

The initiator works directly with the Uniswap v3 contracts, so initiating a position will result in an NFT in your wallet, exactly like it would if using the Uniswap UI directly.<br>
