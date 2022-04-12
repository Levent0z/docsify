# System Design

## Load Balancer
- Can sit between
  - user & web server
  - web servers & internal platform layer (i.e. cache or app servers)
  - internal platform layer and database
- Load balancing methods:
  - Least connection
  - Least response time
  - Least bandwidth
  - Round-robin
  - Weighted round-robin (based on HW caps)
  - IP hash
- Redundancy through clustering, dual load balancer monitor each other, when one fails the other takes over
- Implementations
  - Client-side
  - dedicated hardware
  - software "HAProxy"

## Caching
- Types
  - Application server cache
  - Distributed cache
  - Global cache
  - CDN
- Cache Invalidation
  - write-through
    - data written to cache and store at the same time
    - data consistency, low risk of data-loss but high latency for writes
  - write-around
  	- data written to store directly
  	- data inconsistency for a while, might increase higher latency for reads
  - write-back
  	- data written to cache alone
  	- low-latency & high throughput but high risk of data loss
- Cache eviction
  - FIFO
  - LIFO
  - LRU
  - MRU
  - LFU
  - Random

## Sharding or Data Partitioning
- Methods
  - Horizontal (range-based, possibly uneven distribution)
  - Vertical (based on features)
  - Directory-based (lookup service)
- Criteria
  - Key or hash-based
  - List partitioning 
  - Round-robin
  - Composite
- Problems
  - Joins & denormalization
  - Referential integrity
  - Rebalancing

## Indexes

## Proxies

## Queues
  - Examples: RabbitMQ, ZeroMQ, ActiveMQ, BeanstalkD
		
		

## NoSQL
- Key-Value Store
  - Examples: Redis, Voldemort, Dynamo
- Document Database
  - Each document can have an entirely different structure
  - Examples: MongoDB, CouchDB
- Wide-Column Datase
  - Columns are containers for rows
  - Rows don’t need to have the same number of columns
  - Columns need not be known ahead of time
  - Examples: Cassandra, HBase
- Graph
  - Data is represented as nodes and edge
  - Examples: Neo4J, InfiniteGraph

`ACID`: Atomicity, Consistency, Isolation, Durability

NoSQL sacrifices ACID for performance and (horiontal) scalability

### CAP Theorem (Pick two)
- Three possibilities
  1. Consistency
  2. Availability
  3. Partition Tolerance
- 1 & 2 -> RDBMC
- 1 & 3 -> BigTable, MongoDB, HBase
- 2 & 3 -> Cassandra & CouchDB

## Consistent Hashing (can be used for distributed caching)
- Hash function maps key to an integer in the range [A, B)
- Put the values in a ring
- Hash servers to an integer value in that range (and put it in the ring)
- Add redundancy / load balancing: Virtual replicas for the caches, which map to multiple points on the ring

Long-Polling, Web-Sockets, Server-Sent events


# Key Characteristics of Distributed Systems
- Scaling
  - Horizontal vs. Vertical
- Reliability (high reliability --> higher availability)
- Availability (high availability !--> higher reliability)
- Efficiency
  - Response time and throughput
- Serviceability / Manageability
	
