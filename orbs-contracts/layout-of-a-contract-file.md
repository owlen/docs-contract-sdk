# Layout of a contract file

Orbs contacts are written in Golang, you can see some high level explanation on [Becoming a Go developer](https://orbs.gitbook.io/contract-sdk/~/edit/drafts/-LVnlbSBlfPGStLbU5Xx/getting-started/untitled) in the Getting Started episode. In this page we will go over the layout of a single contract and explain the different elements of code that the contract is comprised of.

### package _main_

Each contract must be of `package main`

This requirement originates from the way we later compile and incorporate the code into the blockchain. Orbs do not support multi-package projects at this moment.

In means of good practice around writing contracts, we have seen that usually, when a multi-package contract requirement arises, it means that the design might be calling for two different contracts in regards to storage isolation and code security. More on that later.

### Imports

As multi-package environment is not supported, the `import` area of your code can only comprise of Golang standard libraries or Orbs Contract SDK imports.  

### Exporting functions, events, and the constructor

In Golang, functions beginning with the lowercase letters are considered as 'private' or not exported, and those starting with an uppercase are 'public' and exported.

In Orbs, all functions should be written as 'private', meaning beginning with a lowercase letter, and functions that should be 
exported should be declared explicitly using the `sdk.Export()` function, which accepts pointer to a function (i.e. the function name).

The exception to this rule is events, which still need to be exported with a special `EVENTS` variable.

#### PUBLIC

The `PUBLIC` export is used to define which functions should be exported and be accessible by the distributed app client. For example:

```go
var PUBLIC = sdk.Export(transfer, getBalance)
```

This example will export two functions named `transfer` and `getBalance`.

#### EVENTS

The `EVENTS` export is used to declare which events are exported by the contract, for example:

```go
var EVENTS = sdk.Export(Approval)
```

This example will export an event named `Approval`

#### SYSTEM

The special system export is reserved, right now, only for the constructor function `_init`, 
it must exist at any contract when the special constructor function exists. This export usually looks like:

```go
var SYSTEM = sdk.Export(_init)
```

It enables the contract compiler to call the constructor function.

### Event declaration

Usually, after the initial implementation, the best practice would be to declare which events exist as part of the contract.

[Events](https://orbs.gitbook.io/contract-sdk/~/edit/drafts/-LVnlbSBlfPGStLbU5Xx/orbs-contracts/events) are declared by writing an empty 'public' function as such:

```go
func Approval(sender string, spender string, amount uint64) {}
```

Note that the empty curly braces `{}` must be explicitly written at the end of the line.

### Function implementation

Next, and finally, the functions themself should be written as part of the code. These are the functions that may be also exported for client usage.

The functions themselves can either change state or not. A function that does not change the state can later be used under the **run query** operation, while a function that changes the state (writes to it) must be executed under a **transaction**.

```go
func getBalance(targetAddress []byte) uint64 {
	address.ValidateAddress(targetAddress)
	return state.ReadUint64(targetAddress)
}
```

The example above creates a function called `getBalance` which accepts a byte array to a variable named `targetAddress`. 
The logic then validates the address and reads from the state whatever data that was stored there, which should be a unsigned
number of up to 64bit in size using `state.ReadUint64(targetAddress)`. 
Since the logic only reads data off the blockchain, it is possible to run this function using `run-query` API, but the contract 
must export the function as described above. 



