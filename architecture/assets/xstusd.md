---
description: XOR Synthetic USD
---

# XSTUSD

XSTUSD is a XOR synthetic stablecoin linked to the price of USD, as determined by the XOR-DAI exchange rate on the Polkaswap DEX. It is a synthetic stablecoin, meaning it is backed by minting/burning of XOR tokens. A good high level overview can be found in this [Forbes article](https://www.forbes.com/sites/tatianakoffman/2021/11/23/the-rise-of-decentralized-money-on-polkadotnew-algorithmic-stablecoin-launches-on-sora/?sh=7341b64131bc) or this [blog post](https://medium.com/@polkaswapcommunitycollective/xst-synthetic-assets-and-the-launch-of-xstusd-fee262c63acd).

#### XOR-DAI Exchange Rate

XSTUSD is pegged to the XOR-DAI exchange rate on Polkaswap. The XOR-DAI exchange rate is calculated by calculating a moving average of the XOR-DAI price on Polkaswap over 30 blocks. To prevent manipulative attacks, the average is has a maximum rate of change per block of 0.197% upwards and 0.007% downwards. The entire calculation is done on-chain, without the use of centralized middleware or oracles.

Practically, if someone were to crash the XOR-DAI price in order to manipulate the XOR-DAI rate, then the price will go down slowly over around 40 minutes\~1 hour (depending on the % change), which gives others ample time to move DAI across the HASHI bridge to do arbitrage on the difference in XOR price on Polkswap with other exchanges, as well as to get a good deal.

#### Combining XST and XYK Liquidity

XSTUSD is implemented as an additional liquidity source in Polkaswap called XST. It is used by the SMART matching algorithm to automatically combine with liquidity in the XOR-XSTUSD XYK pool, returning the best price to the user who swaps to or from XSTUSD and XOR.
