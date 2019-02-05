# Working with multiple environments

## Motivation

In a standard workflow, the first steps of development will be facing a locally running Gamma server. This server runs multiple nodes in-memory on your local machine.

In later stages of the development process, the contract should also be tested on a test net. Since the test net is external, the HTTP endpoints used will have to change.

To make this process easier, Gamma CLI supports multiple environments with an optional config file.

## Gamma config JSON

To configure multiple environments create a file named `orbs-gamma-config.json` in the local directory, with the following format

{% code-tabs %}
{% code-tabs-item title="orbs-gamma-config.json" %}
```javascript
{
  "Environments": {
    "local": {
      "VirtualChain": 42,
      "Endpoints": ["localhost"]
    },
    "testnet1": {
      "VirtualChain": 90043,
      "Endpoints": ["http://192.168.1.1", "http://192.168.2.2:8080"]
    },
    "testnet2": {
      "VirtualChain": 3007,
      "Endpoints": ["http://10.1.1.122", "https://node-example.com", "http://another.io:8081"]
    }
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
If a config file does not exist, the default environment is `"local"` with virtual chain `42` and the endpoint `"localhost"`
{% endhint %}

## Choosing environment in Gamma CLI

You can choose the active environment by passing the `-env` command line argument to every command. 

For example, to work with environment **testnet2**

```text
gamma-cli send-tx transfer.json -signer user1 -env testnet2
```

