# State

Part of the smart contract infrastructure that Orbs support requires not only code, which is the written functions in the contract, but also the **state**, which is the data that the contract stores.

This state \(data\) is isolated per contract, meaning each contract can only access its own data, and the state is never shared between contracts. If the contract owner wants to share its state, the way to do this is by using an exported method.

Orbs contracts behave in accordance with statically typed languages, specifically with Go. You may refer to the [Data types](https://orbs.gitbook.io/contract-sdk/~/edit/drafts/-LVnlbSBlfPGStLbU5Xx/orbs-contracts/data-types) page for details on supported types that can be used and stored to or read from the state

The state in Orbs can be referred to as a map or dictionary. The API is in the form of:

```text
state.write(key, value)
value = state.read(key)
```

To use the state in your contract, you must add the following import line to your contract code:

```go
import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/state"
)
```

### Scope

The state is 'storing' data in the contract's scope, meaning that the data stored is available only for the contract it was stored at, and can be only read by that contract

### Writing to state

The following write actions are available to use:

```go
state.WriteBytes(key, value)
state.WriteString(key, value)
state.WriteUint32(key, value)
state.WriteUint64(key, value)
```

Each function accepts value with the given type and stores it to the state at the given key.

The **key** is binary as well, an array of bytes.

### Reading from the state

The following read actions are available to use:

```go
state.ReadBytes(key)
state.ReadString(key)
state.ReadUint32(key)
state.ReadUint64(key)
```

Each function accepts the key of the value you want to read and returns the typed value from the contract state.

Reading a value that was never set returns the zero value of its type.

### Removing data

It is also possible to remove data from the state using the `Clear` function:

```go
state.Clear(key)
```

Clear does not return any value.
