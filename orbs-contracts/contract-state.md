# State

Part of the smart contract infrastructure that Orbs support requires not only code, which are the written functions in the contract, but also the **state** which is the data that the contract stores.

This state \(data\) is isolated per contract, meaning each contract can only access its own data and the state is never shared between contracts - if the contract owner wants to share its state, the way to do this is using an exported method.

Orbs contracts will always behave with accordance to statically typed languages, specifically with Go, you may refer to the [Data types](https://orbs.gitbook.io/contract-sdk/~/edit/drafts/-LVnlbSBlfPGStLbU5Xx/orbs-contracts/data-types) page for details on supported types that can be used and stored to or  read from the state

The state in Orbs can be referred to a map or dictionary, the api will always be in the form of:

```text
state.write(key, value)
value = state.read(key)
```

In order to use the state in your contract, you must add the following import line to your contract code:

```go
import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/state"
)
```

### Scope

The state is 'storing' data in a contract scope, meaning that the data stored is available only for the contract it was stored at, and can be read only by that contract

### Writing to state

The following write actions are available to use:

```go
state.WriteBytes(key, value)
state.WriteString(key, value)
state.WriteUint32(key, value)
state.WriteUint64(key, value)
```

Each function will accept value with the given type and store it to the state at the given key

The **key** will always be binary as well, an array of bytes

### Reading from the state

The following read actions are available to use:

```go
state.ReadBytes(key)
state.ReadString(key)
state.ReadUint32(key)
state.ReadUint64(key)
```

Each function will accept the key of the value you need to read, and return the typed value from the contract state.

Reading a value that was never set will return the zero value of its type.

### Removing data

It is also possible to remove data from the state using the `Clear` function:

```go
state.Clear(key)
```

Clear does not return any value.

