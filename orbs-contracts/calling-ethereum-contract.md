# Calling Ethereum contract

It is possible to perform a cross-chain call and access a contract that is deployed on Ethereum from within an Orbs contract.

The API for this is included in the ethereum library:

```go
import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/ethereum"
)
```

The library exposes two different functions described below:

### GetBlockNumber

This function is used to get the latest 'safe' block number in Ethereum. The 'safe' block means a block which is in the past, around 25 minutes, to avoid forks.

```go
GetBlockNumber()
```

### CallMethod

This function is used to perform a method call on ethereum, the action performed in this function is `call` in ethereum - we do not perform transactions from within our blockchain, mainly due to response time and finality considerations.

```go
CallMethod(
        ethContractAddress string, 
        jsonAbi string, 
        methodName string, 
        out interface{}, 
        args ...interface{})
```

The arguments `CallMethod` takes are:

* `contractAddress` - The Ethereum contract address with a 0x prefix
*  `jsonAbi` - The ABI of the call, as a JSON string
* `methodName` - The method to call in the contract
* `out` - The result of the contract call - this needs to be a pointer to the expected return value/struct, the struct members need to be defined as PascalCase style, see examples below
* `args` - The variadic parameter list for the method you are calling on Ethereum

For example, using the following contract on Ethereum:

```text
pragma solidity ^0.4.0;
contract SimpleStorage {
    struct Item {
        uint256 intValue;
        string stringValue;
    }
    Item item;

    constructor(uint256 _intValue, string _stringValue) public {
        set(_intValue, _stringValue);
    }

    function set(uint256 _intValue, string _stringValue) private {
        item.intValue = _intValue;
        item.stringValue = _stringValue;
    }

    function getInt() view public returns (uint256) {
        return item.intValue;
    }

    function getIntMultiple(uint256 _multiple) view public returns (uint256) {
        return _multiple * item.intValue;
    }

    function getString() view public returns (string) {
        return item.stringValue;
    }

    function getValues() public view returns (uint256 intValue, string stringValue) {
        intValue = item.intValue;
        stringValue = item.stringValue;
    }
}
```

If we want to call `getValues` we use the following code in our Orbs contract:

```go
package main

import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1"
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/ethereum"
)

var PUBLIC = sdk.Export(readString, readStringFromValues)
var SYSTEM = sdk.Export(_init)

func _init() {
}

func readStringFromValues(address, abi string) string {
    // getValues return a uint256 and a string, note the PascalCase
    out := new(struct { // creates a pointer to a struct of the expected return value
        IntValue    *big.Int
        StringValue string
    })
        
    ethereum.CallMethod(address, abi, "getValues", out)
    return ret.StringValue
}

func readString(address, abi string) string {
    var out string
    ethereum.CallMethod(address, abi, "getString", &out)
    return out
}
```

### CallMethodAtBlock

This function is the same as the CallMethod function, and it only allows to define which block you want to use.

```go
CallMethodAtBlock(
        ethBlockNumber uint64,
        ethContractAddress string, 
        jsonAbi string, 
        methodName string, 
        out interface{}, 
        args ...interface{})
```

### GetTransactionLog 

This function can enable you to access the Transaction Receipt of a specific transaction on Ethereum to access and filter its logs according to a specific event name.

```go
GetTransactionLog(
                ethContractAddress string, 
                jsonAbi string, 
                ethTxHash string, 
                eventName string, 
                out interface{}) (ethBlockNumber uint64, ethTxIndex uint32)
```

The arguments `GetTransactionLog` takes are:

* `ethContractAddress` - The Ethereum contract address with a 0x prefix
* `jsonAbi` - The ABI of the contract with the event, as a JSON string
* `ethTxHash` - The Ethereum transaction address with a 0x prefix
* `eventName` - The event to filter by
* `out` - The event data, this needs to be a pointer to the expected return value/struct, the struct members need to be defined as PascalCase style. See an examples below.

The function returns:

* `ethBlockNumber` - The block number of the log requested
* `ethTxIndex` - The transaction index in the block

An example of using the `GetTransactionLog()` for the following event ABI:

```javascript
{
      "constant": false,
      "inputs": [
        {
          "name": "tuid",
          "type": "uint256"
        },
        {
          "name": "ethAddress",
          "type": "address"
        },
        {
          "name": "orbsAddress",
          "type": "bytes20"
        },
        {
          "name": "value",
          "type": "uint256"
        }
      ],
      "name": "transferOut",
      "outputs": [],
      "payable": false,
      "stateMutability": "nonpayable",
      "type": "function"
    }
```

The Orbs contract code should look like:

```go
package main

import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1"
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/ethereum"
)

var PUBLIC = sdk.Export(filterLogs)
var SYSTEM = sdk.Export(_init)

func _init() {
}

type EmitEvent struct {
    Tuid        *big.Int
    EthAddress  [20]byte
    OrbsAddress [20]byte
    Value       *big.Int
}

func filterLogs(address, abi, txHash string) {
    event := new(EmitEvent)
    ethereum.GetTransactionLog(address, abi, txHash, "transferOut", event)
    // do something with the event data
}
```

