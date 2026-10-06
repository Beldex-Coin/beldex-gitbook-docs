# Privacy Token Guide

## Privacy Token Wallet RPC Guide

This guide explains how to register, mint, update and burn privacy tokens with `beldex-wallet-rpc`.

### Before you begin

You need:

* a synchronized `beldexd` node;
* a synchronized `beldex-wallet-rpc` wallet;
* unlocked BDX to pay the network fee and the applicable token-operation charge; and
* for mint and update, the wallet that owns the token.

The examples use the wallet RPC endpoint `http://127.0.0.1:19092/json_rpc`. Keep the RPC service private and configure `--rpc-login` when appropriate. If authentication is enabled, add `--digest -u USERNAME:PASSWORD` to each `curl` command.

{% hint style="warning" %}
The methods on this page create transactions and can move or permanently destroy tokens. Test your integration on a non-production network first. Never expose an unrestricted wallet RPC endpoint to the public internet.
{% endhint %}

### Common transaction parameters

The four methods accept some or all of these common parameters.

<table data-search="false"><thead><tr><th>Parameter</th><th>Type</th><th>Required?</th><th>Description</th></tr></thead><tbody><tr><td><code>account_index</code></td><td>unsigned integer</td><td>No</td><td>Wallet account used to pay BDX fees. Defaults to <code>0</code>. <code>update_token</code> must use account <code>0</code>.</td></tr><tr><td><code>subaddr_indices</code></td><td>array of unsigned integers</td><td>No</td><td>Subaddresses from which BDX fee inputs may be selected. Do not pass this field to <code>update_token</code>.</td></tr><tr><td><code>priority</code></td><td>unsigned integer</td><td>No</td><td>Transaction priority. <code>0</code> lets the wallet use its default behavior.</td></tr><tr><td><code>do_not_relay</code></td><td>boolean</td><td>No</td><td>If <code>true</code>, builds but does not broadcast the transaction. Defaults to <code>false</code>.</td></tr><tr><td><code>get_tx_key</code></td><td>boolean</td><td>No</td><td>Returns the transaction key when <code>true</code>. Treat the key as sensitive.</td></tr><tr><td><code>get_tx_hex</code></td><td>boolean</td><td>No</td><td>Returns the serialized transaction when <code>true</code>.</td></tr><tr><td><code>get_tx_metadata</code></td><td>boolean</td><td>No</td><td>Returns metadata for later transaction submission. Supported by mint, update and burn.</td></tr></tbody></table>

Amounts in these RPC calls are unsigned integers expressed in atomic token units. Native BDX values, including response fee fields, use atomic BDX units: **1 BDX = 1,000,000,000 atomic units**.

### Register a privacy token

`register_privacy_token` creates the token, assigns the wallet as its owner and returns the calculated token ID. If `current_supply` is greater than zero, that initial supply is issued to the registering wallet.

#### Inputs

<table data-search="false"><thead><tr><th>Parameter</th><th>Type</th><th>Required?</th><th>Description</th></tr></thead><tbody><tr><td><code>json_string</code></td><td>string</td><td>Yes</td><td>The complete token descriptor encoded as a JSON string.</td></tr><tr><td><code>account_index</code></td><td>unsigned integer</td><td>No</td><td>Account used for BDX inputs. Defaults to <code>0</code>.</td></tr><tr><td><code>subaddr_indices</code></td><td>array</td><td>No</td><td>Subaddresses used for BDX inputs.</td></tr><tr><td><code>priority</code></td><td>unsigned integer</td><td>No</td><td>Transaction priority.</td></tr><tr><td><code>do_not_relay</code></td><td>boolean</td><td>No</td><td>Build without broadcasting when <code>true</code>.</td></tr><tr><td><code>get_tx_key</code></td><td>boolean</td><td>No</td><td>Return the transaction key.</td></tr><tr><td><code>get_tx_hex</code></td><td>boolean</td><td>No</td><td>Return the serialized transaction in <code>tx_hex</code>.</td></tr></tbody></table>

#### Request

```bash
curl -X POST http://127.0.0.1:19092/json_rpc \
  -H 'Content-Type: application/json' \
  -d `{
  "jsonrpc": "2.0",
  "id": "0",
  "method": "register_privacy_token",
  "params": {
    "json_string": "{\"version\":1,\"ticker\":\"PRIV\",\"full_name\":\"Private Example Token\",\"total_max_supply\":100000000,\"current_supply\":10000000,\"decimal_point\":2,\"meta_info\":\"https://example.com/token.json\"}",
    "account_index": 0,
    "priority": 0,
    "get_tx_key": true,
    "get_tx_hex": false,
    "do_not_relay": false
  }
}`
```

#### Outputs

<table data-search="false"><thead><tr><th>Field</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><code>token_id</code></td><td>string</td><td>Hex-encoded 32-byte token ID. Use it for later lifecycle operations.</td></tr><tr><td><code>tx_hash</code></td><td>string</td><td>Registration transaction hash.</td></tr><tr><td><code>tx_key</code></td><td>string</td><td>Transaction key when requested; otherwise empty.</td></tr><tr><td><code>tx_hex</code></td><td>string</td><td>Serialized transaction when requested; otherwise empty.</td></tr><tr><td><code>ticker</code></td><td>string</td><td>Accepted ticker.</td></tr><tr><td><code>full_name</code></td><td>string</td><td>Accepted full name.</td></tr><tr><td><code>tx_fee</code></td><td>unsigned integer</td><td>Total transaction fee in atomic BDX units.</td></tr></tbody></table>

#### Example response

```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "token_id": "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
    "tx_hash": "bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb",
    "tx_key": "cccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccc",
    "tx_hex": "",
    "ticker": "PRIV",
    "full_name": "Private Example Token",
    "tx_fee": 1000123456789
  }
}
```

{% hint style="info" %}
The hashes, key and fee in this response are illustrative. Use the values returned by your wallet. On mainnet, registration currently also locks 10,000 BDX as collateral for 518,400 blocks and applies a 1,000 BDX operation charge, in addition to the ordinary network fee.
{% endhint %}

### Mint additional supply

`mint_token` creates more units of an existing token and sends them to the owner's primary wallet address. Only the token owner can mint. The resulting `current_supply` must not exceed `total_max_supply`.

#### Inputs

<table data-search="false"><thead><tr><th>Parameter</th><th>Type</th><th>Required?</th><th>Description</th></tr></thead><tbody><tr><td><code>token_id</code></td><td>string</td><td>Yes</td><td>Hex-encoded token ID returned during registration.</td></tr><tr><td><code>amount</code></td><td>unsigned integer</td><td>Yes</td><td>Amount to mint in atomic token units; must be greater than zero.</td></tr><tr><td><code>account_index</code></td><td>unsigned integer</td><td>No</td><td>Account used for BDX fee inputs.</td></tr><tr><td><code>subaddr_indices</code></td><td>array</td><td>No</td><td>Subaddresses used for BDX fee inputs.</td></tr><tr><td><code>priority</code></td><td>unsigned integer</td><td>No</td><td>Transaction priority.</td></tr><tr><td><code>do_not_relay</code></td><td>boolean</td><td>No</td><td>Build without broadcasting when <code>true</code>.</td></tr><tr><td><code>get_tx_key</code></td><td>boolean</td><td>No</td><td>Return the transaction key.</td></tr><tr><td><code>get_tx_hex</code></td><td>boolean</td><td>No</td><td>Return the serialized transaction in <code>tx_blob</code>.</td></tr><tr><td><code>get_tx_metadata</code></td><td>boolean</td><td>No</td><td>Return relay metadata.</td></tr></tbody></table>

#### Request

With `decimal_point: 2`, the example amount `250000` represents `2,500.00` tokens.

```bash
TOKEN_ID="aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"

curl -X POST http://127.0.0.1:19092/json_rpc \
  -H 'Content-Type: application/json' \
  -d '{
    "jsonrpc":"2.0",
    "id":"0",
    "method":"mint_token",
    "params":{
      "token_id":"'"$TOKEN_ID"'",
      "amount":250000,
      "account_index":0,
      "priority":0,
      "get_tx_key":true,
      "get_tx_hex":false,
      "get_tx_metadata":false,
      "do_not_relay":false
    }
  }'
```

#### Outputs

| Field         | Type             | Description                            |
| ------------- | ---------------- | -------------------------------------- |
| `tx_hash`     | string           | Mint transaction hash.                 |
| `tx_key`      | string           | Transaction key when requested.        |
| `fee`         | unsigned integer | Total fee in atomic BDX units.         |
| `tx_blob`     | string           | Serialized transaction when requested. |
| `tx_metadata` | string           | Relay metadata when requested.         |

Minting currently applies a 50 BDX mainnet operation charge in addition to the ordinary network fee.

### Update token metadata

`update_token` changes only the descriptor's `meta_info`. The wallet reads the live descriptor from the daemon and preserves all immutable fields. The transaction must be issued by the token owner's primary account.

#### Inputs

<table data-search="false"><thead><tr><th>Parameter</th><th>Type</th><th>Required?</th><th>Description</th></tr></thead><tbody><tr><td><code>token_id</code></td><td>string</td><td>Yes</td><td>Hex-encoded token ID.</td></tr><tr><td><code>json_string</code></td><td>string</td><td>One of these</td><td>Inline JSON containing the new <code>meta_info</code>. Recommended for RPC clients.</td></tr><tr><td><code>json_filename</code></td><td>string</td><td>One of these</td><td>Path to a descriptor file on the machine running <code>beldex-wallet-rpc</code>.</td></tr><tr><td><code>priority</code></td><td>unsigned integer</td><td>No</td><td>Transaction priority.</td></tr><tr><td><code>account_index</code></td><td>unsigned integer</td><td>No</td><td>Must be <code>0</code>.</td></tr><tr><td><code>do_not_relay</code></td><td>boolean</td><td>No</td><td>Build without broadcasting when <code>true</code>.</td></tr><tr><td><code>get_tx_key</code></td><td>boolean</td><td>No</td><td>Return the transaction key.</td></tr><tr><td><code>get_tx_hex</code></td><td>boolean</td><td>No</td><td>Return the serialized transaction in <code>tx_blob</code>.</td></tr><tr><td><code>get_tx_metadata</code></td><td>boolean</td><td>No</td><td>Return relay metadata.</td></tr></tbody></table>

Do not pass `subaddr_indices` to this method. The new `meta_info` must differ from the current value.

#### Request

```bash
TOKEN_ID="aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"

curl -X POST http://127.0.0.1:19092/json_rpc \
  -H 'Content-Type: application/json' \
  --data-binary @- <<JSON
{
  "jsonrpc": "2.0",
  "id": "0",
  "method": "update_token",
  "params": {
    "token_id": "$TOKEN_ID",
    "json_string": "{\"meta_info\":\"https://example.com/token-v2.json\"}",
    "account_index": 0,
    "priority": 0,
    "get_tx_key": true,
    "get_tx_hex": false,
    "get_tx_metadata": false,
    "do_not_relay": false
  }
}
JSON
```

#### Outputs

| Field         | Type             | Description                            |
| ------------- | ---------------- | -------------------------------------- |
| `tx_hash`     | string           | Update transaction hash.               |
| `tx_key`      | string           | Transaction key when requested.        |
| `fee`         | unsigned integer | Total fee in atomic BDX units.         |
| `tx_blob`     | string           | Serialized transaction when requested. |
| `tx_metadata` | string           | Relay metadata when requested.         |

Updating currently applies a 10 BDX mainnet operation charge in addition to the ordinary network fee.

### Burn token supply

`burn_token` permanently destroys the requested amount by spending token outputs controlled by the wallet. A burn cannot be reversed.

#### Inputs

| Parameter         | Type             | Required? | Description                                                      |
| ----------------- | ---------------- | --------- | ---------------------------------------------------------------- |
| `token_id`        | string           | Yes       | Hex-encoded token ID.                                            |
| `amount`          | unsigned integer | Yes       | Amount to burn in atomic token units; must be greater than zero. |
| `account_index`   | unsigned integer | No        | Account used for BDX fee inputs.                                 |
| `subaddr_indices` | array            | No        | Subaddresses used for BDX fee inputs and token selection.        |
| `priority`        | unsigned integer | No        | Transaction priority.                                            |
| `do_not_relay`    | boolean          | No        | Build without broadcasting when `true`.                          |
| `get_tx_key`      | boolean          | No        | Return the transaction key.                                      |
| `get_tx_hex`      | boolean          | No        | Return the serialized transaction in `tx_blob`.                  |
| `get_tx_metadata` | boolean          | No        | Return relay metadata.                                           |

#### Request

```bash
TOKEN_ID="aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa"

curl -X POST http://127.0.0.1:19092/json_rpc \
  -H 'Content-Type: application/json' \
  -d '{
    "jsonrpc":"2.0",
    "id":"0",
    "method":"burn_token",
    "params":{
      "token_id":"'"$TOKEN_ID"'",
      "amount":50000,
      "account_index":0,
      "priority":0,
      "get_tx_key":true,
      "get_tx_hex":false,
      "get_tx_metadata":false,
      "do_not_relay":false
    }
  }'
```

#### Outputs

| Field         | Type             | Description                            |
| ------------- | ---------------- | -------------------------------------- |
| `tx_hash`     | string           | Burn transaction hash.                 |
| `tx_key`      | string           | Transaction key when requested.        |
| `fee`         | unsigned integer | Total fee in atomic BDX units.         |
| `tx_blob`     | string           | Serialized transaction when requested. |
| `tx_metadata` | string           | Relay metadata when requested.         |

There is currently no additional mainnet operation charge for burning, but the ordinary network transaction fee still applies.

### Error handling

JSON-RPC failures return an `error` object rather than a `result` object.

```json
{
  "id": "0",
  "jsonrpc": "2.0",
  "error": {
    "code": -1,
    "message": "Error message from the wallet"
  }
}
```

Common causes include:

* the wallet or daemon is not synchronized;
* the privacy-token network upgrade is not active;
* the token ID is malformed or unknown;
* the wallet does not own the token for a mint or update;
* the mint would exceed the maximum supply;
* the wallet has insufficient unlocked BDX for fees or collateral;
* the wallet has insufficient unlocked token outputs for a burn; or
* an update repeats the existing `meta_info` value.

Only treat an operation as submitted when the response contains a `result` and a non-empty `tx_hash`. If `do_not_relay` is `true`, the transaction has been built but not broadcast.
