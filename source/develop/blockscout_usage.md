# 使用Blockscout连接UBCOS

[Blockscout](https://github.com/blockscout/blockscout)是一个开源的区块链浏览器，用于查看区块链的交易和区块信息。在本文中，我们将介绍如何使用Blockscout连接到UBCOS。

为了Blockscout能够连接到UBCOS，我们对Blockscout进行了二次开发。代码链接：https://github.com/kyonRay/blockscout/tree/feature-ubcos

## 步骤1：开启UBCOS的Web3 JSON RPC配置

在UBCOS中，您需要开启Web3 JSON RPC配置，以便Metamask、Hardhat以及Blockscout等的Web3工具能够连接到UBCOS。您可以在UBCOS的配置文件中`config.ini`设置Web3 JSON RPC的IP端口。例如：

```ini
[web3_rpc]
    enable=true
    listen_ip=0.0.0.0
    listen_port=8545
    thread_count=16
```

在配置文件中，您需要设置`enable`为`true`，并设置`listen_ip`和`listen_port`为您的IP地址和端口号，端口号默认为`8545`。然后重启UBCOS，使配置生效。

在创世块中，配置了Web3 `chain_id`字段，该字段将用于Web3工具辨认链的标识，必须在启动初始化时确定。其默认值为`20200`。

```ini
[web3]
    chain_id=20200
```

旧节点升级到新版本时，想要开启Web3的功能时，可以参考链接进行配置：[旧节点升级并开启Web3配置](https://fisco-bcos-doc.readthedocs.io/zh-cn/latest/docs/develop/web3_usage.html#id1)

## 步骤2：下载Blockscout

```bash
git clone https://github.com/kyonRay/blockscout -b feature-ubcos
```

## 步骤3：启动Blockscout

若你的UBCOS区块链网络是在本地搭建的，且配置均为默认值，你可以使用docker-compose一键启动Blockscout。

```bash
cd ./docker-compose
docker-compose up --build
```

在经过一段时间的构建后，您可以在浏览器中输入`http://localhost`访问Blockscout的Web界面。

## 配置Blockscout

若你的UBCOS区块链网络不是在本地的，或者配置不是默认值，您需要修改Blockscout的`docker-compose.yml`配置文件，设置UBCOS的Web3 JSON RPC的IP地址和端口号。

```yml
    environment:
    # 对下面的配置进行正确的设置
        ETHEREUM_JSONRPC_HTTP_URL: http://host.docker.internal:8545/
        ETHEREUM_JSONRPC_TRACE_URL: http://host.docker.internal:8545/
        #ETHEREUM_JSONRPC_WS_URL: 
        CHAIN_ID: '20200'
```

若你想更深度配置Blockscout，可以参考Blockscout的[官方文档系统参数](https://docs.blockscout.com/setup/env-variables)。
