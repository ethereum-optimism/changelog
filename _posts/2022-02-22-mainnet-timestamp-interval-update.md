---
title: Mainnet Timestamp Interval Update
layout: version
packages:
    kovan:
        - name: batch-submitter-service
          version: 0.1.4
---

This release updates a runtime parameter on mainnet to reduce the timestamp update interval from 5 minutes to 15 seconds.

Apart from the timestamp change, we also upgraded the Kovan batch submitter with some minor fixes:

- `bcbde5f`: Fixes a bug that causes the txmgr to not wait for the configured numConfirmations