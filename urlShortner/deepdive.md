□ Identifier generation
□ Uniqueness
□ Length
□ Collision handling

> For simplicity and guaranteed uniqueness, I'd use a database-generated numeric ID encoded using Base62. If identifier predictability is a security or privacy concern, I'd instead use cryptographically secure random IDs and enforce a unique database constraint, retrying on collisions.

□ Database
□ Primary key
□ Index on identifier
□ Unique constraint
□ Storage

□ Cache
□ Cache key/value
□ TTL
□ Cache miss
□ DB fallback

□ Redirect
□ 301 vs 302
□ URL not found - 404 Not Found
□ URL expired - 410 Gone

- the URL shortener doesn't proxy the original website.
- 301 - permanent redirect, browsers, crawlers, CDN can cache the url
- 302 - temporary redirect,
  > I'd use 302 for the default implementation because the redirect service remains in control of the destination and can support expiration, disabling, and destination changes. If the mapping is guaranteed to be permanent, 301 can reduce redirect-service traffic through caching.

□ Reliability

□ DB failure

- read replicas (replication + failover)
  □ Cache failure
  □ Server failure
- Use multiple stateless application servers behind a load balancer.
- stateful and stateless
