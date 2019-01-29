### 区块

每个加密货币的核心要素是一个被称为区块链的公共分类账本，账本将区块连接在一起。
由于链中的区块是有序的，因此完整的交易历史记录保存在区块链中。区块链中的后续区块的一直增加，高度与前一个相差一。
区块作为永久介质存储在数据库中。NEM将链中的第一个区块叫做复仇女神之块。
NEM出块时间在15秒，使交易确认足够快，以便日常使用

!> 配置参数是可编辑的。公共网络配置可能不同。
 
 ### 区块创建
 
 区块由帐户创建。创建新区块的过程称为收获。收获账户称为收获者，并获得区块中交易的手续费。这使收获者有动力将尽可能多的交易添加到区块中。
 
 ### 指南
 
 * 监听新的区块 </br>
 当新的区块被创建时,收到通知
 
 * 获取区块的高度 </br>
 给定一个高度，获取区块的信息
 
 
 ### 结构描述(Schemas)
 
 ### 区块头部
 
 **inlines**
 * VerifiableEntity
 * EntityBody
 
|属性|类型|说明|
|:---|:---|:---|
|height|uint64|区块的高度。每个区块都有不同的高度，后面的区块跟前面的区块相差1|
|timestamp|uint64|自第一个区块创建以来经过的秒数|
|difficulty|uint64|区块难度值|
|previousBlockHash|32 bytes(binary)|前一个区块的hash值|
|blockTransactionHash|32 bytes(binary)|该区块中的所有交易形成了一个Merkle树。树根的Hash值|
|stateHash|32 bytes (binary)|每一个区块的状态(state)存储在RocksDB数据库中，形成一个Patricia树，值为树根的hash值|

**Verison**:字节高位表示网络类型

|Id|说明|
|:---|:---|
|0x68 (MAIN_NET)|公有链|
|0x98 (TEST_NET)|公有测试链|
|0x60 (MIJIN)|私有链|
|0x90 (MIJIN_TEST)|私有测试链|

**Type**：区块类型

|Id|说明|
|:---|:---|
|0x8043|复仇女神之块(创世块)|
|0x8143|区块|

### VerifiableEntity

|属性|类型|说明|
|:---|:---|:---|
|signature|64 bytes(binary)|签名者生成的实体签名|

### EntityBody

|属性|类型|说明|
|:---|:---|:---|
|signer|32 bytes (binary)|签名者的公匙|
|version|uint16|结构体的版本|
|type|uint16|实体类型。对于交易类型。查看交易类型|
