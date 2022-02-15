---
title: Mainnet Berlin Hardfork
layout: version
packages:
    kovan:
        - name: go-batch-submitter
          version: 0.1.3
    mainnet:
        - name: l2geth
          version: 0.5.11
---

This release upgrades mainnet with the Berlin hardfork. The hardfork is set to activate at block `3950000`. Given current usage, this will be sometime next week. Please upgrade your replicas to l2geth `0.5.11` as soon as possible.

The upgrade process is the same as it was on Kovan, with slightly different parameters:

1. Stop Geth if it is running.
2. Run the following command: `geth init https://storage.googleapis.com/optimism/mainnet/genesis-berlin.json 0x106b0a3247ca54714381b1109e82cc6b7e32fd79ae56fbcc2e7b1541122f84ea`. This will automatically download the updated genesis state and apply it.
3. Start Geth.

Note that you will need to run the steps above even if you upgraded `l2geth` to version `0.5.11` last week in order to mitigate the [critical security bug](/2022/02/08/critical-security-update.html). Upgrading the node software and updating the genesis configuration are distinct processes.

Apart from the Berlin hardfork, we also upgraded the Kovan batch submitter with some minor fixes:

- `69118ac`: Switch num_elements_per_batch from Histogram to Summary
- `df98d13`: Remove extra space in metric names
- `3ec0630`: Default to JSON logs, add LOG_TERMINAL flag for debugging
- `fe32161`: Unify metric name format
- `93a2681`: Fixes a bug where clearing txs are rejected on startup due to missing gas limit