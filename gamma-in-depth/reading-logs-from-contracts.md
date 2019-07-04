# Reading Logs from Contracts

In multiple cases it is required to log information about the execution of your contracts - these logs are intended for development purposes only and should not be a part of your final contract.

During the development lifecycle, it is possible to use `println()` function from the standard Go library, this will output the message out to the stderr of the server.

In order to 'listen' to these log messages, Gamma-cli enables you to run

```text
gamma-cli logs
```

which will run indefinitely and listen to the output pipe from within the docker instance which runs the gamma server.

To stop listening, send a break signal using `ctrl+c`

