# Run a Consensus Node

Consensus nodes are responsible for validating transactions and producing new blocks. Also, consensus nodes do a block-by-block validation of the blockchain, including downloading and verifying the block body and state data for each block.

- Stores full blockchain data (although this is periodically pruned so a full node does not store all state data back to genesis)

- Participates in block validation, verifies all blocks and states.

- Serves the network and provides data on request.

## 1. POTOS Structure Overview

## 2. System Requirements

运行一个POTOS的Consensus节点需要满足以下软硬件要求。

### 2.1 硬件要求

| Specifications | Recommended            | Lowest               |
|----------------|------------------------|----------------------|
| CPU            | 32-cores               | 16 cores             |
| Memory         | 128 GB                 | 32 GB                |
| Storage        | > 4 TB SSD, 4,000 Mbps | > 1 TB SSD, 800 Mbps |
| Network        | 10 Gbps                | 1 Gbps               |

### 2.2 存储要求

POTOS的Consensus节点需要大量的存储空间来存储区块链数据，且会随着时间的推移而增长。假设每个区块的大小为20KB，其中每个区块包含100笔交易，每笔交易的大小为200B。假设POTOS的区块链网络的TPS为100，那么每天的存储增长大致为1.6GB/天（200\*100\*86400）。因此，我们建议您在初始时至少准备4TB的存储空间。

### 2.3 操作系统要求

- (Recommended) AWS Amazon Linux2, or other linux-based environments in mainstream cloud services provider.
- (Recommended) Ubuntu 22.04 LTS in x86_64 or arm64.
- CentOS 7/8 in x86_64 ir arm 64.
- macOS 13.0 or later in x86_64 or arm64.

### 2.4 系统依赖

POTOS Consensus节点在运行时没有特别的依赖，但是在安装时需要以下软件包：

- openssl: version 1.1.1 or later
- curl: latest version
- wget: latest version
- java: version 8 or later

你可以根据你的操作系统的包管理器使用以下命令安装这些软件包：

- YUM Package Manager:

```bash
yum install -y openssl openssl-devel curl wget java java-devel
```

- Apt Package Manager:

```bash
apt install -y openssl curl wget default-jdk
```

- Homebrew Package Manager:

```bash
brew install openssl@1.1 curl wget openjdk@8
```

## 3. Network Configuration

### 3.1 POTOS节点网络监听端口

POTOS Consensus节点在运行时将会涉及到三个端口号：

- `30300`: P2P端口，用于节点之间的通信。
- `20200`: JSON-RPC端口，用于外部应用程序通过UBCOS SDK与节点之间的通信。
- `8545`: Web3 JSON-RPC端口，用于外部应用程序通过以太坊标准JSON RPC与节点之间的通信。

上述端口号在节点的配置文件中可以进行修改。在节点的配置文件`config.ini`中，您可以找到以下配置项：

```ini
[p2p]
    listen_ip=0.0.0.0
    listen_port=30300

[rpc]
    listen_ip=0.0.0.0
    listen_port=20200

[web3_rpc]
    enable=true
    listen_ip=0.0.0.0
    listen_port=8545
```

因此，在您的网络中，您需要确保这些端口号没有被其他应用程序占用。如果您的网络中有防火墙，您需要确保这些端口号已经被放行。

### 3.2 配置节点的网络连接

在POTOS的区块链网络中，节点之间通过P2P协议进行通信。节点需要配置主动连接区块链网络的其中一个节点，你可以从配置文件`nodes.json`找到以下配置项：

```json
{"nodes":["node.eightart.hk:30300"]}
```

### 3.3 为节点申请IP白名单

由于POTOS的P2P网络连接是有IP白名单限制的，因此需要为节点的IP地址申请白名单。您可以通过以下命令查看节点的IP外网地址：

```bash
curl ifconfig.me
```

## 4. Installation

### 4.1 获取POTOS Consensus节点安装包

POTOS Consensus节点在接入POTOS主网是需要准入的，因此您需要联系POTOS的官方团队获取POTOS Consensus节点的安装包。

### 4.2 安装POTOS Consensus节点

在您获取到POTOS Consensus节点安装包以后，您可以通过以下命令解压缩安装包：

```bash
mkdir -p ~/path/to/Consensus
tar -zxvf potos-consensus-3.14.0.tar.gz -C ~/path/to/consensus
```

在解压缩以后，您可以查看解压缩后的文件夹：

```bash
tree potos-consensus-node
./potos-consensus-node
.
├── console             # Console directory
│   ├── apps
│   ├── conf            # Configuration directory
│   ├── contracts       # Contracts demo directory
│   ├── lib
│   └── start.sh        # Start script of console
├── node0               # Node directory
│   ├── conf            # Configuration directory
│   │   ├── ca.crt      # CA Certificate file
│   │   ├── cert.cnf    # Certificate configuration file
│   │   ├── node.nodeid # Node ID file, used to identify the node, which is public key of the node
│   │   ├── node.pem    # Node private key file
│   │   ├── ssl.crt     # SSL certificate file, which issued by CA
│   │   ├── ssl.key     # SSL private key file, which is used to encrypt the communication package
│   │   └── ssl.nodeid  # SSL ID file, which is used to identify in p2p network, and it is the public key of the node
│   ├── config.genesis  # Genesis block configuration file
│   ├── config.ini      # Node configuration file
│   ├── nodes.json      # Node list file
│   ├── start.sh        # Start script
│   └── stop.sh         # Stop script
├── start_all.sh        # Start all nodes script
├── stop_all.sh         # Stop all nodes script
└── universal-bcos      # Universal BCOS binary file
```

### 4.3 启动POTOS Consensus节点

使用以下命令启动POTOS Consensus节点：

```bash
cd ~/path/to/consensus/potos-consensus-node/
bash ./start_all.sh
# Consensus node pid is 9862
 node0 start successfully pid=9862

# Check the process
ps -ef | grep bcos
501 9862     1   0 10:36下午 ttys019   13:33.97 /path/to/observer/observer_node/node0/../universal-bcos -c config.ini -g config.genesis
```

可以通过以下命令查看POTOS Consensus节点的日志，确认节点是否正常启动：

```bash
tail -f node0/log/* | grep Report

# Many logs will be printed, and the following is an example of the log
info|2024-10-15 22:36:31.415281|[CONSENSUS][PBFT][METRIC]^^^^^^^^Report,sealer=2,txs=1,committedIndex=203,consNum=204
```

在节点初次启动时，将会同步区块链数据，这个过程可能会持续几个小时。在同步完成后，您可以通过以下命令查看节点是否完成同步，当`number`和`highestNumber`相等时，表示节点已经完成同步：

```bash
cat node0/log/* | grep -ia "BLOCK SYNC" | grep "commitBlockState success"

# Many logs will be printed, and the following is an example of the log
info|wbbc-occnode|7857|2025-02-11 19:12:52.658698|exec-0x000000016d263000|[BLOCK SYNC][blk-3546][METRIC]commitBlockState success,number=3546,hash=864fb9c9...,executedBlock=3546,commitBlockTimeCost=12,node=fe63028d...,txsSize=1,highestNumber=3546,sealer=1
```

### 4.4 将新节点加入到POTOS共识

在您的POTOS Consensus节点启动并且已经完成同步后，您可以将新节点加入到POTOS共识网络中。您可以通过以下命令查看新节点的node ID：

```bash
cat node0/conf/node.nodeid

72750a8ea22face974a28dbcf1bda95e6a8a3c9ab78826a25b619c24016927a97236fb456dde70cc38c308f583cdbe547a73f781b371fb995aa3b019fa82ec70
```

然后可以将新节点的node ID提供给POTOS共识网络的管理员，由管理员将新节点加入到共识网络中。

### 4.5 与POTOS Consensus节点交互

POTOS Consensus节点提供了Web3 JSON-RPC接口，您可以使用Web3工具通过Web3 JSON-RPC接口与POTOS Consensus节点进行交互。

- [Connecting MetaMask to UBCOS](https://universal-bcos.readthedocs.io/en/latest/develop/wallet_usage.html)
- [Connecting Remix to UBCOS](https://universal-bcos.readthedocs.io/en/latest/develop/remix_usage.html)
- [Deploy smart contract using Hardhat](https://universal-bcos.readthedocs.io/en/latest/develop/hardhat_usage.html)

### 4.6 停止POTOS Consensus节点

使用以下命令停止POTOS Consensus节点：

```bash
cd ~/path/to/consensus/potos-consensus-node/
bash ./stop_all.sh
```

## 5. Configuration

UBCOS configuration encompasses both on-chain and off-chain settings.

On-chain configuration requires administrators to send transactions to the chain, where all consensus nodes reach an agreement, unifying the network’s configuration.

Off-chain configuration refers to individual node configuration options that can be modified by operators without sending transactions by simply updating the configuration files.

For more detail, see [UBCOS Configuration Guide](https://universal-bcos.readthedocs.io/en/latest/develop/config.html)
