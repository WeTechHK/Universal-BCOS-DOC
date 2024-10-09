# How to deploy node

This chapter helps users master the Universal BCOS deployment process by deploying a 4-node Universal BCOS private chain on a single machine.

## 1. Install dependencies

### For Apt-based Linux distributions

It is recommended to use Ubuntu 22.04 version or later.

```bash
apt install -y curl openssl wget
```

### For Yum-based Linux distributions

It is recommended to use CentOS7 or later.

```bash
yum install -y curl openssl openssl-devel wget
```

### For macOS

It is recommended to use macOS 15.0 or later.

```bash
# The latest homebrew is downloaded as openssl @ 3 by default, which requires a specified version of openssl @ 1.1
brew install openssl@1.1 curl wget
```

## 2. Download the installation script

```bash
# Create action directory
cd ~ && mkdir -p bcos && cd bcos

# Download the chain building script
curl -#LO https://raw.githubusercontent.com/WeTechHK/Universal-BCOS/refs/heads/i18n/tools/BcosAirBuilder/build_chain.sh && chmod u+x build_chain.sh
```

## 3. Build a 4-node private chain

Run the following command in the `bcos` directory to generate a Universal BCOS chain of 4 nodes:

```bash
bash build_chain.sh -l 127.0.0.1:4 -p 30300,20200
```

Where the -p option specifies the starting port, which is the p2p listening port and the rpc listening port respectively.

After the command succeeds, it will output ‘All completed’:

```bash
[INFO] Generate ca cert successfully!
Processing IP:127.0.0.1 Total:4
writing RSA key
[INFO] Generate ./nodes/127.0.0.1/sdk cert successful!
writing RSA key
[INFO] Generate ./nodes/127.0.0.1/node0/conf cert successful!
writing RSA key
[INFO] Generate ./nodes/127.0.0.1/node1/conf cert successful!
writing RSA key
[INFO] Generate ./nodes/127.0.0.1/node2/conf cert successful!
writing RSA key
[INFO] Generate ./nodes/127.0.0.1/node3/conf cert successful!
[INFO] Admin account: 0x4c7239cfef6d41b7322c1567f082bfc65c69acc5
[INFO] Generate uuid success: 167A2233-5444-4CA4-8792-C8E68130D5FC
[INFO] Generate uuid success: CC117CAF-224C-4940-B548-6DED31D24B18
[INFO] Generate uuid success: 16B5E4BD-51C1-416E-BF44-6D1BB05F7666
[INFO] Generate uuid success: 60DD77F2-F3A5-49F2-8C7F-8151E8823C6D
==============================================================
[INFO] GroupID              : group0
[INFO] ChainID              : chain0
[INFO] bcos path            : bin/universal-bcos
[INFO] Auth mode            : false
[INFO] Start port           : 30300 20200
[INFO] Server IP            : 127.0.0.1:4
[INFO] SM model             : false
[INFO] enable HSM           : false
[INFO] Output dir           : ./nodes
[INFO] All completed. Files in ./nodes
```

## 4. Start the Universal BCOS chain

Start all nodes：

```bash
bash nodes/127.0.0.1/start_all.sh
```

Successful startup will output the following information.Otherwise use `netstat -an|grep tcp` check machine `30300 ~ 30303,20200 ~ 20203` ports are occupied.

```bash
try to start node0
try to start node1
try to start node2
try to start node3
 node3 start successfully pid=36430
 node2 start successfully pid=36427
 node1 start successfully pid=36433
 node0 start successfully pid=36428
```

## 5. Check the node process

- Check if the process is started:

```bash
ps aux |grep -v grep |grep '-bcos'
```

Normally there would be output similar to the following. If the number of processes is not 4, the process is not started (usually caused by the port being occupied)

- View the number of network connections per node. Take node0 for example:

```bash
tail -f nodes/127.0.0.1/node0/log/* |grep -i "heartBeat,connected count"
```

Under normal circumstances, the connection information is output every 10 seconds. From the output log, it can be seen that node0 is connected to the other three nodes, and the network connection is normal:

```bash
info|2022-08-15 19:38:59.270112|[P2PService][Service][METRIC]heartBeat,connected count=3
info|2022-08-15 19:39:09.270210|[P2PService][Service][METRIC]heartBeat,connected count=3
info|2022-08-15 19:39:19.270335|[P2PService][Service][METRIC]heartBeat,connected count=3
info|2022-08-15 19:39:29.270427|[P2PService][Service][METRIC]heartBeat,connected count=3
```