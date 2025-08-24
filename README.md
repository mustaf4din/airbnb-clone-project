# airbnb-clone-project

## Overview
A robust, scalable backend that powers core Airbnb‑like features: user management, property listings, bookings, payments, and reviews. The service exposes both REST and GraphQL APIs, is containerized for predictable deployments, and includes a CI/CD pipeline for fast, reliable delivery.

## Team Roles

**Backend Developer** – Implements API endpoints, business logic, validations, and integrations; writes tests and docs.

**Frontend Developer** – (If applicable) Integrates with APIs, implements UI flows for hosts/guests and admin tools.

**Database Administrator (DBA)** – Models schema, performance tuning, indexing, backups/restore, and data governance.

**DevOps Engineer** – CI/CD pipelines, containerization, infrastructure as code, observability, scaling and reliability.

**QA Engineer** – Test strategy and automation (unit/integration/e2e), performance and regression testing.

## Technology Stack

**Django** – Web framework and project foundation (auth, admin, ORM, settings, middlewares).

**Django REST Framework (DRF)** – REST API layer with serializers, viewsets, throttling, and browsable API.

**GraphQL** – Flexible data retrieval with typed schemas and resolvers.

**PostgreSQL** – Primary relational database (ACID, rich SQL, indexing, JSONB where useful).

**Redis** – Caching (e.g., listing search results), rate limiting, background job broker.

**Celery** – Asynchronous tasks (emails, notifications, payment webhooks, reconciliations).

**Docker & Docker Compose** – Reproducible local dev and containerized deployments.

**CI/CD Pipelines** – build, test, lint, scan, package, and deploy.

## Database Design

### Core Entities & Key Fields

- **User** (users)

  - id (UUID/PK)
  - email (unique)
  - password_hash
  - full_name
  - role (guest|host|admin)

- **Property** (properties)

  - id (UUID/PK)
  - host_id (FK → users.id)
  - description
  - address
  - price_per_night

- **Booking** (bookings)

  - id (UUID/PK)
  - property_id (FK)
  - guest_id (FK → users.id)
  - check_in
  - check_out
  - total_price

- **Payment** (payments)

  - id (UUID/PK)
  - booking_id (FK)
  - amount
  - paid_at
  - created_at

- **Review** (reviews)

  - id (PK),
  - property_id (FK)
  - author_id (FK → users.id)
  - rating (1–5),
  - comment

### Relationships

- A User (host) can own many Properties.

- A User (guest) can create many Bookings; each Booking belongs to one Property and one guest.

- A Booking has zero or one Payment records (potentially more for multi‑payment scenarios).

- A Property has many Reviews.

- A Review belongs to a Property and is authored by a User (guest who stayed).


