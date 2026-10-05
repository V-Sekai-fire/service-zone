# service-zone

One zone as one deployable domain: the planes and transport layers that share a shared-memory ring, packed together.

## What it is for

A domain is a packing of planes and transport layers. Members that exchange per-tick data over iceoryx2 shared memory must sit on one machine, so the ring decides the membership rather than a choice. Each member stays its own repository and image, and this repository holds the packing that runs them together. Members reach each other through shared memory, so only the transport layers listen on a socket.

## Build

There is nothing to build yet: the repository holds the packing, and no unit or machine definitions.

## Licence

MIT; see `LICENSE`.
