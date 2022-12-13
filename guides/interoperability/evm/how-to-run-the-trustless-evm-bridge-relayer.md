# How to run the Trustless EVM Bridge Relayer

**Docker**

`docker run --rm -e "RUST_LOG=relayer=debug,info" --entrypoint relayer sora2/substrate:bridge --help`

**Build from source**

`cargo build --release --bin relayer` `./target/release/relayer --help`

### Transfers

We will use BRIDGE STAGE environment endpoint as example

**Transfer ETH(Mordor) tokens from Ethereum to Sora**

`relayer --ethereum-url https://www.ethercluster.com/mordor --substrate-url wss://ws.framenode-1.b1.stg1.sora2.soramitsu.co.jp:443 --ethereum-key your_ethereum_private_key bridge transfer-to-sora --asset-id 0x0200070000000000000000000000000000000000000000000000000000000000 --recipient your_account_id_in_sora_network --amount 1000000000000000000`

**Transfer ERC20 tokens from Ethereum to Sora**

We will use **FTT(First Test Token)** for example. The relayer will automatically mint this token and approve transfer to bridge contract.

You can find **asset\_id** for your token using **polkadot.js/apps->developer->chain state->erc20App.assetsByAddresses**

`relayer --ethereum-url https://www.ethercluster.com/mordor --substrate-url wss://ws.framenode-1.b1.stg1.sora2.soramitsu.co.jp:443 --ethereum-key your_ethereum_private_key bridge transfer-to-sora --asset-id 0x005963f9e01c987ae213bca46603d8b569ebbf91d3c52ab59207d7e4dae87bff --recipient your_account_id_in_sora_network --amount 1000000000000000000`

**Transfer tokens from Sora to Ethereum**

For example, send some XOR to Ethereum. Derive path for your account can be your account seed, for example

`relayer --ethereum-url https://www.ethercluster.com/mordor --substrate-url wss://ws.framenode-1.b1.stg1.sora2.soramitsu.co.jp:443 --substrate-key derive_path_for_your_sora_account bridge transfer-to-sora --asset-id 0x0200000000000000000000000000000000000000000000000000000000000000 --recipient your_ethereum_address --amount 1000000000000000000`

### Relay messages

**Ethereum → Sora**

You’ll need at least 10GB of space on disk with path\_for\_dag\_cache

`relayer --ethereum-url https://www.ethercluster.com/mordor --substrate-url wss://ws.framenode-1.b1.stg1.sora2.soramitsu.co.jp:443 --substrate-key derive_path_for_your_sora_account bridge relay ethereum --base-path path_for_dag_cache`

**Sora → Ethereum**

`relayer --ethereum-url https://www.ethercluster.com/mordor --substrate-url wss://ws.framenode-1.b1.stg1.sora2.soramitsu.co.jp:443 --ethereum-key your_ethereum_private_key bridge relay substrate`
