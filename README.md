# Appointly - SaaS Reservation System
<img width="1849" height="782" alt="image" src="https://github.com/user-attachments/assets/9788992f-8014-448d-b1e1-5f7df518d3f2" />


## 🚀 About The Project

**Appointly** is a modern, full-stack SaaS solution designed to streamline appointment booking and business management for service providers (e.g.,consultants, beauty salons, medical clinics).

The system is built with a **backend-first approach**, prioritizing data integrity, security, and scalability. It utilizes **Hexagonal Architecture (Ports & Adapters)** to decouple business logic from external frameworks, ensuring long-term maintainability.

> **⚠️ Note on Source Code:**
> This is a commercial project intended for market release. The source code is currently **private**. This repository serves as a technical showcase, outlining the architecture, technology stack, and features of the system.

---

## 🛠️ Technology Stack

### Backend (Core)
* **Language:** Java 21
* **Framework:** Spring Boot 3
* **Architecture:** Hexagonal Architecture (Ports & Adapters)
* **Database:** PostgreSQL (Production), inMemory (Testing)
* **ORM:** Hibernate / Spring Data JPA
* **Security:** Spring Security 6, JWT (JSON Web Tokens)
* **Testing:** JUnit 5, Mockito, AssertJ (Unit & Integration tests)
* **Tools:** Lombok, Maven, Docker

### Frontend
* **Framework:** React 18
* **Build Tool:** Vite
* **Styling:** TailwindCSS
* **HTTP Client:** Axios (with interceptors)
* **Internationalization:** i18next (PL/EN support)

---

## 🏗️ Architecture Highlights

Appointly follows **Domain-Driven Design (DDD)** principles within a Hexagonal Architecture structure.

* **Domain Layer:** Pure Java code containing business logic and entities (e.g., `Reservation`, `Employee`, `Schedule`). No framework dependencies.
* **Application Layer:** Use Cases and Services (e.g., `CreateReservationUseCase`) orchestrating the flow.
* **Infrastructure Layer:** Adapters for database (JPA Repositories), REST Controllers, and external services (Email, Notifications).

### 📐 Architecture Decision Records (ADR)
Detailed documentation of key architectural choices and trade-offs:

* [ADR-0001: Use Hexagonal Architecture (Ports & Adapters)](docs/adr/0001-use-hexagonal-architecture.md)
* [ADR-0002: React + Vite + TailwindCSS for Frontend](docs/adr/0002-use-react-vite-frontend.md)
* [ADR-0003: Strict Data Integrity & Validation Strategy](docs/adr/0003-data-integrity-and-validation-strategy.md)



### Key Technical Achievements
* **Custom Mappers:** Robust DTO <-> Domain mapping strategies to prevent circular dependencies and StackOverflow errors.
* **Strict Validation:** Logic-heavy validation in the Domain layer ensuring no invalid state ever reaches the database (e.g., "zombie" reservations without services).
* **Concurrency Handling:** Mechanisms to prevent double-booking and schedule collisions.
* **Modular Frontend:** Optimized React components with dynamic translations and theme support (Dark/Light mode).

---

## ✨ Key Features

### For Clients
* 📅 **Smart Booking:** Interactive calendar with real-time availability check (excluding holidays and employee leaves).
* 🌍 **i18n Support:** Fully translated interface (English & Polish).
* 🔔 **Notifications:** Email alerts for booking confirmations and status changes.
* 📱 **Responsive Design:** Seamless experience on mobile and desktop.

### For Service Providers & Employees
* 📊 **Dashboard:** Real-time statistics and daily schedule overview.
* 🛠️ **Service Management:** CRUD operations for offered services, prices, and durations.
* 👥 **Employee Management:** Managing schedules, specializations, and availability.
* ✅ **Reservation Handling:** Workflow for confirming, canceling, or completing visits.

### For Admins
* 🛡️ **User Management:** Role-based access control (RBAC).
* 🏢 **Multi-tenancy Ready:** Structure prepared for managing multiple companies.

---

## 📸 Gallery

### 1. Appointment Booking Flow
<img width="1850" height="821" alt="image" src="https://github.com/user-attachments/assets/63fe91af-66ba-4953-a8a2-f2ccdeaa16af" />



### 2. Interactive Schedule & Dashboard
<img width="1871" height="734" alt="image" src="https://github.com/user-attachments/assets/b9f43ed2-4244-486c-b1d9-7bbe0b0c1be6" />




### 3. Dark Mode & Internationalization
<img width="1833" height="801" alt="image" src="https://github.com/user-attachments/assets/4532e12f-2c5f-4612-a601-6c7fbe09e831" />



---

## 📬 Contact

If you are interested in the technical details or potential collaboration, feel free to reach out:

* **LinkedIn:** https://www.linkedin.com/in/anna-praszczyk-44575b2b2/?locale=en-US
* **Email:** anna.praszczyk@wp.pl
