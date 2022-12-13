# Transfers

This article explains how to make transfers in trustless ethereum bridge and watch on transfer progress

### Sora → Ethereum <a href="#sora-ethereum" id="sora-ethereum"></a>

We have 2 bridge pallets for different asset kinds: **ethApp** for native Ethereum tokens and **erc20App** for ERC20 contracts(both native and external). To transfer tokens to Ethereum you need to call **ethApp.burn(networkId, recipient, amount)** or **erc20App.burn(networkId, recipient, amount).** Also now available **evmBridgeProxy.burn(networkId, assetId, recipient, amount)**, which is support all asset kinds

**networkId** (U256) - chainId of selected Ethereum network

**assetId** (AssetId) - asset id

**recipient** (H160) - ethereum address

**amount** (Balance) - amount of tokens to transfer

#### Watching progress <a href="#watching-progress" id="watching-progress"></a>

**Progress:**

1. Message in queue… After **burn** transaction is placed in queue (**incentivizedOutboundChannel.messageQueues(networkId)**) and **MessageAccepted(nonce)** event is created
2. Update state on Ethereum side (1/2)… **newSignatureCommitment** function is called in **BeefyLightClient** on Ethereum side by relayer
3. Update state on Ethereum side (2/2)… **completeSignatureCommitment** function is called in **BeefyLightClient** on Ethereum side by relayer
4. Submitting messages… **incentivizedInboundChannel.submit** is called on Ethereum side by relayer

### &#x20;Ethereum → Sora <a href="#ethereum-sora" id="ethereum-sora"></a>

User need to call one of those functions to transfer tokens from Ethereum to Sora:

1. **ethApp.lock(bytes32 recipient)** - should be used for native Ethereum tokens. Amount is passed as msg.value of transaction.
2. **erc20App.lock(address token, bytes32 recipient, uint256 amount)** - should be used for external (created by another companies and users) ErC20 tokens.
3. **sidechainApp.lock(address token, bytes32 recipient, uint256 amount)** - should be used for tokens which is native for Sora network (PSWAP, VAL, XOR, CERES)

**recipient** - address in Sora network

**token** - address of token to be transferred. Bridge contract should have enough allowance

**amount** - amount of tokens

#### Watching progress <a href="#watching-progress.1" id="watching-progress.1"></a>

As in previous bridge implementation we need to wait 30 blocks until transaction can be included in Sora network. **ethereumLightClient.finalizedBlock** storage contains latest block which is considered as finalized in Ethereum light client. When block with transfer transaction is finalized, relayer can import transaction with **incentivizedInboundChannel.submit** extrinsic and tokens will be minted/unlocked on Sora side.

**Progress:**

1. Waiting for block finalization (1..30/30)…
2. Waiting for transaction submit…

### Get info about bridge <a href="#get-info-about-bridge" id="get-info-about-bridge"></a>

**1. token address by asset id**

erc20App.tokenAddresses(networkId, assetId)

ethApp.addresses(networkId) - first value of tuple is token address

**2. asset id by token address**

erc20App.assetsByAddresses(networkId, address)

ethApp.addresses(networkId) - second value of tuple is asset id

**3. transaction history by user**

evmBridgeProxy.userTransactions(network\_id, account\_id) - get list of transaction hashes made by given user

evmBridgeProxy.transactions(network\_id, hash) - get transaction details by hash

### Links <a href="#links" id="links"></a>

**Substrate extrinsics**

[erc20App.burn](https://github.com/soramitsu/sora2-substrate/blob/7589b1457631a0734f98791be8ebc7c6853a254d/pallets/trustless-eth-bridge/erc20-app/src/lib.rs#L239)

[ethApp.burn](https://github.com/soramitsu/sora2-substrate/blob/7589b1457631a0734f98791be8ebc7c6853a254d/pallets/trustless-eth-bridge/eth-app/src/lib.rs#L145)

**Ethereum contract functions**

[erc20App.lock](https://github.com/soramitsu/sora2-substrate/blob/7589b1457631a0734f98791be8ebc7c6853a254d/ethereum-bridge-contracts/contracts/ERC20App.sol#L66)

[ethApp.lock](https://github.com/soramitsu/sora2-substrate/blob/7589b1457631a0734f98791be8ebc7c6853a254d/ethereum-bridge-contracts/contracts/ETHApp.sol#L54)

[sidechainApp.lock](https://github.com/soramitsu/sora2-substrate/blob/7589b1457631a0734f98791be8ebc7c6853a254d/ethereum-bridge-contracts/contracts/SidechainApp.sol#L67)

**Contracts ABI**

{% embed url="https://github.com/sora-xor/sora2-network/tree/115bc84a4620a4a2be8a001fcf912d355728c9c2/relayer/ethereum-gen/src/bytes" %}
