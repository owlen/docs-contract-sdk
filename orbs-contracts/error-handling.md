# Error handling

The execution flow of Orbs Contracts does not include error handling, meaning that once an error occurs, the code will simply stop execution, the state in the blockchain will not be stored and any changes done up until the error will be reverted.

When the contract execution hits an error, the `ExecutionResult` will be `ERROR_SMART_CONTRACT` and the error message will be displayed in `OutputArguments`.

Using `panic` is the simplest way to report an error from within a contract and in a similar way seen above, the error message will be returned as part of the output arguments of the execution.

So for example, the below code

```go
func throw() {
	panic("the error message from the code")
}
```

Will output the following result on execution

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



