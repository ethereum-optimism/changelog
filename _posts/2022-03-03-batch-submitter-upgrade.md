---
title: Batch Submitter Upgrade
layout: version
packages:
    mainnet:
        - name: batch-submitter-service
          version: 0.1.4
---

This release replaces our legacy batch submitter with a newer, more efficient one written in Go. Unless you are operating a batch submitter as part of a private Optimism testnet, no action is required. The new batch submitter lays the groundwork for concurrent batch submission and batch compression, which together will let us increase throughput and reduce fees.

As part of this release, we re-evaluated our batch submission rate given the network's current usage. We've set the batch submission rate to be once every 30 minutes as a result of our findings. Tangibly, this means that messages sent from L2 to L1 may take up to 30 minutes to arrive. We're working on a solution  that will let us bring our batch submission rate back up - stay tuned.