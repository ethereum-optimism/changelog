---
title: High Nonce Deposit DoS
date: 2022-01-25
layout: post
---

We deployed a hotfix to our sequencer this morning in order to eliminate a DoS vector. The hotfix was rolled out simultaneously to all major infrastructure providers. **If you are running a replica, please upgrade `l2geth` to version `0.5.8` as soon as possible.** Otherwise, you don’t need to do anything.

Before getting into details, we want to make a couple of things clear:

- No funds were ever at risk.
- The issue was never exploited.
- Even if the issue was exploited, users could have withdrawn their funds on L1.

**Issue Details**

Optimism, like other rollup-based L2s, allows users to send L2 transactions from L1. Transactions sent from L1 are added to a queue in the `CanonicalTransactionChain` contract. The sequencer then processes these transactions asynchronously and adds them to the L2 chain’s state.

For the sake of clarity, we’ll call L2 transactions that get initiated on L1 “bridged transactions.” The sequencer needs to derive an L2 counterpart for every bridged transaction on L1. Since derived transactions are created by the sequencer itself, they are subject to some special consensus rules. The rules relevant to this issue are:

- The nonce of a bridged transaction on L2 is set to the index at which the transaction appears in the CTC queue.
- The `ecrecover` address of a bridged transaction is set to the null address.

You can see these rules at work by viewing the null address [on Etherscan](https://optimistic.etherscan.io/address/0x0000000000000000000000000000000000000000).

Geth performs a nonce check as part of its consensus rules. The nonce check is performed on a `Message` object that gets calculated using the `Transaction` object described above. Crucially, the sender of a `Message` object is the value received from performing an `ecrecover` on the transaction’s ECDSA signature - which is the zero address. This means that any account whose nonce on Optimism is higher than the maximum queue index would be unable to deposit via `enqueue`, since Geth would reject the transaction with a `nonce too low` error.

This alone, however, was not enough to justify an emergency release. That justification came from a quirk of how we implemented CTC synchronization in the sequencer. When the sequencer restarts, it goes into “sync mode” and tries to catch up with the latest transactions on the CTC. Any sync failures that occur while in sync mode cause the sequencer to exit. Since sync mode disables itself once the sequencer catches up with the CTC, this would mean that all sequencers - including replicas - could not be restarted if the issue was exploited. The queue index was \~44,000 when we discovered this issue, so given a fee of $2/tx it would cost just shy of $90,000 to cause a DoS of the Optimism network.

Luckily, we’ve been spending the last few months beefing up our internal testing and QA processes. As a result, we caught this issue on an internal stress testing environment before anyone was able to exploit it. After verifying the fix we immediately updated our sequencer and coordinated with infrastructure providers to update their replicas.

It’s never our plan to perform emergency hotfixes like this one. But we’ll always put the security of our network first. In this case, the hotfix prevented a potential DoS and avoided hours of downtime.