# Overview

## Privacy Tokens

Privacy tokens are user-defined tokens issued on the Beldex blockchain. They use Beldex's private-token transaction model to conceal the amount and token identifier carried by an output while preserving verifiable ownership and supply rules.

Unlike BDX, a privacy token is created and managed by a token owner. The owner registers the token descriptor and can later mint additional units, up to the declared maximum supply, or update the token's metadata. Anyone holding units of the token can burn the units they control.

{% hint style="info" %}
Privacy tokens are available only after the privacy-token network upgrade is active. Make sure `beldexd` and `beldex-wallet-rpc` are synchronised and running compatible versions before using the token RPC methods.
{% endhint %}

### Token lifecycle

| Operation | Purpose                                                            | Who can perform it?                             |
| --------- | ------------------------------------------------------------------ | ----------------------------------------------- |
| Register  | Creates the token descriptor, token ID and optional initial supply | The registering wallet, which becomes the owner |
| Mint      | Creates additional units without exceeding `total_max_supply`      | The token owner                                 |
| Update    | Changes `meta_info`; immutable token fields are preserved          | The token owner                                 |
| Burn      | Permanently removes held units from circulation                    | A wallet that can spend the units being burned  |

Each token is identified by a 32-byte token ID returned by the registration transaction. Save this ID: the mint, update and burn RPC methods require it.

### Token descriptor

A token is registered with a JSON descriptor.

```json
{
  "ticker": "PRIV",
  "full_name": "Private Example Token",
  "total_max_supply": 100000000,
  "current_supply": 10000000,
  "decimal_point": 2,
  "meta_info": "https://example.com/token.json"
}
```

<table data-search="false"><thead><tr><th>Field</th><th>Required?</th><th>Description</th></tr></thead><tbody><tr><td><code>ticker</code></td><td>Yes</td><td>Token symbol. Must contain 1–14 ASCII letters or digits.</td></tr><tr><td><code>full_name</code></td><td>Yes</td><td>Display name, 1–64 characters. Letters, digits, spaces, <code>_</code>, <code>-</code> and <code>.</code> are accepted.</td></tr><tr><td><code>total_max_supply</code></td><td>Yes</td><td>Maximum lifetime supply in atomic token units. Must be greater than zero.</td></tr><tr><td><code>current_supply</code></td><td>No</td><td>Supply created during registration, in atomic token units. Defaults to <code>0</code> and cannot exceed <code>total_max_supply</code>.</td></tr><tr><td><code>decimal_point</code></td><td>No</td><td>Number of decimal places used to display token amounts. Defaults to <code>0</code>; maximum is <code>18</code>.</td></tr><tr><td><code>meta_info</code></td><td>No</td><td>Project-defined metadata, such as a URI or JSON string. Maximum length is 4,096 characters.</td></tr><tr><td><code>owner</code></td><td>No</td><td>Main wallet address or hex-encoded spend public key. When omitted, the registering wallet is used. If supplied through the wallet RPC, it must identify that wallet and cannot be a subaddress.</td></tr></tbody></table>

All supply and amount fields use **atomic token units**, not display units. For example, with `decimal_point` set to `2`, an RPC amount of `1250` represents `12.50` tokens.

{% hint style="warning" %}
The ticker, full name, maximum supply, decimal point and descriptor version are immutable after registration. Check the descriptor carefully before submitting it.
{% endhint %}

### What privacy tokens hide

Privacy-token outputs use confidential commitments and per-output token-ID blinding:

* The output amount is not recorded on-chain in plain text.
* The token ID associated with an ordinary token output is blinded.
* Ring signatures conceal which eligible output is actually spent.

The blockchain still reveals that a transaction contains privacy-token inputs or outputs, the number of those inputs and outputs, and the split between native BDX outputs and token outputs. Registration, mint, update and burn transactions also have identifiable transaction types. Privacy tokens therefore provide confidential amounts and token identifiers, not complete transaction-metadata invisibility.

### Ownership and supply

The network validates every lifecycle operation:

* Mint and update transactions require a proof from the token owner.
* Minting cannot increase the current supply beyond `total_max_supply`.
* A burn must spend existing outputs of the same token and cannot exceed the wallet's spendable token balance.
* Burned units are removed permanently and cannot be recovered.

For copy-ready JSON-RPC requests, see Privacy Token Wallet RPC Guide.
