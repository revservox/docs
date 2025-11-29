# User Guide

### Check your position

For any tracked Uniswap v3 position, click on the **'Compound fees'** button to see estimations of auto-compounding profits and decide if you want to auto-compound a position, depending on the possible improvement over different periods, up to a year, and your expected time preference.

![](<../.gitbook/assets/Group 260 (1).png>)

### Activate Auto-Compounding

When an LP clicks on "**Activate Autocompound"** their wallet permissions will be prompted, asking for authorization to set the [auto-compounder contract](../resources/contract-addresses.md) as operator for the position.\
\
Once the transaction has finished successfully, the Revert auto-compounder will compound uncollected fees when it's profitable to do so given their expected rewards and gas costs as constraints.

![](<../.gitbook/assets/Group 262.png>)

### Manage position

While your position is auto-compounded, you can manage your position as you would normally, add/remove liquidity, collect fees, or manually auto-compound (self-compound).

![](<../.gitbook/assets/Group 263.png>)

### Deactivate Auto-Compounding

To deactivate the auto-compounding, LPs click on the 'Compound fees' button to expand the compounding options. \
\
Clicking the **'Stop Autocompound'** button will prompt the wallet authorization screen, and clear the auto-compounder contract as operator for the position.

![](<../.gitbook/assets/Frame 255.png>)

