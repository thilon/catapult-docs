## 配置开发环境

本段将引导您逐步安装所需要的工具，以便开始在NEM投石车(Catapult)上进行开发。

### 运行投石车(Catapult)服务引导程序(Bootstrap)

**Catapult Server节点**（第1层）构建对等的区块链网络。**Catapult Rest节点**（第2层）提供应用程序可用于访问区块链及其功能的API网关。

您将使用Catapult Service Bootstrap运行私人链以进行学习。此服务在本地运行Catapult服务器实例和Catapult REST节点。

1. 在运行以下命令之前，请确保已安装docker和docker-compose：
> $> git clone https://github.com/tech-bureau/catapult-service-bootstrap.git --branch v0.1.0
$> cd catapult-service-bootstrap
$> docker-compose up


