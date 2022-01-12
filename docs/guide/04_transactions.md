###  Transaction

Transactions here refer to operations initiated by externally owned accounts, i.e. accounts managed by humans, not contracts.

##### Trading Information

- `recipient` – the receiving address (if an externally-owned account, the transaction will transfer value. If a contract account, the transaction will execute the contract code)
- `signature` – the identifier of the sender. This is generated when the sender's private key signs the transaction and confirms the sender has authorized this transaction
- `value` – amount of BTM to transfer from sender to recipient
- `data` – optional field to include arbitrary data
- `gasLimit` – the maximum amount of gas units that can be consumed by the transaction. Units of gas represent computational steps
- `maxPriorityFeePerGas` - the maximum amount of gas to be included as a tip to the miner
- `maxFeePerGas` - the maximum amount of gas willing to be paid for the transaction (inclusive of `baseFeePerGas` and `maxPriorityFeePerGas`)

##### Example

```js
//Request
{
  "id": 2,
  "jsonrpc": "2.0",
  "method": "account_signTransaction",
  "params": [
    {
      "from": "0x1923f626bb8dc025849e00f99c25fe2b2f7fb0db",
      "gas": "0x55555",
      "maxFeePerGas": "0x1234",
      "maxPriorityFeePerGas": "0x1234",
      "input": "0xabcd",
      "nonce": "0x0",
      "to": "0x07a565b7ed7d7a678680a4c162885bedbb695fe0",
      "value": "0x1234"
    }
  ]
}

//Respond
{
  "jsonrpc": "2.0",
  "id": 2,
  "result": {
    "raw": "0xf88380018203339407a565b7ed7d7a678680a4c162885bedbb695fe080a44401a6e4000000000000000000000000000000000000000000000000000000000000001226a0223a7c9bcf5531c99be5ea7082183816eb20cfe0bbc322e97cc5c7f71ab8b20ea02aadee6b34b45bb15bc42d9c09de4a6754e7000908da72d48cc7704971491663",
    "tx": {
      "nonce": "0x0",
      "maxFeePerGas": "0x1234",
      "maxPriorityFeePerGas": "0x1234",
      "gas": "0x55555",
      "to": "0x07a565b7ed7d7a678680a4c162885bedbb695fe0",
      "value": "0x1234",
      "input": "0xabcd",
      "v": "0x26",
      "r": "0x223a7c9bcf5531c99be5ea7082183816eb20cfe0bbc322e97cc5c7f71ab8b20e",
      "s": "0x2aadee6b34b45bb15bc42d9c09de4a6754e7000908da72d48cc7704971491663",
      "hash": "0xeba2df809e7a612a0a0d444ccfa5c839624bdc00dd29e3340d46df3870f8a30e"
    }
  }
}
```

##### Transaction Type

- On BMC there are a few different types of transactions:
  - Regular transactions: a transaction from one wallet to another.
  - Contract deployment transactions: a transaction without a 'to' address, where the data field is used for the contract code

##### Transaction Life Cycle

Once the transaction has been submitted the following happens:

1. Once you send a transaction, cryptography generates a transaction hash: `0x97d99bc7729211111a21b12c933c949d4f31684f1d6954ff477d0477538ff017`
2. The transaction is then broadcast to the network and included in a pool with lots of other transactions.
3. A miner must pick your transaction and include it in a block in order to verify the transaction and consider it "successful".
  - You may end up waiting at this stage if the network is busy and miners aren't able to keep up.
4. Your transaction will receive "confirmations". The number of confirmations is the number of blocks created since the block that included your transaction. The higher the number, the greater the certainty that the network processed and recognized the transaction.
  - Recent blocks may get re-organized, giving the impression the transaction was unsuccessful; however, the transaction may still be valid but included in a different block.
  - The probability of a re-organization diminishes with every subsequent block mined, i.e. the greater the number of confirmations, the more immutable the transaction is.

