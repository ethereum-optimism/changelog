---
title: Kovan Batch Compression
layout: version
packages:
    mainnet:
        - name: batch-submitter-service
          version: 0.1.7
---

#### Batch Compression

This release enables batch compression on Kovan. **Batch compression will be rolled out to mainnet next week,** so please upgrade your `data-transport-layer`s to at least version `0.5.20` as soon as possible if you are syncing from L1. See [this release](/2022/03/08/kovan-system-addresses.html) for more information on batch compression.