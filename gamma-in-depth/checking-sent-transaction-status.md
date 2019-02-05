# Checking sent transaction status

## Life span of a transaction

Once a transaction is sent to the blockchain, it is held in the ****transaction pool of nodes until it is executed \(mined\). During this time the transaction is in `PENDING` status.

When the transaction is finally executed, verified under consensus and added to a block, it transitions to`COMMITTED` status. It now also includes a **receipt** holding the execution output.

If the transaction fails to verify or ultimately expires, its status changes to `REJECTED`.

## Using Gamma CLI

After sending a transaction with `gamma-cli send-tx`, the transaction ID should be returned.

Use the **TxId** to check the status of the transaction

```text
gamma-cli get-status 0x189403BAA46F80150F1EA77fE9F47f40Fb1d8C52AF0b90D83DCB084385f1C6e5F7763D62D276bF86
```

## Command parameters

```text
gamma-cli get-status <TX_ID>
```

* `<TX_ID>` Transaction ID in [Base64](https://en.wikipedia.org/wiki/Base64) as returned from `gamma-cli send-tx`

## Cryptographic proof for a transaction

The Orbs blockchain is able to provide cryptographic proof for the execution of a transaction. This proof can be verified by light clients or third-party auditors without synchronizing the entire blockchain state.

Use the **TxId** to obtain the proof

```text
gamma-cli tx-proof 0x189403BAA46F80150F1EA77fE9F47f40Fb1d8C52AF0b90D83DCB084385f1C6e5F7763D62D276bF86
```

The command parameters are identical to `gamma-cli send-tx`

