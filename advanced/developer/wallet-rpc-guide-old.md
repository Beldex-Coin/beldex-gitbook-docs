# Wallet RPC Guide

### &#x20;<a href="#introduction" id="introduction"></a>

### Introduction <a href="#introduction" id="introduction"></a>

This is a list of the beldex-wallet-rpc calls, their inputs and outputs, and examples of each. The program beldex-wallet-rpc replaced the rpc interface that was in simplewallet and then beldex-wallet-cli.

All beldex-wallet-rpc methods use the same JSON RPC interface. For example:

```
IP=127.0.0.1
PORT=19092
METHOD="make_integrated_address"
PARAMS="{\"payment_id\":\"1234567890123456789012345678900012345678901234567890123456789000\"}"
curl \
    -X POST http://$IP:$PORT/json_rpc \
    -d '{"jsonrpc":"2.0","id":"0","method":"'$METHOD'","params":'"$PARAMS"'}' \
    -H 'Content-Type: application/json'
```

If the beldex-wallet-rpc was executed with the `--rpc-login` argument as `username:password`, then follow this example:

```
IP=127.0.0.1
PORT=19092
METHOD="make_integrated_address"
PARAMS="{\"payment_id\":\"1234567890123456789012345678900012345678901234567890123456789000\"}"
curl \
    -u username:password --digest \
    -X POST http://$IP:$PORT/json_rpc \
    -d '{"jsonrpc":"2.0","id":"0","method":"'$METHOD'","params":'"$PARAMS"'}' \
    -H 'Content-Type: application/json'

```

Note: "atomic units" refer to the smallest fraction of 1 BDX according to the beldexd implementation. **1 BDX = 1e9 atomic units.**

#### Index of JSON RPC Methods: <a href="#index-of-json-rpc-methods" id="index-of-json-rpc-methods"></a>

* [get\_balance](wallet-rpc-guide-old.md#get_balance)
* [get\_address](wallet-rpc-guide-old.md#get_address)
* [get\_address\_index](wallet-rpc-guide-old.md#get_address_index)
* [create\_address](wallet-rpc-guide-old.md#create_address)
* [validate\_address](wallet-rpc-guide-old.md#label_address)
* [label\_address](wallet-rpc-guide-old.md#label_address)
* [get\_accounts](wallet-rpc-guide-old.md#get_accounts)
* [create\_account](wallet-rpc-guide-old.md#create_account)
* [label\_account](wallet-rpc-guide-old.md#label_account)
* [get\_account\_tags](wallet-rpc-guide-old.md#get_account_tags)
* [tag\_accounts](wallet-rpc-guide-old.md#tag_accounts)
* [untag\_accounts](wallet-rpc-guide-old.md#untag_accounts)
* [set\_account\_tag\_description](wallet-rpc-guide-old.md#set_account_tag_description)
* [get\_height](wallet-rpc-guide-old.md#get_height)
* [transfer](wallet-rpc-guide-old.md#transfer)
* [transfer\_split](wallet-rpc-guide-old.md#transfer_split)
* [sign\_transfer](wallet-rpc-guide-old.md#sign_transfer)
* [submit\_transfer](wallet-rpc-guide-old.md#submit_transfer)
* [sweep\_dust](wallet-rpc-guide-old.md#sweep_dust)
* [sweep\_all](wallet-rpc-guide-old.md#sweep_all)
* [sweep\_single](wallet-rpc-guide-old.md#sweep_single)
* [relay\_tx](wallet-rpc-guide-old.md#relay_tx)
* [store](wallet-rpc-guide-old.md#store)
* [get\_payments](wallet-rpc-guide-old.md#get_payments)
* [get\_bulk\_payments](wallet-rpc-guide-old.md#get_bulk_payments)
* [incoming\_transfers](wallet-rpc-guide-old.md#incoming_transfers)
* [query\_key](wallet-rpc-guide-old.md#query_key)
* [make\_integrated\_address](wallet-rpc-guide-old.md#make_integrated_address)
* [split\_integrated\_address](wallet-rpc-guide-old.md#split_integrated_address)
* [stop\_wallet](wallet-rpc-guide-old.md#stop_wallet)
* [rescan\_blockchain](wallet-rpc-guide-old.md#rescan_blockchain)
* [set\_tx\_notes](wallet-rpc-guide-old.md#set_tx_notes)
* [get\_tx\_notes](wallet-rpc-guide-old.md#get_tx_notes)
* [set\_attribute](wallet-rpc-guide-old.md#set_attribute)
* [get\_attribute](wallet-rpc-guide-old.md#get_attribute)
* [get\_tx\_key](wallet-rpc-guide-old.md#get_tx_key)
* [check\_tx\_key](wallet-rpc-guide-old.md#check_tx_key)
* [get\_tx\_proof](wallet-rpc-guide-old.md#get_tx_proof)
* [check\_tx\_proof](wallet-rpc-guide-old.md#check_tx_proof)
* [get\_spend\_proof](wallet-rpc-guide-old.md#get_spend_proof)
* [check\_spend\_proof](wallet-rpc-guide-old.md#check_spend_proof)
* [get\_reserve\_proof](wallet-rpc-guide-old.md#get_reserve_proof)
* [check\_reserve\_proof](wallet-rpc-guide-old.md#check_reserve_proof)
* [get\_transfers](wallet-rpc-guide-old.md#get_transfers)
* [get\_transfer\_by\_txid](wallet-rpc-guide-old.md#get_transfer_by_txid)
* [sign](wallet-rpc-guide-old.md#sign)
* [verify](wallet-rpc-guide-old.md#verify)
* [export\_outputs](wallet-rpc-guide-old.md#export_outputs)
* [import\_outputs](wallet-rpc-guide-old.md#import_outputs)
* [export\_key\_images](wallet-rpc-guide-old.md#export_key_images)
* [import\_key\_images](wallet-rpc-guide-old.md#import_key_images)
* [make\_uri](wallet-rpc-guide-old.md#make_uri)
* [parse\_uri](wallet-rpc-guide-old.md#parse_uri)
* [get\_address\_book](wallet-rpc-guide-old.md#get_address_book)
* [add\_address\_book](wallet-rpc-guide-old.md#add_address_book)
* [delete\_address\_book](wallet-rpc-guide-old.md#delete_address_book)
* [refresh](wallet-rpc-guide-old.md#refresh)
* [rescan\_spent](wallet-rpc-guide-old.md#rescan_spent)
* [start\_mining](wallet-rpc-guide-old.md#start_mining)
* [stop\_mining](wallet-rpc-guide-old.md#stop_mining)
* [get\_languages](wallet-rpc-guide-old.md#get_languages)
* [create\_wallet](wallet-rpc-guide-old.md#create_wallet)
* [open\_wallet](wallet-rpc-guide-old.md#open_wallet)
* [close\_wallet](wallet-rpc-guide-old.md#close_wallet)
* [change\_wallet\_password](wallet-rpc-guide-old.md#change_wallet_password)
* [is\_multisig](wallet-rpc-guide-old.md#is_multisig)
* [prepare\_multisig](wallet-rpc-guide-old.md#prepare_multisig)
* [make\_multisig](wallet-rpc-guide-old.md#make_multisig)
* [export\_multisig\_info](wallet-rpc-guide-old.md#export_multisig_info)
* [import\_multisig\_info](wallet-rpc-guide-old.md#import_multisig_info)
* [finalize\_multisig](wallet-rpc-guide-old.md#finalize_multisig)
* [sign\_multisig](wallet-rpc-guide-old.md#sign_multisig)
* [submit\_multisig](wallet-rpc-guide-old.md#submit_multisig)
* [get\_version](wallet-rpc-guide-old.md#get_version)
* [bns\_buy\_mapping](wallet-rpc-guide-old.md#sources)
* [bns\_renew\_mapping](wallet-rpc-guide-old.md#sources-1)
* [bns\_update\_mapping](wallet-rpc-guide-old.md#sources-2)
* [bns\_make\_update\_mapping\_signature](wallet-rpc-guide-old.md#sources-3)
* [bns\_hash\_name](wallet-rpc-guide-old.md#sources-4)
* [bns\_known\_names](wallet-rpc-guide-old.md#sources-5)
* [bns\_add\_known\_names](wallet-rpc-guide-old.md#sources-6)
* [bns\_encrypt\_value](wallet-rpc-guide-old.md#sources-7)
* [bns\_decrypt\_value](wallet-rpc-guide-old.md#sources-8)
* [coin\_burn](wallet-rpc-guide-old.md#sources-9)

### JSON RPC Methods: <a href="#json-rpc-methods" id="json-rpc-methods"></a>

### **get\_balance** <a href="#get_balance" id="get_balance"></a>

Return the wallet's balance.

Alias: _getbalance_.

Inputs:

* _account\_index_ - unsigned int; Return balance for this account.
* _address\_indices_ - array of unsigned int; (Optional) Return balance detail for those subaddresses.

Outputs:

* _balance_ - unsigned int; The total balance of the current beldex-wallet-rpc in session.
* _unlocked\_balance_ - unsigned int; Unlocked funds are those funds that are sufficiently deep enough in the beldex blockchain to be considered safe to spend.
* _multisig\_import\_needed_ - boolean; True if importing multisig data is needed for returning a correct balance.
* _per\_subaddress_ - array of subaddress information; Balance information for each subaddress in an account.
  * _address\_index_ - unsigned int; Index of the subaddress in the account.
  * _address_ - string; Address at this index. Base58 representation of the public keys.
  * _balance_ - unsigned int; Balance for the subaddress (locked or unlocked).
  * _unlocked\_balance_ - unsigned int; Unlocked balance for the subaddress.
  * _label_ - string; Label for the subaddress.
  * _num\_unspent\_outputs_ - unsigned int; Number of unspent outputs available for the subaddress.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_balance","params":{"account_index":0,"address_indices":[0,1]}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "balance": 157443303037455077,
    "multisig_import_needed": false,
    "per_subaddress": [{
      "address": "83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "address_index": 0,
      "balance": 157360317826255077,
      "label": "Primary account",
      "num_unspent_outputs": 5281,
      "unlocked_balance": 157360317826255077
    },{
      "address": "8BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
      "address_index": 1,
      "balance": 59985211200000,
      "label": "",
      "num_unspent_outputs": 1,
      "unlocked_balance": 59985211200000
    }],
    "unlocked_balance": 157443303037455077
  }
}

```

### **get\_address** <a href="#get_address" id="get_address"></a>

Return the wallet's addresses for an account. Optionally filter for specific set of subaddresses.

Alias: _getaddress_.

Inputs:

* _account\_index_ - unsigned int; Return subaddresses for this account.
* _address\_index_ - array of unsigned int; (Optional) List of subaddresses to return from an account.

Outputs:

* _address_ - string; The 95-character hex address string of the beldex-wallet-rpc in session.
* _addresses_ array of addresses informations
  * _address_ string; The 95-character hex (sub)address string.
  * _label_ string; Label of the (sub)address
  * _address\_index_ unsigned int; index of the subaddress
  * _used_ boolean; states if the (sub)address has already received funds

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_address","params":{"account_index":0,"address_index":[0,1,4]}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "address": "83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
    "addresses": [{
      "address": "83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "address_index": 0,
      "label": "Primary account",
      "used": true
    },{
      "address": "8BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
      "address_index": 1,
      "label": "",
      "used": true
    },{
      "address": "87xa6Dha7kzCQuvmd8iB5VYoMkdenwCNRU9khGhExXQ8KLL3z1N1ZATBD1sFPenyHWT9cm4fVFnCAUApY53peuoZFtwZiw5",
      "address_index": 4,
      "label": "test2",
      "used": true
    }]
  }
}

```

### **get\_address\_index** <a href="#get_address_index" id="get_address_index"></a>

Get account and address indexes from a specific (sub)address

Alias: _None_.

Inputs:

* _address_ - String; (sub)address to look for.

Outputs:

* _index_ - subaddress informations
  * _major_ unsigned int; Account index.
  * _minor_ unsigned int; Address index.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_address_index","params":{"address":"8BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "index": {
      "major": 0,
      "minor": 1
    }
  }
}

```

### **create\_address** <a href="#create_address" id="create_address"></a>

Create a new address for an account. Optionally, label the new address.

Alias: _None_.

Inputs:

* _account\_index_ - unsigned int; Create a new address for this account.
* _label_ - string; (Optional) Label for the new address.

Outputs:

* _address_ - string; Newly created address. Base58 representation of the public keys.
* _address\_index_ - unsigned int; Index of the new address under the input account.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"create_address","params":{"account_index":0,"label":"new-sub"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "address": "7BG5jr9QS5sGMdpbBrZEwVLZjSKJGJBsXdZLt8wiXyhhLjy7x2LZxsrAnHTgD8oG46ZtLjUGic2pWc96GFkGNPQQDA3Dt7Q",
    "address_index": 5
  }
}

```

### validate\_address <a href="#label_address" id="label_address"></a>

Performs address validation and determines the corresponding network classification.

Inputs:

* address (string, **required**)
  * &#x20;The address to be validated.
* any\_net\_type (bool, **optional**)
  * If set to `true`, allows detection of addresses from any network type (mainnet, testnet or devnet). Default is `false`.

Outputs:

* nettype (string)
  * The network type associated with the address (`mainnet`, `testnet` or `devnet`).
* integrated (bool)
  * Indicates whether the address is an integrated address (`true`) or not (`false`).
* subaddress (bool)
  * Indicates whether the address is a subaddress (`true`) or a standard address (`false`).
* valid (bool)
  * Returns `true` if the address is valid, otherwise `false`.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"validate_address","params":{"address":"bxcVLYgjDBZDJqCtnrEE2fhTG7r1WyrMLdX3fC22NkQm35B7MM7mU8kN5xvqKAdQTAivPFR7duNauVhXKE17BTqh2kMtAqgXs","any_net_type":true}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "integrated": false,
    "nettype": "mainnet",
    "openalias_address": "",
    "subaddress": false,
    "valid": true
  }
}
```

### **label\_address** <a href="#label_address" id="label_address"></a>

Label an address.

Alias: _None_.

Inputs:

* _index_ - subaddress index; JSON Object containing the major & minor address index:
  * _major_ - unsigned int; Account index for the subaddress.
  * _minor_ - unsigned int; Index of the subaddress in the account.
* _label_ - string; Label for the address.

Outputs: _None_.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"label_address","params":{"index":{"major":0,"minor":5},"label":"myLabel"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **get\_accounts** <a href="#get_accounts" id="get_accounts"></a>

Get all accounts for a wallet. Optionally filter accounts by tag.

Alias: _None_.

Inputs:

* _tag_ - string; (Optional) Tag for filtering accounts.

Outputs:

* _subaddress\_accounts_ - array of subaddress account information:
  * _account\_index_ - unsigned int; Index of the account.
  * _balance_ - unsigned int; Balance of the account (locked or unlocked).
  * _base\_address_ - string; Base64 representation of the first subaddress in the account.
  * _label_ - string; (Optional) Label of the account.
  * _tag_ - string; (Optional) Tag for filtering accounts.
  * _unlocked\_balance_ - unsigned int; Unlocked balance for the account.
* _total\_balance_ - unsigned int; Total balance of the selected accounts (locked or unlocked).
* _total\_unlocked\_balance_ - unsigned int; Total unlocked balance of the selected accounts.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_accounts","params":{"tag":"myTag"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "subaddress_accounts": [{
      "account_index": 0,
      "balance": 157663195572433688,
      "base_address": "83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "label": "Primary account",
      "tag": "myTag",
      "unlocked_balance": 157443303037455077
    },{
      "account_index": 1,
      "balance": 0,
      "base_address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
      "label": "Secondary account",
      "tag": "myTag",
      "unlocked_balance": 0
    }],
    "total_balance": 157663195572433688,
    "total_unlocked_balance": 157443303037455077
  }
}

```

### **create\_account** <a href="#create_account" id="create_account"></a>

Create a new account with an optional label.

Alias: _None_.

Inputs:

* _label_ - string; (Optional) Label for the account.

Outputs:

* _account\_index_ - unsigned int; Index of the new account.
* _address_ - string; Address for this account. Base58 representation of the public keys.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"create_account","params":{"label":"Secondary account"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "account_index": 1,
    "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp"
  }
}

```

### **label\_account** <a href="#label_account" id="label_account"></a>

Label an account.

Alias: _None_.

Inputs:

* _account\_index_ - unsigned int; Apply label to account at this index.
* _label_ - string; Label for the account.

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"label_account","params":{"account_index":0,"label":"Primary account"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "account_tags": [{
      "accounts": [0,1],
      "label": "",
      "tag": "myTag"
    }]
  }
}

```

### **get\_account\_tags** <a href="#get_account_tags" id="get_account_tags"></a>

Get a list of user-defined account tags.

Alias: _None_.

Inputs: _None_.

Outputs:

* _account\_tags_ - array of account tag information:
  * _tag_ - string; Filter tag.
  * _label_ - string; Label for the tag.
  * _accounts_ - array of int; List of tagged account indices.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_account_tags","params":""}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "account_tags": [{
      "accounts": [0],
      "label": "Test tag",
      "tag": "myTag"
    }]
  }
}

```

### **tag\_accounts** <a href="#tag_accounts" id="tag_accounts"></a>

Apply a filtering tag to a list of accounts.

Alias: _None_.

Inputs:

* _tag_ - string; Tag for the accounts.
* _accounts_ - array of unsigned int; Tag this list of accounts.

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"tag_accounts","params":{"tag":"myTag","accounts":[0,1]}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **untag\_accounts** <a href="#untag_accounts" id="untag_accounts"></a>

Remove filtering tag from a list of accounts.

Alias: _None_.

Inputs:

* _accounts_ - array of unsigned int; Remove tag from this list of accounts.

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"untag_accounts","params":{"accounts":[1]}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **set\_account\_tag\_description** <a href="#set_account_tag_description" id="set_account_tag_description"></a>

Set description for an account tag.

Alias: _None_.

Inputs:

* _tag_ - string; Set a description for this tag.
* _description_ - string; Description for the tag.

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"set_account_tag_description","params":{"tag":"myTag","description":"Test tag"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **get\_height** <a href="#get_height" id="get_height"></a>

Returns the wallet's current block height.

Alias: _getheight_.

Inputs: _None_.

Outputs:

* _height_ - unsigned int; The current beldex-wallet-rpc's blockchain height. If the wallet has been offline for a long time, it may need to catch up with the daemon.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_height"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "height": 145545
  }
}

```

### **transfer** <a href="#transfer" id="transfer"></a>

Send beldex to a number of recipients.

Alias: _None_.

Inputs:

* _destinations_ - array of destinations to receive BDX:
  * _amount_ - unsigned int; Amount to send to each destination, in atomic units.
  * _address_ - string; Destination public address.
* _account\_index_ - unsigned int; (Optional) Transfer from this account index. (Defaults to 0)
* _subaddr\_indices_ - array of unsigned int; (Optional) Transfer from this set of subaddresses. (Defaults to 0)
* _priority_ - unsigned int; Set a priority for the transaction. Accepted Values are: 0 and 1 for: flash and unimportant.
* _mixin_ - unsigned int; Number of outputs from the blockchain to mix with (0 means no mixing).
* _ring\_size_ - unsigned int; Number of outputs to mix in the transaction (this output + N decoys from the blockchain).
* _unlock\_time_ - unsigned int; Number of blocks before the beldex can be spent (0 to not add a lock).
* _payment\_id_ - string; (Optional) Random 32-byte/64-character hex string to identify a transaction.
* _get\_tx\_key_ - boolean; (Optional) Return the transaction key after sending.
* _do\_not\_relay_ - boolean; (Optional) If true, the newly created transaction will not be relayed to the beldex network. (Defaults to false)
* _get\_tx\_hex_ - boolean; Return the transaction as hex string after sending (Defaults to false)
* _get\_tx\_metadata_ - boolean; Return the metadata needed to relay the transaction. (Defaults to false)

Outputs:

* _amount_ - Amount transferred for the transaction.
* _fee_ - Integer value of the fee charged for the txn.
* _multisig\_txset_ - Set of multisig transactions in the process of being signed (empty for non-multisig).
* _tx\_blob_ - Raw transaction represented as hex string, if get\_tx\_hex is true.
* _tx\_hash_ - String for the publically searchable transaction hash.
* _tx\_key_ - String for the transaction key if get\_tx\_key is true, otherwise, blank string.
* _tx\_metadata_ - Set of transaction metadata needed to relay this transfer later, if get\_tx\_metadata is true.
* _unsigned\_txset_ - String. Set of unsigned tx for cold-signing purposes.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"transfer","params":{"destinations":[{"amount":100000000000,"address":"8BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"},{"amount":200000000000,"address":"75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv"}],"account_index":0,"subaddr_indices":[0],"priority":1,"ring_size":7,"get_tx_key": true}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount": 300000000000,
    "fee": 86897600000,
    "multisig_txset": "",
    "tx_blob": "",
    "tx_hash": "7663438de4f72b25a0e395b770ea9ecf7108cd2f0c4b75be0b14a103d3362be9",
    "tx_key": "25c9d8ec20045c80c93d665c9d3684aab7335f8b2cd02e1ba2638485afd1c70e236c4bdd7a2f1cb511dbf466f13421bdf8df988b7b969c448ca6239d7251490e4bf1bbf9f6ffacffdcdc93b9d1648ec499eada4d6b4e02ce92d4a1c0452e5d009fbbbf15b549df8856205a4c7bda6338d82c823f911acd00cb75850b198c5803",
    "tx_metadata": "",
    "unsigned_txset": ""
  }
}

```

### **transfer\_split** <a href="#transfer_split" id="transfer_split"></a>

Same as transfer, but can split into more than one tx if necessary.

Alias: _None_.

Inputs:

* _destinations_ - array of destinations to receive BDX:
  * _amount_ - unsigned int; Amount to send to each destination, in atomic units.
  * _address_ - string; Destination public address.
* _account\_index_ - unsigned int; (Optional) Transfer from this account index. (Defaults to 0)
* _subaddr\_indices_ - array of unsigned int; (Optional) Transfer from this set of subaddresses. (Defaults to 0)
* _mixin_ - unsigned int; Number of outputs from the blockchain to mix with (0 means no mixing).
* _ring\_size_ - unsigned int; Sets ringsize to n (mixin + 1).
* _unlock\_time_ - unsigned int; Number of blocks before the beldex can be spent (0 to not add a lock).
* _payment\_id_ - string; (Optional) Random 32-byte/64-character hex string to identify a transaction.
* _get\_tx\_keys_ - boolean; (Optional) Return the transaction keys after sending.
* _priority_ - unsigned int; Set a priority for the transactions. Accepted Values are: 0-3 for: default, unimportant, normal, elevated, priority.
* _do\_not\_relay_ - boolean; (Optional) If true, the newly created transaction will not be relayed to the beldex network. (Defaults to false)
* _get\_tx\_hex_ - boolean; Return the transactions as hex string after sending
* _new\_algorithm_ - boolean; True to use the new transaction construction algorithm, defaults to false.
* _get\_tx\_metadata_ - boolean; Return list of transaction metadata needed to relay the transfer later.

Outputs:

* _tx\_hash\_list_ - array of: string. The tx hashes of every transaction.
* _tx\_key\_list_ - array of: string. The transaction keys for every transaction.
* _amount\_list_ - array of: integer. The amount transferred for every transaction.
* _fee\_list_ - array of: integer. The amount of fees paid for every transaction.
* _tx\_blob\_list_ - array of: string. The tx as hex string for every transaction.
* _tx\_metadata\_list_ - array of: string. List of transaction metadata needed to relay the transactions later.
* _multisig\_txset_ - string. The set of signing keys used in a multisig transaction (empty for non-multisig).
* _unsigned\_txset_ - string. Set of unsigned tx for cold-signing purposes.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"transfer_split","params":{"destinations":[{"amount":1000000000000,"address":"8BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"},{"amount":2000000000000,"address":"75sNpRwUtekcJGejMuLSGA71QFuK1qcCVLZnYRTfQLgFU5nJ7xiAHtR5ihioS53KMe8pBhH61moraZHyLoG4G7fMER8xkNv"}],"account_index":0,"subaddr_indices":[0],"priority":0,"ring_size":7,"get_tx_key": true}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount_list": [3000000000000],
    "fee_list": [85106400000],
    "multisig_txset": "",
    "tx_hash_list": ["c8d815f48f27d53fdaf198a74b292a91bfaf87529a9a9a9ee66079a890b3b58b"],
    "unsigned_txset": ""
  }
}

```

### **sign\_transfer** <a href="#sign_transfer" id="sign_transfer"></a>

Sign a transaction created on a read-only wallet (in cold-signing process)

Alias: _None_.

Inputs:

* _unsigned\_txset_ - string. Set of unsigned tx returned by "transfer" or "transfer\_split" methods.
* _export\_raw_ - boolean; (Optional) If true, return the raw transaction data. (Defaults to false)

Outputs:

* _signed\_txset_ - string. Set of signed tx to be used for submitting transfer.
* _tx\_hash\_list_ - array of: string. The tx hashes of every transaction.
* _tx\_raw\_list_ - array of: string. The tx raw data of every transaction.

In the example below, we first generate an unsigned\_txset on a read only wallet before signing it:

Generate unsigned\_txset using the above "transfer" method on read-only wallet:

```
curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"transfer","params":{"destinations":[{"amount":1000000000000,"address":"8BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"}],"account_index":0,"subaddr_indices":[0],"priority":0,"ring_size":7,"do_not_relay":true,"get_tx_hex":true}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount": 1000000000000,
    "fee": 15202740000,
    "multisig_txset": "",
    "tx_blob": "...long_hex...",
    "tx_hash": "c648ba0a049e5ce4ec21361dbf6e4b21eac0f828eea9090215de86c76b31d0a4",
    "tx_key": "",
    "tx_metadata": "",
    "unsigned_txset": "...long_hex..."
  }
}

```

Sign tx using the previously generated unsigned\_txset

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sign_transfer","params":{"unsigned_txset":...long_hex..."}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signed_txset": "...long_hex...",
    "tx_hash_list": ["ff2e2d49fbfb1c9a55754f786576e171c8bf21b463a74438df604b7fa6cebc6d"]
  }
}

```

### **submit\_transfer** <a href="#submit_transfer" id="submit_transfer"></a>

Submit a previously signed transaction on a read-only wallet (in cold-signing process).

Alias: _None_.

Inputs:

* _tx\_data\_hex_ - string; Set of signed tx returned by "sign\_transfer"

Outputs:

* _tx\_hash\_list_ - array of: string. The tx hashes of every transaction.

In the example below, we submit the transfer using the signed\_txset generated above:

```
curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"submit_transfer","params":{"tx_data_hex":...long_hex..."}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "tx_hash_list": ["40fad7c828bb383ac02648732f7afce9adc520ba5629e1f5d9c03f584ac53d74"]
  }
}

```

### **sweep\_dust** <a href="#sweep_dust" id="sweep_dust"></a>

Send all dust outputs back to the wallet's, to make them easier to spend (and mix).

Alias: _sweep\_unmixable_.

Inputs:

* _get\_tx\_keys_ - boolean; (Optional) Return the transaction keys after sending.
* _do\_not\_relay_ - boolean; (Optional) If true, the newly created transaction will not be relayed to the beldex network. (Defaults to false)
* _get\_tx\_hex_ - boolean; (Optional) Return the transactions as hex string after sending. (Defaults to false)
* _get\_tx\_metadata_ - boolean; (Optional) Return list of transaction metadata needed to relay the transfer later. (Defaults to false)

Outputs:

* _tx\_hash\_list_ - array of: string. The tx hashes of every transaction.
* _tx\_key\_list_ - array of: string. The transaction keys for every transaction.
* _amount\_list_ - array of: integer. The amount transferred for every transaction.
* _fee\_list_ - array of: integer. The amount of fees paid for every transaction.
* _tx\_blob\_list_ - array of: string. The tx as hex string for every transaction.
* _tx\_metadata\_list_ - array of: string. List of transaction metadata needed to relay the transactions later.
* _multisig\_txset_ - string. The set of signing keys used in a multisig transaction (empty for non-multisig).
* _unsigned\_txset_ - string. Set of unsigned tx for cold-signing purposes.

Example (In this example, `sweep_dust` returns nothing because there are no funds to sweep):

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sweep_dust","params":{"get_tx_keys":true}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "multisig_txset": "",
    "unsigned_txset": ""
  }
}

```

### **sweep\_all** <a href="#sweep_all" id="sweep_all"></a>

Send all unlocked balance to an address.

Alias: _None_.

Inputs:

* _address_ - string; Destination public address.
* _account\_index_ - unsigned int; Sweep transactions from this account.
* _subaddr\_indices_ - array of unsigned int; (Optional) Sweep from this set of subaddresses in the account.
* _priority_ - unsigned int; (Optional) Priority for sending the sweep transfer, partially determines fee.
* _mixin_ - unsigned int; Number of outputs from the blockchain to mix with (0 means no mixing).
* _ring\_size_ - unsigned int; Sets ringsize to n (mixin + 1).
* _unlock\_time_ - unsigned int; Number of blocks before the beldex can be spent (0 to not add a lock).
* _payment\_id_ - string; (Optional) Random 32-byte/64-character hex string to identify a transaction.
* _get\_tx\_keys_ - boolean; (Optional) Return the transaction keys after sending.
* _below\_amount_ - unsigned int; (Optional) Include outputs below this amount.
* _do\_not\_relay_ - boolean; (Optional) If true, do not relay this sweep transfer. (Defaults to false)
* _get\_tx\_hex_ - boolean; (Optional) return the transactions as hex encoded string. (Defaults to false)
* _get\_tx\_metadata_ - boolean; (Optional) return the transaction metadata as a string. (Defaults to false)

Outputs:

* _tx\_hash\_list_ - array of: string. The tx hashes of every transaction.
* _tx\_key\_list_ - array of: string. The transaction keys for every transaction.
* _amount\_list_ - array of: integer. The amount transferred for every transaction.
* _fee\_list_ - array of: integer. The amount of fees paid for every transaction.
* _tx\_blob\_list_ - array of: string. The tx as hex string for every transaction.
* _tx\_metadata\_list_ - array of: string. List of transaction metadata needed to relay the transactions later.
* _multisig\_txset_ - string. The set of signing keys used in a multisig transaction (empty for non-multisig).
* _unsigned\_txset_ - string. Set of unsigned tx for cold-signing purposes.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sweep_all","params":{"address":"83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","subaddr_indices":[4],"ring_size":7,"unlock_time":0,"get_tx_keys":true}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount_list": [9985885770000],
    "fee_list": [14114230000],
    "multisig_txset": "",
    "tx_hash_list": ["ab4b6b65cc8cd8c9dd317d0b90d97582d68d0aa1637b0065b05b61f9a66ea5c5"],
    "tx_key_list": ["b9b4b39d3bb3062ddb85ec0266d4df39058f4c86077d99309f218ce4d76af607"],
    "unsigned_txset": ""
  }
}

```

### **sweep\_single** <a href="#sweep_single" id="sweep_single"></a>

Send all of a specific unlocked output to an address.

Alias: _None_.

Inputs:

* _address_ - string; Destination public address.
* _account\_index_ - unsigned int; Sweep transactions from this account.
* _subaddr\_indices_ - array of unsigned int; (Optional) Sweep from this set of subaddresses in the account.
* _priority_ - unsigned int; (Optional) Priority for sending the sweep transfer, partially determines fee.
* _mixin_ - unsigned int; Number of outputs from the blockchain to mix with (0 means no mixing).
* _ring\_size_ - unsigned int; Sets ringsize to n (mixin + 1).
* _unlock\_time_ - unsigned int; Number of blocks before the beldex can be spent (0 to not add a lock).
* _payment\_id_ - string; (Optional) Random 32-byte/64-character hex string to identify a transaction.
* _get\_tx\_keys_ - boolean; (Optional) Return the transaction keys after sending.
* _key\_image_ - string; Key image of specific output to sweep.
* _below\_amount_ - unsigned int; (Optional) Include outputs below this amount.
* _do\_not\_relay_ - boolean; (Optional) If true, do not relay this sweep transfer. (Defaults to false)
* _get\_tx\_hex_ - boolean; (Optional) return the transactions as hex encoded string. (Defaults to false)
* _get\_tx\_metadata_ - boolean; (Optional) return the transaction metadata as a string. (Defaults to false)

Outputs:

* _tx\_hash\_list_ - array of: string. The tx hashes of every transaction.
* _tx\_key\_list_ - array of: string. The transaction keys for every transaction.
* _amount\_list_ - array of: integer. The amount transferred for every transaction.
* _fee\_list_ - array of: integer. The amount of fees paid for every transaction.
* _tx\_blob\_list_ - array of: string. The tx as hex string for every transaction.
* _tx\_metadata\_list_ - array of: string. List of transaction metadata needed to relay the transactions later.
* _multisig\_txset_ - string. The set of signing keys used in a multisig transaction (empty for non-multisig).
* _unsigned\_txset_ - string. Set of unsigned tx for cold-signing purposes.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sweep_single","params":{"address":"74Jsocx8xbpTBEjm3ncKE5LBQbiJouyCDaGhgSiebpvNDXZnTAbW2CmUR5SsBeae2pNk9WMVuz6jegkC4krUyqRjA6VjoLD","ring_size":7,"unlock_time":0,"key_image":"a7834459ef795d2efb6f665d2fd758c8d9288989d8d4c712a68f8023f7804a5e","get_tx_keys":true}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount": 27126892247503,
    "fee": 14111630000,
    "multisig_txset": "",
    "tx_blob": "",
    "tx_hash": "106d4391a031e5b735ded555862fec63233e34e5fa4fc7edcfdbe461c275ae5b",
    "tx_key": "",
    "tx_metadata": "",
    "unsigned_txset": ""
  }
}

```

### **relay\_tx** <a href="#relay_tx" id="relay_tx"></a>

Relay a transaction previously created with `"do_not_relay":true`.

Alias: _None_.

Inputs:

* _hex_ - string; transaction metadata returned from a `transfer` method with `get_tx_metadata` set to `true`.

Outputs:

* _tx\_hash_ - String for the publically searchable transaction hash.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"relay_tx","params":{"hex":"...tx_metadata..."}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "tx_hash": "1c42dcc5672bb09bccf33fb1e9ab4a498af59a6dbd33b3d0cfb289b9e0e25fa5"
  }
}

```

### **store** <a href="#store" id="store"></a>

Save the wallet file.

Alias: _None_.

Inputs: _None_.

Outputs: _None_.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"store"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **get\_payments** <a href="#get_payments" id="get_payments"></a>

Get a list of incoming payments using a given payment id.

Alias: _None_.

Inputs:

* _payment\_id_ - string; Payment ID used to find the payments (16 characters hex).

Outputs:

* _payments_ - list of:
  * _payment\_id_ - string; Payment ID matching the input parameter.
  * _tx\_hash_ - string; Transaction hash used as the transaction ID.
  * _amount_ - unsigned int; Amount for this payment.
  * _block\_height_ - unsigned int; Height of the block that first confirmed this payment.
  * _unlock\_time_ - unsigned int; Time (in block height) until this payment is safe to spend.
  * _subaddr\_index_ - subaddress index:
    * _major_ - unsigned int; Account index for the subaddress.
    * _minor_ - unsigned int; Index of the subaddress in the account.
  * _address_ - string; Address receiving the payment; Base58 representation of the public keys.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_payments","params":{"payment_id":"60900e5603bf96e3"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "payments": [{
      "address": "83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "amount": 1000000000000,
      "block_height": 127606,
      "payment_id": "60900e5603bf96e3",
      "subaddr_index": {
        "major": 0,
        "minor": 0
      },
      "tx_hash": "3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f",
      "unlock_time": 0
    }]
  }
}

```

### **get\_bulk\_payments** <a href="#get_bulk_payments" id="get_bulk_payments"></a>

Get a list of incoming payments using a given payment id, or a list of payments ids, from a given height. This method is the preferred method over `get_payments`because it has the same functionality but is more extendable. Either is fine for looking up transactions by a single payment ID.

Alias: _None_.

Inputs:

* _payment\_ids_ - array of: string; Payment IDs used to find the payments (16 characters hex).
* _min\_block\_height_ - unsigned int; The block height at which to start looking for payments.

Outputs:

* _payments_ - list of:
  * _payment\_id_ - string; Payment ID matching one of the input IDs.
  * _tx\_hash_ - string; Transaction hash used as the transaction ID.
  * _amount_ - unsigned int; Amount for this payment.
  * _block\_height_ - unsigned int; Height of the block that first confirmed this payment.
  * _unlock\_time_ - unsigned int; Time (in block height) until this payment is safe to spend.
  * _subaddr\_index_ - subaddress index:
    * _major_ - unsigned int; Account index for the subaddress.
    * _minor_ - unsigned int; Index of the subaddress in the account.
  * _address_ - string; Address receiving the payment; Base58 representation of the public keys.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_bulk_payments","params":{"payment_ids":["60900e5603bf96e3"],"min_block_height":"120000"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "payments": [{
      "address": "83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "amount": 1000000000000,
      "block_height": 127606,
      "payment_id": "60900e5603bf96e3",
      "subaddr_index": {
        "major": 0,
        "minor": 0
      },
      "tx_hash": "3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f",
      "unlock_time": 0
    }]
  }
}

```

### **incoming\_transfers** <a href="#incoming_transfers" id="incoming_transfers"></a>

Return a list of incoming transfers to the wallet.

Inputs:

* _transfer\_type_ - string; "all": all the transfers, "available": only transfers which are not yet spent, OR "unavailable": only transfers which are already spent.
* _account\_index_ - unsigned int; (Optional) Return transfers for this account. (defaults to 0)
* _subaddr\_indices_ - array of unsigned int; (Optional) Return transfers sent to these subaddresses.
* _verbose_ - boolean; (Optional) Enable verbose output, return key image if true.

Outputs:

* _transfers_ - list of:
  * _amount_ - unsigned int; Amount of this transfer.
  * _global\_index_ - unsigned int; Mostly internal use, can be ignored by most users.
  * _key\_image_ - string; Key image for the incoming transfer's unspent output (empty unless verbose is true).
  * _spent_ - boolean; Indicates if this transfer has been spent.
  * _subaddr\_index_ - unsigned int; Subaddress index for incoming transfer.
  * _tx\_hash_ - string; Several incoming transfers may share the same hash if they were in the same transaction.
  * _tx\_size_ - unsigned int; Size of transaction in bytes.

Example, get all transfers:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"incoming_transfers","params":{"transfer_type":"all","account_index":0,"subaddr_indices":[3],"verbose":true}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "transfers": [{
      "amount": 60000000000000,
      "global_index": 122405,
      "key_image": "768f5144777eb23477ab7acf83562581d690abaf98ca897c03a9d2b900eb479b",
      "spent": true,
      "subaddr_index": 3,
      "tx_hash": "f53401f21c6a43e44d5dd7a90eba5cf580012ad0e15d050059136f8a0da34f6b",
      "tx_size": 159
    },{
      "amount": 27126892247503,
      "global_index": 594994,
      "key_image": "7e561394806afd1be61980cc3431f6ef3569fa9151cd8d234f8ec13aa145695e",
      "spent": false,
      "subaddr_index": 3,
      "tx_hash": "106d4391a031e5b735ded555862fec63233e34e5fa4fc7edcfdbe461c275ae5b",
      "tx_size": 157
    },{
      "amount": 27169374733655,
      "global_index": 594997,
      "key_image": "e76c0a3bfeaae35e4173712f782eb34011198e26b990225b71aa787c8ba8a157",
      "spent": false,
      "subaddr_index": 3,
      "tx_hash": "0bd959b59117ee1254bd8e5aa8e77ec04ef744144a1ffb2d5c1eb9380a719621",
      "tx_size": 158
    }]
  }
}

```

Example, get available transfers:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"incoming_transfers","params":{"transfer_type":"available","account_index":0,"subaddr_indices":[3],"verbose":true}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "transfers": [{
      "amount": 27126892247503,
      "global_index": 594994,
      "key_image": "7e561394806afd1be61980cc3431f6ef3569fa9151cd8d234f8ec13aa145695e",
      "spent": false,
      "subaddr_index": 3,
      "tx_hash": "106d4391a031e5b735ded555862fec63233e34e5fa4fc7edcfdbe461c275ae5b",
      "tx_size": 157
    },{
      "amount": 27169374733655,
      "global_index": 594997,
      "key_image": "e76c0a3bfeaae35e4173712f782eb34011198e26b990225b71aa787c8ba8a157",
      "spent": false,
      "subaddr_index": 3,
      "tx_hash": "0bd959b59117ee1254bd8e5aa8e77ec04ef744144a1ffb2d5c1eb9380a719621",
      "tx_size": 158
    }]
  }
}

```

Example, get unavailable transfers:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"incoming_transfers","params":{"transfer_type":"unavailable","account_index":0,"subaddr_indices":[3],"verbose":true}}' -H 'Content-Type: application/json'
{
"id": "0",
"jsonrpc": "2.0",
"result": {
  "transfers": [{
    "amount": 60000000000000,
    "global_index": 122405,
    "key_image": "768f5144777eb23477ab7acf83562581d690abaf98ca897c03a9d2b900eb479b",
    "spent": true,
    "subaddr_index": 3,
    "tx_hash": "f53401f21c6a43e44d5dd7a90eba5cf580012ad0e15d050059136f8a0da34f6b",
    "tx_size": 159
  }]
}
}

```

### **query\_key** <a href="#query_key" id="query_key"></a>

Return the spend or view private key.

Alias: _None_.

Inputs:

* _key\_type_ - string; Which key to retrieve: "mnemonic" - the mnemonic seed (older wallets do not have one) OR "view\_key" - the view key

Outputs:

* _key_ - string; The view key will be hex encoded, while the mnemonic will be a string of words.

Example (Query view key):

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"query_key","params":{"key_type":"view_key"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "key": "0a1a38f6d246e894600a3e27238a064bf5e8d91801df47a17107596b1378e501"
  }
}

```

Example (Query mnemonic key):

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"query_key","params":{"key_type":"mnemonic"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "key": "vocal either anvil films dolphin zeal bacon cuisine quote syndrome rejoices envy okay pancakes tulips lair greater petals organs enmity dedicated oust thwart tomorrow tomorrow"
  }
}

```

### **make\_integrated\_address** <a href="#make_integrated_address" id="make_integrated_address"></a>

Make an integrated address from the wallet address and a payment id.

Alias: _None_.

Inputs:

* _standard\_address_ - string; (Optional, defaults to primary address) Destination public address.
* _payment\_id_ - string; (Optional, defaults to a random ID) 16 characters hex encoded.

Outputs:

* _integrated\_address_ - string
* _payment\_id_ - string; hex encoded;

Example (Payment ID is empty, use a random ID):

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"make_integrated_address","params":{"standard_address":"83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "integrated_address": "5F38Rw9HKeaLQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZXCkbHUXdPHyiUeRyokn",
    "payment_id": "420fa29b2d9a49f5"
  }
}

```

### **split\_integrated\_address** <a href="#split_integrated_address" id="split_integrated_address"></a>

Retrieve the standard address and payment id corresponding to an integrated address.

Alias: _None_.

Inputs:

* _integrated\_address_ - string

Outputs:

* _is\_subaddress_ - boolean; States if the address is a subaddress
* _payment_ - string; hex encoded
* _standard\_address_ - string

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"split_integrated_address","params":{"integrated_address": "5F38Rw9HKeaLQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZXCkbHUXdPHyiUeRyokn"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "is_subaddress": false,
    "payment_id": "420fa29b2d9a49f5",
    "standard_address": "83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt"
  }
}

```

### **stop\_wallet** <a href="#stop_wallet" id="stop_wallet"></a>

Stops the wallet, storing the current state.

Alias: _None_.

Inputs: _None_.

Outputs: _None_.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"stop_wallet"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **rescan\_blockchain** <a href="#rescan_blockchain" id="rescan_blockchain"></a>

Rescan the blockchain from scratch, losing any information which can not be recovered from the blockchain itself.\
This includes destination addresses, tx secret keys, tx notes, etc.

Alias: _None_.

Inputs: _None_.

Outputs: _None_.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"rescan_blockchain"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **set\_tx\_notes** <a href="#set_tx_notes" id="set_tx_notes"></a>

Set arbitrary string notes for transactions.

Alias: _None_.

Inputs:

* _txids_ - array of string; transaction ids
* _notes_ - array of string; notes for the transactions

Outputs: _None_.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"set_tx_notes","params":{"txids":["3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"],"notes":["This is an example"]}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **get\_tx\_notes** <a href="#get_tx_notes" id="get_tx_notes"></a>

Get string notes for transactions.

Alias: _None_.

Inputs:

* _txids_ - array of string; transaction ids

Outputs:

* _notes_ - array of string; notes for the transactions

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_tx_notes","params":{"txids":["3292e83ad28fc1cc7bc26dbd38862308f4588680fbf93eae3e803cddd1bd614f"]}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "notes": ["This is an example"]
  }
}

```

### **set\_attribute** <a href="#set_attribute" id="set_attribute"></a>

Set arbitrary attribute.

Alias: _None_.

Inputs:

* _key_ - string; attribute name
* _value_ - string; attribute value

Outputs: _None_.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"set_attribute","params":{"key":"my_attribute","value":"my_value"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **get\_attribute** <a href="#get_attribute" id="get_attribute"></a>

Get attribute value by name.

Alias: _None_.

Inputs:

* _key_ - string; attribute name

Outputs:

* _value_ - string; attribute value

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_attribute","params":{"key":"my_attribute"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "value": "my_value"
  }
}

```

### **get\_tx\_key** <a href="#get_tx_key" id="get_tx_key"></a>

Get transaction secret key from transaction id.

Alias: _None_.

Inputs:

* _txid_ - string; transaction id.

Outputs:

* _tx\_key_ - string; transaction secret key.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_tx_key","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "tx_key": "feba662cf8fb6d0d0da18fc9b70ab28e01cc76311278fdd7fe7ab16360762b06"
  }
}

```

### **check\_tx\_key** <a href="#check_tx_key" id="check_tx_key"></a>

Check a transaction in the blockchain with its secret key.

Alias: _None_.

Inputs:

* _txid_ - string; transaction id.
* _tx\_key_ - string; transaction secret key.
* _address_ - string; destination public address of the transaction.

Outputs:

* _confirmations_ - unsigned int; Number of block mined after the one with the transaction.
* _in\_pool_ - boolean; States if the transaction is still in pool or has been added to a block.
* _received_ - unsigned int; Amount of the transaction.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_tx_key","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","tx_key":"feba662cf8fb6d0d0da18fc9b70ab28e01cc76311278fdd7fe7ab16360762b06","address":"8BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "confirmations": 0,
    "in_pool": false,
    "received": 1000000000000
  }
}

```

### **get\_tx\_proof** <a href="#get_tx_proof" id="get_tx_proof"></a>

Get transaction signature to prove it.

Alias: _None_.

Inputs:

* _txid_ - string; transaction id.
* _address_ - string; destination public address of the transaction.
* _message_ - string; (Optional) add a message to the signature to further authenticate the prooving process.

Outputs:

* _signature_ - string; transaction signature.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_tx_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","address":"8BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o","message":"this is my transaction"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signature": "InProofV13vqBC86dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ"
  }
}

```

### **check\_tx\_proof** <a href="#check_tx_proof" id="check_tx_proof"></a>

Prove a transaction by checking its signature.

Alias: _None_.

Inputs:

* _txid_ - string; transaction id.
* _address_ - string; destination public address of the transaction.
* _message_ - string; (Optional) Should be the same message used in `get_tx_proof`.
* _signature_ - string; transaction signature to confirm.

Outputs:

* _confirmations_ - unsigned int; Number of block mined after the one with the transaction.
* _good_ - boolean; States if the inputs proves the transaction.
* _in\_pool_ - boolean; States if the transaction is still in pool or has been added to a block.
* _received_ - unsigned int; Amount of the transaction.

In the example below, the transaction has been proven:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_tx_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","address":"8BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o","message":"this is my transaction","signature":"InProofV13vqBC86dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "confirmations": 482,
    "good": true,
    "in_pool": false,
    "received": 1000000000000
  }
}

```

In the example below, the wrong message is used, avoiding the transaction to be proved:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_tx_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","address":"8BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o","message":"wrong message","signature":"InProofV13vqBC86dpSAXkypZmSEMPGVnNRFDX2vscUYeVS4WnSVnV5BwLs31T9q6Etfj9Wts6tAxSAS4gkMeSYzzLS7Gt4vvCSQRh9niGJMUDJsB5hTzb2XJiCkUzWkkcjLFBBRVD5QZ"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "confirmations": 0,
    "good": false,
    "in_pool": false,
    "received": 0
  }
}

```

### **get\_spend\_proof** <a href="#get_spend_proof" id="get_spend_proof"></a>

Generate a signature to prove a spend. Unlike proving a transaction, it does not requires the destination public address.

Alias: _None_.

Inputs:

* _txid_ - string; transaction id.
* _message_ - string; (Optional) add a message to the signature to further authenticate the prooving process.

Outputs:

* _signature_ - string; spend signature.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_spend_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","message":"this is my transaction"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signature": "SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB"
  }
}

```

### **check\_spend\_proof** <a href="#check_spend_proof" id="check_spend_proof"></a>

Prove a spend using a signature. Unlike proving a transaction, it does not requires the destination public address.

Alias: _None_.

Inputs:

* _txid_ - string; transaction id.
* _message_ - string; (Optional) Should be the same message used in `get_spend_proof`.
* _signature_ - string; spend signature to confirm.

Outputs:

* _good_ - boolean; States if the inputs proves the spend.

In the example below, the spend has been proven:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_spend_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","message":"this is my transaction","signature":"SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": true
  }
}

```

In the example below, the wrong message is used, avoiding the spend to be proved:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_spend_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","message":"wrong message","signature":"SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": false
  }
}

```

### **get\_reserve\_proof** <a href="#get_reserve_proof" id="get_reserve_proof"></a>

Generate a signature to prove of an available amount in a wallet.

Alias: _None_.

Inputs:

* _all_ - boolean; Proves all wallet balance to be disposable.
* _account\_index_ - unsigned int; Specify the account from witch to prove reserve. (ignored if `all` is set to true)
* _amount_ - unsigned int; Amount (in atomic units) to prove the account has for reserve. (ignored if `all` is set to true)
* _message_ - string; (Optional) add a message to the signature to further authenticate the prooving process.

Outputs:

* _signature_ - string; reserve signature.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_reserve_proof","params":{"all":false,"account_index":0,"amount":100000000000}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signature": "ReserveProofV11BZ23sBt9sZJeGccf84mzyAmNCP3KzYbE1111112VKmH111118NfCYJQjZ6c46gT2kXgcHCaSSZeL8sRdzqjqx7i1e7FQfQGu2o113UYFVdwzHQi3iENDPa76Kn1BvywbKz3bMkXdZkBEEhBSF4kjjGaiMJ1ucKb6wvMVC4A8sA4nZEdL2Mk3wBucJCYTZwKqA8i1M113kqakDkG25FrjiDqdQTCYz2wDBmfKxF3eQiV5FWzZ6HmAyxnqTWUiMWukP9A3Edy3ZXqjP1b23dhz7Mbj39bBxe3ZeDNu9HnTSqYvHNRyqCkeUMJpHyQweqjGUJ1DSfFYr33J1E7MkhMnEi1o7trqWjVix32XLetYfePG73yvHbS24837L7Q64i5n1LSpd9yMiQZ3Dyaysi5y6jPx7TpAvnSqBFtuCciKoNzaXoA3dqt9cuVFZTXzdXKqdt3cXcVJMNxY8RvKPVQHhUur94Lpo1nSpxf7BN5a5rHrbZFqoZszsZmiWikYPkLX72XUdw6NWjLrTBxSy7KuPYH86c6udPEXLo2xgN6XHMBMBJzt8FqqK7EcpNUBkuHm2AtpGkf9CABY3oSjDQoRF5n4vNLd3qUaxNsG4XJ12L9gJ7GrK273BxkfEA8fDdxPrb1gpespbgEnCTuZHqj1A"
  }
}

```

### **check\_reserve\_proof** <a href="#check_reserve_proof" id="check_reserve_proof"></a>

Proves a wallet has a disposable reserve using a signature.

Alias: _None_.

Inputs:

* _address_ - string; Public address of the wallet.
* _message_ - string; (Optional) Should be the same message used in `get_reserve_proof`.
* _signature_ - string; reserve signature to confirm.

Outputs:

* _good_ - boolean; States if the inputs proves the reserve.

In the example below, the reserve has been proven:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_reserve_proof","params":{"address":"83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","signature":"ReserveProofV11BZ23sBt9sZJeGccf84mzyAmNCP3KzYbE1111112VKmH111118NfCYJQjZ6c46gT2kXgcHCaSSZeL8sRdzqjqx7i1e7FQfQGu2o113UYFVdwzHQi3iENDPa76Kn1BvywbKz3bMkXdZkBEEhBSF4kjjGaiMJ1ucKb6wvMVC4A8sA4nZEdL2Mk3wBucJCYTZwKqA8i1M113kqakDkG25FrjiDqdQTCYz2wDBmfKxF3eQiV5FWzZ6HmAyxnqTWUiMWukP9A3Edy3ZXqjP1b23dhz7Mbj39bBxe3ZeDNu9HnTSqYvHNRyqCkeUMJpHyQweqjGUJ1DSfFYr33J1E7MkhMnEi1o7trqWjVix32XLetYfePG73yvHbS24837L7Q64i5n1LSpd9yMiQZ3Dyaysi5y6jPx7TpAvnSqBFtuCciKoNzaXoA3dqt9cuVFZTXzdXKqdt3cXcVJMNxY8RvKPVQHhUur94Lpo1nSpxf7BN5a5rHrbZFqoZszsZmiWikYPkLX72XUdw6NWjLrTBxSy7KuPYH86c6udPEXLo2xgN6XHMBMBJzt8FqqK7EcpNUBkuHm2AtpGkf9CABY3oSjDQoRF5n4vNLd3qUaxNsG4XJ12L9gJ7GrK273BxkfEA8fDdxPrb1gpespbgEnCTuZHqj1A"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": true,
    "spent": 0,
    "total": 100000000000
  }
}

```

In the example below, all wallet reserve has been proven:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_reserve_proof","params":{"address":"83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","message":"I have 10 at least","signature":"...signature..."}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": true,
    "spent": 0,
    "total": 164113855714662789
  }
}

```

In the example below, the wrong message is used, avoiding the reserve to be proved:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"check_spend_proof","params":{"txid":"19d5089f9469db3d90aca9024dfcb17ce94b948300101c8345a5e9f7257353be","message":"wrong message","signature":"SpendProofV1aSh8Todhk54736iXgV6vJAFP7egxByuMWZeyNDaN2JY737S95X5zz5mNMQSuCNSLjjhi5HJCsndpNWSNVsuThxwv285qy1KkUrLFRkxMSCjfL6bbycYN33ScZ5UB4Fzseceo1ndpL393T1q638VmcU3a56dhNHF1RPZFiGPS61FA78nXFSqE9uoKCCoHkEz83M1dQVhxZV5CEPF2P6VioGTKgprLCH9vvj9k1ivd4SX19L2VSMc3zD1u3mkR24ioETvxBoLeBSpxMoikyZ6inhuPm8yYo9YWyFtQK4XYfAV9mJ9knz5fUPXR8vvh7KJCAg4dqeJXTVb4mbMzYtsSZXHd6ouWoyCd6qMALdW8pKhgMCHcVYMWp9X9WHZuCo9rsRjRpg15sJUw7oJg1JoGiVgj8P4JeGDjnZHnmLVa5bpJhVCbMhyM7JLXNQJzFWTGC27TQBbthxCfQaKdusYnvZnKPDJWSeceYEFzepUnsWhQtyhbb73FzqgWC4eKEFKAZJqT2LuuSoxmihJ9acnFK7Ze23KTVYgDyMKY61VXADxmSrBvwUtxCaW4nQtnbMxiPMNnDMzeixqsFMBtN72j5UqhiLRY99k6SE7Qf5f29haNSBNSXCFFHChPKNTwJrehkofBdKUhh2VGPqZDNoefWUwfudeu83t85bmjv8Q3LrQSkFgFjRT5tLo8TMawNXoZCrQpyZrEvnodMDDUUNf3NL7rxyv3gM1KrTWjYaWXFU2RAsFee2Q2MTwUW7hR25cJvSFuB1BX2bfkoCbiMk923tHZGU2g7rSKF1GDDkXAc1EvFFD4iGbh1Q5t6hPRhBV8PEncdcCWGq5uAL5D4Bjr6VXG8uNeCy5oYWNgbZ5JRSfm7QEhPv8Fy9AKMgmCxDGMF9dVEaU6tw2BAnJavQdfrxChbDBeQXzCbCfep6oei6n2LZdE5Q84wp7eoQFE5Cwuo23tHkbJCaw2njFi3WGBbA7uGZaGHJPyB2rofTWBiSUXZnP2hiE9bjJghAcDm1M4LVLfWvhZmFEnyeru3VWMETnetz1BYLUC5MJGFXuhnHwWh7F6r74FDyhdswYop4eWPbyrXMXmUQEccTGd2NaT8g2VHADZ76gMC6BjWESvcnz2D4n8XwdmM7ZQ1jFwhuXrBfrb1dwRasyXxxHMGAC2onatNiExyeQ9G1W5LwqNLAh9hvcaNTGaYKYXoceVzLkgm6e5WMkLsCwuZXvB"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": false
  }
}

```

### **get\_transfers** <a href="#get_transfers" id="get_transfers"></a>

Returns a list of transfers.

Alias: _None_.

Inputs:

* _in_ - boolean; (Optional) Include incoming transfers.
* _out_ - boolean; (Optional) Include outgoing transfers.
* _pending_ - boolean; (Optional) Include pending transfers.
* _failed_ - boolean; (Optional) Include failed transfers.
* _pool_ - boolean; (Optional) Include transfers from the daemon's transaction pool.
* _filter\_by\_height_ - boolean; (Optional) Filter transfers by block height.
* _min\_height_ - unsigned int; (Optional) Minimum block height to scan for transfers, if filtering by height is enabled.
* _max\_height_ - unsigned int; (Opional) Maximum block height to scan for transfers, if filtering by height is enabled (defaults to max block height).
* _account\_index_ - unsigned int; (Optional) Index of the account to query for transfers. (defaults to 0)
* _subaddr\_indices_ - array of unsigned int; (Optional) List of subaddress indices to query for transfers. (defaults to 0)

Outputs:

* _in_ array of transfers:
  * _address_ - string; Public address of the transfer.
  * _amount_ - unsigned int; Amount transferred.
  * _confirmations_ - unsigned int; Number of block mined since the block containing this transaction (or block height at which the transaction should be added to a block if not yet confirmed).
  * _double\_spend\_seen_ - boolean; True if the key image(s) for the transfer have been seen before.
  * _fee_ - unsigned int; Transaction fee for this transfer.
  * _height_ - unsigned int; Height of the first block that confirmed this transfer (0 if not mined yet).
  * _note_ - string; Note about this transfer.
  * _payment\_id_ - string; Payment ID for this transfer.
  * _subaddr\_index_ - JSON object containing the major & minor subaddress index:
    * _major_ - unsigned int; Account index for the subaddress.
    * _minor_ - unsigned int; Index of the subaddress under the account.
  * _suggested\_confirmations\_threshold_ - unsigned int; Estimation of the confirmations needed for the transaction to be included in a block.
  * _timestamp_ - unsigned int; POSIX timestamp for when this transfer was first confirmed in a block (or timestamp submission if not mined yet).
  * _txid_ - string; Transaction ID for this transfer.
  * _type_ - string; Transfer type: "in"
  * _unlock\_time_ - unsigned int; Number of blocks until transfer is safely spendable.
* _out_ array of transfers (see above).
* _pending_ array of transfers (see above).
* _failed_ array of transfers (see above).
* _pool_ array of transfers (see above).

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_transfers","params":{"in":true,"account_index":1}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "in": [{
      "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
      "amount": 200000000000,
      "confirmations": 1,
      "double_spend_seen": false,
      "fee": 21650200000,
      "height": 153624,
      "note": "",
      "payment_id": "0000000000000000",
      "subaddr_index": {
        "major": 1,
        "minor": 0
      },
      "suggested_confirmations_threshold": 1,
      "timestamp": 1535918400,
      "txid": "c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a",
      "type": "in",
      "unlock_time": 0
    }]
  }
}

```

### **get\_transfer\_by\_txid** <a href="#get_transfer_by_txid" id="get_transfer_by_txid"></a>

Show information about a transfer to/from this address.

Alias: _None_.

Inputs:

* _txid_ - string; Transaction ID used to find the transfer.
* _account\_index_ - unsigned int; (Optional) Index of the account to query for the transfer.

Outputs:

* _transfer_ - JSON object containing payment information:
  * _address_ - string; Address that transferred the funds. Base58 representation of the public keys.
  * _amount_ - unsigned int; Amount of this transfer.
  * _confirmations_ - unsigned int; Number of block mined since the block containing this transaction (or block height at which the transaction should be added to a block if not yet confirmed).
  * _destinations_ - array of JSON objects containing transfer destinations:
    * _amount_ - unsigned int; Amount transferred to this destination.
    * _address_ - string; Address for this destination. Base58 representation of the public keys.
  * _double\_spend\_seen_ - boolean; True if the key image(s) for the transfer have been seen before.
  * _fee_ - unsigned int; Transaction fee for this transfer.
  * _height_ - unsigned int; Height of the first block that confirmed this transfer.
  * _note_ - string; Note about this transfer.
  * _payment\_id_ - string; Payment ID for this transfer.
  * _subaddr\_index_ - JSON object containing the major & minor subaddress index:
    * _major_ - unsigned int; Account index for the subaddress.
    * _minor_ - unsigned int; Index of the subaddress under the account.
  * _suggested\_confirmations\_threshold_ - unsigned int; Estimation of the confirmations needed for the transaction to be included in a block.
  * _timestamp_ - unsigned int; POSIX timestamp for the block that confirmed this transfer (or timestamp submission if not mined yet).
  * _txid_ - string; Transaction ID of this transfer (same as input TXID).
  * _type_ - string; Type of transfer, one of the following: "in", "out", "pending", "failed", "pool"
  * _unlock\_time_ - unsigned int; Number of blocks until transfer is safely spendable.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_transfer_by_txid","params":{"txid":"c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "transfer": {
      "address": "83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "amount": 300000000000,
      "confirmations": 1,
      "destinations": [{
        "address": "8BnERTpvL5MbCLtj5n9No7J5oE5hHiB3tVCK5cjSvCsYWD2WRJLFuWeKTLiXo5QJqt2ZwUaLy2Vh1Ad51K7FNgqcHgjW85o",
        "amount": 100000000000
      },{
        "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
        "amount": 200000000000
      }],
      "double_spend_seen": false,
      "fee": 21650200000,
      "height": 153624,
      "note": "",
      "payment_id": "0000000000000000",
      "subaddr_index": {
        "major": 0,
        "minor": 0
      },
      "suggested_confirmations_threshold": 1,
      "timestamp": 1535918400,
      "txid": "c36258a276018c3a4bc1f195a7fb530f50cd63a4fa765fb7c6f7f49fc051762a",
      "type": "out",
      "unlock_time": 0
    }
  }
}

```

### **sign** <a href="#sign" id="sign"></a>

Sign a string.

Alias: _None_.

Inputs:

* _data_ - string; Anything you need to sign.

Outputs:

* _signature_ - string; Signature generated against the "data" and the account public address.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sign","params":{"data":"This is sample data to be signed"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signature": "SigV14K6G151gycjiGxjQ74tKX6A2LwwghvuHjcDeuRFQio5LS6Gb27BNxjYQY1dPuUvXkEbGQUkiHSVLPj4nJAHRrrw3"
  }
}

```

### **verify** <a href="#verify" id="verify"></a>

Verify a signature on a string.

Alias: _None_.

Inputs:

* _data_ - string; What should have been signed.
* _address_ - string; Public address of the wallet used to `sign` the data.
* _signature_ - string; signature generated by `sign` method.

Outputs:

* _good_ - boolean;

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"verify","params":{"data":"This is sample data to be signed","address":"83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","signature":"SigV14K6G151gycjiGxjQ74tKX6A2LwwghvuHjcDeuRFQio5LS6Gb27BNxjYQY1dPuUvXkEbGQUkiHSVLPj4nJAHRrrw3"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "good": true
  }
}

```

### **export\_outputs** <a href="#export_outputs" id="export_outputs"></a>

Export all outputs in hex format.

Alias: _None_.

Inputs: _None_.

Outputs:

* _outputs\_data\_hex_ - string; wallet outputs in hex format.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"export_outputs"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "outputs_data_hex": "...outputs..."
  }
}

```

### **import\_outputs** <a href="#import_outputs" id="import_outputs"></a>

Import outputs in hex format.

Alias: _None_.

Inputs:

* _outputs\_data\_hex_ - string; wallet outputs in hex format.

Outputs:

* _num\_imported_ - unsigned int; number of outputs imported.

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"import_outputs","params":{"outputs_data_hex":"...outputs..."}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "num_imported": 6400
  }
}

```

### **export\_key\_images** <a href="#export_key_images" id="export_key_images"></a>

Export a signed set of key images.

Alias: _None_.

Inputs: _None_.

Outputs:

* _signed\_key\_images_ - array of signed key images:
  * _key\_image_ - string;
  * _signature_ - string;

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"export_key_images"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signed_key_images": [{
      "key_image": "cd35239b72a35e26a57ed17400c0b66944a55de9d5bda0f21190fed17f8ea876",
      "signature": "c9d736869355da2538ab4af188279f84138c958edbae3c5caf388a63cd8e780b8c5a1aed850bd79657df659422c463608ea4e0c730ba9b662c906ae933816d00"
    },{
      "key_image": "65158a8ee5a3b32009b85a307d85b375175870e560e08de313531c7dbbe6fc19",
      "signature": "c96e40d09dfc45cfc5ed0b76bfd7ca793469588bb0cf2b4d7b45ef23d40fd4036057b397828062e31700dc0c2da364f50cd142295a8405b9fe97418b4b745d0c"
    },...]
  }
}

```

### **import\_key\_images** <a href="#import_key_images" id="import_key_images"></a>

Import signed key images list and verify their spent status.

Alias: _None_.

Inputs:

* _signed\_key\_images_ - array of signed key images:
  * _key\_image_ - string;
  * _signature_ - string;

Outputs:

* _height_ - unsigned int;
* _spent_ - unsigned int; Amount (in atomic units) spent from those key images.
* _unspent_ - unsigned int; Amount (in atomic units) still available from those key images.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"import_key_images", "params":{"signed_key_images":[{"key_image":"cd35239b72a35e26a57ed17400c0b66944a55de9d5bda0f21190fed17f8ea876","signature":"c9d736869355da2538ab4af188279f84138c958edbae3c5caf388a63cd8e780b8c5a1aed850bd79657df659422c463608ea4e0c730ba9b662c906ae933816d00"},{"key_image":"65158a8ee5a3b32009b85a307d85b375175870e560e08de313531c7dbbe6fc19","signature":"c96e40d09dfc45cfc5ed0b76bfd7ca793469588bb0cf2b4d7b45ef23d40fd4036057b397828062e31700dc0c2da364f50cd142295a8405b9fe97418b4b745d0c"}]}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "height": 76428,
    "spent": 62708953408711,
    "unspent": 0
  }
}

```

### **make\_uri** <a href="#make_uri" id="make_uri"></a>

Create a payment URI using the official URI spec.

Alias: _None_.

Inputs:

* _address_ - string; Wallet address
* _amount_ - unsigned int; (optional) the integer amount to receive, in **atomic**units
* _payment\_id_ - string; (optional) 16 or 64 character hexadecimal payment id
* _recipient\_name_ - string; (optional) name of the payment recipient
* _tx\_description_ - string; (optional) Description of the reason for the tx

Outputs:

* _uri_ - string; This contains all the payment input information as a properly formatted payment URI

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"make_uri","params":{"address":"83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt","amount":10,"payment_id":"420fa29b2d9a49f5","tx_description":"Testing out the make_uri function.","recipient_name":"el00ruobuob Stagenet wallet"}}'  -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "uri": "beldex:83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt?tx_payment_id=420fa29b2d9a49f5&tx_amount=0.000000000010&recipient_name=el00ruobuob%20Stagenet%20wallet&tx_description=Testing%20out%20the%20make_uri%20function."
  }
}

```

### **parse\_uri** <a href="#parse_uri" id="parse_uri"></a>

Parse a payment URI to get payment information.

Alias: _None_.

Inputs:

* _uri_ - string; This contains all the payment input information as a properly formatted payment URI

Outputs:

* _uri_ - JSON object containing payment information:
  * _address_ - string; Wallet address
  * _amount_ - unsigned int; Decimal amount to receive, in **coin** units (0 if not provided)
  * _payment\_id_ - string; 16 or 64 character hexadecimal payment id (empty if not provided)
  * _recipient\_name_ - string; Name of the payment recipient (empty if not provided)
  * _tx\_description_ - string; Description of the reason for the tx (empty if not provided)

Example:

```
$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"parse_uri","params":{"uri":"beldex:83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt?tx_payment_id=420fa29b2d9a49f5&tx_amount=0.000000000010&recipient_name=el00ruobuob%20Stagenet%20wallet&tx_description=Testing%20out%20the%20make_uri%20function."}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "uri": {
      "address": "83LTR8KniP4LQGJSPtbYDacR7dz8RBFnsfAKMaMuwUNYX6aQbBcovzDPyrQF9KXF9tVU6Xk3K8no1BywnJX6GvZX8yJsXvt",
      "amount": 10,
      "payment_id": "420fa29b2d9a49f5",
      "recipient_name": "el00ruobuob Stagenet wallet",
      "tx_description": "Testing out the make_uri function."
    }
  }
}

```

### **get\_address\_book** <a href="#get_address_book" id="get_address_book"></a>

Retrieves entries from the address book.

Alias: _None_.

Inputs:

* _entries_ - array of unsigned int; indices of the requested address book entries

Outputs:

* _entries_ - array of entries:
  * _address_ - string; Public address of the entry
  * _description_ - string; Description of this address entry
  * _index_ - unsigned int;
  * _payment\_id_ - string;

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_address_book","params":{"entries":[0,1]}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "entries": [{
      "address": "77Vx9cs1VPicFndSVgYUvTdLCJEZw9h81hXLMYsjBCXSJfUehLa9TDW3Ffh45SQa7xb6dUs18mpNxfUhQGqfwXPSMrvKhVp",
      "description": "Second account",
      "index": 0,
      "payment_id": "0000000000000000000000000000000000000000000000000000000000000000"
    },{
      "address": "78P16M3XmFRGcWFCcsgt1WcTntA1jzcq31seQX1Eg92j8VQ99NPivmdKam4J5CKNAD7KuNWcq5xUPgoWczChzdba5WLwQ4j",
      "description": "Third account",
      "index": 1,
      "payment_id": "0000000000000000000000000000000000000000000000000000000000000000"
    }]
  }
}

```

### **add\_address\_book** <a href="#add_address_book" id="add_address_book"></a>

Add an entry to the address book.

Alias: _None_.

Inputs:

* _address_ - string;
* _payment\_id_ - (optional) string, defaults to "0000000000000000000000000000000000000000000000000000000000000000";
* _description_ - (optional) string, defaults to "";

Outputs:

* _index_ - unsigned int; The index of the address book entry.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"add_address_book","params":{"address":"78P16M3XmFRGcWFCcsgt1WcTntA1jzcq31seQX1Eg92j8VQ99NPivmdKam4J5CKNAD7KuNWcq5xUPgoWczChzdba5WLwQ4j","description":"Third account"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "index": 1
  }
}

```

### **delete\_address\_book** <a href="#delete_address_book" id="delete_address_book"></a>

Delete an entry from the address book.

Alias: _None_.

Inputs:

* _index_ - unsigned int; The index of the address book entry.

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"delete_address_book","params":{"index":1}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **refresh** <a href="#refresh" id="refresh"></a>

Refresh a wallet after openning.

Alias: _None_.

Inputs:

* _start\_height_ - unsigned int; (Optional) The block height from which to start refreshing.

Outputs:

* _blocks\_fetched_ - unsigned int; Number of new blocks scanned.
* _received\_money_ - boolean; States if transactions to the wallet have been found in the blocks.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"refresh","params":{"start_height":100000}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "blocks_fetched": 24,
    "received_money": true
  }
}

```

### **rescan\_spent** <a href="#rescan_spent" id="rescan_spent"></a>

Rescan the blockchain for spent outputs.

Alias: _None_.

Inputs: _None_.

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"rescan_spent"}' -H 'Content-Type: application/json'

{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **start\_mining** <a href="#start_mining" id="start_mining"></a>

Start mining in the beldex daemon.

Alias: _None_.

Inputs:

* _threads\_count_ - unsigned int; Number of threads created for mining.
* _do\_background\_mining_ - boolean; Allow to start the miner in background
* _ignore\_battery_ - boolean; Ignore battery status

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"start_mining","params":{"threads_count":1,"do_background_mining":true,"ignore_battery":false}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **stop\_mining** <a href="#stop_mining" id="stop_mining"></a>

Stop mining in the beldex daemon.

Alias: _None_.

Inputs: _None_.

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"stop_mining"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **get\_languages** <a href="#get_languages" id="get_languages"></a>

Get a list of available languages for your wallet's seed.

Alias: _None_.

Inputs: _None_.

Outputs:

* _languages_ - array of string; List of available languages

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_languages"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "languages": ["Deutsch","English","Español","Français","Italiano","Nederlands","Português","русский язык","日本語","简体中文 (中国)","Esperanto","Lojban"]
  }
}

```

### **create\_wallet** <a href="#create_wallet" id="create_wallet"></a>

Create a new wallet. You need to have set the argument "–wallet-dir" when launching beldex-wallet-rpc to make this work.

Alias: _None_.

Inputs:

* _filename_ - string; Wallet file name.
* _password_ - string; (Optional) password to protect the wallet.
* _language_ - string; Language for your wallets' seed.

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"create_wallet","params":{"filename":"mytestwallet","password":"mytestpassword","language":"English"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **open\_wallet** <a href="#open_wallet" id="open_wallet"></a>

Open a wallet. You need to have set the argument "–wallet-dir" when launching beldex-wallet-rpc to make this work.

Alias: _None_.

Inputs:

* _filename_ - string; wallet name stored in –wallet-dir.
* _password_ - string; (Optional) only needed if the wallet has a password defined.

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"open_wallet","params":{"filename":"mytestwallet","password":"mytestpassword"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **close\_wallet** <a href="#close_wallet" id="close_wallet"></a>

Close the currently opened wallet, after trying to save it.

Alias: _None_.

Inputs: _None_.

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"close_wallet"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **change\_wallet\_password** <a href="#change_wallet_password" id="change_wallet_password"></a>

Change a wallet password.

Alias: _None_.

Inputs:

* _old\_password_ - string; (Optional) Current wallet password, if defined.
* _new\_password_ - string; (Optional) New wallet password, if not blank.

Outputs: _None_.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"change_wallet_password","params":{"old_password":"theCurrentSecretPassPhrase","new_password":"theNewSecretPassPhrase"}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
  }
}

```

### **is\_multisig** <a href="#is_multisig" id="is_multisig"></a>

Check if a wallet is a multisig one.

Alias: _None_.

Inputs: _None_.

Outputs:

* _multisig_ - boolean; States if the wallet is multisig
* _ready_ - boolean;
* _threshold_ - unsigned int; Amount of signature needed to sign a transfer.
* _total_ - unsigned int; Total amount of signature in the multisig wallet.

Example for a non-multisig wallet:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"is_multisig"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "multisig": false,
    "ready": false,
    "threshold": 0,
    "total": 0
  }
}

```

Example for a multisig wallet:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"is_multisig"}' -H 'Content-Type: application/json'                  {
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "multisig": true,
    "ready": true,
    "threshold": 2,
    "total": 2
  }
}

```

### **prepare\_multisig** <a href="#prepare_multisig" id="prepare_multisig"></a>

Prepare a wallet for multisig by generating a multisig string to share with peers.

Alias: _None_.

Inputs: _None_.

Outputs:

* _multisig\_info_ - string; Multisig string to share with peers to create the multisig wallet.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"prepare_multisig"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "multisig_info": "MultisigV1BFdxQ653cQHB8wsj9WJQd2VdnjxK89g5M94dKPBNw22reJnyJYKrz6rJeXdjFwJ3Mz6n4qNQLd6eqUZKLiNzJFi3UPNVcTjtkG2aeSys9sYkvYYKMZ7chCxvoEXVgm74KKUcUu4V8xveCBFadFuZs8shnxBWHbcwFr5AziLr2mE7KHJT"
  }
}

```

### **make\_multisig** <a href="#make_multisig" id="make_multisig"></a>

Make a wallet multisig by importing peers multisig string.

Alias: _None_.

Inputs:

* _multisig\_info_ - array of string; List of multisig string from peers.
* _threshold_ - unsigned int; Amount of signatures needed to sign a transfer. Must be less or equal than the amount of signature in `multisig_info`.
* _password_ - string; Wallet password

Outputs:

* _address_ - string; multisig wallet address.
* _multisig\_info_ - string; Multisig string to share with peers to create the multisig wallet (extra step for N-1/N wallets).

Example for 2/2 Multisig Wallet:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"make_multisig","params":{"multisig_info":["MultisigV1K4tGGe8QirZdHgTYoBZMumSug97fdDyM3Z63M3ZY5VXvAdoZvx16HJzPCP4Rp2ABMKUqLD2a74ugMdBfrVpKt4BwD8qCL5aZLrsYWoHiA7JJwDESuhsC3eF8QC9UMvxLXEMsMVh16o98GnKRYz1HCKXrAEWfcrCHyz3bLW1Pdggyowop"],"threshold":2}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "address": "55SoZTKH7D39drxfg862k8T4adVFjmDLUXnbzEKYf1MoYwnmTNKKaqGfxm4sqeKCHXQ5up7PVxrkoeRzXu83d8xYURouMod",
    "multisig_info": ""
  }
}

```

Example for 2/3 Multisig Wallet:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"make_multisig","params":{"multisig_info":["MultisigV1MTVm4DZAdJw1PyVutpSy8Q4WisZBCFRAaZY7hhQnMwr5AZ4swzThyaSiVVQM5FHj1JQi3zPKhQ4k81BZkPSEaFjwRJtbfqfJcVvCqRnmBVcWVxhnihX5s8fZWBCjKrzT3CS95spG4dzNzJSUcjheAkLzCpVmSzGtgwMhAS3Vuz9Pas24","MultisigV1TEx58ycKCd6ADCfxF8hALpcdSRAkhZTi1bu4Rs6FdRC98EdB1LY7TAkMxasM55khFgcxrSXivaSr5FCMyJGHmojm1eE4HpGWPeZKv6cgCTThRzC4u6bkkSoFQdbzWN92yn1XEjuP2XQrGHk81mG2LMeyB51MWKJAVF99Pg9mX2BpmYFj"],"threshold":2}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "address": "51sLpF8fWaK1111111111111111111111111111111111ABVbHNf1JFWJyFp5YZgZRQ44RiviJi1sPHgLVMbckRsDkTRgKS",
    "multisig_info": "MultisigxV18jCaYAQQvzCMUJaAWMCaAbAoHpAD6WPmYDmLtBtazD654E8RWkLaGRf29fJ3stU471MELKxwufNYeigP7LoE4tn2Sscwn5g7PyCfcBc1V4ffRHY3Kxqq6VocSCUTncpVeUskaDKuTAWtdB9VTBGW7iG1cd7Zm1dYgur3CiemkGjRUAj9bL3xTEuyaKGYSDhtpFZFp99HQX57EawhiRHk3qq4hjWX"
  }
}

```

### **export\_multisig\_info** <a href="#export_multisig_info" id="export_multisig_info"></a>

Export multisig info for other participants.

Alias: _None_.

Inputs: _None_.

Outputs:

* _info_ - string; Multisig info in hex format for other participants.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"export_multisig_info"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "info": "4d6f6e65726f206d756c7469736967206578706f72740105cf6442b09b75f5eca9d846771fe1a879c9a97ab0553ffbcec64b1148eb7832b51e7898d7944c41cee000415c5a98f4f80dc0efdae379a98805bb6eacae743446f6f421cd03e129eb5b27d6e3b73eb6929201507c1ae706c1a9ecd26ac8601932415b0b6f49cbbfd712e47d01262c59980a8f9a8be776f2bf585f1477a6df63d6364614d941ecfdcb6e958a390eb9aa7c87f056673d73bc7c5f0ab1f74a682e902e48a3322c0413bb7f6fd67404f13fb8e313f70a0ce568c853206751a334ef490068d3c8ca0e"
  }
}

```

### **import\_multisig\_info** <a href="#import_multisig_info" id="import_multisig_info"></a>

Import multisig info from other participants.

Alias: _None_.

Inputs:

* _info_ - array of string; List of multisig info in hex format from other participants.

Outputs:

* _n\_outputs_ - unsigned int; Number of outputs signed with those multisig info.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"import_multisig_info","params":{"info":["...multisig_info..."]}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "n_outputs": 35
  }
}

```

### **finalize\_multisig** <a href="#finalize_multisig" id="finalize_multisig"></a>

Turn this wallet into a multisig wallet, extra step for N-1/N wallets.

Alias: _None_.

Inputs:

* _multisig\_info_ - array of string; List of multisig string from peers.
* _password_ - string; Wallet password

Outputs:

* _address_ - string; multisig wallet address.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"finalize_multisig","params":{"multisig_info":["MultisigxV1JNC6Ja2oBt5Sqea9LN2YEF7WYZCpHqr2EKvPG89Trf3X4E8RWkLaGRf29fJ3stU471MELKxwufNYeigP7LoE4tn2McPr4SbL9q15xNvZT5uwC9YRr7UwjXqSZHmTWN9PBuZEKVAQ4HPPyQciSCdNjgwsuFRBzrskMdMUwNMgKst1debYfm37i6PSzDoS2tk4kYTYj83kkAdR7kdshet1axQPd6HQ","MultisigxV1Unma7Ko4zdd8Ps3Af4oZwtj2JdWKzwNfP6s2G9ZvXhMoSscwn5g7PyCfcBc1V4ffRHY3Kxqq6VocSCUTncpVeUskMcPr4SbL9q15xNvZT5uwC9YRr7UwjXqSZHmTWN9PBuZE1LTpWxLoC3vPMSrqVVcjnmL9LYfdCZz3fECjNZbCEDq3PHDiUuY5jurQTcNoGhDTio5WM9xaAdim9YByiS5KyqF4"]}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "address": "5B9gZUTDuHTcGGuY3nL3t8K2tDnEHeRVHSBQgLZUTQxtFYVLnho5JJjWJyFp5YZgZRQ44RiviJi1sPHgLVMbckRsDqDx1gV"
  }
}

```

### **sign\_multisig** <a href="#sign_multisig" id="sign_multisig"></a>

Sign a transaction in multisig.

Alias: _None_.

Inputs:

* _tx\_data\_hex_ - string; Multisig transaction in hex format, as returned by `transfer` under `multisig_txset`.

Outputs:

* _tx\_data\_hex_ - string; Multisig transaction in hex format.
* _tx\_hash\_list_ - array of string; List of transaction Hash.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"sign_multisig","params":{"tx_data_hex":"...multisig_txset..."}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "tx_data_hex": "...multisig_txset...",
    "tx_hash_list": ["4996091b61c1be112c1097fd5e97d8ff8b28f0e5e62e1137a8c831bacf034f2d"]
  }
}

```

### **submit\_multisig** <a href="#submit_multisig" id="submit_multisig"></a>

Submit a signed multisig transaction.

Alias: _None_.

Inputs:

* _tx\_data\_hex_ - string; Multisig transaction in hex format, as returned by `sign_multisig`under `tx_data_hex`.

Outputs:

* _tx\_hash\_list_ - array of string; List of transaction Hash.

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"submit_multisig","params":{"tx_data_hex":"...tx_data_hex..."}}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "tx_hash_list": ["4996091b61c1be112c1097fd5e97d8ff8b28f0e5e62e1137a8c831bacf034f2d"]
  }
}

```

### **get\_version** <a href="#get_version" id="get_version"></a>

Get RPC version Major & Minor integer-format, where Major is the first 16 bits and Minor the last 16 bits.

Alias: _None_.

Inputs: _None_.

Outputs:

* _version_ - unsigned int; RPC version, formatted with `Major * 2^16 + Minor`(Major encoded over the first 16 bits, and Minor over the last 16 bits).

Example:

```
$ curl -X POST http://localhost:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"get_version"}' -H 'Content-Type: application/json'
{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "version": 65539
  }
}
```

### bns\_buy\_mapping <a href="#sources" id="sources"></a>

Map the BNS name to the BChat Id, Belnet key, bdx address and ETH address.

Alias: _None_.

Inputs:

* _years_ - string; (Optional) The mapping years "1year || 1y" , "2years || 2y" , "5years || 5y" , "10years || 10y".
* _owner_ - string; (Optional) The ed25519 public key or wallet address that has authority to update the mapping.
* _backup\_owner_ - string; (Optional) The secondary, backup public key that has authority to update the mapping.
* _name_ - string; The name to purchase via Beldex Name Service.
* _value\_bchat_ - string; The value of bchat id that the name maps to Beldex Name Service.
* _value\_wallet_ - string; The value of wallet that the name maps to Beldex Name Service.
* _value\_eth\_addr_ - string; The value of ETH address that the name maps to Beldex Name Service.
* _value\_belnet_ - string; The value of belnet address that the name maps to Beldex Name Service.
* _account\_index_ - uint32\_t; (Optional) Transfer from this account index. (Defaults to 0).
* _subaddr\_indices_ - array of unsigned int; (Optional) List of subaddress indices to query for transfers. (defaults to 0).
* _priority_ - unsigned int; Set a priority for the transaction. Accepted Values are: 0 and 1 for: flash and unimportant.
* _get\_tx\_key_ - boolean; (Optional) Return the transaction keys after sending.
* _do\_not\_relay_ - boolean; (Optional) If true, do not relay this sweep transfer. (Defaults to false).
* _get\_tx\_hex_ - boolean; (Optional) return the transactions as hex encoded string. (Defaults to false).
* _get\_tx\_metadata_ - boolean; (Optional) return the transaction metadata as a string. (Defaults to false).

Outputs:

* _tx\_hash_ - String for the publicly searchable transaction hash.
* _tx\_key_ - String for the transaction key if get\_tx\_key is true, otherwise, blank string.
* _amount_ - Amount transferred for the transaction.
* _fee_ - Integer value of the fee charged for the txn.
* _tx\_blob_ - Raw transaction represented as hex string, if get\_tx\_hex is true.
* _tx\_metadata_ - Set of transaction metadata needed to relay this transfer later, if get\_tx\_metadata is true.
* _multisig\_txset_ - Set of multisig transactions in the process of being signed (empty for non-multisig).
* _unsigned\_txset_ - String. Set of unsigned tx for cold-signing purposes.

Example:

<pre><code><strong>$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"bns_buy_mapping","params":{"years":"5y","name":"toretto.bdx","value_bchat":"bdb37ba20b46b5576012eec7547f70eb532276085bb04b6152354de5b187b29807","value_wallet":"9zy7tYvhhjGUPByuk8AxvjJtK2gK7Vt4ebHSS7QuKojeD7hR6G2253aMmFCpcwaAjXR75BWy7Vjor5chH3nG79Uk3aRqWtR"}}' -H 'Content-Type: application/json'
</strong>{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount": 0,
    "fee": 2000010858940,
    "multisig_txset": "",
    "tx_blob": "",
    "tx_hash": "6176445481d469dc45cbe694503d0c415233ede9324a08c6db1e073a6d8ad37f",
    "tx_key": "",
    "tx_metadata": "",
    "unsigned_txset": ""
  }
}
</code></pre>

### bns\_renew\_mapping <a href="#sources" id="sources"></a>

Renew the BNS name for,

* 1 Year&#x20;
* 2 Years
* 5 Years
* 10 Years

Alias: _None_.

Inputs:

* _years_ - string; (optional)The mapping years "1year || 1y" , "2years || 2y" , "5years || 5y" , "10years || 10y". Default value is "1 year"
* _name_ - string; The name to Renew.
* _account\_index_ - uint32\_t; (Optional) Transfer from this account index. (Defaults to 0).
* _subaddr\_indices_ - array of unsigned int; (Optional) List of subaddress indices to query for transfers. (defaults to 0).
* _priority_ - unsigned int; Set a priority for the transaction. Accepted Values are: 0 and 1 for: flash and unimportant.
* _get\_tx\_key_ - boolean; (Optional) Return the transaction keys after sending.
* _do\_not\_relay_ - boolean; (Optional) If true, do not relay this sweep transfer. (Defaults to false).
* _get\_tx\_hex_ - boolean; (Optional) return the transactions as hex encoded string. (Defaults to false).
* _get\_tx\_metadata_ - boolean; (Optional) return the transaction metadata as a string. (Defaults to false).

Outputs:

* _tx\_hash_ - String for the publicly searchable transaction hash.
* _tx\_key_ - String for the transaction key if get\_tx\_key is true, otherwise, blank string.
* _amount_ - Amount transferred for the transaction.
* _fee_ - Integer value of the fee charged for the txn.
* _tx\_blob_ - Raw transaction represented as hex string, if get\_tx\_hex is true.
* _tx\_metadata_ - Set of transaction metadata needed to relay this transfer later, if get\_tx\_metadata is true.
* _multisig\_txset_ - Set of multisig transactions in the process of being signed (empty for non-multisig).
* _unsigned\_txset_ - String. Set of unsigned tx for cold-signing purposes.

Example:

<pre><code><strong>$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"bns_renew_mapping","params":{"years":"10y","name":"toretto.bdx"}}' -H 'Content-Type: application/json'
</strong>{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount": 0,
    "fee": 4000013525340,
    "multisig_txset": "",
    "tx_blob": "",
    "tx_hash": "70675a41576dae95c7b06bc5efa04003f4c84cd409ced7b20d45aae717e06469",
    "tx_key": "",
    "tx_metadata": "",
    "unsigned_txset": ""
  }
}
</code></pre>

### bns\_update\_mapping <a href="#sources" id="sources"></a>

Modify the Bchat and Belnet key values, as well as the wallet's address and ETH address. Additionally, it is possible to update both the Owner and Backup Owner information.

Alias: _None_.

Inputs:

* _name_ - string; The name to Update.
* _value\_bchat_ - string; The value of bchat id that the name maps to Beldex Name Service.
* _value\_wallet_ - string; The value of wallet that the name maps to Beldex Name Service.
* _value\_eth\_addr_ - string; The value of ETH address that the name maps to Beldex Name Service.
* _value\_belnet_ - string; The value of belnet address that the name maps to Beldex Name Service.
* _owner_ - string; (Optional) The ed25519 public key or wallet address that has authority to update the mapping.
* _backup\_owner_ - string; (Optional) The secondary, backup public key that has authority to update the mapping.
* _signature_ - string; (Optional) Signature derived using libsodium generichash on {current txid blob, new value blob} of the mapping to update. By default the hash is signed using the wallet's spend key as an ed25519 keypair, if signature is specified.
* _account\_index_ - uint32\_t; (Optional) Transfer from this account index. (Defaults to 0).&#x20;
* _subaddr\_indices_ - array of unsigned int; (Optional) List of subaddress indices to query for transfers. (defaults to 0).
* _priority_ - unsigned int; Set a priority for the transaction. Accepted Values are: 0 and 1 for: flash and unimportant.
* _get\_tx\_key_ - boolean; (Optional) Return the transaction keys after sending.
* _do\_not\_relay_ - boolean; (Optional) If true, do not relay this sweep transfer. (Defaults to false).
* _get\_tx\_hex_ - boolean; (Optional) return the transactions as hex encoded string. (Defaults to false).
* _get\_tx\_metadata_ - boolean; (Optional) return the transaction metadata as a string. (Defaults to false).

Outputs:

* _tx\_hash_ - String for the publically searchable transaction hash.
* _tx\_key_ - String for the transaction key if get\_tx\_key is true, otherwise, blank string.
* _amount_ - Amount transferred for the transaction.
* _fee_ - Integer value of the fee charged for the txn.
* _tx\_blob_ - Raw transaction represented as hex string, if get\_tx\_hex is true.
* _tx\_metadata_ - Set of transaction metadata needed to relay this transfer later, if get\_tx\_metadata is true.
* _multisig\_txset_ - Set of multisig transactions in the process of being signed (empty for non-multisig).
* _unsigned\_txset_ - String. Set of unsigned tx for cold-signing purposes.

Example:

<pre><code><strong>$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"bns_update_mapping","params":{"name":"toretto.bdx","value_bchat" : "bdff403a579c24edd0b973f9f00211ab3574ec083b2fd97b8b87de0e413e969942","value_belnet":"i85hpmcge4huukrxp8xnobkh7eodhsuy7dy8yphq9zafhcqeeago.bdx"}}' -H 'Content-Type: application/json'
</strong>{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount": 0,
    "fee": 14445250,
    "multisig_txset": "",
    "tx_blob": "",
    "tx_hash": "54dfe6c38c37135274380cfcffaeb4167f76176e15d13b4377fcc5c88115efb7",
    "tx_key": "",
    "tx_metadata": "",
    "unsigned_txset": ""
  }
}
</code></pre>

### bns\_make\_update\_mapping\_signature <a href="#sources" id="sources"></a>

In order to modify the Owner or BackupOwner of a wallet that currently lacks ownership, it is imperative to provide the corresponding signature. This signature is essential for executing the alteration through the bns\_update\_mapping function within alternative wallets.

Alias: _None_.

Inputs:

* _name_ - string; The name to Update using signature.
* _owner_ - string; (Optional) The ed25519 public key or wallet address that has authority to update the mapping.
* _backup\_owner_ - string; (Optional) The secondary, backup public key that has authority to update the mapping.
* _account\_index_ - uint32\_t; (Optional) Transfer from this account index. (Defaults to 0).&#x20;

Output:

* _signature -_ A signature valid for using in BNS to update an underlying mapping.

Example:

<pre><code><strong>$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"bns_make_update_mapping_signature","params":{"name":"toretto.bdx","owner" : "A2Xf197qvYWAiCq525cREG2HdWhDvACVDSmmQzGa3Ajm3H5P3ktXiUTSP4j3RZ5ZnMDnDkpFihr3oFRrj2iYkuvX47LeHmT"}}' -H 'Content-Type: application/json'
</strong>{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "signature": "73ef1fbcdb98f73250252cb7fece312a37eac58875451145f498eaa49a9514051d8fcdb417026192a7c07269a092c5184a9be53e8896deceb5d42716b7cb5c03"
  }
}
</code></pre>

### bns\_hash\_name <a href="#sources" id="sources"></a>

View the hash of the BNS name.

Alias: _None_.

Input:

* _name_ - string; The desired name to hash.

Output:

* name  - The name hashed and represented in base64.

Example:

<pre><code><strong>$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"bns_hash_name","params":{"name":"toretto.bdx"}}' -H 'Content-Type: application/json'
</strong>{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "name": "4dknDpBMCXaxpvT72UvmYkyL4CgH7D0wVx3I1/unikg="
  }
}
</code></pre>

### bns\_known\_names <a href="#sources" id="sources"></a>

Retrieve a list of BNS Names linked with a wallet.

Alias: _None_.

Inputs:

* _decrypt_ - boolean; (Optional) If true (default false) then also decrypt and include the \`value\` field.
* _include\_expired_ - boolean; (Optional) If true (default false) then also include expired records.

Outputs:

* _hashed_ - The hashed name (in base64).
* _name_ - The plaintext name.
* _owner_ - Address of the wallet.
* _backup\_owner_ - backup\_owner address if given.
* _encrypted\_bchat\_value_ - Encrypted value of bchat that the name maps to, in hex.
* _encrypted\_wallet\_value_ - Encrypted value of BDX wallet address that the name maps to, in hex.
* _encrypted\_eth\_addr\_value_ - Encrypted value of eth address that the name maps to, in hex.
* _encrypted\_belnet\_value_ - Encrypted value of belnet  address that the name maps to, in hex.
* _bchat\_value_ - Decrypted bchat value that  the name maps to.  Only provided if \`decrypt: true\` was specified in the request.
* _wallet\_value_ - Decrypted wallet value that  the name maps to.  Only provided if \`decrypt: true\` was specified in the request.
* _belnet\_value_ - Decrypted belnet value that that the name maps to.  Only provided if \`decrypt: true\` was specified in the request.
* _eth\_addr\_value_ - Decrypted etc address value that the name maps to.  Only provided if \`decrypt: true\` was specified in the request.
* _update\_height_ - Last height that this Beldex Name Service entry was updated on the Blockchain.
* _expiration\_height_ - For records that expire, this will be set to the expiration block height.
* _expired_ - Indicates whether the record has expired. Only included in the response if "include\_expired" is specified in the request.
* _txid_ - transaction id.

Example:

<pre><code><strong>$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"bns_known_names","params":{"decrypt":true}}' -H 'Content-Type: application/json'
</strong>{ 
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "known_names": [{
      "encrypted_bchat_value": "a55e54b4a5ed729db677a5ab1b64255de2a8e0311611e273ad52c0e260a542a1a0979f7ff1c09a6ba3aafc6524d41161b991dccd9f45bc0e1f9c2ac57ad9b77718a59ee27aa9d1957c",
      "encrypted_belnet_value": "407e37d23b2679fbfc21a3c0232b43f003e457a10dd942032f6d44c91683028e160eda51baeecc3f82935a7a7607266493317132236e93c9785cdbf2a24beba7804de46e86f2807d",
      "encrypted_wallet_value": "",
      "encrypted_eth_addr_value": "",
      "expiration_height": 1358011,
      "hashed": "4dknDpBMCXaxpvT72UvmYkyL4CgH7D0wVx3I1/unikg=",
      "name": "toretto.bdx",
      "owner": "9zy7tYvhhjGUPByuk8AxvjJtK2gK7Vt4ebHSS7QuKojeD7hR6G2253aMmFCpcwaAjXR75BWy7Vjor5chH3nG79Uk3aRqWtR",
      "txid": "54dfe6c38c37135274380cfcffaeb4167f76176e15d13b4377fcc5c88115efb7",
      "update_height": 1314827,
      "value_bchat": "bdff403a579c24edd0b973f9f00211ab3574ec083b2fd97b8b87de0e413e969942",
      "value_belnet": "i85hpmcge4huukrxp8xnobkh7eodhsuy7dy8yphq9zafhcqeeago.bdx"
    }]
  }
}
</code></pre>

### bns\_add\_known\_names <a href="#sources" id="sources"></a>

Add the BNS names in the cache.

Alias: _None_.

Input:

* _names_ - array of string; The (unhashed) name of the record.

Outputs: _None_.

Example:

<pre><code><strong>$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{ "jsonrpc": "2.0","id": "0", "method":"bns_add_known_names","params": {"names": [{"name": "victor.bdx"},{"name":"toretto.bdx"}]}}' -H 'Content-Type:application/json'
</strong><strong>{
</strong>  "id": "0",
  "jsonrpc": "2.0",
  "result": {}
} 
</code></pre>

### bns\_encrypt\_value <a href="#sources" id="sources"></a>

Retrieve the encrypted value of the specified BNS value by indicating the type.

Alias: _None_.

Input:

* _name_ - string; The BNS name with which to encrypt the value.
* _type_ - string; The mapping type: "bchat" or "belnet" or "wallet".
* _value - string;_ The value to be encrypted.

Output:

* _encrypted\_value -_ The encrypted value, in hex.

Example:

<pre><code><strong>$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"bns_encrypt_value","params":{"name":"toretto.bdx","type":"wallet","value":"9zy7tYvhhjGUPByuk8AxvjJtK2gK7Vt4ebHSS7QuKojeD7hR6G2253aMmFCpcwaAjXR75BWy7Vjor5chH3nG79Uk3aRqWtR"}}' -H 'Content-Type: application/json'
</strong>{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "encrypted_value": "10686ec966200761f967ff88084590a91eb1770b9a374f2752f63b715b50be4169ad3271387ef1bf03c2ebff362df66359eff223680e6f5ad07f5b6dc24a3b2ba0f9c6bfc62083a0d2"
  }
}
</code></pre>

### bns\_decrypt\_value <a href="#sources" id="sources"></a>

Decrypt the BNS value corresponding to the provided encrypted value.

Alias: _None_.

Inputs:

* _name_ - string; The BNS name with which to encrypt the value.
* _type_ - string; The mapping type: "bchat" or "belnet" or "wallet".
* _encrypted\_value_ - string; The encrypted value represented in hex.

Output:

* _value -_ The value decrypted.

Example:

<pre><code><strong>$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"bns_decrypt_value","params":{"name":"toretto.bdx","type":"bchat","encrypted_value":"10686ec966200761f967ff88084590a91eb1770b9a374f2752f63b715b50be4169ad3271387ef1bf03c2ebff362df66359eff223680e6f5ad07f5b6dc24a3b2ba0f9c6bfc62083a0d2"}}' -H 'Content-Type: application/json'
</strong>{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "value": "bdff403a579c24edd0b973f9f00211ab3574ec083b2fd97b8b87de0e413e969942"
  }
}
</code></pre>

### coin\_burn <a href="#sources" id="sources"></a>

The specified amount will be burnt from the provided tx\_id using the unspent transaction or amount.

Alias: _None_.

Inputs:

* _amount_ - uint64\_t; burn amount.
* _tx\_id_ - string; Transaction ID used to find the transfer.
* _account\_index_ - uint32\_t; (Optional) Transfer from this account index. (Defaults to 0).&#x20;
* _subaddr\_indices_ - array of unsigned int; (Optional) List of subaddress indices to query for transfers. (defaults to 0).
* _priority_ - unsigned int; Set a priority for the transaction. Accepted Values are: 0 and 1 for: flash and unimportant.
* _get\_tx\_key_ - boolean; (Optional) Return the transaction keys after sending.
* _do\_not\_relay_ - boolean; (Optional) If true, do not relay this sweep transfer. (Defaults to false).
* _get\_tx\_hex_ - boolean; (Optional) return the transactions as hex encoded string. (Defaults to false).
* _get\_tx\_metadata_ - boolean; (Optional) return the transaction metadata as a string. (Defaults to false).

Output:

* _tx\_hash_ - String for the publicly searchable transaction hash.
* _tx\_key_ - String for the transaction key if get\_tx\_key is true, otherwise, blank string.
* _amount_ - Amount transferred for the transaction.
* _fee_ - Integer value of the fee charged for the txn.
* _tx\_blob_ - Raw transaction represented as hex string, if get\_tx\_hex is true.
* _tx\_metadata_ - Set of transaction metadata needed to relay this transfer later, if get\_tx\_metadata is true.
* _multisig\_txset_ - Set of multisig transactions in the process of being signed (empty for non-multisig).
* _unsigned\_txset_ - String. Set of unsigned tx for cold-signing purposes.

Examples:

**coin burn using tx\_id**

<pre><code><strong>$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"coin_burn","params":{"tx_id" : "3d3d3b30bbf64ea1e7308bdb6e30f88660dd6b0084ae49092c4b264a0335f503"}}' -H 'Content-Type: application/json'
</strong>{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount": 0,
    "fee": 10000000000,
    "multisig_txset": "",
    "tx_blob": "",
    "tx_hash": "903497fe966ce2c0b311d22565eb92b00e3fcb5ebce5f2d89ec2922f92e2afdc",
    "tx_key": "",
    "tx_metadata": "",
    "unsigned_txset": ""
  }
}
</code></pre>

**coin burn using amount**

<pre><code><strong>$ curl -X POST http://127.0.0.1:19092/json_rpc -d '{"jsonrpc":"2.0","id":"0","method":"coin_burn","params":{"amount":1000000000}}' -H 'Content-Type: application/json'
</strong>{
  "id": "0",
  "jsonrpc": "2.0",
  "result": {
    "amount": 0,
    "fee": 1012638760,
    "multisig_txset": "",
    "tx_blob": "",
    "tx_hash": "8d5dfd6d451da2d7aa730fb17ee95d6669774878889ff8f78d4c2f85a3fdcb06",
    "tx_key": "",
    "tx_metadata": "",
    "unsigned_txset": ""
  }
}
</code></pre>



#### Sources: <a href="#sources" id="sources"></a>

Reworked [GetMonero.org](https://ww.getmonero.org/resources/developer-guides/wallet-rpc.html) RPC calls for Beldex under their [copyright license](https://ww.getmonero.org/legal/#copyright).
