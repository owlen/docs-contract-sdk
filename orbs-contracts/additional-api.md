# API Reference

This page is used to describe all the additional API which exists as part of the Contract SDK

## Env

To use the `Env` package, you need to import it

```go
import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/env"
)
```

It provides the following functions

### GetBlockHeight

Used to get the block height which will be the one this transaction be a part of

```go
GetBlockHeight() uint64
```

It will return the block height in decimal values

### GetBlockTimestamp

Used to get the block timestamp \(creation time\) which will be the one this transaction be a part of

```go
GetBlockTimestamp() uint64
```

It will return the block timestamp representing the Unix epoch in nanoseconds

### GetVirtualChainId

Used to get the virtual chain id this contract is executing under

```go
GetVirtualChainId() uint32
```

It will return the virtual chain id in decimal values

## Safemath

To use the `Safemath` package, you need to import it

```go
import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/safemath/safeuint256"
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/safemath/safeuint64"
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/safemath/safeuint32"
)
```

It gives the ability to work with 32, 64 and 256 bit unsigned integers, in a 'safe' way meaning there is overflow/underflow and illegal operation protection around the arithmetic operation done.

The API is uniform between the different variants and consist of the following functions

#### Add

Adds two numbers and returns the result, the numbers are validated so that they do not overflow after the addition.

```go
Add(x *big.Int, y *big.Int) *big.Int
Add(x uint32, y uint32) uint32
Add(x uint64, y uint64) uint64
```

#### Sub

Subtract `y` from `x`. The result is validated so if it becomes negative, an error is returned.

```go
Sub(x *big.Int, y *big.Int) *big.Int
Sub(x uint32, y uint32) uint32
Sub(x uint64, y uint64) uint64
```

#### Mul

Multiplies the values and returns the new number, the result is validated so that it does not overflow.

```go
Mul(x *big.Int, y *big.Int) *big.Int
Mul(x uint32, y uint32) uint32
Mul(x uint64, y uint64) uint64
```

#### Div

Performs the integer division of `x` and `y`. The remainder is discarded as it should in integer arithmetic and the input \(`y`\) is validated to not be zero.

```go
Div(x *big.Int, y *big.Int) *big.Int
Div(x uint32, y uint32) uint32
Div(x uint64, y uint64) uint64
```

#### Mod

Performs the modulo operation between `x` and `y`. The input is validated to be valid \(meaning `y` is not zero to avoid invalid division\) - the resulting number will hold the reminder as expected

```go
Mod(x *big.Int, y *big.Int) *big.Int
Mod(x uint32, y uint32) uint32
Mod(x uint64, y uint64) uint64
```

#### Validate

{% hint style="info" %}
Only relevant for `safeuint256`
{% endhint %}

The function validates that the number is not negative and did not overflow. If validation fails, the code will panic with the appropriate message

```go
Validate(n *big.Int)
```

It is called automatically on each operation, meaning after using `Add` or `Sub` or any operation of the safemath library, there is no need to manually validate.

