# Project Overview

This microservice evaluates how productively an HR team is using the platform. It collects indices from multiple internal services and computes a score per product area — if a team runs few surveys, for example, their people management score reflects that.

For each product area, the system outputs a score and a set of actionable recommendations, telling the HR team exactly what they should do to improve it. The goal is to give HR managers a clear picture of where they are underutilizing the platform and what actions would move the needle.

## How it works

Data is collected from other microservices through two integration paths: event-based (SNS/SQS) and direct read replica access. An AWS Lambda processes and normalizes incoming events, forwarding them to the Rails API. Background jobs handle async score recalculation via Sidekiq, ensuring scores are always up to date as new activity comes in.

- [Database](./database.md)
- [Models](./models.md)
- [Services](./services.md)
- [Jobs](./jobs.md)

## Tech Stack

See [stack.md](./stack.md).

## Architecture Decisions

- **Event-based integration (SNS/SQS):** chosen for services that already published domain events, avoiding coupling and extra load on their databases.
- **Read replica access:** used for services with no event system, keeping reads isolated from their primary DB.
- **Lambda as Event Processor:** stateless, scales automatically with SQS volume, no infrastructure to manage.
- **Sidekiq for score recalculation:** async processing with built-in retry, better observability than Lambda for stateful aggregation jobs.