---
description: >-
  You are encouraged to look at the Contract SDK itself, although that is not
  required in order to build contracts on the Orbs Network.
---

# Downloading the Contract SDK

Every feature of the SDK is documented at the [Orbs Contract](../orbs-contracts/smart-contracts.md) chapter of the Contract SDK documentation. The Contract SDK is also published as a Go Module to ease usage when developing a contract. \([what are Go Modules](https://blog.golang.org/using-go-modules) - from the golang blog\)

Having that said, the [examples in the Contract SDK](https://github.com/orbs-network/orbs-contract-sdk/tree/master/go/examples) project can be useful in order to assist with getting started on creating more complex contracts.

## Cloning the SDK

Download the SDK to your computer by running the following in a terminal

```
go get -u github.com/orbs-network/orbs-contract-sdk/...
```

It is recommended to avoid cloning the repo manually with git because the SDK has to be placed in the appropriate path within your Go workspace. The SDK also includes a few git submodules which may be a little tricky to clone recursively.

## Quick tour of the SDK contents

The SDK will download to your Go workspace, typically at

```text
~/go/src/github.com/orbs-network/orbs-contract-sdk
```

The first place to explore in the SDK is the contract examples found at

```text
~/go/src/github.com/orbs-network/orbs-contract-sdk/go/examples
```

Every example contains a README explaining the nature of the contract and how to test it. The automated tests include both a unit test and an end-to-end test running on Gamma server.

The API of the SDK is found at

```text
~/go/src/github.com/orbs-network/orbs-contract-sdk/go/sdk/v1
```

## Updating the SDK

In order to update the SDK to the latest version, run the same command used to download it initially.

Notice that the SDK folder in your workspace is actually a git repo. You can also update the SDK by running git pull manually.

