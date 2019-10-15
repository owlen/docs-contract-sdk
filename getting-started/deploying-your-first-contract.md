---
description: >-
  This tutorial will take you through the entire process of writing a contract and deploying
  it on a local instance of ORBS in just a few minutes.
---

# Deploying your first contract

## 1. Write a simple contract

Let's write a simple example that implements a counter. Create a file named `counter.go` and type in the following content

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

Don't worry if you don't fully understand the code at this point.

## 2. Start Gamma server

We'll test our contract on Gamma server. Start it from terminal

```text
gamma-cli start-local
```

You can keep an eye on Prism (http://localhost:3000/) to see new blocks and transactions apear 
as you continue with the deployment in the next steps.  

## 3. Deploy the contract

To deploy the counter contract, run in terminal

```text
gamma-cli deploy counter.go -name MyCounter
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

> More Information about sending transactions and the Gamma-cli json files structures can be found at the [gamma in depth chapter](../gamma-in-depth/sending-transactions-and-queries.md) of this documentation

To increment the counter by 75, let's send this transaction 3 times from terminal

```text
gamma-cli send-tx add-25.json -signer user1
gamma-cli send-tx add-25.json -signer user1
gamma-cli send-tx add-25.json -signer user1
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
gamma-cli run-query get.json
```

Note that transactions that change state require consensus by several nodes. Reading state with queries is a simpler action that doesn't require consensus.

## 6. Stop Gamma server

Since we're done testing, the server is no longer needed. Let's stop it from terminal

```text
gamma-cli stop-local
```

