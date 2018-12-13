---
description: >-
  This page is for informational purposes only for advanced users. These
  technical details are abstracted away from developers by Gamma CLI.
---

# Gamma server under the hood

Gamma server runs under the hood on [Docker](https://www.docker.com/). Docker is a platform that performs operating-system-level virtualization, also known as "containerization".

## Docker image for Gamma

You can print docker images that are available on your machine using the docker CLI

```text
docker images
```

If you've installed Gamma CLI successfully, you should see among the results something similar to

```text
REPOSITORY          TAG                      IMAGE ID            CREATED             SIZE
orbsnetwork/gamma   v0.7.0                   b208261722bf        2 weeks ago         382MB
```

Gamma CLI downloads this image automatically from [Docker Hub](https://hub.docker.com/) with `docker pull`

## Running the docker image

When Gamma CLI is starting Gamma server, under the hood it's running

```text
docker run -d --name orbs-gamma-server orbsnetwork/gamma
```

When Gamma CLI stops Gamma server, under the hood it's running

```text
docker stop orbs-gamma-server
docker rm -f orbs-gamma-server
```

You can check if a docker container is currently running with

```text
docker ps
```

And if it is, you can examine the logs of the container with

```text
docker logs -f orbs-gamma-server
```

