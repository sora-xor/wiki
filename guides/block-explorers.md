# Block Explorers

## Theory

A **block explorer** is a tool that is used to view all blockchain transactions online. Specifically, to view all current and past **transactions** on the **blockchain**.

In other words, a block explorer is an online blockchain browser that reveals the data of individual blocks and transactions. With this tool, we can monitor transaction histories and balances of addresses.

The SORA mainnet has 2 block explorers:

1. [SORAscan](https://sorascan.com/sora-mainnet) based on [Polkascan](https://polkascan.io/). The code of SORAscan is open source. You can find the source code on the [GitHub](https://github.com/sora-xor/polkascan-os).
2. [Subscan](https://sora.subscan.io/) block explorer. The SORA network block explorer is supported by the Subscan team.

You can find any information that you need on:

1. Block details
2. Transaction details
3. Transaction events
4. Account information

## Practice

**We recommend using the SORA testnet for practice exercises. Here are the Testnet links:**

1. [Polkaswap test application](https://test.polkaswap.io/)
2. [Polkadot js SORA testnet application](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fws.stage.sora2.soramitsu.co.jp#/explorer)
3. [Android testnet application](https://play.google.com/store/apps/details?id=jp.co.soramitsu.sora.communitytesting\&hl=en\&gl=US)
4. [iOS testnet application](https://testflight.apple.com/join/670hF438)

**The limitation in this lesson is that Subscan only supports the SORA mainnet. If you're doing an exercise on the testnet, only SORAscan will be available.**

#### SORAscan

Open the testnet SORAscan [https://test.sorascan.com/sora-staging](https://test.sorascan.com/sora-staging)

![](<../.gitbook/assets/Untitled (8) (3).png>)

Here you see the main dashboard that contains:

1. The search box where you can put the block number, transaction id, and account address as search fields
2. Number of blocks. You can click on it to open the block list
3. Number of transactions. You can click on it to open the list of transactions
4. Number of transfers from Ethereum to SORA network. You can click on it to open the list of transfers from Ethereum to the SORA network
5. Number of transfers from SORA to Ethereum. You can click on it to open the list of transfers from SORA to Ethereum.
6. Number of events. You can click on it to open the list of events
7. Number of active accounts. You can click on it to open the list of accounts
8. Number of Runtime versions. You can click on it to get the network upgrade history.

#### How to find a transaction

There are a few ways to find a transaction in the block explorer.

* Open the Polkaswap Account screen. And open the Activity tab to find your transaction. Then click on it. You'll see the transaction details screen. On the details screen you can copy the transaction number or open it in the block explorer.

![](<../.gitbook/assets/Untitled (24).png>)

![](<../.gitbook/assets/Untitled (1) (4).png>)

![](<../.gitbook/assets/Untitled (2) (3).png>)

* If you know the transaction number, you can open the transaction in the block explorer. Paste the transaction number in the search box and press Enter. This will open the transaction details.

![](<../.gitbook/assets/Untitled (3) (6).png>)

![](<../.gitbook/assets/Untitled (4) (5).png>)

#### How to find an account

You can get all the information about an account. Click on Accounts then select All accounts from the drop-down menu to get the list of accounts.

![](<../.gitbook/assets/Untitled (5) (1).png>)

You can also find an account using the search box on the main dashboard.

![](<../.gitbook/assets/Untitled (6) (1).png>)

On the Account page, you can find all the transaction and XOR balance history

![](<../.gitbook/assets/Untitled (7) (3).png>)

![](<../.gitbook/assets/Untitled (9) (2).png>)

#### Assets

You can find all Assets in the network if you open Chain, then select Assets from the drop-down menu.

![](<../.gitbook/assets/Untitled (10) (1).png>)

You can click the asset address and open the Asset details page where the information about asset holders is located.

![](<../.gitbook/assets/Untitled (11) (2).png>)

#### Transactions

Transactions are the most important part of the block explorer. You can find all the transactions in Chain, then select Transactions from the drop-down menu.

![](<../.gitbook/assets/Untitled (12).png>)

You can filter transactions by module and call. For example Assets transfer will list all transfers

![](<../.gitbook/assets/Untitled (13).png>)

#### Subscan

**Subscan is only available for the SORA mainnet. This means that you will not be able to find transactions made on the testnet in Subscan.**

Open [mainnet Subscan ](https://sora.subscan.io/)

![](<../.gitbook/assets/Untitled (14) (1).png>)

Here you will see the main dashboard that contains:

1. Search box. Use it to search via account, transaction, block id, or number.
2. Network statistics
3. XOR allocation
4. List of latest blocks
5. List of latest extrinsics

#### How to find a transaction

If you have the transaction hash or id you can find it using the search box. Just paste the transaction number into the search box and click Search.

![](<../.gitbook/assets/Untitled (15) (1).png>)

On the Transaction details screen you will see all the information about extrinsics including parameters and events.

![](<../.gitbook/assets/Untitled (16).png>)

#### How to find an account

If you have an account address then you can find it using the search box. Just paste or enter the account address into the search box and click Search.

![](<../.gitbook/assets/Untitled (17) (3).png>)

On the account details view, you can find information about the XOR balance, transfers and transactions that were made by the account.

![](<../.gitbook/assets/Untitled (18) (2).png>)

#### Transactions

Transactions are the most important part of the block explorer. You can find all the transactions in Blockchain, then select Extrinsics from the drop-down menu.

![](<../.gitbook/assets/Untitled (19).png>)

On the extrinsic list page you can find the extrinsic history.

![](<../.gitbook/assets/Untitled (20) (1).png>)

You can filter an extrinsic by date or block range, by account, module, and call. It is very useful for viewing account activity or the history of a specific operation.

