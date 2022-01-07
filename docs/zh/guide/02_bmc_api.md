## Node API

### 如何去使用 API

| Client   | URL   |
|:--:   |:--:   |
|Go   |http://localhost:8545|

### Go
```js
//请求
curl --location --request POST 'http://localhost:8545' \
--header 'Content-Type: application/json' \
--data '{
    "jsonrpc": "2.0",
    "method": "eth_blockNumber",
    "params": [],
    "id": 12
}'

//响应
{
"jsonrpc":"2.0",
"id":12,
"result":"0x92765"
}
```

### API 方法

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

返回当前块高度。

##### 参数

`Object`:

- `String` - *jsonrpc*
- `String` - *method*
- `String` - *params*，空
- `String` - *id*

##### 返回值

`Object`:

- `String` - *jsonrpc*
- `String` - *id*
- `String` - *result*, 返回当前区块高度（^0x（[1-9a-f]+[0-9a-f]*|0）$）

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' \
--header 'Content-Type: application/json' \
--data '{
    "jsonrpc": "2.0",
    "method": "eth_blockNumber",
    "params": [],
    "id": 12
}'

//响应
{
"jsonrpc":"2.0",
"id":12,
"result":"0x92765"
}
```
#### `eth_getBlockByNumber`

按区块编号（十六进制编码的无符号整数）返回有关区块的信息。

##### 参数

`Object`:

- `String` - *jsonrpc*
- `String` - *method*，方法名
- `String` & `Boolean`- *params*，参数
  - `String` - *Block Number*，区块号
  - `Boolean`, 如果为 true，则返回完整的交易对象，如果为 false，则仅返回交易的哈希值。
- `String` - *id*

##### 返回值

`Object`:

- `String` - *jsonrpc*
- `String` - *id*
- `String` - *result* 
  {
  - `String` - *difficulty*，难度值（ ^0x[0-9a-f]*$）
  - `String` - *extraData*，额外数据（ ^0x[0-9a-f]*$）
  - `String` - *gasLimit*，燃料限制（^0x([1-9a-f]+[0-9a-f]*|0)$）
  - `String` - *gasUsed*，使用的燃料（ ^0x([1-9a-f]+[0-9a-f]*|0)$）
  - `String` - *hash*，哈希
  - `String` - *logsBloom*，Bloom filter(pattern - ^0x[0-9a-f]{512}$).
  - `String` - *miner*，Coinbase 矿工（^0x[0-9,a-f,A-F]{40}$）
  - `String` - *mixHash*，混合哈希（^0x[0-9a-f]{64}$）
  - `String` - *nonce*，随机数（^0x[0-9a-f]*$）
  - `String` - *Number*，区块号（^0x([1-9a-f]+[0-9a-f]*|0)$）
  - `String` - *parentHash*，父区块哈希（^0x[0-9a-f]{64}$）
  - `String` - *receiptsRoot*，根哈希（^0x[0-9a-f]{64}$）
  - `String` - *sha3Uncles*，叔块哈希（^0x[0-9a-f]{64}$）
  - `String` - *size*，区块大小（^0x([1-9a-f]+[0-9a-f]*|0)$）
  - `String` - *stateRoot*，状态根（^0x[0-9a-f]{64}$）
  - `String` - *timestamp*，时间戳（^0x([1-9a-f]+[0-9a-f]*|0)$）
  - `String` - *totalDifficulty*，总难度值（^0x([1-9a-f]+[0-9a-f]*|0)$）
  - `String` - *transactions*，交易
  - `String` - *transactionsRoot*，交易的哈希根（^0x[0-9a-f]{64}$）
  - `String` - *uncles* 
}

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_getBlockByNumber",
    "params": ["0x92765",true],
    "id": 12
}'

//响应
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

返回给定区块号的总交易数。

##### 参数

`Object`:

- `String` - *jsonrpc*
- `String` - *method*
- `String` - *params*, 区块编号：十六进制编码的无符号整数（^0x([1-9a-f]+[0-9a-f]*|0)$）。
- `String` - *id*

##### 返回值

`Object`:

- `String` - *jsonrpc*
- `String` - *id*
- `String` - *result* ,交易计数，十六进制编码的无符号整数（^0x([1-9a-f]+[0-9a-f]*|0)$）

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_getBlockTransactionCountByNumber",
    "params": ["0x92765"],
    "id": 12
}'

//响应
{
"jsonrpc":"2.0",
"id":12,
"result":"0x0"
}

```
#### `eth_getUncleCountByBlockNumber`

根据给定区块号，返回块中的交易数。

##### 参数

`Object`:

- `String` - *jsonrpc*
- `String` - *method*
- `String` - *params*，区块号，十六进制编码的无符号整数（^0x([1-9a-f]+[0-9a-f]*|0)$）
- `String` - *id*

##### 返回值

`Object`:

- `String` - *jsonrpc*
- `String` - *id*
- `String` - *result*, 交易数（^0x([1-9a-f]+[0-9a-f]*|0)$）

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_getUncleCountByBlockNumber",
    "params": ["0x92765"],
    "id": 12
}'

//响应
{
"jsonrpc":"2.0",
"id":12,
"result":"0x0"
}
```

#### `eth_syncing`

根据 Tendermint 同步协议的详细信息，导出布尔值的同步状态。

##### 参数

- `String` - *jsonrpc*
- `String` - *method*
- `String` - *params*，空
- `String` - *id*

##### 返回值

`Object`:

- `String` - *jsonrpc*
- `String` - *id*
- `Boolean` - *result*，如果不同步，应该总是返回 false。

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_syncing",
    "params": [],
    "id": 12
}'

//响应
{
"jsonrpc": "2.0",
  "id": 12,
  "result":false
}
```

#### `eth_accounts`

返回客户端拥有的地址列表。

##### 参数

- `String` - *jsonrpc*
- `String` - *method*
- `String` - *params*，空
- `String` - *id*

##### 返回值

`Object`:

- `String` - *jsonrpc*
- `String` - *id*
- `String` - *result*, *Accounts*,十六进制编码地址（pattern - ^0x[0-9,a-f,A-F]{40}$）

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_accounts",
    "params": [],
    "id": 12
}'

//响应
{
"jsonrpc": "2.0",
 "id": 12,
 "result":[]
}
```

#### `eth_gasPrice`

以wei为单位返回每个gas的当前价格。

##### 参数

`Object`:

- `String` - *jsonrpc*
- `String` - *method*
- `String` - *params*，空
- `String` - *id*

##### 返回值

`Object`:

- `String` - *jsonrpc*
- `String` - *id*
- `String` - *result*, Gas价格（^0x([1-9a-f]+[0-9a-f]*|0)$）

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_gasPrice",
    "params": [],
    "id": 12
}'

//响应
{
"jsonrpc": "2.0",
"id": 12,
"result":"0x3b9aca00"
}
```

#### `eth_newBlockFilter`

在节点中创建过滤器，用以在新块到达时进行通知。

##### 参数

`Object`:

- `String` - *jsonrpc*
- `String` - *method*
- `String` - *params*，空
- `String` - *id*

##### 返回值

`Object`:

- `String` - *jsonrpc*
- `String` - *id*
- `String` - *result*, 过滤器，一个十六进制编码的无符号整数（^0x([1-9a-f]+[0-9a-f]*|0)$）

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_newBlockFilter",
    "params": [],
    "id": 12
}'

//响应
{
"jsonrpc": "2.0",
"id": 12,
"result":"0xbffb379bfba8434b4f7b45bc09718300"
}
```
#### `eth_newPendingTransactionFilter`

在节点中创建过滤器，用以在新的待处理交易到达时进行通知。

##### 参数

`Object`:

- `String` - *jsonrpc*
- `String` - *method*
- `String` - *params*，空
- `String` - *id*

##### 返回值

`Object`:

- `String` - *jsonrpc*
- `String` - *id*
- `String` - *result*, 交易过滤器，十六进制编码的无符号整数（^0x([1-9a-f]+[0-9a-f]*|0)$）

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_newPendingTransactionFilter",
    "params": [],
    "id": 12
}'

//响应
{
"jsonrpc": "2.0",
"id": 12,
"result":"0x11a1e4f3e5e6ead5922574ed4e9b4b2b"
}
```

#### `eth_uninstallFilter`

删除具有给定过滤器 ID 的过滤器。 如果过滤器已成功卸载，则返回 true，否则返回 false。

##### 参数

`Object`:

- `String` - *jsonrpc*
- `String` - *method*
- `String` - *params*，交易哈希
- `String` - *id*

##### 返回值

`Object`:

- `String` - *jsonrpc*
- `String` - *id*
- `Boolean` - *result*

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_uninstallFilter",
    "params": ["0x11a1e4f3e5e6ead5922574ed4e9b4b2b"],
    "id": 12
}'

//响应
{
"jsonrpc": "2.0",
"id": 12,
"result":"false"
}
```

#### `eth_mining`

返回客户端是否正在挖掘新区块。

##### 参数

`Object`:

- `String` - *jsonrpc*
- `String` - *method*
- `String` - *params*，空
- `String` - *id*

##### 返回值

`Object`:
- `String` - *jsonrpc*
- `String` - *id*
- `Bool` - *result*,  挖矿状态

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_mining",
    "params": [],
    "id": 12
}'

//响应
"jsonrpc": "2.0",
"id": 12,
"result":"false"
```

#### `eth_hashrate`

返回节点正在挖矿的每秒哈希数。

##### 参数

`Object`:

- `String` - *jsonrpc*
- `String` - *method*
- `String` - *params*，空
- `String` - *id*

##### 返回值

`Object`:

`Object`:
- `String` - *jsonrpc*
- `String` - *id*
- `String` - *result*
- `String` - *Hashrate*,哈希（^0x([1-9a-f]+[0-9a-f]*|0)$）

##### 例子

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_mining",
    "params": [],
    "id": 12
}'

//响应
"jsonrpc": "2.0",
"id": 12,
"result":"0x0"
```
