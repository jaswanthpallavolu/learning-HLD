> Rate limiter system that controls how many requests an user send to an API within a specific period
> A rate limiter controls how many requests a client can make within a defined policy.

- Difficult part isn't counting the requests
- Enforcing the policy across many servers while keeping latency low and handling failures safley

#### FR

- User should be able to send limited no of request to an API within a specific period
- User request will be rejected by the system if the user requests limit got exceed within a specific period
- System should track no of requests made by each user and to the given limit

- Different limits: Global vs Configurable
- Time period: fixed window vs rolling (sliding) window
- Distributed System: Local counters vs Shared state
  - storing the counter in the server memory is fragile, it will be lost when the server restarted or traffic can move when infrastructure changes
  - shared state is not enought, updates must be atomic
  - simultaneous requests try to increment the counter, we use automic check-and-update
  - atomicity solves the race condition within this shared store operation

#### NFR

- low latency (processing time)
- high throughput and scalabilty
- availability and fault tolerance (server failures)
- Accuracy and consistency (handle concurrency)
- Security and abuse resistance
