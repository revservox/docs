# Lending

### Lending Tokens

When a user decides to lend tokens in the Revert Lend protocol, they deposit their assets into the lending pool, which follows the ERC-4626 Tokenized Vault Standard. Upon depositing, the lender receives rlTokens, such as rlUSDC, which represent their share of the lending pool. These rlTokens are equivalent in value to the underlying tokens at the time of deposit and serve as proof of the lender’s contribution to the pool.

<figure><img src="../.gitbook/assets/Captura de pantalla 2024-08-30 a la(s) 12.10.14 p.m..png" alt=""><figcaption></figcaption></figure>

### Accumulating Interest

As borrowers take out loans from the lending pool, they repay these loans with interest. This interest accumulates in the lending pool and increases the value of the rlTokens over time. Initially, rlTokens have a 1-to-1 exchange rate with the deposited asset, but as interest accrues, their value appreciates. This means that when the lender eventually redeems their rlTokens, they will receive more than they initially deposited, reflecting the interest earned on their lent tokens.



