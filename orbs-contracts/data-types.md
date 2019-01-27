# Data types

Data types refer to arguments in functions and return values. In Orbs, the implementations of the contract will always be statically typed, which means that the type must be known at compile time.

All types are passed by value in the Orbs Contract SDK, and the following types are supported

### Integers

The supported way of working with integers right now is using `uint32` or `uint64`. Currently that is the only two number formats which will pass compilation and runtime execution.

It is possible to run any arithmetic operation which exists in Go.

### Strings

The Orbs Contract SDK enables you to work with `string` values. As with integers, the string will behave like any other string in Go.

### Byte arrays

For any data related operation, including passing of addresses, the Go `[]byte` should be used. Similarly to strings and integers, you are able to run any operation on these byte arrays with Go.







