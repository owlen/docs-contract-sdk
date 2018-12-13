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
{
  "user1": {
    "PrivateKey": "CVbAcCK9AsEdx+cxlzQW0svCRneVptJyYQtCGpunzU3kBUBTShRXAo0Whtr6n4Nj4tVilwL6vrmUcSiW9A5pYw==",
    "PublicKey": "5AVAU0oUVwKNFoba+p+DY+LVYpcC+r65lHEolvQOaWM=",
    "Address": "pGdqwA6dnTyjMXE8LBnh2HvhaJg"
  },
  "user2": {
    "PrivateKey": "mQUAnmIftxonjYBUlCks4EfPzRJqgO5uRtfy3wq/sIjKfzei69ZV1wRhm0VExY5in8exVsvi1I65VqSXXhG1Zg==",
    "PublicKey": "yn83ouvWVdcEYZtFRMWOYp/HsVbL4tSOuVakl14RtWY=",
    "Address": "4WhWtACPTeBLokzQsHWLrKXgD4j7"
  },
  "user3": {
    "PrivateKey": "AN68zZOvVWRhip2lMfiVOToRjHtIx89X8auZgAKJJYfE0S5lvC7g7mp/nAbK379/AieuSotXM90LJxph1RNyAA==",
    "PublicKey": "xNEuZbwu4O5qf5wGyt+/fwInrkqLVzPdCycaYdUTcgA=",
    "Address": "3qH4WAToY4SnzibNsBCqNSvuRSUD"
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Feel free to edit the file manually and add your own accounts. "Real-life" accounts are usually created using the [Orbs Client SDK](https://github.com/orbs-network/orbs-client-sdk-go).

The fields are encoded as follows:

* Textual IDs for every account \(eg. `user2`\) can be changed to any string you prefer
* Key fields are encoded in [Base64](https://en.wikipedia.org/wiki/Base64)
* Address fields are strings as returned from the client SDK \(encoded in [Base58](https://en.wikipedia.org/wiki/Base58)\)

