---
title: Mainnet System Addresses, Batch Compression Upgrade Warning
layout: version
packages:
    kovan:
        - name: data-transport-layer
          version: 0.5.21
        - name: batch-submitter-service
          version: 0.1.7
    mainnet:
        - name: l2geth
          version: 0.5.14
        - name: data-transport-layer
          version: 0.5.20
        - name: gas-oracle
          version: 0.1.7
---

#### System Addresses

This release adds support for system addresses on mainnet. **If you haven't already , please upgrade `l2geth` to at least version `0.5.14`.** See the [Kovan Release](/2022/03/08/kovan-system-addresses.html) for more information on system addresses.

#### Rate Limiting

As part of this release, we upgraded our caching infrastructure and began enforcing a rate limit on our public mainnet endpoint. The limit is quite high, and is designed to deter misconfigured/malicious clients from degrading the service. If you go over the limit, your IP will be banned for 1 minute. If you need a higher rate limit than what the public endpoint affords we recommend using a third-party infrastructure provider.

#### Batch Compression Upgrade Warning

We will be enabling batch compression on Kovan on Thursday the 17th. We'll be enabling it on mainnet on the 21st. Please upgrade your `data-transport-layer`s to at least version `0.5.20` as soon as possible if you are syncing from L1. See [last week's release](/2022/03/08/kovan-system-addresses.html) for more information on the batch compression spec.

#### Routine Upgrades

Apart from the above, we also performed a routine upgrade of other services.

**data-transport-layer**

- Updated dependencies [`b3f9bde`]
- Updated dependencies [`175ae0b`]
- Updated dependencies [`e53b578`]
  - @eth-optimism/common-ts@0.2.2
  - @eth-optimism/contracts@0.5.17

**batch-submitter-service**

- `aca0684`: Add 20% buffer to gas estimation on tx-batch submission to prevent OOG reverts
- `75040ca`: Adds MIN_L1_TX_SIZE configuration