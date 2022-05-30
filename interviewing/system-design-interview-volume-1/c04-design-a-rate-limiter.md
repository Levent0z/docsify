# Design a Rate Limiter

> This is a summary of Chapter 4 of [System Design Interview Volume 1](https://www.amazon.com/System-Design-Interview-insiders-Second/dp/B08CMF2CQF/).

## Algorithms for Rate Limiting

1. `Token bucket`
    - Every $n$ seconds, bucket is filled up to $k$ tokens. 
    - A request uses up a token. If no tokens left, request is dropped.
    - **Pros**: easy to implement, memory efficient, allows a burst of traffic for short periods
    - **Cons**: Challenging to tune the two parameters.

<br>

2. `Leaking bucket`
    - Implemented with a FIFO queue of length size $k$.
    - If queue is full, request is dropped.
    - Queue is dequeued at regular intervals. (i.e. Request is processed every $n$ seconds)
    - **Pros**: memory efficient, stable outflow
    - **Cons**: Challenging to tune the two parameters.

<br>

3. `Fixed window counter`
   - Divides the timeline into fixed-size windows (e.g. 1 minute) and assigns a counter to them.
   - Each request increments the corresponding counter
   - If counter > max, request is dropped.
   - **Pros**: memory efficient
   - **Cons**: A burst of traffic at edges can allow more than quota

<br>

4. `Sliding window log`
   - Keep track of request timestamps (e.g. in sorted sets in Redis) 
   - When a new request arrives, remove stale timestamps (those before the time window start). Add time stamp.
   - If log-size > max, request is dropped.
   - **Pros**: very accurate
   - **Cons**: not memory efficient because even rejected requests are kept in the log

<br>

5. `Sliding window counter`
    - Hybrid approach of 3 & 4.