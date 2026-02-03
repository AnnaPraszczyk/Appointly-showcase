# Adopt Modular Monolith Architecture with DDD and CQRS

* Status: Accepted
* Date: 2026-02-03
* Deciders: Anna Praszczyk

## Context and Problem Statement
Appointly is evolving from an educational project to a professional-grade SaaS platform.
The initial architecture placed core domain concepts (`User`, `Reservation`, `Company`) in a shared structure, leading to high coupling. Specifically:
* The `User` class became a "God Object" handling authentication, personal data, and employee context simultaneously.
* Adding new features (like Payments) risked destabilizing the core Reservation logic.
* Querying availability was becoming inefficient due to complex joins in the transactional model.

I need an architecture that supports complex business logic, separates distinct business domains, and prepares the system for potential future scaling (microservices) without the immediate operational overhead of distributed systems.

## Decision Drivers
* **Separation of Concerns:** Distinct business areas (Identity vs. Scheduling) have different lifecycles and change rates.
* **Performance:** Availability checks (reads) happen 100x more often than schedule changes (writes).
* **Maintainability:** Refactoring one part of the system should not break unrelated parts.
* **Simplicity:** Avoiding the complexity of distributed transactions and network latency inherent in microservices at this stage.

## Considered Options
* **Classic Monolith:** Shared database, code (Rejected due to maintainability issues).
* **Microservices:** Physical separation of services (Rejected due to "Microservice Premium" - high DevOps complexity for a single developer).
* **Modular Monolith:** Logical separation within a single deployment unit (Chosen).

## Decision Outcome
Chosen option: **Modular Monolith with DDD and CQRS**.

I will restructure the backend into four distinct, loosely coupled modules based on **Bounded Contexts**:

1.  **Identity Context:** Handles Authentication and Authorization (JWT). The `User` entity here is strictly for security (`AuthUser`).
2.  **Availability Context:** Handles Companies, Employees, and Resources. Owns the "Truth" about schedules.
    * *Pattern:* **Physical CQRS** (Separate read model `AvailableSlots` updated asynchronously).
3.  **Booking Context:** Handles the lifecycle of a Reservation.
    * *Pattern:* **Logical CQRS** (Optimized DTO projections for reading lists).
4.  **Payment Context:** Handles integration with payment gateways.
    * *Pattern:* **Event-Driven Integration** (Publishing `PaymentCompleted` events).

### Architecture Rules
* **Hexagonal Architecture:** Each module has its own internal Hexagonal layers (Domain, Ports, Adapters).
* **Database:** Single physical database, but logically separated tables (schema-per-module approach). Cross-module JOINs are strictly forbidden.
* **Communication:**
    * **Synchronous:** Via public Facades (Java method calls) for simple queries (e.g., Booking asks Availability).
    * **Asynchronous:** Via Domain Events (Spring Events / In-Memory Bus) for side effects (e.g., Payment -> Booking).

## Visualisation (C4 Model)

```mermaid
C4Context
      title Modular Monolith Decomposition

      Container_Boundary(backend, "Appointly Backend") {
        Component(identity, "Identity", "Generic Subdomain", "Auth & Security")
        Component(avail, "Availability", "Core Domain", "Schedules & Resources")
        Component(booking, "Booking", "Core Domain", "Reservations Logic")
        Component(payment, "Payment", "Supporting Subdomain", "Gateway Integration")
      }

      Rel(booking, avail, "Uses Facade", "Sync")
      Rel(payment, booking, "Publishes Event", "Async")
