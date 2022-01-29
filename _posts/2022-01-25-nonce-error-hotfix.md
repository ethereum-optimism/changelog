---
title: Nonce Error Hotfix
layout: version
packages:
    mainnet:
        - name: l2geth
          version: 0.5.6_b48f6045
        - name: batch-submitter
          version: 0.4.12
    kovan:
        - name: l2geth
          version: 0.5.8
        - name: data-transport-layer
          version: 0.5.11
        - name: gas-oracle
          version: 0.1.6
        - name: batch-submitter
          version: 0.4.13
hotfix: yes
---

This release fixes a critical bug in `l2geth`'s nonce handling logic that could have caused a denial-of-service. The fix has been rolled out across both Kovan and mainnet, as well as to all major infrastructure providers. **If you are running a replica, please upgrade `l2geth` to version `0.5.8` as soon as possible.** No funds were ever at risk, and the issue was never exploited.

For full details of what went wrong, see the [Nonce Error Hotfix Post-Mortem](/post-mortems/high-nonce-dos.html).

This release also deploys last week's timestamp changes to mainnet and performs a bunch of routine upgrades.