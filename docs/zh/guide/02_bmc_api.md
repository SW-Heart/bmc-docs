## Node API

### How to use API

| Client   | URL   |
|:--:   |:--:   |
|Go   |http://localhost:8545|

### Go
```js
//Request
curl --location --request POST 'http://localhost:8545' \
--header 'Content-Type: application/json' \
--data '{
    "jsonrpc": "2.0",
    "method": "eth_blockNumber",
    "params": [],
    "id": 12
}'

//response
{
"jsonrpc":"2.0",
"id":12,
"result":"0x92765"
}
```

### API method

* [`eth_blockNumber`](#eth_blockNumber)
* [`eth_getBlockByNumber`](#eth_getBlockByNumber)
* [`eth_getBlockTransactionCountByNumber`](#eth_getBlockTransactionCountByNumber)
* [`eth_getUncleCountByBlockNumber`](#eth_getUncleCountByBlockNumber)
* [`eth_syncing`](#eth_syncing)
* [`eth_accounts`](#eth_accounts)
* [`eth_gasPrice`](#eth_gasPrice)
* [`eth_newBlockFilter`](#eth_newBlockFilter)
* [`eth_newPendingTransactionFilter`](#eth_newPendingTransactionFilter)
* [`eth_uninstallFilter`](#eth_uninstallFilter)
* [`eth_mining`](#eth_mining)
* [`eth_hashrate`](#eth_hashrate)

#### `eth_blockNumber`

It is to return the number of most recent block,it is a hex encoded unsigned integer.

##### Parameters

none

##### Returns

`Object`:

- `String` - *Number*,the number of most recent block.(pattern:^0x([1-9a-f]+[0-9a-f]*|0)$)

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' \
--header 'Content-Type: application/json' \
--data '{
    "jsonrpc": "2.0",
    "method": "eth_blockNumber",
    "params": [],
    "id": 12
}'

//response
{
"jsonrpc":"2.0",
"id":12,
"result":"0x92765"
}
```
#### `eth_getBlockByNumber`

Returns information about a block number(hex encoded unsigned integer).

##### Parameters

`Object`:

- `String` - *Number*,hex encoded unsigned integer(pattern:^0x([1-9a-f]+[0-9a-f]*|0)$).
- `bool` - *hydrated*,Hydrated transactions

##### Returns


`Object`:
- `String` - *parentHash*,Parent block hash(pattern:^0x[0-9a-f]{64}$).
- `String` - *sha3Uncles*,Ommers hash(pattern - ^0x[0-9a-f]{64}$)
- `String` - *miner*,miner of  Coinbase(pattern - ^0x[0-9,a-f,A-F]{40}$).
- `String` - *stateRoot*,the stateRoot(pattern - ^0x[0-9a-f]{64}$).
- `String` - *transactionsRoot*,the root of transactions(pattern - ^0x[0-9a-f]{64}$).
- `String` - *receiptsRoot*,Receipts root(pattern - ^0x[0-9a-f]{64}$).
- `String` - *logsBloom*,Bloom filter(pattern - ^0x[0-9a-f]{512}$).
- `String` - *difficulty*,Difficulty(pattern - ^0x[0-9a-f]*$).
- `String` - *Number*,Number(pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$).
- `String` - *gasLimit*,Gas limit(pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$).
- `String` - *gasUsed*,Gas used(pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$).
- `String` - *timestamp*,timestamp(pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$).
- `String` - *extraData*,Extra data(pattern - ^0x[0-9a-f]*$).
- `String` - *mixHash*,mixHash(pattern - ^0x[0-9a-f]{64}$).
- `String` - *nonce*,Nonce(pattern - ^0x[0-9a-f]*$).
- `String` - *totalDifficulty*Total difficult(pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$)
- `String` - *baseFeePerGas*,Base fee per gas(pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$).
- `String` - *size*,Block size(pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$).
- `String` - *transactions*
- `String` - *uncles*

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_getBlockByNumber",
    "params": ["0x92765",true],
    "id": 12
}'

//Respond
{
"jsonrpc":"2.0",
"id":12,
"result":{"difficulty":"0x2",
"extraData":"0xd883010000846765746888676f312e31332e34856c696e7578000000b27786dcf244b57773227818910a33c3af6ed4c4cd43e71694bc33aeec38e01add410948445bae6221179c480240cc9a185e9e1d3e582023dee006f71c0e0f4ebc36ffb500",
"gasLimit":"0x1c9c380",
"gasUsed":"0x0",
"hash":"0x66f2ef5b9eddaa63b5501dec4a3d6740c914ddf6419aec1771479c6476454a11",
"logsBloom":"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
"miner":"0x52093c7d03be906c37e0ecb42fd0d9ea1cfb1c0a",
"mixHash":"0x0000000000000000000000000000000000000000000000000000000000000000",
"nonce":"0x0000000000000000",
"number":"0x92765",
"parentHash":"0xd301cd0fe5752cd5a6395f926a195e8350f38cab1287316cc3a67bd87b7f3d0e",
"receiptsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
"sha3Uncles":"0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
"size":"0x262",
"stateRoot":"0x2813cddc28afe8313026fbb878ff5de2625b8a903af20eea899db233e3059f32",
"timestamp":"0x61d68803",
"totalDifficulty":"0x124cc3",
"transactions":[],"transactionsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
"uncles":[]}}
```

#### `eth_getBlockTransactionCountByNumber`

Returns the number of transactions in a block from a block matching the given block number.

##### Parameters

`Object`:

- `String` - *Block number*,hex encoded unsigned integer(pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$).

##### Returns

`Object`:

- `String` - *Transaction count*,hex encoded unsigned integer(pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$)

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_getBlockTransactionCountByNumber",
    "params": ["0x92765"],
    "id": 12
}'

//Respond
{
"jsonrpc":"2.0",
"id":12,
"result":"0x0"
}

```
#### `eth_getUncleCountByBlockNumber`

Returns the number of transactions in a block from a block matching the given block number.

##### Parameters

`Object`:

- `String` - *Transaction count*,hex encoded unsigned integer(pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$)

##### Returns

`Object`:

- `String` - *Transaction count*,hex encoded unsigned integer(pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$)

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_getUncleCountByBlockNumber",
    "params": ["0x92765"],
    "id": 12
}'

//Respond
{
"jsonrpc":"2.0",
"id":12,
"result":"0x0"
}
```

#### `eth_syncing`

Returns an object with data about the sync status or false.

##### Parameters

none

##### Returns

`Object`:

- `Bool` - *Not syncing*,Should always return false if not syncing.

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_syncing",
    "params": [],
    "id": 12
}'

//Respond
{
"jsonrpc": "2.0",
  "id": 12,
  "result":false
}
```

#### `eth_accounts`

Return a list of addresses owned by client.

##### Parameters

none

##### Returns

`Object`:

- `String` - *Accounts*,hex encoded address(pattern - ^0x[0-9,a-f,A-F]{40}$).

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_accounts",
    "params": [],
    "id": 12
}'

//Respond
{
"jsonrpc": "2.0",
 "id": 12,
 "result":[]
}
```

#### `eth_gasPrice`

Return the current price per gas in wei.

##### Parameters

none

##### Returns

`Object`:

- `String` - *Gas price* Gas price(^0x([1-9a-f]+[0-9a-f]*|0)$).

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_gasPrice",
    "params": [],
    "id": 12
}'

//Respond:
{
"jsonrpc": "2.0",
"id": 12,
"result":"0x3b9aca00"
}
```

#### `eth_newBlockFilter`

Creates a filter in the node, to notify when a new block arrives.

##### Parameters

none

##### Returns

`Object`:

- `String` - *Filter*,hex encoded unsigned integer(^0x([1-9a-f]+[0-9a-f]*|0)$).

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_newBlockFilter",
    "params": [],
    "id": 12
}'

//Respond
{
"jsonrpc": "2.0",
"id": 12,
"result":"0xbffb379bfba8434b4f7b45bc09718300"
}
```
#### `eth_newPendingTransactionFilter`

Creates a filter in the node, to notify when new pending transactions arrive.

##### Parameters

none

##### Returns

`Object`:

- `String` - *TransactionFilter*,hex encoded unsigned integer(^0x([1-9a-f]+[0-9a-f]*|0)$).

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_newPendingTransactionFilter",
    "params": [],
    "id": 12
}'

//Respond
{
"jsonrpc": "2.0",
"id": 12,
"result":"0x11a1e4f3e5e6ead5922574ed4e9b4b2b"
}
```

#### `eth_uninstallFilter`

Uninstalls a filter with given id.

##### Parameters

`Object`:

- `String` - *uninstallFilter*, hex encoded unsigned integer(^0x([1-9a-f]+[0-9a-f]*|0)$).

##### Returns

`Object`:

- `Bool` - *result*

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_uninstallFilter",
    "params": ["0x11a1e4f3e5e6ead5922574ed4e9b4b2b"],
    "id": 12
}'

//Respond
{
"jsonrpc": "2.0",
"id": 12,
"result":"false"
}
```

#### `eth_mining`

Returns whether the client is actively mining new blocks.

##### Parameters

none

##### Returns

`Object`:

- `Bool` - *miningStatus*

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_mining",
    "params": [],
    "id": 12
}'

//Respond
"jsonrpc": "2.0",
"id": 12,
"result":"false"
```

#### `eth_hashrate`

Return the number of hashes per second that the node is mining with.

##### Parameters

none

##### Returns

`Object`:

- `String` - *Hashrate*,pattern - ^0x([1-9a-f]+[0-9a-f]*|0)$

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_mining",
    "params": [],
    "id": 12
}'

//Respond
"jsonrpc": "2.0",
"id": 12,
"result":"0x0"
```
