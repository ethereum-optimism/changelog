---
title: Berlin Hardfork
layout: version
packages:
    kovan:
      - name: batch-submitter
        version: 0.4.16
      - name: l2geth
        version: 0.5.9
    mainnet:
      - name: data-transport-layer
        version: 0.5.13
critical: no
---

This release deploys the Berlin hardfork on Kovan. Please upgrade your version of l2geth to version `0.5.9` as soon as possible. The hardfork activates at block `1138900`, and any unupgraded nodes will fall out of sync at that time.

Our Berlin hardfork includes a subset of mainnet's Berlin EIPs:

- EIP-2929
  - **Note:** We used to use a modified EIP-2929. This hardfork makes our EIP-2929 implementation match mainnet.
- EIP-2565
- EIP-3529

It does not include typed transactions.

To upgrade an existing Kovan node, you'll need to reinitialize Geth. To do that:

1. Stop Geth if it is running.
2. Run the following command: `geth init https://storage.googleapis.com/optimism/kovan/kovan-berlin-genesis.json 0xaed938bc5dee7eb703658d4bec1f3e28f8b92bd9c032b2be779186eafc2b5a2a`. This will automatically download the updated genesis state and apply it.
3. Start Geth.

Alternatively, if you're using [op-replica](https://github.com/optimisticben/op-replica), set the `SHARED_ENV` environment variable to `mainnet-gen5-kovan` to do this automatically.

You will need to do this again on mainnet in a few weeks.