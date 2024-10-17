---
myst:
  html_meta:
    "description lang=en": |
      Development steps on Universal BCOS.
---

# Development

## Before you start

This guide will help you get started with developing on the UBCOS.

It will guide you through the process of setting up your development environment, creating a new project, and deploying it to the BCOS.

And more，you can also learn how to participate in consensus and governance on the UBCOS.

## Prerequisites

Before you start developing on the UBCOS, you need to have the following prerequisites:

- Basic knowledge of blockchain technology, see more in [Intro to blockchain](../basic/blockchain.md), [Intro to wallet](../basic/wallet.md).
- Understanding advanced concepts of the UBCOS, see more in [](../advance/index.md).
- Learning Solidity smart contract language, see more in [Solidity](./solidity.md) chapter.

## For Web3 developers

If you are new to the UBCOS, you can start with the following steps, which will help you get started with developing on the UBCOS.

### Step 1: Set up your smart contract environment

[Remix](https://remix.ethereum.org) is one of the most famous browser-based IDE (Integrated Development Environment) for developing `Solidity` contracts. It provides a lot of features to help you write, test, and deploy your smart contracts.

For more details: [Connecting Remix to UBCOS](./remix_usage.md)

### Step 2: Connect to the UBCOS

Crypto wallet is the bridge between reality and the blockchain. It allows you to interact with the blockchain, such as sending transactions, deploying smart contracts, and so on.

[MetaMask](https://metamask.io/) is a popular crypto wallet in Web3. And it is also compatible with the UBCOS.

For more details: [Connecting MetaMask to UBCOS](./wallet_usage.md)

### Step 3: Deploy your smart contract

After you have set up your smart contract environment, implemented your smart contract, and connected to the UBCOS, you can deploy your smart contract to the UBCOS.

During Step 2, you have connected to the UBCOS using MetaMask. Now you can deploy your smart contract to the UBCOS using Remix.

Here is another simple example to deploy a smart contract using [Hardhat](https://hardhat.org/), which is a smart-contract development environment. [Deploy a smart contract using Hardhat](./hardhat_usage.md).

After you have deployed your smart contract to the UBCOS, you can check the transaction on the UBCOS explorer. Check the usage of explorer: [UBCOS Explorer](./explorer_usage.md)

### Step 4: Develop your DApp

After you have deployed your smart contract to the UBCOS, you can develop your [DApp](../basic/dapp.md) to interact with the smart contract.

Here is a tutorial of build a first DApp: [Build a first DApp](./dapp_guide.md).

## For nodes maintainers

If you want to build a blockchain instance of UBCOS in your computer or remote server, or run a node of UBCOS, to be a observator, or to participate in consensus and governance, you can start with the following steps.

### Step 1: Build a chain

Follow the [Build a chain](./build_chain.md) guide to build a simple 4-node blockchain.

### Step 2: Run a node

For you to run a node, you can follow the [Run a node](./run_node.md) guide to run a node in your computer or remote server.

- If you want to participate in consensus and governance, you can follow the [Run a consensus node](./run_consensus.md) guide to run a consensus node.
- If you want to be a observer, you can follow the [Run a observer node](./run_observer.md) guide to run a observer node.

More information of node types instructions in [Node types](../advance/nodes.md).

### Step 3: Configuration and management

After you have built a chain and run a node, you can follow the [Configuration](./config.md) guide to configure and manage your blockchain instance.

And you can also follow the [Management of chain](./management.md) guide to manage your node.

## For UBCOS contributors

Thank you for considering making Universal BCOS even better! Your contributions are most welcome and appreciated.

To get started, refer to our [CONTRIBUTING](https://github.com/WeTechHK/Universal-BCOS/blob/i18n/CONTRIBUTING.md) guide for a detailed walk-through of the contribution process.

For any contributors interested in developing new features for UBCOS, your participation is highly welcome. You can refer to this document for compiling the source code: [Compile UBCOS from source code](./compile_from_source.md).

```{toctree}
:maxdepth: 1

solidity
remix_usage
wallet_usage
hardhat_usage
explorer_usage
dapp_guide
build_chain
run_node
config
management
compile_from_source
```
