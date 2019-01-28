## 配置开发环境

本段将引导您逐步安装所需要的工具，以便开始在NEM投石车(Catapult)上进行开发。

### 运行投石车(Catapult)服务引导程序(Bootstrap)

**Catapult Server节点**（第1层）构建对等的区块链网络。**Catapult Rest节点**（第2层）提供应用程序可用于访问区块链及其功能的API网关。

您将使用Catapult Service Bootstrap运行私人链以进行学习。此服务在本地运行Catapult服务器实例和Catapult REST节点。

1. 在运行以下命令之前，请确保已安装docker和docker-compose：

``` 
$> git clone https://github.com/tech-bureau/catapult-service-bootstrap.git --branch v0.1.0
$> cd catapult-service-bootstrap  
$> docker-compose up
```

!> 如果投石车服务引导程序无法工作，请查看catapult-service-bootstrap-known-issues

1. 检查是否能获得第一个块信息：

```
$> curl localhost：3000 / block / 1
```

### 创建测试账户

帐户(Account)是与存储在NEM区块链中的可变状态相关联的密钥对（私钥和公钥）。换句话说，在区块链上有一个“存款箱”，只有使用密钥对才能进行修改。顾名思义，私钥必须始终保密。有权访问私钥的任何人最终都可以控制该帐户。

该公钥来自私钥。这需要数百万年才能完成相反的过程，因此公钥可以安全地共享。
最后，使用公钥生成帐户地址，遵循NEM区块链协议。共享此地址而不是公钥，因为它包含更多信息，例如有效性检查或它使用的网络（公共，testnet或私有）。
NEM2-CLI方便地允许您执行终端中最常用的命令，即使用它与区块链交互，设置账户，发送资金等。
