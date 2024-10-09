# Connecting Remix to UBCOS

Remix is a browser-based IDE (Integrated Development Environment) for developing Solidity contracts. In this guide, you will learn how to:

* Create and Upload a pre-built smart contract on Remix IDE.
* Compile the smart contract.
* Set up deployment environment
* Import account
* Connect Kaia to Remix using MetaMask
* Deploy the smart contract.
* Verify the smart contract.

This will cover connecting Remix with UBCOS. If you want to know more about how to use Remix, please refer to [Remix docs](https://remix-ide.readthedocs.io/en/latest/) or [Remix IDE](https://remix.ethereum.org/).

## Creating a file on Remix

To start building a smart contract, click on **New File** icon in the **contracts** folder in the **File explorer** tab and name it `MyToken.sol`

Next is to copy and paste the smart contract code provided below into the newly created MyToken.sol file.

```sol
// SPDX-License-Identifier: Apache 2.0
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Permit.sol";

contract MyToken is ERC20, ERC20Permit {
    constructor() ERC20("MyToken", "MTK") ERC20Permit("MyToken") {}

    function mint(uint256 value) public {
        _mint(msg.sender, value);
    }
}
```

![](./remix-create-new-file.png)

## Compile smart contract

To compile your contract, do the following:

* Go to the **Solidity Compiler** tab
* Select compiler version to 0.8.27
* Turn on the 'Auto compile' option.
* Cliick on the Compile MyToken.sol  button to compile `MyToken.sol` contract.
* After successful compilation, it will show a green tick mark on the Compiler tab button

![](./remix-compile-contract.png)

## Setting up deployment environment

* Select the appropriate [Environment].
* You can select Injected Provider - MetaMask

![](./remix-deploy-env.png)

## Import account in Metamask

You can use Metamask create new account or import exist account. [More about account in Metamask](./wallet_usage.md)

* When you see the MetaMask pop-up, select the account by clicking it.
* Once you are successfully connected to the Network, you will see the Chain ID and Account of the connected network.

## Deploying the smart contract

In this section, we will deploy the MyToken.sol contract using Kaia Wallet. Having compiled the contract in the Compile Section, follow the deployment process below:

* Set your deployment ENVIRONMENT to `Injected Provider -  Metamask`.
* Select the contract you want to deploy in the CONTRACT field.
* Click on the Deploy button. This would generate a Kaia Wallet popup that requires transaction confirmation. Simply confirm the transaction!

![](./remix-deploy-contract.png)
