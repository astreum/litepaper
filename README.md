
# Astreuos

A Next Generation Blockchain for Apps, Storage and Compute that's Distributed, Secure and Sustainable.

## Introduction

Astreuos is an accounts based blockchain which primarily works by keeping track of all the accounts and their details such as the balance, number of transactions and storage.

Astreuos includes storage and compute protocols.

The motivation for building Astreuos is to build a better blockchain for creating trusted smart contracts and price mechanisms for currency stability.

Astreuos features trust-less consensus, permission-less access and great security for users.

These features provide everyone in the world with uncensored access of financial and digital empowerment from the platform.

digital empowerment

Astreuos aims to be a competitive platform for digital services by:

- offering native value, storage and compute on the blockchain
- pricing services in a dynamic currency
- implementing a pricing mechanism that promotes currency stability

## Contents

1. Accounts
2. Blocks
3. Transactions
4. Solar
5. Nova Consensus
6. Fusion Contracts
7. Nebula Storage Layer
8. Reactor Compute Layer
9. Application
10. Components

### Accounts

An Astreuos Account is a makeup of an address and details associated to that account. Each account has a balance, a counter and storage.

`Accounts State`

```

                                        + - - - - - - - - - - - +
                                        |     accounts hash     |
                                        + - - - - - - - - - - - +
                                                    ^
                                . - - - - - - - - - - - - - - - - - - - .
                                ^                                       ^
                        + - - - - - - - - +                   + - - - - - - - - - +
                        | account 1 hash  |                   |   account 2 hash  |
                        + - - - - - - - - +                   + - - - - - - - - - +
                                ^
                  . - - - - - - - - - - - - - .
                  ^                           ^
        + - - - - - - - - - +       + - - - - - - - - - +
        |   address hash    |       |   details hash    |
        + - - - - - - - - - +       + - - - - - - - - - +
                                              ^
                  . - - - - - - - - - - - - - + - - - - - - - - - - - - - .
                  ^                           ^                           ^
          + - - - - - - - - +       + - - - - - - - - - +       + - - - - - - - - - +
          |  balance hash   |       |   counter hash    |       |   storage hash    |
          + - - - - - - - - +       + - - - - - - - - - +       + - - - - - - - - - +

```

`Account Storage`


```

                                                  + - - - - - - - +
                                                  |  storage hash |
                                                  + - - - - - - - +
                                                          ^
                                        . - - - - - - - - + - - - - - - - - - .
                                        ^                                     ^
                                + - - - - - - - - - +               + - - - - - - - - - - - +
                                |  key-value 1 hash |               |   key-value 2 hash    |
                                + - - - - - - - - - +               + - - - - - - - - - - - +
                                        ^
                        . - - - - - - - + - - - - - - - .
                        ^                               ^
                + - - - - - - - +               + - - - - - - - +
                |  key 1 hash   |               |  value 1 hash |
                + - - - - - - - +               + - - - - - - - +

```

`Accounts State Transition`

```

            Block #1                                Block #2
        + - - - - - - - +                       + - - - - - - - +
        |               |                       |               | 
        |   Previous    |      Transactions     |     Latest    |
        |   Accounts    |   - - - - - - - - ->  |    Accounts   |
        |     State     |                       |     State     |
        |               |                       |               |
        + - - - - - - - +                       + - - - - - - - +

```

The account balance is in the native unit of value which is a `Quark`.

Value magnitudes are:

- 10^24: YottaQuark (YQ)
- 10^21: ZettaQuark (ZQ)
- 10^18: ExaQuark (EQ)
- 10^15: PetaQuark (PQ)
- 10^12: TeraQuark (TQ)
- 10^9: GigaQuark (GQ)
- 10^6: MegaQuark (MQ)
- 10^3: KiloQuark (KQ)
- 10^0: Quark (Q)

### Blocks

A Block consists of the block body and the validator's ed25519 signature of the body's merkle tree root.

The block body has:

1. accounts hash
2. chain
3. number
4. previous block hash
5. receipts hash
6. solar price
7. solar used
8. time
9. transactions hash
10. validator

The Receipt is the result from the application of a transaction to the Astreuos Account State.

A receipt consists of the solar used and status of the transaction application procedure.

### Transactions

A Transaction consists of the transaction body and the sender's ed25519 signature of the body's merkle tree root.

The transaction body has:

1. chain
2. counter
3. recipient
4. sender
5. solar limit
6. solar price
7. value

### Solar

`Solar` is the currency for work done on the blockchain, in contrast with `Quark` with is the currency for value.

The solar limit of a block is set at 1,000,000,000.

| Fee | Solar |
|---|---|
| Transaction Processing | 1,000 |
| Account Creation | 200,000 |

Solar pricing mechanism:

- The solar price is fixed for every block.
- The solar price varies by 1 `Quark`.
- The solar price increases when more than 75%, and decreases when less than 25%, of the previous solar limit was used.
- The base solar price is set at 1 `Quark`.

### Nova Consensus

`Nova` is the consensus protocol for creating new blocks and validating the blockchain.

A validator must be staked, by sending `Quarks` to the nova account, to participate in the protocol.

The nova account address is 0x 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 6E 6F 76 61.

An epoch lasts approximately one week. The block time target is five seconds. A slot is the five seconds period when new blocks are created.

Slots are allocated pro rata with a validator's stake every epoch and are removed after slot selection.

A slot miss occurs when a validator does not create a new block or created a malicious block when selected.

Slot selection determines the validator for the next block at any time:

- Get validator addresses with slot allocations in the nova account storage.
- Check slot misses from the last block to the current time.
- If no slot miss, the latest block hash is used as the seed in the weighted random address selector.
- If slot misses, the linear-feedback shift register, shifted to the number of slot misses, of the lastest block hash is used as the seed in the weighted random address selector.

Transactions are ordered by the ascending value and the ascending xor from the previous transaction hash.

The creator of a new block is payed a fee 1,000,000,000 Solar at the current block's solar price.

### Fusion Contracts

Fusion is the applications platform on the Astreuos Blockchain.

Contracts are applications that run through transaction calls.

The Fusion Language is a dialect of the Lisp programming language for developing Fusion Applications.

The Fusion Machine is a stack based native runtime for Fusion Machine Code interfacing with the Astreuos Accounts State.

Helium is the Fusion code manager.

- runs automated tests
- compiles your fusion script into fusion machine code

New transaction types:

- App Creation
- App Calls

A Storage Put costs 100,000 Solar, Storage Get costs 100 Solar and all other Stack Operations cost 1 Solar.

Standards to help developers create trusted Fusion Contracts.

- Tokens
- Oracles
- Governance

### Nebula Storage Layer

Nebula is a protocol for storing and retrieving Nebula Objects.

A Nebula Object is a data structure with three fields:

- Leaf: True/False
- Data: a blob of binary data of size < 32KB
- Size: the cumulative size of the object

Puslar Network Upgrade:

- Nebula Route
- Message Kinds for get and put on nebula objects

`Object Get Flow`

```

        Client                                          Nebula
        + - - - +                                       
        |       |             object hash               + - - - - - - - +
        |       | - - - - - - - - - - - - - - - - - - > |    Nearest    |
        |       | < - - - - - - - - - - - - - - - - - - |     Node      |
        |       |        Nearer Node Pubkey & Ip        + - - - - - - - +
        |       |
        |       |
        |       |             object hash               + - - - - - - - +
        |       | - - - - - - - - - - - - - - - - - - > |    Nearer     |
        |       | < - - - - - - - - - - - - - - - - - - |     Node      |
        |       |        Index Node Pubkey & Ip         + - - - - - - - +
        |       |                  or
        |       |           Object if cached
        |       |
        |       |
        |       |             object hash               + - - - - - - - +
        |       | - - - - - - - - - - - - - - - - - - > |    Index      |
        |       | < - - - - - - - - - - - - - - - - - - |     Node      |
        |       |       Storage Node Pubkey & Ip        + - - - - - - - +
        |       |
        |       |
        |       |             object hash               + - - - - - - - +
        |       | - - - - - - - - - - - - - - - - - - > |    Storage    |
        |       | < - - - - - - - - - - - - - - - - - - |     Node      |
        |       |               Object                  + - - - - - - - +
        |       |
        + - - - +

```

The index route stores the index of the object hash and the storage provider's id.

The route is updated every five minutes to remove deleted objects and redistribute indexes adding new objects.

An indexer must prove they are storing their part of the index.

A node can use the returned id to query the storage route for the storage provider to retrieve the object.

The storage provider is paid storage fees for the storage period and retrival fees for serving an object.

A stoage provider must prove they are storing their assigned objects.

Indexers are incentivized to cache objects by earning retrival fees for returning objects instead of storage provider's id.

An indexer also earns a commission for facilitating a put contract and indexing the underlying data.

The Retrieval Fees for 32KB is 100,000 Solar.

The Storage Fees for 32KB/mo is 200,000 Solar.

### Reactor Compute Layer

Reactor is a protocol for distributed serverless computation with proof of work staking.

Reactor computations can be Open or Private.

Open Computation works by processing Fusion Applications stored on Nebula and are callable by anyone on the blockchain.

Private Compute is confidential computing enabling users to use private data and protect software intellectual property on the protocol while allowing for restricted access to calls.

### Application

#### Global Payments

#### Local Exchanges

#### Smart Contracts

#### User Powered

#### Transparency

#### Self Hosting

#### Serverless

### Components

| Project | Description | Status |
|---|---|---|
| [Astro Format](https://github.com/stelar-labs/rust-astro-format) | Encoding Format | ✅ |
| [NeutronDB](https://github.com/stelar-labs/rust-neutrondb) | Key Value Store | ✅ |
| [Opis](https://github.com/stelar-labs/rust-opis) | Integer Arithmetic | ✅ |
| [Fides](https://github.com/stelar-labs/rust-fides) | Cryptography | ✅ |
| [Pulsar Network](https://github.com/stelar-labs/rust-pulsar-network) | Messaging | ✅ |
| [Rust Astreuos](https://github.com/astreuos/rust-astreuos) | Official Node | ✅ |
| V1 Testnet Launch | | Q2 2022 |
| V1 Mainnet Launch | | Q2 2022 |

2022-04-19
