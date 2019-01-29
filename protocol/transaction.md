### 交易

交易是对区块链采取的改变其状态的行动。当帐户签署交易并且网络接受该交易时，该帐户将永久存储在块上。
交易有不同的类型。例如，您可以在帐户之间传输马赛克，传输或配置帐户的所有权（包括使用多重签名(multisig)规则）等。

**Mosaic Transactions**

|Id|类型|说明|
|:---|:---|:---|
|0x414D|Mosaic Definition Transaction|注册一个新的马赛克|
|0x424D|Mosaic Supply Change Transaction|改变一个先有的马赛克供应量|
|publicKey|String|返回新创建账户的公匙|

**Namespace Transactions**

|Id|类型|说明|
|:---|:---|:---|
|0x414E|Register Namespace Transaction|注册一个命名空间，以便管理你的资产|

**Transfer**

|Id|类型|说明|
|:---|:---|:---|
|0x4154|Transfer Transaction|在两个账号之间发送马赛克和消息|

**Multisignature Transactions**

|Id|类型|说明|
|:---|:---|:---|
|0x4155|Modify Multisig Account Transaction|创建或修改一个多重签名合约|
|0x4141|Aggregate Complete Transaction|将批量交易发送到不同的账户|
|0x4241|Aggregate Bonded Transaction|在不同账户之间发起多个交易|
|0x4148|Hash Lock Transaction|Deposit to announce aggregate bonded transactions. Prevents the network spamming.|
|-|Cosignature Transaction|Cosign an aggregate bonded transaction.|

**Account Filters**

|Id|类型|说明|
|:---|:---|:---|
|0x4150|Account Properties Address Transaction|允许或阻止给定地址集的转入交易|
|0x4250|Account Properties Mosaic Transaction|允许或阻止转入交易中包含给定的马赛克|
|0x4350|Cosignature Transaction|按照交易类型来允许或阻止交易|

**Cross-chain swaps Transactions**

|Id|类型|说明|
|:---|:---|:---|
|0x4152|Secret Lock Transaction|在不同的链之间开始马赛克交换|
|0x4252|Secret Proof Transaction|结束不同链之间的马赛克交换|

### 定义一个交易

每笔交易都有一些共同的属性。每个交易都从交易模板定义扩展，添加了类型的特定属性。
交易以序列化形式定义。我们建议使用NEM2-SDK来定义交易。

### 签署一个交易
帐户必须在将交易通知网络之前对其进行签名。签署交易表示帐户同意更改所定义的网络状态。
例如，转移交易描述了谁是收件人以及要转移的马赛克数量。在这种情况下，签署交易意味着接受将这些马赛克从一个帐户移动到另一个帐户。
该帐户使用其私钥生成已签名交易的前100个字节的签名。然后，签名将附加到交易的正文，从而产生签过名的交易。
一旦将Sha3-256算法应用于序列化交易，就会生成交易的Hash值。

### 宣布交易

已签署的交易已准备好向网络公布。

在宣布交易之后，REST API将始终立即返回OK响应。此时，仍然不知道交易是否有效。
第一次验证发生在API节点中。如果交易出现一些错误，WebSocket将通过状态通道发出通知。在肯定的情况下，交易以未确认的状态到达P2P网络。永远不要依赖具有未经证实状态的交易。目前尚不清楚它是否会被包含在一个块中，因为它应该在之前通过第二次验证。
第二次验证在将交易添加到收获块中之前完成。如果有效，则收集器将交易存储在块中，并且它达到确认状态。
继续前面的示例，交易得到处理，并且所述金额从签名者的帐户转移到收件人的帐户。此外，交易费用从签名者的账户中扣除。
此时交易的确认数为零。当另一个块添加到区块链时，该交易有一个确认。添加到链中的下一个块将给出两个确认，依此类推。

### 回滚

加密货币可以回滚部分区块链。回滚对于解决区块链的分叉至关重要。
“重写限制”是可以回滚的最大块数。因此，分叉也只能被解析到一定的深度。
NEM具有360块的重写限制。一旦交易超过360次确认，就无法撤消。
在现实生活中，除非由于代码中的错误或攻击导致区块链出现严重问题，否则不会发生超过20个区块的分叉。
