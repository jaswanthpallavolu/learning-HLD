> System that allows application to send notifications to user through multiple channels.

> Functional requirements

- send notification to one or more users
- multiple channels: in-app, push, email etc...
- User preference
- notification history
- read/unread notifications
- Retry failed notifications
- real-time delivery for in-app notification

> Non-Functional requirements

- Scalabilty: handle millions of users, high notification throughput
- Low-Latency: in-app and push notifications should be delivered quickly
- fault tolerance: if one channel fails others should not be affected
- Idempotency: Avoid duplicate notifications during retries
- Availability: Notification processing should remain available during partial failures
- Reliability: Avoid loosing accepted notification requests

> Estimation calculation

- total registered users 10M
- daily active users 2M
- notifications per user in a day 5
- peak traffic 3x
- Average notification payload 1KB
- Average retention 90days
