<h2>账户</h2>

一个帐户(Account)是与存储在NEM区块链上的可变状态相关联的密钥对（私钥和公钥）。换句话说，区块链中有一个"保险柜"，只有您可以使用密钥对进行修改。顾名思义，私钥必须始终保密。有权访问私钥的任何人最终都可以控制该帐户。

将NEM帐户视为区块链中资产的容器。与大多数区块链一样，账户可以代表代币存款。但是，它也可以表示一个必须唯一且可更新的单个对象：要装运的包裹，房屋的契约或要公证的文件。

账户具有如下属性：

> **私匙(Private Key)** </br>
一个私钥是一个帐户的钥匙。拥有帐户私钥的任何人都可以发起任何与帐户相关的操作。

!> 私钥必须不惜一切代价保密。确保您的私钥在离线地方被安全备份。

> **公钥(Public Key)** </br>
公钥可以用来验证帐户的签名。公钥与第一个发布的交易一起存储在区块链中。未发布任何交易的帐户，其公钥字段为空。

> **地址(Address)** </br>
每个帐户都有一个唯一的地址。您通常会共享衍生的地址，因为它更短并聚了更多的信息。

> **马赛克(Mosaics)** </br>
帐户拥有的不同马赛克的数量。

> **过滤器(Filters)** </br>
帐户可以配置一组智能规则，以阻止在给定一系列约束的情况下通知或接收交易。

<h2>多重签名账户</h2>

当使用特殊规则（直接在NEM区块链上）配置时，帐户变得非常智能，这些规则定义了它们之间的关联和控制方式，以及如何更新和传输其内容。一种重要的规则是多重签名(multisig)控制，允许在多方之间以各种方式共享基于帐户的资产的所有权。
