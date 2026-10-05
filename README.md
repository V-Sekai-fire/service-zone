# service-zone

One zone as one deployable domain: the planes and transport layers that share a shared-memory ring, packed together.

## What it is for

A domain is a packing of planes and transport layers. Members that exchange per-tick data over iceoryx2 shared memory must sit on one machine, so the ring decides the membership rather than a choice. Each member stays its own repository and image. Members reach each other through shared memory, so only the transport layers listen on a socket.

## Members

| member | why it is in the zone |
| --- | --- |
| `interactor-weft` | the runtime reaches the data plane through an in-process NIF |
| the data plane | the ring itself |
| `interactor-crowd` | reads and writes entity state every tick |
| `transport-ingest-c` | decodes player input datagrams and hands them to the data plane |
| `transport-gateway-c` | decodes control streams and hands them to the control plane |
| `interactor-tool` | is called from the ring, and a tool call carries a mesh or a stage worth not copying |
| `interactor-janet` | samples the ring at its own rate, outside the per-packet path |

## Not in the zone

`datasource-queen`, the store domain, tolerates one FoundationDB round trip, so it needs no ring. `service-behaviour`, the behaviour domain, changes a plan in seconds and wants a GPU, and neither is a reason to make every zone carry one.

## Build

There is nothing to build yet: the repository holds the member list, and no unit or machine definitions.

## Licence

MIT; see `LICENSE`.
