# A quick start guide to how to use address & best practices

## Addresses and smart contracts

As in real life, each entity needs a unique identifier in order to have a exclusive identity in the space.  
 The need for a unique identity is mandatory for -

* possessions of assets
* perform actions on assets
* make statement on an identity behalf

  Address may store any supported primitive types.

Smart contracts are a bunch of rules with a storage capability. When combining smart contracts with addresses, the result unlock the possibilites mentioned above -

* possessions of assets - a token contract maintain a mapping of addresses and its token balance
* perform actions on assets - a transfer method of a token contract enables transfer of tokens between addresses
* make statement on an identity behalf

## Addresses implementation in ORBs

The representation of an address in ORBs smart contracts is by a byte array. The value of an address is the a computation on a private key.

The computation uses the cryptographic hashes [Ripemd](https://en.wikipedia.org/wiki/RIPEMD) and [Sha256](https://en.wikipedia.org/wiki/SHA-2).

## Basics

### Get Caller Address

#### GO

Get the caller address:

```text
    GetSignerAddress(ctx Context) (Ripmd160Sha256, error)
```

Example:

```text
     callerAddress := c.Address.GetCallerAddress(ctx)
```

### Write to an address

#### GO

Write to an address a uint64 value:

```text
    WriteUint64ByAddress(ctx Context, address Ripmd160Sha256, value uint64) error
```

Example:

```text
     c.State.WriteUint64ByAddress(ctx, 2db0030F1555492f79537BDAC3052e6176B6143C, 66792218564)
```

It is possible to write different types into an address, see more [here](https://github.com/orbs-network/orbs-contract-sdk/blob/master/go/sdk/sdk.go$L16).

### Read from an address

#### GO

Read from an address a uint64 value:

```text
    ReadUint64ByAddress(ctx Context, address Ripmd160Sha256, value uint64) error
```

Example:

```text
    value := c.State.ReadUint64ByAddress(ctx, 2db0030F1555492f79537BDAC3052e6176B6143C)
```

It is possible to read different types from an address, see more [here](https://github.com/orbs-network/orbs-contract-sdk/blob/master/go/sdk/sdk.go#L6).

### Get Caller Address

#### GO

Get the caller address:

```text
    GetCallerAddress(ctx Context) (Ripmd160Sha256, error)
```

Example:

```text
    callerAddress := c.Address.GetCallerAddress(ctx)
```

## More Examples

### Validate Address

#### GO

Validate a given address:

```text
    ValidateAddress(ctx Context, address Ripmd160Sha256) error
```

Example - a valid address:

```text
    c.Address.ValidateAddress(ctx,2db0030F1555492f79537BDAC3052e6176B6143C)
```

Example - a non-valid address:

```text
    c.Address.ValidateAddress(ctx,07767723e1d1AD5c4F911302B82351486dE4F9C7EbB7fF515bC18b20E02EA8422A)
```

### Get Signer Address

#### GO

Get the transaction signer address:

```text
    GetSignerAddress(ctx Context) (Ripmd160Sha256, error)
```

Example:

```text
    callerAddress := c.Address.GetSignerAddress(ctx)
```

### Clear Address

#### GO

Clear the value of a given address:

```text
    ClearByAddress(ctx Context, address Ripmd160Sha256) error
```

Example:

```text
    c.State.ClearByAddress(ctx, 07767723e1d1AD5c4F911302B82351486dE4F9C7EbB7fF515bC18b20E02EA8422A)
```

## Addresses - What should be avoided

//TODO

## END

// ? Address or account? what's the difference? do we care?   
 // ? mention boil-plates because of Go \(vs JS\)   
 // ? Contract name - in deployment Json or contract code?   
 // ? Address validity, at the moment \(according to sdk\_address.go\) it's only length. // ? Write a basic intro to each processor \(i.e for GO, explain all the bolierplates\)

