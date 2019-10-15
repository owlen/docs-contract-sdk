# Error handling

The execution flow of Orbs contracts does not include error handling, meaning that once an error occurs, code execution stops, the state in the blockchain is not stored, and any changes done up until the error are reverted.

When the contract execution hits an error, the `ExecutionResult` is set to `ERROR_SMART_CONTRACT`, and an error message is set in `OutputArguments`.

Using `panic` is the simplest way to report an error from within a contract, and in a similar way seen above, the error message is returned as part of the output arguments of the execution.

For example, the code:

```go
func throw() {
    panic("the error message from the code")
}
```

Will output the following result on execution:

```javascript
{
  "RequestStatus": "COMPLETED",
  "ExecutionResult": "ERROR_SMART_CONTRACT",
  "OutputArguments": [
    {
      "Type": "string",
      "Value": "the error message from the code"
    }
  ]
}
```



