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

2. 检查是否能获得第一个块信息：

```
$> curl localhost:3000/block/1
```

### 创建测试账户

帐户(Account)是与存储在NEM区块链中的可变状态相关联的密钥对（私钥和公钥）。换句话说，在区块链上有一个“存款箱”，只有使用密钥对才能进行修改。顾名思义，私钥必须始终保密。有权访问私钥的任何人最终都可以控制该帐户。

该公钥来自私钥。这需要数百万年才能完成相反的过程，因此公钥可以安全地共享。

最后，使用公钥生成帐户地址，遵循NEM区块链协议。共享此地址而不是公钥，因为它包含更多信息，例如有效性检查或它使用的网络（公共，testnet或私有）。

NEM2-CLI方便地允许您执行终端中最常用的命令，即使用它与区块链交互，设置账户，发送资金等。

1. 使用npm安装NEM2-CLI:

```
$> sudo npm install --global nem2-cli
```

2. 使用命令行工具创建帐户:

```
$> nem2-cli account generate --network MIJIN_TEST --save --url http://localhost:3000
```

该设置为MIJIN_TEST。测试网络是用于开发和测试目的的替代NEM区块链。'network flag'

用于在您的计算机上存储该帐户。NEM2-CLI使用存储的帐户对您启动的事务进行签名。'save flag'

3.您应该能够在终端中看到包含帐户凭据的以下行：

> 新账户：SCVG35-ZSPMYP-L2POZQ-JGSVEG-RYOJ3V-BNIU3U-N2E6
> 公钥：33E0 ... 6ED
> 私钥：0168 ... 595

### 什么是XEM以及如何获得它？

NEM网络的基础加密货币称为XEM。NEM区块链上的每个操作都需要XEM，以便为验证和保护网络的人提供激励。

我们使用已经拥有XEM的帐户。我们需要它来注册命名空间和马赛克。

1. 打开终端，然后转到下载Catapult Bootstrap Service的目录。
```
$> cd   build/generated-addresses/ 
$> cat addresses.yaml
```

2. 在该部分下nemesis_addresses，您将找到包含XEM的密钥对。
3. 在NEM2-CLI中将第一个帐户作为配置文件加载。

```
$> nem2-cli profile create 

Introduce network type (MIJIN_TEST, MIJIN, MAIN_NET, TEST_NET): MIJIN_TEST
Introduce your private key: 41************************************************************FF
Introduce NEM 2 Node URL. (Example: http://localhost:3000): http://localhost:3000
Insert profile name (blank means default and it could overwrite the previous profile):
```

### 设置开发环境
是时候选择编程语言了。选择您最满意的那个，或者按照您的项目要求。

为新项目创建一个文件夹，然后运行所选语言的命令。

### TypeScript和JavaScript

1. Create a ‘package.json’ file. The minimum required Node.js version is 8.9.X.

```
$> npm init
```

2. 安装nem2-sdk和rxjs library.

```
$> npm install nem2-sdk rxjs
```

3. nem2-sdk是用TypeScript构建。在构建NEM区块链应用时，推荐用TypeScript替代JavaScript。

确认TypeScript版本号最低为2.5.x

```
$> sudo npm install --global typescript
$> typescript --version
```

4.使用ts-node用node执行TypeScript文件。

```
$> sudo npm install --global ts-node
```

如果要直接使用javascript，可以执行节点来运行js文件。

### JAVA
打开一个新的Java gradle项目。最低JDK版本是JDK8。

1. 使用您喜欢的IDE或从命令行创建项目

```
gradle init --type java-application
```

2. 编辑'build.gradle'以使用Maven central repository

```
repositories {
    mavenCentral()
}
```

3. 添加nem2-sdk和reactive library作为dependency

```
dependencies {
    compile "io.nem:sdk:0.9.1"
    compile "io.reactivex.rxjava2:rxjava:2.1.7"
}
```

4. 执行‘gradle build’和‘gradle run’运行你的程序。

### C#

1. 使用C＃IDE创建一个新项目。如果是Visual Studio，请使用程序包管理器控制台安装nem2-sdk。

2. 打开菜单命令。‘Tools > NuGet Package Manager > Package Manager Console’。

3. 在终端中输入nem2-sdk和反应库包名称

```
$> Install-Package nem2-sdk 
$> Install-Package System.Reactive
```

你在使用其他IDE吗？在这种情况下，请查看安装NuGet包的不同方法(https://docs.microsoft.com/en-us/nuget/consume-packages/ways-to-install-a-package)
