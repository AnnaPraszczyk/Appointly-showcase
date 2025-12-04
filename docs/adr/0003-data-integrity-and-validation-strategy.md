# Strict Data Integrity and Validation Strategy

* Status: Accepted
* Date: 2025-11-28
* Deciders: Anna Praszczyk

## Context and Problem Statement
In a reservation system, data consistency is critical. We encountered issues with "zombie" reservations (reservations created without associated services) and potential double-booking conflicts. We need a strategy to prevent invalid states from ever persisting to the database.

## Decision Drivers
* Prevention of invalid domain states.
* Ensuring that a Reservation aggregate is always complete (Atomic consistency).
* Clear error reporting to the user.

## Considered Options
* Database constraints only.
* Validation in the Controller layer (DTOs).
* Validation in the Domain layer (Constructor/Builder validation).

## Decision Outcome
Chosen option: **Multi-layer Validation with Domain Guardrails**.

1. **DTO Validation:** Basic checks (e.g., `@NotNull`) at the Controller level using Jakarta Validation.
2. **Domain Validation:** Strict checks in Domain Entity constructors/builders (e.g., a Reservation cannot be created with an empty list of services).
3. **Database Constraints:** Foreign keys and constraints as a final safety net.

## Consequences
* **Good:** Impossible to instantiate an invalid `Reservation` object in the business logic.
* **Good:** Early failure (Fail Fast) prevents corrupted data.
* **Bad:** Validation logic is sometimes duplicated between DTOs and Domain objects.
