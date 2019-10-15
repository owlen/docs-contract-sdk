# Events

Orbs contract events give you the ability to log information into the blockchain that is stored as part of the receipt block.

Here is a simple contract that emits an event. We will go over it in details:

```go
package main

import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1"
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/events"
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/state"
)

var PUBLIC = sdk.Export(giveBirth)
var SYSTEM = sdk.Export(_init)
var EVENTS = sdk.Export(BabyBorn)

func BabyBorn(name string, weight uint32) {}

func _init() {
    state.WriteUint64([]byte("some_data"), 1)
}

func giveBirth(name string) {
    events.EmitEvent(BabyBorn, name, uint32(3))
}
```

Using the Events API require you first to import it:

```go
import (
    "github.com/orbs-network/orbs-contract-sdk/go/sdk/v1/events"
)
```

Next, we export the event:

```go
var EVENTS = sdk.Export(BabyBorn)
```

Then we declare it as an empty function. Note that the empty bracers are required \(`{}`\):

```go
func BabyBorn(name string, weight uint32) {}
```

When the function `giveBirth(name string)` is called, we want the event to be emitted, so we call the `events.EmitEvent` function:

```go
events.EmitEvent(BabyBorn, name, uint32(3))
```

The arguments are a pointer to the event function \(which is also exported\) and the event arguments.



