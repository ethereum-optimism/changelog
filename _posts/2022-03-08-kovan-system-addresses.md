---
title: Kovan System Addresses
layout: version
packages:
    kovan:
        - name: l2geth
          version: 0.5.14
        - name: data-transport-layer
          version: 0.5.20
        - name: gas-oracle
          version: 0.1.7
        - name: batch-submitter-service
          version: 0.1.6
    mainnet:
        - name: l2geth
          version: 0.5.13
---

#### System Addresses

This release adds support for two additional system addresses to our Kovan sequencer. System addresses are special addresses of the form `0x420...NN`, and are used for things like our cross chain messenger contract. **This change is technically a hardfork, so please upgrade your replicas to at least `0.5.14` as soon as possible in order to avoid a chain split.**

Note that both system addresses are currently empty. Unupgraded nodes will continue to work until we deploy a contract at one of the system addresses. However, you should still upgrade as soon as possible since we might deploy a system contract at any time without warning.

We'll be deploying these changes to mainnet next Tuesday.

#### Typed Batches and Batch Compression

This release also adds support for typed batches and batch compression. Please see the [announcement post](https://medium.com/ethereum-optimism/the-road-to-sub-dollar-transactions-part-2-compression-edition-6bb2890e3e92) for more information. We will be enabling compression on Kovan on the 17th, and mainnet on the 24th. Unless you are running an L1-syncing replica or parsing L1 batches yourself, no action is required.

**If you are running an L1-syncing replica,** please upgrade your `data-transport-layer` to at least version `0.5.20`.

**If you are parsing L1 batches yourself,** please see the specification at the end of this post.

#### Typed Batches/Batch Compression Spec

Transaction batches are specified as follows:

```
Sequencer Batch Appended Calldata
Starting tx index:                       5 bytes
Number of elements in batch:             3 bytes
Number of batch contexts:                3 bytes
Number of contexts * batch context size: number of contexts * 16 bytes
transaction length:                      3 bytes
raw transaction:                         transaction length number of bytes

Batch Context
Number of txs sent directly to L2:       3 bytes
Number of deposits:                      3 bytes
Timestamp:                               5 bytes
Block Number:                            5 bytes
```

To support a "versioning" of batches, we introduce the concept of a type batch. Typed batches include a dummy context with a timestamp of 0. It would be impossible to have a real context with a timestamp of 0, so this very clearly defines that the transaction batch is typed. The block number is then used as an enum to describe which batch type is in use.

**Transaction Batch Types**

**Type 0**

```
Sequencer Batch Appended Calldata
Starting tx index:                           5 bytes
Number of elements in batch:                 3 bytes
Number of batch contexts:                    3 bytes
Dummy Context
  Number of txs:      0x000000
  Number of deposits: 0x000000
  Timestamp:          0x0000000000
  Blocknumber:        0x0000000000
Number of contexts - 1 * batch context size: number of contexts - 1 * 16 bytes
zlib.compress:
  transaction length:                      3 bytes
  raw transaction:                         transaction length number of bytes

Batch Context
Number of txs sent directly to L2:       3 bytes
Number of deposits:                      3 bytes
Timestamp:                               5 bytes
Block Number:                            5 bytes
```

The main difference for this batch type is that the transaction data is compressed with zlib. There is an implementation of zlib in the [node.js standard library](https://nodejs.org/api/zlib.html) as well as the [golang standard library](https://pkg.go.dev/compress/zlib).

#### Routine Upgrades

Apart from the above, we also performed a routine upgrade of other services and added caching and automated failover to our public endpoints.

**data-transport-layer**

- `3873b69`: Enable typed batch support
- Updated dependencies [`962f36e`]
- Updated dependencies [`f2179e3`]
- Updated dependencies [`b6a4fa4`]
- Updated dependencies [`b7c0a5c`]
- Updated dependencies [`5a6f539`]
- Updated dependencies [`27d8942`]
    - @eth-optimism/contracts@0.5.16
    - @eth-optimism/core-utils@0.8.1

**gas-oracle**

- `fed748e`: Update to go-ethereum v1.10.16

**batch-submitter-service**

- `6af67df`: Move L2 dial logic out of bss-core to avoid l2geth dependency
- `fe68056`: Enable the usage of typed batches and type 0 zlib compressed batches 