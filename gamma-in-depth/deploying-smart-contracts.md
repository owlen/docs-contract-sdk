# Deploying smart contracts

## Using Gamma CLI

To deploy a smart contract run the command `gamma-cli deploy` and provide the contract name. You will also need to provide the source code for the contract.

For example, to deploy a contract named **MyToken**

```text
gamma-cli deploy -name MyToken -code contract.go -signer user1
```

### Command parameters

* `-name` Name of the contract on the blockchain \(used by future transaction senders\)
* `-code` Path of the file containing the source code implementation of the contract
* `-signer` Account ID of the signer of the deploy transaction \(from `orbs-test-keys.json`\)

## Caveats

Contracts are immutable. If you want to update the code for a contract, deploy it again under a different name.

Remember that Gamma server is an in-memory blockchain. When you stop the server with `gamma-cli stop-local` all contracts will disappear.

Contracts are currently limited to a single source file. If you have multiple files, combine them into one.

