# Sending transactions and queries

## Using Gamma CLI

Transactions are different from read-only queries by the fact they're able to change state. Transactions require consensus by several nodes whereas read-only queries can rely on a single node.

Send transactions to contracts by running `gamma-cli send-tx` and giving a JSON file containing the call arguments.

For example, to send the transaction with arguments in **transfer.json**

```text
gamma-cli send-tx -i transfer.json -signer user1
```

Perform queries and call read-only contract methods by running `gamma-cli read` and giving a similar JSON file.

For example, to make the read call with arguments in **get-balance.json**

```text
gamma-cli read -i get-balance.json -signer user1
```

### Command parameters

* `-i` Path of the JSON file containing the call arguments
* `-signer` Account ID of the signer of the call \(from `orbs-test-keys.json`\)

## Call argument JSON

This simple JSON file is used to let Gamma CLI know which contract method should be executed and what arguments should be passed to it.

An example of such a JSON is

```javascript
{
  "ContractName": "CounterExample",
  "MethodName": "add",
  "Arguments": [
    {
      "Type": "uint64",
      "Value": "25"
    }
  ]
}
```

The **ContractName** should be the name chosen during deployment of the contract with `gamma-cli deploy`. The method name should be one of the exported methods found in the contract source code.

The array of arguments should be given according to the declaration of the method in contract source code.

### Supported argument types

* `uint32` - Integer with 32 bit precision. Matches the `uint32` type in Go contracts. Provided in the JSON as a string of a decimal number. For example

```javascript
  {
    "Type": "uint32",
    "Value": "25"
  }
```

* `uint64` - Integer with 64 bit precision. Matches the `uint64` type in Go contracts. Provided in the JSON as a string of a decimal number. For example

```javascript
  {
    "Type": "uint64",
    "Value": "10029999"
  }
```

* `string` - String. Matches the `string` type in Go contracts. Provided in the JSON as a UTF8 string. For example

```javascript
  {
    "Type": "string",
    "Value": "Hello world"
  }
```

* `bytes` - An array of bytes \(blob\). Matches the `[]byte` type in Go contracts. Provided in the JSON as a hex string. For example

```javascript
  {
    "Type": "bytes",
    "Value": "00ff018e00ab"
  }
```

In addition to these primitives, Gamma CLI supports several aliases for convenience:

* `gamma:keys-file-address` - An account address by ID. The value should be an account ID from `orbs-test-keys.json`. An alias for the type `bytes` which means it matches the `[]byte` type in Go contracts. Used to pass the account address in raw form.

```javascript
  {
    "Type": "gamma:keys-file-address",
    "Value": "user3"
  }
```

