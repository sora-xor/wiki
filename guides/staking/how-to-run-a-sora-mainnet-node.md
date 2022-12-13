# How to Run a SORA Mainnet Node

## TL;DR <a href="#3375" id="3375"></a>

{% hint style="info" %}
* Anyone can run a node on the SORA mainnet
* There are two types of nodes:
  * Syncing nodes (that just receive and relay data)
  * Validating nodes (that make the blocks)
{% endhint %}

## Prerequisites <a href="#cd81" id="cd81"></a>

You will need:

* A machine with Linux, Windows or macOS
* [Docker](https://docs.docker.com/get-docker/). Follow the installation guide for your operating system.
* At least 8GB RAM (preferably 16GB RAM, although 64GB RAM will be needed for production)
* 300GB free space (preferably SSD, with the ability to expand)
* Intel(R) Core(TM) i7–7700K CPU @ 4.20GHz (alternatively, a 4-Core processor with a frequency of 2.2 GHz)

Check that docker is installed using the `docker --version` command in terminal.



```
C:\\Users\\Pg> docker --version
Docker version 20.10.2, build 2291f61
C:\\Users\\Pg>
```

It’s recommended to use the latest docker version.

Check the container with the `docker run hello-world` command in terminal. If everything works fine, Docker will pull the hello-world image and run it. You should see the following output:

<pre data-overflow="wrap" data-line-numbers><code>C:\\Users\\Pg> docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete
Digest: sha256:95ddb6c31407e84e91a986b004aee40975cb0bda14b5949f6faac5d2deadb4b9
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

<strong>To generate this message, Docker took the following steps:
</strong> 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
    
To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash
 
Share images, automate workflows, and more with a free Docker ID:
 &#x3C;https://hub.docker.com/>
 
For more examples and ideas, visit:
 &#x3C;https://docs.docker.com/get-started/>
</code></pre>

If something went wrong, please visit the [Docker documentation](https://docs.docker.com/) site, and depending on your operating system, you can also download Docker here:

* [macOS](https://docs.docker.com/get-docker/#docker-for-mac)
* [Windows](https://docs.docker.com/get-docker/#docker-for-windows/install/)
* [Linux](https://docs.docker.com/get-docker/#docker-for-linux)

## Get the latest SORA Node version number <a href="#d729" id="d729"></a>

{% hint style="warning" %}
Users should use version **1.4.5** for the time being. We will update this article with the latest version after every update.
{% endhint %}

You should use the latest SORA Node version in order to run a node. You can see the [latest build number here](https://hub.docker.com/r/sora2/substrate/tags?page=1\&ordering=last\_updated), and find the last version with the`x.y.z` format.

<figure><img src="https://miro.medium.com/max/720/1*IqL5luP5B4OUXco4BKZahQ.png" alt=""><figcaption></figcaption></figure>

Use this version number for further `docker` commands in this guide. The number of the version will be marked as **`<version>`** in the commands (_note: enter the version number without the brackets_).

## Running a Syncing Node <a href="#2b3d" id="2b3d"></a>

### On Linux/Mac <a href="#12f3" id="12f3"></a>

Pull the docker image from the docker repository:

```
docker pull sora2/substrate:1.4.5
```

Create a folder for the node configuration:

```
mkdir sora2
cd sora2
```

And grant access to the folder

```
chown 10000:10000 `pwd`
```

{% hint style="info" %}
On macOS you might need to use **i**nstead**:**

`sudo chown <username>:1000`
{% endhint %}

Run the docker image (don’t forget to insert your version below!)

```
docker run --rm -p 127.0.0.1:9933:9933 -p 127.0.0.1:9944:9944 -v `pwd`:/chain sora2/substrate:1.2.1 --name sora2-node --chain main --base-path /chain --unsafe-ws-external --unsafe-rpc-external --wasm-execution compiled
```

### On Windows <a href="#8dca" id="8dca"></a>

Pull the docker image from the docker repository

```
docker pull sora2/substrate:1.4.5
```

Create a folder for the node configuration

```
C:\\Users\\<username>\\sora2-node
```

Check access to the folder:

<figure><img src="https://miro.medium.com/max/640/1*OZJvwruBb0AuWHl3yqc-1w.png" alt=""><figcaption></figcaption></figure>

All checkboxes should be activated for the user:

<figure><img src="https://miro.medium.com/max/640/1*Rk1ndV2dhtIfbrifcIF_oQ.png" alt=""><figcaption></figcaption></figure>

Run the docker command_:_

{% code overflow="wrap" %}
```
docker run --rm -p 127.0.0.1:9933:9933 -p 127.0.0.1:9944:9944 -v sora2-node:/chain -u 0 sora2/substrate:1.4.5 --name sora2-node --chain main --base-path /chain --unsafe-ws-external --unsafe-rpc-external --wasm-execution compiled
```
{% endcode %}

Now you can connect to your node with [polkadot.js apps](https://polkadot.js.org/apps/#/explorer). Select _Local node_ and click _Switch._

<figure><img src="https://miro.medium.com/max/640/1*gRpHLRjPrJn1qst7Ox0B4w.png" alt=""><figcaption></figcaption></figure>

Then your node should sync!

## Running a Validator Node <a href="#903b" id="903b"></a>

### On Linux/Mac <a href="#64b3" id="64b3"></a>

```
docker pull sora2/substrate:1.4.5
```

Create a folder for the node configuration

```
mkdir sora2
cd sora2
```

And grant access to the folder

```
chown 10000:10000 `pwd`
```

{% hint style="info" %}
On macOS you might need to use **i**nstead**:**

`sudo chown <username>:1000`
{% endhint %}

And run the Docker command

{% code overflow="wrap" %}
```
docker run --rm -p 127.0.0.1:9933:9933 -p 127.0.0.1:9944:9944 -v `pwd`:/chain sora2/substrate:1.4.5 --name sora2-node --chain main --base-path /chain --validator --rpc-methods Unsafe --rpc-cors all --execution Wasm --wasm-execution compiled
```
{% endcode %}

You can add the following flag to enable [Telemetry](https://telemetry.polkadot.io/#list/SORA) for your node

```
--telemetry-url "wss://telemetry.polkadot.io/submit/ 0"

```

### On Windows <a href="#4ce9" id="4ce9"></a>

Pull the docker image from the docker repository

```
docker pull sora2/substrate:1.4.5
```

Create a folder for the node configuration

```
C:\\Users\\<username>\\sora2-node
```

Check the access to the folder:

<figure><img src="https://miro.medium.com/max/640/1*OZJvwruBb0AuWHl3yqc-1w.png" alt=""><figcaption></figcaption></figure>

All checkboxes should be activated for the user:

<figure><img src="https://miro.medium.com/max/640/1*Rk1ndV2dhtIfbrifcIF_oQ.png" alt=""><figcaption></figcaption></figure>

Run the Docker command

{% code overflow="wrap" %}
```
docker run --rm -p 127.0.0.1:9933:9933 -p 127.0.0.1:9944:9944 -v `pwd`:/chain sora2/substrate:1.4.5 --name sora2-node --chain main --base-path /chain --validator --rpc-methods Unsafe --rpc-cors all --execution Wasm --wasm-execution compiled
```
{% endcode %}

## Get session keys <a href="#6401" id="6401"></a>

### With polkadot.js app

Open [polkadot.js apps](https://polkadot.js.org/apps/#/explorer) and switch to your local node.

<figure><img src="https://miro.medium.com/max/720/1*7lLnloFZTyqVOLUci94Uzg.png" alt=""><figcaption></figcaption></figure>

In the Development section, select Local Node _(ws://127.0.0.1:9944)_ and click _Switch_.

<figure><img src="https://miro.medium.com/max/640/1*ygjPTZezTA3Yq2kXkFiunA.png" alt=""><figcaption></figcaption></figure>

Now you’re able to see the screen with your node information. _(Once your node has fully synced)_

<figure><img src="https://miro.medium.com/max/720/1*XETzax0tetc_w1YMyobepg.png" alt=""><figcaption></figcaption></figure>

Navigate to _Developer_ → _RPC calls_

<figure><img src="https://miro.medium.com/max/720/1*TO_EGJKVgXs_P-19xTpTJw.png" alt=""><figcaption></figcaption></figure>

Select _author_ → _rotateKeys()_

<figure><img src="https://miro.medium.com/max/720/1*9JZlJpAKezhqoVUkxz4Rzg.png" alt=""><figcaption></figcaption></figure>

And click _Submit RPC call_ button.

<figure><img src="https://miro.medium.com/max/720/1*0e0ZkSMphJR3witfFeN9BQ.png" alt=""><figcaption></figcaption></figure>

You’ll get your session key in the output. Copy the key as you will need them for a further step.



### With command line <a href="#acb2" id="acb2"></a>

Open the terminal (or other command line client) and run the command

{% code overflow="wrap" %}
```
curl -H “Content-Type: application/json” -d ‘{“id”:1, “jsonrpc”:”2.0", “method”: “author_rotateKeys”, “params”:[]}’ http://localhost:9933
```
{% endcode %}

The output will contain the session key

{% code overflow="wrap" %}
```
{“jsonrpc”:”2.0",”result”:”0x5e977ddcc0c69a6aed067052d5bd8f6bd365fae03562fd447d434e9814ac415d7c9ffe722364922bda314e44654f5c0cdc00d152470d5433f12cb73d078061863ac769d5f17b5460f042d221edf0099d2ce4c23edbe96ac943452cc4d3ad6d72”,”id”:1}
```
{% endcode %}

Copy the _result,_ in the current example it is

{% code overflow="wrap" %}
```
0x5e977ddcc0c69a6aed067052d5bd8f6bd365fae03562fd447d434e9814ac415d7c9ffe722364922bda314e44654f5c0cdc00d152470d5433f12cb73d078061863ac769d5f17b5460f042d221edf0099d2ce4c23edbe96ac943452cc4d3ad6d72
```
{% endcode %}

## Adding a Validator <a href="#e7a0" id="e7a0"></a>

First, you should go to _Accounts_ and already have an account connected.

Navigate to Network → Staking → Account actions

and click _Validator_:

<figure><img src="https://miro.medium.com/max/720/1*TxLGnO5LX06pmpcDtxAR_g.png" alt=""><figcaption></figcaption></figure>

Select stash and controller account. It’s recommended to use different accounts for stash and controller. _(In the example we are using PAVEL (EXTENSION))_

Set the bonded value:

<figure><img src="https://miro.medium.com/max/720/1*kY5qSuLETelc_iy1VPXGzw.png" alt=""><figcaption></figcaption></figure>

Set the session key (_the result of rotateKeys call_) and reward commission:

<figure><img src="https://miro.medium.com/max/720/1*EsDims5wovN2BUyTzt4GRg.png" alt=""><figcaption></figcaption></figure>

And sign the transaction.

<figure><img src="https://miro.medium.com/max/720/1*arn-bPmxTVn9HJdlL1sgVg.png" alt=""><figcaption></figcaption></figure>

Make sure that you have been added to the stashes:

<figure><img src="https://miro.medium.com/max/720/1*OLssDW2317pQp7ilsKiCBQ.png" alt=""><figcaption></figcaption></figure>

Finally, wait for the next Era.

<figure><img src="https://miro.medium.com/max/720/1*PvYAGhbH2y8xw_E1AqcrBw.png" alt=""><figcaption></figcaption></figure>

When the next Era starts, your validator will be added.

## Get Payouts <a href="#cb1c" id="cb1c"></a>

Open _Staking → Payouts._ If your validator participates in the consensus, then you’ll be able to get payouts after the Era.

Polkadot.js apps always display XOR, because they don’t support multi assets. There should be said VAL on the screenshot below.

<figure><img src="https://miro.medium.com/max/720/1*nGcoFSWtkN7gtXwhSCQ1Eg.png" alt=""><figcaption></figcaption></figure>

Click the _Payout all_ button and sign the transaction

<figure><img src="https://miro.medium.com/max/720/1*bFqBuFQfUU3gAs3crGbWXQ.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://miro.medium.com/max/720/1*jCgoi_SgoZfdzYT223aWnQ.png" alt=""><figcaption></figcaption></figure>

Make sure to pay attention as the reward will be shared among Validator and Nominators according the Stake.

## Add node to Telemetry <a href="#8f23" id="8f23"></a>

If you want to add your node to [telemetry](https://telemetry.polkadot.io/#list/SORA) just add this tag when you run the docker image

```
--telemetry-url "wss://telemetry.polkadot.io/submit/ 0"
```

You can change the name of your node by editing the parameter value of:

```
--name sora2-node
```

## Running an Archive node <a href="#a465" id="a465"></a>

### On Linux/Mac <a href="#4cac" id="4cac"></a>

```
docker pull sora2/substrate:1.4.5
```

Create a folder for the node configuration

```
mkdir sora2
cd sora2
```

And grant access to the folder

```
chown 10000:10000 `pwd`
```

{% hint style="info" %}
On macOS you might need to use **i**nstead**:**

`sudo chown <username>:1000`
{% endhint %}

And run the Docker command

{% code overflow="wrap" %}
```
docker run --rm -p 127.0.0.1:9933:9933 -p 127.0.0.1:9944:9944 -v `pwd`:/chain sora2/substrate:1.4.5 --name sora2-my-node --chain main --base-path /chain --unsafe-ws-external --pruning archive --unsafe-rpc-external --wasm-execution compiled
```
{% endcode %}

### On Windows <a href="#7824" id="7824"></a>

Pull the docker image from the docker repository

```
docker pull sora2/substrate:1.4.5
```

Create a folder for the node configuration

```
C:\\Users\\<username>\\sora2-node
```

Check the access to the folder

<figure><img src="https://miro.medium.com/max/640/1*OZJvwruBb0AuWHl3yqc-1w.png" alt=""><figcaption></figcaption></figure>

All checkboxes should be activated for the user

<figure><img src="https://miro.medium.com/max/640/1*Dal0Nw6dfZeyEgXRQXUPWQ.png" alt=""><figcaption></figcaption></figure>

Run the Docker command

{% code overflow="wrap" %}
```
docker run --rm -p 127.0.0.1:9933:9933 -p 127.0.0.1:9944:9944 -v sora2-node:/chain -u 0 sora2/substrate:1.4.5 --name sora2-my-node --chain main --base-path /chain --unsafe-ws-external --pruning archive --unsafe-rpc-external --wasm-execution compiled
```
{% endcode %}

The node will take some time to sync. The output in logs should look like this:

{% code overflow="wrap" %}
```
2021-04-30 11:33:33 💤 Idle (0 peers), best: #0 (0x7e4e…8ad5), finalized #0 (0x7e4e…8ad5), ⬇ 37.1kiB/s ⬆ 16.3kiB/s    
2021-04-30 11:33:38 ⚙️  Syncing 31.0 bps, target=#38470 (1 peers), best: #155 (0xa9e2…5b22), finalized #0 (0x7e4e…8ad5), ⬇ 127.6kiB/s ⬆ 0.9kiB/s    
2021-04-30 11:33:43 ⚙️  Syncing 35.6 bps, target=#38470 (2 peers), best: #333 (0x4c68…2957), finalized #0 (0x7e4e…8ad5), ⬇ 7.9kiB/s ⬆ 0.2kiB/s    
2021-04-30 11:33:48 ⚙️  Syncing 32.4 bps, target=#38471 (2 peers), best: #495 (0x9082…f220), finalized #0 (0x7e4e…8ad5), ⬇ 41.3kiB/s ⬆ 1.1kiB/s    
2021-04-30 11:33:53 ⚙️  Syncing 34.6 bps, target=#38471 (2 peers), best: #668 (0xb34a…121a), finalized #512 (0x1f6e…cc65), ⬇ 0.1kiB/s ⬆ 0
```
{% endcode %}

You can connect to your own node with Polkadot.js apps. [Open Polkadot.js apps](https://polkadot.js.org/apps/) and navigate to the Development section in the network selector.

<figure><img src="https://miro.medium.com/max/720/1*fSHcEgcXWL9ZSa-BRtLtVw.png" alt=""><figcaption></figcaption></figure>

If you’re running a node on your local machine then select _Local Node_ and click _Switch_. Otherwise, enter your custom endpoint and save.

## FAQ <a href="#4121" id="4121"></a>

Q: **I’m getting an error starting the node**.

A: _Double check if you have entered the command and flags correctly and that there are no typos. If that does not work,_ l_ocate your Sora2 folder, erase its contents, pull the docker image and try running the node again._

Q: **I don’t have XOR for initial staking**.

A: _You can exchange tokens for XOR on_ [_Polkaswap_](https://test.polkaswap.io/exchange/swap), or transfer tokens from ETH to the SORA Mainnet using the [bridge function in Polkaswap](https://polkaswap.io/#/bridge) and then exchange for XOR.

Q: **Where can I see my node in telemetry?**

A: _You can see it_ [_here_](https://telemetry.polkadot.io/#map/SORA)

Q: **My node is having trouble syncing, what can I do?**

A: You can add the setting `--in-peers 80` and that should solve the issue, otherwise _see the next question_.

Q: **I have checked all the documentation and my question still has no answer, who else can I ask?**

A: You can always join the [SORA Devs Telegram community](https://t.me/soradevs) and ask any other questions you may have there, other community members and the admins will be happy to help!
