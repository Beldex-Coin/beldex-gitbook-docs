# Sub Address

Subaddress is what you should be using by default to receive Beldex.

### Learn for what you are being paid <a href="#learn-for-what-you-are-being-paid" id="learn-for-what-you-are-being-paid"></a>

By providing a unique subaddress for each anticipated payment you will know for what you are being paid.

This use case overlaps with integrated addresses. Subaddresses are generally prefered for reasons outlined below.

### Prevent payer from linking your payouts together <a href="#prevent-payer-from-linking-your-payouts-together" id="prevent-payer-from-linking-your-payouts-together"></a>

To prevent the payer from linking your payouts together simply generate a new subaddress for each payout. This way services like [Shapeshift](https://shapeshift.io/) wouldn't know it is you again receving Beldex.

Note it won't help if you have an account with the service. Then your payouts are already linked in the service database, regardless of Beldex.

### Group funds into accounts <a href="#group-funds-into-accounts" id="group-funds-into-accounts"></a>

!!! Note Feel free to skip this if your are new to Beldex. Accounts are not essential and currently not supported by the GUI.

**Accounts** are a convenience wallet-level feature to group subaddresses under one label and balance.

You may want to organize your funds into accounts like "cash", "work", "trading", "mining", "donations", etc.

As accounts are only groupings of subaddresses, they themselves do not have an address.

Accounts are deterministically derived from the root private key along with subaddresses.

As of September 2018 accounts are only supported by the CLI wallet and missing from GUI wallet.

Accounts are similar to subaccounts in your classic bank account. There is a very important difference though. In Beldex funds don't really sit on accounts or public addresses. Public addresses are conceptually a gateway or a routing mechanism. Funds sit on transactions' unspent outputs. Thus, a single transaction can - in principle - aggregate and spend outputs from multiple addresses (and by extension from multiple accounts). The CLI or GUI wallet may not directly support creating such transactions for simplicity.

In short, think of accounts as a **soft** grouping of your funds.

### Why not multiple wallets? <a href="#why-not-multiple-wallets" id="why-not-multiple-wallets"></a>

The advantage over creating multiple wallets is that you only have a **single seed** to manage. All subaddresses can be derived from the wallet seed.

Additionally, you conveniently manage your subaddresses within a single user interface.

### Wallet level feature <a href="#wallet-level-feature" id="wallet-level-feature"></a>

Subaddresses and accounts are a wallet-level feature to construct and interpret transactions. They do not affect the consensus.&#x20;

### Data structure <a href="#data-structure" id="data-structure"></a>

Subaddress has a dedicated "network byte":

| Index | Size in bytes | Description                                                                                                                                                                                                                                                                                                                                  |
| ----- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 0     | 1             | identifies the network and address type; [116](https://github.com/beldex-coin/beldex/blob/master/src/cryptonote\_config.h#L183) - mainnet; [36](https://github.com/beldex-coin/beldex/blob/master/src/cryptonote\_config.h#L226) - stagenet; [158](https://github.com/beldex-coin/beldex/blob/master/src/cryptonote\_config.h#L203)- testnet |

Otherwise the data structure is the same as for the [main address](main-address.md).

### Generating <a href="#generating" id="generating"></a>

Each subaddress conceptually has:

* account index (also known as "major" index)
* subaddress index within the account (also known as "minor" index)

The indexes are 0-based. By default wallets use account index 0.

The indexes are not directly included in the subaddress data structure. Instead, they are used as input to generating subaddress keys.

#### Private view key <a href="#private-view-key" id="private-view-key"></a>

The subaddress private view key `m` is derived as follows:

```
m = Hs("SubAddr" || a || account_index || subaddress_index_within_account)
```

Where:

* `Hs` is a Keccak-256 hash function interpreted as integer and modulo `l` (maximum edwards25519 scalar)
* `||` is a byte array concatenation operator
* `SubAddr` is a 0-terminated fixed string (8 bytes total)
* `a` is a private view key of the main address (a 32 byte little endian unsigned integer)
* `account_index` is index of an account (a 32 bit little endian unsigned integer)
* `subaddress_index_within_account` is index of the subaddress within the account (a 32 bit little endian unsigned integer)

Deriving "sub view keys" from the main view key allows for creating a view only wallet that monitors the entire wallet including subaddresses.

#### Public spend key <a href="#public-spend-key" id="public-spend-key"></a>

The subaddress public spend key `D` is derived as follows:

```
D = B + m*G
```

Where:

* `B` is main address public spend key
* `m` is subaddress private view key
* `G` is the "base point"; this is simply a constant specific to edwards25519

#### Public view key <a href="#public-view-key" id="public-view-key"></a>

The subaddress public view key `C` is derived as follows:

```
C = a*D
```

Where:

* `a` is a private view key of the main address
* `D` is a public spend key of the subaddress

#### Special case for (0, 0) <a href="#special-case-for-0-0" id="special-case-for-0-0"></a>

The subaddress #0 on the account #0 is the [main address](main-address.md). As main address has different generation rules, this is simply implemented via an `if` statement.

#### Building the address string <a href="#building-the-address-string" id="building-the-address-string"></a>

The procedure is the same as for the [main address](main-address.md).

### Caveats <a href="#caveats" id="caveats"></a>

* It is not recommended to sweep all the balances of subaddress to main address in a single transaction. That links the subaddresses together on the blockchain. However, this only concerns privacy against specific sender and the situation will never get worse than not using subaddresses in the first place. If you need to join funds while preserving maximum privacy do it with individual transactions (one per subaddress).
* Convenience labels are not preserved when recreating from seed.

### Reference <a href="#reference" id="reference"></a>

* [monero-python](https://github.com/emesik/monero-python/blob/125d5eac0d4583b586b98e21b28fb9a291db26e5/monero/wallet.py#L195) - the easiest to follow implementation by Michał Sałaban
* [get\_subaddress\_spend\_public\_key()](https://github.com/monero-project/monero/blob/16dc6900fb556b61edaba5e323497e9b8c677ae2/src/device/device\_default.cpp#L143) - Monero reference implementation
* [historical discussion on Github](https://github.com/monero-project/monero/pull/2056) - gives context but is not up to date with all details
* [StackExchange answer](https://monero.stackexchange.com/questions/10674/how-are-subaddresses-and-account-addresses-generated-from-master-wallet-keys/10676#10676) - excellent summary by knaccc
