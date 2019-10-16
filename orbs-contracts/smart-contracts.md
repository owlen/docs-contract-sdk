# Smart contracts

Smart contracts are the cornerstone of decentralized systems. When developers are building a decentralized app, they are implementing
one or more smart contracts, and ultimately deploying them to run over a blockchain infrastructure like Orbs.


### Orbs smart contracts

The Orbs smart contracts are the logic of your apps: the high level workflow is creating the contracts \(code\) using the Orbs Contract SDK, testing it and experimenting with the Gamma framework, and later deploying your contract to the Orbs blockchain.

Currently, the contracts can be written in the Golang language. In the future the Orbs contract SDK will be available in other languages as well.

Similar to other Smart Contract frameworks, an Orbs contract is comprised of the written code \(functions\) and data \(state\) that resides inside of the blockchain. 

Here is an example of a straightforward contract that implements a counter. It has two main functions, `get` and `add`, and it stores a single state value called `counter`.  


{% code-tabs %}
{% code-tabs-item title="counter.go" %}
```go
package main

import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1"
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/state"
)

var PUBLIC = sdk.Export(add, get)
var SYSTEM = sdk.Export(_init)

var COUNTER_KEY = []byte("count")

func _init() {
	state.WriteUint64(COUNTER_KEY, 0)
}

func add(amount uint64) {
	count := state.ReadUint64(COUNTER_KEY)
	count += amount
	state.WriteUint64(COUNTER_KEY, count)
}

func get() uint64 {
	return state.ReadUint64(COUNTER_KEY)
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}


### Storage and State

The line `state.WriteUint64([]byte("count"), 0)` will use the `state` library to write to the state. The state library is the only way to interact with the contract state and thus non-volatile storage. In the `get()` function, the line `return state.ReadUint64([]byte("count"))` will read the `count` value \(and return it\), that `count` value is the same one that was written in the `_init()` function or the `add()`  function.

The state is described in more detail at the [Contract state](https://orbs.gitbook.io/contract-sdk/~/edit/drafts/-LVnlbSBlfPGStLbU5Xx/orbs-contracts/contract-state) documentation page.

### Exported functions

In Golang, functions beginning with the lowercase letters are considered as 'private' or not exported, and those whose name starts with an uppercase are 'public' and exported.

In Orbs, all functions should be written as 'private', meaning beginning with a lowercase letter, and functions that should be exported will be declared explicitly using the `sdk.Export()` function. In the example above, we can see that the functions `add` and `get` are declared as exported.

### Transactions and Queries

There are two ways of interacting with the Orbs blockchain: sending a **transaction** or running a **query**.

Sending a **transaction** means that the logic executed by the contract inside the virtual machine is executed under consensus, and thus the logic is **allowed** to change the state.

Running a **query** is a more lightweight operation which does not happen under consensus. However, if the logic of the querry is executed and the state is being written to, the result of the execution will be an **error**, as the operation was not done under a transaction.


