# Use Hexagonal Architecture (Ports & Adapters) for Backend

* Status: Accepted
* Date: 2025-09-05
* Deciders: Anna Praszczyk

## Context and Problem Statement
We are building Appointly, a SaaS reservation system with complex business logic (scheduling, availability checks). 
We need to ensure that the core domain logic remains independent of external frameworks, databases, and UI implementations to facilitate long-term maintenance and testing.

## Decision Drivers
* Need for high testability of business rules without spinning up the database.
* Decoupling domain logic from the persistence layer (PostgreSQL).
* Flexibility to change external adapters (e.g., swapping email providers or API types) without touching the core logic.

## Considered Options
* Layered Architecture (Controller -> Service -> Repository)
* Hexagonal Architecture (Ports & Adapters)
* Modular Monolith

## Decision Outcome
Chosen option: **Hexagonal Architecture**.

We define the Domain model and Use Cases (Input Ports) in the core. Infrastructure implementations (Output Adapters like Repositories) depend on the Domain, inverting the traditional dependency direction.

## Consequences
* **Good:** Domain logic is pure Java, easy to unit test.
* **Good:** Clear separation of concerns.
* **Bad:** More boilerplate code (mapping between DTOs, Domain Entities, and JPA Entities).
* **Bad:** Higher initial learning curve for new developers.
