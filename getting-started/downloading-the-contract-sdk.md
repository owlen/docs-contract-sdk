---
description: >-
  Once you have a working Go environment on your machine, the next step is
  downloading the contract SDK to your local Go workspace.
---

# Downloading the Contract SDK

## Cloning the SDK

Download the SDK to your computer by running the following in terminal

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
~/go/src/github.com/orbs-network/orbs-contract-sdk/go/sdk
```

## Updating the SDK

In order to update the SDK to the latest version, run the same command used to download it initially.

 Notice that the SDK folder in your workspace is actually a git repo. You can also update the SDK by running git pull manually.

