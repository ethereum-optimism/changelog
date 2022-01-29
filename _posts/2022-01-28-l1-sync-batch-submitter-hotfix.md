---
title: Batch Submitter L1 Sync Hotfix
layout: version
packages:
    kovan:
        - name: batch-submitter
          version: 0.4.15
---

We discovered a bug in the batch submitter that led to state root divergence between nodes that sync from L1 and nodes that sync from L2. The majority of our node operators sync from L2, and are unaffected by this issue. For the node operators that sync from L1, we're fixing this issue in phases:

1. Fix the batch submitter.
2. Add "patch configs" to the DTL that will overwrite the invalid timestamps submitted to L1.

This release implements phase one for Kovan. Phase 2 will complete shortly, then we'll roll everything out to mainnet. **Once we've deployed the updated batch submitter to mainnet, all L1 syncing replicas will need to update their DTL and batch submitter versions and resync.**

Again, you do not need to do anything if your node syncs from L2. To find out which sync mode your node is in, check the value of the `ROLLUP_BACKEND` environment variable. If it's set to `l1`, then you are affected by this issue. If it's undefined or set to `l2`, then you are not affected by this issue.