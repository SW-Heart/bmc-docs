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

//Response
{
"jsonrpc":"2.0",
"id":12,
"result":"0x92765"
}
```

### API method

* [`eth_blockNumber`](#eth_blockNumber)
* [`eth_getBlockByNumber`](#eth_getBlockByNumber)
* [`eth_getBlockByHash`](#eth_getBlockByHash)
* [`eth_getBlockTransactionCountByNumber`](#eth_getBlockTransactionCountByNumber)
* [`eth_getBlockTransactionCountByHash`](#eth_getBlockTransactionCountByHash)
* [`eth_getUncleCountByBlockHash`](#eth_getUncleCountByBlockHash)
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

Returns the current block height.

##### Parameters

None

##### Returns

`Object`:

- `String` - *result*,Returns the current block height

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

//Response
{
"jsonrpc":"2.0",
"id":12,
"result":"0x92765"
}
```
#### `eth_getBlockByNumber`

Returns information about a block by block number(hex encoded unsigned integer).

##### Parameters

`Object`:

- `String` & `Boolean`- *params*
  - `String` - *Block Number*
  - `Boolean`, If true it returns the full transaction objects, if false only the hashes of the transactions.

##### Returns

`Object` - The matching block object, or null if the block is not found, the structure is as follows:

- `String` - *result* 
  {
  - `String` - *difficulty*,The difficulty value of the block, as an integer.
  - `String` - *extraData*,Block extra data.
  - `String` - *gasLimit*,The maximum amount of gas allowed for this block.
  - `String` - *gasUsed*,The total gas used by all transactions in this block.
  - `String` - *hash*,The block hash, the pending block is null.
  - `String` - *logsBloom*,Bloom filter for the block log, pending blocks are null.
  - `String` - *miner*,The receiving account of mining rewards.
  - `String` - *mixHash*,mixHash
  - `String` - *nonce*,nonce
  - `String` - *Number*,The block number, the pending block is null.
  - `String` - *parentHash*,Parent block hash.
  - `String` - *receiptsRoot*,The root node of the block transaction receipt tree.
  - `String` - *sha3Uncles*,The SHA3 hash of the uncle data in the block.
  - `String` - *size*,Block size, the number of bytes in this block.
  - `String` - *stateRoot*,The root node of the final state tree of the block.
  - `String` - *timestamp*,timestamp
  - `String` - *totalDifficulty*,The total difficulty on the chain as of this block.
  - `String` - *transactions*,An array of transaction objects, or a 32-byte long array of transaction hashes.
  - `String` - *transactionsRoot*,Transaction data root node.
  - `String` - *uncles* ,Array of uncle block hashes.
}

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
"result":{
"difficulty":"0x2",
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
"transactions":[],
"transactionsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
"uncles":[]}}
```

#### `eth_getBlockByHash`

##### Parameters

`Object`:

- `String` - *Block Number*, 32-byte block hash.
- `Boolean`, If true it returns the full transaction objects, if false only the hashes of the transactions.

##### Returns

`Object` - The matching block object, or null if the block is not found, the structure is as follows:

- `String` - *result* 
  {
  - `String` - *difficulty*,The difficulty value of the block, as an integer.
  - `String` - *extraData*,Block extra data.
  - `String` - *gasLimit*,The maximum amount of gas allowed for this block.
  - `String` - *gasUsed*,The total gas used by all transactions in this block.
  - `String` - *hash*,The block hash, the pending block is null.
  - `String` - *logsBloom*,Bloom filter for the block log, pending blocks are null.
  - `String` - *miner*,The receiving account of mining rewards.
  - `String` - *mixHash*,mixHash
  - `String` - *nonce*,nonce
  - `String` - *Number*,The block number, the pending block is null.
  - `String` - *parentHash*,Parent block hash.
  - `String` - *receiptsRoot*,The root node of the block transaction receipt tree.
  - `String` - *sha3Uncles*,The SHA3 hash of the uncle data in the block.
  - `String` - *size*,Block size, the number of bytes in this block.
  - `String` - *stateRoot*,The root node of the final state tree of the block.
  - `String` - *timestamp*,timestamp
  - `String` - *totalDifficulty*,The total difficulty on the chain as of this block.
  - `String` - *transactions*,An array of transaction objects, or a 32-byte long array of transaction hashes.
  - `String` - *transactionsRoot*,Transaction data root node.
  - `String` - *uncles* ,Array of uncle block hashes.
}

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_getBlockByHash",
    "params": ["0x92765",true],
    "id": 12
}'

//Respond
{
"jsonrpc":"2.0",
"id":12,
"result":{
"difficulty":"0x2",
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
"transactions":[],
"transactionsRoot":"0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
"uncles":[]}}
```

#### `eth_getBlockTransactionCountByNumber`

Returns the total transaction count for a given block number.

##### Parameters

`Object`:

- `String` - *params*, a Block number,hex encoded unsigned integer

##### Returns

`Object`:

- `String` - *result* ,Specifies the number of transactions within the block.

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

#### `eth_getBlockTransactionCountByHash`

Returns the number of transactions within the given hash block.

##### Parameters

`Object`:

- `String` - *params*, 32-byte block hash.

##### Returns

`Object`:

- `String` - *result*, Specifies the number of transactions within the block, an integer.

##### Example

```js
//Request
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_getBlockTransactionCountByHash",
    "params": ["0x66f2ef5b9eddaa63b5501dec4a3d6740c914ddf6419aec1771479c6476454a11"],
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

Returns the number of uncle blocks for a given block number.

##### Parameters

`Object`:

- `String` - *params*,a Block number,hex encoded unsigned integer

##### Returns

`Object`:

- `String` - *result*, the number of uncle blocks for the specified block.

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

For synchronized clients, the call returns an object describing the synchronization state; for unsynchronized clients, it returns false.

##### Parameters

None

##### Returns

`Object` - Sync state object or false.

- `Boolean` - *result*, should always return false if out of sync.

The structure of the synchronization object is as follows:

- `String` - *startingBlock*, starting block.
- `String` - *currentBlock*, the current block.
- `String` - *highestBlock*, estimated highest block.

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

None

##### Returns

`Object`:

- `String` - *result*, A list of address strings held by the client.

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

None

##### Returns

`Object`:

- `String` - *result*, Integer, the current gas price in wei.

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

Create a filter in the node to be notified when a new block is generated. To check for state changes, call `eth_getFilterChanges`.

##### Parameters

None

##### Returns

`Object`:

- `String` - *result*,filter number.

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

Create a filter in the node to be notified when pending transactions are generated. To check for state changes, call `eth_getFilterChanges`.

##### Parameters

None

##### Returns

`Object`:

- `String` - *result*, filter number.

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

Write on the filter with the specified number. This call is always executed when listening is no longer required. Additionally, the filter automatically times out if the `eth_getFilterChanges` call is not received within a certain period of time.

##### Parameters

`Object`:

- `String` - *params*,filter number.

##### Returns

`Object`:

- `Boolean` - *result*,Returns true if the uninstall was successful, false otherwise.

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

None

##### Returns

`Object`:

- `Bool` - *result*,  Returns true when the client is mining, otherwise returns false.

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

Returns the number of hashes the node can compute per second when mining.

##### Parameters

None

##### Returns

`Object`:

- `String` - *Hashrate*,The number of hashes computed per second.

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
