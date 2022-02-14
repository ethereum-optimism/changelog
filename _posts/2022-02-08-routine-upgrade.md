---
title: Routine Upgrade
layout: version
packages:
    mainnet:
        - name: data-transport-layer
          version: 0.5.13
        - name: batch-submitter
          version: 0.4.16
    kovan:
        - name: l2geth
          version: 0.5.11
        - name: data-transport-layer
          version: 0.5.16
        - name: batch-submitter
          version: 0.4.18
hotfix: no
---

Kovan l2geth:
- 9ef215b: Various small changes to reduce our upstream Geth diff
- 2e7f6a5: Fixes incorrect timestamp handling for L1 syncing verifiers
- 81d9056: Bring back RPC methods that were previously blocked

Kovan data-transport-layer:
- 8f72064: Handle case where the remote block isn't found for GET /eth/context/latest and GET /eth/context/blocknumber/:number
- 1741d88: Updates DTL to correctly parse L1 to L2 tx timestamps after the first bss hardfork

Kovan batch-submitter:
Migrate to Go based batch-submitter service

Mainnet, update versions.
