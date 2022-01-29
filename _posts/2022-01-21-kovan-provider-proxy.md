---
title: Kovan Provider Proxy
layout: version
packages:
    mainnet:
    kovan:
        - name: proxyd
          version: 3.6.0
hotfix: yes
---

This release adds a caching proxy called `proxyd` to our public Kovan endpoint that routes traffic to infrastructure providers like Alchemy and Infura. This gives the Kovan public endpoint similar consistency and scalability guarantees to mainnet, and lets us test `proxyd` before rolling it out on mainnet.