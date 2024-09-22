---
description: An overview of Beldex Master Node
---

# Overview

Although Beldex implements novel changes on top of the [CryptoNote protocol](https://beldex.io/whitepaper.pdf) ([ASIC Resistance](https://docs.beldex.io/MasterNodes/Mining/ASICResistance/), [Dynamic Block Size](https://beldex.io/whitepaper.pdf) & [Static Ring Signatures](https://beldex.io/whitepaper.pdf)), much of Beldex’s networking functionality and scalability is enabled by a set of incentivised nodes called Master Nodes. To operate a Master Node, an operator [time-locks a significant amount of Beldex](master-node-functions.md) and provides a minimum level of bandwidth and storage to the network. In return for their services, Beldex Master Node operators receive a portion of the block reward from each block.

The resulting network provides market-based resistance to Sybil attacks, addressing a range of problems with existing mixnets and confidentiality-focused services. This resistance is based on supply and demand interactions which help prevent single actors from having a large enough stake in Beldex to have a significant negative impact on the second-layer confidentiality services Beldex provides. [DASH](https://github.com/dashpay/dash/wiki/Whitepaper) first theorised that Sybil attack resistant networks can be derived from cryptoeconomics. As an attacker accumulates Beldex, the circulating supply decreases, in turn applying demand-side pressure, driving the price of Beldex up. As this continues, it becomes increasingly costly for additional Beldex to be purchased, making the attack prohibitively expensive.

To achieve this economic protection, Beldex encourages the active suppression of the circulating supply. In particular, the [emissions curve](master-node-functions.md) and [collateral requirements](staking-requirement.md) must be designed to ensure enough circulating supply is locked and reasonable returns are provided for operators to ensure Sybil attack resistance

### Master Node Activities <a href="#master-node-activities" id="master-node-activities"></a>

Right now Master Nodes are full nodes on the Beldex network. Full nodes become Master Nodes when the owner [locks the required amount of Beldex](staking-requirement.md) for 30 days (2 days on testnet) and submits a registration transaction. Once accepted by the network, the Master Node is eligible to win [block rewards](https://www.beldex.io/whitepaper.pdf). Multiple participants can be involved in one Master Node and can have the reward automatically distributed.

### Guides & Resources <a href="#guides-resources" id="guides-resources"></a>

| **Guide/Resource**                                                    | **Description**                                                                                      |
| --------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Setting up Master Node**                                            | How to host and maintain a Master Node using the [CLI wallet](../wallets/guides/cli-linux-setup.md). |
| [**Updating your Master Node**](guides/master-node-update-guide.md)   | How to update your Master Node version.                                                              |
| [**Master Node RPC**](../advanced/developer/master-node-rpc-guide.md) | How to use JSON 2.0 RPC Calls with Master Nodes.                                                     |
| [**Active Master Node List**](https://explorer.beldex.io)             | Beldex Block explorer showing the current Master Node Pubkeys.                                       |
