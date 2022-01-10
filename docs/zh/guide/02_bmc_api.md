## Node API

### 如何使用 API

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

返回当前块高度。

##### 参数

空

##### 返回值

`Object`:

- `String` - *result*, 返回当前区块高度。

##### 示例代码

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

- `String` & `Boolean`- *params*
  - `String`，区块号
  - `Boolean`，如果为 true，则返回完整的交易对象，如果为 false，则仅返回交易的哈希值。

##### 返回值

`Object` - 匹配的区块对象，如果未找到区块则返回null，结构如下：

- `String` - *result* 
  {
  - `String` - *difficulty*，区块的难度值，为整数。
  - `String` - *extraData*，区块额外数据。
  - `String` - *gasLimit*，本区块允许的最大gas用量。
  - `String` - *gasUsed*，本块中所有交易使用的总gas用量。
  - `String` - *hash*，区块哈希，挂起块为null。
  - `String` - *logsBloom*， 区块日志的bloom过滤器，挂起块为null。
  - `String` - *miner*，挖矿奖励的接收账户。
  - `String` - *mixHash*，混合哈希。
  - `String` - *nonce*，随机数。
  - `String` - *Number*，区块编号，挂起块为null。
  - `String` - *parentHash*，父区块哈希。
  - `String` - *receiptsRoot*，区块交易收据树的根节点。
  - `String` - *sha3Uncles*，区块中叔伯数据的SHA3哈希。
  - `String` - *size*，区块大小，本区块字节数。
  - `String` - *stateRoot*，区块最终状态树的根节点。
  - `String` - *timestamp*，时间戳。
  - `String` - *totalDifficulty*，截止到本块的链上总难度。
  - `String` - *transactions*，交易对象数组，或32字节长的交易哈希数组。
  - `String` - *transactionsRoot*，交易数据根节点。
  - `String` - *uncles* ，叔伯区块哈希数组。
}

##### 示例代码

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

#### `eth_getBlockByHash`

返回具有指定哈希的块。

##### 参数

`Object`:

- `String` - 32字节的区块哈希。
- `Boolean`，为true时返回完整的交易对象，否则仅返回交易哈希。

##### 返回值

`Object` - 匹配的块对象，如果未找到块则返回null，结构如下：

- `String` - *result* 
  {
  - `String` - *difficulty*，块的难度值，为整数。
  - `String` - *extraData*，区块额外数据。
  - `String` - *gasLimit*，本区块允许的最大gas用量。
  - `String` - *gasUsed*，本块中所有交易使用的总gas用量。
  - `String` - *hash*，区块哈希，挂起块为null。
  - `String` - *logsBloom*， 区块日志的bloom过滤器，挂起块为null。
  - `String` - *miner*，挖矿奖励的接收账户。
  - `String` - *mixHash*，混合哈希。（^0x[0-9a-f]{64}$）
  - `String` - *nonce*，随机数。
  - `String` - *Number*，区块编号，挂起块为null。
  - `String` - *parentHash*，父区块哈希。
  - `String` - *receiptsRoot*，块交易收据树的根节点。
  - `String` - *sha3Uncles*，区块中叔伯数据的SHA3哈希。
  - `String` - *size*，区块大小，本区块字节数。
  - `String` - *stateRoot*，区块最终状态树的根节点。
  - `String` - *timestamp*，时间戳。
  - `String` - *totalDifficulty*，截止到本块的链上总难度。
  - `String` - *transactions*，交易对象数组，或32字节长的交易哈希数组。
  - `String` - *transactionsRoot*，交易数据根节点。
  - `String` - *uncles* ，叔伯哈希数组。
}

##### 示例代码

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_getBlockByHash",
    "params": ["0x66f2ef5b9eddaa63b5501dec4a3d6740c914ddf6419aec1771479c6476454a11",true],
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

返回给定编号区块内的交易数量。

##### 参数

`Object`:

- `String` - *params*, 区块编号：十六进制编码的无符号整数。

##### 返回值

`Object`:

- `String` - *result* ,指定区块内的交易数量。

##### 示例代码

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

#### `eth_getBlockTransactionCountByHash`

返回给定哈希区块内的交易数量。

##### 参数

- `String` - *params*，32字节的区块哈希。

##### 返回值

- `String` - *result*，指定块内的交易数量，整数。

##### 示例代码

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_getBlockTransactionCountByHash",
    "params": ["0x66f2ef5b9eddaa63b5501dec4a3d6740c914ddf6419aec1771479c6476454a11"],
    "id": 12
}'

//响应
{
"jsonrpc":"2.0",
"id":12,
"result":"0x0"
}

```

#### `eth_getUncleCountByBlockHash`

返回指定哈希的区块的叔伯块数量。

##### 参数

- `String` - *params*，32字节的区块哈希

##### 返回值

- `String` - *result*，指定块的叔伯数量，整数。

##### 示例代码

```js
//请求
curl --location --request POST 'http://localhost:8545' --header 'Content-Type: application/json' --data '{
    "jsonrpc": "2.0",
    "method": "eth_getUncleCountByBlockHash",
    "params": ["0x66f2ef5b9eddaa63b5501dec4a3d6740c914ddf6419aec1771479c6476454a11"],
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

返回给定编号区块的叔伯块数量。

##### 参数

`Object`:

- `String` - *params*，区块号，十六进制编码的无符号整数

##### 返回值

`Object`:

- `String` - *result*, 指定块的叔伯块数量

##### 示例代码

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

对于已经同步的客户端，该调用返回一个描述同步状态的对象；对于未同步客户端，返回false。

##### 参数

空

##### 返回值

`Object` - 同步状态对象或false。

- `Boolean` - *result*，如果不同步，应该总是返回 false。

同步对象的结构如下：

- `String` - *startingBlock*，开始块
- `String` - *currentBlock*，当前块
- `String` - *highestBlock*，预估最高块

##### 示例代码

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

空

##### 返回值

`Object`:

- `String` - *result*, 客户端持有的地址字符串列表。

##### 示例代码

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

返回当前的gas价格，单位：wei。

##### 参数

空

##### 返回值

`Object`:

- `String` - *result*, 整数，以wei为单位的当前gas价格。

##### 示例代码

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

在节点中创建一个过滤器，以便当新块生成时进行通知。要检查状态是否变化， 请调用`eth_getFilterChanges`。

##### 参数

空

##### 返回值

`Object`:

- `String` - *result*,，过滤器编号。

##### 示例代码

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

在节点中创建一个过滤器，以便当产生挂起交易时进行通知。 要检查状态是否发生变化，请调用`eth_getFilterChanges`。

##### 参数

空

##### 返回值

`Object`:

- `String` - *result*, 过滤器编号。

##### 示例代码

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

写在具有指定编号的过滤器。当不在需要监听时，总是需要执行该调用。另外，过滤器 如果在一定时间内未接收到`eth_getFilterChanges`调用会自动超时。

##### 参数

`Object`:

- `String` - *params*，过滤器编号

##### 返回值

`Object`:

- `Boolean` - *result*，如果成功卸载则返回true，否则返回false。

##### 示例代码

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

如果客户端在积极挖矿则返回true。

##### 参数

空

##### 返回值

`Object`：

- `Bool` - *result*,  当客户端在挖矿时返回true，否则返回false。

##### 示例代码

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

返回节点挖矿时每秒可算出的哈希数量。

##### 参数

空

##### 返回值

`Object`:

- `String` - *Hashrate*,每秒算出的哈希数量。

##### 示例代码

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


