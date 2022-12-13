# EVM

### Ethereum light client

Ethereum light client is based on a [merkle proofs of a DAG](https://github.com/tranvictor/ethashproof#explanations). Ethereum block considered as finalized after 30 confirmations

### Substrate light client

To verify messages from substrate on Ethereum side we use light client based on BEEFY. Full validation of BEEFY commitment require to send at least 2/3 of validator signatures which is require a lot of gas on Ethereum side. Instead we use small randomized subset of signatures to verify BEEFY commitment.

### Pallets

**ethereum-light-client**

Pallet used to validate and store Ethereum headers and for transaction receipts verification.

Relayer interact with this pallet via ‘import\_header’ extrinsic

**basic(incentivized)-inbound-channel**

Pallet used to send messages from Ethereum. This pallet use ethereum-light-client pallet to verify receipt

Relayer interact with this pallet via ‘submit’ extrinsic

**basic(incentivized)-outbound-channel**

Pallet used by another pallets to send messages to Ethereum. Every 10 blocks creates commitment with queued messages. Messages is saved in offchain DB, commitment hash with network id and channel id added to digest.

**dispatch**

Pallet used by inbound channels to decode and dispatch calls

**eth-app**

Pallet used to handle native Ethereum token transfers

User interact with ‘burn’ extrinsic

**erc20-app**

Pallet used to handle ERC20 tokens transfers

This pallet interact with ERC20App.sol for sidechain ERC20 tokens and with SidechainApp for tokens owned by SORA

User interact with ‘burn’ extrinsic

**migration-app**

Pallet used to migrate from old Ethereum bridge.

**leaf-provider**

This pallet provides MMR leaf extra data with hash of the digest items used by bridge

### Smart contracts

**BeefyLightClient**

Contract used to update MMR tree root and validators Merkle tree root

Relayer interact with `newSignatureCommitment` and `completeSignatureCommitment` functions

**ValidatorRegistry**

Used to functions to store and verify validators

**Basic(Incentivized)InboundChannel**

Used by relayer to submit commitments from Substrate. Verifies commitment using BeefyLightClient and dispatch calls to App contracts

**Basic(Incentivized)OutboundChannel**

Used by App contracts to send messages to Substrate. Works only with allowed contracts

**EthApp**

Handle native Ethereum token transfers

**ERC20App**

Handle common ERC20 tokens transfers

**SidechainApp**

Handle transfers with tokens owned by SORA

### **Sequence diagrams**

Substrate to Ethereum message sequence

![image](https://user-images.githubusercontent.com/20982317/184415127-19239676-3010-4313-86fe-dbae00b7e559.png)

Ethereum to Substrate message sequence

![image](https://user-images.githubusercontent.com/20982317/184415250-eb80da64-b63e-4817-828e-307cc6b0fede.png)

### References

[Beefy Docs](https://github.com/paritytech/grandpa-bridge-gadget/tree/master/docs)

[Snowbridge Docs](https://github.com/Snowfork/snowbridge/tree/main/docs)

[DAG Merkle Proof](https://github.com/tranvictor/ethashproof#explanations)

### Testnet Bridge Endpoints

* `wss://ws.framenode-1.b1.stg1.sora2.soramitsu.co.jp`
* [rpc.framenode-1.b1.stg1.sora2.soramitsu.co.jp](http://rpc.framenode-1.b1.stg1.sora2.soramitsu.co.jp/)
* [Polkadot.js/apps framenode-1](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fws.framenode-1.b1.stg1.sora2.soramitsu.co.jp#/explorer)
* `wss://ws.framenode-2.b1.stg1.sora2.soramitsu.co.jp`
* [rpc.framenode-2.b1.stg1.sora2.soramitsu.co.jp](http://rpc.framenode-2.b1.stg1.sora2.soramitsu.co.jp/)
* [Polkadot.js/apps framenode-2](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fws.framenode-2.b1.stg1.sora2.soramitsu.co.jp#/explorer)
* `wss://ws.framenode-3.b1.stg1.sora2.soramitsu.co.jp`
* [rpc.framenode-3.b1.stg1.sora2.soramitsu.co.jp](http://rpc.framenode-3.b1.stg1.sora2.soramitsu.co.jp/)
* [Polkadot.js/apps framenode-3](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fws.framenode-3.b1.stg1.sora2.soramitsu.co.jp#/explorer)

Mordor network (chainId = 63) [Link](https://core-geth.org/contribute-to-mordor)

### Bridge contracts

* BeefyLightClient: `0x93a668Afa9055235c27FE017bE510e3BeA68297E`
* Bitfield: `0xd6eC25735308cBC8370dd83Bbd14d069AbC61d24`
* ERC20App: `0x42d90437f0a0D9a97D71a909B740f4A4E7Ad783F`
* ETHApp: `0xf5Aa7f6E47d37133612a80432141C0EFDD4cd77C`
* InboundChannel: `0xa1BB118A2912D536E292EFeD93c7b70Ab4dc8f89`
* MerkleProof: `0xd960Da7cB929758B033ff25C02a9C071d0d08DC2`
* MigrationApp: `0xB95E6f19dB0AF089Af28cF76D40336147eA8CDC7`
* OutboundChannel: `0x3B7A22BCF40910C2e98CC6017E7390900B726b9a`
* ScaleCodec: `0x5ae337AC707E579f55cD8A9d35d522CE9064E7E1`
* SidechainApp: `0xFE0016cB30cEAe9bf0F0893A4A5917c74B9E58c7`
* SimplifiedMMRVerification: `0xe3c8D6F7503c95E1D757b01581aFBC9e8FbD3E60`
* ValidatorRegistry: `0x6c36Bf19801F10104C3e00ed0aDE9b5e75362552`
