# Design a Key-Value Store

> This is a summary of Chapter 6 of [System Design Interview Volume 1](https://www.amazon.com/System-Design-Interview-insiders-Second/dp/B08CMF2CQF/).

In a key-value pair, the key must be unique. The value is opaque.

**Example key-value stores**: Amazon Dynamo, Memcached, Redis

## Characteristics of an example key-value store:

- Size of key-value is < 10KB
- Ability to store big data
- High Availability
- High Scalability
- Atomatic Scaling (based on traffic)
- Tunable consistency
- Low Latency

In-memory key-value store isn't enough to fit big data. 

Need a `distributed key-value store` (aka `distributed hash table`), which distributes key-value pairs across many servers.

## CAP Theorem

1. `Consistency`: All clients see the same data at the same time independent of server
2. `Availability`: Requests get served even if some nodes are down
3. `Partition Tolerance`: A partition indicates a comms break between two nodes. With partition tolerance, the system continues to operate despite network partitions.

CAP Theorem: "Must pick 2 our of the 3". Available combinations: `CA`, `CP`, `AP`.

Both highly consistent & highly available systems are not realistic because partitions do happen.

Banks are **high-consistency** systems, so in case of a partition issue, it sacrifices availability (i.e. returns an error if consistency can't be achieved) - since it can't return inconsistent results (e.g. account balance).

In **high-availability** systems, the system can return stale data. Writes will be accepted and eventually resolved.

## Components of a key-value store

1. **Data partition** - Use consistent hashing, more virtual nodes for servers of higher capacity
2. **Data replication** - Replicate data in the next $n$ unique nodes (to take into account virtual nodes)
3. **Consistency** - Synchronize data across replicas
4. **Inconsistency resolution** - Using `vector clocks`
5. **Handling Failures** - Use `gossip protocol` 
6. **System architecture diagram**
7. **Write path**
8. **Read Path**

Based on examples from Dynamo, Cassandra, BigTable.

### Consistency:
- Define $N$=Number of replicas, $W$=Write quorum size, $R$=Read quorum size. 
- Quorum is the minimum number of servers necessary to have acknowledged success. 
- The larger the quorum, the more the consistency, the lesser the latency
- R=1, optimized for fast read
- W=1, optimized for fast write
- W+R > N strong consistency is guaranteed (e.g. N=3, W=R=2)
  
Dynamo & Cassandra adopt eventual consistency, which is a form of weak consistency that eventually reaches consistency across all replicas.

### Handling Failures

Use `Gossip Protocol` to identify which server is down:
1. Each node maintains a node membership list of IDs and heartbeat counters
2. Each node periodically increments its heartbeat counter
3. Each node periodically sends heartbeats to a set of random nodes, which get propoagated
4. Once a node received heartbeats, it updates its info
5. If the heartbeat has not increased for more than a period, that member is considered offline.

**Handling temporary failures:**
1. `Strict quorum`: R/W is blocked until consensus
2. `Sloppy quorum`: System chooses first W and R healthy servers respectively for read/write on the hash ring, ignoring offline servers.

When a server comes back, data will be pushed back to it via `hinted handoff`.

**Handling permanent failures:**
Use anti-entropy prorocol to keep replicas in sync. A `Merkle tree` is used for inconsistency detection and minimizing the amount of data transferred.

Merkle Tree: 
1. Divide key space into buckets
2. Hash each key in bucket using a uniform hashing method
3. Create a hash per bucket (becomes a parent node)
4. Pair up parent nodes to create grand-parent node (hash their hashes)

Comparing merkle trees is like searching in a binary search tree, where you pick the left/right node based on inequality of the hashes.


