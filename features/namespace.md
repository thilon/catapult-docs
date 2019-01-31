<h2>命名空间</h2>

通过命名空间(Namespace)您可以在NEM区块链上为您的业务和资产创建一个独特的`链接位置`

命名空间以您选择的名称开头，类似于Internet域名。如果一个帐户创建了一个名称空间，那么它将在NEM生态系统中是唯一的。

注册命名空间后，您可以定义自己的子域以及马赛克的名称。

<h2>子命名空间</h2>

在互联网上，域可以具有子域。在NEM中，命名空间可以具有子命名空间。

可以创建多个具有相同名称的子命名空间（例如：`foo.bar`和`foo2.bar`，`bar`是子命名空间/子域）。

命名空间最多可以包含`3`级别，命名空间及其两级子空间域。

<h2>相关文档</h2>

[注册命名空间](https://nemtech.github.io/guides/namespace/registering-a-namespace.html)
[注册子命名空间](https://nemtech.github.io/guides/namespace/registering-a-subnamespace.html)

<h2>Schemas</h2>

!> 配置参数是可编辑的。公共网络配置可能不同

<h2>RegisterNamespaceTransaction</h2>

宣布注册名称空间交易以注册和重新租用命名空间。

**版本号:** 0x02

**实体类型:** 0x414E

**Inlines:**

Transaction or EmbeddedTransaction

|属性|类型|说明|
|:---|:---|:---|
|namespaceType|namespaceType|已注册命名空间的类型|
|duration|uint64|租用期限表示我们要租用命名空间的已确认块的数量。在租赁期间，可以通过发送带有额外确认块的寄存器命名空间交易来扩展租用以租用命名空间。租赁期结束时，命名空间将变为非活动状态。|
|parentId|uint64|如果它是子域，则需要对父命名空间名称的引用。|
|namespaceId|uint64|命名空间的Id。|
|namespaceNameSize|uint8|命名空间名字的长度。|
|name|uint64|如果它是子域，则需要对父命名空间名称的引用。|
|parentId|array(bytes, namespaceNameSize)|命名空间名称必须是唯一的，并且可以具有最大`64`字符长度。允许的字符是a，b，c，...，z，0,1,2，...，9，'，_， - 。|

<h2>NamespaceType</h2>

|ID|说明|
|:---|:---|
|0x00|根命名空间|
|0×01|子命名空间|
