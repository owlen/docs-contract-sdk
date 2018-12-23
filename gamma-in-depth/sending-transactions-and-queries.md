# Sending transactions and queries

## Using Gamma CLI

Transactions are different from read-only queries by the fact they're able to change state. Transactions require consensus by several nodes whereas read-only queries can rely on a single node.

Send transactions to contracts by running `gamma-cli send-tx` and giving a JSON file containing the call arguments.

For example, to send the transaction with arguments in **transfer.json**

```text
gamma-cli send-tx transfer.json -signer user1
```

Perform queries and call read-only contract methods by running `gamma-cli run-query` and giving a similar JSON file.

For example, to make the read call with arguments in **get-balance.json**

```text
gamma-cli run-query get-balance.json -signer user1
```

## Command parameters

```text
gamma-cli send-tx <INPUT_FILE> -arg# [OVERRIDE_ARG_#] -signer [ID_FROM_KEYS_JSON]
```

```text
gamma-cli run-query <INPUT_FILE> -arg# [OVERRIDE_ARG_#] -signer [ID_FROM_KEYS_JSON]
```

* `-signer` Account ID of the signer of the call \(from `orbs-test-keys.json`\)
* `-arg#` Override the value of argument number \# from the input call argument JSON

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
    "Value": "00ff018e00ab2fe901"
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

## Overriding arguments from command line

Consider a JSON for a typical **transfer** method

{% code-tabs %}
{% code-tabs-item title="transfer-15.json" %}
```javascript
{
  "ContractName": "MyToken",
  "MethodName": "transfer",

  "Arguments": [
    {
      "Type": "uint64",
      "Value": "15"
    },
    {
      "Type": "bytes",
      "Value": "b3d1caa2b3680e2c8feffa269c207c553fbbc828"
    }
  ]
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The first argument is the **amount** and the second argument is the **recipient address**.

If you want to send multiple transactions with different amounts or different addresses, creating multiple JSON files containing the different values can be a hassle.

Instead, use the optional `-arg1` and `-arg2` command line arguments to override values

```text
gamma-cli send-tx transfer-15.json
```

           will send **15** tokens to recipient **b3d1caa2b3680e2c8feffa269c207c553fbbc828**

```text
gamma-cli send-tx transfer-15.json -arg1 22
```

           will send **22** tokens to recipient **b3d1caa2b3680e2c8feffa269c207c553fbbc828**

```text
gamma-cli send-tx transfer-15.json -arg2 7ccd7f7c18c0cb749dd8b8949f4b4e31f7188394
```

           will send **15** tokens to recipient **7ccd7f7c18c0cb749dd8b8949f4b4e31f7188394**

