# Creating a new contract

Developing a contract should be done via a Golang IDE, just any other project using Go.

### Development

After starting a new project/workspace, depending on the IDE, the development should start by creating the contract file, which contains the main package.

{% hint style="info" %}
The contract file name should be meaningful. When deploying, if the contract name is not specified, we use the contract filename as the deployed contract name.
{% endhint %}

The following boilerplate can be a good start to work with:

```go
package main

import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1"
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/state"
)

var PUBLIC = sdk.Export() // TODO: add exported methods
var SYSTEM = sdk.Export(_init)

func _init() {
    // TODO: add init logic
}
// TODO: add contract logic (methods)
```

Next, add your functions and export them as needed.

### Testing

Testing your contract is done by utilizing the gamma-cli, which is an emulation of the full blockchain. As part of the contract sdk we expose the following import:

```go
import (
    "github.com/orbs-network/orbs-contract-sdk/go/testing/gamma"
)
```

It wraps the gamma-cli and enables the testing code to deploy and run functions on gamma, emulating the Orbs blockchain and ensuring your contract is behaving as expected.

We recommend creating a `test` folder under the location of your contract go file and add tests there. 

The example below uses a standard ERC20 contract to run some tests, the folder structure is as such:

```text
/
 - /test
 - - /balanceOf_user1.json
 - - /token_init_test.go
 - /erc20.go
```

In that folder structure, `erc20.go` is the contract implementation, `token_init_test.go` holds some testing code which we explore later, and `balanceOfuser1.json` holds the gamma-cli query payload, which is executed over the Orbs blockchain \(gamma\) and runs the test.

Observing the testing code, `token_init_test.go` we can see the following:

{% code-tabs %}
{% code-tabs-item title="token\_init\_test.go" %}
```go
package test

import (
    "github.com/orbs-network/orbs-contract-sdk/go/testing/gamma"
    "strings"
    "testing"
)

func TestTokenInit(t *testing.T) {
    gammaCli := gamma.Cli().Start()
    defer gammaCli.Stop()

    out := gammaCli.Run("deploy ../erc20.go -name OrbsERC20 -signer user1")
    if !strings.Contains(out, `"ExecutionResult": "SUCCESS"`) {
        t.Fatal("deploy failed")
    }

    if !strings.Contains(out, `"EventName": "Transfer",`) {
        t.Fatal("initial transfer (mint) did not fire during init")
    }

    out = gammaCli.Run("run-query balanceOf-user1.json")
    if !strings.Contains(out, `"Value": "1000000000000000"`) {
        t.Fatal("initial get failed")
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

We can see that it uses the `gamma` package, which is the wrapping of gamma-cli inside go code. Using `Start()` tells it to run gamma and wait for it to start, which can take several seconds to complete.

Next, the test itself tried to deploy the contract, the command to deploy inside the `Run()` function is exactly the same as you would execute from within the command line, as this is wrapping gamma execution directly.

The testing code then asserts for two things:

* If the execution of the deploy was successful
* Then if there was a `Transfer` event, as the ERC20 implementation performs a transfer in its `_init()` function, and the ERC20 spec requires an event on transfer

Next, a query is executed to assert that the balance of `user1` is as expected. This is more of a sanity check on the deploy, to make sure that indeed the blockchain was updated correctly and that the contract initiated everything as expected. The payload inside `balanceOf_user1.json` is:

```javascript
{
  "ContractName": "OrbsERC20",
  "MethodName": "balanceOf",
  "Arguments": [
    {
      "Type": "gamma:keys-file-address",
      "Value": "user1"
    }
  ]
}
```

Which means that the method `balanceOf` in contract `OrbsERC20` is executed with the argument specified, which is the key for user1 \(the user which was used to sign the deploy transaction\)



