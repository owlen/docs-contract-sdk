---
description: >-
  Contracts running on Orbs are developed in the Go programming language. This
  page will help you set up a working Go environment on your machine.
---

# Becoming a Go developer

## Installing Go

The recommended way to install Go on Mac is with [brew](https://brew.sh/)

```
brew install go
```

If you prefer a regular package installer instead, those are available [here](https://golang.org/dl/). If you run into trouble, go over the official Go [installation instructions](https://golang.org/doc/install).

## Verifying the installation

Verify Go is installed correctly by running in terminal

```text
go version
```

Any version above 1.11 should suffice.

## The Go workspace

Go creates a workspace on your machine where source files should be placed. This is a bit different from other programming languages which are less opinionated about the location of your source files.

Unless configured explicitly otherwise, your Go workspace is found at

```text
~/go/src
```

The common convention is to place files in a directory structure that mirrors easily to Github. If your Github username is `johnsnow` and your repo name is `mycontract` you should place your files at

```text
~/go/src/github.com/johnsnow/mycontract
```

For more information about workspaces, consult the official Go [documentation](https://golang.org/doc/code.html#Workspaces).

## Choosing an editor

Working with an [IDE](https://en.wikipedia.org/wiki/Integrated_development_environment) that has good Go support is highly recommended for code completion, syntax highlighting and debugging.

[Atom](https://atom.io/) is an excellent free editor which has Go support through the [go-plus](https://atom.io/packages/go-plus) plugin. You can install both by running in terminal

```text
brew cask install atom
apm install go-plus
```

Another free alternative is [VSCode](https://code.visualstudio.com/), which [supports](https://code.visualstudio.com/docs/languages/go) Go out of the box. A commercial alternative is [GoLand](https://www.jetbrains.com/go/) by JetBrains. For the complete list of editors consult the official Go [documentation](https://golang.org/doc/editors.html).

## Learning Go

One of the main benefits of the Go programming language is its simplicity. It should not require more than a few days to gain a firm grasp of the syntax.

The official documentation contains a fantastic [Tour of Go](https://tour.golang.org) - an interactive tutorial that teaches the basics of the language in an hour or so. Another way to dive quickly into the language is using this [cheat sheet](https://learnxinyminutes.com/docs/go/) which contains all syntax in one page.

If you don't feel like learning the language first that's also fine. Most of the contract examples are simple enough to understand without any prior knowledge.

