---
description: >-
  Introduction to smart contracts in general and contracts inside Orbs
  specifically.
---

# About smart contracts

## What is a smart contract

Smart contracts are the cornerstone of decentralized systems. When a developer is building a decentralized app, they will find themselves implementing one or more smart contracts, and ultimately deploying them to run over a blockchain infrastructure like Orbs.

The two main services provided by a blockchain infrastructure in this regard are _compute under consensus_ - where multiple nodes execute the contract code and reach consensus over the execution results; and _storage under consensus_ - where the executed code can store state variables persistently.

Compared to centralized cloud platforms, contracts are very similar to serverless compute services such as [AWS Lambda](https://aws.amazon.com/lambda/). Developers deploy code to run directly over the cloud infrastructure and then build clients that make API calls to these services.

## Programming languages for contracts

The first popularized smart contract programming language is [Solidity](https://en.wikipedia.org/wiki/Solidity), which was developed as part of the [Ethereum](https://www.ethereum.org/) project.

Solidity was a brand new language that was designed from scratch for this purpose. This design choice came with benefits - such as the ability to support fine grained execution fees with [gas](https://ethereum.stackexchange.com/questions/3/what-is-meant-by-the-term-gas), and drawbacks - such as an immature toolchain and third party library ecosystem.

The new age of smart contract development is turning towards established programming languages that have already reached industry maturity.

## Programming contracts in Go

Smart contracts in Orbs are developed using the [Go](https://en.wikipedia.org/wiki/Go_%28programming_language%29) programming language.

Go is a low-level open source language developed by Google for extreme performance. It is very popular in the blockchain space and was used to implement the node core of popular blockchains like Ethereum and Hyperledger. It rivals the performance of C++ but is substantially simpler and easier to learn.

Go is also a mature language, with millions upon millions of lines of code used in production for the last 10 years. Go comes with a powerful toolchain, multiple IDEs and a rich ecosystem of third party libraries.

To ensure the secure and deterministic execution of Orbs smart contract, there are several limitations set on what features you can use of the Go language when building contracts. They are [described here](../orbs-contracts/limitations-of-orbs-contracts.md) but it is recommended to go over them only after you familiarize yourself with Go.

