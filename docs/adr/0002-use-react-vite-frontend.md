# Use React with Vite and TailwindCSS for Frontend

* Status: Accepted
* Date: 2025-11-14
* Deciders: Anna Praszczyk

## Context and Problem Statement
The application requires a dynamic, responsive user interface with complex state management (calendar interactions, form handling). We need a modern, performant stack that allows rapid development and easy styling.

## Decision Drivers
* Need for a responsive and interactive UI (SPA).
* Performance and build speed.
* Requirement for internationalization (i18n) support.

## Considered Options
* Server-Side Rendering (Thymeleaf/JSP with Spring Boot)
* Angular
* React + Vite

## Decision Outcome
Chosen option: **React + Vite + TailwindCSS**.

React provides a flexible component-based structure ideal for the interactive calendar. Vite ensures extremely fast build times compared to Webpack/CRA. TailwindCSS allows for rapid UI prototyping directly in HTML classes.

## Consequences
* **Good:** Fast development cycle with HMR (Hot Module Replacement).
* **Good:** Rich ecosystem (e.g., libraries for Calendars, Axios, i18next).
* **Bad:** Requires separate deployment/build process from the Spring Boot backend (or integration strategy).
* **Bad:** Need to manage state complexity on the client side.
