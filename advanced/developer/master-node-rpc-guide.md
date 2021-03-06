---
description: A detailed guide for Masternode RPC endpoints
---

# Master Node RPC Guide

## JSON 2.0 RPC Calls

### get\_quorum\_state

Get the quorum state which is the list of public keys of the nodes who are voting, and the list of public keys of the nodes who are being tested.

**Testnet Example**

```
    curl -X POST http://127.0.0.1:38157/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_quorum_state", "params": {"height": 200}}' -H 'Content-Type: application/json'
```

**Result**

```
    {
      "id": "0",
      "jsonrpc": "2.0",
      "result": {
        "nodes_to_test":
           ["578e5ee53150a3276dd3c411cb6313324a63b530cf3651f5c15e3d0ca58ceddd",
            …
            "c917034e9fcd0e9b0d423638664bbfc36eb8a2eeb68a1ff8bed8be5f699bc3c0"],
        "quorum_nodes":
           ["fc86a737756b6ed9f81233d22da3baee32537f3087901c3e94384be85ca1a9ee",
            …
            "ee597c5c7bbf1452e689a785f1133fc1355889b4111955d54cb5ed826cd35a32"],
        "status": "OK",
        "untrusted": false
      }
    }
```

Nodes have been omitted with “...” for brevity in nodes\_to\_test and quorum\_nodes.

**Inputs**

* Int height

> The height to query the quorum state for

**Outputs**

* String\[] nodes\_to\_test

> An array of public keys identifying service nodes which are being tested for the queried height.

* String\[] quorum\_state

> An array of public keys identifying service nodes which are responsible for voting on the queried height.

### get\_staking\_requirement

Get the required amount of Beldex to become a Master Node at the queried height. For stagenet and testnet values, ensure the daemon is started with the --stagenet or --testnet flags respectively.

**Testnet Example**

```
    curl -X POST http://127.0.0.1:38157/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_staking_requirement", "params": {“height”: 111111}}' -H 'Content-Type: application/json'  

```

**Result**

```
    {
      "id": "0",
      "jsonrpc": "2.0",
      "result": {
        "staking_requirement": 100000000000,
        "status": "OK"
      }
    }
```

**Inputs**

* Int height

> The height to query the staking requirement for

**Outputs**

* Uint64 staking\_requirement

> The staking requirement in Beldex atomic units for the queried height

### get\_master\_node\_key

Get the master node public key of the queried daemon. The daemon must be started in --maste-node mode otherwise this RPC command will fail.

**Testnet Example**

```
    curl -X POST http://127.0.0.1:38157/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_master_node_key"}' -H 'Content-Type: application/json'  

```

**Result**

```
    {
      "id": "0",
      "jsonrpc": "2.0",
      "result": {
        "master_node_pubkey": "8d56c1fa0304884e612ee2efe763b2c50991a66329418fd084a3f23c75399f34",
        "status": "OK"
      }
    }
```

**Inputs**

* N/A

**Outputs**

* String master\_node\_pubkey

> The public key identifying the queried master node

### **get\_master\_nodes**

Get the metadata currently associated with the queried master node public keys such as, registration height and contributors, etc. If no public key is specified, this returns all the metadata for every service node the queried daemon currently knows about.

**Testnet Example**

```
    curl -X POST http://127.0.0.1:38157/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_master_nodes", “params”: {“master_node_pubkeys”: []}}' -H 'Content-Type: application/json'
```

**Result**

```
    {
      "id": "0",
      "jsonrpc": "2.0",
      "result": {
        "master_node_states": [{
          "contributors": [{
            "address":    "86kZfTEf5JGw2SgLrGuxRNFxRTf51fvbbcCYW949RsKjX75JMA1B1d8CT4VbwfGR8uf3f3AJSTaBHGpN3QRG2N2LyiksWVg",
            "amount": 100000000000,
            "reserved": 100000000000
          }],
          "last_reward_block_height": 2968,
          "last_reward_transaction_index": 4294967295,
          "last_uptime_proof": 0,
          "operator_address": "86kZfTEf5JGw2SgLrGuxRNFxRTf51fvbbcCYW949RsKjX75JMA1B1d8CT4VbwfGR8uf3f3AJSTaBHGpN3QRG2N2LyiksWVg",
          "portions_for_operator": 18446744073709551612,
          "registration_height": 1860,
          "master_node_pubkey": "3afa36a4855a429f5eac1b2f8e7e77657a2e862999ab4d59e473826f9b15f2da",
          "staking_requirement": 100000000000,
          "total_contributed": 100000000000,
          "total_reserved": 100000000000
        }],
        "status": "OK"
      }
    }
```

**Inputs**

* String\[] master\_node\_pubkeys

> An array of master node public keys in strings that you wish to query metadata for. If an empty array is given, this RPC command returns all master nodes it knows about.

**Outputs**

* Entry\[] master\_node\_states

> The array of metadata for the queried master node(s)&#x20;

* String master\_node\_pubkey

> The queried master node’s identifying public key

* Uint64 registration\_height

> The height at which the registration transaction arrived on the blockchain

* Uint64 last\_reward\_block\_height

> The last block height this master node received a reward. Rewards are sent to service nodes whom have been waiting longest since their last reward and are then sent to the back of the queue.

* Uint64 last\_reward\_transaction\_index

> The position in the queue to receive a reward for the master nodes grouped in the last\_reward\_block\_height.

* Uint64 last\_uptime\_proof

> Unix epoch timestamp of the last time this daemon has received a ping from the queried master node.

* Contribution\[] contributors

> An array consisting of all the addresses that have contributed to the queried master node.

* Uint64 Contribution.amount

> The amount of Beldex in atomic units the contributor has staked.

* Uint64 Contribution.reserved

> The amount of Beldex in atomic units the contributor has reserved and must fulfill to completely contribute their part to the service node. Amount is equal to reserved once the contributor has fully contributed their part.

* String Contribution.address

> The Beldex address that funds must come from to fulfill the contribution requirement.

* Uint64 total\_contributed

> The total Beldex currently contributed going towards the staking requirement.

* Uint64 total\_reserved

> The total Beldex that has been reserved by all contributors. The remaining Beldex is open for other contributors to increase their stake towards the master node.

* Uint64 portions\_for\_operator

> The operator cut expressed as a value from 0 -> STAKING\_PORTIONS (defined in beldex/src/cryptonote\_config.h) which is the fee taken from the master node reward and given to the operator address before rewards are distributed to the contributors.

* Uint64 operator\_address

> The wallet address which is the primary owner of the master node and also the address which the operator cut is sent to.
