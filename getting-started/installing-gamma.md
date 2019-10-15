---
description: >-
  Gamma is a personal Orbs blockchain running locally that allows developers to
  easily test, run and deploy smart contracts.
---

# Installing Gamma - local blockchain

## Installing Gamma

Gamma uses [Docker](https://www.docker.com/) to run a personal blockchain with multiple nodes locally. Make sure Docker is available on your machine. See installation instructions [here](https://docs.docker.com/docker-for-mac/install/).

Next, install the Gamma CLI with [brew](https://brew.sh/)

```
brew install orbs-network/devtools/gamma-cli
```

Verify the installation by running in terminal

```text
gamma-cli version
```

## Gamma CLI

`gamma-cli` is the command line tool for developers to interact with a Gamma server instance running on their machine.

See the various commands supported by the CLI by running in terminal

```text
gamma-cli help
```

You can use the CLI to start and stop Gamma server, deploy contracts and send transactions.

## Gamma server

Gamma server is an in-memory virtual chain on top of an Orbs blockchain with several nodes on your local machine. The server allows you to test your contracts locally before deploying them to production.

Gamma server will be installed automatically by the CLI.

Start Gamma server by running in terminal

```text
gamma-cli start-local
```

If everything went well, you now have a running ORBS blockchain on your local machine. Yes, it's that simple! You can browse to http://localhost:8080/ to view the status of your local ORBS instance.

The `start-local` comands also runs our block explorer, Prism. You can use Prism to get more info about your blockchain instance by browsing to http://localhost:3000/. 

When finished with the server, stop it by running in terminal

```text
gamma-cli stop-local
```

