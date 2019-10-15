# Calling other contracts

Orbs contracts can call other orbs contracts as part of the execution logic. We call this action a service call.

To call other contracts from your contrat, you must to import the service library:

```go
import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/service"
)
```

The service library exposes a single function called `CallMethod`. `CallMethod` is used to call the external contract, which must be deployed on the same virtual chain of the Orbs blockchain.

```go
CallMethod(serviceName string, methodName string, args ...interface{}) []interface{}
```

This function received the following arguments:

* `serviceName` - The contract name
* `methodName` - The method to call in that contract
* `args` - The variadic parameter for the method arguments 

The return value contains the array of the result of the function execution.
