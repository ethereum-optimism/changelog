---
title: DTL L1 Syncing Fix
layout: version
packages:
    kovan:
        - name: l2geth
          version: 0.5.13
        - name: data-transport-layer
          version: 0.5.18
---

This release adds patch blocks to the DTL so that it can properly sync from L1. As mentioned in the [Batch Submitter L1 Sync Hotfix](/2022/01/28/l1-sync-batch-submitter-hotfix.html) release, we discovered a bug in the batch submitter that led to state root divergence between nodes that sync from L1 and nodes that sync from L2. If you are one of the small number of node operators that sync from L1, you will need to update your DTL to use version `0.5.18` and resync.

Note that this fix only applies to mainnet. L1 syncing on Kovan is affected by a different issue which we are still looking into a fix for.


This release also includes routine updates and bugfixes for `l2geth`.


**l2geth**:

- `0002b1d`: Remove dead code in l2geth
- `1187dc9`: Don't block read rpc requests when syncing
- `bc342ec`: Fix queue index comparison

**data-transport-layer**:

- `275eb81`: Include patch contexts for bss hf1
- `baece50`: Hardcodes BSS HF1 block into the DTL