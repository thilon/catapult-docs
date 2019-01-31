<h2>马赛克</h2>

马赛克(Mosaic)是智能资产系统独特和灵活的一部分。它们是NEM区块链上的固定资产，可以表示一组不会发生变化的相同事物。

马赛克可以是一个标记，但它也可以是更专业的资产的集合，如奖励积分，股票，签名，状态标志，投票甚至其他货币。

每个马赛克都有一组可配置的属性。在马赛克创建过程中，您可以定义：

|属性|类型|说明|
|:---|:---|:---|
|Divisibility|Integer|确定马赛克可以分割的小数位。3的可分性意味着马赛克可以分为0.001马赛克的最小部分。可分性必须在0到6的范围内。|
|Duration|Integer|指定租用马赛克的已确认块的数量。|
|Initial supply|Integer|表示马赛克的发行量。初始供应必须在0到9,000,000,000范围内。|
|Supply mutable|Boolean|如果设置为true，则马赛克供应量可能会在以后更改。否则，马赛克供应量是不可改变的。|
|Transferability|Boolean|如果设置为true，则可以在任意帐户之间传输马赛克。否则，马赛克只能转移回马赛克创建者。|

<h2>相关阅读</h2>

[创建马赛克](https://nemtech.github.io/guides/mosaic/creating-a-mosaic.html)

[修改马赛克供应量](https://nemtech.github.io/guides/mosaic/modifying-mosaic-supply.html)

<h2>Schemas</h2>

!> 配置参数是可编辑的。公共网络配置可能不同。

<h2>MosaicDefinitionTransaction</h2>

宣布马赛克定义交易以创建新马赛克。

**版本**：0x02

**实体类型**：0x414D

**inlines**：

Transaction或 EmbeddedTransaction

|属性|类型|说明|
|:---|:---|:---|
|parentId|uint64|命名空间父ID。|
|mosaicId|uint64|马赛克Id。|
|mosaicNameLength|uint8|马赛克名称长度。|
|count|uint8|可选属性中的元素数。|
|flags|MosaicFlag|马赛克旗帜。|
|divisibility|uint8|马赛克的可分性。|
|mosaicName|array(byte, mosaicNameLength)|马赛克名称可以具有最大`64`字符长度。允许的字符是a，b，c，...，z，0,1,2，...，9，'，_， - 。|
|property|array(MosaicProperty, count)|可选的马赛克属性。|

<h2>MosaicSupplyChangeTransaction</h2>

宣布供应变更交易以增加或减少马赛克的供应。

**版本**：0x02

**实体类型**：0x424D

**inlines**：

Transaction或EmbeddedTransaction

|属性|类型|说明|
|:---|:---|:---|
|mosaicId|uint64|受影响的马赛克的id。|
|direction|MosaicSupplyChangeDirection|供应变化方向。|
|delta|uint64|供应量增加或减少。|

<h2>MosaicProperty</h2>

|属性|类型|说明|
|:---|:---|:---|
|ID|uint8|属性id。（0x02）代表持续时间。|
|mosaicId|UINT64|马赛克Id。|

<h2>Mosaic</h2>

|属性|类型|说明|
|:---|:---|:---|
|mosaicId|uint64|马赛克Id。|
|amount|uint64|马赛克数量。|
|property|array(MosaicProperty, count)|可选的马赛克属性。|

<h2>UnresolvedMosaic</h2>

|属性|类型|说明|
|:---|:---|:---|
|mosaicId|uint64|马赛克Id。|
|amount|uint64|马赛克数量。|
|property|array(MosaicProperty, count)|可选的马赛克属性。|

<h2>MosaicFlags</h2>

|id|类型|说明|
|:---|:---|:---|
|0x00|uint8|没有标记|
|0x01|uint8|马赛克供应是可变的|
|0x02|uint8|马赛克是可转移的|
|0x04|uint8|马赛克征税是可变的|

<h2>MosaicSupplyChangeDirection</h2>

|id|类型|说明|
|:---|:---|:---|
|0x00|uint8|增加|
|0x01|uint8|减少|

