# sdbitcoiner
sdbitcoiner (a portmanteau of instant + sidechain) is a decentralized, real-time 2nd layer sidechain with instant transaction confirmations and near 0 fees, with a 2-way peg so you can deposit and withdraw btc directly to and from the btc network. It features a decentralized, non-distributed architecture that enables anyone to run a node (a.k.a their own sidechain) and process transactions. Node operators do not need any permission to run a node, and users can connect to any (1 or more) node they choose to.

## Raison d'etre
* Support micropayments, merchant, and p2p payments by offering instantly confirmed transactions that settle on bitcoin.
* Develop an open protocol that exchanges, payment processors, banks, neo-banks, and legacy or crypto fintech companies can easily implement to increase bitcoin adoption and free market competition.
* Scale bitcoin to billions of users by a decentralized, horizontally scalable layer 2 solution.
* Make bitcoin easier to use by offering a familiar account-based ledger paired with pseudonymous public key-based transactions/messaging.
* Prevent proprietary software/networks from offering bitcoin payment processing services.
* Get rid of centralized platforms that don't allow withdrawing btc (Robinhood, Cash App, Venmo).

## Step-by-step Tutorial
Here is a simple tutorial that shows depositing, withdrawing, and transferring using the sdbitcoiner layer2 ledger:

First, clone the repo and navigate to the `/Wallet` folder. This folder contains all the files needed to interact with the network. The wallet itself is a Python file, so you will need to first install the dependencies located in the `requirements.txt` file. You can install it globally or create a [virtual environment](https://docs.python.org/3/library/venv.html); the virtual env is recommended for cleanliness.

Once the dependencies are installed, run the `wallet-cli.py` file. It should output something like this:

```shell
PS C:\sdbitcoiner\sdbitcoiner\Wallet> python .\wallet-cli.py
sdbitcoiner Wallet v0.1a - CLI
Warning: config.json not found
```

You can ignore the "Warning: config.json not found", as the config file is for things like automatically loading a wallet at startup or setting a default node URL.

### Creating and Managing Wallets

1. **Create a New Wallet**

    ```shell
    (no wallet loaded) > new-wallet wallet.json
    4BS6izr4fukPKa91auxCgkn4nPvWLqMLoHBGdySpuds5SvFwU9686cXp81zfF5GaLcDcKFp5WHKLzETumafD1USK
    ```

    This creates a new wallet called "wallet.json" and automatically generates an address, which is then printed. The wallet generates a public key and private key pair for the address.

2. **Create New Address**

    ```shell
    (wallet.json)(node: https://testnet.instachain.io/) > new-address
    3k4wgpDz4o4bmTxEhRis9AYWBniPAyozrWkgmn9z8Xsryk8XHUukC9MyKhRU9jY4oZA8sgQyJq15UDDe4V8rUS5K
    ```

    You can create as many addresses as needed.

3. **List All Addresses**

    ```shell
    (wallet.json)(node: https://testnet.instachain.io/) > list-addresses
    4BS6izr4fukPKa91auxCgkn4nPvWLqMLoHBGdySpuds5SvFwU9686cXp81zfF5GaLcDcKFp5WHKLzETumafD1USK
    3k4wgpDz4o4bmTxEhRis9AYWBniPAyozrWkgmn9z8Xsryk8XHUukC9MyKhRU9jY4oZA8sgQyJq15UDDe4V8rUS5K
    ```

### Depositing Funds

1. **Get Deposit Address**

    ```shell
    (wallet.json)(node: https://testnet.instachain.io/) > get-deposit-address 4BS6izr4fukPKa91auxCgkn4nPvWLqMLoHBGdySpuds5SvFwU9686cXp81zfF5GaLcDcKFp5WHKLzETumafD1USK
    mrBXA86UumhJc4aQTYs5NQeWgaqrEzzaKX
    ```

    This command prints a layer 1 address to send funds to. After transferring funds to this address, your layer 2 address will be credited after the required confirmations.

2. **Display Wallet Balance**

    ```shell
    (wallet.json)(node: https://testnet.instachain.io/) > list-wallet-balance
    4BS6izr4fukPKa91auxCgkn4nPvWLqMLoHBGdySpuds5SvFwU9686cXp81zfF5GaLcDcKFp5WHKLzETumafD1USK: 100000
    3k4wgpDz4o4bmTxEhRis9AYWBniPAyozrWkgmn9z8Xsryk8XHUukC9MyKhRU9jY4oZA8sgQyJq15UDDe4V8rUS5K: 0
    ```

### Transferring Funds

1. **Transfer Funds Between Addresses**

    ```shell
    (wallet.json)(node: https://testnet.instachain.io/) > transfer 3k4wgpDz4o4bmTxEhRis9AYWBniPAyozrWkgmn9z8Xsryk8XHUukC9MyKhRU9jY4oZA8sgQyJq15UDDe4V8rUS5K 1500
    Transaction id: FFcNPSH2tS3tj1m1KzHsP9FEVxyZ3egj
    Asset id: 0x100000001
    {"error_code":0,"error_message":"Success"}
    ```

2. **View Transaction Details**

    ```shell
    (wallet.json)(node: https://testnet.instachain.io/) > view-transaction FFcNPSH2tS3tj1m1KzHsP9FEVxyZ3egj
    {"error_code":0,"error_message":"Success","transaction":{...}}
    ```

### Withdrawing Funds

1. **Withdraw to Base Layer**

    ```shell
    (wallet.json)(node: https://testnet.instachain.io/) > withdraw 4BS6izr4fukPKa91auxCgkn4nPvWLqMLoHBGdySpuds5SvFwU9686cXp81zfF5GaLcDcKFp5WHKLzETumafD1USK tb1qe6gqflmgn8p2ppunscqd8khd524kvwh8j4slqa 22000
    Transaction id: TOMa9040af33GtSD7JuMNq18sbkI77YO
    {"error_code":0,"error_message":"Success"}
    ```

### Viewing Transactions

1. **List Wallet Transactions**

    ```shell
    (wallet.json)(node: https://testnet.instachain.io/) > list-wallet-transactions
    Address: 4BS6izr4fukPKa91auxCgkn4nPvWLqMLoHBGdySpuds5SvFwU9686cXp81zfF5GaLcDcKFp5WHKLzETumafD1USK
    Transaction ID  Source  Amount  Destination
    FFcNPSH2tS3tj1m1KzHsP9FEVxyZ3egj  4BS6izr4fukPKa91auxCgkn4nPvWLqMLoHBGdySpuds5SvFwU9686cXp81zfF5GaLcDcKFp5WHKLzETumafD1USK  -1500  3k4wgpDz4o4bmTxEhRis9AYWBniPAyozrWkgmn9z8Xsryk8XHUukC9MyKhRU9jY4oZA8sgQyJq15UDDe4V8rUS5K
    ```

2. **List Address Transactions**

    ```shell
    (wallet.json)(node: https://testnet.instachain.io/) > list-address-transactions 4BS6izr4fukPKa91auxCgkn4nPvWLqMLoHBGdySpuds5SvFwU9686cXp81zfF5GaLcDcKFp5WHKLzETumafD1USK
    Address: 4BS6izr4fukPKa91auxCgkn4nPvWLqMLoHBGdySpuds5SvFwU9686cXp81zfF5GaLcDcKFp5WHKLzETumafD1USK
    Transaction ID  Source  Amount  Destination
    FFcNPSH2tS3tj1m1KzHsP9FEVxyZ3egj  4BS6izr4fukPKa91auxCgkn4nPvWLqMLoHBGdySpuds5SvFwU9686

cXp81zfF5GaLcDcKFp5WHKLzETumafD1USK  -1500  3k4wgpDz4o4bmTxEhRis9AYWBniPAyozrWkgmn9z8Xsryk8XHUukC9MyKhRU9jY4oZA8sgQyJq15UDDe4V8rUS5K
    ```

### Other Commands

1. **Switch Node**

    ```shell
    (wallet.json)(node: https://testnet.instachain.io/) > switch-node https://another-node-url.com/
    Switched to node: https://another-node-url.com/
    ```

2. **Show Wallet Information**

    ```shell
    (wallet.json)(node: https://testnet.instachain.io/) > show-wallet-info
    Wallet file: wallet.json
    Node URL: https://testnet.instachain.io/
    Addresses:
    4BS6izr4fukPKa91auxCgkn4nPvWLqMLoHBGdySpuds5SvFwU9686cXp81zfF5GaLcDcKFp5WHKLzETumafD1USK
    3k4wgpDz4o4bmTxEhRis9AYWBniPAyozrWkgmn9z8Xsryk8XHUukC9MyKhRU9jY4oZA8sgQyJq15UDDe4V8rUS5K
    ```

## Inspiration
The need for fast, low-cost Bitcoin transactions inspired us to create SdBitcoiner. We aimed to provide a decentralized, scalable solution to make Bitcoin more accessible and practical for everyday use.

## What it does
SdBitcoiner is a second-layer sidechain for Bitcoin that offers instant transaction confirmations and near-zero fees. It allows users to deposit and withdraw BTC directly to and from the Bitcoin network, supporting micropayments, merchant transactions, and peer-to-peer payments.

## How we built it
We built SdBitcoiner using a decentralized, non-distributed architecture, enabling anyone to run a node and process transactions without needing permission. The system was developed with Python, leveraging an open protocol to ensure easy implementation by various financial and fintech institutions.

## Challenges we ran into
One of the main challenges was ensuring the security and reliability of the 2-way peg mechanism for seamless BTC deposits and withdrawals. We also faced difficulties in optimizing transaction speeds and minimizing fees while maintaining decentralization.

## Accomplishments that we're proud of
We are proud to have created a functional, decentralized sidechain that allows for instant and nearly free Bitcoin transactions. Our protocol is open and easy to implement, promoting Bitcoin adoption and fostering competition in the financial sector.

## What we learned
Throughout the development of SdBitcoiner, we learned the importance of balancing security, speed, and decentralization. We also gained insights into the complexities of creating a robust 2-way peg system and the necessity of thorough testing and iteration.

## What's next for SdBitcoiner
Our next steps include further enhancing the security and efficiency of SdBitcoiner, expanding node compatibility, and encouraging adoption among exchanges, payment processors, and fintech companies. We also plan to develop additional features and tools to improve user experience and facilitate broader Bitcoin adoption.