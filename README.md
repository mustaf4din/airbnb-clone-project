# airbnb-clone-project

### Overview
A robust, scalable backend that powers core Airbnb‑like features: user management, property listings, bookings, payments, and reviews. The service exposes both REST and GraphQL APIs, is containerized for predictable deployments, and includes a CI/CD pipeline for fast, reliable delivery.

### Team Roles

**Backend Developer** – Implements API endpoints, business logic, validations, and integrations; writes tests and docs.

**Frontend Developer** – (If applicable) Integrates with APIs, implements UI flows for hosts/guests and admin tools.

**Database Administrator (DBA)** – Models schema, performance tuning, indexing, backups/restore, and data governance.

**DevOps Engineer** – CI/CD pipelines, containerization, infrastructure as code, observability, scaling and reliability.

**QA Engineer** – Test strategy and automation (unit/integration/e2e), performance and regression testing.

### Technology Stack

**Django** – Web framework and project foundation (auth, admin, ORM, settings, middlewares).

**Django REST Framework (DRF)** – REST API layer with serializers, viewsets, throttling, and browsable API.

**GraphQL** – Flexible data retrieval with typed schemas and resolvers.

**PostgreSQL** – Primary relational database (ACID, rich SQL, indexing, JSONB where useful).

**Redis** – Caching (e.g., listing search results), rate limiting, background job broker.

**Celery** – Asynchronous tasks (emails, notifications, payment webhooks, reconciliations).

**OpenAPI / Swagger UI & Redoc** – Auto‑generated REST API documentation.

**Docker & Docker Compose** – Reproducible local dev and containerized deployments.

**GitHub Actions** – CI/CD: build, test, lint, scan, package, and deploy.

**pytest** – Unit/integration testing.
