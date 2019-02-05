# Test keys and accounts

## User accounts

When a user sends a transaction to the blockchain, the transaction needs to be signed with the user's private key. A standard user account includes the following details:

* User public key
* User private key
* User address

## Test accounts for Gamma CLI

Gamma CLI simulates transactions for testing contracts and therefore needs a set of demo user accounts.

When Gamma server is first started, Gamma CLI automatically creates 10 testing accounts and saves their details in a JSON file named `orbs-test-keys.json` in the local directory.

{% hint style="danger" %}
These keys are for testing only and should not be used in secure production environments.
{% endhint %}

Every account is assigned a textual ID, from `user1` to `user10` which can be provided as a command line argument to Gamma CLI to specify that a specific account should sign a transaction.

## Generating new test accounts

To replace the keys with a new batch of 10 accounts run in terminal

```text
gamma-cli gen-test-keys
```

This will override `orbs-test-keys.json` with new data.

## Editing account details manually

The JSON format of `orbs-test-keys.json` is straightforward

{% code-tabs %}
{% code-tabs-item title="orbs-test-keys.json" %}
```javascript
  "user1": {
    "PrivateKey": "0x8fc915f55aD5c6EFA5dC9a20F14a1Ec365afa23Ed1E5eB42a7512e2977C6693D77b5D6bFDbFb44A441330d1EDcD7d654240fb6B1b5FfeDAB94695fc70576eCE1",
    "PublicKey": "0x77B5D6bFDbfb44A441330d1eDCD7d654240Fb6B1b5FfEDAb94695Fc70576eCE1",
    "Address": "0xAECf291DA35F40D161B18eA01439CE3173D31AFf"
  },
  "user2": {
    "PrivateKey": "0x09f781c591826F7c2c59905e1Ad3c735DbA4C66611f952BF11eb00f982b1644e4Be27318345a3A3dbb38aC64A603dd573d886EB22B1634B580661fd164467670",
    "PublicKey": "0x4be27318345a3A3dBb38ac64A603DD573d886eB22B1634b580661fd164467670",
    "Address": "0xD66D89bB766745943c1c87062Ca0D3587e7D926B"
  },
  "user3": {
    "PrivateKey": "0x31e9AF96EF98957B966078b3Ea7cB058bFa10282b6A20DF832d817e4302114aa150FBFb587be65E07765a075988fB49e3CeaAe034E5e731aa961fAfc1375142a",
    "PublicKey": "0x150FbfB587BE65e07765a075988fb49e3cEAAe034E5e731aA961faFc1375142a",
    "Address": "0x28E445b353BC8376FD13291583Ec55e3e6140Ec5"
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Feel free to edit the file manually and add your own accounts. "Real-life" accounts are usually created using the [Orbs Client SDK](https://github.com/orbs-network/orbs-client-sdk-go).

The fields are encoded as follows:

* Textual IDs for every account \(eg. `user2`\) can be changed to any string you prefer
* Key and Address fields are encoded in [Base64](https://en.wikipedia.org/wiki/Base64)



