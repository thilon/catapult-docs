## 编写第一个应用

本指南将指导您完成一个NEM开发周期。在组合了一些NEM内置功能后，您将会把第一笔交易发送到区块链。

### 背景

二级票务市场，也称为转售市场，是指个人在从初始供应商处购买票证之后发生的票证交换。最初的供应商可以是活动网站，在线售票平台，商店或活动入口处的摊位。

从不是最初供应商的人那里购买机票并不一定意味着会为机票支付更多费用。也有可能成为购买假货或重复票的受害者，而原始供应商却无法做任何事情来解决这一问题。

**我们想要解决什么**

票务供应商想要建立一个系统：

a. 确定每个购票者。
b. 避免票证转售。
c. 避免使用非正版票证和重复票证。

**我们为什么要使用NEM？**

区块链技术在以下情况下有意义：

* 有不同的参与者参与。
* 这些参与者需要相互信任。
* 需要跟踪一组不可变的事件。

**NEM是一种灵活的区块链**技术。您可以通过API调用使用其经过测试的功能来传输和存储价值，授权，可追溯性和识别，而不是将所有应用程序逻辑上传到区块链中。

其余的代码仍然是链下的。这可以降低固有的不变性风险，因为您可以在必要时更改流程。

### 先决条件

* 完成入门部分
* 文本编辑器或IDE
* NEM2-SDK和CLI
* XEM帐户

### 让我们查阅一些代码
**1. 为每个参与者创建一个帐户**

首先，我们确定参与我们要解决的问题的参与者：
* 售票机。
* 门票买家。

我们已决定将门票供应商和买家代表为单独的帐户。每个帐户都是唯一的，并由地址标识。帐户可以访问区块链中的存款箱，可以使用适当的私钥进行修改。

您是否加载了测试XEM的帐户？如果不是这样，请返回入门部分。您创建的帐户代表门票供应商。

1. 运行以下命令后，您应该在屏幕上看到类似于以下内容的行：

```
$> nem2-cli account info

New Account: SCVG35-ZSPMYP-L2POZQ-JGSVEG-RYOJ3V-BNIU3U-N2E6

[...]

Mosaics

3628d0b327fb1dd8:       1000000
```

2. 此帐户拥有1.000.000XEM。如果马赛克(Mosaics)后面的行是空的，请按照之前的指南说明进行操作。
3. 创建第二个帐户以标识购票者。

```
$> nem2-cli account generate --network MIJIN_TEST --save --url http：// localhost：3000 --profile buyer
```

**2. 监控(Monitoring)区块链**
帐户通过交易更改区块链状态。一旦帐户宣布交易，如果格式正确，服务器将返回OK响应。

接收到OK响应并不意味着交易有效，这意味着它仍未包含在区块中。一个好的做法是在宣布之前监控交易。
我们建议开设三个新终端：
1.第一个终端监控已宣布的交易验证错误。

```
$> nem2-cli monitor status
```

2. 监控'unconfirmed'显示哪些交易已到达网络，但尚未包含在区块中。

```
$> nem2-cli monitor unconfirmed
```

3. 一旦包含交易，您将在'confirmed'终端下看到它。

```
$> nem2-cli monitor confirmed
```

**3. 创建门票**

我们将门票表示为NEM马赛克(Mosaics)。马赛克(Mosaics)可用于表示区块链中的任何资产，例如对象，门票，优惠券，股票，甚至您的加密货币。它们具有可配置的属性，这些属性在创建时定义。例如，我们选择将**transferable属性**设置为false。这意味着购票者只能将门票发回给马赛克的创建者，从而避免门票转售。

在使用门票供应商帐户创建马赛克(Mosaics)之前，您需要注册命名空间(Namespace)。一个命名空间是给出了一个可识别的名称，你的资产在网络中的唯一名称。

1. 注册名为的命名空间`company`。我们来看看这个名字是否可用。

```
$> nem2-cli namespace info --name company
```

2. 命名空间(Namespace)是否可用？通过设置命名空间(Namespace)名称及其租用持续时间来注册它。

```
$> nem2-cli transaction namespace --name foo --rootnamespace --duration 1000
```

您是否检查过监控帐户交易的终端发生了什么？该交易首先出现在`unconfirmed`终端下，并在一段时间后得到确认`confirmed`。

3. 创建一个名为Ticket的马赛克
*它应该在`company`命名空间下，总供应量为100。
*马赛克配置为`transferability`设置为false。
*可分性应设置为0，因为没有人应该能够发送“0.5公司：门票”。

```
$> nem2-cli transaction mosaic --mosaicname ticket  -  namespacename company  -  amount 1000000 --supplymutable --divisibility 0 --duration 1000
```

**4. 发送门票**

将一个`company:ticket`发送到门票供应商帐户，宣布转账类型交易，这是NEM中最常用的操作之一。

1. 准备转账交易。转移交易的三个主要属性：
收件人帐户地址：`SC7A4H-7CYCSH-4CP4XI-ZS4G2G-CDZ7JP-PR5FRG-2VBU`
包含一条消息：`enjoy your ticket`
一个马赛克数组：`[1 company:ticket]`

TypeScript

```TypeScript
import {
    Account, Address, Deadline, UInt64, NetworkType, PlainMessage, TransferTransaction, Mosaic, MosaicId,
    TransactionHttp
} from 'nem2-sdk';

const transferTransaction = TransferTransaction.create(
    Deadline.create(),
    Address.createFromRawAddress('SC7A4H-7CYCSH-4CP4XI-ZS4G2G-CDZ7JP-PR5FRG-2VBU'),
    [new Mosaic(new MosaicId(company:ticket'), UInt64.fromUint(1))],
    PlainMessage.create(‘enjoy your ticket’'),
    NetworkType.MIJIN_TEST
);
```

Java

```Java
import io.nem.sdk.model.account.Address;
import io.nem.sdk.model.blockchain.NetworkType;
import io.nem.sdk.model.mosaic.Mosaic;
import io.nem.sdk.model.mosaic.MosaicId;
import io.nem.sdk.model.transaction.Deadline;
import io.nem.sdk.model.transaction.PlainMessage;
import io.nem.sdk.model.transaction.TransferTransaction;

import java.math.BigInteger;
import java.util.Arrays;

import static java.time.temporal.ChronoUnit.HOURS;

final TransferTransaction transferTransaction = TransferTransaction.create(
    Deadline.create(2, HOURS),
    Address.createFromRawAddress("SC7A4H-7CYCSH-4CP4XI-ZS4G2G-CDZ7JP-PR5FRG-2VBU"),
    Arrays.asList(new Mosaic(new MosaicId("company:ticket"), BigInteger.valueOf(1))),
    PlainMessage.create("enjoy your ticket"),
    NetworkType.MIJIN_TEST
);
```
!> 虽然创建了交易，但尚未向网络公布。

2. 首先在票务供应商帐户中签署交易，以便网络可以验证交易的真实性

TypeScript

```TypeScript
const privateKey = process.env.PRIVATE_KEY;

const account = Account.createFromPrivateKey(privateKey, NetworkType.MIJIN_TEST);

const signedTransaction = account.sign(transferTransaction);
```

Java

```Java
final String privateKey = "";

final Account account = Account.createFromPrivateKey(privateKey,NetworkType.MIJIN_TEST);

final SignedTransaction signedTransaction = account.sign(transferTransaction);
```

3.签名后，将该交易通知给网络。

typescript

```typescript
const transactionHttp = new TransactionHttp('http://localhost:3000');

transactionHttp.announce(signedTransaction).subscribe(
    x => console.log(x),
    err => console.log(err)
);
```

Java

```Java
final TransactionHttp transactionHttp = new TransactionHttp("http://localhost:3000");

transactionHttp.announceTransaction(signedTransaction).toFuture().get();
```

Bash

```Bash
$> nem2-cli transaction transfer --recipient SD5DT3-CH4BLA-BL5HIM-EKP2TA-PUKF4N-Y3L5HR-IR54 --mosaics company:ticket::1 --message enjoy_your_ticket
```

确认交易后，检查门票买方是否已收到门票。

```
$> nem2-cli account info --profile buyer
```
