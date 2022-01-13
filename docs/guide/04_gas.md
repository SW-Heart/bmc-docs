## Gas and Fees

This tutorial will introduce you to Gas in BMC.

#### What is Gas ?

Gas refers to the computational effort required to perform a specific operation on the BMC.

Since each transaction requires computing resources to execute, each transaction needs to be paid, and Gas refers to the cost of a successful transaction. (*Note: Gas on BMC needs to be paid with BTM, and the accuracy of BTM is 10^-18^*)

#### Why do gas fees exist ?

Gas fees help ensure the security of the BMC network. There is a charge for every computation performed on the network, which prevents participants from spamming the network. To prevent unintentional, malicious, infinite loops or other computational waste in the code, each transaction is required to place a limit on the computational steps the code can perform.

#### Gas calculation rules

Each block has a base fee, and the network calculates the minimum price per unit of gas based on block space requirements. Since the base fee for transaction fees is burned, users also set a tip (priority fee) in their transactions. The small fee is for miners to execute and broadcast blocks containing user transactions and is expected to be set automatically by most wallets.

The total transaction fee is calculated as follows: `Gas unit (limit) * (base fee + tip)`

Suppose Jordan needs to pay Taylor 1 BTM. In the transaction, the miner compensation is limited to 21,000 units, and the price of the base fee is 100 *10^-18^ BTM. Jordan paid 10 *10^-18^ BTM as a tip.

Using the formula above, we can calculate `21,000 * (100 + 10) = 0.00231 BTM` .

When Jordan transfers money, 1.00231 BTM will be debited from Jordan's account. Taylor will get 1.0000 BTM. Miners get 0.00021 BTM. The base fee of 0.0021 BTM is burned.

Additionally, Jordan can set a maximum fee (`maxFeePergas`) for transactions. The difference between the maximum fee and the actual charge will be returned to Jordan. For example: `Refund = Maximum Fee - (Basic Fee + Priority Fee)`. Jordan can set a maximum amount for the execution transaction fee without worrying about "overpaying" the base fee when executing a transaction.

##### Block size

The block size can be changed, with a target size of 15 million gas per block, but the block size will increase or decrease based on network demand. Up to a block limit of 30 million gas (2x the target block size). The protocol achieves an average block size of 15 million through a process of *tâtonnement*. This means that if the block size exceeds the target block size, the protocol will increase the base fee for the following blocks. Likewise, if the block size is lower than the target block size, the protocol will reduce the base fee. The base fee is adjusted in proportion to the difference between the current block size and the target block size.

##### Base fee

Each block has a base fee that is the reserve price. To be eligible to be included in a block, the gas fee quote must be at least equal to the base fee. Base fees are calculated independently of the current block and are determined by blocks preceding the block, making it easier for users to predict transaction fees. When blocks are mined, this base fee is "burned", removed from the cycle.

The base fee is calculated by comparing the size of the previous block (the amount of gas used in all transactions) to the target size. If the target block size is exceeded, the base fee for a block will increase by up to 12.5%. This exponential growth makes it economically unfeasible for block sizes to remain high indefinitely.

| Block Number | Included Gas | Fee Increase | Cueernt Base Fee |
| :------- | :--------- | :------- | :----------- |
| 1        | 15M        | 0%       | 100 *10 ^-9^ BTM    |
| 2        | 30M        | 0%       | 100 *10 ^-9^ BTM    |
| 3        | 30M        | 12.5%    | 112.5 *10 ^-9^ BTM  |
| 4        | 30M        | 12.5%    | 126.6 *10 ^-9^ BTM  |
| 5        | 30M        | 12.5%    | 142.4 *10 ^-9^ BTM  |
| 6        | 30M        | 12.5%    | 160.2 *10 ^-9^ BTM  |
| 7        | 30M        | 12.5%    | 180.2 *10 ^-9^ BTM  |
| 8        | 30M        | 12.5%    | 202.7 *10 ^-9^ BTM  |

##### Priority fee (tips)

Tipping exists to incentivize miners to include transactions in blocks. Without tipping, miners would find it economically viable to mine empty blocks, since they would receive the same block reward. Under normal circumstances, a small tip provides miners with the minimum incentive to include the transaction. For transactions that need to be executed preferentially in the same block, a higher tip is required to try to outbid competing transactions.

##### Max fee

To execute transactions on the network, users can specify a maximum amount of transaction execution fees they are willing to pay. This optional parameter is called `maxFeePergas`. In order to execute the transaction, the maximum fee must exceed the sum of the base fee and tip, and if there is a balance, the difference between the maximum fee and the sum of the base fee and tip is also refunded to the sender of the transaction.

##### EIP - 1559

The gas fee mechanism satisfies [EIP-1559](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1559.md). Users can set a `maxFeePergas` when submitting a transaction, indicating how much they are willing to pay for executing the transaction, knowing that the amount will not exceed the market price of gas (`BaseFeePergas`), and get the remaining refund minus the tip.

#### What is gas limit ?

The gas limit is the maximum amount of gas you are willing to spend in a transaction. More complex transactions involving smart contracts require more computational work, so they require higher gas limits than simple payments. Standard BTM transfers generally require a gas limit of 21,000 units.

For example, if you set a 50,000 gas limit on a simple BTM transfer. The EVM will consume 21,000 and you will receive the remaining 29,000. However, if you set too little gas, say, for a simple BTM transfer, the gas limit is 20,000. The EVM will cost you 20,000 gas trying to implement the transaction, but it won't complete. The EVM then reverts all changes, but since the miner has done work worth 20k gas, the gas is consumed.


