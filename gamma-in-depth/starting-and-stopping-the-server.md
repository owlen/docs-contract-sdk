# Starting and stopping the server

## Using Gamma CLI

Start Gamma server by running in terminal

```text
gamma-cli start-local
```

When finished with the server, stop it by running in terminal

```text
gamma-cli stop-local
```

When you're not sending transactions, the nodes that make up Gamma server will still keep closing empty blocks. It is therefore recommended to stop the server when it's not needed.

### Customizing the Gamma server port

Gamma server is an actual blockchain instance running on your local machine. Clients like Gamma CLI are able to communicate with this instance using HTTP.

By default, Gamma server listens on port **8080**. To start Gamma server on a different port, **8089** for example, run the following in terminal

```text
gamma-cli start-local -port 8089
```

## Running Prism

Prism is the Orbs block explorer, you can access the actual one at: [https://prism.orbs.network](https://prism.orbs.network)

When running gamma and starting the server, it will also automatically run prism which will be accessible locally by browsing to http://localhost:3000

### Customizing the Prism port

Prism will start on port **3000** by default, to start it on a different port, **3003** for example, run the following when starting gamma in the terminal

```text
gamma-cli start-local -prismPort 3003
```

This command line flag can of course be chained with other flags.

### Disable Prism

If you do not wish Prism to start with Gamma, use the `no-ui` flag, and run the following when starting Gamma in the terminal

```text
gamma-cli start-local -no-ui
```

## In-memory instance

{% hint style="warning" %}
It's important to understand that Gamma server is only running in-memory. 
{% endhint %}

Every time you restart Gamma server, all contracts and state disappear from memory. You will need to deploy the contracts again when the server is started.

