# Design Consistent Hashing

> This is a summary of Chapter 5 of [System Design Interview Volume 1](https://www.amazon.com/System-Design-Interview-insiders-Second/dp/B08CMF2CQF/).

We use hashing to balance load across $n$ servers.

Typically, $serverIndex = hash(key)\;mod\;N$.

The problem: if server count changes, the rehash results in remapping of nearly all data. For example, if servers are caches, then rehashing causes lots of cache misses. Consistent Hashing mitigates this problem.

`Consistent Hashing` is a special kind of hashing such that in case of resizing, only $k/n$ keys needs to be remapped on average, where $k$ is the number of keys and $n$ is the number of slots.

`SHA-1`'s `hash space` goes from 0 to $2^{160}-1$. The `hash ring` means that the the next value after the max is 0. Note that there is no modulo (because the ring is conceptual. See below).

The servers are hashed on to the `hash ring`. In an item lookup, the item should be contained in the next server on the ring going clock-wise. (I.e. each server contains the data that correspond to the the range of hashes between its own hash, and the previous server's hash, where the previous server is the one that's adjacent to it going counter-clockwise.)

A problem of `non-uniform key distribution` can be solved by using `virtual nodes`. This means that a server has multiple hashes on the ring that maps to it.

When a server is added, data in the range between its hash and the previous server now belong to the new server.

When a server is removed, its data needs to be redistributed to the next server (in clockwise fashion)

