# AGENTS.md

## Stack

- **Service:** Auth API Service
- **Type:** business
- **Technologies:**
- Node.js
- Express.js
- jsonwebtoken (JWT)
- bcrypt
- Joi / express-validator
- Sequelize / Knex.js
- pg-pool
- Bull (Redis-backed job queue)
- Nodemailer
- Docker
- Kubernetes / AWS ECS / Azure Container Apps
- Winston / Morgan (structured logging)
- **Responsibilities:**
- Validate user credentials (email format, password rules) on the server side using Joi/express-validator
- Compare submitted passwords against bcrypt-hashed values stored in PostgreSQL
- Issue short-lived JWT access tokens upon successful authentication
- Enforce account lockout logic after configurable failed login attempts
- Generate and store time-limited password reset tokens (15-minute expiry)
- Validate password reset tokens and update hashed passwords on reset
- Enqueue password reset email dispatch jobs to the Redis-backed Bull queue (async, non-blocking)
- Write structured audit log entries (UserID, Timestamp, Status, IPAddress) to the LoginAudit table
- Read and write rate-limiting counters and token metadata to Redis Cache
- Retrieve secrets (JWT secret, DB credentials, email API keys) from Secrets Manager at startup
- Expose health-check and readiness endpoints for load balancer and orchestration platform
- Stream structured application logs and authentication metrics to Cloud Monitoring

## General Rules

- Always read files in /specs before implementing
- Never implement without acceptance criteria
- Code should be simple and readable
- Avoid overengineering
- The project follows a hexagonal architecture

## Required Workflow

1. Read the specs in the /specs directory
2. Generate tasks.md if it does not exist
3. Implement based on the tasks
4. Create automated tests
5. Validate acceptance criteria

## Testing

- Cover all acceptance criteria
- Tests should be clear and straightforward
- Generated code must reach **90% unit test coverage**

## Constraints

- Do not invent requirements that are not described
- Do not change behavior without updating the spec
