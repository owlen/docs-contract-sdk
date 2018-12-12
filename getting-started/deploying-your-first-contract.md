---
description: >-
  This tutorial will take you through the entire process of writing and
  deploying a contract from start to finish in just a few minutes.
---

# Deploying your first contract

## 1. Write a simple contract

Let's write a simple example that implements a counter. Create a file named `counter.go` and type in the following content

{% code-tabs %}
{% code-tabs-item title="counter.go" %}
```go
package main

import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk"
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/state"
)

var PUBLIC = sdk.Export(add, get)
var SYSTEM = sdk.Export(_init)

func _init() {
    state.WriteUint64ByKey("count", 0)
}

func add(amount uint64) {
    count := state.ReadUint64ByKey("count")
    count += amount
    state.WriteUint64ByKey("count", count)
}

func get() uint64 {
    return state.ReadUint64ByKey("count")
}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

Don't worry if you don't fully understand the code at this point.

## 2. Start Gamma server

We'll test our contract on Gamma server. Start it from terminal

```text
gamma-cli start-local
```

## 3. Deploy the contract

To deploy the counter contract, run in terminal

```text
gamma-cli deploy -name MyCounter -code counter.go
```

If the deploy is successful, you'll see a response similar to this

```javascript
{
  "RequestStatus": "COMPLETED",
  "TxId": "7Y4urVmKvunYsxh7kKhUoQ72XjSJcdkBxxzBcauC9icC9gzMy8mPDcg",
  "ExecutionResult": "SUCCESS",
  "OutputArguments": [],
  "TransactionStatus": "COMMITTED",
  "BlockHeight": "1869",
  "BlockTimestamp": "2018-12-05T13:05:51.347Z"
}
```

## 4. Send a transaction to increment the counter

Write the transaction details in a JSON file named `add-25.json`

{% code-tabs %}
{% code-tabs-item title="add-25.json" %}
```javascript
{
  "ContractName": "MyCounter",
  "MethodName": "add", 
  "Arguments": [
    {
      "Type": "uint64",
      "Value": "25"
    }
  ]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

To increment the counter by 75, let's send this transaction 3 times from terminal

```text
gamma-cli send-tx -i add-25.json -signer user1
gamma-cli send-tx -i add-25.json -signer user1
gamma-cli send-tx -i add-25.json -signer user1
```

Note that the transaction will be signed by `user1`, an example account found in `orbs-test-keys.json`

## 5. Read the counter value

Write the query details in a JSON file named `get.json`

{% code-tabs %}
{% code-tabs-item title="get.json" %}
```javascript
{
  "ContractName": "MyCounter",
  "MethodName": "get",
  "Arguments": []
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

This query will read the counter value from the contract's state. Send it from terminal

```text
gamma-cli read -i get.json
```

Note that transactions that change state require consensus by several nodes. Reading state is a simpler action that doesn't require consensus.

## 6. Stop Gamma server

Since we're done testing, the server is no longer needed. Let's stop it from terminal

```text
gamma-cli stop-local
```

