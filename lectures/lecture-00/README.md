# `lecture-0`

Introduction to solidity programming language. Introduction to the Compilation Process onto the blockchain.

Morgan Bergen, B.S. Computer Science - Director of Education [University of Kansas Blockchain Institute](https://kublockchain.com)

![cover](https://user-images.githubusercontent.com/65584733/188204397-74f80efe-7234-424a-ba55-23ce0d5e2b4a.jpeg)

## Learning Objective

By the end of this lecture you will be able to build and deploy your first `simple.sol` program

```
// SPDX-License-Identifier:  GPL-3.0
pragma solidity >= 0.4.16 < 0.9.0;

contract SimpleStorage {

    uint storedData;

    function set(uint x) public {

        storedData = x;

    }

}

```

## What is solidity?

Solidity is an object-oriented, high-level language for implementing smart contracts. Smart contracts are programs which govern the behaviour of accounts within the Ethereum state.
Solidity is a curly-bracket language designed to target the Ethereum Virtual Machine (EVM). It is influenced by C++, Python and JavaScript. You can find more details about which languages Solidity has been inspired by in the language influences section. Solidity is statically typed, supports inheritance, libraries and complex user-defined types among other features. With Solidity you can create contracts for uses such as voting, crowdfunding, blind auctions, and multi-signature wallets. When deploying contracts, you should use the latest released version of Solidity. Apart from exceptional cases, only the latest version receives security fixes. Furthermore, breaking changes as well as new features are introduced regularly. We currently use a 0.y.z version number to indicate this fast pace of change.

#### I. Technical Requirements

This is a programming lecture series, thus most of the work and teaching here will consist of programming and implementing programs on the Ethereum Virtual Machine. Execute the instructions, given in this lecture, will focus on deployment on a macOS machine, however you can use a machine with any operating system (Windows, Linux).

Ethereum-based blockchain programs can be deployed to multiple public networks, test networks, or private networks. The following will be the Ethereum-based tools and utilities that are necessary for building our programs. The following are the required assets you need to set up your development enviroment for building testing, deploying, & interacting with solidity contracts.

In order to derive the most value from this lecture series the following skills are recommended:

1. Experience using the command line tool
2. Basic knowledge regarding Ethereum protocols

In order to get the most value from the tutorials on this page, the following skills are necessary:

1. Experience using the command line
2. Basic knowledge about Ethereum and testnets
3. Basic knowledge about HTTP and JavaScript

**What you will need for this lecture series**:

1.  [Solidity Programming Essentials by Ritesh Modi ](https://oiipdf.com/solidity-programming-essentials-a-beginners-guide-to-build-smart-contracts-for-ethereum-and-blockchain)

2.  [Git Code Repository](https://github.com/PacktPublishing/Solidity-Programming-Essentials-Second-Edition.git)

3.  [Solidity compiler 0.18.13](https://github.com/ethereum/solidity/blob/v0.8.16/docs/installing-solidity.rst)

4.  [web3.js v1.5.3](https://web3js.readthedocs.io/en/v1.7.5/) is a collection of libraries that allow you to interact with a local or remote ethereum node using HTTP, IPC or WebSocket.

5.  [node.js](https://nodejs.org/en/) is an open-source, cross-platform, JavaScript runtime environment.
    CLI install method with homebrew `$ brew install node`

6.  [Ganache v7.0.3](https://github.com/trufflesuite/ganache.git) is a Personal blockchain for Ethereum development CLI install method with homebrew `$ brew install --cask ganache`

7.  [Geth](https://geth.ethereum.org/downloads/) is the Golang implementation of the Ethereum protocol. It is fast, open source software that is actively maintained.

#### II. Overview of Solidity

Solidity is an object-oriented contract-oriented language designed to compile code for the Ethereum Virtual Machine.

#### III. Installing Ethereum & Solidity

The important utilities related to the Ethereum ecosystem will be provided along with Geth, which is one of the main Ethereum implementations.

##### Ethereum Networks

Ethereum is an open source platform for building and deploying dApps (distrubuted/decentralized applications). Ethereum is a P2P (peer-to-peer) network of computers (also known as nodes) all interconnected and used to store data in the distributed data structure (commonly refered to as a ledger). This means that a copy of the ledger is available to each node on the network. There are different types of networks that developers can utilize in order to deploy their dApps. (We will be building our programs on networks that will not actually cost any ether or money.) The three different.

**Types of Ethereum Networks:**

1.  Permissioned
2.  Private
3.  Public

**Main Network**

The main Ethereum network is a global public network that anyone can use. It can be accessed using an account, and anyone can deploy their solutions and smart contacts. Deploying and using this main network incurs a cost in terms of gas. The main netwrok is a public chain that is accesible over the internet and anyone can connect to it and acces both data and transactions stored in it.

**Testnets**

Testnets (known as Test networks) are intended to help with oboarding adoption of Ethereum blockchains and testing facilities on this chain. This network has a different ledger and storage than the main network and is completely free of cost. This is because test ethers can be generated using faucets and used on these networks. There are multiple different test networks,

[**1. Ropsten**](https://ropsten.etherscan.io)

Originally named **Morden** this is the the most widely used test networks that uses PoW (Proof of Work) consensus methods for generating blocks. This network can be used with the `--testnet` option available in Geth. (more on using this network in the following sections)

[**2. Rinkeby**](https://www.rinkeby.io/#stats)

Another Ethereum-based test network that uses PoA (Proof of Authority) consensus methods.

[**3. Kovan Testnet**](https://kovan-testnet.github.io/website/)

Kovan is another PoA (Proof of Authority) publicly accessible network; created and maintained by a consortium of Ethereum developers, this network can only be used by parity clients and therefore will not be utilized or discussed later on.

[**4. Goerli**](https://goerli.net)

Goerli is the last PoA consensus method based test network, this too is a cross client network and will not be utilized or discussed later on.

**Private Network**

A private network is created and hosted on private infrastructure. Private networks are controlled by a single organization, and it has full control over it. There are solutions, contracts, and use cases that an organization might not want to put on a public network, even for test purposes. They may want to use private chains for development, testing, and production environments. Organizations should create and host a private network, and they will have full control over it. Further in this chapter, we will see how to create your own private network.

**Consortium Network**

Lastly a consortium network is a private network but the network comprises of onodes that are managed by different organizations. No organization has total control over the data and chain, however it is shared within an organization and everyone can view and modify it's current state. These networks are accessible through the internet or completely private networks requiring VPNs (Virtual private networks).

https://user-images.githubusercontent.com/65584733/182721343-878654ff-b494-4f3e-8f2a-0463456655b3.mov

### Installing and Configuring Geth

Implementation of Ethereum nodes and clients is available in multiple languages, including Go, C++, Python, JavaScript, Java, and Ruby. The functionality or usability of these clients is the same across languages, and developers should choose the language implementation they are most comfortable with.

Geth is the Go implementation which acts as an Ethereum client to connect to public and test networks, but also used to create the mining and EVM (transaction nodes) for private networks. Geth is a CLI tool written in Go and used for creating a node and miners on a private chain. This lecture will provide how to install Geth on macOS.

## :warning: WARNING USING **`$ Geth`** COMMAND

Just typing `Geth` and executing it will connect Geth to a public main network, and it will start syncing and downloading all of the blocks and transactions from the Ethereum blockchain. Currently the chain has over 5 TeraBytes of data and at the time of writing this it is growing each and everyday. The `help` command shows all of the commands and options with `Geth`.

Geth is based on the JSON-RPC protocol. It defines the specification for remote procedure calls, with payload encoded in the JSON format.Geth allows connectivity to JSON-RPC using the following three different protocols.

**IPC**

Inter-Process Communication: This protocol is used for inter-process communication within the same computer.

**RPC**

Remote Procedure Calls: This protocol is used for inter-process communication across computers. This is generally based on TCP & HTTP protocols.

**WS**

WebSockets:This protocol is used to connect Geth using sockets over HTTPS.

Commands, Switches, and Options for configuring Geth:

1. Configuring the IPC, RPC, WS protocols.
2. Configuring network types to connect - private, Ropsten, and Rinkeby
3. Mining options
4. Console and API
5. Networking
6. Debugging and logging

`$ geth --mainnet`

Geth can be used to connect to a public network, there are multiple different network IDs, the main

![geth--mainnet](https://user-images.githubusercontent.com/65584733/182727608-903f27a5-dbdc-47d2-ac9c-1b82d6b47951.png)

- Ethereum network
- Intsalling and Configuring Geth
- Creating a private network
- Intsalling ganache-cli
- Installing the solidity compiler
- Installing the web3 framework
- Installing and working with MetaMask

#### IV. An Introduction to the simpliest version of a Smart Contract

In this simple contract we will be setting a value of a variable and expose it for other contracts to access.

```console

// machine-readable license specifiers are important in a setting where publishing the source code is the default
// SPDX-License-Identifier:  GPL-3.0-or-later

//pragmas are instructions that are executed by the compiler before the code is compiled and executed.
//this is a preprocessor directive analogous to C++'s #include directive.
pragma solidity >=0.4.16 <0.9.0;

// a contract is a collection of functions and data, analogous to a class in C++.
contract SimpleStorage {
    // private state variables are variables that are only visible within the contract.
    uint256 storedData;

    // public method that defines set in order to modify the storedData variable.
    function set(uint256 x) public {
        storedData = x;
    }

    // public method that defines get in order to return the storedData variable.
    function get() public view returns (uint256) {
        return storedData;
    }
}

/*

This contract does not do much except store a number.
Because of the infrastructure built by Ethereum, anyone can store a single number that is accessible by anyone in the world without a (feasible) way to prevent you from publishing this number.  Anyone could call set aain with a different value adn overwrite your number, however the number is still stored in the history of the blockchain.
Later you will see how you can improse access resturctions os that only you can alter the number.


*/


```

A contract in the sense of Solidity is a collection of code (functions) and data (states) that resides at a specific address on the Ethereum blockchain. Now this contract does not do much except store a number.
Because of the infrastructure built by Ethereum, anyone can store a single number that is accessible by anyone in the world without a (feasible) way to prevent you from publishing this number. Anyone could call set aain with a different value adn overwrite your number, however the number is still stored in the history of the blockchain.
Later you will see how you can improse access resturctions os that only you can alter the number.

#### V. Subcurrency Example

coin.sol

**Pre-processor Directives and Versions**

```
// SPDX-License-Identifier:  GPL-3.0
pragma solidity ^0.8.4;
```

**state variable declaration**

```
contract Coin {

    address public minter;
    ...
}
```

In this line the state variable is of data type **address**

### `Address` Data Type (High Level Overview)

**The address type comes in two forms:**

1. `address`: holds a 20 byte value (size of an Ethereum Address)
2. `address payable`: Is the same address, however it contains the members `transfer` & `send`

`address` is a 160-bit value that does not allow any arithemtic operations, it is intended for storing addresses of contracts (such as `SimpleStorage.storedData` from our `simple.sol` module), or a hash of the public half of a keypair belonging to external accounts.

`address payable` is the address you send Ether to, address payable allows for accepting payments from smart contacts irrespective if that contract was built to accept Ether or not.

### `public`

- `public` is a keyword that automatically/implicitly generates a function that allows you access the current value of the state variable from outside the contracts enviroment.
- The generated function is generated by the compiler is equivalent to the following:
  `function minter() external view returns (address) { return minter; }`
- You do not need to add this function yourself, the comiler will do this for you behind the scenes.

### `Accounts`

**There are two kinds of accounts in Ethereum which share the same address space:**

**External Accounts** are controlled by public-private key pairs.

- The address of the external account is determined from the public key.

**Contract Accounts** are controlled by the code stored together with the account.

- The address of a contract is determined at the time the contract is constructed.
- This is derived from the creator address and the number of transactions sent from that address.
  `minter` contains the creator address value which == 20 byte value
- The number of transactions sent from that address is the `nonce`.
- ∀ account has a persistent key-value store mapping 256-bit word called storage.
- ∀ account has a balance in Ether (in "Wei" to be exact, 1 ether is 10\*\*18 wei) which can be modified by sending transactiosn that include Ether.
