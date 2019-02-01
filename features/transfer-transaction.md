<h1>Transfer Transaction</h1>

`Transfer transactions`被用于在两个账户之间传递马赛克(mosaics),并且可携带一条长度为`1023`的消息。

![](../images/transfer-transaction.png)

!> 即使地址之前没有参与任何交易，也可以将马赛克发送到任何有效地址。如果没有人拥有收件人帐户的私钥，那么资金很可能永远丢失。

<h2>相关文档</h2>

<h2>Schemas</h2>

!> 配置参数是可编辑的。公共网络配置可能不同。

<h2>TransferTransaction</h2>

宣布在两个帐户之间发送马赛克或消息

**版本**：0x03

**实体类型**：0x4154

**inlines**：

Transaction或EmbeddedTransaction

|属性|类型|说明|
|:---|:---|:---|
|recipient|25 bytes (binary)|收款帐户的地址|
|messageSize|uint16|附加消息的大小|
|mosaicsCount|uint8|附加马赛克的数量|
|message|array(byte, messageSize)|消息类型（0）和最多为`1023`字节的有效负载。|
|mosaics|array(UnresolvedMosaic, mosaicsCount)|要发送的不同的马赛克。|
