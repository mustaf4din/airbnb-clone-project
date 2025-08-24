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

## Features Breakdown

1) **API Documentation**  
   The backend is documented with the **OpenAPI** standard so clients can discover endpoints and payloads easily. **Django REST Framework (DRF)** exposes a clear RESTful interface for CRUD on core resources. **GraphQL** adds a flexible query layer when clients need to fetch exactly the fields they want.

2) **User Authentication** (`/users/`, `/users/{user_id}/`)  
   Supports registering new users, authenticating, and managing profiles. This ensures only authorized users can access protected actions and keeps account data organized and retrievable.

3) **Property Management** (`/properties/`, `/properties/{property_id}/`)  
   Lets hosts create, update, retrieve, and delete property listings. These endpoints power the core inventory that guests browse and book.

4) **Booking System** (`/bookings/`, `/bookings/{booking_id}/`)  
   Enables users to make, update, and manage bookings, including check-in and check-out details. It connects guests to properties and tracks the lifecycle of each stay.

5) **Payment Processing** (`/payments/`)  
   Handles payment transactions tied to bookings and records payment details. This allows bookings to be confirmed only after successful payment.

6) **Review System** (`/reviews/`, `/reviews/{review_id}/`)  
   Allows users to post and manage reviews and ratings for properties. Reviews provide feedback and trust signals that help future guests make decisions.

7) **Database Optimizations**  
   **Indexing** speeds up frequent lookups on common filters and identifiers. **Caching** reduces database load and improves response times for read-heavy operations.


