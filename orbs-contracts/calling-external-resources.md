# Calling other contracts

Orbs contracts are able to call other orbs contracts as part of the execution logic, we call this action a service call.

In order to call other contracts, you will need to import the service library

```go
import (
	"github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/service"
)
```

The service library exposes a single function called `CallMethod` which is used to call the external contract which is deployed on the same virtual chain of the Orbs blockchain.

```go
CallMethod(serviceName string, methodName string, args ...interface{}) []interface{}
```

This function received the following arguments:

* `serviceName` - The contract name
* `methodName` - The method to call in that contract
* `args` - The variadic parameter for the method arguments 

The return value will contain the array of the result of the function execution.





